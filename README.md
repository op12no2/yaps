# YAPS

**Yet another population simulator.** A browser-only tool for playing with population projections. Set up one population, shape how its fertility, life expectancy, retirement age and migration change over the coming decades, and watch the projection update as you drag. Try it here: https://op12no2.github.io/yaps/

It is a single `index.html` file. No install, no build step, no server. Open it in a browser or host it on GitHub Pages.

## What it does

- Projects the population year by year for as far ahead as you choose (10 to 200 years).
- Charts one measure at a time: total population, births and deaths per year, median age, the share of people past retirement age, the age mix, or the MVP ratio (see below). Click the coloured chips above the chart to switch. Hover the chart to read off the value for any year.
- Recomputes instantly on every change. There is no run button.
- Remembers your set-up in the browser, and can pack the whole thing into a link you can send to someone else.

## Getting started

Open the page. It starts with a plain, flat set-up: 70 million people, an age profile roughly like the UK's in the 2020s, working age from 17 to 65, fertility held at 1.6, life expectancy held at 82 and no migration. Everything is yours to change.

The left-hand panel holds the inputs. The chart fills the rest of the screen.

- **Start year** (top bar) is the calendar year the scenario begins in. It only affects the labels: the model itself does not know what year it is, so a saved scenario is not tied to any date. It starts at the current year.
- **Years ahead** (top bar) is a slider from 10 to 200 years.
- **Lifetime** (top bar) is a slider with two handles: drag one to a person's birth year and the other to their death year. A dashed line then climbs across the chart, from the birth year at the bottom to the death year at the top, so you can see where a life falls across the years shown. Hovering the chart also tells you how old that person is in that year. It changes nothing in the model; it is only a marker. To get rid of it, drag both handles to years outside the chart.
- **Copy share link** puts your entire set-up into the page address and copies it. Anyone who opens that link sees exactly what you see.
- **Reset** throws away your changes and goes back to the factory defaults. Click it twice: the first click arms it for three seconds, the second does it.

## Reading the chart

The years along the bottom are the start year plus however far ahead you set. They are labels only. Nothing in the model depends on the date, so the same set-up describes a country in 2026 or a colony in 2200, and the start year slider just changes what the axis says.

The chips above the chart pick what it shows. One is active at a time, so the vertical axis is always in real units for that measure: people, people per year, years, a percentage, or the ratio.

**Births & deaths** draws both lines on the same axis because they share a unit. The year the deaths line crosses above the births line is the year the population would start shrinking without migration.

**Age mix** stacks the population into three bands, children, working age and retired, with the two boundaries set by the start-of-work and retirement graphs, so the height of the whole stack is the total population and the bands inside it show who makes it up. The retired band divided by the working-age band is the MVP ratio. Because the bands follow those graphs, dragging retirement upwards visibly moves people from the top band into the middle one, and dragging the start of work upwards moves people from the middle band into the bottom one. Hovering gives the people and the percentage in each band.

Hover anywhere on the chart for the exact values in that year. The active chip is saved with everything else.

## The inputs

At the top of the panel is a one-line summary: population at the start, population at the end of the projection, the percentage change, how the median age moves, and where the MVP ratio ends up.

- **Population.** A slider from 100 thousand to 12 billion. It moves in proportional steps, so a small town and the whole planet are both within reach without the low end being cramped.
- **Age profile.** A graph of how many people there are at each age at the start, from 0 to 150 along the bottom. Drag it into shape, or click Young, Balanced or Older to load a starting shape. Balanced is roughly the UK, with its baby-boom bump in the late fifties. Young is a country like Nigeria, Older is a country like Japan. It matters a lot: an older population keeps shrinking for decades even if fertility recovers, because there are fewer people of parenting age.
- **Five more small graphs** for fertility, life expectancy, start of working age, retirement age and net migration, each running from the start year to the end of the projection. See the next section.

## The small graphs

All six inputs use the same kind of graph. The first, the age profile, runs across ages 0 to 150 and its height is how many people there are at that age. The other five run from the start year (left edge) to the last year of the projection (right edge), and their height at any year is the value used for that year. Either way the line *is* the setting.

Every graph starts flat, with a point at each end.

- **Drag a point up or down** to change the value at that year. The end points are locked to their years and only move vertically.
- **Double-click anywhere on the graph** to add a new point there. Interior points can be dragged in both directions, so you can decide when a change happens as well as how big it is.
- **Drag a point well above or below the graph** to remove it. It turns red when it is about to be dropped. Let go to confirm.
- **Hover a point** to see its exact value and year.

The curve between points is smooth and never overshoots, so two or three points are enough for any realistic shape: a steady decline, a fall that levels off, a bump that fades.

**Click a graph's heading**, for example RETIREMENT AGE, and that graph opens full size in the main area for easier editing. The chart pauses while it is open. Press Done, or Escape, to go back, and the projection recalculates once with your changes.

Above each graph is a sentence describing the current shape, for example "4.5 in 2026, falling to 2.3 by 2101". If the sentence says what you meant, the graph is right.

### Age profile

The vertical scale is relative, so only the shape matters: the population slider sets how many people there are in total, and the graph divides them between the ages. Hovering a point tells you what share of people are that age. The summary above the graph gives the median age and the share of children and retired people that the shape implies.

One thing to know: the height at age 0 is the number of babies born recently, and the fertility graph decides how many are born from next year on. If the two disagree, the first year of the projection has a small step in births. The Balanced shape and the default fertility of 1.6 are close to each other.

### Fertility

Children per woman over her lifetime. The faint line labelled "replacement 2.1" is the level at which a population roughly sustains itself without migration. Most rich countries are between 1.2 and 1.8. Sub-Saharan Africa is mostly between 3 and 6 and falling.

### Life expectancy

Expected years of life for a baby born that year. Rich countries sit in the low to mid 80s. The graph allows anything up to 150, for the optimists.

### Start of working age

The age at which people stop counting as children and start counting as working-age. It starts at 17 and runs from 10 to 30. Push it up to model longer education, or down for a society where people work younger. Together with the retirement age it defines the working-age band that the MVP ratio and the age mix are built on.

### Retirement age

The age at which people stop counting as working-age and start counting as retired. It feeds the "share past retirement age" view and the MVP ratio. It is a graph rather than a single number because the two can move together: if medicine keeps people productive for longer, retirement can drift upwards over the decades and the MVP ratio settles back down. The graph runs from 40 to 120.

### Net migration

People arriving minus people leaving, per year. Positive means the population gains people. The vertical scale adjusts to the size of the population. For a large country this is often the single biggest lever, so it is worth dragging it to zero to see how much of the growth it accounts for.

## How the model works

The simulator does not use a single growth rate. The population is tracked as 171 age groups, one for each year of age from 0 to 170 and over (the top end leaves room for a life expectancy of 150), and every simulated year:

1. Everyone gets a year older, and a share of each age group dies according to an age-specific mortality curve. The curve is a Gompertz curve, the standard shape for adult mortality, with an infant-mortality bump, scaled so that life expectancy at birth matches the value on the graph for that year.
2. Births are calculated from the fertility rate for that year, spread over women aged 15 to 49 with a typical age pattern that peaks in the late twenties. Half of each age group is assumed to be female.
3. Net migrants are added or removed with a typical migrant age profile, concentrated in young adults.

The starting age structure comes straight from the age profile graph, scaled to the population slider, with a short tail beyond age 150.

### How migrants are spread across ages

Net migration is one number per year, and the model spreads it across ages using a single fixed profile: a bell curve centred on age 27 with a spread of about ten years, plus a smaller bump around age 8 for children travelling with their parents, cut off at age 80. Roughly:

| Age band | Share of net migrants |
|---|---|
| 0 to 14 | about 12% |
| 15 to 24 | about 27% |
| 25 to 34 | about 40% |
| 35 to 44 | about 17% |
| 45 and over | about 4% |

That is a fair match for typical international migration, which is dominated by people in their twenties and early thirties. The assumptions that follow from it:

- **One shape for both directions.** Positive migration adds people with this profile, negative removes them with the same profile. In reality emigration often skews older than immigration, for example retirees leaving, and the model cannot show that.
- **Migrants become locals on arrival.** They join the same age groups as everyone else, so from that year on they have the same fertility and mortality as the existing population. There is no separate fertility rate for arrivals and no tracking of descendants.
- **No sex split.** The model does not track sex, so migrants are taken to be half women like everyone else.
- **The shape never changes.** It is the same in year 1 and year 200, and it does not react to anything else in the model.
- **Nobody over 80 moves.** Migration cannot add or remove people above that age.
- **Age groups cannot go below zero.** If heavy emigration would empty an age group, it stops at zero, so a very large outflow removes fewer people than the graph says.

## The MVP ratio

Minimum viable population. In nature it is the size below which a population is effectively extinct even though individuals remain. For a country, the suggestion here is that the limit is not size but shape: the number of people past retirement age for every person of working age, where working age runs from the start-of-work graph up to the retirement graph.

The **MVP ratio** chip above the chart shows it. A value of 0.30 means three retirees for every ten working-age adults. Higher is worse: the line climbs as a population ages, so a line rising towards the threshold is heading for trouble and a low, flat line is healthy. This is the reverse of the biological version, where a population falls down to its minimum viable size. The threshold is 1.00, one retiree per working-age adult, the proposed point beyond which the fabric of society is assumed to give way: the cost of supporting the old falls on too few, debt mounts, and the people who can leave do. Japan in the 2020s is around 0.55 and no country has yet recorded 1.00, so the line marks territory the model can reach but the real world has not.

Things to bear in mind when reading it:

- The retirement age graph moves the boundary year by year. Push life expectancy up without moving retirement and the ratio soars; let retirement rise with it and the ratio settles back.
- Not everyone of working age works. If you mean retirees per actual worker, the equivalent threshold on this chart is nearer 0.7.
- The model does not yet react to the ratio. Migration follows the graph you drew whether or not the threshold is crossed. A feedback where people leave as the ratio climbs is a natural next step.

## Sharing and saving

Changes are saved in your browser automatically, so closing the tab does not lose anything. Nothing is sent anywhere.

Copy share link creates an address containing the complete set-up. Sending it to someone lets them open exactly your inputs and graphs, and then change them without affecting yours.

## Hosting it yourself

Put `index.html` in a GitHub repository, turn on GitHub Pages for that repository, and the page is live. There is nothing else to build or configure. The page loads its two typefaces from Google Fonts and falls back to the system font if that is blocked.

## Ideas for later

- Real age pyramids for a few countries and the world as one-click starting points.
- Migration that responds to the MVP ratio: fewer arrivals and more departures as the threshold approaches.
- More time-varying inputs using the same drag-point graphs: GDP per head, health spending, and so on.
- Comparing two scenarios side by side.

## Licence

MIT. See `LICENSE`.
