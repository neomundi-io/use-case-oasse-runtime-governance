# OASSE × NeoMundi

**Runtime governance signaling and downstream policy enforcement — interoperability pilot.**

[🇫🇷 Lire en français](#version-française)

---

# English

## What happened here?

A controlled benchmark of **60 runtime calls** was executed through the NeoMundi × OASSE integration.

NeoMundi produced runtime governance signals in `OBS` wire mode. OASSE independently applied its own FAM policy. Gatekeeper then composed both layers into operational actions.

All **60 calls completed successfully**, all **60 Gatekeeper artifacts were sealed**, and all **60 NeoMundi trace IDs were reconciled one-to-one with the supplied NeoMundi audit export**.

### What this shows

This pilot provides evidence that:

- a third-party governance infrastructure can consume NeoMundi runtime signals;
- NeoMundi does not need to replace the partner's local policy engine;
- a local policy can remain authoritative while consuming an independent runtime measurement layer;
- NeoMundi signals and local verdicts can be deterministically composed into downstream operational actions;
- traceability and evidence integrity can be preserved across both infrastructures.

**In simple terms: NeoMundi measures and signals. OASSE applies its own policy. Gatekeeper composes the operational action.**

This is a completed focused interoperability benchmark. It is not, by itself, a claim of production readiness or universal interoperability.

---

## Overview

This repository documents the **NeoMundi × OASSE 60-Pull Focused Benchmark**, executed on **4 August 2026**.

The experiment tested a complete runtime governance path in which NeoMundi supplied an independent runtime signal while OASSE retained its own policy and enforcement authority.

Reference run:

`run-d86e7abe7d55`

## Architecture

    Controlled case
          ↓
    Runner / integration bridge
          ↓
          ├───────────────┐
          ↓               ↓
    NeoMundi OBS       OASSE FAM
    runtime signal     local policy verdict
          ↓               ↓
          └───────┬───────┘
                  ↓
              Gatekeeper
                  ↓
        PROCEED / HOLD / DENY
                  ↓
          sealed artifact
                  ↓
        trace reconciliation

NeoMundi and OASSE therefore perform different functions.

**NeoMundi measures and reports runtime behavior.**

**OASSE FAM applies the partner's local policy.**

**Gatekeeper composes the two layers into an operational action.**

## Benchmark

- **Partner infrastructure:** OASSE / Oak & Sparrow Systems
- **Measurement layer:** NeoMundi ControlTower
- **Benchmark:** 60-Pull Focused Governance Benchmark
- **Reference run:** `run-d86e7abe7d55`
- **Cases attempted:** 60
- **Cases completed:** 60
- **Gatekeeper artifacts sealed:** 60
- **Technical failures:** 0
- **NeoMundi wire mode:** `OBS`
- **Internal OASSE benchmark designation:** `GOV`

The distinction between `OBS` and `GOV` is important:

- `OBS` is the authoritative NeoMundi wire-level mode used during the run;
- `GOV` is OASSE's internal designation for the governance-path benchmark.

## Results

### NeoMundi runtime signals

| Outcome | Count | Share |
|---|---:|---:|
| `ALLOW` | 58 | 96.67% |
| `FLAG` | 2 | 3.33% |

### OASSE FAM local verdicts

| Outcome | Count | Share |
|---|---:|---:|
| `ALLOW` | 50 | 83.33% |
| `BLOCK` | 10 | 16.67% |

### Gatekeeper final actions

| Action | Count | Share |
|---|---:|---:|
| `PROCEED` | 48 | 80.00% |
| `DENY` | 10 | 16.67% |
| `HOLD` | 2 | 3.33% |

These distributions come from a deliberately controlled benchmark pack and must not be interpreted as production incident rates.

## Decision composition

The observed composition matrix was:

| OASSE FAM verdict | NeoMundi signal | Gatekeeper action | Count |
|---|---|---|---:|
| `BLOCK` | `ALLOW` | `DENY` | 10 |
| `ALLOW` | `FLAG` | `HOLD` | 2 |
| `ALLOW` | `ALLOW` | `PROCEED` | 48 |

This demonstrates both directions of authority preservation:

- a NeoMundi `ALLOW` does **not** override an OASSE `BLOCK`;
- a NeoMundi `FLAG` can transform an otherwise admissible operation into `HOLD`.

The final operational action is therefore produced by the partner-side composition layer, not by NeoMundi alone.

## Traceability and evidence integrity

The focused benchmark recorded:

- 60 / 60 successful result rows;
- complete ordinals from 1 through 60;
- complete artifact sequences from 1 through 60;
- a continuous outer previous-hash chain;
- FAM previous-hash fields consistent with the enclosing Gatekeeper chain;
- unique NeoMundi trace IDs;
- unique source-response hashes;
- 60 / 60 NeoMundi trace IDs reconciled against the audit export;
- matching audit decisions and sealed facts;
- matching G-Scores between audit records and sealed facts;
- stable bridge implementation digest;
- stable measurement version;
- stable runner version.

The evidence package therefore supports re-validation of the focused run from both the OASSE result set and the NeoMundi audit export.

## Runtime score summary

Observed NeoMundi scores across the 60 sealed responses:

| Score | Mean | Median | P95 | Minimum | Maximum |
|---|---:|---:|---:|---:|---:|
| G-Score | 0.5933 | 0.6000 | 0.6000 | 0.4000 | 0.6000 |
| G-Final | 0.9852 | 0.9885 | 0.9885 | 0.8898 | 0.9885 |
| V-Score | 0.9667 | 1.0000 | 1.0000 | 0.0000 | 1.0000 |
| Stability | 0.9128 | 0.9231 | 0.9231 | 0.6154 | 0.9231 |

These values are runtime measurements associated with this benchmark. They are not universal verdicts or production incident rates.

## Timing

Observed timing for the successful path:

| Metric | Mean | Median | P95 | P99 | Maximum |
|---|---:|---:|---:|---:|---:|
| Full pipeline | 20.336 s | 20.325 s | 20.393 s | 20.563 s | 20.798 s |
| NeoMundi processing | 20024.02 ms | 20024.54 ms | 20031.75 ms | 20033.56 ms | 20033.60 ms |
| OASSE + transport residual | 311.74 ms | 299.72 ms | 366.73 ms | 539.07 ms | 776.39 ms |

The measured window lasted **20.34 minutes**, corresponding to an effective throughput of **177.01 sealed artifacts per hour**.

The OASSE + transport value is a residual measurement. It may include network transit, serialization, bridge normalization, policy evaluation, sealing, persistence and client overhead.

## Responsibility separation

| Layer | Responsibility |
|---|---|
| NeoMundi | Runtime measurement, scoring, signaling and audit trace |
| OASSE FAM | Independent local policy evaluation |
| Gatekeeper | Deterministic composition and operational action |
| Partner environment | Final operational authority and execution |

The core architectural rule is:

> **NeoMundi does not replace the business or operational authority of the integrated system. NeoMundi provides an independent runtime measurement and signaling layer consumable by that authority.**

## What this pilot establishes — and does not establish

### It establishes, within this benchmark

- successful end-to-end execution of the focused 60-call pipeline;
- consumption of NeoMundi runtime signals by OASSE;
- preservation of independent local policy authority;
- deterministic cross-layer decision composition;
- one-to-one trace reconciliation with NeoMundi audit records;
- continuity and integrity of the sealed evidence chain;
- stable bridge, runner and measurement versions across the focused run.

### It does not establish

- production readiness on its own;
- universal interoperability across all third-party systems;
- universal policy semantics;
- universal performance or incident rates;
- legal or regulatory compliance;
- native NeoMundi enforcement of `PROCEED`, `HOLD` or `DENY`;
- production-scale resilience, security, SLA or continuous monitoring.

## Interpretation boundary

NeoMundi operated in `OBS` mode throughout the benchmark.

OASSE applied downstream enforcement through its own policy and Gatekeeper layers.

The benchmark therefore demonstrates **runtime governance signaling with downstream partner enforcement**, not native NeoMundi enforcement.

## Repository purpose

This repository is intended to make the interoperability pilot inspectable and citable.

It should preserve the distinction between:

1. runtime measurement;
2. local policy interpretation;
3. operational enforcement;
4. evidence and audit.

The repository does not need to expose NeoMundi's proprietary internal measurement mechanisms in order to document the observed interoperability.

## Supporting report

The benchmark report documents:

- execution results;
- timing;
- governance outcomes;
- cross-gate composition;
- NeoMundi score summaries;
- evidence integrity;
- trace reconciliation;
- source manifest;
- reproducibility boundaries.

## NeoMundi resources

- [NeoMundi Research](https://neomundi.org)
- [ControlTower](https://controltower.neomundi.io/welcome)
- [Runtime Interoperability Contract](https://github.com/neomundi-io/runtime-interoperability-contract)
- [NeoMundi AI Observatory](https://github.com/neomundi-io/neomundi-ai-observatory)

## Status

**Focused interoperability benchmark completed and technically validated for the pilot phase.**

The run demonstrates that OASSE can preserve independent policy and operational authority while consuming NeoMundi runtime signals through a traceable and auditable integration.

Further validation is required before any broader claim of production readiness or universal interoperability.

---

# Version française

[🇬🇧 Back to English](#english)

## Qu’est-ce qui a été fait ici ?

Un benchmark contrôlé de **60 appels runtime** a été exécuté au travers de l’intégration NeoMundi × OASSE.

NeoMundi a produit des signaux de gouvernance runtime en mode wire `OBS`. OASSE a appliqué indépendamment sa propre politique FAM. Gatekeeper a ensuite composé les deux couches pour produire des actions opérationnelles.

Les **60 appels ont été exécutés avec succès**, les **60 artefacts Gatekeeper ont été scellés**, et les **60 identifiants de trace NeoMundi ont été réconciliés un à un avec l’export d’audit NeoMundi fourni**.

### Ce que cela montre

Ce pilote apporte des éléments montrant que :

- une infrastructure tierce de gouvernance peut consommer les signaux runtime NeoMundi ;
- NeoMundi n’a pas besoin de remplacer le moteur de politique locale du partenaire ;
- une politique locale peut rester souveraine tout en consommant une couche indépendante de mesure runtime ;
- les signaux NeoMundi et les verdicts locaux peuvent être composés de manière déterministe en actions opérationnelles ;
- la traçabilité et l’intégrité des preuves peuvent être conservées entre les deux infrastructures.

**En termes simples : NeoMundi mesure et signale. OASSE applique sa propre politique. Gatekeeper compose l’action opérationnelle.**

Il s’agit d’un benchmark d’interopérabilité ciblé terminé. Il ne constitue pas, à lui seul, une démonstration de préparation à la production ni d’interopérabilité universelle.

---

## Vue d’ensemble

Ce dépôt documente le **benchmark ciblé NeoMundi × OASSE de 60 appels**, exécuté le **4 août 2026**.

L’expérience a testé une chaîne complète de gouvernance runtime dans laquelle NeoMundi fournissait un signal runtime indépendant tandis qu’OASSE conservait sa propre politique et son autorité d’enforcement.

Run de référence :

`run-d86e7abe7d55`

## Architecture

    Cas contrôlé
          ↓
    Runner / bridge d’intégration
          ↓
          ├───────────────┐
          ↓               ↓
    NeoMundi OBS       OASSE FAM
    signal runtime     verdict de politique locale
          ↓               ↓
          └───────┬───────┘
                  ↓
              Gatekeeper
                  ↓
        PROCEED / HOLD / DENY
                  ↓
          artefact scellé
                  ↓
       réconciliation des traces

NeoMundi et OASSE remplissent donc des fonctions différentes.

**NeoMundi mesure et rapporte le comportement runtime.**

**OASSE FAM applique la politique locale du partenaire.**

**Gatekeeper compose les deux couches pour produire une action opérationnelle.**

## Benchmark

- **Infrastructure partenaire :** OASSE / Oak & Sparrow Systems
- **Couche de mesure :** NeoMundi ControlTower
- **Benchmark :** 60-Pull Focused Governance Benchmark
- **Run de référence :** `run-d86e7abe7d55`
- **Cas tentés :** 60
- **Cas terminés :** 60
- **Artefacts Gatekeeper scellés :** 60
- **Échecs techniques :** 0
- **Mode wire NeoMundi :** `OBS`
- **Désignation interne OASSE :** `GOV`

La distinction entre `OBS` et `GOV` est importante :

- `OBS` est le mode wire NeoMundi effectivement utilisé pendant le run ;
- `GOV` est la désignation interne OASSE du benchmark de gouvernance.

## Résultats

### Signaux runtime NeoMundi

| Résultat | Nombre | Part |
|---|---:|---:|
| `ALLOW` | 58 | 96,67 % |
| `FLAG` | 2 | 3,33 % |

### Verdicts locaux OASSE FAM

| Résultat | Nombre | Part |
|---|---:|---:|
| `ALLOW` | 50 | 83,33 % |
| `BLOCK` | 10 | 16,67 % |

### Actions finales Gatekeeper

| Action | Nombre | Part |
|---|---:|---:|
| `PROCEED` | 48 | 80,00 % |
| `DENY` | 10 | 16,67 % |
| `HOLD` | 2 | 3,33 % |

Ces distributions proviennent d’un benchmark volontairement contrôlé et ne doivent pas être interprétées comme des taux d’incident en production.

## Composition des décisions

La matrice observée est la suivante :

| Verdict OASSE FAM | Signal NeoMundi | Action Gatekeeper | Nombre |
|---|---|---|---:|
| `BLOCK` | `ALLOW` | `DENY` | 10 |
| `ALLOW` | `FLAG` | `HOLD` | 2 |
| `ALLOW` | `ALLOW` | `PROCEED` | 48 |

Cette matrice démontre les deux directions de conservation de l’autorité :

- un `ALLOW` NeoMundi ne neutralise **pas** un `BLOCK` OASSE ;
- un `FLAG` NeoMundi peut transformer une opération autrement admissible en `HOLD`.

L’action opérationnelle finale est donc produite par la couche de composition du partenaire, et non par NeoMundi seul.

## Traçabilité et intégrité des preuves

Le benchmark ciblé a enregistré :

- 60 / 60 lignes de résultats avec statut succès ;
- des ordinals complets de 1 à 60 ;
- des séquences d’artefacts complètes de 1 à 60 ;
- une chaîne externe `previous-hash` continue ;
- des champs `previous-hash` FAM cohérents avec la chaîne Gatekeeper ;
- des identifiants de trace NeoMundi uniques ;
- des hashes de réponse source uniques ;
- 60 / 60 trace IDs NeoMundi réconciliés avec l’export d’audit ;
- une concordance des décisions d’audit avec les faits scellés ;
- une concordance des G-Scores entre audit et faits scellés ;
- un digest stable de l’implémentation du bridge ;
- une version de mesure stable ;
- une version du runner stable.

Le package de preuve permet donc une revalidation du run ciblé à partir des résultats OASSE et de l’export d’audit NeoMundi.

## Résumé des scores runtime

Scores NeoMundi observés sur les 60 réponses scellées :

| Score | Moyenne | Médiane | P95 | Minimum | Maximum |
|---|---:|---:|---:|---:|---:|
| G-Score | 0,5933 | 0,6000 | 0,6000 | 0,4000 | 0,6000 |
| G-Final | 0,9852 | 0,9885 | 0,9885 | 0,8898 | 0,9885 |
| V-Score | 0,9667 | 1,0000 | 1,0000 | 0,0000 | 1,0000 |
| Stability | 0,9128 | 0,9231 | 0,9231 | 0,6154 | 0,9231 |

Ces valeurs sont des mesures runtime associées à ce benchmark. Elles ne constituent ni des verdicts universels ni des taux d’incident en production.

## Temps d’exécution

Temps observés sur le chemin réussi :

| Métrique | Moyenne | Médiane | P95 | P99 | Maximum |
|---|---:|---:|---:|---:|---:|
| Pipeline complet | 20,336 s | 20,325 s | 20,393 s | 20,563 s | 20,798 s |
| Traitement NeoMundi | 20024,02 ms | 20024,54 ms | 20031,75 ms | 20033,56 ms | 20033,60 ms |
| Résiduel OASSE + transport | 311,74 ms | 299,72 ms | 366,73 ms | 539,07 ms | 776,39 ms |

La fenêtre mesurée a duré **20,34 minutes**, soit un débit effectif de **177,01 artefacts scellés par heure**.

La valeur OASSE + transport est un résiduel. Elle peut inclure le transit réseau, la sérialisation, la normalisation du bridge, l’évaluation de la politique, le scellement, la persistance et l’overhead client.

## Séparation des responsabilités

| Couche | Responsabilité |
|---|---|
| NeoMundi | Mesure runtime, scoring, signalement et trace d’audit |
| OASSE FAM | Évaluation indépendante de la politique locale |
| Gatekeeper | Composition déterministe et action opérationnelle |
| Environnement partenaire | Autorité opérationnelle finale et exécution |

La règle architecturale centrale est :

> **NeoMundi ne remplace pas l’autorité métier ou opérationnelle du système intégré. NeoMundi fournit une couche indépendante de mesure et de signalement runtime, consommable par cette autorité.**

## Ce que ce pilote établit — et n’établit pas

### Il établit, dans le périmètre du benchmark

- l’exécution réussie de bout en bout du pipeline ciblé de 60 appels ;
- la consommation des signaux runtime NeoMundi par OASSE ;
- la conservation d’une autorité de politique locale indépendante ;
- une composition déterministe des décisions entre couches ;
- une réconciliation un à un des traces avec les enregistrements d’audit NeoMundi ;
- la continuité et l’intégrité de la chaîne de preuves scellées ;
- la stabilité des versions du bridge, du runner et de la mesure pendant le run ciblé.

### Il n’établit pas

- une préparation à la production à lui seul ;
- une interopérabilité universelle entre tous les systèmes tiers ;
- une sémantique de politique universelle ;
- des performances ou taux d’incident universels ;
- une conformité juridique ou réglementaire ;
- un enforcement natif NeoMundi de `PROCEED`, `HOLD` ou `DENY` ;
- la résilience, la sécurité, les SLA ou le monitoring continu à l’échelle de production.

## Frontière d’interprétation

NeoMundi a fonctionné en mode `OBS` pendant tout le benchmark.

OASSE a appliqué l’enforcement en aval au travers de ses propres couches FAM et Gatekeeper.

Le benchmark démontre donc **un signalement de gouvernance runtime avec enforcement partenaire en aval**, et non un enforcement natif NeoMundi.

## Objet du dépôt

Ce dépôt vise à rendre le pilote d’interopérabilité inspectable et citable.

Il doit préserver la distinction entre :

1. mesure runtime ;
2. interprétation par la politique locale ;
3. enforcement opérationnel ;
4. preuve et audit.

Le dépôt n’a pas besoin d’exposer les mécanismes internes propriétaires de mesure NeoMundi pour documenter l’interopérabilité observée.

## Rapport de référence

Le rapport du benchmark documente notamment :

- les résultats d’exécution ;
- les temps d’exécution ;
- les résultats de gouvernance ;
- la composition cross-gate ;
- les scores NeoMundi ;
- l’intégrité des preuves ;
- la réconciliation des traces ;
- le manifeste des sources ;
- les limites de reproductibilité et d’interprétation.

## Ressources NeoMundi

- [NeoMundi Research](https://neomundi.org)
- [ControlTower](https://controltower.neomundi.io/welcome)
- [Runtime Interoperability Contract](https://github.com/neomundi-io/runtime-interoperability-contract)
- [NeoMundi AI Observatory](https://github.com/neomundi-io/neomundi-ai-observatory)

## Statut

**Benchmark d’interopérabilité ciblé terminé et techniquement validé pour la phase pilote.**

Le run montre qu’OASSE peut conserver une politique et une autorité opérationnelle indépendantes tout en consommant les signaux runtime NeoMundi au travers d’une intégration traçable et auditable.

Des validations supplémentaires sont nécessaires avant toute affirmation plus large concernant la préparation à la production ou l’interopérabilité universelle.
