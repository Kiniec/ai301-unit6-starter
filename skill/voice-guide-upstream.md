# Voice guide, the upstream section: how I talk to maintainers

<!--
THIS IS THE PART YOU WRITE (the unit-6 hole). Append everything below
this comment to YOUR voice guide, then fill it. Your guide has held
your outgoing words to your own rules since unit 2; this section aims
those rules at the wild, where the readers are maintainer strangers
who owe you nothing and your house rules do not travel.

Same format as unit 2, on purpose: each rule needs a wrong/right pair
from your own hand. One line you might actually have written that
breaks the rule, and the line you would post instead. The pair is
what makes a rule executable; a rule without one is a wish. "Be
polite" is advice for everyone and therefore a rule for no one.

Three subsections. Fill all three: your claims, your questions, your
pings each leave your keyboard under your name. Once your rules are
written, delete these instruction comments: the guide of record
carries rules, not scaffolding.
-->

## Upstream: how I talk to maintainers

### Claims I post

<!-- 1-2 rules. What your claim promises and how it sounds: intent,
a concrete first step, a realistic timeframe, in your register. Think
about what you refuse to do too: claiming over a stranger, squatting
silently, promising dates you cannot keep.

#### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

#### Rule: check before I claim

I claim only after reading the thread and the Development box: no assignee, no open linked PR, and no claim comment in the last 30 days that a maintainer answered. The claim says what I checked.

- Wrong: "I'd like to work on this!"
- Right: "I'd like to take this. I checked and there's no assignee or open PR linked. I'll start by reproducing it on v3.2.4."

#### Rule: a first step and a window, not a deadline

A claim names one concrete first step and a rough window I can keep, and says I'll post here if I drop it. No dated promises, and no promise of a PR before the maintainer has seen my approach.

- Wrong: "I'll have a PR up by Friday."
- Right: "I'm planning to look at `targets.py` this week. If I can't get to it, I'll say so here so someone else can take it."

### Questions I ask

<!-- 1-2 rules. What a question of yours must carry before it goes
up: answerable from the maintainer's chair, what you already tried,
one question rather than five. -->

#### Rule: one question, with what I tried

Each question is a single question a maintainer can answer from the chair they're in. It states what I already read or ran, and my best guess at the answer.

- Wrong: "How does this work? Where should the fix go? Do you want tests? Which branch?"
- Right: "I ran `npm test` and it passes on `main`. I think the fix belongs in `ResolveByTaskType`, not `GetServiceTasks`. Is that the right place?"

#### Rule: ask before building on a guess

If the issue leaves the approach open, I ask which direction the maintainers prefer before writing code, and I name both options.

- Wrong: "I went ahead and made it fail at startup. PR coming."
- Right: "The issue allows either a consistent outcome or a startup error. I lean toward the startup error. Is that acceptable before I start?"


### Pings I send

<!-- 1 rule is enough. When you nudge and how it sounds: measured
against the repo's own reply rhythm, never your clock, and never
pressure dressed as politeness. -->

#### Rule: ping on the repo's rhythm

I nudge only after the repo's usual reply time has passed (I check recent threads for it), at most once, and I add something new instead of "any update?".

- Wrong: "Hi, any update on this? It's been 3 days."
- Right: "Following up: I've pushed a repro commit at <link>. Maintainers here usually reply within about a week, so no rush. I wanted the evidence in the thread."

<!--
NO UNIT 2 GUIDE? The frame carries you. Write ALL the sections fresh
in your canonical guide, today: first the three unit 2 sections
listed below, then the Upstream section above. Write every rule as
plain text, outside these comment blocks. It is more writing, and it is
entirely doable; ask a TF if you want a second pair of eyes on your
first rules.

The unit-2 frame, so you do not need the old materials open:

  ## Who I am in threads
    2-3 lines. Who is talking when you comment: your experience level
    stated plainly, what you are doing in this repo, what readers can
    expect from you.

  ## Rules I write by
    3-5 rules, wrong/right pair each, same format as above.

  ## Things I never post
    A short list. Promises you cannot keep, tones you refuse,
    shortcuts you know you reach for when tired.
-->
