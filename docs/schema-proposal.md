# CICLSALDR schema proposal (draft for committee review)

## Identifier scheme

```
icl:<slug>
icl:familia-<slug>
```

- **`icl:`** — namespace prefix (placeholder pending committee decision; note that the
  scope includes societies of apostolic life, which are canonically distinct from
  consecrated life — the prefix reads as the repository's shorthand, not as a canonical
  classification of every entry).
- **`<slug>`** — the institute's conventional postnominal abbreviation, lowercase, where
  one exists and is unambiguous (`osb`, `op`, `ofm`, `ofmcap`, `sj`, `cm`, `cssr`);
  otherwise the official Latin name, ASCII-folded, lowercase, hyphenated. Postnominals
  are the de facto canonical keys of this domain — stable for centuries, used by the
  Annuario Pontificio — so they serve as slugs directly.
- **`familia-<slug>`** — family-level groupings (the *familiæ religiosæ* of
  Martyrologium Romanum Praenotanda n. 38): `icl:familia-franciscana`,
  `icl:familia-vincentiana`. A proprium (martyrology or calendar) may be owned by a
  family or by a single institute; member institutes reference their family via the
  `family` attribute.

### Rules

1. **Identity survives reorganization**: renames and constitutional changes keep the
   ID; a union of institutes produces a new ID with predecessors kept as suppressed
   entries pointing to the successor (as in the CECDR).
2. **Branches are distinct entries**: OFM, OFMCap and OFMConv are three institutes,
   related through `family: icl:familia-franciscana`; likewise male/female/secular
   branches (First, Second, Third Orders) are distinct entries within a family.
3. **Postnominal collisions** (rare: e.g. CP is used by Passionists; historical reuse
   exists) are resolved by giving the better-established institute the bare slug and
   qualifying the other from its Latin name, mirroring the CRMEDR collision rules.

## Entry shape

```json
{
  "id": "icl:cm",
  "postnominal": "C.M.",
  "latin_name": "Congregatio Missionis",
  "common_name": "Vincentians (Lazarists)",
  "type": "society_of_apostolic_life",
  "family": "icl:familia-vincentiana"
}
```

`type` is one of: `religious_institute` (orders and congregations, monastic and
apostolic), `secular_institute`, `society_of_apostolic_life`, `family`. Finer
sub-typing (monastic / mendicant / clerks regular / congregation; pontifical vs
diocesan right) is planned as additional attributes, not identity.

## Open questions for the committee

1. Prefix coordination across the registries (`mr:` / `circ:` / `icl:`).
2. The authority list for systematic compilation: the Annuario Pontificio's indices of
   institutes of consecrated life and societies of apostolic life, and how to handle
   institutes of diocesan right (thousands; likely a second phase, possibly namespaced
   under their diocese's CECDR ID).
3. Whether family groupings should be curated top-down (a closed list) or emerge from
   the propria that actually exist.
4. Cross-references to external datasets (e.g. Wikidata) as attributes.
