# CICLSALDR

The home of the **Common Institutes of Consecrated Life and Societies of Apostolic Life Data Repository**, curated by the **Catholic Engineering Task Force** of the [Catholic Digital Commons Foundation](https://github.com/CatholicOS).

## What is CICLSALDR?

The Common Institutes of Consecrated Life and Societies of Apostolic Life Data Repository (CICLSALDR) provides a canonicalized list of identifiers for the institutes of consecrated life and the societies of apostolic life of the Catholic Church — religious orders, religious congregations, monastic orders, secular institutes, and societies of apostolic life — together with the family-level groupings (the *religious families*) that several institutes may share.

The name deliberately follows the canonical umbrella used by the Holy See itself (the Dicastery for Institutes of Consecrated Life and Societies of Apostolic Life): "consecrated life" alone would exclude the societies of apostolic life — Vincentians, Sulpicians, Oratorians and the like — whose members do not necessarily profess the evangelical counsels by vow (can. 731), yet who certainly hold proper liturgical calendars and proper martyrologies.

## Why?

Canonical institute identifiers are needed wherever Catholic data references a religious institute:

- **religious-family proper eulogies** of the Roman Martyrology (*Proprium Martyrologii seu Appendix Martyrologii*, Praenotanda n. 38 as amended by the decree *Postquam Summus Pontifex*, 2021), which the [CRMEDR](https://github.com/CatholicOS/crmedr) plans to namespace by owner — n. 38's own term for these owners is *familiæ religiosæ*;
- proper liturgical calendars of religious institutes;
- attribution of saints, blesseds, clergy and institutions to their institutes in any dataset.

Praenotanda n. 38 attaches propria at the level of the *family* — one Franciscan martyrology can serve the Friars Minor, Capuchins, Conventuals and Poor Clares alike — so the registry models both individual institutes and family groupings, and a proprium may be owned by either.

## The identifier scheme (draft)

```
icl:<slug>                e.g. icl:osb, icl:ofmcap, icl:cm
icl:familia-<slug>        e.g. icl:familia-franciscana
```

Where an institute has a conventional postnominal abbreviation (OSB, OP, SJ, CM…) the slug is its lowercase form; otherwise the slug derives from the official Latin name. The full proposal is in [docs/schema-proposal.md](docs/schema-proposal.md). **All IDs are drafts pending committee review.**

## Repository contents

- [`data/institutes.json`](data/institutes.json) — an **illustrative** seed of well-known institutes, societies and families, demonstrating the entry shape; the systematic compilation (from the Annuario Pontificio's lists) is future work.
- [`docs/schema-proposal.md`](docs/schema-proposal.md) — the proposed schema and the open questions for the committee.
