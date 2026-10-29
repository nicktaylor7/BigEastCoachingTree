# Big East Coaching Tree

*Concept developed by Nicholas Taylor*

An interactive map of how Big East men's basketball head coaches learned the job. It starts with Dave Gavitt, who founded the league, and its charter coaches (the men on the sidelines in its first season), and runs through every Big East head coach since, down to today's benches. You can see who worked on whose staff, which branches produced the most coaches and titles, and who ended up taking over for his old boss.

> **Independent fan project.** Not affiliated with, endorsed by or sponsored by the NCAA or the Big East Conference. All team and conference names belong to their owners.

---

## What's in it

**Three views**

| View | What it does |
|---|---|
| **Tree** | A zoomable family tree. Click a coach to open his branch and read his bio. Only one path is open at a time, and everything off that path fades back. |
| **Breakdown** | A drill-down chart. It starts from one total and splits it branch by branch, with a bar for each branch's share. You can count Big East head coaches, current head coaches, everyone on the tree, national titles or Final Fours. |
| **Other sites** | Links to Nicholas Taylor's other Big East projects. |

**Each coach's bio panel shows**
- National titles and Final Fours
- The path back to Dave Gavitt
- Who he worked under, and who came off his staffs
- Career stops, with the stops that create a tree line highlighted
- Sources

**Search.** Type any coach's name to jump straight to him in either view.

---

## How to read the tree

| Mark | Meaning |
|---|---|
| Orange-red bar on the left of a card | Current Big East head coach |
| Black bar on the left of a card | Former Big East head coach |
| Light grey bar, italic name | Mentor who never coached in the Big East |
| Orange-red dot | NCAA national title |
| Green square | NCAA Final Four without a title |
| Thick blue line | He later took over for his old boss at that school |
| Bold dotted line | Inferred from dates (see below) |
| Orange dashed line | He also worked under this coach (shown only for the selected coach) |
| `+12` badge | Number of coaches hidden inside a collapsed branch |

Hover over a line, or tap it on a phone, to see the actual job behind the connection.

---

## The rule for a connection

**A line only counts if the coach worked on that coach's staff.**

- Playing for someone does **not** count. Ronald Nored played for Brad Stevens at Butler, but his line comes from working on Stevens's Celtics staff.
- Being related does **not** count. Dan Hurley's father, Bob Hurley Sr., is not on Dan's line. Richard Pitino is on the tree because he worked on his father's Louisville staff, not because he is his son.
- Administrative, operations and graduate-assistant jobs on a staff do count.

---

## Scope

- **Every head coach** at a Big East school during its Big East years, from the league's founding to today. That includes schools that later left the league: Syracuse, Pittsburgh, Boston College, Notre Dame, Louisville, West Virginia, Cincinnati, Rutgers, Miami, Virginia Tech and South Florida.
- **Mentors** who never coached in the league (Billy Donovan, Herb Sendek, Brad Stevens and others) appear when they are the link between two Big East coaches.
- **Not included:** one-season interim coaches.
- **No years or dates** are shown anywhere on the page, by design.
- Coaches with no staff line back to a charter coach sit on a separate branch called **Lines from outside**.

Current totals: 86 Big East head coaches and 105 people on the tree.

---

## Data notes

**Titles and Final Fours** follow the NCAA's official record, so vacated runs are excluded (for example Louisville's in 2012 and 2013, and Kansas's in 2018). They count NCAA tournament results only, not Big East titles.

**Inferred links.** For nine connections the source confirms the assistant job but does not name the head coach. These were matched to whoever was head coach at that school during those years. They are drawn as bold dotted lines and labeled "inferred" in the bio panel:

- Lou Carnesecca → Brian Mahoney
- Brendan Malone → Al Skinner
- Rick Barnes → Frank Haith
- Dave Odom → Frank Haith
- Rick Barnes → Ricky Stokes
- Dave Odom → Ricky Stokes
- Jamie Dixon → Mike Rice
- Roy Williams → Matt Doherty
- Mike Krzyzewski → Steve Wojciechowski

**Entries that still need a source:** Steve Wojciechowski, Chris Mullin and John Beilein have no linked source yet.

**Main sources:** Wikipedia coaching histories for each coach, official school staff bios, team news releases, and the NCAA and Wikipedia records of national champions and Final Four participants. Each coach's bio panel links the specific sources behind his connections.

Corrections are welcome. If you know a connection that's wrong or missing, please open an issue with a source.

---

## Running it

The whole project is one self-contained file, `big-east-coaching-tree.html`.

- **Locally:** open the file in any modern browser.
- **GitHub Pages:** rename the file to `index.html`, commit it to a repository, and turn on Pages under *Settings → Pages*.

It needs an internet connection to load two things:
- the [d3](https://d3js.org) library (v7.8.5, from cdnjs)
- the Newsreader and Public Sans fonts, from Google Fonts

If the fonts can't load, it falls back to standard system fonts.

It works on desktop browsers and on iPhone and Android:
- On phones, the legend sits behind a **Key** button.
- The bio opens as a short sheet at the bottom of the screen; tap it to read the full bio.
- Pinch to zoom and drag to pan.
- It follows the device's light or dark mode.

---

## Updating the data

All of the data lives in the `<script>` near the bottom of the HTML file.

**Coaches (`const D = [...]`).** Each coach is one entry:

```js
{ id: "hodgson",            // unique short id
  parent: "oats",           // the boss whose staff puts him on the tree
  also: ["someone"],        // optional: other bosses he worked under (dashed lines)
  kind: "cur",              // "cur" current Big East HC, "be" former Big East HC, "men" mentor
  name: "Bryan Hodgson",
  sub: "Providence",        // school(s) shown under the name
  bio: "Short bio...",
  stops: [["Buffalo", "assistant under Nate Oats", "k"]],  // "k" marks a stop that draws a line
  src: [["Source title", "https://..."]] }
```

**Results (`const RES`).** NCAA results as `id: [Final Fours, national titles]`.

**Took over for his boss (`const SUCC`).** `staffId: ["bossId", "School"]`.

**Inferred links (`const SOFT`).** `"bossId>staffId"` strings.

When a coaching change happens, update the outgoing coach's `kind` from `"cur"` to `"be"` and add the new coach with `kind: "cur"`.

---

## More by Nicholas Taylor

- [Big East Gami](https://nicktaylor7.github.io/BigEastGami/): every final score in Big East men's basketball, with the rare and repeated scorelines called out.
- [Big East Big Data](https://nicktaylor7.github.io/BigEastBigData/): historical Big East men's basketball stats, from conference-wide numbers down to teams and players.

---

*Independent fan project. Not affiliated with, endorsed by or sponsored by the NCAA or the Big East Conference.*
