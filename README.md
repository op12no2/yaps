# YAPS

**Yet another population simulator.** A browser-only tool for playing with population projections. Set up one population, shape how its fertility, life expectancy and migration change over the coming decades, and watch the projection update as you drag.

It is a single `index.html` file. No install, no build step, no server. Open it in a browser or host it on GitHub Pages.

## What it does

- Projects the population year by year for as far ahead as you choose (10 to 200 years).
- Draws the result on a chart. Hover the chart to read off the value for any year.
- Switch what the chart shows: total population, births per year, deaths per year, median age, the share of people past retirement age, or the MVP ratio (see below).
- Recomputes instantly on every change. There is no run button.
- Remembers your set-up in the browser, and can pack the whole thing into a link you can send to someone else.

## Getting started

Open the page. It starts with a plain, flat set-up: 70 million people, a balanced age profile, retirement at 65, fertility held at 1.6, life expectancy held at 82 and no migration. Everything is yours to change.

The left-hand panel holds the inputs. The chart fills the rest of the screen.

- **Years ahead** (top bar) sets how far into the future to project.
- **Show** (top bar) picks which measure the chart draws.
- **Copy share link** puts your entire set-up into the page address and copies it. Anyone who opens that link sees exactly what you see.
- **Reset** throws away your changes and goes back to the factory defaults.

## The inputs

At the top of the panel is a one-line summary: population today, population at the end of the projection, the percentage change, how the median age moves, and where the MVP ratio ends up.

- **Population today.** Type a number however you like: `68m`, `68 million`, `68,000,000` and `0.068b` all work.
- **Retirement age.** The age at which people stop counting as working-age. It feeds the "share past retirement age" view and the MVP ratio. Raise it and the ratio falls.
- **Age profile.** A three-way choice: Young, Balanced or Older. This is a rough description of how many children versus pensioners there are today. A country like Nigeria is Young, most of Western Europe is Balanced, Japan is Older. It matters a lot: an Older population keeps shrinking for decades even if fertility recovers, because there are fewer people of parenting age.
- **Three small graphs** for fertility, life expectancy and net migration. See the next section.

## The small graphs

Each of the three time-varying inputs is drawn as a line running from today (left edge) to the last year of the projection (right edge). The line *is* the setting. Its height at any year is the value used for that year.

Every graph starts flat, with a point at each end.

- **Drag a point up or down** to change the value at that year. The end points are locked to their years and only move vertically.
- **Double-click anywhere on the graph** to add a new point there. Interior points can be dragged in both directions, so you can decide when a change happens as well as how big it is.
- **Drag a point well above or below the graph** to remove it. It turns red when it is about to be dropped. Let go to confirm.
- **Hover a point** to see its exact value and year.

The curve between points is smooth and never overshoots, so two or three points are enough for any realistic shape: a steady decline, a fall that levels off, a bump that fades.

Above each graph is a sentence describing the current shape, for example "4.5 now, falling to 2.3 by 2101". If the sentence says what you meant, the graph is right.

Under each graph are preset buttons for common shapes. They reset the graph to a two-point line, so use them first and then add detail.

### Fertility

Children per woman over her lifetime. The faint line labelled "replacement 2.1" is the level at which a population roughly sustains itself without migration. Most rich countries are between 1.2 and 1.8. Sub-Saharan Africa is mostly between 3 and 6 and falling.

### Life expectancy

Expected years of life for a baby born that year. Rich countries sit in the low to mid 80s. The presets add 5 or 10 years by the end of the projection, or take it all the way to 150 for the optimists. The graph allows anything up to 150.

### Net migration

People arriving minus people leaving, per year. Positive means the population gains people. The vertical scale adjusts to the size of the population. For a large country this is often the single biggest lever, so it is worth trying "Fall to zero" to see how much of the growth it accounts for.

## How the model works

The simulator does not use a single growth rate. The population is tracked as 171 age groups, one for each year of age from 0 to 170 and over (the top end leaves room for a life expectancy of 150), and every simulated year:

1. Everyone gets a year older, and a share of each age group dies according to an age-specific mortality curve. The curve is a Gompertz curve, the standard shape for adult mortality, with an infant-mortality bump, scaled so that life expectancy at birth matches the value on the graph for that year.
2. Births are calculated from the fertility rate for that year, spread over women aged 15 to 49 with a typical age pattern that peaks in the late twenties. Half of each age group is assumed to be female.
3. Net migrants are added or removed with a typical migrant age profile, concentrated in young adults.

The starting age structure is derived from the Young / Balanced / Older choice using a stable-population approximation. That is the roughest part of the model and the first thing worth replacing with a real age pyramid.

Migrants join the same age groups as everyone else, so from the year they arrive they have the same fertility and mortality as the existing population.

## The MVP ratio

Minimum viable population. In nature it is the size below which a population is effectively extinct even though individuals remain. For a country, the suggestion here is that the limit is not size but shape: the number of people past retirement age for every person of working age, taken as 17 up to the retirement age.

Choose **MVP ratio** in the Show menu to chart it. A value of 0.30 means three retirees for every ten working-age adults. Higher is worse: the line climbs as a population ages, so a line rising towards the threshold is heading for trouble and a low, flat line is healthy. This is the reverse of the biological version, where a population falls down to its minimum viable size. The chart draws a reference line at 1.00, one retiree per working-age adult, as the proposed threshold beyond which the fabric of society is assumed to give way: the cost of supporting the old falls on too few, debt mounts, and the people who can leave do. Japan today is around 0.55 and no country has yet recorded 1.00, so the line marks territory the model can reach but the real world has not.

Things to bear in mind when reading it:

- The retirement age input moves the boundary. Push life expectancy up without moving retirement and the ratio soars; move retirement with it and the ratio settles back.
- Not everyone of working age works. If you mean retirees per actual worker, the equivalent threshold on this chart is nearer 0.7.
- The model does not yet react to the ratio. Migration follows the graph you drew whether or not the threshold is crossed. A feedback where people leave as the ratio climbs is a natural next step.

## Sharing and saving

Changes are saved in your browser automatically, so closing the tab does not lose anything. Nothing is sent anywhere.

Copy share link creates an address containing the complete set-up. Sending it to someone lets them open exactly your inputs and graphs, and then change them without affecting yours.

## Hosting it yourself

Put `index.html` in a GitHub repository, turn on GitHub Pages for that repository, and the page is live. There is nothing else to build or configure. The page loads its two typefaces from Google Fonts and falls back to the system font if that is blocked.

## Ideas for later

- A real starting age pyramid instead of the three presets.
- Migration that responds to the MVP ratio: fewer arrivals and more departures as the threshold approaches.
- More time-varying inputs using the same drag-point graphs: GDP per head, health spending, and so on.
- An age-pyramid view for any year.
- Comparing two scenarios side by side.

## Licence

MIT. See `LICENSE`.
