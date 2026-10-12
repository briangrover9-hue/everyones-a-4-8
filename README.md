# Everyone's a 4.8

An interactive essay on how we rate people. When I booked an Airbnb for my dad's 70th, every place was rated 4.8 or higher, and the stars couldn't tell me which one was good. We rate food and hotels honestly and go easy on people, and now that AI writes the resumes and reads them too, hiring leans on the ratings we're worst at giving. The page measures that gap and runs a simulated company of 80 coworkers to see which rules still find the best people.

By [Brian Grover](https://www.linkedin.com/in/briantgrover) ([@briantgrover](https://x.com/briantgrover)), October 2026.

## What's on the page

Six full-screen scenes under a fixed frame: the title and the page's own rating at the top, a counter with dots at the bottom. One scroll, swipe or arrow key moves one scene.

1. **Everyone's a 4.8.** The Airbnb search for my dad's 70th, and the idea: we rate things honestly and people generously, and hiring now runs on the second kind.
2. **Booking an Airbnb? Guess the typical rating.** Drag the star to guess. The answer, from our count of this year's listings in San Francisco and New York, is 4.84. Packaged food then appears on the same scale as a gold line: only 7 in 100 food products average 4.8 or more. Airbnb's own explanation of why its ratings skew high follows.
3. **We go easy on people.** Grids of 100 stars in two rows. Rating people: Harvard grades that are A's, eBay feedback that's positive, Airbnb listings at 4.5+. Rating things: TripAdvisor hotels, packaged food and beauty products at 4.5+. Each number counts up as its stars fill.
4. **Likes miss half the best people.** The same 80 simulated coworkers rated two ways, on two charts that share one axis: one-click likes above, real work and trusted references below. Likes catch 5 of the 10 best in the page's run; real work and trusted references catch 9.
5. **Which rules find the best people?** One bar for each set of rules, best first in gold, each averaged over 12 simulated companies, with each rule's gain over one-click likes. A tap on a bar reruns the lower chart under those rules.
6. **What this means for hiring.** What the simulation and the research say, what to do about it (ask for real work, ask references about specific work, trust people whose past calls held up), and a question for the reader.

Scenes 2, 4 and 6 each have a "Why?" that opens a few sentences of evidence, with sources, in a frosted card over the scene's text. The page's rating climbs from 3.0 to 5.0 as you go, and the last scene says so. `methods.html` holds the rest behind a short summary, in four parts that open on request: the data, the lab's rules, the research, and the sources.

## Data and sources

- `research/airbnb_measure.py` downloads Inside Airbnb's detailed listings for San Francisco and New York City (snapshot of 14 June 2026) and writes the rating distribution to `data/airbnb.json`. Inside Airbnb data is licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); credit to [Inside Airbnb](https://insideairbnb.com/).
- Packaged food and beauty: our count of public customer reviews posted in 2025 on Amazon, Walmart, Target and Kroger product pages, from a commercial collection of retailer reviews. The raw reviews can't be republished; the counts the page draws are in `data/food.json`, and `methods.html#m-food` says how they were made.
- `research/sources.md` lists every number the page uses, the primary source it came from, and the ones that were cut.
- `data/figures.json` holds the numbers drawn in the charts, each traceable to the ledger. Its `rules` block is scene 5's bars; `node tools/lab-check.mjs` fails if any of them drifts from the model.

## How it was built

Built with [Claude Code](https://claude.com/claude-code). Research agents traced every number to its primary source, other agents built the lab and the charts, six specialist agents reviewed the design, motion, scrolling, accessibility, layout and loading, and a fresh reviewer checked the finished page against the sources.

The page is static HTML, CSS and JavaScript with no framework, no build step, no cookies and no tracking.

- `index.html`: the six scenes and all their copy; `methods.html`: the notes, research and methods
- `css/style.css`: the design system (paper, ink and gold, the two type roles, the one motion curve, the grain); `css/stage.css` for the scenes and the frame; `css/charts.css` and `css/lab.css` for the interactive parts; `css/methods.css` for the notes page
- `js/stage.js`: the scenes, the frame, the "Why?" cards and the inputs that move between scenes
- `js/motion.js`: the page's one easing curve and timings, for scripts
- `js/charts.js`: the guess, the drift grids, and the two charts on the notes page
- `js/lab-model.js`: the trust lab's model, with no DOM code, so it runs in Node too; `js/lab.js` draws it, and `node tools/lab-check.mjs` checks the claims the page makes about it
- `js/methods.js`: the blind-reveal cards on the notes page
- `js/stars.js`: the star used everywhere
- `tools/`: the share card and icon templates, the script that renders them, and the lab check

## Run it locally

```sh
python3 -m http.server 8800
```

Then open http://localhost:8800. The page needs a server (not a `file://` URL) because it loads JSON and JavaScript modules.

To re-measure the Airbnb data:

```sh
python3 research/airbnb_measure.py
```

## Credits

Airbnb data is from Inside Airbnb under CC BY 4.0. Fonts are Newsreader (Production Type) and IBM Plex Mono (IBM), both under the SIL Open Font License.
