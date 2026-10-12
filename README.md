# Everyone's a 4.8

An interactive drop about trust signals in hiring. AI now writes the resumes and AI reads them, so hiring leans harder on who will vouch for you. The rating systems people have built for that job tend to drift toward the top of their scales, where they tell fewer and fewer people apart. The drop measures that drift, explains the forces behind it, and lets you run a simulated company of 80 coworkers to see which rules keep a vouch worth something.

By [Brian Grover](https://www.linkedin.com/in/briantgrover) ([@briantgrover](https://x.com/briantgrover)), October 2026. We judge restaurants and hotels honestly and go easy on people. This drop shows what that does to ratings, and what it means for hiring now that AI writes and reads the resumes.

## What's on the page

Six full-screen scenes under a fixed frame: the title and the page's own rating at the top, a counter with dots at the bottom. One scroll, swipe or arrow key moves one scene, and each scene's line hands off to the next.

1. **Everyone's a 4.8.** We'll tell a restaurant its fries were soggy, but rate a person and almost everyone gets a 4.8. Now that AI writes and reads the resumes, hiring leans on the ratings we're worst at giving.
2. **Booking an Airbnb? Guess the typical rating.** Drag the star to guess the typical rating in San Francisco and New York. The answer, from our own measurement of this year's listings, is 4.84.
3. **We go easy on people.** Grids of 100 stars for Harvard grades, eBay sellers, LinkedIn endorsements, GitHub stars, and Airbnb against TripAdvisor hotels. When a person is on the other end, the scores crowd the top; hotels, rated as businesses, spread out, about 1 in 5 star ratings on Yelp in 2023 was a single star, and a third of food products with 10+ reviews on big US store sites averaged under 4 stars in 2025.
4. **The comparison.** The same 80 simulated coworkers rated two ways at once, on two charts that share one axis: one-click likes above, real work and vetted vouches below. Likes find about half of the 10 most skilled; real work and vetted vouches find 9 in the page's run.
5. **Which rules find the best people?** In our simulation, one bar for each set of rules, best first, each averaged over 12 simulated companies. A tap on a bar reruns the lower chart under those rules, and a line under the bars says the numbers are simulated, not measured.
6. **What this means for hiring.** We're good at judging things and bad at judging each other: on one freelance site, 28% of employers who privately said they'd never rehire a worker still gave that worker 4 stars or more in public. So lean on signals that are hard to fake: real work, references about specific work, and more weight on people whose past calls held up.

Scenes 2, 4 and 6 each have a "Why?" that opens a few sentences of evidence, with sources, in a frosted card over the scene's text. The page's rating climbs from 3.0 to 5.0 as you go, and the last scene says so. `methods.html` holds the rest behind a short summary, in four parts that open on request: the data, the lab's rules, the research, and the sources.

## Data and sources

- `research/airbnb_measure.py` downloads Inside Airbnb's detailed listings for San Francisco and New York City (snapshot of 14 June 2026) and writes the rating distribution to `data/airbnb.json`. Inside Airbnb data is licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); credit to [Inside Airbnb](https://insideairbnb.com/).
- `research/sources.md` lists every number the page uses, the primary source it came from, and the ones that were cut.
- `data/figures.json` holds the numbers drawn in the charts, each traceable to the ledger. Its `rules` block is scene 5's bars; `node tools/lab-check.mjs` fails if any of them drifts from the model.

## How it was built

Built with [Claude Code](https://claude.com/claude-code). Research agents traced every number to its primary source, other agents built the lab and the charts, six specialist agents reviewed the design, motion, scrolling, accessibility, layout and loading, and a fresh reviewer checked the finished page against the sources. The full conversation is in `TRANSCRIPT.md`.

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
