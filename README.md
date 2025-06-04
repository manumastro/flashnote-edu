# FlashNote EDU 🎓📱

> Trasforma video-lezioni YouTube in flashcard e quiz adattivi in meno di 30 secondi

## 📋 Panoramica del Progetto

FlashNote EDU è un'applicazione mobile che rivoluziona l'apprendimento digitale convertendo automaticamente video educativi di YouTube in **flashcard intelligenti**, **quiz adattivi**, **mappe mentali** e **riassunti strutturati**. Utilizza intelligenza artificiale avanzata per estrarre contenuti chiave e creare materiali di studio personalizzati con sistema di ripetizione dilazionata (spaced repetition).

### 🎯 Problema Risolto
- Il 90% degli studenti usa strumenti AI per studiare ma mancano soluzioni integrate mobile-first
- Nessuna app unisce efficacemente "video → flashcard + quiz" con gamification
- Google offre riassunti video ma non spaced repetition personalizzata

### 💡 Valore Unico
- **Velocità**: < 30 secondi da video a contenuti di studio
- **Multi-formato**: Flashcard, quiz, mappe mentali, riassunti
- **Gamification**: Streaks, badge, statistiche avanzate
- **Cross-platform**: Export verso Anki/Quizlet/PDF
- **Mobile-first**: Esperienza ottimizzata per smartphone

## 🎓 Funzionalità Principali

### 📚 Generazione Contenuti AI

**Flashcard Intelligenti**
- Creazione automatica da trascrizioni video
- Q&A pairs basati su tassonomia di Bloom
- Supporto per diversi tipi: definizioni, applicazioni, analisi
- Metadata con timestamp per riferimenti video

**Quiz Adattivi**
- Multiple choice generati automaticamente
- Cloze deletion (riempimento spazi)
- True/False con giustificazioni
- Difficulty scaling basato su performance utente

**Mappe Mentali Automatiche**
- Struttura gerarchica dei concetti chiave
- Connessioni semantiche tra argomenti
- Export in formato JSON/SVG
- Visualizzazione interattiva touch-friendly

**Riassunti Strutturati**
- Bullet points organizzati per sezioni
- Evidenziazione concetti chiave
- Timeline degli argomenti con timestamp
- Abstract esecutivo per revisione rapida

### 🧠 Sistema di Apprendimento

**Spaced Repetition (SM-2)**
- Algoritmo scientifico per ottimizzare ritenzione
- Intervalli personalizzati basati su performance
- Curve di oblio individualmente calibrate
- Predizione accuracy per prossime sessioni

**Modalità Studio Multiple**
- **Focus Mode**: Solo flashcard critiche
- **Quick Review**: Sessioni da 5-10 minuti
- **Deep Dive**: Studio completo con mappe mentali
- **Challenge Mode**: Quiz competitivi con timer

**Progress Tracking Avanzato**
- Heatmap di attività giornaliera
- Curve di apprendimento per argomento
- Confidence tracking per ogni concetto
- Previsioni tempo necessario per mastery

## 🏗️ Architettura Tecnica

### Stack Tecnologico

**Frontend Mobile**
- React Native con TypeScript
- React Navigation per navigazione
- React Context per state management
- RevenueCat per in-app purchases

**Backend & AI**
- Supabase (Database PostgreSQL + Edge Functions)
- Node.js/TypeScript per API
- WhisperX per trascrizione audio
- Google Gemini Pro per generazione Q&A
- Algoritmo SM-2 per spaced repetition

**Infrastruttura**
- Supabase Storage per file audio/JSON
- Supabase Auth per autenticazione
- Stripe per pagamenti
- Mixpanel per analytics

### Architettura High-Level

```
┌─────────────────────┐          ┌───────────────────────────┐
│    Mobile App       │          │    Landing Page / Web     │
│ React Native (TS)   │          │   (Typedream / Marketing) │
│                     │          └───────────┬───────────────┘
│ - Login / Auth      │                      │
│ - Aggiungi Video    │                      │
│ - Review Flashcards │                      │
└───────┬─────────────┘                      │
        │                                    │
        │ (API Calls)                        │
        ▼                                    │
┌────────────────────────────────────────────────────────────────┐
│      Supabase Edge Functions (Node.js / TS)                   │
│                                                              │
│  • /process-video           • /generate-cards                 │
│  • /review                  • /check-subscription              │
│                                                              │
│  – Gestisce:                                                 │
│    • Download audio YouTube (ytdl-core)                       │
│    • Invocazione WhisperX / trascrizione                      │
│    • Invocazione LLM per Q/A generation                       │
│    • Logica SM-2 (spaced repetition)                          │
│    • Verifica piano Stripe / RevenueCat                       │
└───────┬──────────────────────────────────────────┬──────────────┘
        │                                          │
        ▼                                          ▼
┌───────────────────────┐                ┌───────────────────────┐
│    Supabase Database  │                │  Supabase Storage     │
│    (Postgres)         │                │  (File audio .mp3,    │
│                       │                │   JSON trascrizioni)  │
│  • users              │                └───────────────────────┘
│  • videos             │
│  • transcriptions     │
│  • flashcards         │
│  • user_flashcards    │
│  • subscriptions      │
└───────────────────────┘
```

## 📊 Schema Database

### Tabelle Principali

**users**
```sql
id (UUID, PK)
email (text, unique)
password_hash (text)
plan (text: free/pro/school)
streak_days (int)
created_at (timestamp)
```

**videos**
```sql
id (UUID, PK)
user_id (UUID, FK → users.id)
youtube_url (text)
supabase_audio_path (text)
status (enum: pending/processing/done)
created_at (timestamp)
```

**flashcards**
```sql
id (UUID, PK)
transcription_id (UUID, FK → transcriptions.id)
question (text)
answer (text)
type (enum: basic/cloze/mcq)
difficulty (int 1-5)
metadata (jsonb) -- timestamp, riferimenti
created_at (timestamp)
```

**quizzes**
```sql
id (UUID, PK)
transcription_id (UUID, FK → transcriptions.id)
question (text)
options (jsonb) -- array opzioni MCQ
correct_answer (text)
explanation (text)
type (enum: mcq/true_false/fill_blank)
```

**mind_maps**
```sql
id (UUID, PK)
transcription_id (UUID, FK → transcriptions.id)
nodes (jsonb) -- struttura nodi e connessioni
root_concept (text)
layout_data (jsonb) -- posizioni, styling
```

**summaries**
```sql
id (UUID, PK)
transcription_id (UUID, FK → transcriptions.id)
content (jsonb) -- bullet points strutturati
key_concepts (text[])
timeline (jsonb) -- timestamp -> concetto
abstract (text)
```

**user_flashcards** (Spaced Repetition)
```sql
id (UUID, PK)
user_id (UUID, FK → users.id)
flashcard_id (UUID, FK → flashcards.id)
interval (float)
repetition (int)
easiness (float)
next_review (date)
```

## 🔄 Pipeline di Elaborazione

### Flusso YouTube → Flashcard

1. **Input Video**: Utente inserisce URL YouTube
2. **Download Audio**: Edge Function estrae audio con ytdl-core
3. **Trascrizione**: WhisperX genera testo con timestamps
4. **Generazione Q&A**: Gemini Pro crea 20 domande/risposte
5. **Salvataggio**: Flashcard salvate nel database
6. **Review**: Sistema SM-2 per ripetizione dilazionata

```
[YouTube URL] → [Audio Extract] → [WhisperX] → [LLM Q&A] → [Flashcards] → [SM-2 Review]
```

## 🚀 API Endpoints

### Core Endpoints

| Endpoint | Metodo | Descrizione |
|----------|--------|-------------|
| `/process-video` | POST | Avvia pipeline video → flashcard |
| `/review` | GET | Ottiene flashcard da ripassare oggi |
| `/review` | POST | Invia feedback qualità (0-5) per SM-2 |
| `/generate-cards` | POST | Genera Q&A da trascrizione |
| `/check-subscription` | POST | Verifica stato abbonamento |
| `/user-stats` | GET | Statistiche utente (streak, progress) |

### Autenticazione
- Supabase Auth con JWT tokens
- Support per email/password e OAuth

## 📱 Navigazione UI

### Schermate Principali

1. **Splash/Login**: Autenticazione utente
2. **Dashboard**: Hub principale con azioni rapide
3. **Add Video**: Input URL YouTube e processing
4. **Review**: Sessione studio flashcard con SM-2
5. **Stats**: Grafici progresso e achievements
6. **Profile**: Impostazioni e gestione abbonamento

### Flow Utente
```
Login → Dashboard → [Add Video | Review | Stats] → Profile
```

## 💰 Modello di Business

### Piani di Abbonamento

| Piano | Prezzo | Funzionalità |
|-------|--------|--------------|
| **Free** | 0€ | 3 video/mese, 30 flashcard, ads |
| **Student Pro** | 7€/mese | Illimitato, export Anki, dark mode |
| **School Pack** | 499€/anno | 100 licenze + dashboard docente |

### Metriche Target
- **Break-even**: 300 abbonati Pro
- **CAC/LTV ratio**: 1:6 (Student Pro)
- **Retention D7**: 40% target

## 🔧 Setup Sviluppo

### Prerequisiti
```bash
# Node.js 18+
# React Native CLI
# Supabase CLI
# Docker (per WhisperX)
```

### Installazione Rapida
```bash
# Clone repository
git clone https://github.com/username/flashnote-edu
cd flashnote-edu

# Install dependencies
npm install

# Setup Supabase
supabase init
supabase start

# Setup environment
cp .env.example .env
# Configura API keys (Gemini, Stripe, etc.)

### Quick Start

Per iniziare con il progetto FlashNote EDU, segui questi semplici passaggi:

1.  **Clona il repository:**
    ```bash
git clone https://github.com/tuo-utente/flashnote-edu.git
cd flashnote-edu
    ```

2.  **Installa le dipendenze (per il frontend web):**
    ```bash
npm install
    ```

3.  **Avvia l'applicazione web:**
    ```bash
npm start
    ```
    Questo avvierà un server di sviluppo e aprirà l'applicazione nel tuo browser predefinito.

### Sviluppo Frontend Mobile (React Native)

Per lavorare sul frontend mobile, segui questi passaggi:

1.  **Assicurati di avere i prerequisiti di sviluppo installati:**
    - Node.js 18+
    - React Native CLI (installabile con `npm install -g react-native-cli`)
    - Supabase CLI
    - Docker

2.  **Installa le dipendenze del progetto mobile:**
    ```bash
cd src/FlashNoteEDUApp
npm install
    ```

3.  **Avvia l'applicazione mobile:**
    Puoi avviare l'applicazione mobile direttamente dalla directory radice del progetto:
    ```bash
npm run start:mobile
    ```
    Questo avvierà il Metro Bundler di React Native. Dovrai poi avviare l'applicazione su un emulatore o un dispositivo fisico (es. `npx react-native run-android` o `npx react-native run-ios` dalla directory `src/FlashNoteEDUApp`).

# Run development
npm run dev
```

### Variabili Ambiente
```bash
SUPABASE_URL=your_supabase_url
SUPABASE_ANON_KEY=your_anon_key
GEMINI_API_KEY=your_gemini_key
STRIPE_SECRET_KEY=your_stripe_key
REVENUECAT_API_KEY=your_revenuecat_key
```

## 🧪 Testing Strategy

### Test Coverage
- **Unit Tests**: Jest per funzioni SM-2 e utilities
- **Integration Tests**: Edge Functions e DB operations  
- **E2E Tests**: Detox per flow completi mobile
- **A/B Tests**: Mixpanel + GPT-Analytics per UX

### Quality Assurance
- ESLint + Prettier per code quality
- TypeScript per type safety
- Sentry per crash reporting
- Performance monitoring con Supabase Analytics

## 📈 Metriche e Analytics

### KPI Principali
- **Activation**: 60% completano primo deck
- **Retention D7**: 40% target
- **Revenue**: 5% conversion Free → Pro
- **Engagement**: Streak giornaliero medio

### Tools Monitoring
- Mixpanel per user behavior
- Supabase Analytics per backend metrics
- RevenueCat per subscription analytics
- Sentry per error tracking

## 🔒 Privacy e Sicurezza

### Data Protection
- GDPR compliant data handling
- Audio files processati e eliminati dopo trascrizione
- JWT tokens per autenticazione sicura
- Encryption at rest per dati sensibili

### Content Safety
- Fair use per trascrizioni (solo testo)
- Cache locale per evitare copyright issues
- Chain-of-verification per ridurre AI hallucinations

## 🚀 Deployment

### Production Environment
- **Mobile**: TestFlight (iOS) + Google Play Console (Android)
- **Backend**: Supabase Edge Functions auto-deploy
- **Database**: Supabase managed PostgreSQL
- **Storage**: Supabase Storage per file audio/JSON

### CI/CD Pipeline
```bash
# GitHub Actions workflow
Build → Test → Deploy → Monitor
```

## 🤝 Contributing

### Development Workflow
1. Fork repository
2. Create feature branch
3. Implement con vibe coding (Cursor/Replit)
4. Test thoroughly
5. Submit pull request

### Code Style
- TypeScript strict mode
- Functional components (React)
- Tailwind CSS per styling
- Conventional commits

## 📞 Support

### Community
- Discord server per developer community
- GitHub Issues per bug reports
- Documentation su GitBook

### Business Contact
- Email: hello@flashnoteedu.app
- Website: https://flashnoteedu.app
- Twitter: @FlashNoteEDU

---

**Built with ❤️ using Vibe Coding principles**

*Trasforma ogni video in conoscenza, ogni ripetizione in padronanza.*