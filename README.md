# Arch 1 website

The public website for Arch 1, the University of Michigan's architectural competition team. It's free to host on GitHub Pages, and anyone with the link can see it with no login.

All the content lives in three small files in the `data` folder, plus the images in the `images` folder. Officers never need to touch `index.html`.

```
index.html                  the site (don't edit)
data/competitions.json      competitions → each team's entry → its gallery images and board pages
data/members.json           board and members
data/site.json              tagline, about text, sliding words, contact info, front-page images
images/renderings/          gallery images (main renderings) — shown when you click a competition
images/boards/<competition>/  full board pages, one image per page (shown when you click a rendering)
images/members/             member portraits
```

**How the site uses them:** Clicking a competition in the Index opens its gallery of renderings, with each team's project name underneath. Clicking a rendering opens that team's full boards, page by page. The scattered images on the front page are listed in `data/site.json`.

---

## 1. Put the site online (one time)

1. Sign in at github.com, or create a free account. Using a club email for the account is best.
2. Click **+** at the top right, then **New repository**. Name it something like `arch1` and set it to **Public**. Click **Create repository**.
3. Click **uploading an existing file**. Drag in *everything* from this folder: `index.html`, `README.md`, and the `data` and `images` folders. Then click **Commit changes**.
4. Go to **Settings**, then **Pages**. Under "Branch," choose **main** and **/ (root)**, then click **Save**.
5. Wait about a minute. The site will be live at `https://YOUR-ACCOUNT.github.io/arch1/`.

To let other officers edit, go to **Settings → Collaborators → Add people**.

---

## 2. Competitions, renderings and boards

Each competition in `data/competitions.json` has a list of `groups`, one per Arch 1 team. Each group looks like this:

```json
{
  "title": "Heat House",
  "team": "Name One, Name Two, Name Three",
  "term": "Spring 2026",
  "result": "",
  "description": "Optional short paragraph.",
  "images": ["images/renderings/heat-house-1.jpg"],
  "boards": [
    "images/boards/iceland-slow-sauna/heat-house-p1.jpg",
    "images/boards/iceland-slow-sauna/heat-house-p2.jpg"
  ]
}
```

- **`images`:** The renderings shown in the competition's gallery. The first one is also used on the front page and as the Index preview.
- **`boards`:** The full board pages, in order. Use one image per page.
- **`result`:** Something like `"3rd place"`. It shows as a tag and in the Awards table.
- **`cover`:** Each competition has an optional `cover`, which picks the image used in the Index preview.

### Replace a screenshot with the real file (easiest)
The current boards and renderings are cropped from screenshots. To upgrade one:
1. Export the real board page or rendering as a **JPG**. Around 2400 px wide is plenty, and under about 3 MB is best.
2. Rename it to **exactly** the same name as the file you're replacing, for example `heat-house-p1.jpg`.
3. In GitHub, open that folder (for example `images/boards/iceland-slow-sauna/`), click **Add file → Upload files**, drop it in, and click **Commit changes**.

That's it. GitHub replaces the old file and you don't need to change any text.

### Add more pages or renderings
Upload the new files, then add their paths to that group's `boards` or `images` list. Keep a comma between items and none after the last one.

### Add a team to a competition
Upload its renderings and board pages, then copy a whole group block (`{ ... }`) in `data/competitions.json` and fill it in.

### Add a new competition
Copy a whole competition block. Change `code` (for example `M-ARCH 007`), `name` (the short name shown in the Index), `competition` (the full title), `host` and `date`, and start with `"groups": []`. The Index lists competitions in the same order as the file.

**If the site goes blank after an edit**, a missing comma or quote is almost always the cause. Paste the file into jsonlint.com to find the line.

## Front-page images
`heroImages` in `data/site.json` lists the scattered images. Each one is written like
`{"src": "images/renderings/therma-1.jpg", "competition": "M-ARCH 005"}`. Clicking it opens that competition, and hovering shows the project name. `featureImage` is the one that zooms open into the sliding words.

## 3. Add a member

1. Upload their portrait to `images/members/`. A vertical photo of about 1000 px works well; the site crops it to 4:5 and shows it in black and white.
2. Edit `data/members.json`. It starts as `[]` (empty). Add one block per person inside the brackets:

```json
[
  {
    "name": "Jane Kim",
    "role": "Principal Director",
    "group": "board",
    "order": 1,
    "major": "B.S. Architecture",
    "year": "Junior",
    "email": "uniqname@umich.edu",
    "photo": "images/members/jane-kim.jpg"
  },
  {
    "name": "Alex Park",
    "role": "Member",
    "group": "team",
    "major": "B.S. Architecture",
    "year": "Sophomore",
    "email": "uniqname@umich.edu",
    "photo": "images/members/alex-park.jpg"
  }
]
```

- **`group`:** Use `"board"` for the board of directors (sorted by `order`) and `"team"` for everyone else (sorted by name).
- **Public info:** The email shows publicly when someone clicks a portrait, so only include it if the member is okay with that.

## 4. Change the text

Edit `data/site.json` to change the tagline, the about paragraphs, the sliding words (`words`), the email, the Instagram handle, or the location.

## Color instead of black and white

The front page, Index previews and gallery are black and white (gallery images turn to color on hover), and board pages stay in full color. To make everything color, find `--bw:grayscale(1) contrast(1.05)` near the top of `index.html` and change it to `--bw:none`.

## Previewing on your own computer

Opening `index.html` by double-clicking won't load the content, because browsers block that. Look at the live GitHub Pages link instead. If you're comfortable with a terminal, you can also run `python3 -m http.server` in this folder and open `http://localhost:8000`.
