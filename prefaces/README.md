# PGN — Front matter (prefaces)

OCR + translation of the **front matter** (title pages, dedication, foreword, table of contents, and author's preface) of:

> **Sharma, Tej Ram.** *Personal and Geographical Names in the Gupta Inscriptions.* Delhi: Concept Publishing Company, 1978. (xxvi, 378 p.) Originally the author's doctoral thesis, Banaras Hindu University, 1968.

This is the **PGN** source of the Cologne Digital Sanskrit Lexicon (CDSL) — a *koṣa*-style index of personal and geographical names drawn from the Gupta inscriptions, not a conventional alphabetical dictionary. CDSL editors: Jim Funderburk, Thomas Malten, Peter M. Scharf.

- **Source language:** English (with embedded Sanskrit in IAST). Therefore the per-page base `.md` files **are** the English edition; there are no separate `.en.md` files. Russian translations are provided as `.ru.md`.
- **Cologne scan source:** [pgnpref.html](https://sanskrit-lexicon.uni-koeln.de/scans/csldev/csldoc/build/dictionaries/prefaces/pgnpref.html) (10 scans, `_images/pgn_Page_0NN_Image_0002.png`).
- Digitizer running-header / footer stamps were omitted (they are added to every scan and are not part of the original).

## File conventions

| Suffix | Meaning |
|---|---|
| `pgnprefNN.md` | Faithful transcription of scan page NN (English source). |
| `pgnprefNN.ru.md` | Russian translation of page NN. |
| `pgnpref_all.en.md` | All pages in order, English (source), with table of contents. |
| `pgnpref_all.ru.md` | All pages in order, Russian, with table of contents. |
| `build_combined.py` | Reproducible builder for the `pgnpref_all.*` files (reads each page's YAML; `DICT=pgn python build_combined.py`). |
| `scans/` | The 10 native Cologne PNG scans. |

## Consolidated editions

| Edition | File |
|---|---|
| English (source) | [pgnpref_all.en.md](pgnpref_all.en.md) |
| Русский | [pgnpref_all.ru.md](pgnpref_all.ru.md) |
| Builder | [build_combined.py](build_combined.py) |

## Contents

| NN | Section | Vol. | Source | EN | RU |
|---|---|---|---|---|---|
| 01 | Title | 1 | [scan](scans/pgn_Page_007_Image_0002.png) | [en](pgnpref01.md) | [ru](pgnpref01.ru.md) |
| 02 | Dedication | 1 | [scan](scans/pgn_Page_009_Image_0002.png) | [en](pgnpref02.md) | [ru](pgnpref02.ru.md) |
| 03 | Foreword, 1 | 1 | [scan](scans/pgn_Page_011_Image_0002.png) | [en](pgnpref03.md) | [ru](pgnpref03.ru.md) |
| 04 | Foreword, 2 | 1 | [scan](scans/pgn_Page_012_Image_0002.png) | [en](pgnpref04.md) | [ru](pgnpref04.ru.md) |
| 05 | Foreword, 3 | 1 | [scan](scans/pgn_Page_013_Image_0002.png) | [en](pgnpref05.md) | [ru](pgnpref05.ru.md) |
| 06 | Contents, 1 | 1 | [scan](scans/pgn_Page_014_Image_0002.png) | [en](pgnpref06.md) | [ru](pgnpref06.ru.md) |
| 07 | Contents, 2 | 1 | [scan](scans/pgn_Page_015_Image_0002.png) | [en](pgnpref07.md) | [ru](pgnpref07.ru.md) |
| 08 | Preface, 1 *(= Contents tail)* | 1 | [scan](scans/pgn_Page_016_Image_0002.png) | [en](pgnpref08.md) | [ru](pgnpref08.ru.md) |
| 09 | Preface, 2 | 1 | [scan](scans/pgn_Page_017_Image_0002.png) | [en](pgnpref09.md) | [ru](pgnpref09.ru.md) |
| 10 | Preface, 3 | 1 | [scan](scans/pgn_Page_018_Image_0002.png) | [en](pgnpref10.md) | [ru](pgnpref10.ru.md) |

## Signatures, dates & notes found

- **Foreword** signed **Lallanji Gopal**, *Banaras Hindu University, VARANASI, U.P.* (no date printed).
- **Preface** by the author Tej Ram Sharma; references J. F. Fleet's *Corpus Inscriptionum Indicarum*, Vol. III as the inscription-ordering source; the study was accepted as a doctoral thesis by Banaras Hindu University in **1968**.
- Sanskrit dictum quoted in the Preface: *yathā nāma tathā guṇaḥ*.
- The toctree labels page 08 "Preface, 1", but the scan in fact shows the **tail of the Contents** (Appendices + Maps and Plates) — flagged in [pgnpref08.md](pgnpref08.md).
- **Page 06 (Contents, 1)** scan `pgn_Page_014_Image_0002.png` is a near-blank, very low-ink capture (~8 KB) — only a faint running head and 2–3 indistinct rows survive; it is marked `[illegible]`. The **full** table of contents is legibly present on page 07.

<details>
<summary><strong>OCR run notes (2026-06-22)</strong> — cost, timing, and technical lessons</summary>

Produced by the `/cologne-preface-ocr` skill (synchronous, no subagents — per `.preface_retry_rules.md`). Process retrospective, not part of the deliverable.

**Cost.** Single main thread, no subagents. ~10 scans downloaded one-at-a-time; ~30 native-resolution crop reads (3 bands × dense pages + contrast-enhanced retries for page 06) + 20 page/translation writes + the consolidated build. Estimated **≈0.4–0.5 M tokens** total.

**Time.** Wall-clock ≈ a few minutes; gated by sequential foreground `curl` (1 s sleeps) and per-page crop→read loop.

**Technical lessons (reusable):**
1. PGN csldoc scans are **low-resolution** (~824×1347 px, already ≤1900 px) — no full-page-downsample trap, but several are low-ink. Page 06 (`Page_014`, ~8 KB) is effectively blank; `ImageOps.autocontrast` + point-threshold did not recover it → marked `[illegible]`. The complete TOC is on page 07, so no content was lost.
2. Source is **English**, so base `.md` = the English edition; only `.ru.md` translations were produced (`.en.md` skipped, per skill rule).
3. Toctree label ≠ content for page 08: labeled "Preface, 1" but is the Contents tail (Appendices / Maps & Plates). Trust the scan, annotate the mismatch.
4. The digitized `pgn.txt` (csl-orig) was a useful cross-check for the Foreword/Preface prose but the scans were the OCR authority.

</details>

---

> **Home-repo flag:** PGN has **no local dictionary repo** cloned under `GitHub/` (only the data lives in `csl-orig/v02/pgn/`). This `prefaces/` work currently sits in the standalone working dir `GitHub/prefaces_pgn/` and is **not committed anywhere** — it needs a home-repo decision (e.g. a new `sanskrit-lexicon/PGN` repo, or fold into `csl-orig`/another container). No commit/push was performed.
