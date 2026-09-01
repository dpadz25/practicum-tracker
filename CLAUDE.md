# CLAUDE.md — practicum-tracker

## What this is
A single-file practicum hours tracker for Delan's MA in Clinical &
Counseling Psychology at William Paterson University (2026–2027).
Everything lives in `index.html` — vanilla HTML/CSS/JS, no build step,
opens by double-click or via the preview server.

## Program facts (verified from wpunj.edu, July 2026)
- Requirement: 600 supervised practicum hours, including 240 direct
  client contact hours, completed within 12 months (second year,
  Practicum I & II).
- Fall 2026 semester: Aug 26 – Dec 12, 2026.
- Spring 2027 semester: Jan 21 – May 12, 2027.
- Semester end dates are informational only — hours can continue past
  May 12. The hard limit shown in the app is the 12-month window starting
  from the first logged entry.

## How the app works
- Entries are time blocks: date + time in + time out + category +
  optional client initials + optional activity note. Duration is always
  computed from the two times, stored and summed in integer minutes.
- Categories are the seven columns on the WPU "Record of Supervised
  Hours" form: `direct`, `indSup` (individual supervision), `grpSup`
  (group supervision), `indirect` (admin/indirect), `training`,
  `research`, `other`. `CATEGORIES` in index.html is the single source of
  truth — the select, filter chips, table pills and totals all derive
  from it.
- Data persists in localStorage under key `practicum-tracker-v2`:
  `{ userName, siteName, entries: [{id, date, timeIn, timeOut, category,
  clientInitials, note}] }`. On first load under v2 the old
  `practicum-tracker-v1` store is migrated forward automatically (old
  `supervision` category maps to `grpSup`); v1 is left in place as a
  backup.
- Export/Import buttons download and restore a JSON backup (`version: 2`;
  version 1 files still import and get category-migrated, invalid entries
  skipped, restore replaces all data).
- UI: two SVG progress rings (600 total, 240 direct), stat cards,
  semester countdown cards, log form with inline validation and an
  overlap warning (overridable), filterable/sortable table with
  two-step delete, and a "Totals by category" bar chart under the table
  mirroring the form's per-column totals.
- No per-row edit — fixing a mistake means delete + re-add.

## Design
Follows `design-system.md` (Botanical / Organic Serif): Playfair Display
+ Source Sans 3 from Google Fonts CDN, sage/clay/stone/terracotta palette,
paper grain overlay, pill buttons, 24px rounded cards. Light mode only.

## Dev notes
- Preview server: `.claude/launch.json` runs `npx http-server` on
  port 8642 (config name `practicum-tracker`).
- Follow the general rules in `E:\dev\CLAUDE.md` (plan first, confirm
  before big changes, no em dashes, etc).
