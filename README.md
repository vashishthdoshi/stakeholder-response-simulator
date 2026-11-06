# Stakeholder Reaction Simulator

During any corporate crises, the comms team works round the clock to present acceptable statements that face the collective wrath of affected users, journalists, internal employees. With data and security breaches more frequent than ever, I figure the comms team needs help.

This product simulates the reaction of any set of stakeholders in a crisis to specific phrasing, compares statements by sentiments, proof-reads communication against an ‘internal source of truth’ and flags inaccuracies.

After feedback-driven iterations, this version provides a comms writer, legal analyst, CMO/ CCO executive a side-by-side view of competing statement drafts, and their simulated reactions per stakeholder.

This doesn’t replace deep, stakeholder research, but is meant to assist quick iterations in the comms writing teams. You can flex the simulated stakeholders’ characters to represent whoever you want. Are you concerned how your draft will read to a niche influencer? Use this to find out.

The same approach works for any statement/ communication that several audiences will read differently: product announcements, policy positions, internal change memos/ social media updates.

The link below leads to the public, free version of this to test. Use access code `0511`. Please raise an issue to recommend changes, or report flaws.

**Try it:** https://vashishthdoshi.github.io/stakeholder-response-simulator/

## Features

- **Simulated stakeholder panel.** Each stakeholder reacts in their own voice, points to the phrases that trigger them, lists the questions they would ask, and says what would most improve their reaction.
- **Side-by-side comparison.** Paste two drafts. Each stakeholder scores both and also compares them head to head, shown in random order, to say which better addresses their concerns.
- **Fact check.** Each draft is checked against your fact sheet for figures that contradict confirmed facts, open questions stated as settled, and withdrawn claims repeated. Rounded figures are noted, not failed, and confident phrasing is left alone.
- **What to fix first.** Suggestions from every stakeholder are merged into one ranked list.

## How to use it

1. **Scenario and panel.** Add the public context, a fact sheet (`ID | confirmed, unconfirmed or withdrawn | fact`), any phrases your team avoids, one or two drafts, and the stakeholders you want on the panel.
2. **Run.** Enter the access code and run the simulation, or try the preloaded sample scenario without a code. The page shows how many model calls a run will make.
3. **Read and compare.** Scores by stakeholder, the head-to-head verdict, fact-check findings, the ranked fixes and each stakeholder's reaction. Results export as Markdown or JSON.

## How scoring works

Every stakeholder starts at -5, the worst takeaway at the start of the crisis. A statement earns up to 2 points each for clarity, transparency, positivity, communal outlook and apologetic framing, so scores run from -5 to +5. Each stakeholder runs more than once; when the runs disagree, the result is marked as uncertain.

## Data

Live runs send your scenario text to OpenAI through a small proxy. Use fictional or approved, non-confidential material only.

## Feedback

Raise an issue to recommend changes or report flaws: open a [GitHub issue](https://github.com/vashishthdoshi/stakeholder-response-simulator/issues) or email vashishth.doshi@gmail.com.

Built by [Vashishth Doshi](https://www.linkedin.com/in/vashishth-doshi/).
