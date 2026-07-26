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

## Identifier durability

Three cases are already on this repository's record. None is a mistake of execution; each
is what a name-derived identifier does when the name, the type, or the editorial judgment
behind it moves.

- **The prefix already misclassifies live entries, and says so.** The scheme records that
  "the scope includes societies of apostolic life, which are canonically distinct from
  consecrated life" and that "the prefix reads as the repository's shorthand, not as a
  canonical classification of every entry". Four seeded entries prove it live — `icl:cm`,
  `icl:fdlc`, `icl:mep`, `icl:co` all carry `"type": "society_of_apostolic_life"` under an
  `icl:` prefix, and `icl:cm` is the entry this proposal prints as its worked example. A
  canonical ID needing a disclaimer to be read correctly asserts what it cannot keep.
- **A collision is settled by frozen editorial judgment.** Postnominal collisions "(rare:
  e.g. CP is used by Passionists; historical reuse exists)" are "resolved by giving the
  better-established institute the bare slug and qualifying the other from its Latin name".
  `icl:cp` is seeded to the Passionists, so the bare slug now encodes a ranking of two
  institutes — made once, unrevisable afterwards without renaming a live ID.
- **The stability rule and the slug rule contradict each other.** Rule 1 promises that
  "Identity survives reorganization" — "renames and constitutional changes keep the ID" —
  but the ID is minted *from* the name: "the institute's conventional postnominal
  abbreviation … otherwise the official Latin name, ASCII-folded, lowercase, hyphenated".
  A rename that keeps the ID leaves the identifier recording a name no longer in use. The
  seed already shows the name layer is not one language: `icl:sdb`, `icl:fdlc` and
  `icl:mep` each carry a postnominal whose letters do not correspond to the Latin name on
  the same row (`S.D.B.` against `Societas Sancti Francisci Salesii`; `F.d.l.C.` against
  `Societas Filiarum Caritatis Sancti Vincentii de Paulo`).

Each case dissolves when the canonical identifier is machine-readable and the
human-readable layer is guaranteed beside it — both, not one at the cost of the other:

```text
id:      R4hVn8sQ2yMpKd7Tb3Wr9x        # canonical, machine-readable, minted once
                                       # (illustrative value: shape only, not a minted ID)
alias:   icl:cm                        # permanent, resolvable, never reused
alias:   C.M.                          # the postnominal, kept as a resolvable key
labels:  "Congregatio Missionis"@la · "Vincentians (Lazarists)"@en
type:    society_of_apostolic_life     # an attribute, as the entry shape already records
family:  icl:familia-vincentiana       # a permanent alias of the family's canonical ID
```

Under that shape the prefix classifies nothing, because `type` is the only thing that types
an entry — "additional attributes, not identity", as the entry shape already says of finer
sub-typing; the CP collision needs no ranking, because each claimant holds a distinct
canonical ID from the moment it is seeded and both postnominals resolve as aliases; and a
rename or a union adds a label and an alias instead of stranding one, `icl:cm` and `C.M.`
resolving forever whatever the institute is called next.

The general argument — why canonical identifiers should be machine-readable, what that
costs, and how the human-readable layer is guaranteed rather than left optional — is set
out once in *Identifier Durability: Machine-Readable Canonical IRIs* (CDCF
`foundation-docs`, `research/identifier-durability-opaque-canonical-iris.md`) and is not
restated here.

## Open questions for the committee

1. Prefix coordination across the registries (`mr:` / `circ:` / `icl:`).
2. The authority list for systematic compilation: the Annuario Pontificio's indices of
   institutes of consecrated life and societies of apostolic life, and how to handle
   institutes of diocesan right (thousands; likely a second phase, possibly namespaced
   under their diocese's CECDR ID).
3. Whether family groupings should be curated top-down (a closed list) or emerge from
   the propria that actually exist.
4. Cross-references to external datasets (e.g. Wikidata) as attributes.
5. Whether the canonical ID of an institute, society or family should be machine-readable
   and minted once, with every slug this scheme produces (`icl:cm`, `icl:cp`,
   `icl:familia-vincentiana`) and every postnominal (`C.M.`, `C.P.`) kept as a permanent
   resolvable alias, and every Latin, common and vernacular name carried as a multilingual
   label — keeping this scheme intact as the human-readable layer rather than replacing it
   (see "Identifier durability").
