# greater-sudbury-address-import

The **Greater Sudbury city checkout** of the address-import family — city
#11, scaffolded 2026-08-16 by the breadth-first onboarding loop (engine
`future-work/multi-city/onboarding-queue.md`). Status: **onboarding**. No
proposal published, no uploads made; the config is a first draft for
conflation baseline runs.

The pipeline lives in the engine repo,
[`address-importer-friend`](https://github.com/skfd/address-importer-friend)
(see its README for setup). This repo carries only Greater Sudbury's
`config.toml`, credentials (`.env.*`, gitignored, from the `.example`
files), and — locally, gitignored — `data/` with the OSM extract and
`data/greater-sudbury/tool.db`.

```bash
cd ../address-importer-friend
python run.py --city-dir ../greater-sudbury-address-import
```

Source data: City of Greater Sudbury addresses via the sibling
[`ontario-address-changes`](https://github.com/skfd/ontario-address-changes)
tracker (`data/greater-sudbury/greater-sudbury.db`, 70,066 active rows /
58,813 civic addresses at snapshot 63, 2026-08-16). The 2026-08-12 survey
measured 53.8% missing.

Distinctive traits (details in config comments): mixed-case long-form
streets (no title-casing needed — first since Guelph); the **status filter
is load-bearing** here, not just protective — the live layer carries 896
`Retired` rows that would otherwise conflate as MISSING;
`UNIT_OR_AMENITY` is a row-kind flag (secondary dwellings + POIs at the
parent address, no unit numbers) that collapse-to-civic handles exactly;
798 number-less named places (islands, lakes); 25 communities from the
2001 amalgamation drive both dedup keying and the tile fabric (23 census
community polygons, 99.97% point coverage). The 3,600 km² extent is the
portfolio's largest.

Entry state probed 2026-08-16 (`onboarding/entry-state-2026-08-16.json`):
**greenfield with a hand-mapped core** — `TristanA` mapped downtown Sudbury
addresses onto buildings in 2013–14 (1,176 of 1,851 sampled elements,
including postal codes), the largest manual address effort found in any
probed city; the outlying communities are thin CanVec plus Matthew Darwin's
2018 rename retag. No import tags, no wiki page, essentially quiet since.
The 53.8% gap lives in the outlying communities, not the core. TristanA is
owed the Kevo-style courtesy conversation before any changeset. Convention
warning: `addr:city` splits three ways ('Greater Sudbury' 612 / 'Sudbury'
565 / 'Chelmsford' 99) — the amalgamated-city naming question is general
after all (engine TODO §2 updated).

Before any production upload: wiki proposal page, forum announcement, and
feedback window per the
[OSM Import Guidelines](https://wiki.openstreetmap.org/wiki/Import/Guidelines)
— Toronto's [`IMPORT_PROPOSAL.mediawiki`](https://github.com/skfd/toronto-2-address-import/blob/main/IMPORT_PROPOSAL.mediawiki)
is the template.

MIT licensed.
