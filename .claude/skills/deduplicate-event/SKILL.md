FILE 1:
.claude/skills/classify-route-event/SKILL.md

---

## description: Classifies Bosnia and Herzegovina monitoring events by significance and determines whether they should be ignored, archived in #bih-events-log, or additionally alerted in #bih-alerts. Use for every candidate event discovered during a monitoring run.

# Purpose

Evaluate each candidate development according to its real-world significance.

Classify the underlying event, not the article.

Use one of these outcomes:

* REJECT
* LOW
* MEDIUM
* HIGH
* CRITICAL

# Step 1: Relevance test

First determine whether the development is relevant to Bosnia and Herzegovina.

REJECT when it is:

* unrelated to Bosnia and Herzegovina
* ordinary entertainment news
* ordinary sports news
* routine local crime with no broader significance
* trivial personal news
* routine ceremonial activity
* ordinary political insults
* repetitive commentary
* an opinion article with no new factual basis
* clickbait
* unsupported rumor
* simple republication of an old event
* another article about an already known event with no material update

# Step 2: Classify significance

## LOW

Use LOW for a genuinely new and credible development that is relevant but currently has limited wider impact.

Examples:

* a relevant local political development
* a minor but concrete party organizational change
* a small institutional step
* a relevant statement containing some new factual information
* a limited economic development
* an early weak signal supported by at least one credible source
* a minor implementation step connected to a larger process
* a relevant meeting with a concrete but limited new outcome

LOW must still contain genuinely new information.

Do not use LOW as a destination for noise.

## MEDIUM

Use MEDIUM when the event may influence an important process but does not yet justify urgent notification.

Examples:

* credible indications of political negotiations
* meaningful change in rhetoric by an important actor
* preparation of potentially important legislation
* an emerging candidate
* significant internal party tension
* a concrete coalition disagreement
* an important meeting with substantive outcome
* a developing industrial problem
* a significant foreign investment negotiation
* a credible early indication of sanctions
* a credible early indication of legal action
* meaningful diplomatic signaling
* coordinated messaging by several important actors
* an emerging protest mobilization
* a developing institutional dispute

## HIGH

Use HIGH for a development with substantial political, institutional, security, economic, legal, electoral, or international consequences.

Examples:

* formal announcement of an important election candidate
* candidate withdrawal with electoral consequences
* major coalition agreement or rupture
* formal introduction of highly consequential legislation
* adoption of important legislation
* important court decision
* major prosecutorial action
* new sanctions
* lifting of major sanctions
* significant OHR action
* major EUFOR development
* important US or EU policy change
* serious institutional blockade
* constitutional escalation
* major industrial shutdown
* strategically important investment agreement
* major defense industry contract
* serious security incident
* large politically significant protest
* major change in relations with Serbia or Croatia
* major implementation step in a secession-related process

## CRITICAL

Use CRITICAL only when the event may have immediate or exceptional consequences.

Examples:

* acute constitutional crisis
* major security emergency
* violent large-scale unrest
* immediate threat to institutional functioning
* extraordinary OHR intervention
* major secession-related institutional action
* deployment or emergency action with major security implications
* collapse of a governing arrangement with immediate state consequences
* event with strong risk of rapid escalation

# Step 3: Confidence

Assign:

* LOW confidence
* MEDIUM confidence
* HIGH confidence

Confidence is separate from significance.

A potentially major event can be:

CRITICAL significance + LOW confidence

Do not confuse importance with verification.

# Step 4: Routing

Use these rules:

REJECT:

* send nowhere

LOW:

* send to #bih-events-log only

MEDIUM:

* send to #bih-events-log only

HIGH:

* send a structured archive record to #bih-events-log
* also send a concise urgent alert to #bih-alerts

CRITICAL:

* send a structured archive record to #bih-events-log
* also send a concise urgent alert to #bih-alerts

# Archive format

For every LOW, MEDIUM, HIGH, or CRITICAL event, post to #bih-events-log in Bulgarian:

📌 EVENT

ID: [stable unique ID]

Засечено: [exact detection date and time]
Събитие от: [actual event date and time when known]

Категория: [category]
Подкатегория: [subcategory]

Актьори:

* [actor]
* [actor]

Значимост: [LOW / MEDIUM / HIGH / CRITICAL]
Потвърждение: [Ниско / Средно / Високо]
Статус: [Потвърдено / Частично потвърдено / Непотвърдено]

Събитие:
[1–3 concise factual sentences]

Какво е новото:
[precisely state what changed]

Източници:

* [source name] — [URL]
* [source name] — [URL]

Тагове:
#[tag] #[tag] #[tag]

# Alert format

For HIGH:

🚨 HIGH: [short concrete title]

Какво се случи:
[1–2 concise factual sentences]

Кога:
[actual event date and time]

Статус:
[verification status]

Източници:

* [source]
* [source]

For CRITICAL:

🛑 CRITICAL: [short concrete title]

Какво се случи:
[1–2 concise factual sentences]

Кога:
[actual event date and time]

Статус:
[verification status]

Източници:

* [source]
* [source]

# Final principle

Classify conservatively but do not require full certainty for relevant early signals.

The archive should capture meaningful weak signals.

The alert channel should remain selective.

==================================================

FILE 2:
.claude/skills/deduplicate-event/SKILL.md

---

## description: Checks candidate Bosnia and Herzegovina monitoring events against previous Slack archive and alert messages to prevent duplicate reporting while allowing material updates. Use before posting any candidate event.

# Purpose

Prevent repeated reporting of the same underlying event.

Before posting any candidate event, search:

* #bih-events-log
* #bih-alerts

# Core rule

Compare underlying events semantically.

Do not compare only:

* titles
* exact wording
* source names
* URLs

Different articles can describe the same event.

# Duplicate test

Treat a candidate as a duplicate when the core real-world event is already recorded and there is no material change.

Examples:

* a second newspaper reports the same decision
* a politician comments on an already recorded decision
* an article republishes yesterday's event
* a new headline describes the same event differently
* a foreign outlet repeats an already recorded local report
* an additional source confirms something already recorded as confirmed

# Material update test

A known event may be recorded again only when at least one meaningful new element exists:

* new official decision
* formal adoption
* implementation
* escalation
* reversal
* withdrawal
* new legal effect
* new major consequence
* new major actor
* authoritative confirmation of a previously uncertain event
* substantial change in scope
* substantial change in timing
* substantial change in political alignment

# Search procedure

For each candidate event:

1. Identify the core event in one sentence.
2. Identify:

   * actors
   * institution
   * action
   * object of action
   * actual event date
3. Search #bih-events-log for semantically similar events.
4. Search #bih-alerts for semantically similar alerts.
5. Compare the candidate with previous records.
6. Decide:

   * NEW EVENT
   * DUPLICATE
   * MATERIAL UPDATE

# Outcome

NEW EVENT:

* continue to classification and routing

DUPLICATE:

* post nothing

MATERIAL UPDATE:

* classify the update independently
* create a new archive record
* explicitly link it to the previous event when possible

# Update wording

For a material update, include in the archive record:

Свързано с:
[previous event ID or concise previous event description]

Какво се промени:
[precise new development]

# Time handling

Always distinguish:

* when the article was published
* when the underlying event happened

A newly published article about an old event is not a new event.

# Final principle

The database unit is the real-world event, not the article.

