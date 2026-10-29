---
layout: single
title: "Mapping the Literature on Engaging Data Presentation"
excerpt: "Making data analysis engaging draws on five bodies of work: empirical visualization research, design principles, narrative practice, video explainers, and interactive web journalism."
tags: [Blog]
date: 2026-10-29
---


# Mapping the Literature on Engaging Data Presentation

Oct 29, 2026 · @Xin

## Introduction

Making data analysis engaging draws on five bodies of work: empirical visualization research, design principles, narrative practice, video explainers, and interactive web journalism. Each answers a different question, and none is sufficient alone.

| Strand | Question it answers | Core resources |
| --- | --- | --- |
| Academic research | What does evidence say about engagement and memory? | Segel & Heer (2010), Borkin et al. (2013), Bateman et al. (2010) |
| Foundational principles | What makes a chart honest and clear? | Tufte, Cairo |
| Narrative practice | How do I turn an analysis into a story? | Knaflic |
| Video exemplars | How does data work in a linear, timed medium? | Rosling, 3Blue1Brown, Kurzgesagt, Vox |
| Web and interactive exemplars | How can readers explore data themselves? | The Pudding, The Upshot, Nicky Case, Bret Victor |

The central tension running through all five strands is clarity versus engagement. Minimalists argue that every non-data mark is a cost. Researchers and practitioners in the other camp show that decoration, narrative and personality can improve memory without hurting comprehension. Reading both sides is the fastest way to build your own judgement.

## 1. Academic entry points

Three papers frame the field: one maps the design space of data stories, and two test empirically whether "chart junk" helps or hurts. Together they form a small literature you can read in a weekend.

### Segel & Heer (2010): Narrative Visualization: Telling Stories with Data

- **Publication:** IEEE Transactions on Visualization and Computer Graphics (Proc. InfoVis), vol. 16, no. 6, 2010. Written at Stanford; [paper page](https://idl.uw.edu/papers/narrative).
- **Status:** Widely treated as the seminal paper on data storytelling. It received the IEEE InfoVis 10-Year Test of Time Award in 2020 ([UW news](https://news.cs.washington.edu/2020/10/30/professor-jeffrey-heer-and-alumnus-dominik-moritz-honored-at-ieee-vis-for-outstanding-contributions-in-data-visualization/)).
- **Method:** The authors catalogued 58 examples of narrative visualization, mostly from online journalism, and coded their design features ([Microsoft Research technical report, 2016](https://microsoft.com/en-us/research/wp-content/uploads/2016/04/MSR-TR-2016-14-Storytelling-Techniques.pdf)).
- **Key output 1, seven genres:** magazine style, annotated chart, partitioned poster, flow chart, comic strip, slide show, and film/video/animation ([paper PDF](https://homes.cs.washington.edu/~jheer/files/narrative.pdf)).
- **Key output 2, the author–reader spectrum:** Author-driven stories impose a fixed sequence and message. Reader-driven stories let the audience explore. Hybrid structures sit between, such as the "martini glass": a guided opening that widens into free exploration.
- **Why it matters for you:** Video is the most author-driven genre. The paper explains what you gain (control of pacing and punchline) and what you give up (the viewer cannot dig into the chart).

### Borkin et al. (2013): What Makes a Visualization Memorable?

- **Publication:** IEEE TVCG (Proc. InfoVis 2013), vol. 19, no. 12, pp. 2306–2315. Harvard SEAS and MIT; [project page](https://vcg.seas.harvard.edu/publications/20130101-what-makes-a-visualization-memorable).
- **Method:** The team gathered 5,693 visualizations from news media, government reports, scientific journals and infographics. They ran an online memory experiment on Amazon Mechanical Turk using 2,070 single-panel images ([Harvard SEAS news](https://seas.harvard.edu/news/2013/10/what-makes-data-visualization-memorable)).
- **Findings:** People agree strongly on which charts are memorable. Color and a human-recognizable object (a photo, person, cartoon or logo) raise memorability. Familiar chart types such as bar and line charts are less memorable than unusual ones.
- **Author's caveat:** Borkin herself stresses that a memorable chart is not automatically a good one.
- **Follow-up:** Borkin et al. (2016), *Beyond Memorability: Visualization Recognition and Recall*, used eye-tracking. It found titles and text are the elements people look at and recall most, and that redundancy aids understanding ([World Bank Data Blog summary](https://blogs.worldbank.org/opendata/what-makes-data-visualization-memorable)).
- **Critique:** Stephen Few argued the study measured only one-second glance recognition, not memory of the content ([Perceptual Edge](https://www.perceptualedge.com/blog/?paged=27)). Read the critique alongside the paper; as an econometrician you will want to judge the outcome variable yourself.

### Bateman et al. (2010): Useful Junk?

- **Full title:** *Useful Junk? The Effects of Visual Embellishment on Comprehension and Memorability of Charts.* CHI 2010, pp. 2573–2582. University of Saskatchewan; [paper PDF](https://vis.csail.mit.edu/classes/6.859/readings/pdfs/Bateman-UsefulJunk.pdf).
- **Method:** Participants saw plain charts and heavily illustrated charts by the designer Nigel Holmes, then were tested on comprehension and recall.
- **Findings:** Comprehension was about equal. Recall of embellished charts was no better immediately, but clearly better after two to three weeks ([summary](https://medium.com/@jopuga/useful-junk-the-effects-of-visual-embellishment-on-comprehension-and-memorability-of-charts-cf9b7539dae0)).
- **The authors' own limit:** They do not recommend embellishment everywhere. Background images, for example, made interpretation harder.
- **Critique:** Stephen Few's 2011 response concedes that well-chosen imagery tied to the message can work as a mnemonic, but argues its scope is narrow ([Few 2011 PDF](https://webspace.science.uu.nl/~telea001/uploads/VACourse/Few11.pdf)). Robert Kosara's blog posts at eagereyes.org argue the opposite side ([eagereyes 2011](https://eagereyes.org/blog/2011/want-to-make-chart-memorable-add-junk)).
- **Practical rule from the debate:** Decoration helps when it is related to the message; unrelated decoration can hurt recall ([IJSW study](https://journals.shareok.org/ijsw/article/view/54)).

### The chartjunk debate in one paragraph

Tufte coined "chartjunk" in 1983 for non-data ink that adds nothing. Bateman (2010) and Borkin (2013) showed that some of that ink improves long-term memory. Few and others replied that memory of the picture is not memory of the data. The current consensus is conditional: in analytical work, stay minimal; in communication to a general audience, purposeful decoration tied to the message is defensible. For a YouTube channel you are almost always in the second case.

### Search keywords for Google Scholar

| Keyword | What you will find |
| --- | --- |
| narrative visualization | Follow-ups to Segel & Heer, genre taxonomies |
| data storytelling | Broader, interdisciplinary work; start with the 2023 systematic review by Schröder et al. ([arXiv](https://arxiv.org/pdf/2312.01164)) |
| data videos | Amini et al.'s analysis of 50 professionally made data videos and later work |
| visualization memorability | Borkin's line of research and replications |
| chartjunk OR visual embellishment | The minimalism debate, Few's critiques |
| storytelling techniques visualization | Hullman, Lee and colleagues on specific narrative mechanisms |

A good tactic: open Segel & Heer on Google Scholar, click "Cited by", and sort by relevance. The most-cited descendants form the field's backbone.

## 2. Foundational principles

Tufte teaches restraint and integrity; Cairo keeps integrity but adds beauty and audience. Read Tufte first so you know the rules, then Cairo so you know when to bend them.

### Edward Tufte, The Visual Display of Quantitative Information

- **Publication:** Graphics Press. First edition 1983, second edition 2001, about 200 pages ([publisher page](https://www.edwardtufte.com/book/the-visual-display-of-quantitative-information/)). The second edition adds color reproductions of William Playfair's graphics.
- **Reputation:** Statisticians Frederick Mosteller and John Tukey both praised it on publication. It remains the standard reference on statistical graphics.
- **Structure:** Part I covers graphical practice, excellence and integrity. Part II is a theory of data graphics, with chapters on data-ink, chartjunk ("vibrations, grids, and ducks"), multifunctioning elements, data density and small multiples ([chapter list](https://apps-cce.grad-college.iastate.edu/resources-database/view/?id=456)).
- **Core concepts to know:**
  - *Data-ink ratio:* the share of ink that encodes data. Maximize it, erase non-data and redundant ink, then revise.
  - *Chartjunk:* decoration that adds no information, such as 3D effects, heavy grids, or the "duck" (a chart turned into a picture of itself).
  - *Lie factor:* the size of an effect in the graphic divided by its size in the data. A value far from 1 signals distortion.
  - *Small multiples:* the same small chart repeated across categories or time, so the eye compares like with like.
  - *Sparklines:* word-sized charts set inline with text (developed in his later book *Beautiful Evidence*, 2006).
- **Companion volumes:** *Envisioning Information* (1990) and *Visual Explanations* (1997). The latter is most relevant to video, since it deals with explaining causes and processes over time.
- **How to read it critically:** Tufte writes for analytical readers studying a page at leisure. A YouTube viewer sees a chart for a few seconds while listening to you. Section 1 shows why pure minimalism is not always optimal for that audience.

### Alberto Cairo, How Charts Lie

- **Publication:** W. W. Norton, October 2019, about 256 pages ([WorldCat](https://search.worldcat.org/title/1121263715)). Cairo holds the Knight Chair in Visual Journalism at the University of Miami ([faculty page](https://com.miami.edu/profile/alberto-cairo/)).
- **Audience:** General readers. It teaches *graphicacy*, his term for chart literacy, through news and political examples.
- **Structure:** Five ways charts mislead: poor design, dubious data, insufficient data, concealed or confusing uncertainty, and misleading patterns ([British Library record](https://eld.bl.uk/catalog/019567342)).
- **Why an economist will like it:** Many examples are about correlation versus causation, base rates, aggregation and missing denominators. These are the same traps you teach in econometrics, made visual.
- **Use for your channel:** Each "lie" is a ready-made episode format. Show a misleading chart, ask the viewer what is wrong, then reveal it.

### Alberto Cairo, The Functional Art and The Truthful Art

- **The Functional Art** (New Riders, 2012): an introduction to infographics and visualization, written for his journalism courses. It argues that visualization is "functional art": form follows the function of the message ([Pearson](https://pearson.com/us/higher-education/program/Cairo-Truthful-Art-The-Data-Charts-and-Maps-for-Communication/PGM178828.html)).
- **The Truthful Art** (New Riders, 2016, about 400 pages): the follow-up. Part I is a statistics primer for journalists and designers. It defines five qualities of great visualizations: truthful, functional, beautiful, insightful and enlightening ([O'Reilly table of contents](https://oreilly.com/library/view/the-truthful-art/9780133440492)).
- **Which to read:** With your statistics background, skip most of the Truthful Art's primer. Read its chapters on the five qualities and on chart choice. *How Charts Lie* is the shortest and most enjoyable entry point of the three.

### Tufte versus Cairo at a glance

| Question | Tufte | Cairo |
| --- | --- | --- |
| Main goal | Precise, efficient display for analysis | Truthful communication to a broad audience |
| Attitude to decoration | Remove it | Acceptable if it serves the message |
| Role of beauty | Follows from clarity | A quality in its own right |
| Best use for you | Self-editing checklist | Episode ideas and audience framing |

## 3. Narrative practice

*Storytelling with Data* is the most practical bridge from "I have a finished analysis" to "I have a story". It is short, workflow-driven and can be applied the same week you read it.

### Cole Nussbaumer Knaflic, Storytelling with Data

- **Publication:** *Storytelling with Data: A Data Visualization Guide for Business Professionals*, Wiley, November 2015, about 288 pages ([Bookshop](https://bookshop.org/p/books/storytelling-with-data-a-data-visualization-guide-for-business-professionals-cole-nussbaumer-knaflic/05d99a7a2d5b9c51)).
- **Author:** Knaflic worked on Google's People Analytics team, where she taught her data visualization course more than 50 times before founding her own company, storytelling with data (SWD) ([book foreword](https://vdoc.pub/documents/storytelling-with-data-a-data-visualization-guide-for-business-professionals-2g3jl7umcbj0)).
- **Reach:** The book has been translated into about a dozen languages and is used as a textbook at more than 100 universities ([author bio, 2020](https://download.e-bookshelf.de/download/0013/2320/76/L-G-0013232076-0036925731.pdf)).

### The six lessons

1. **Understand the context.** Who is the audience, what should they know or do, and what tone fits? Write a one-sentence "Big Idea" and a "3-minute story" before opening any chart tool.
2. **Choose an appropriate visual.** A short set of chart types covers most needs: simple text, tables, heatmaps, line, slope and bar charts. Avoid pies and 3D.
3. **Eliminate clutter.** Remove borders, gridlines, redundant labels and legends. This applies Gestalt principles such as proximity, similarity and enclosure.
4. **Focus attention.** Use preattentive attributes (color, size, position, bold) to steer the eye. Grey everything, then highlight one thing.
5. **Think like a designer.** Affordances, accessibility and aesthetics; the action title that states the conclusion.
6. **Tell a story.** Use a three-act structure: setup, conflict, resolution. Keep the narrative flow and repeat the main point.

The book's central demonstration is a before-and-after makeover: one cluttered chart rebuilt step by step into a clear one ([R-bloggers review](https://www.r-bloggers.com/2016/03/book-review-storytelling-with-data/)).

### Companion resources

- ***storytelling with data: let's practice!*** (Wiley, 2019): an exercise book with guided and open-ended tasks for each lesson. Useful if you learn by doing.
- **SWD website and community:** a blog, podcast and monthly visualization challenges where people submit makeovers of the same dataset. Studying others' submissions is a ready-made teardown library.

### What it does not cover

Knaflic writes for business presentations: slides, reports and a seated audience. She says little about humor, personality, animation or pacing. Use her for structure and decluttering, and the video exemplars in Section 4 for performance and timing.

### Applying it to a video episode

| Knaflic concept | Video translation |
| --- | --- |
| Big Idea | The one sentence the viewer should repeat to a friend |
| 3-minute story | Your episode outline before scripting |
| Grey then highlight | Build the chart on screen, then light up one bar or line as you speak |
| Action title | An on-screen caption stating the takeaway, not the variable names |
| Three-act structure | Hook question, surprising data, what it means for the viewer |

## 4. Video exemplars

These four creators show four different answers to the same problem: how to hold attention on data in a medium the viewer cannot pause to study. Rosling uses performance, 3Blue1Brown uses progressive revelation, Kurzgesagt uses illustrated metaphor, and Vox uses journalistic visual essays.

| Exemplar | Main engagement device | Production scale | Closest fit for a solo creator |
| --- | --- | --- | --- |
| Hans Rosling | Live performance, props, sports-commentator energy | One presenter plus software | Very high |
| 3Blue1Brown | Step-by-step animated build-up | One creator plus code (Manim) | High, if you code |
| Kurzgesagt | Illustrated characters, scale metaphors | Studio of about 70 people | Low for production; high for ideas |
| Vox | Narration over archive footage and motion graphics | Newsroom video team | Medium |

### Hans Rosling: TED, Gapminder and Factfulness

- **Who:** Swedish physician and statistician (1948–2017), professor of international health at Karolinska Institute ([Britannica](https://www.britannica.com/biography/Hans-Rosling)).
- **The TED talk:** *The best stats you've ever seen*, recorded at TED2006 in Monterey. TED's page shows over 16 million plays ([TED](https://www.ted.com/talks/hans_rosling_the_best_stats_you_ve_ever_seen)). He gave 10 TED talks in total.
- **Gapminder:** Founded in Stockholm in 2005 by Hans Rosling, his son Ola Rosling and Anna Rosling Rönnlund. Its bubble-chart software Trendalyzer was bought by Google in 2007 ([Gapminder history](https://www.gapminder.org/about/about-gapminder/history/)). Gapminder's free tools and datasets are still online.
- **Documentaries:** *The Joy of Stats* (BBC, 2010) and *Don't Panic: The Truth about Population* (2013).
- **Book:** *Factfulness: Ten Reasons We're Wrong About the World—and Why Things Are Better Than You Think* (2018), with Ola Rosling and Anna Rosling Rönnlund. It opens with a quiz most audiences fail, then explains ten instincts behind the errors.
- **What to study:** Watch the 2006 talk with the sound off, then with sound only. You will see that the chart is simple (an animated scatter) and the engagement comes from his commentary: he narrates bubbles like racehorses. Also watch *200 Countries, 200 Years, 4 Minutes* from *The Joy of Stats*, a short piece built around one animated chart.
- **Lesson for you:** Rosling's persona was the enthusiastic professor. Yours is the self-ironic economist. Both work because the personality carries the data, not the reverse.

### 3Blue1Brown and Manim

- **Who:** Grant Sanderson, a Stanford mathematics graduate, runs the channel; it launched in 2015 and teaches mathematics through animation.
- **Style:** Each idea is built on screen one element at a time, so the viewer never faces a finished, complex image. Recurring "pi creature" characters ask the viewer's questions aloud.
- **Manim:** Sanderson wrote his own Python animation engine, Manim ("Mathematical Animation"). His version is now called ManimGL. A separate Community Edition (ManimCE) is maintained by volunteers and is the recommended starting point; Sanderson's own FAQ says so ([3Blue1Brown FAQ](https://www.3blue1brown.com/faq/), [ManimCE docs](https://docs.manim.community/en/stable/index.html)).
- **Licensing:** Manim is MIT-licensed, but the pi creatures are copyrighted and should not be reused.
- **Good entry point:** Sanderson's 2024 video *How I animate 3Blue1Brown*, a Manim demo with Ben Sparks.
- **Lesson for you:** Progressive revelation suits econometric ideas well, for example drawing a confounder into a causal graph one arrow at a time. Manim installs with `pip install manim`.

### Kurzgesagt – In a Nutshell

- **Who:** A Munich animation and design studio founded by Philipp Dettmer in July 2013, after he graduated from Munich University of Applied Sciences. The English channel had over 25 million subscribers as of mid-2026 ([Wikipedia](https://en.wikipedia.org/wiki/Kurzgesagt)). The studio also runs a German-language channel.
- **Scale:** A studio of about 70 people; early on, a single 5–6 minute video took about 200 working hours ([Bird in Flight](https://birdinflight.com/en?p=119056)).
- **Style:** Flat, colorful illustrations and recurring bird characters. Huge or tiny numbers are made tangible through scale comparisons, such as zooming from a cell to a planet. Its tagline is "optimistic nihilism".
- **Lesson for you:** You cannot match the production, but you can copy the technique of turning one number into a picture the viewer can feel. The studio is also in your city, which may be useful for future episodes or networking.

### Vox explainers

- **Who:** Vox.com was founded in April 2014 by Ezra Klein, Matt Yglesias and Melissa Bell around "explanatory journalism". Its YouTube channel has published explainers since 2014 and has over 12 million subscribers ([Wikipedia](<https://en.wikipedia.org/wiki/Vox_(website)>)).
- **Style:** Narration over archive footage, animated maps and charts, and graphics overlaid on real footage. The team learned that visuals must show evidence, not decorate ([Fast Company](https://www.fastcompany.com/40575395/voxs-netflix-ambitions-are-just-the-beginning)).
- **Netflix:** *Explained*, produced by Vox Media, premiered on Netflix in May 2018 and ran for three seasons.
- **Lesson for you:** The "X, explained" format and the visual-essay structure translate directly to economics topics. Former Vox producer Johnny Harris, now an independent creator, shows how the style works for one person on camera.

### How to watch these as research

Pick one video from each creator on a topic you know well. For each, note the timestamp of the first question, the first number, the first surprise and the first joke. Comparing those four timestamps across creators is a quick, quantitative way to see how each structures attention.

## 5. Web and interactive exemplars

Interactive pieces engage by letting the reader act: guess a curve, move a slider, run a simulation. Even if your main medium is video, these pieces are the best source of ideas for formats that make the audience participate.

### The Pudding

- **What it is:** A digital publication of "visual essays" that explain ideas debated in culture, launched in 2017 as the editorial arm of the data-design studio Polygraph, founded by Matt Daniels ([Pudding About page](https://pudding.cool/about), [Nieman Lab](https://www.niemanlab.org/2017/05/this-site-publishes-high-touch-time-intensive-data-visualizations-and-has-a-business-that-sustains-it/)).
- **Business model:** No ads or paywall. Polygraph does paid client work (for example Google Trends and LinkedIn) that funds the editorial side ([Polygraph](https://polygraph.cool/)).
- **Team:** A small group of journalist-engineers, each able to research, analyze, design, write and code ([ONA awards entry](https://awards.journalists.org/entries/the-puddings-portfolio/)).
- **Recognition:** A Peabody Award in 2017 and an Online Journalism Award in 2023 ([Wikipedia](https://en.wikipedia.org/wiki/The_Pudding)).
- **Style:** Few words, original datasets, scroll-driven graphics, and topics from pop culture rather than the news cycle. Its founders argue there is no fixed story shape for a visual essay; the shape comes from the data ([Storybench](https://www.storybench.org/?p=8613)).
- **Lesson for you:** Topic choice is half the fun. The Pudding picks questions people already argue about over dinner, then settles them with data. Many of its pieces publish their data and code on GitHub, so you can study how they were built.

### The New York Times: The Upshot

- **What it is:** The Times's data and explanatory-journalism section, launched on 22 April 2014 under editor David Leonhardt ([Wikipedia](https://en.wikipedia.org/wiki/The_Upshot)).
- **Key figure:** Amanda Cox, a statistician by training, was a graphics editor there and later editor of The Upshot from 2016 to January 2022 ([Wikipedia](https://en.wikipedia.org/wiki/Amanda_Cox)).
- **Signature piece:** *You Draw It: How Family Income Predicts Children's College Chances* (2015). Readers draw the curve they expect before the real data is revealed. The gap between guess and truth is the hook.
- **Lesson for you:** "Guess first, then reveal" transfers directly to video. Pause and ask viewers to predict a number in the comments, then show it. It also produces engagement signals that YouTube rewards.

### Nicky Case and explorable explanations

- **Who:** An independent game and interactive designer who turns models from social science into playable pieces ([Wikipedia](https://en.wikipedia.org/wiki/Nicky_Case)).
- ***Parable of the Polygons*** (2014, with Vi Hart): a playable version of Thomas Schelling's segregation model. Shapes with only a mild preference for similar neighbors end up fully segregated ([ncase.me/polygons](https://ncase.me/polygons/)).
- ***The Evolution of Trust*** (2017): an interactive guide to the iterated prisoner's dilemma, framed by the 1914 Christmas truce. Readers pit strategies against each other and watch which ones survive.
- **Explorable Explanations hub:** Case set up a site collecting interactive lessons by many authors, which spread the term widely ([Case's blog](https://blog.ncase.me/explorable-explanations-the-plan)).
- **Interview:** *Data Stories* podcast episode 103 covers Case's approach and advice for beginners ([Data Stories](https://datastori.es/103-explorable-explanations-with-nicky-case/)).
- **Lesson for you:** Both pieces are economics and network-science models made fun. They are the clearest proof that your own research toolkit (game theory, emergent network effects) can be entertaining.

### Bret Victor: the origin of explorable explanations

- **The essay:** *Explorable Explanations*, published 10 March 2011 on his site worrydream.com, with a postscript added in February 2024 ([essay](https://worrydream.com/ExplorableExplanations/)).
- **Argument:** Readers should be active, not passive. Text should be an environment to think in, not just information to consume.
- **Three ideas in the essay:**
  - *Reactive documents:* the reader changes the author's assumptions and sees the consequences instantly.
  - *Explorable examples:* concrete, manipulable cases that build intuition about how a system behaves.
  - *Contextual information:* related material available on the spot, so the reader can check claims.
- **Why it matters for an econometrician:** A reactive document forces the author to disclose the model behind the argument. That is essentially a call for transparent, reproducible assumptions, presented as a reading experience.
- **Further reading:** His talk *Inventing on Principle* (2012) and his essay on model-driven communication, *What Can a Technologist Do About Climate Change?* (2015).

### What transfers from interactive to video

| Interactive device | Video equivalent |
| --- | --- |
| You Draw It (predict, then reveal) | Pause and ask for a guess in comments; reveal after a beat |
| Slider that changes an assumption | Show two or three scenarios side by side and narrate the difference |
| Playable simulation | Run the simulation on screen and react to it like a sports match |
| Scroll-driven reveal | Progressive build-up of the chart, one element per sentence |

## 6. Suggested reading order

A four-week sequence moves from framework to evidence to practice, alternating reading with watching so the ideas are tested against real examples straight away.

1. **Week 1, the framework.** Read Segel & Heer (2010). Then read the first half of *Storytelling with Data* (lessons 1–3). Watch Rosling's 2006 TED talk twice: once for content, once for technique.
2. **Week 2, the evidence.** Read Bateman et al. (2010), Borkin et al. (2013) and Few's 2011 critique together. Write one paragraph on where you stand in the chartjunk debate for a YouTube audience.
3. **Week 3, principles and practice.** Skim Tufte's chapters on data-ink and chartjunk; read Cairo's *How Charts Lie*. Finish *Storytelling with Data* (lessons 4–6). Watch one 3Blue1Brown, one Kurzgesagt and one Vox video, logging the four timestamps from Section 4.
4. **Week 4, interaction and synthesis.** Read Bret Victor's essay; play *Parable of the Polygons* and *The Evolution of Trust*; browse five Pudding essays and The Upshot's *You Draw It*. Then list the five devices you most want to try in your own episodes.

After week 4, run Google Scholar's "Cited by" on Segel & Heer and Borkin et al. to go deeper wherever your own experiments raise questions.

## References

**Papers**

- Segel, E., & Heer, J. (2010). Narrative Visualization: Telling Stories with Data. *IEEE TVCG*, 16(6). [Paper page](https://idl.uw.edu/papers/narrative) · [PDF](https://homes.cs.washington.edu/~jheer/files/narrative.pdf)
- Borkin, M. A., et al. (2013). What Makes a Visualization Memorable? *IEEE TVCG*, 19(12), 2306–2315. [Project page](https://vcg.seas.harvard.edu/publications/20130101-what-makes-a-visualization-memorable)
- Bateman, S., et al. (2010). Useful Junk? The Effects of Visual Embellishment on Comprehension and Memorability of Charts. *CHI 2010*, 2573–2582. [PDF](https://vis.csail.mit.edu/classes/6.859/readings/pdfs/Bateman-UsefulJunk.pdf)
- Few, S. (2011). Critique of Bateman et al. [PDF](https://webspace.science.uu.nl/~telea001/uploads/VACourse/Few11.pdf)
- Schröder, K., et al. (2023). Telling Stories with Data: A Systematic Review. [arXiv](https://arxiv.org/pdf/2312.01164)
- Victor, B. (2011). Explorable Explanations. [Essay](https://worrydream.com/ExplorableExplanations/)

**Books**

- Tufte, E. R. (2001). *The Visual Display of Quantitative Information* (2nd ed.). Graphics Press. [Publisher](https://www.edwardtufte.com/book/the-visual-display-of-quantitative-information/)
- Cairo, A. (2012). *The Functional Art*. New Riders.
- Cairo, A. (2016). *The Truthful Art*. New Riders. [O'Reilly](https://oreilly.com/library/view/the-truthful-art/9780133440492)
- Cairo, A. (2019). *How Charts Lie*. W. W. Norton. [WorldCat](https://search.worldcat.org/title/1121263715)
- Knaflic, C. N. (2015). *Storytelling with Data*. Wiley. [Bookshop](https://bookshop.org/p/books/storytelling-with-data-a-data-visualization-guide-for-business-professionals-cole-nussbaumer-knaflic/05d99a7a2d5b9c51)
- Rosling, H., Rosling, O., & Rosling Rönnlund, A. (2018). *Factfulness*.

**Creators and sites**

- [Hans Rosling, The best stats you've ever seen (TED 2006)](https://www.ted.com/talks/hans_rosling_the_best_stats_you_ve_ever_seen) · [Gapminder](https://www.gapminder.org/about/about-gapminder/history/)
- [3Blue1Brown](https://www.3blue1brown.com/faq/) · [Manim Community Edition](https://docs.manim.community/en/stable/index.html)
- [Kurzgesagt](https://en.wikipedia.org/wiki/Kurzgesagt)
- [Vox](<https://en.wikipedia.org/wiki/Vox_(website)>)
- [The Pudding](https://pudding.cool/about) · [Polygraph](https://polygraph.cool/)
- [The Upshot](https://en.wikipedia.org/wiki/The_Upshot)
- [Nicky Case, Parable of the Polygons](https://ncase.me/polygons/) · [Explorable explanations plan](https://blog.ncase.me/explorable-explanations-the-plan)

**Commentary and context**

- [Harvard SEAS news on Borkin et al.](https://seas.harvard.edu/news/2013/10/what-makes-data-visualization-memorable)
- [World Bank Data Blog on Beyond Memorability](https://blogs.worldbank.org/opendata/what-makes-data-visualization-memorable)
- [Stephen Few, Perceptual Edge blog](https://www.perceptualedge.com/blog/?paged=27)
- [Robert Kosara, eagereyes](https://eagereyes.org/blog/2011/want-to-make-chart-memorable-add-junk)
- [UW news on the Test of Time award](https://news.cs.washington.edu/2020/10/30/professor-jeffrey-heer-and-alumnus-dominik-moritz-honored-at-ieee-vis-for-outstanding-contributions-in-data-visualization/)
- [Storybench on The Pudding](https://www.storybench.org/?p=8613)
- [Fast Company on Vox video](https://www.fastcompany.com/40575395/voxs-netflix-ambitions-are-just-the-beginning)
- [Data Stories episode 103 with Nicky Case](https://datastori.es/103-explorable-explanations-with-nicky-case/)
