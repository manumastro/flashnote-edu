# Regole del Progetto FlashNote EDU

## Stack Tecnologico

Il progetto FlashNote EDU è costruito utilizzando il seguente stack tecnologico:

### Frontend Mobile
- **React Native** con TypeScript
- **React Navigation** per la navigazione
- **React Context** per la gestione dello stato
- **RevenueCat** per gli acquisti in-app

### Backend & AI
- **Supabase** (Database PostgreSQL + Edge Functions)
- **Node.js/TypeScript** per le API
- **WhisperX** per la trascrizione audio
- **Google Gemini Pro** per la generazione di Q&A
- **Algoritmo SM-2** per la ripetizione dilazionata

### Infrastruttura
- **Supabase Storage** per file audio e JSON
- **Supabase Auth** per l'autenticazione
- **Stripe** per i pagamenti
- **Mixpanel** per l'analisi

### Prerequisiti di Sviluppo
- Node.js 18+
- React Native CLI
- Supabase CLI
- Docker (per WhisperX)