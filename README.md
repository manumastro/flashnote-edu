# FlashNote EDU 🎓📱
*Documentazione Tecnica Completa v2.0*

> Trasforma video-lezioni YouTube in flashcard e quiz adattivi in meno di 30 secondi

---

## 📋 Executive Summary

### Panoramica del Progetto
FlashNote EDU è un'applicazione mobile rivoluzionaria che trasforma l'apprendimento digitale convertendo automaticamente video educativi di YouTube in **flashcard intelligenti**, **quiz adattivi**, **mappe mentali interattive** e **riassunti strutturati**. L'app utilizza intelligenza artificiale avanzata per estrarre contenuti chiave e creare materiali di studio personalizzati con sistema di ripetizione dilazionata scientificamente provato.

### 🎯 Analisi del Problema
- **Gap di Mercato**: Il 90% degli studenti utilizza strumenti AI per studiare ma mancano soluzioni integrate mobile-first
- **Frammentazione**: Nessuna app unisce efficacemente "video → flashcard + quiz" con elementi di gamification
- **Limitazioni Esistenti**: Google offre riassunti video ma non spaced repetition personalizzata
- **Tempo Sprecato**: Gli studenti perdono ore a creare manualmente flashcard da video lunghi

### 💡 Proposta di Valore Unica
- **Velocità Estrema**: Trasformazione completa in < 30 secondi da video a contenuti di studio
- **Multi-formato Intelligente**: Flashcard, quiz, mappe mentali, riassunti tutti generati simultaneamente
- **Gamification Avanzata**: Streaks, badge, classifiche e statistiche dettagliate
- **Interoperabilità Totale**: Export verso Anki, Quizlet, PDF e altri formati standard
- **Mobile-first Design**: Esperienza ottimizzata specificamente per smartphone e tablet

---

## 🎓 Funzionalità Core

### 📚 Sistema di Generazione Contenuti AI

#### 📚 **Flashcard Intelligenti**

**Processo di Creazione**
1.  **Estrazione Trascrizioni**: Utilizzo API YouTube per ottenere sottotitoli automatici/manuali
2.  **Analisi Semantica**: Elaborazione NLP per identificare concetti chiave, definizioni, esempi
3.  **Tassonomia di Bloom**: Classificazione domande per livelli cognitivi (ricordare, comprendere, applicare, analizzare, valutare, creare)
4.  **Ottimizzazione Contesto**: Bilanciamento lunghezza domande/risposte per la lettura su mobile

**Tipi Supportati**
-   **Definizioni**: "Cos'è X?" → Spiegazione concisa con esempi
-   **Applicazioni**: "Come si usa X?" → Passaggi procedurali con contesto
-   **Confronti**: "Differenza tra X e Y?" → Tabelle comparative
-   **Cause-Effetto**: "Perché accade X?" → Relazioni causali
-   **Esempi**: "Esempio di X?" → Casi di studio concreti

**Metadati Avanzati**
-   Timestamp precisi per riferimenti al video originale
-   Punteggio di difficoltà basato sulla complessità linguistica
-   Tag automatici per la categorizzazione
-   Punteggio di confidenza dell'AI sull'accuratezza
-   Collegamenti semantici tra flashcard correlate

#### 📚 **Quiz Adattivi Multi-Formato**

**Scelta Multipla Intelligente**
-   Generazione di distrattori plausibili basati su errori comuni
-   Bilanciamento della difficoltà attraverso analisi statistica
-   Feedback immediato con spiegazioni dettagliate
-   Domande adattive basate sulla cronologia delle prestazioni

**Cloze Deletion (Completamento di Spazi Vuoti)**
-   Identificazione automatica di parole chiave critiche
-   Spazi vuoti multipli per frasi complesse
-   Suggerimenti progressivi per supportare l'apprendimento
-   Variazioni con sinonimi per un test completo

**Vero/Falso con Giustificazioni**
-   Affermazioni basate su fatti estratti dal video
-   Richiesta di giustificazione per ogni risposta
-   Analisi del ragionamento dell'utente per feedback personalizzato
-   Database di errori comuni per miglioramento continuo

**Scala di Difficoltà Dinamica**
-   Tracciamento delle prestazioni in tempo reale per aggiustamenti
-   Machine learning per la previsione del livello di sfida ottimale
-   Personalizzazione basata sullo stile di apprendimento individuale
-   A/B testing continuo per l'ottimizzazione degli algoritmi

#### 📚 **Mappe Mentali Automatiche**

**Struttura Gerarchica Intelligente**
-   Concetti principali identificati tramite analisi di frequenza
-   Sotto-argomenti organizzati per flusso logico
-   Livelli di profondità ottimizzati per la visualizzazione su mobile
-   Riferimenti incrociati tra rami correlati

**Connessioni Semantiche**
-   Word embedding per il rilevamento della similarità
-   Mappatura delle relazioni causali
-   Sequenze temporali per argomenti cronologici
-   Dipendenze dei prerequisiti per i percorsi di apprendimento

**Visualizzazione Interattiva**
-   Gesti touch per una navigazione fluida
-   Zoom e pan per l'esplorazione dei dettagli
-   Comprimi/espandi nodi per la gestione del focus
-   Codifica a colori per la differenziazione delle categorie

**Capacità di Esportazione**
-   JSON strutturato per integrazioni esterne
-   Grafica vettoriale SVG per qualità di stampa
-   PNG rasterizzato per la condivisione sui social
-   HTML interattivo per l'incorporamento web

#### 📚 **Riassunti Strutturati Multi-Livello**

**Organizzazione Gerarchica**
-   Sommario esecutivo (2-3 frasi)
-   Concetti principali (punti elenco prioritari)
-   Spiegazioni dettagliate con esempi
-   Punti chiave e azioni da intraprendere

**Evidenziazione Intelligente**
-   Evidenziazione di parole chiave basata sull'importanza
-   Citazioni dirette dal video con timestamp
-   Dati statistici e numeri chiave
-   Definizioni di termini tecnici

**Timeline Navigabile**
-   Organizzazione cronologica degli argomenti
-   Link per passare direttamente a punti specifici del video per approfondimenti
-   Indicatori di progresso per il tracciamento del completamento
-   Segnalibri per riferimenti rapidi

## 🏗️ Architettura Tecnica Dettagliata

### Stack Tecnologico Completo

#### **Frontend Mobile (React Native)**


**Core Framework & Development Environment**
L'applicazione utilizza React Native 0.72+ con TypeScript in modalità strict per garantire type safety completa e ridurre errori runtime. Metro bundler viene configurato con transform personalizzati per ottimizzare bundle size e performance. L'integrazione Flipper permette debugging avanzato con network inspection, database viewer e performance profiling. CodePush abilita aggiornamenti over-the-air per fix critici e feature rollout graduale senza passare per app store review.

**Navigation & State Management Architecture**
React Navigation 6.x implementa navigazione type-safe con parametri tipizzati, supportando deep linking e state restoration. Redux Toolkit gestisce stato globale con slice pattern per modularity, mentre React Query ottimizza server state con caching intelligente, background refetch e optimistic updates. AsyncStorage fornisce persistenza locale per user preferences, offline data e session recovery.

**UI/UX Component System**
React Native Elements fornisce component library consistente con tema personalizzato e accessibilità integrata. Reanimated 3 gestisce animazioni performanti con worklet thread separato, abilitando 60fps smooth transitions. Gesture Handler intercetta touch events nativi per interazioni fluide come swipe, pinch e pan. Vector Icons supporta icon sets personalizzati con font optimization per ridurre app size.

**Performance Optimization Strategy**
Implementazione sistematica di React.memo per prevenire re-render inutili, useMemo/useCallback per operazioni costose come sorting e filtering. FlatList virtualization gestisce dataset grandi con rendering on-demand, mentre Image lazy loading con progressive enhancement riduce memory usage e miglira perceived performance. Bundle splitting e code splitting riducono initial load time.

#### **Backend Infrastructure (Supabase)**

**Database Schema & Architecture**
PostgreSQL database strutturato con tabelle ottimizzate per performance e scalabilità. Users table gestisce profili utente con preferenze apprendimento in formato JSONB per flessibilità. Videos table centralizza metadata video YouTube con transcript processed (da Gemini) e categorizzazione automatica (da Gemini). Flashcards table implementa relazioni many-to-many tra users e videos, includendo metadata per spaced repetition algorithm. Study Sessions tracking permette analytics dettagliate e progress monitoring. User Progress table aggrega metriche a lungo termine per insights e gamification.

**Edge Functions & Serverless Logic**
Supabase Edge Functions (Deno runtime) gestiscono le chiamate all'**API Gemini** per la generazione e l'analisi dei contenuti. Queste funzioni orchestrano l'invio del video/trascrizione all'API Gemini e la ricezione/parsing dei risultati. Functions isolate permettono scaling automatico e reduced latency through geographic distribution. Webhook handlers processano YouTube video updates e user events in real-time. Background jobs gestiscono batch processing per video analysis e user analytics computation.

**Real-time Capabilities**
PostgreSQL built-in pub/sub system abilita real-time updates per multiplayer features, leaderboards live e collaborative study sessions. Row Level Security (RLS) policies garantiscono data isolation e privacy compliance. Connection pooling ottimizza database performance sotto load elevato.

### 🤖 AI Content Generation Flow (con API Gemini)

#### 📥 1. Input
- L’utente inserisce un link YouTube o carica un video.
- Un Edge Function Supabase attiva il parsing dell’ID del video e recupera i metadati necessari tramite l'API di YouTube (come titolo, descrizione, e se disponibili, trascrizioni ufficiali).

#### 🔊 2. Trascrizione e Comprensione del Contenuto Video
- L'Edge Function invia il link del video (o l'audio/video stesso, se caricato direttamente) all'**API Gemini**.
- L'API Gemini, grazie alle sue capacità multimodali, processa il contenuto video:
    - Esegue la trascrizione dell'audio, idealmente con timestamp a livello di parola o frase.
    - Comprende il contesto semantico del video.
- Se una trascrizione di alta qualità è già disponibile tramite l'API di YouTube, questa può essere passata come input testuale diretto a Gemini per l'elaborazione semantica, potenzialmente accelerando il processo e riducendo i costi.

#### 🧠 3. Elaborazione Semantica e Generazione Contenuti con API Gemini
- La trascrizione e/o la comprensione del video ottenuta da Gemini (o la trascrizione preesistente) viene utilizzata come input per ulteriori chiamate all'**API Gemini** (ad esempio, usando un modello come Gemini 1.5 Pro).
- Vengono inviati prompt specifici e strutturati all'API Gemini per generare:
    - **Flashcard**: Seguendo la tassonomia di Bloom, tipi di domande/risposte vari, definizioni, ecc.
    - **Quiz**: Domande a scelta multipla (con distrattori), cloze deletion (fill-in-the-blank), vero/falso con giustificazioni.
    - **Mappa Mentale**: Una struttura dati gerarchica (es. JSON) che rappresenta i concetti chiave e le loro relazioni.
    - **Riassunto Strutturato**: Riassunti a più livelli di dettaglio, dai punti chiave a spiegazioni più elaborate.
- Ogni prompt è ingegnerizzato per massimizzare la qualità e la pertinenza dell'output per il tipo di contenuto desiderato.

#### 🗂️ 4. Salvataggio Contenuti
- I contenuti strutturati (JSON, testo) restituiti dall'API Gemini vengono parsati e salvati nelle tabelle appropriate del database Supabase:
  - `flashcards`, `summaries`, `mindmap_data`, `quiz_items` (tutti relazionati al `video_id`).
- I metadati includono:
  - Eventuali confidence score forniti da Gemini o stimati.
  - Timestamp (se correlabili al video).
  - User ID.
  - Versione del modello Gemini utilizzata (per tracciabilità e futuri aggiornamenti).

#### 🔄 5. Update Realtime Client
- Tramite le funzionalità realtime/pubsub di Supabase:
  - Il frontend React Native riceve una notifica che i contenuti sono pronti.
  - L'interfaccia utente si aggiorna dinamicamente per mostrare le flashcard, i quiz, la mappa mentale e il riassunto generati.