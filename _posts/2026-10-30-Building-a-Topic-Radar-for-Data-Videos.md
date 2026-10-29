---
layout: single
title: "Building a Topic Radar for Data Videos"
excerpt: "A small pipeline that turns trending topics into a weekly shortlist of data-video ideas: collect, cluster, derive, check, score, verify, and learn from feedback."
tags: [Blog]
date: 2026-10-30
---


# Building a Topic Radar for Data Videos

Oct 30, 2026

## Introduction

Finding a topic for a data video takes two judgments at once: will people care, and can the data actually answer the question? Topic Radar is a small tool that makes both judgments every week. It watches what the English-speaking internet is talking about, turns those trends into concrete questions, checks that the data exists, and ranks the results in a dashboard.

| Stage | Question it answers | Done by |
| --- | --- | --- |
| Collection | What is trending today? | Python, daily |
| Clustering | Which trends are the same story? | Python, weekly |
| Derivation | What would a curious viewer ask about it? | Language model, in an interactive session |
| Title checks | Is the title plain enough? | Python |
| Scoring and verification | Is it worth making, and does the data exist? | Python plus real data samples |
| Preference learning | What does the channel actually like? | Python, from dashboard feedback |

The design rule behind the whole pipeline is simple: deterministic work goes to code, judgment goes to a language model, and nothing the model writes reaches the final brief without passing a code check or a human review.

## 1. Collection

Every morning a scheduled task takes a snapshot of trending items from nine sources and stores them in one SQLite file.

- **Search and news:** Google Trends and Google News, for the US and the UK.
- **Sustained attention:** English Wikipedia page views.
- **Video:** YouTube trending.
- **Tech and social:** Hacker News, Bluesky, Reddit.
- **Prediction markets:** Polymarket and Kalshi, added as two new plugins to an open-source trend aggregator.

Prediction markets turned out to be the most useful source. A market with real money on it is a strong signal that people care about an outcome, and every market comes with a price history, which is ready-made data for an event study.

A few practical rules kept collection reliable:

- **Isolate failures.** Each source and region is called separately. One broken source is logged and the run continues.
- **Filter noise at the source.** Low-volume markets and single sports games are dropped; political markets are kept and tagged.
- **Respect the sources.** Rate limits are honored, and sources that require a contact in the User-Agent get a real one. No login walls or bot detection are bypassed.

## 2. From keywords to clusters

A week of snapshots holds a few thousand keywords. Preprocessing reduces them to about ten to fourteen stories.

- **Clustering:** TF-IDF similarity groups keywords about the same story, such as a Kalshi market, a Polymarket market and a news headline about the same election.
- **Heat:** each cluster's score combines its strongest within-source rank, the number of sources that picked it up, and the number of days it stayed visible.
- **Lifecycle:** emerging, peak, declining or fading, from the slope of its attention.
- **Exclusions:** stories about an individual's death, criminal cases or celebrity gossip are removed by pattern rules and checked again by hand.

Lexical clustering is fast but imperfect. It once merged an actress's name with a stone-carving video because they shared a word. The derivation step therefore reviews each cluster before using it.

## 3. Derivation: two layers per topic

The first version of the tool produced questions like this:

> Event study of the 10 biggest news days of the campaign on the House control market.

The analysis is sound, but no one would click on it. The fix was to split every topic into two layers.

- **Front stage** (what the viewer sees): a title, two alternative titles, and a one-sentence plain answer. Everyday English, no methods.
- **Back stage** (what the analyst sees): the research question, the data sources and the identification strategy.

The four categories are now defined by what a viewer would ask, and the methods move to the back stage.

| Category | What a viewer would ask | Back-stage methods |
| --- | --- | --- |
| Diagnose | Why did this really happen? | Attribution, decomposition |
| Evaluation | Is X really the best, or overrated? | Rankings, bias tests, forecast accuracy |
| Experiment | Does X actually cause Y? | Event study, difference-in-differences, synthetic control |
| Simulation | What if? What are the odds? | Monte Carlo, scenarios |

### Hook patterns

Each question gets three title variants, each built on one of eight hook patterns: counterintuitive, versus, money, myth bust, mega simulation, ranked, absurd what-if, and about you. A title may only promise what the data can deliver.

### Three gate tests

A question is dropped if it fails any of these:

1. **Dinner-table test:** would a non-expert bring this up with friends?
2. **One-sentence test:** can the answer be said in one sentence without jargon?
3. **Surprise-or-stake test:** is the answer surprising, or does it touch the viewer's money, health, team or country?

In the first regenerated week, the gates removed 11 of 62 questions. Eight failed the dinner-table test, including several narrow market event studies that early ratings had flagged as too niche.

## 4. Title checks

Language models are good at writing titles and bad at judging their own. So every title passes three deterministic checks.

- **Jargon list:** words such as *causal*, *regression*, *model*, *effect of* or *distribution* fail the title. Matching is whole-word and includes plurals.
- **Readability:** Flesch reading ease of at least 60, computed with the `textstat` package.
- **Length:** 50 characters for Shorts, 65 for long-form videos.

A failing title goes back for a rewrite, at most twice. After that it is dropped, and a question with no surviving title is dropped too.

The effect is easy to measure. None of the 72 original questions would have passed as titles: all were too long, and six contained jargon. After the change, median reading ease rose from 63.6 to 87.9.

One lesson: Flesch is harsh on short text. A single three-syllable word such as *economy* or *favorite* can sink a seven-word title. About a quarter of the variants needed one rewrite, and a few rewrites came out stilted. The threshold is a setting worth revisiting.

## 5. Scoring and verification

Each surviving question is scored on eight dimensions, all mapped to the 0–1 range.

| Dimension | Source | Shorts weight | Long-form weight |
| --- | --- | --- | --- |
| Hook strength | Judged, 1–5 | 0.27 | 0.25 |
| Accessibility | Judged, 1–5 | 0.23 | 0.20 |
| Heat | Computed | 0.15 | 0.12 |
| Time window | Computed | 0.15 | 0.12 |
| Data availability | Computed from the data grade | 0.10 | 0.13 |
| Saturation | YouTube search count | 0.06 | 0.08 |
| Production cost | Judged, 1–5 | 0.04 | 0.05 |
| Method fit | Judged, 1–5 | 0 | 0.05 |

Method fit, the dimension that rewards analytical depth, became a tie-breaker only. Hook strength and accessibility carry the most weight.

The six best questions go to verification: a short script fetches 10–50 real rows of the data each question needs. This step caught two problems in the first week.

- **A stale title.** A title quoted market odds that had already moved by the time the sample was fetched, so the title was rewritten with current numbers. Titles with live numbers now carry a note to refresh them before production.
- **A missing pre-period.** A synthetic-control question about a health reform relied on a series that starts four years *after* the reform. Without data from before the reform there is no control comparison, so the outcome was switched to a series that starts earlier.

Neither problem was visible from the question alone. Fetching even a small sample is the cheapest way to find out whether an idea is real.

## 6. Learning preferences

Ratings in the dashboard (👍, ⭐, 👎 with a reason) teach the tool what the channel likes.

- **Model:** one Beta posterior per feature value, across nine features: category, domain, direction, data grade, format, signal source, lifecycle, identification strategy and hook pattern. A like counts as one success, a star as two, a dislike as one failure.
- **Title picks:** choosing a preferred title variant counts as one success for its hook pattern only.
- **Decay:** feedback loses half its weight every ten weeks, so taste can drift.
- **Preference score:** the geometric mean, across features, of each posterior mean divided by the prior mean. A question with no feedback scores exactly 1.

### Why the geometric mean

The alternative, summing log means, grows with the number of features. A question with three signal sources would be pushed further from neutral than a question with one, for no good reason. The geometric mean keeps the same multiplicative logic, where one strongly disliked feature still drags the score down, but it stays comparable across questions.

### Exploration and a proxy that failed

About 20% of the weekly story slots are filled by Thompson sampling, so topics the model knows little about keep getting tried. In the first four weeks the share rises to 35%.

A simulation exposed a problem. Before questions are written, a story has only two known features: its sources and its lifecycle. In the simulation, a viewer who liked health questions about one Reddit-sourced story lifted "Reddit" as a whole. Unrelated Reddit posts about vegetables and job offers then climbed to the top of the ranking.

Two fixes followed:

1. **Count each story once.** Features shared by all questions of a story now update once per story, not once per rated question.
2. **Keep weak proxies out of the main ranking.** Preference affects which stories are selected only through the exploration draw. The main slots rank by heat and timing, and full preferences apply later, when each question is scored.

## 7. Division of labour

| Task | Code | Language model | Human |
| --- | --- | --- | --- |
| Collect, cluster, score | ✓ | | |
| Write questions, titles, data cards | | ✓ | |
| Check titles, verify data | ✓ | | |
| Review the event calendar | | drafts | approves |
| Update the taste profile | | proposes a diff | approves |
| Rate questions | | | ✓ |

Everything runs on one machine with one configuration file and one database. The language model works inside an interactive coding session rather than through an API, and every change to the taste profile or the calendar is shown as a diff and committed only after review.

## 8. What the first weeks taught

The biggest gain did not come from better data or smarter scoring. It came from separating what the viewer sees from what the analyst does. Once titles had to pass a jargon list, a readability score and three plain-language gates, the same trends produced questions that sound like conversations instead of paper abstracts. The analysis behind them stayed exactly as rigorous. The next step is to close the loop with audience data: import view and retention numbers for published videos, and weigh them against the ratings.

## References

**Methods**

- Flesch reading ease: [Flesch–Kincaid readability tests](https://en.wikipedia.org/wiki/Flesch%E2%80%93Kincaid_readability_tests)
- Thompson sampling: [overview](https://en.wikipedia.org/wiki/Thompson_sampling)
- Beta distribution as a conjugate prior: [overview](https://en.wikipedia.org/wiki/Beta_distribution)

**Tools and data**

- [textstat](https://pypi.org/project/textstat/) (readability scores)
- [Streamlit](https://streamlit.io/) (dashboard)
- [Polymarket documentation](https://docs.polymarket.com/)
- [Kalshi API documentation](https://docs.kalshi.com/)
- [World Bank Indicators API](https://datahelpdesk.worldbank.org/knowledgebase/articles/889392-about-the-indicators-api-documentation)
- [OpenFEC API](https://api.open.fec.gov/developers/)
