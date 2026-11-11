## Environment

- OS: macOS 27.0.1, arm64
- Tools: git 2.50.0, curl, gh CLI (Node v25.2.1 is installed but I did not build the site)
- Docs repo: `ChurchCRM/docs.churchcrm.io`, shallow clone of `main` at commit `296ac7821c64475380cc32aad6f2a7f3616bad3c` (2026-11-10)
- Docs pin: `crm-release.json` says `{"version": "7.8.3"}`, the same release the issue's feature (PR #10907) shipped in
- ChurchCRM source: tag `7.8.3`
- I read the docs files and the 7.8.3 source and generated specs. I did not run the ChurchCRM app or build the docs site.

## Steps to reproduce

1. Clone the docs repo and check what it is pinned to.

   ```
   git clone --depth 1 https://github.com/ChurchCRM/docs.churchcrm.io.git
   cd docs.churchcrm.io
   cat crm-release.json
   ```

2. Search the docs for the new pattern.

   ```
   grep -rniE 'monthly-weekday|nth weekday|RecurWOM|RecurDOW|on a weekday|1st.{0,6}5th' docs/
   ```

3. Read what the Ministry Calendar tab page says about the Repeats choices.

   ```
   sed -n '50p' docs/user-guide/ministries/events-and-calendar.md
   ```

4. Check whether the Repeat Events editor is documented.

   ```
   grep -nEi 'repeat|recurrence|pattern|monthly|weekly' docs/user-guide/events.md
   ```

5. Confirm the feature exists in 7.8.3 (the `-s` flag keeps curl quiet).

   ```
   curl -fsSL https://raw.githubusercontent.com/ChurchCRM/CRM/7.8.3/src/event/views/repeat-editor.php | grep -nE 'monthly-weekday|RecurWOM'
   curl -fsSL https://raw.githubusercontent.com/ChurchCRM/CRM/7.8.3/docs/openapi/generated/private-api.yaml | grep -nE 'monthly-weekday|RecurWOM'
   ```

## Reproduction evidence

**Step 1.** The docs are pinned to 7.8.3.

```
{
  "version": "7.8.3"
}
```

**Step 2.** The new pattern appears nowhere in `docs/`. The grep printed nothing and found no matches.

**Step 3.** The Ministry Calendar page lists only three repeat choices and has no "Monthly, on a weekday" option:

```
| **Repeats** | Recurring only: **Weekly** on a **Day of the week**, **Monthly** on a **Day of the month** (if a month does not have that day, for example the 31st in April, the event falls on that month's last day), or **Yearly** on a **Date each year**. |
```

**Step 4.** `docs/user-guide/events.md` never describes the Repeat Events editor's recurrence options. The only matches are these:

```
10:Events can be recurring (such as a weekly church service) or unique (such as a community outreach day).
96:Event types behave like templates which define the parameters for events you will create in the future. Event types allow you to set details such as the recurrence frequency and the default start time an event can have.
115:* **Recurrence Pattern**: None
```

**Step 5.** The feature exists in 7.8.3, in the editor source and in the generated private API spec:

```
repeat-editor.php:172:    value="monthly-weekday">
repeat-editor.php:174:    <select name="RecurWOM" id="RecurWOM" ...
private-api.yaml:1238:  enum: [weekly, monthly, monthly-weekday, yearly]
private-api.yaml:1251:  RecurWOM:
private-api.yaml:1252:    description: 'Week of the month (1-5) for monthly-weekday recurrence: 2 with RecurDOW Tuesday is the 2nd Tuesday'
```

## My findings

I reproduced part of the issue, and one part does not look like a gap.

- **Ministry Calendar tab: reproduced.** The shipped dialog offers a "Monthly, on a weekday" choice (the issue's wording), but the page's Repeats row lists only Weekly, Monthly on a day of the month, and Yearly.
- **Repeat Events editor: reproduced, with a caveat.** The new "Every month on the [1st-5th] [weekday]" row has no docs, but the editor's recurrence options are not documented anywhere in `events.md` either. So this may mean writing new text, not fixing an existing sentence.
- **API (`POST /api/events/repeat`): not reproduced as a gap.** The generated `private-api.yaml` at 7.8.3 already lists `monthly-weekday` and `RecurWOM`. The docs repo only holds `docs/api/` index pages and downloads the specs from the pinned release at build time (`scripts/download-openapi.sh`), so the published API reference should already show these fields. I did not build the site to confirm the rendered page.
- **"Event types cannot store this pattern": no docs mention it.** I found no sentence about it. Line 96 of `events.md` says event types set "the recurrence frequency", which could mislead, but I haven't confirmed that against the app.

I did not run the app, so I haven't checked the screenshots or labels in the live dialog.
