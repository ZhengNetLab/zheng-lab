# Reading Romano's Feed: A Small Data Experiment Before the Ballon d'Or

Oct 23, 2026 · @Xin

## The idea

The 2026 Ballon d'Or will be announced in London on October 26. A few days before, I asked a slightly silly question: does Fabrizio Romano's feed already lean toward a winner?

Romano is football's best-known transfer reporter, and he has said nothing about the result. But he posts a steady stream of quotes about the two favourites, Harry Kane and Lamine Yamal. If the mood around the award shifts, his feed might show it.

## The data

I collected every Romano post on X that mentions Kane or Yamal between October 1 and 23, 2026: 68 posts in total. For each one I kept the date, the player it mentions, the text and a screenshot.

One post mentions both players, so Kane appears in 39 posts and Yamal in 30.

## The method

I kept the analysis deliberately simple: one cutoff date and one keyword rule.

- **Cutoff:** October 14, the date of the last post in which someone backs Yamal for the award (Rafa Leão: "I hope Lamine Yamal wins the Ballon d'Or").
- **Keyword rule:** a post counts as "about the award" only if its text says "Ballon d'Or".

For each player I then compared the share of posts about the award before and after the cutoff. The one post that mentions both players counts for both.

## What the numbers show

Kane's share of award posts stays flat, while Yamal's falls from 45% to 5%.

| Player | Before Oct 14 | After Oct 14 |
| --- | --- | --- |
| Harry Kane | 7 of 23 posts (30%) | 5 of 16 posts (31%) |
| Lamine Yamal | 5 of 11 posts (45%) | 1 of 19 posts (5%) |

The single Yamal post after the cutoff that mentions the award is Thibaut Courtois, saying the Ballon d'Or should go to Kylian Mbappé. So after October 14, nothing in Romano's feed backs Yamal for the trophy.

Yamal still gets praise. Five posts after the cutoff call him "the best (player) in the world", from Fermín López, Neymar, Hansi Flick (twice) and Pedri. None of them uses the words "Ballon d'Or". My playful reading in the video: it is almost as if they know who is winning, and back Yamal anyway.

## What this does not show

This is a pattern in one feed, not proof that anyone knows the result. Five reasons to stay humble:

- **Fixtures drive the feed.** Romano mostly reposts press-conference quotes, so his posts follow the match calendar: PSG vs Barcelona on October 20, Bayern vs Arsenal on October 21.
- **Small sample.** Only 35 posts fall after the cutoff, and just one of them is a Yamal award post.
- **The cutoff was chosen after looking.** A fair test moves the cutoff day by day and checks whether the gap survives.
- **The keyword rule matters.** If "best in the world" counted as backing, support for Yamal would run until October 19.
- **Public mood is not inside knowledge.** Even a real shift reflects what everyone can see. Bookmakers already had Kane at about a 75% chance on October 22 ([Squawka](https://www.squawka.com/en/outright-markets/ballon-dor-odds-2026/)).

## Turning it into a Short

The video, "Romano Already Knows? 👀", is a 60-second vertical Short built only from the screenshots and the table above. There is no footage. Three colours carry the meaning throughout: red for Kane, blue-violet for Yamal, gold for "mentions the Ballon d'Or".

1. **Story.** Open on the Leão post fading to grey. Shrink all 68 posts into tiles, split them at October 14, and light up the award posts row by row. End on the lonely Courtois post, then the five "best in the world" posts.
2. **Screenshot prep.** A short Python script runs OCR (Tesseract) on each screenshot, finds the key words and draws a gold box around them. The originals stay untouched.
3. **Index file.** One CSV row per post (date, player, before or after, mentions the award or not) decides which tiles glow. The table in this post is computed from the same file.
4. **Render.** One prompt to Claude Code holds the scene timeline, colours, mobile safe areas and checks. Before rendering, it recomputes the four numbers from the CSV and stops if they do not match.
5. **Voice.** Narration comes from Google Cloud Text-to-Speech, one line per scene, fitted to the scene length. The silent master and the voice track are kept separate, so I can swap in my own recording later.

## Takeaways

- A tiny dataset can tell a clear story when the rule is simple and stated up front.
- The honest claim is smaller than the hook: Romano's feed moved on from Yamal, which is not the same as Romano knowing.
- The guess is checkable. On October 26 we find out, and either way it is material for the next video.

## Sources

- [Sky Sports: 2026 Ballon d'Or ceremony on October 26 in London](https://www.skysports.com/football/news/13582892/ballon-dor-2026-harry-kane-declan-rice-jude-bellingham-among-nominees-but-no-cristiano-ronaldo)
- [Squawka: Ballon d'Or odds, October 22](https://www.squawka.com/en/outright-markets/ballon-dor-odds-2026/)
- Romano's posts on X, [@FabrizioRomano](https://x.com/FabrizioRomano), October 1–23, 2026
