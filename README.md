# KPI Tree

A simple browser-based tool to visualize hierarchical business metrics as an interactive tree graph.

Compared to a flat spreadsheet or dashboard, a value tree makes metric dependencies and relationships immediately visible.


<img width="1489" height="821" alt="image" src="https://github.com/user-attachments/assets/4aace069-5cc0-4c58-af8c-871255a1a422" />


## Use Cases
- Trace downstream issues to their upstream drivers (e.g., identify which lever is causing a red metric).
- Assess the impact of improving a metric by seeing what it influences downstream.
- Ensure comprehensive metric coverage with minimal overlap (MECE).
- Filter metrics by segment, owner, benchmark/target, status, and MoM trend.

## Getting Started

The app runs entirely locally in your browser, so your data never leaves your machine.

**Option 1: Drag-and-Drop (Easiest)**
1. Open `index.html` in your browser.
2. Drag and drop your `source.csv` into the window.

**Option 2: Local Server**
If you are actively modifying the CSV and want the graph to reload on refresh without dragging-and-dropping:
```bash
python3 -m http.server 8080
open http://localhost:8080
```

## Data Schema (`source.csv`)

The application expects a `.csv` file. A dummy `source.csv` is provided to demonstrate one way to organize metrics (e.g., splitting by B2C, B2B, and Company Level). You can customize this to fit your own business. 

The columns are mapped by index, so headers can be changed. The expected structure is:

| Index | Description |
| :---: | :--- |
| 0 | `id` - Unique identifier for the metric. |
| 1 | `parent` - The `id` of this metric's parent node. |
| 2 | `metric` - Display name. |
| 3 | `formula` - Mathematical formula or definition. |
| 4 | `why` - Explanation of why this metric matters. |
| 5 | `cadence` - Reporting frequency (e.g., Monthly, Quarterly). |
| 6 | Segment 1 value |
| 7 | Segment 1 previous period value (for trend calculation) |
| 8 | Segment 2 value |
| 9 | Segment 2 previous period value |
| 10 | Segment 3 (e.g., Combined) value |
| 11 | Segment 3 previous period value |
| 12 | Segment 1 target/benchmark |
| 13 | Segment 2 target/benchmark |
| 14 | Segment 3 target/benchmark |
| 15 | Benchmark source link (optional) |
| 16 | Segment 1 owner |
| 17 | Segment 2 owner |
| 18 | Segment 3 owner |

*Note: The segment tabs in the UI (currently labeled B2C, B2B, Company Level) read from the segment blocks defined above. You can easily modify the tab names in `index.html` to reflect your own segments.*

## Architecture
- `index.html`: Contains all application logic and styling in a single file for portability.
- `cytoscape.min.js`: Graph layout engine fetched via CDN.

## License
MIT License
