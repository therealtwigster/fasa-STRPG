# Star Trek RPG Project — README & Handover

*A personal-use digitization and game-building project based on the FASA-era
**Star Trek: The Role Playing Game**. This document is both the README (what
everything is and how to use it) and the handover (current state, conventions,
and how to continue the work in a future session).*

Last updated: 2026-08-22  ·  Current game build: **v0.5**

---

## 1. What this project is

The owner is digitizing their own scanned FASA sourcebooks into clean text, then
building original playable material on top of them. There are three layers:

1. **Source conversion** — five scanned sourcebook PDFs turned into searchable
   OCR markdown.
2. **Original adventure content** — a solo branching gamebook set in *The
   Triangle*, written from the converted material.
3. **Playable software** — a self-contained HTML game of that adventure, plus a
   companion FASA officer character generator, now bridged so the game can
   import a character from the generator.

Everything is a personal-use conversion or original creative work derived from
the owner's own books.

---

## 2. File inventory

### Deliverables — `/mnt/user-data/outputs/`

| File | Size | What it is |
|---|---|---|
| `2002_The_Klingons_ocr.md` | 559 KB · ~90,000 words | OCR of *The Klingons* (140 pp) |
| `2008_The_Orions_ocr.md` | 543 KB · ~86,600 words | OCR of *The Orions* (132 pp) |
| `2011_The_Federation_ocr.md` | 444 KB · ~66,200 words | OCR of *The Federation* (130 pp) |
| `2007_The_Triangle_ocr.md` | 441 KB · ~70,500 words | OCR of *The Triangle* (99 pp) |
| `2005_The_Romulans_ocr.md` | 334 KB · ~53,900 words | OCR of *The Romulans* (88 pp) |
| `adventure_the_precipice_run.md` | 28 KB | "The Precipice Run" — original solo gamebook |
| `precipice_run_game.html` | ~83 KB | Playable single-file HTML game — **v0.5** (portraits, sound, dossier, customization) |
| `README.md` | — | This document |

### Project knowledge — `/mnt/project/`

Read-only copies of the five OCR files above live here alongside one extra:

| File | Size | What it is |
|---|---|---|
| `star_trek_rpg_boxset_ocr.md` | 762 KB | OCR of the core boxed set — the **format reference** for all OCR output |

### Sources — `/mnt/user-data/uploads/` (read-only)

| File | Size | Notes |
|---|---|---|
| `2002_The_Klingons.pdf` | 79 MB | Scanned image PDF (no text layer) |
| `2008_The_Orions.pdf` | 62 MB | Scanned image PDF |
| `2007_The_Triangle.pdf` | 60 MB | Scanned image PDF |
| `2011_The_Federation.pdf` | 59 MB | Scanned image PDF |
| `2005_The_Romulans.pdf` | 40 MB | Scanned image PDF |
| `star_trek_character_generator.html` | 718 KB | Owner's FASA officer generator (mostly embedded portrait JPEGs) |

---

## 3. The OCR pipeline (reproduce this for any new book)

Every source PDF is a **scanned image PDF with no text layer**, so real OCR is
required. The established, repeatable pipeline — used identically for all five
books — is:

1. **Diagnose.** `pdfinfo` for page count; `pdffonts` to confirm no embedded
   fonts (i.e. it's scanned, not text).
2. **Rasterize** each page to 300 DPI grayscale:
   `pdftoppm -gray -r 300 -f N -l N "<pdf>" /tmp/ocr/pg`
3. **OCR** each page with Tesseract 5.3.4 (eng), `--psm 3`. The container has a
   **single CPU**, so run in **small synchronous batches** — background `nohup`
   jobs did **not** persist, and one 30-page batch hit the bash time limit
   (~page 121) and had to be resumed. Delete each `.pgm` after OCR to save space.
4. **Assemble** into markdown with a Python pass, matching the boxset format
   exactly:
   - Top title: `# Star Trek: The Role Playing Game — <Book> (<year> scan)`
   - An italic OCR-caveat line, then `---`
   - Per page: `<!-- PDF page N -->`, then `## Page N`, then cleaned text
     (rstrip lines, trim leading/trailing blanks, collapse 3+ blank lines to 2).
   - Missing/failed page → `*[OCR unavailable for this page]*`
5. **Verify.** Spot-check, list "sparse pages" (<15 words — usually art plates),
   confirm zero hard failures, copy to `/mnt/user-data/outputs/`, and present.

**Naming convention:** `<year>_<Book>_ocr.md`.

Sparse-page notes already recorded, in case they're useful for re-scans:
Klingons 1,54,55,56,131 · Federation 1,2,5,7,19,127 · Romulans 1,3,36,37,47,86,87 ·
Orions 1,41,121 · Triangle 1,2.

---

## 4. The gamebook — "The Precipice Run"

`adventure_the_precipice_run.md` is an original solo choose-your-own-adventure
set in **The Triangle**. You captain the free trader *Verity's Gambit* and take a
job smuggling a cryo-container holding a defecting Romulan subcommander, S'Tal,
who carries Neutral Zone keys and cloaking-flaw intel. Play tracks Latinum, four
faction Standings, and Tokens, with six endings gated by which tokens you earned.
It is grounded in details greped from the converted books (the Affiliation of
Outer Free Worlds, Baker's World, the Imperial Klingon States, the D-10 cruiser,
worlds such as Haven / Precipice / Cyclopus / Eternity, the Orion Frontier
Mercantile Association, and more).

---

## 5. The playable game — `precipice_run_game.html`

A **single self-contained HTML file** — vanilla JavaScript, no build step, no
external calls. Open it in any browser and it runs offline.

### Aesthetic
An original amber-CRT "smuggler's console" look (scanlines, phosphor glow) using
only offline-safe fonts. It deliberately avoids trademarked LCARS styling in this
newly-authored asset.

### What it does
- **Character creation, two on-ramps:**
  - *Roll in-game* — seven FASA races (Human, Vulcan, Andorian, Tellarite,
    Klingon, Romulan, Orion), each with attribute mods and a signature trait,
    and a six-attribute set (STR/END/INT/DEX/CHA/LUC) rolled 2d6+3 (range 5–15)
    with two re-rolls.
  - *Import an officer* — paste a sheet from the companion generator (see §6).
- **Portraits with customization** (v0.5): every captain gets an in-code SVG
  portrait — pick **presentation**, **expression**, and **eyebrow shape** in the
  creator, with a live preview; it also appears as the HUD avatar. Six named NPCs
  have their own portraits and fitting expressions.
- **Dice checks** shown live in an overlay: best applicable attribute + trait
  bonus + 1d10 vs a target number. (The beloved on-screen roll animation is
  unchanged — sound was layered on top, not swapped in.)
- **Sound** (v0.3) via the Web Audio API, fully offline (no files): disruptor and
  photon-torpedo fire, an evade *whoosh*, a combat klaxon, impact hits, verdict
  chimes, and dice ticks — with a persistent 🔊/🔇 toggle top-right.
- **Ship dossier** (v0.2) in FASA *Combat Simulator* format for both hulls, from
  the title screen or the HUD **REGISTRY** link; `SHIP_SPRITES` (v0.4) lets real
  bitmap sprites drop in over the SVG silhouettes.
- **A Klingon D-10 ship-combat encounter** (fire / evade / target-tractor /
  surrender) — near-unwinnable by canon, with crippled → surrender/ram branches,
  now with ship silhouettes and combat audio.
- **35 story nodes** including the v0.3 additions — a *Before You Burn* pre-flight
  (with priced options, v0.4), a *Silent Skiff* derelict encounter, and a
  *Precipice customs* approach — leading to **seven ending states** (`end_wage`,
  `end_thirty`, `end_quiet`, `end_free`, `end_warlord`, `end_marked`, and the
  `end_grounded` fail state).
- **Save / load** via a base64 code — **no `localStorage`** (browser storage is
  intentionally avoided; state is in memory + copyable code).
- A persistent HUD tracking Latinum, Standings, attributes, hull, tokens, and the
  captain's avatar.

### Architecture (for future edits)
- Story lives in a `NODES` object (`p1`…`p28` plus the ending nodes).
  `combat_d10` is handled in code, not in `NODES`; `renderNode()` resolves it
  before its missing-node guard so mid-combat saves resume correctly.
- `newState()` holds the run: captain/ship/race/attrs/latinum/stand{k,f,r,o}/
  tokens/hull/pay/contract/freeReroll/romulanKin/node/combat, plus the newer
  `psi` and `imported` fields.
- `traitBonus(s, tag, attrUsed)` grants per-race bonuses in checks.
- `renderHUD` builds the attribute grid from `ATTRS` (six) and a tokens row.
- Title screen buttons call `startCreate()`, `showImport()`, and `showLoad()`.

### Validation done
Headless Node + a DOM-stub harness: `node --check` passes; a graph walk reports
**35 nodes**, all seven endings reachable, zero dead links, correct race
start-bonuses, and no bad art references; a closure sim runs every node/check
effect against live state; and all **720** portrait combinations (race ×
presentation × expression × eyebrow) render as well-formed SVG. The importer was
tested against realistically-pasted sheets (see §6).

---

## 6. The character generator and the import bridge

### The generator (`star_trek_character_generator.html`) — the owner's own file
A faithful FASA **core-rulebook Star Fleet officer** creator ("Star Fleet
Personnel File"). Its model is different from the game's:
- **Seven attributes on the percentile (1–100) scale:** STR, END, INT, DEX, CHA,
  LUC, and **PSI**. STR/END/INT/DEX/CHA roll 3D10+40; LUC/PSI roll d100; then
  racial mods and a bonus pool apply.
- **Six Federation-member species:** Human, Vulcan, Andorian, Caitian, Edoan,
  Tellarite (no Klingon/Romulan/Orion — it builds a Star Fleet officer).
- Full flow: portrait → name → species → department → generate, producing a
  **ranked officer** (Ensign→Captain) with Academy skills, a Cadet Cruise
  assignment, and a service log. Most of the 718 KB is embedded portrait JPEGs.

### The bridge (chosen approach: keep the two tools separate)
Only **the game file was modified** — the generator is untouched, so there was no
need to re-emit its large payload. The game now **accepts a pasted stat block**:

- The title screen's **"Import an officer from a Personnel File"** opens a paste
  box → **Read stat block**.
- A tolerant parser scrapes the seven attributes (`STR 78 roll 38+20 …` and
  looser `str:66` forms both work), detects the species, and reads a `Name:`
  line if present. Text with no stats is rejected with a helpful message.
- **Percentile → game scale** conversion (`convertPct`): roughly 40→6, 55→9,
  70→11, 85→14, 99→16, clamped to 4–17. This keeps the existing checks, combat,
  and endings balanced without re-tuning them. The preview shows both numbers.
- **PSI is carried as flavor only** — shown on the preview and as a HUD chip, but
  no check uses it.
- **Species traits fire**, including the two the generator has that the game
  originally lacked: **Caitian** → +2 piloting/evade, **Edoan** → +2 tech/logic.
  Human still gets its free re-roll.
- **Frame:** the imported officer takes the *Verity's Gambit* on detached,
  independent duty — an in-universe reason a trained officer is out in the
  Triangle.

**Known limitation:** the generator prints the character name as a heading, not
as a `Name:` line, so the parser usually can't capture it — which is why the
import screen has an **editable Captain's name field** (pre-filled when
detectable, yours to set otherwise).

### How to use the two together
1. Open `star_trek_character_generator.html`, roll an officer, and copy the
   finished sheet text.
2. Open `precipice_run_game.html` → **Import an officer** → paste → **Read stat
   block** → confirm the name → **Take the helm**.

---

## 7. Conventions & constraints (read before continuing)

- **Reuse the OCR format exactly** for any further books; name outputs
  `<year>_<Book>_ocr.md`. The boxset file is the format reference.
- **Environment:** single CPU. Run OCR in **small synchronous batches** — avoid
  the bash time limit, and note background jobs don't persist.
- **No browser storage** in HTML/artifacts. Use in-memory state plus base64 save
  codes. (The game already follows this.)
- **Keep original sci-fi styling; avoid trademarked LCARS** in newly-authored
  assets. The owner's own generator is exempt — it's their file.
- **Scope big builds honestly and confirm forks before starting.** The import
  work offered three options (full bridge / lighter reskin / keep separate); the
  owner chose *keep separate*, which is what shipped.
- **Track versions.** First build is v0.1; +0.1 per iteration. Bump
  `GAME_VERSION` (title-screen stamp) and add a row to §0 on every change.
- **All work is personal-use** conversion or original creation from the owner's
  own scanned FASA books.

---

## 0. Version history

Versioning convention: the first build is **v0.1**; every subsequent iteration
increments by **0.1**. Bump `GAME_VERSION` at the top of the game's `<script>`
(it renders as a *Build vX.Y* stamp on the title screen) whenever you ship a
change, and add a row here.

| Version | Change |
|---|---|
| **v0.1** | Original build. Core engine: seven FASA races, six attributes rolled 2d6+3, the live on-screen **dice-roll overlay**, four faction standings, tokens, 28 story nodes, six endings plus a `grounded` fail state, the Klingon **D-10 ship-combat** encounter, base64 save codes, and the paste-in **officer-import bridge**. |
| **v0.2** | **Ship dossier** in FASA *Starship Combat Simulator* format, with canonical stats grounded in the OCR — *Verity's Gambit* modelled as a Lightning-Class IV blockade-runner variant, the *IKS Devastator* as a D-10 (Riskadh) Class VIII–X cruiser. Reachable from the title and a HUD **REGISTRY** link. |
| **v0.3** | **SVG character portraits** (player + six NPCs, drawn in-code, offline, no trademarked art); a **Web Audio sound suite** — disruptor / photon-torpedo / evade-*whoosh* / klaxon / impact / verdict chimes, plus dice ticks — with a persistent mute toggle, **preserving the original dice-roll effects**; and **five new branch nodes** (28 → 35): the *Before You Burn* pre-flight, the *Silent Skiff* derelict encounter, and the *Precipice customs* approach. |
| **v0.4** | **Cost transparency** in *Before You Burn* — live latinum count, an explicit price on every paid option, and purchase-status flags — plus a drop-in **bitmap ship-sprite hook** (`SHIP_SPRITES`, with the SVG silhouettes as fallback) for art parity with the separate *Tactical Command* Combat-Simulator project. |
| **v0.5** | **Portrait customization** in the creator: **presentation** (masculine / feminine / neutral), **expression** (neutral / smiling / stern / frown), and **eyebrow shape** (auto / flat / arched / angled / heavy / worried), with a live preview; per-NPC expressions so characters read at a glance; and the **Build vX.Y** version stamp on the title. |

*(v0.2 and v0.3 were developed in one working session but are distinct feature
sets, so they're logged as separate versions. It's your scheme — renumber freely.)*

---

## 8. Handover — current status & next steps

### Status: complete and validated (game at v0.5)
- All five sourcebooks OCR'd, verified, and delivered.
- Gamebook written and delivered.
- Playable game built, graph-validated, and shipped; augmented through v0.5
  (dossier, portraits, sound, five new nodes, cost transparency, sprite hook,
  portrait customization). See §0 for the per-version log.
- Generator inspected; import bridge built into the game and tested end to end.

### Possible next steps (none in progress)
- **More books.** Any additional scanned sourcebook can go through the §3
  pipeline unchanged.
- **Add Klingon/Romulan/Orion to the generator.** If desired, authentic FASA
  percentile modifiers for those species can be pulled from the already-OCR'd
  Klingons / Romulans / Orions files and added to the generator's `RACES` array,
  so imported officers can be those species too.
- **Name capture.** If cleaner name import is wanted, the simplest fix is a small
  "Export stat block" button in the generator that emits a labelled line
  (including `Name:`); the game's parser already reads that field.
- **Deeper mechanical fidelity.** If ever desired, the game's checks could be
  switched to authentic FASA roll-under-d100 for imported officers (this was the
  "full bridge" option, not taken) — a larger change that would re-tune balance.

### Quick reference for a future session
- Deliverables are in `/mnt/user-data/outputs/`; project copies and the boxset
  format reference are in `/mnt/project/`; source PDFs and the generator are in
  `/mnt/user-data/uploads/` (read-only).
- To validate the game after edits: extract the `<script>`, run `node --check`,
  and re-run the DOM-stub graph walk / importer harness.

*Qapla'.*
