# Audio sources (PRD §5.6, CLAUDE.md §5.4)

## Recorded: none yet

- **Planned:** Dasar's minimal and stress pairs and sound words, every Tirukan sentence, and the
  España rows: 77 clips for the live rungs (`npm run audio:list`). Latin American lines by a speaker
  of neutral Mexico City Spanish; España rows (`variety: es`) by a speaker from Spain.
- **Source:** not chosen (docs/spanish/human-tasks.md H2). Either commissioned speakers, or an
  existing set **only if** its licence allows trimming and redistribution in a free public app.
  Record the speakers, the licence and the date here when chosen.
- **Until then:** everything plays with the browser's Spanish voice: es-MX, then es-US, es-419 and
  other es-* for Latin American lines; es-ES for Spain lines and when the learner picks "Spanyol"
  (natural voices preferred, novelty voices avoided, the gender setting respected). Unlike the kana
  in Japanese Ladder, Spanish words and pairs may fall back to the browser voice.

## Keys

`sha1(normEs(text) + '|' + variety)`, first 12 hex digits (core `audioKey`): `latam` for Latin
American lines, `es` for Spain lines. A recording plays wherever the same text appears.

## Workflow

1. `npm run audio:list -- --all > to-record.csv` lists what to record; the `file` column is the name
   to save each recording under.
2. Put the files in `apps/spanish/recordings/` and run `npm run audio:ingest` (needs ffmpeg). It trims
   silence, normalises loudness to −16 LUFS, writes mono 48 kbps MP3 named by content hash, and updates
   `manifest.json`. The service worker caches clips on first play.
