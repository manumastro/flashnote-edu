# FlashNote EDU – Roadmap di Sviluppo

> Versione 1.1 · Aggiornamento 4 giugno 2025

---

## Legenda delle Fasi

| Fase                              | Descrizione                                                                    | Durata stimata |
| --------------------------------- | ------------------------------------------------------------------------------ | -------------- |
| **Phase 0 – Design & Research**   | Ricerca utenti, definizione UX/UI, architettura informativa.                   | 2 settimane    |
| **Phase 1 – MVP Core**            | Pipeline video → flashcard + spaced repetition.                                | 4 settimane    |
| **Phase 2 – MVP Plus**            | Quiz adattivi, mappe mentali, riassunti strutturati, modalità studio multiple. | 4 settimane    |
| **Phase 3 – Launch Prep**         | Paywall, export, beta testing, QA completa.                                    | 3 settimane    |
| **Phase 4 – Launch & Monitoring** | Deploy store, monitoraggio costi AI, analytics & hot‑fix.                      | 2 settimane    |
| **Phase 5 – Scale & Growth**      | Gamification avanzata, ottimizzazione performance, marketing e partnership.    | Ongoing        |

---

## Timeline Dettagliata

| Week    | Phase | Epic / Obiettivo             | Deliverable chiave                                 |
| ------- | ----- | ---------------------------- | -------------------------------------------------- |
| **0**   | 0     | Discovery & Personas         | Interviste, competitive analysis report            |
| **1**   | 0     | UX & Design System           | Wireframe principali, design tokens Figma          |
| **2**   | 1     | Video ingest & transcription | Endpoint `/process-video`, container WhisperX      |
| **3**   | 1     | Flashcard generation         | Endpoint `/generate-cards`, tab “Flashcards”       |
| **4**   | 1     | SM‑2 engine                  | Tabelle `user_flashcards`, scheduling API          |
| **5**   | 2     | Quiz adaptive engine         | Endpoint `/generate-quiz`, schermata “Quiz Review” |
| **6**   | 2     | Mind maps automatiche        | JSON schema `mind_maps`, componente `MindMapView`  |
| **7**   | 2     | Summaries & timeline         | Endpoint `/generate-summary`, tab “Summary”        |
| **8**   | 2     | Studio Modes selector        | Focus / Quick Review / Deep Dive / Challenge       |
| **9**   | 3     | Paywall & subscriptions      | RevenueCat integration, Stripe webhook             |
| **10**  | 3     | Export Anki / Quizlet / PDF  | Funzione `exportDeck()`, menu “Export”             |
| **11**  | 3     | QA & Beta                    | TestFlight + Detox E2E, bug‑fix sprint             |
| **12**  | 4     | Production deploy            | Store submission, Supabase scaling, Sentry alerts  |
| **13**  | 4     | Post‑launch monitoring       | Mixpanel funnel, cost alerting, hot‑fix roll‑up    |
| **14+** | 5     | Gamification avanzata        | Badge tiers, leaderboard, social share             |
| **14+** | 5     | AI cost optimisation         | Caching, quota‑guard, cold‑start mitigation        |
| **14+** | 5     | GTM & marketing              | ASO, Product Hunt, campus ambassadors              |
| **14+** | 5     | Localization & accessibility | i18n, font dislessia, voice over support           |

---

## Dipendenze Chiave

* **WhisperX**: runner GPU disponibile (Docker / cloud GPU)
* **Gemini Pro**: accesso API stabile
* **Store Accounts**: Apple Developer & Google Play
* **Budget AI**: \~500 €/mese per token+transcription

---

## Milestone di Rilascio

* 🎯 **MVP interno** → fine **Week 6**
* 🧪 **Beta pubblica** → fine **Week 11**
* 🚀 **Launch store** → fine **Week 12**
* 👥 **1 000 MAU** → target **Week 20**
* 💸 **Break‑even 300 Pro** → target **Week 28**

---

## Aggiornamento del Documento

La roadmap viene rivista ogni 4 settimane nel **Product Sync** e la versione aggiornata viene pubblicata su GitBook e nel repository `/docs/roadmap.md`.

---

> *Trasforma ogni video in conoscenza, ogni ripetizione in padronanza.*
