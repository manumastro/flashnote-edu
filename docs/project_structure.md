# Struttura del Progetto FlashNote EDU

Questo documento descrive la struttura del repository del progetto FlashNote EDU.

```
flashnote-edu/
├── .gitignore
├── .trae/                  # File di configurazione specifici per Trae AI
│   ├── .ignore
│   └── rules/
│       └── project_rules.md  # Regole e configurazioni del progetto
├── README.md               # Descrizione generale del progetto
├── docs/                   # Documentazione aggiuntiva
│   ├── roadmap.md          # Roadmap di sviluppo del progetto
│   └── tech_stack.md       # Stack tecnologico utilizzato
│   └── project_structure.md  # Struttura del progetto
├── package-lock.json
├── package.json
└── src/
    └── FlashNoteEDUApp/    # Applicazione React Native
        ├── .bundle/
        ├── .eslintrc.js
        ├── .gitignore
        ├── .prettierrc.js
        ├── .watchmanconfig
        ├── App.tsx
        ├── Gemfile
        ├── README.md
        ├── __tests__/
        ├── android/        # Progetto Android nativo
        ├── app.json
        ├── babel.config.js
        ├── index.js
        ├── ios/            # Progetto iOS nativo
        ├── jest.config.js
        ├── metro.config.js
        ├── package-lock.json
        ├── package.json
        ├── public/
        └── tsconfig.json
```

## Descrizione delle Directory Principali

*   `.trae/`: Contiene file di configurazione e regole specifiche per l'ambiente di sviluppo Trae AI.
*   `docs/`: Contiene la documentazione aggiuntiva del progetto, come la roadmap e lo stack tecnologico.
*   `src/FlashNoteEDUApp/`: Questa è la directory principale dell'applicazione React Native. Contiene tutto il codice sorgente, le configurazioni e le risorse relative all'app mobile.
    *   `android/`: Contiene il codice specifico per la piattaforma Android.
    *   `ios/`: Contiene il codice specifico per la piattaforma iOS.

Questa struttura mira a mantenere il progetto organizzato e facile da navigare, separando il codice sorgente dell'applicazione dalla documentazione e dai file di configurazione del repository.