# 📋 LinguaNerd — Diario di Progetto

> **Istruzioni per Claude:** Leggi questo file all'inizio di ogni sessione per capire lo stato del progetto e continuare il lavoro. L'utente allegherà anche i file del progetto (index.html + cartella data/).

---

## 🎯 Cos'è LinguaNerd

App web per l'apprendimento delle lingue, stile Duolingo ma personalizzata. Funziona come **Progressive Web App (PWA)** deployata su **Netlify**. L'utente studia lingue straniere tramite flashcard, quiz, duelli e statistiche.

**Obiettivo reale:** Creare un'app che generi la stessa dipendenza degli scacchi online (rating, streak, progressione visibile) ma applicata allo studio del ceco. L'utente perde tempo ogni giorno sugli scacchi — l'idea è sostituire quella abitudine con LinguaNerd.

**Lingue supportate:** Italiano, Inglese, Ceco, Spagnolo, Francese, Rumeno, Hindi 🇮🇳
**Stack:** HTML + React (CDN) + Babel standalone — tutto in un singolo `index.html`
**Deploy:** Netlify (drag & drop dello ZIP, oppure via GitHub)

---

## 📁 Struttura del Progetto

```
linguanerd/
├── index.html              ← App completa (UI + logica React)
└── data/
    ├── words.json          ← Database parole (25 parole)
    ├── phrases.json        ← Database frasi (30 frasi)
    ├── grammar.json        ← Database grammatica (12 regole)
    └── lessons.json        ← Database lezioni (10 lezioni)
```

---

## ✅ Cosa è stato fatto (cronologico)

### Sessione 1 — Setup base
- Progetto esistente ricevuto dall'utente (`linguanerd.html`)
- App già funzionante con: Home, Studia, Test, Duelli, Stats
- Layout responsive mobile + desktop (PC a 3 colonne)
- Salvataggio progresso con `localStorage`
- Sistema CEFR per misurare il livello (A1→C2)

### Sessione 1 — Dashboard Studia
- Aggiunta dashboard "Sistema di Studio" nella sezione Studia
- Griglia 2×2 di 8 sezioni: Parole, Verbi, Grammatica, Lezioni, Esercizi, Pronuncia, Frasi, Quiz Rapido
- Ogni card ha colore unico, icona, descrizione e barra di progresso
- Cliccando su una card si entra nella schermata dedicata
- Bottone "‹ Torna" per tornare alla dashboard

### Sessione 1 — Separazione Database
- Decisione architetturale: separare i dati dall'HTML
- `index.html` carica `data/words.json` via `fetch()` all'avvio
- Funzione `normalizeWords()` converte il formato JSON al formato interno
- Loading screen animato mentre il DB si carica
- Fallback se il JSON non si carica

### Sessione 1 — Creazione Database JSON
- `words.json` — 25 parole con traduzioni 6 lingue + esempi + livello CEFR
- `phrases.json` — 30 frasi per situazione + livello + pronuncia
- `grammar.json` — 12 regole grammaticali con spiegazioni ed esercizi
- `lessons.json` — 10 lezioni lineari con obiettivi collegati a parole/frasi/grammatica

### Sessione 1 — Visione e Roadmap
- Discussione sulla validità del progetto: **valido e fattibile**
- Identificato il meccanismo chiave: **gamification come gli scacchi**
- Il rating Elo, la streak e la progressione visibile sono il cuore dell'app
- Definito il roadmap in 4 fasi
- Decisione di passare a GitHub per gestire il progetto

---

## 🗺️ Roadmap — 4 Fasi

### Fase 1 — Struttura e contenuto ← SIAMO QUI
- [ ] Far funzionare le 8 sezioni (Lezioni, Grammatica, Frasi, Pronuncia...)
- [ ] Caricare tutti i JSON nell'app (ora carica solo words.json)
- [ ] Popolare i database con molto più contenuto
- [x] Setup GitHub + Netlify automatizzato

### Fase 2 — Gamification e dipendenza
- [ ] Rating Elo più emotivo (sale/scende in modo visibile)
- [ ] Sessioni brevi con ricompensa finale
- [ ] Sistema "ancora una" — la sfida continua
- [ ] Rating che decade se non torni ogni giorno
- [ ] Notifiche / reminder giornaliero

### Fase 3 — Grafica e UX
- [ ] Rifinire interfaccia mobile e desktop
- [ ] Animazioni e microinterazioni
- [ ] Identità visiva coerente

### Fase 4 — Distribuzione
- [ ] PWA completa (manifest.json + sw.js)
- [ ] Far provare ad altri utenti
- [ ] Valutare crescita oltre uso personale

---

## 🏗️ Architettura index.html (punti chiave)

### Caricamento DB
```javascript
fetch("data/words.json")
  .then(r => r.json())
  .then(data => {
    WORDS_DB = normalizeWords(data.words);
    DB_LOADED = true;
  });
// ⚠️ DA FARE: caricare anche phrases.json, grammar.json, lessons.json
```

### Componenti React principali
- `App` — root, gestisce screen (home/app) e tab
- `HomeScreen` — schermata iniziale con selezione lingue
- `StudiaTab` — router tra dashboard e sezione
- `StudiaDashboard` — griglia 8 sezioni
- `StudiaSectionScreen` — sessione di studio dentro una sezione
- `TestTab` — quiz a tempo
- `DuelliTab` — modalità sfida (ancora stub)
- `StatsTab` — statistiche + mappa CEFR
- `PCSidebar` / `PCRightPanel` — layout desktop

### Convenzioni ID nei JSON
- Parole: `w001`, `w002`, ...
- Frasi: `p001`, `p002`, ...
- Grammatica: `g001`, `g002`, ...
- Lezioni: `l001`, `l002`, ...
- Esercizi: `g001_e1`, `g001_e2`, ...

---

## 🛠️ Note tecniche importanti

- **React via CDN** — nessun build step, tutto in un file
- **Babel standalone** — transpila JSX nel browser
- **Service Worker** (`sw.js`) — referenziato ma non ancora creato
- **`manifest.json`** — referenziato ma non ancora creato
- **localStorage** funziona nell'app reale per salvare i progressi
- Consegna a Netlify: sempre uno **ZIP** con index.html + cartella data/

---

## 💬 Stile di lavoro con l'utente

- Sessioni giornaliere con questo diario come punto di continuità
- L'utente vuole vedere i risultati nell'interfaccia Claude (present_files)
- Preferisce lavorare un pezzo alla volta
- Vuole sempre lo ZIP completo quando ci sono più file
- Le decisioni architetturali vengono discusse prima di implementare
- **Prossimo step:** far funzionare le altre sezioni (Lezioni, Grammatica, Frasi...)

---

### Sessione 2 — GitHub + Netlify + Hindi (2026-03-10)
- ✅ Setup GitHub → Netlify: deploy automatico configurato (ogni push aggiorna il sito)
- ✅ Aggiunto Hindi 🇮🇳 (`hi`) a tutte le 25 parole in `words.json` (traduzioni + esempi in devanagari)
- ✅ Aggiunto Hindi nei selettori lingua di `index.html` (flag 🇮🇳, voce `hi-IN` per Web Speech API)
- ✅ Repo: `FIB66/LINGUANERD` — branch `main`
- ✅ Diario spostato su GitHub come `PROGETTO_LINGUANERD.md`
- **Lingue supportate ora:** Italiano, Inglese, Ceco, Spagnolo, Francese, Rumeno, Hindi
- **Flusso di lavoro:** zip del repo → allega a Claude → Claude modifica → carica su GitHub → Netlify si aggiorna

---

## 🔜 Prossimo step suggerito
- Far funzionare le altre sezioni della dashboard (Lezioni, Grammatica, Frasi...)
- Caricare `phrases.json`, `grammar.json`, `lessons.json` nell'app

---

*Ultimo aggiornamento: 2026-03-10 — Sessione 2 completa*
