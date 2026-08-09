# OASSE × NeoMundi

**Runtime measurement, deterministic policy enforcement and evidence integrity — interoperability pilot.**

[🇫🇷 Lire en français](#version-française)

---

# English

## What happened here?

Oak & Sparrow Systems Enterprise (OASSE) integrated the NeoMundi runtime measurement layer into its pre-existing deterministic policy, action-control and evidence architecture.

The articulation was evaluated across **two controlled populations**:

- a focused **60-request evidence benchmark**;
- a broader **1,000-request controlled experiment**.

NeoMundi measured runtime behavior. OASSE independently interpreted the available measurements under its declared policy. Gatekeeper produced the downstream operational action and sealed the resulting evidence.

**In simple terms: NeoMundi measures. OASSE determines and enforces.**

### What this shows

The experiments provide evidence that:

- an independent third-party infrastructure can consume NeoMundi runtime measurements;
- the measurement layer can affect operational routing without becoming the authorization authority;
- the partner can retain its own deterministic policy and enforcement logic;
- measurement, interpretation, action and evidence can remain technically distinct and traceable;
- the same articulation can operate across both a focused evidence run and a larger controlled population.

The results provide **one substantive indication in support of a common metrological layer for heterogeneous AI infrastructures**, while cross-architectural generality remains an open question requiring further comparison and replication.

---

## Overview

This repository documents the NeoMundi × OASSE interoperability articulation and its associated evidence.

The experimental question was narrow:

> Can an independent runtime measurement layer be integrated into a deterministic policy and enforcement architecture while preserving a clear separation between measurement, interpretation and final action?

OASSE already possessed its own deterministic policy packs, rule evaluation, action-control logic, sealed evidence chain and benchmark runners before NeoMundi was integrated.

NeoMundi did not create OASSE's policy authority, FAM determinations, Gatekeeper actions or evidence-chain mechanism.

NeoMundi added an independent runtime measurement and traceability layer.

---

## Architecture

    Controlled request
          ↓
    OASSE integration bridge
          ↓
          ├────────────────────┐
          ↓                    ↓
    NeoMundi OBS            OASSE FAM
    runtime measurement     deterministic policy
          ↓                    ↓
          └─────────┬──────────┘
                    ↓
                Gatekeeper
                    ↓
          PROCEED / HOLD / DENY
                    ↓
            sealed evidence
                    ↓
          trace / audit chain

### Responsibility boundary

**NeoMundi**
→ measures runtime behavior and returns measurement-layer classifications, scores, trace identifiers and supporting evidence.

**OASSE FAM**
→ evaluates the original request independently under declared local policy.

**Gatekeeper**
→ composes the available results, produces the operational action and seals the evidence artifact.

NeoMundi's `ALLOW` and `FLAG` values are treated here as **measurement-layer classifications**, not authorization decisions.

---

## Integration path

The validated integration path was:

1. load a controlled request and its NeoMundi measurement payload;
2. send the payload through the deployed NeoMundi `OBS` interface;
3. preserve and normalize the NeoMundi response;
4. convert selected measurements into versioned and traceable OASSE evidence facts;
5. evaluate the original request independently through the OASSE FAM policy engine;
6. select the strictest combined state;
7. produce a Gatekeeper action of `PROCEED`, `HOLD` or `DENY`;
8. seal the composite evidence artifact;
9. append the artifact to the OASSE evidence chain.

A runnable launcher and HTML console were subsequently packaged around this validated path.

`OBS` is the deployed NeoMundi wire mode.

`GOV` is the internal OASSE designation for the controlled governance scenario.

---

# Focused 60-request benchmark

## Reference run

`run-d86e7abe7d55`

Date: **4 August 2026**

### Execution

- **Cases attempted:** 60
- **Cases completed successfully:** 60
- **Gatekeeper artifacts sealed:** 60
- **Technical failures:** 0
- **NeoMundi trace IDs reconciled:** 60 / 60
- **Distinct source-response hashes:** 60
- **NeoMundi wire mode:** `OBS`

No transport, authentication, validation, timeout or runner failure was observed in the focused result set.

## Outcomes

### NeoMundi measurement layer

| Classification | Count | Share |
|---|---:|---:|
| `ALLOW` | 58 | 96.67% |
| `FLAG` | 2 | 3.33% |

### OASSE FAM

| Verdict | Count | Share |
|---|---:|---:|
| `ALLOW` | 50 | 83.33% |
| `BLOCK` | 10 | 16.67% |

### Gatekeeper

| Action | Count | Share |
|---|---:|---:|
| `PROCEED` | 48 | 80.00% |
| `DENY` | 10 | 16.67% |
| `HOLD` | 2 | 3.33% |

These distributions come from an intentionally controlled benchmark pack and must not be interpreted as production incident rates.

## Cross-layer composition

| OASSE FAM verdict | NeoMundi classification | Gatekeeper action | Count |
|---|---|---|---:|
| `BLOCK` | `ALLOW` | `DENY` | 10 |
| `ALLOW` | `FLAG` | `HOLD` | 2 |
| `ALLOW` | `ALLOW` | `PROCEED` | 48 |

This demonstrates both directions of authority preservation:

- a NeoMundi `ALLOW` did **not** override an OASSE `BLOCK`;
- a NeoMundi `FLAG` moved two otherwise admissible requests to `HOLD`.

The measurement layer influenced operational routing without becoming the authorization authority.

---

## Traceability and evidence integrity

The focused run preserved:

- complete ordinals from 1 through 60;
- complete artifact sequences from 1 through 60;
- continuous outer previous-hash chaining;
- agreement between FAM previous-hash fields and Gatekeeper artifacts;
- unique NeoMundi trace IDs;
- unique source-response hashes;
- 60 / 60 direct trace reconciliation against NeoMundi audit records;
- agreement between matched audit decisions and sealed facts;
- agreement between matched audit G-Scores and sealed facts;
- stable bridge implementation digest;
- stable measurement version;
- stable runner version.

The focused evidence package therefore supports case-level re-validation and reconciliation between OASSE artifacts and NeoMundi audit evidence.

---

## Focused-run performance

| Metric | Mean | Median | P95 | P99 | Maximum |
|---|---:|---:|---:|---:|---:|
| Full pipeline | 20.336 s | 20.325 s | 20.393 s | 20.563 s | 20.798 s |
| NeoMundi processing | 20024.02 ms | 20024.54 ms | 20031.75 ms | 20033.56 ms | 20033.60 ms |
| OASSE + transport residual | 311.74 ms | 299.72 ms | 366.73 ms | 539.07 ms | 776.39 ms |

- **Measured window:** 20.34 minutes
- **Effective throughput:** 177.01 sealed artifacts/hour

The OASSE + transport value is a residual measurement, not an isolated processor timer.

---

# Controlled 1,000-request experiment

The broader controlled experiment extended the same articulation to **1,000 attempted calls**.

### Execution

- **NeoMundi measurements recorded:** 1,000 / 1,000
- **OASSE artifacts sealed:** 996
- **Local response timeouts:** 4
- **Local sealing rate:** 99.6%

The four timed-out calls remained visible in the attempted population and were preserved as reliability evidence rather than rewritten as successes.

## Outcomes

### NeoMundi measurement layer

| Classification | Count / base |
|---|---:|
| `ALLOW` | 253 / 1,000 |
| `FLAG` | 747 / 1,000 |

### OASSE FAM

| Verdict | Count / base |
|---|---:|
| `ABSTAIN` | 115 / 996 |
| `ALLOW` | 232 / 996 |
| `BLOCK` | 440 / 996 |
| `REVIEW` | 209 / 996 |

### Gatekeeper

| Action | Count / base |
|---|---:|
| `PROCEED` | 47 / 996 |
| `HOLD` | 509 / 996 |
| `DENY` | 440 / 996 |

These controlled distributions are experimental populations and must not be interpreted as production incident rates.

---

## 1,000-request performance

| Metric | Observed result |
|---|---:|
| Average full-pipeline duration | 20.414 s |
| Average NeoMundi processing time | 20.023 s |
| Average OASSE + transport residual | 390.77 ms |
| Median residual | 381.79 ms |
| P95 residual | 482.00 ms |
| P99 residual | 701.57 ms |
| Maximum residual | 907.09 ms |
| Effective throughput | 174.26 sealed artifacts/hour |

For the 996 successfully sealed actions, the narrower post-FAM Gatekeeper finalization stage completed below **250 ms in every case**, with a maximum reported finalization time of **1.9541 ms**.

---

## Operational value observed

The main operational value was a complete and separable path showing:

- what NeoMundi measured;
- what OASSE policy determined;
- what Gatekeeper did;
- which evidence supported each stage;
- how long the measured boundaries required.

The articulation therefore demonstrated a functioning:

**measurement → policy → action → evidence**

pipeline with independent runtime measurement, deterministic interpretation, operational routing, traceable provenance, case-level audit reconstruction and chained evidence integrity.

---

## What NeoMundi added

OASSE already had:

- deterministic policy determination;
- action selection;
- sealing;
- evidence persistence;
- policy and statutory provenance;
- controlled runners.

NeoMundi added:

- independent runtime behavioral measurement;
- runtime measurement-layer classifications;
- measurement scores;
- trace identifiers;
- measurement and normalizer versions;
- confidence values;
- G-Score;
- G-Final;
- V-Score;
- Stability;
- processing-time information;
- source-response digests;
- raw response evidence where returned.

OASSE therefore classifies the NeoMundi contribution as **complementary and operationally distinct**.

---

## What this case establishes — and does not establish

### It establishes within these controlled experiments

- successful integration of NeoMundi measurements into an existing third-party governance architecture;
- preservation of independent OASSE policy authority;
- deterministic downstream action composition;
- runtime measurement affecting routing without becoming authorization;
- traceable and reconstructable evidence across both infrastructures;
- successful execution of a focused 60-request evidence benchmark;
- extension of the articulation to a controlled 1,000-request population.

### It does not establish

- universal interoperability across heterogeneous architectures;
- production readiness on its own;
- universal decision relevance of every NeoMundi measurement;
- independent external ground truth for every behavioral measurement;
- universal incident rates or universal performance;
- legal or regulatory compliance;
- native NeoMundi enforcement of partner actions;
- resilience, security, SLA or continuous-monitoring performance at production scale.

---

## Research interpretation

The OASSE research contribution treats this articulation as **one substantive indication in support of a common metrological layer for heterogeneous AI infrastructures**.

The evidence supports complementary operational value in routing, traceability, auditability and evidence quality.

The stronger claim — that the same metrological layer generalizes across very different external architectures — remains an open comparative question requiring additional independent articulations and replication.

---

## Documentation

This repository should preserve two distinct reference documents:

### Focused benchmark report

`OASSE_NeoMundi_60_Pull_Benchmark_2026-08-04.pdf`

Documents:

- the 60-request focused live benchmark;
- timing;
- cross-layer outcomes;
- trace reconciliation;
- evidence-chain integrity;
- source manifest and verification method.

### Research contribution

`NeoMundi_Oak_Sparrow_Common_Metrological_Layer_Research.pdf`

Documents:

- the pre-existing OASSE architecture;
- the NeoMundi integration method;
- the 60-request experiment;
- the controlled 1,000-request experiment;
- operational value;
- limitations;
- the contribution to the common-metrological-layer research question.

---

## Status

**Interoperability articulation completed and technically validated for the controlled pilot phase.**

The evidence shows that OASSE can retain independent deterministic policy and operational authority while consuming NeoMundi runtime measurements through a traceable and auditable integration.

Further cross-architectural replication is required before broader generalisation.

---

## Ressources

### Oak & Sparrow Systems Enterprise

- [Oak & Sparrow Systems Enterprise](https://oakandsparrowsystemsenterprise.io/)

### NeoMundi

- [NeoMundi Research](https://neomundi.org)
- [ControlTower](https://controltower.neomundi.io/welcome)
- [Runtime Interoperability Contract](https://github.com/neomundi-io/runtime-interoperability-contract)
- [NeoMundi AI Observatory](https://github.com/neomundi-io/neomundi-ai-observatory)

---

# Version française

[🇬🇧 Back to English](#english)

## Qu’est-ce qui a été fait ici ?

Oak & Sparrow Systems Enterprise (OASSE) a intégré la couche de mesure runtime NeoMundi dans son architecture préexistante de politique déterministe, de contrôle d’action et de preuve.

L’articulation a été évaluée sur **deux populations contrôlées** :

- un benchmark ciblé de **60 requêtes**, centré sur la preuve ;
- une expérience contrôlée élargie de **1 000 requêtes**.

NeoMundi a mesuré le comportement runtime. OASSE a interprété indépendamment les mesures disponibles sous sa politique déclarée. Gatekeeper a produit l’action opérationnelle en aval et scellé la preuve correspondante.

**En termes simples : NeoMundi mesure. OASSE détermine et applique.**

### Ce que cela montre

Les expériences apportent des éléments montrant que :

- une infrastructure tierce indépendante peut consommer les mesures runtime NeoMundi ;
- la couche de mesure peut influencer le routage opérationnel sans devenir l’autorité d’autorisation ;
- le partenaire peut conserver sa propre politique déterministe et sa logique d’enforcement ;
- mesure, interprétation, action et preuve peuvent rester techniquement distinctes et traçables ;
- la même articulation peut fonctionner sur un run de preuve ciblé puis sur une population contrôlée plus large.

Les résultats constituent **une indication substantielle en faveur d’une couche métrologique commune pour des infrastructures IA hétérogènes**, tandis que la généralité inter-architectures reste une question ouverte nécessitant comparaison et réplication.

---

## Vue d’ensemble

Ce dépôt documente l’articulation d’interopérabilité NeoMundi × OASSE et les preuves associées.

La question expérimentale était volontairement étroite :

> Une couche indépendante de mesure runtime peut-elle être intégrée à une architecture déterministe de politique et d’enforcement tout en maintenant une séparation claire entre mesure, interprétation et action finale ?

Avant NeoMundi, OASSE disposait déjà de ses propres policy packs déterministes, de son moteur de règles, de sa logique de contrôle d’action, de sa chaîne de preuve scellée et de ses runners de benchmark.

NeoMundi n’a créé ni l’autorité de politique OASSE, ni les déterminations FAM, ni les actions Gatekeeper, ni le mécanisme de chaîne de preuve.

NeoMundi a ajouté une couche indépendante de mesure runtime et de traçabilité.

---

## Architecture

    Requête contrôlée
          ↓
    Bridge d’intégration OASSE
          ↓
          ├────────────────────┐
          ↓                    ↓
    NeoMundi OBS            OASSE FAM
    mesure runtime          politique déterministe
          ↓                    ↓
          └─────────┬──────────┘
                    ↓
                Gatekeeper
                    ↓
          PROCEED / HOLD / DENY
                    ↓
             preuve scellée
                    ↓
          chaîne trace / audit

### Frontière des responsabilités

**NeoMundi**
→ mesure le comportement runtime et retourne des classifications de couche de mesure, des scores, des identifiants de trace et les éléments de preuve associés.

**OASSE FAM**
→ évalue indépendamment la requête initiale sous la politique locale déclarée.

**Gatekeeper**
→ compose les résultats disponibles, produit l’action opérationnelle et scelle l’artefact de preuve.

Les valeurs NeoMundi `ALLOW` et `FLAG` sont traitées ici comme des **classifications de couche de mesure**, et non comme des décisions d’autorisation.

---

## Chemin d’intégration

Le chemin validé était :

1. charger une requête contrôlée et son payload de mesure NeoMundi ;
2. envoyer le payload via l’interface NeoMundi `OBS` déployée ;
3. préserver et normaliser la réponse NeoMundi ;
4. convertir certaines mesures en faits de preuve OASSE versionnés et traçables ;
5. évaluer indépendamment la requête initiale via le moteur de politique OASSE FAM ;
6. sélectionner l’état combiné le plus strict ;
7. produire une action Gatekeeper `PROCEED`, `HOLD` ou `DENY` ;
8. sceller l’artefact composite de preuve ;
9. ajouter l’artefact à la chaîne de preuve OASSE.

Un launcher exécutable et une console HTML ont ensuite été packagés autour de ce chemin validé.

`OBS` est le mode wire NeoMundi effectivement déployé.

`GOV` reste la désignation interne OASSE du scénario de gouvernance contrôlé.

---

# Benchmark ciblé de 60 requêtes

## Run de référence

`run-d86e7abe7d55`

Date : **4 août 2026**

### Exécution

- **Cas tentés :** 60
- **Cas terminés avec succès :** 60
- **Artefacts Gatekeeper scellés :** 60
- **Échecs techniques :** 0
- **Trace IDs NeoMundi réconciliés :** 60 / 60
- **Hashes de réponses source distincts :** 60
- **Mode wire NeoMundi :** `OBS`

Aucun échec de transport, d’authentification, de validation, de timeout ou de runner n’a été observé dans le résultat ciblé.

## Résultats

### Couche de mesure NeoMundi

| Classification | Nombre | Part |
|---|---:|---:|
| `ALLOW` | 58 | 96,67 % |
| `FLAG` | 2 | 3,33 % |

### OASSE FAM

| Verdict | Nombre | Part |
|---|---:|---:|
| `ALLOW` | 50 | 83,33 % |
| `BLOCK` | 10 | 16,67 % |

### Gatekeeper

| Action | Nombre | Part |
|---|---:|---:|
| `PROCEED` | 48 | 80,00 % |
| `DENY` | 10 | 16,67 % |
| `HOLD` | 2 | 3,33 % |

Ces distributions proviennent d’un benchmark volontairement contrôlé et ne doivent pas être interprétées comme des taux d’incident en production.

## Composition inter-couches

| Verdict OASSE FAM | Classification NeoMundi | Action Gatekeeper | Nombre |
|---|---|---|---:|
| `BLOCK` | `ALLOW` | `DENY` | 10 |
| `ALLOW` | `FLAG` | `HOLD` | 2 |
| `ALLOW` | `ALLOW` | `PROCEED` | 48 |

Cela démontre les deux directions de conservation de l’autorité :

- un `ALLOW` NeoMundi n’a **pas** neutralisé un `BLOCK` OASSE ;
- un `FLAG` NeoMundi a déplacé deux requêtes autrement admissibles vers `HOLD`.

La couche de mesure a donc influencé le routage opérationnel sans devenir l’autorité d’autorisation.

---

## Traçabilité et intégrité des preuves

Le run ciblé a conservé :

- des ordinals complets de 1 à 60 ;
- des séquences d’artefacts complètes de 1 à 60 ;
- une chaîne externe `previous-hash` continue ;
- une concordance des champs `previous-hash` FAM avec les artefacts Gatekeeper ;
- des trace IDs NeoMundi uniques ;
- des hashes de réponse source uniques ;
- une réconciliation directe de 60 / 60 traces avec les enregistrements d’audit NeoMundi ;
- une concordance entre les décisions d’audit et les faits scellés ;
- une concordance entre les G-Scores d’audit et les faits scellés ;
- un digest stable de l’implémentation du bridge ;
- une version de mesure stable ;
- une version de runner stable.

Le package de preuve ciblé permet donc une revalidation au niveau de chaque cas entre les artefacts OASSE et les preuves d’audit NeoMundi.

---

## Performance du run ciblé

| Métrique | Moyenne | Médiane | P95 | P99 | Maximum |
|---|---:|---:|---:|---:|---:|
| Pipeline complet | 20,336 s | 20,325 s | 20,393 s | 20,563 s | 20,798 s |
| Traitement NeoMundi | 20024,02 ms | 20024,54 ms | 20031,75 ms | 20033,56 ms | 20033,60 ms |
| Résiduel OASSE + transport | 311,74 ms | 299,72 ms | 366,73 ms | 539,07 ms | 776,39 ms |

- **Fenêtre mesurée :** 20,34 minutes
- **Débit effectif :** 177,01 artefacts scellés/heure

La valeur OASSE + transport est une mesure résiduelle, et non un chronométrage isolé du moteur partenaire.

---

# Expérience contrôlée de 1 000 requêtes

L’expérience élargie a étendu la même articulation à **1 000 appels tentés**.

### Exécution

- **Mesures NeoMundi enregistrées :** 1 000 / 1 000
- **Artefacts OASSE scellés :** 996
- **Timeouts locaux :** 4
- **Taux local de scellement :** 99,6 %

Les quatre appels en timeout sont restés visibles dans la population tentée et ont été conservés comme preuve de fiabilité plutôt que réécrits comme des succès.

## Résultats

### Couche de mesure NeoMundi

| Classification | Nombre / base |
|---|---:|
| `ALLOW` | 253 / 1 000 |
| `FLAG` | 747 / 1 000 |

### OASSE FAM

| Verdict | Nombre / base |
|---|---:|
| `ABSTAIN` | 115 / 996 |
| `ALLOW` | 232 / 996 |
| `BLOCK` | 440 / 996 |
| `REVIEW` | 209 / 996 |

### Gatekeeper

| Action | Nombre / base |
|---|---:|
| `PROCEED` | 47 / 996 |
| `HOLD` | 509 / 996 |
| `DENY` | 440 / 996 |

Ces distributions contrôlées sont expérimentales et ne doivent pas être interprétées comme des taux d’incident en production.

---

## Performance sur 1 000 requêtes

| Métrique | Résultat observé |
|---|---:|
| Durée moyenne pipeline complet | 20,414 s |
| Temps moyen NeoMundi | 20,023 s |
| Résiduel moyen OASSE + transport | 390,77 ms |
| Résiduel médian | 381,79 ms |
| P95 résiduel | 482,00 ms |
| P99 résiduel | 701,57 ms |
| Résiduel maximum | 907,09 ms |
| Débit effectif | 174,26 artefacts scellés/heure |

Pour les 996 actions scellées avec succès, l’étape plus étroite de finalisation Gatekeeper post-FAM est restée sous **250 ms dans tous les cas**, avec un maximum rapporté de **1,9541 ms**.

---

## Valeur opérationnelle observée

La principale valeur opérationnelle observée est un chemin complet et séparable permettant d’identifier :

- ce que NeoMundi a mesuré ;
- ce que la politique OASSE a déterminé ;
- ce que Gatekeeper a fait ;
- quelles preuves soutenaient chaque étape ;
- combien de temps chaque frontière mesurée a nécessité.

L’articulation démontre donc un pipeline fonctionnel :

**mesure → politique → action → preuve**

avec mesure runtime indépendante, interprétation déterministe, routage opérationnel, provenance traçable, reconstruction d’audit au niveau des cas et intégrité d’une chaîne de preuve.

---

## Ce que NeoMundi a ajouté

OASSE disposait déjà de :

- la détermination de politique ;
- la sélection d’action ;
- le scellement ;
- la persistance de preuve ;
- la provenance politique et statutaire ;
- des runners contrôlés.

NeoMundi a ajouté :

- une mesure comportementale runtime indépendante ;
- des classifications de couche de mesure ;
- des scores de mesure ;
- des identifiants de trace ;
- des versions de mesure et de normalisation ;
- des valeurs de confiance ;
- G-Score ;
- G-Final ;
- V-Score ;
- Stability ;
- des informations de temps de traitement ;
- des digests de réponse source ;
- les éléments de réponse brute lorsqu’ils étaient retournés.

OASSE classe donc la contribution NeoMundi comme **complémentaire et opérationnellement distincte**.

---

## Ce que ce cas établit — et n’établit pas

### Il établit dans le périmètre de ces expériences contrôlées

- l’intégration réussie des mesures NeoMundi dans une architecture tierce existante ;
- la conservation d’une autorité de politique OASSE indépendante ;
- une composition déterministe des actions en aval ;
- une mesure runtime pouvant influencer le routage sans devenir l’autorité d’autorisation ;
- des preuves traçables et reconstructibles entre les deux infrastructures ;
- l’exécution réussie d’un benchmark de preuve ciblé de 60 requêtes ;
- l’extension de l’articulation à une population contrôlée de 1 000 requêtes.

### Il n’établit pas

- une interopérabilité universelle entre architectures hétérogènes ;
- une préparation à la production à lui seul ;
- la pertinence décisionnelle universelle de chaque mesure NeoMundi ;
- une vérité terrain externe indépendante pour chaque mesure comportementale ;
- des taux d’incident ou performances universels ;
- une conformité juridique ou réglementaire ;
- un enforcement natif NeoMundi des actions du partenaire ;
- la résilience, la sécurité, les SLA ou le monitoring continu à l’échelle de production.

---

## Interprétation scientifique

La contribution de recherche OASSE présente cette articulation comme **une indication substantielle en faveur d’une couche métrologique commune pour des infrastructures IA hétérogènes**.

Les éléments observés soutiennent une valeur opérationnelle complémentaire en matière de routage, traçabilité, auditabilité et qualité de preuve.

La revendication plus forte — selon laquelle une même couche métrologique se généralise à des architectures externes très différentes — reste une question comparative ouverte qui nécessite d’autres articulations indépendantes et des réplications.

---

## Documentation

Ce dépôt doit conserver deux documents de référence distincts.

### Rapport du benchmark ciblé

`OASSE_NeoMundi_60_Pull_Benchmark_2026-08-04.pdf`

Documente :

- le benchmark live ciblé de 60 requêtes ;
- les performances ;
- les résultats inter-couches ;
- la réconciliation des traces ;
- l’intégrité de la chaîne de preuve ;
- le manifeste des sources et la méthode de vérification.

### Contribution de recherche

`NeoMundi_Oak_Sparrow_Common_Metrological_Layer_Research.pdf`

Documente :

- l’architecture OASSE préexistante ;
- la méthode d’intégration NeoMundi ;
- l’expérience de 60 requêtes ;
- l’expérience contrôlée de 1 000 requêtes ;
- la valeur opérationnelle observée ;
- les limites ;
- la contribution à la question de recherche sur une couche métrologique commune.

---

## Statut

**Articulation d’interopérabilité terminée et techniquement validée pour la phase pilote contrôlée.**

Les éléments disponibles montrent qu’OASSE peut conserver une politique déterministe et une autorité opérationnelle indépendantes tout en consommant les mesures runtime NeoMundi au travers d’une intégration traçable et auditable.

Des réplications inter-architectures supplémentaires sont nécessaires avant toute généralisation plus large.

---

## Ressources

### Oak & Sparrow Systems Enterprise

- [Oak & Sparrow Systems Enterprise](https://oakandsparrowsystemsenterprise.io/)

### NeoMundi

- [NeoMundi Research](https://neomundi.org)
- [ControlTower](https://controltower.neomundi.io/welcome)
- [Runtime Interoperability Contract](https://github.com/neomundi-io/runtime-interoperability-contract)
- [NeoMundi AI Observatory](https://github.com/neomundi-io/neomundi-ai-observatory)
