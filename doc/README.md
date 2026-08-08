# Documentation

Supporting documentation for the **OASSE × NeoMundi runtime governance interoperability case**.

[🇫🇷 Lire en français](#version-française)

---

## English

### Purpose

This directory contains the principal reports associated with the interoperability experiments conducted between **NeoMundi** and **Oak & Sparrow Systems Enterprise (OASSE)**.

The documentation covers two controlled experimental populations:

- a focused **60-request benchmark** centered on traceability, decision composition and evidence integrity;
- a broader **1,000-request controlled experiment** used to observe the same articulation across a larger population.

A separate research contribution interprets these results in the context of the hypothesis of a **common metrological layer for heterogeneous AI infrastructures**.

### Documents

#### `OASSE_NeoMundi_60_Pull_Benchmark_2026-08-04.pdf`

Focused 60-request benchmark report.

It documents:

- 60 attempted and successfully completed calls;
- 60 sealed Gatekeeper artifacts;
- NeoMundi runtime classifications;
- OASSE FAM policy verdicts;
- Gatekeeper `PROCEED`, `HOLD` and `DENY` actions;
- one-to-one reconciliation of 60 NeoMundi trace IDs;
- sequential evidence-chain integrity;
- timing and throughput;
- reproducibility and source-manifest information.

This report is the main evidence document for the focused pilot run.

#### `OASSE_NeoMundi_1000_Pull_Benchmark_CORRECTED_V2_2026-07-29.pdf`

Controlled 1,000-request benchmark report.

It documents the broader experimental population in which:

- NeoMundi recorded 1,000 runtime measurements;
- OASSE sealed 996 local artifacts;
- four calls ended in local response timeouts;
- the local sealing rate was 99.6%;
- measurement, local policy and downstream Gatekeeper actions remained separately observable.

This report extends the experimental population beyond the focused 60-request run.

#### `NeoMundi_Oak_Sparrow_Common_Metrological_Layer_Research.pdf`

Research contribution from **Oak & Sparrow Systems Enterprise × NeoMundi Research**.

It places the experimental results in their architectural and research context.

The document describes:

- the OASSE capabilities that existed before NeoMundi integration;
- the integration method;
- the separation between measurement, interpretation and action;
- the 60-request and 1,000-request experiments;
- the operational value observed;
- the main limitations and remaining uncertainties;
- the contribution of this articulation to the research question of a common metrological layer.

The document treats the results as **one substantive indication in support of a common metrological layer**, while leaving cross-architectural generality as an open comparative question.

### Responsibility separation

The documented architecture preserves distinct responsibilities:

**NeoMundi**  
→ measures runtime behavior and provides measurement-layer signals, scores and traceability.

**OASSE FAM**  
→ interprets the request independently under declared local policy.

**Gatekeeper**  
→ produces the downstream operational action and seals the resulting evidence.

**OASSE / partner environment**  
→ retains final operational and enforcement authority.

In short:

**NeoMundi measures. OASSE determines and enforces.**

### Scope

These documents describe controlled interoperability experiments and their associated evidence.

They do **not**, by themselves, establish:

- universal interoperability;
- production readiness;
- universal policy semantics;
- universal performance or incident rates;
- legal or regulatory compliance.

They also do not imply that NeoMundi natively executes OASSE's `PROCEED`, `HOLD` or `DENY` actions.

### Related resources

- [NeoMundi Research](https://neomundi.org)
- [ControlTower](https://controltower.neomundi.io/welcome)
- [Runtime Interoperability Contract](https://github.com/neomundi-io/runtime-interoperability-contract)
- [NeoMundi AI Observatory](https://github.com/neomundi-io/neomundi-ai-observatory)

---

# Version française

[🇬🇧 Back to English](#english)

## Objet

Ce dossier contient les principaux rapports associés aux expériences d’interopérabilité conduites entre **NeoMundi** et **Oak & Sparrow Systems Enterprise (OASSE)**.

La documentation couvre deux populations expérimentales contrôlées :

- un benchmark ciblé de **60 requêtes**, centré sur la traçabilité, la composition des décisions et l’intégrité des preuves ;
- une expérience contrôlée élargie de **1 000 requêtes**, utilisée pour observer la même articulation sur une population plus importante.

Une contribution de recherche distincte interprète ces résultats dans le contexte de l’hypothèse d’une **couche métrologique commune pour des infrastructures IA hétérogènes**.

## Documents

### `OASSE_NeoMundi_60_Pull_Benchmark_2026-08-04.pdf`

Rapport du benchmark ciblé de 60 requêtes.

Il documente notamment :

- 60 appels tentés et terminés avec succès ;
- 60 artefacts Gatekeeper scellés ;
- les classifications runtime NeoMundi ;
- les verdicts de politique OASSE FAM ;
- les actions Gatekeeper `PROCEED`, `HOLD` et `DENY` ;
- la réconciliation un à un de 60 trace IDs NeoMundi ;
- l’intégrité séquentielle de la chaîne de preuve ;
- les temps d’exécution et le débit ;
- les informations de reproductibilité et de manifeste des sources.

Ce rapport constitue le principal document de preuve du run pilote ciblé.

### `OASSE_NeoMundi_1000_Pull_Benchmark_CORRECTED_V2_2026-07-29.pdf`

Rapport du benchmark contrôlé de 1 000 requêtes.

Il documente la population expérimentale élargie dans laquelle :

- NeoMundi a enregistré 1 000 mesures runtime ;
- OASSE a scellé 996 artefacts locaux ;
- quatre appels se sont terminés par des timeouts locaux ;
- le taux local de scellement a été de 99,6 % ;
- la mesure, la politique locale et les actions Gatekeeper en aval sont restées séparément observables.

Ce rapport étend la population expérimentale au-delà du run ciblé de 60 requêtes.

### `NeoMundi_Oak_Sparrow_Common_Metrological_Layer_Research.pdf`

Contribution de recherche **Oak & Sparrow Systems Enterprise × NeoMundi Research**.

Elle replace les résultats expérimentaux dans leur contexte architectural et scientifique.

Le document décrit notamment :

- les capacités OASSE existant avant l’intégration de NeoMundi ;
- la méthode d’intégration ;
- la séparation entre mesure, interprétation et action ;
- les expériences de 60 et 1 000 requêtes ;
- la valeur opérationnelle observée ;
- les principales limites et incertitudes restantes ;
- la contribution de cette articulation à la question de recherche d’une couche métrologique commune.

Le document présente les résultats comme **une indication substantielle en faveur d’une couche métrologique commune**, tout en laissant la généralité inter-architectures comme une question comparative ouverte.

## Séparation des responsabilités

L’architecture documentée maintient des responsabilités distinctes :

**NeoMundi**  
→ mesure le comportement runtime et fournit des signaux de couche de mesure, des scores et de la traçabilité.

**OASSE FAM**  
→ interprète indépendamment la requête selon une politique locale déclarée.

**Gatekeeper**  
→ produit l’action opérationnelle en aval et scelle la preuve correspondante.

**OASSE / environnement partenaire**  
→ conserve l’autorité opérationnelle et l’autorité d’enforcement finales.

En résumé :

**NeoMundi mesure. OASSE détermine et applique.**

## Périmètre

Ces documents décrivent des expériences contrôlées d’interopérabilité et les preuves qui leur sont associées.

Ils n’établissent **pas**, à eux seuls :

- une interopérabilité universelle ;
- une préparation à la production ;
- une sémantique de politique universelle ;
- des performances ou taux d’incident universels ;
- une conformité juridique ou réglementaire.

Ils n’impliquent pas non plus que NeoMundi exécute nativement les actions OASSE `PROCEED`, `HOLD` ou `DENY`.

## Ressources associées

- [NeoMundi Research](https://neomundi.org)
- [ControlTower](https://controltower.neomundi.io/welcome)
- [Runtime Interoperability Contract](https://github.com/neomundi-io/runtime-interoperability-contract)
- [NeoMundi AI Observatory](https://github.com/neomundi-io/neomundi-ai-observatory)
