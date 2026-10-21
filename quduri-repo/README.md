# مختصر القدوري — Mukhtasar al-Quduri Reader

A static, single-page learning site for the Hanafi matn *Mukhtasar al-Quduri*
(Volume 1: Tahara, Salat, Zakat, Sawm, Hajj). Companion to the Urdu sharh
*Al-Tauzih al-Zaruri Sharh al-Quduri* (Maktaba Habibul Ummat, 2026).
No framework and no runtime dependencies. Fonts come from Google Fonts.

## Features
- 5 Kitabs → 22 parts/themes → 46 babs → 431 masa'il, each Kitab with its own colour world
- Meaning colours: rulings (wajib / sunnah / jaiz / makruh / forbidden), numbers, imams (ح ي م ز), ayat and ahadith
- Read mode and Memorize mode (cloze, 3 levels, rulings and numbers hidden first)
- Spaced-repetition review cards (Leitner: 1, 3, 7, 16, 35 days), daily goal and streak
- Auto-generated quizzes: who said it, which number, which ruling
- Progress map, bookmarks, full-text Arabic search, dark mode, font size
- Progress is stored in the browser (`localStorage`) only

## Project layout
```
data/      matn text, one file per section (see format below)
src/       app.js, style.css, plan.json (parts + one-line bab summaries)
build.py   builds docs/index.html from data + src
docs/      generated site (served by GitHub Pages)
```

## Build and run
```bash
python3 build.py          # writes docs/index.html
python3 -m http.server -d docs 8000
```

## Deploy on GitHub Pages
Push to `main`. The included workflow builds and deploys `docs/`.
In the repo: **Settings → Pages → Source: GitHub Actions**.

## Data format (`data/*.txt`)
```
@kitab N | title        starts a Kitab
@bab | title            starts a bab (titles not starting with «باب» are editorial)
~ heading               editorial section heading inside a bab
# label                 label line (e.g. «فرائض الصلاة ستة:»)
> text                  quoted ayah block
any other line          one masalah
```
In `src/plan.json`, `parts` group bab indexes (0-based, contiguous, in matn order)
and `maps` holds one summary line per bab.

## Text notes
- Source: *Mukhtasar al-Quduri* on al-Maktaba al-Shamela (book 124336).
- Obvious typos were corrected. "…" marks a gap in that edition, to be checked against print.
- Parts, bab summaries and «عنوان تنظيمي» headings are learning aids, not part of the original text.
- Ruling/number colouring is automatic by keyword; verify against the masalah itself.

## Roadmap
- Urdu sharh under each masalah (needs OCR, proofreading and publisher permission)
- Remaining Kitabs (Buyu' to Fara'id)
- Verify the "…" gaps against a printed edition

## License
Code: MIT. The matn is a classical public-domain text; the Urdu sharh is not included and remains the publisher's.
