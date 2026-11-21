# Germination Counter

A browser-based tool for counting germinated seeds in petri dish photos. Load a photo, and the app marks every seed as **germinated**, **unsure**, or **not germinated** and reports the germination percentage. You can correct any marker by tapping it, save your marks to reload later, and export results for many dishes as a CSV file.

**Open the app:** https://lilabatvt.github.io/GerminationCounter/

Everything runs in your browser. Photos are never uploaded anywhere, and the app works on desktop, tablet, and phone.

---

## Contents

1. [Quick start](#quick-start)
2. [Taking good photos](#taking-good-photos)
3. [Reading the markers](#reading-the-markers)
4. [Correcting the results](#correcting-the-results)
5. [Adjusting the dish circle](#adjusting-the-dish-circle)
6. [Detection settings](#detection-settings)
7. [Saving, reloading, and exporting](#saving-reloading-and-exporting)
8. [Where your files are saved](#where-your-files-are-saved)
9. [Example workflows](#example-workflows)
10. [File formats](#file-formats)
11. [Troubleshooting](#troubleshooting)
12. [Hosting your own copy](#hosting-your-own-copy)

---

## Quick start

1. Open the app and tap **Load photo**. Choose a photo of one petri dish (JPG, PNG, or HEIC).
2. The app detects the seeds and shows the germination percentage on the right (below the photo on phones).
3. Check the markers. Tap any marker that is wrong to change its category.
4. Tap **Save this dish**. This adds the dish to the results table and downloads a marks file.
5. Repeat for each dish, then tap **Export CSV** to download all results.

To try the app without your own photo, tap **Use the sample dish**.

---

## Taking good photos

Detection works best when photos are consistent. For each dish:

- Shoot from directly above, with the whole dish in the frame and roughly centered.
- Use even lighting and avoid strong reflections on the lid. Removing the lid helps if your protocol allows it.
- Use a plain, dark background around the dish.
- Keep labels, rulers, and text outside the dish circle. Anything inside the circle can be mistaken for a seed.
- Use the same setup (distance, lighting, background) for every dish in an experiment.

Very large photos are fine. The app scales them down to 1000 pixels on the longest side for analysis.

---

## Reading the markers

Each detected seed gets a circle. Shape and color both carry the category, so the markers stay readable for colorblind users.

| Marker | Category | Counted? |
|---|---|---|
| Solid green circle | Germinated | Yes |
| Dashed amber circle | Unsure | Yes |
| Magenta circle with an × | Not germinated | Yes |
| Dotted light blue circle | Misdetection | No |

A marker with a small number beside it (for example **×2**) stands for two or more seeds touching each other.

### How the app decides

- **Seeds** are found by their dark seed coats. A yellow cotyledon with no seed coat nearby also counts as one germinated seedling.
- A seed coat and its yellow cotyledons are joined into one seed, either along the white stem or when they lie close together.
- **Germinated:** yellow cotyledons have emerged, or a white root reaches past the set root length.
- **Unsure:** a short root, or a pale halo the app cannot call either way.
- **Not germinated:** a bare seed coat with no root or cotyledon.

### The results panel

- **Germinated %** = germinated ÷ (germinated + unsure + not germinated), rounded to one decimal place.
- If there are unsure seeds, the panel also shows the percentage you would get by counting them as germinated.
- **Misdetections** are listed separately and are never included in the total or the percentage.

---

## Correcting the results

Choose a tool from the toolbar under the photo, then tap on the image.

| Tool | Tap on a marker | Tap on empty space |
|---|---|---|
| **Tap to cycle** (default) | Germinated → unsure → not germinated → misdetection → back to germinated | Nothing |
| **Germinated** | Marks it germinated | Adds a germinated seed there |
| **Unsure** | Marks it unsure | Adds an unsure seed there |
| **Not germinated** | Marks it not germinated | Adds a not germinated seed there |
| **Misdetection** | Marks it as a misdetection | Nothing |
| **Remove** | Deletes the marker completely | Nothing |

Tips:

- Prefer **Misdetection** over **Remove** for false detections. The marker stays visible, so you can see what was excluded and cycle it back if you change your mind.
- Use the **1× / 2× / 3×** buttons to zoom in on crowded areas. When zoomed, scroll the image to move around.
- Tick **Show detected pixels** in Detection settings to see what the app recognized: red for seed coats, yellow for cotyledons, blue for roots.

> **Note:** Changing a detection setting or adjusting the dish circle re-runs detection, which clears your manual corrections. Adjust the dish and settings first, then make corrections.

---

## Adjusting the dish circle

The app only counts seeds inside the dashed circle. By default the circle is centered and fills most of the photo. If the dish is off-center, or a label or the dish rim is being picked up:

1. Tap **Adjust dish**. The circle turns blue.
2. Drag inside the circle to move it.
3. Drag the circle's edge (or the dot on its right side) to resize it.
4. Let go. Detection re-runs with the new circle.

Then switch back to **Tap to cycle** to continue correcting.

---

## Detection settings

Open **Detection settings** if many seeds are wrong in the same way on a whole batch of photos. Each slider has a short explanation in the app.

| Setting | Default | What it does | When to change it |
|---|---|---|---|
| Seed coat darkness | 105 | How dark a pixel must be to count as seed coat | Raise if seed coats are missed; lower if shadows are picked up |
| Cotyledon color | 70 | How strongly yellow a cotyledon must be | Lower for paler cotyledons; raise if yellowish debris is picked up |
| Root contrast | 16 | How much brighter than the paper a root must be | Lower if roots are missed; raise if paper texture is mistaken for roots |
| Seed coat to cotyledon link | 9× | How far apart a seed coat and its cotyledons can be and still count as one seed, in seed radii | Lower if separate seedlings get merged; raise if one seedling is counted twice |
| Root length for germinated | 5× | Root length, from the seed center in seed radii, needed to call a seed germinated | Match your lab's germination criterion |
| Unsure starts at | 80% | Share of that root length that marks a seed as unsure | Lower to flag more borderline seeds as unsure |

Tap **Reset settings** to return to the defaults. The settings used for each dish are stored in its marks file.

---

## Saving, reloading, and exporting

### Save a dish

When the markers on a photo look right, tap **Save this dish**. This does two things:

1. **Adds a row to the results table** for that image. Saving the same image again updates its row instead of adding a duplicate.
2. **Downloads a marks file** named after the photo. For example, `dish_A3.jpg` produces `dish_A3.marks.json`. The marks file records every marker (including misdetections), the dish circle, and the detection settings.

### Reload marks later

To continue working on a dish you saved earlier, use either method:

- **Both at once:** tap **Load photo** and select the photo **and** its `.marks.json` file together.
- **One after the other:** load the photo, then tap **Load marks** and select its marks file.

Every marker, the dish circle, and the settings come back exactly as you saved them. If the marks file was saved for a different image name, the app still applies it and shows a note.

### Export the results table

Tap **Export CSV** to download every saved dish as one CSV file, named with today's date, for example `germination-results-2026-11-21.csv`. It opens directly in Excel, Google Sheets, or R.

### Manage the table

- Each row has a **Delete** button.
- **Clear table** removes all rows. Tap it twice to confirm.

> **Important:** The results table is stored inside your browser on that device. It survives closing the page, but it does **not** follow you to another computer or browser, and it is erased if you clear your browser data. **Export the CSV at the end of every session.** If a row is lost, you can rebuild it by loading the photo and its marks file and saving again.

---

## Where your files are saved

The app runs in your browser, so saving works like any other download. **Nothing is saved to GitHub.** GitHub only hosts the page and cannot receive your files.

| Device | Where marks files and CSVs go |
|---|---|
| Windows / Mac (Chrome, Edge, Firefox, Safari) | Your **Downloads** folder |
| iPhone / iPad (Safari) | **Files** app → **Downloads** (in iCloud Drive or On My iPhone) |
| Android (Chrome) | The phone's **Downloads** folder |

**Tip:** To save straight into a project folder, turn on your browser's **"Ask where to save each file before downloading"** option (Chrome and Edge: Settings → Downloads; Firefox: Settings → General → Downloads; Safari on Mac: Settings → General → File download location → Ask for each download).

What is **not** saved as a file:

- **The photo itself.** It is never changed or copied. The marks file only refers to it by name, so keep each photo and its `.marks.json` file together.
- **The results table.** It lives in the browser until you export it as a CSV.

To collect results from several people, have each person export their CSV and put it in a shared folder (for example Google Drive, OneDrive, or Teams), or send the files to one person who commits them to the repository.

---

## Example workflows

### Example 1: Scoring one experiment in a single session

You have 12 dishes photographed on day 5, named `T1_rep1.jpg` through `T4_rep3.jpg`.

1. Put all 12 photos in one folder, for example `Germination/Day5/`.
2. Load `T1_rep1.jpg`. If the dish is off-center, use **Adjust dish** first.
3. Correct any wrong markers, then tap **Save this dish**.
4. Move `T1_rep1.marks.json` from Downloads into `Germination/Day5/`, or set your browser to ask where to save.
5. Repeat for the other 11 photos.
6. Tap **Export CSV** and save it as `Germination/Day5/results.csv`.
7. Tap **Clear table** so the next experiment starts fresh.

Your folder ends up looking like this:

```
Germination/Day5/
├── T1_rep1.jpg
├── T1_rep1.marks.json
├── T1_rep2.jpg
├── T1_rep2.marks.json
│   ...
├── T4_rep3.jpg
├── T4_rep3.marks.json
└── results.csv
```

### Example 2: Fixing a dish you already saved

A colleague spots a miscounted seed in `T2_rep1.jpg`.

1. Tap **Load photo** and select both `T2_rep1.jpg` and `T2_rep1.marks.json`.
2. Your earlier marks reappear. Fix the seed.
3. Tap **Save this dish**. The row for `T2_rep1.jpg` is updated and a new marks file is downloaded. Replace the old marks file with the new one. Some browsers add a number to the name, such as `T2_rep1.marks (1).json`, so rename it if needed.
4. Tap **Export CSV** again for an updated results file.

### Example 3: A batch with unusual lighting

The day 2 photos were taken under different lights, and many seed coats are missed.

1. Load the first photo and tick **Show detected pixels**.
2. Raise **Seed coat darkness** until the seed coats turn fully red without picking up shadows.
3. Check the second and third photos with the same settings.
4. Correct and save each dish as usual. The settings are stored in every marks file, so reloading a dish later brings back the right settings.

### Example 4: Converting iPhone photos on a Mac

The app opens HEIC photos directly, but converting first makes loading faster. In Terminal, inside the folder of photos:

```bash
mkdir -p jpg
for f in *.HEIC *.heic; do [ -e "$f" ] && sips -s format jpeg -s formatOptions 90 "$f" --out "jpg/${f%.*}.jpg"; done
```

This writes JPG copies into a `jpg` subfolder and leaves the originals untouched. To stop the iPhone from saving HEIC in the first place, go to **Settings → Camera → Formats → Most Compatible**.

---

## File formats

### Results CSV

One row per saved dish:

| Column | Meaning |
|---|---|
| `image` | Photo file name |
| `germinated` | Number of germinated seeds |
| `unsure` | Number of unsure seeds |
| `not_germinated` | Number of not germinated seeds |
| `total_seeds` | germinated + unsure + not_germinated |
| `misdetections` | Markers flagged as misdetections (not counted) |
| `germination_percent` | germinated ÷ total_seeds × 100 |
| `germination_percent_unsure_as_germinated` | (germinated + unsure) ÷ total_seeds × 100 |
| `saved_at` | Date and time the dish was saved (UTC) |

Example:

```csv
image,germinated,unsure,not_germinated,total_seeds,misdetections,germination_percent,germination_percent_unsure_as_germinated,saved_at
T1_rep1.jpg,26,0,1,27,0,96.3,96.3,2026-11-21T15:02:11.482Z
T1_rep2.jpg,22,3,5,30,2,73.3,83.3,2026-11-21T15:06:40.019Z
T2_rep1.jpg,9,4,17,30,1,30,43.3,2026-11-21T15:11:58.773Z
```

### Marks file (`.marks.json`)

Positions are stored as fractions of the image size, so marks line up with the photo whatever its resolution.

```json
{
 "app": "germination-counter",
 "version": 1,
 "image": "T1_rep1.jpg",
 "saved_at": "2026-11-21T15:02:11.482Z",
 "width": 985,
 "height": 1000,
 "dish": { "cx": 0.5, "cy": 0.5, "r": 0.46 },
 "settings": { "dark": 105, "yellow": 70, "root": 16, "link": 9, "rootLen": 5, "unsureFrac": 0.8 },
 "counts": { "germinated": 26, "unsure": 0, "not_germinated": 1, "misdetections": 0 },
 "seeds": [
  { "x": 0.46056, "y": 0.10833, "n": 1, "cat": "g" },
  { "x": 0.45838, "y": 0.47083, "n": 1, "cat": "n" }
 ]
}
```

| Field | Meaning |
|---|---|
| `dish.cx`, `dish.cy` | Dish center as a fraction of image width and height |
| `dish.r` | Dish radius as a fraction of image width |
| `seeds[].x`, `seeds[].y` | Seed position as a fraction of image width and height |
| `seeds[].n` | Number of seeds the marker stands for (usually 1) |
| `seeds[].cat` | `g` germinated, `u` unsure, `n` not germinated, `x` misdetection |

Marks files are plain text and can be read in Python or R for your own analysis.

---

## Troubleshooting

| Problem | What to do |
|---|---|
| "That file could not be opened as an image" | Use a JPG, PNG, or HEIC photo. Other formats (TIFF, RAW) need converting first. |
| HEIC photo will not convert | The converter downloads the first time you load a HEIC photo, so you need an internet connection. If it still fails, convert the photo to JPG (see Example 4). |
| Text, a ruler, or the dish rim is counted as seeds | Use **Adjust dish** to shrink the circle so it covers only the inside of the dish. Mark any remaining false detections as **Misdetection**. |
| Many seed coats are missed | Raise **Seed coat darkness**. Tick **Show detected pixels** to check. |
| One seedling is counted twice (coat and cotyledon separately) | Raise **Seed coat to cotyledon link**. |
| Two separate seedlings are merged into one | Lower **Seed coat to cotyledon link**. |
| Too many seeds are germinated, or too few | Adjust **Root length for germinated** to match your protocol. |
| My corrections disappeared | Changing a setting or adjusting the dish re-runs detection. Set those first, then correct. If you saved the dish, reload its marks file. |
| The results table is empty on another computer | The table is stored per browser. Export the CSV on the original computer, or reload each dish's marks file and save it again. |
| Markers are too small to tap on a phone | Use the **2×** or **3×** zoom buttons. |

---

## Hosting your own copy

The whole app is a single file, `index.html`, with no installation or server needed.

1. Create a public GitHub repository, for example `GerminationCounter`.
2. Upload `index.html` and this `README.md`.
3. In the repository, go to **Settings → Pages**, set **Source** to **Deploy from a branch**, choose `main` and `/ (root)`, and save.
4. After a minute or two, the app is live at `https://lilabatvt.github.io/GerminationCounter/`.

To update the app, upload the new `index.html` over the old one. GitHub Pages refreshes within a few minutes; if you still see the old version, reload the page.

### Privacy

Photos, marks, and results never leave your device. The only network requests the page makes are for its font and, when you load a HEIC photo, the HEIC converter library.
