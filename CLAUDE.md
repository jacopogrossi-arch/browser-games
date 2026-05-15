# CLAUDE.md

This file gives Claude Code the context to work well in this repository.

---

## Chi lavora qui

Jacopo è un giovane italiano che studia fashion design ed economia, e in parallelo agli studi studia e applica l'AI — soprattutto automazioni e generazione video. Claude Code è il suo secondo cervello: lo usa sia per imparare che per costruire concretamente le cose su cui sta lavorando.

Sul piano tecnico, Jacopo non è uno sviluppatore. Usa Claude Code con una certa fluidità, capisce la logica dei workflow, ma non ha esperienza con API, n8n, o programmazione generale. Questo non è un limite — è il punto di partenza. Quando lavoro con lui, l'obiettivo non è fare le cose al suo posto: è fargli capire quello che stiamo costruendo insieme, perché domani potrebbe doverlo spiegare agli iscritti della sua community.

Il principio guida di questo repo: **semplice e funzionante batte elegante e complesso**. Non perché Jacopo non possa imparare cose complesse — ma perché il suo tempo vale di più sull'apprendimento e sulle decisioni strategiche.

---

## Struttura del repository

```
jackss-hq/
├── CLAUDE.md                        ← questo file
├── claude-signals.md                ← segnali dal Daily Log Agent (aggiornamento notturno)
├── n8n-automation/                  ← progetto automazione contenuti video
│   ├── overview.md                  — obiettivo, stack, pipeline, monetizzazione
│   ├── progress.md                  — stato avanzamento e note tecniche
│   ├── workflows/
│   │   └── workflow-01.md           — schema nodo-per-nodo del workflow attivo
│   └── prompts/
│       └── system-prompt.md         — system prompt Claude per generare gli script
├── ai-content-claude/               ← progetto apprendimento creativo AI image/video
│   ├── style-guide.md               — identità visiva, palette, prompt master
│   ├── platform-cheatsheet.md       — quale tool usare per cosa
│   ├── progress.md                  — log avanzamento homework
│   └── prompts/
│       ├── hw1-image-prompts.md     — prompt immagini Homework 1 (3 varianti + JSON)
│       └── hw2-video-prompts.md     — prompt video Homework 2 (Kling TTV/I2V)
├── snake3.html                      ← gioco Snake (progetto precedente)
└── tictactoe.html                   ← gioco Tic Tac Toe (progetto precedente)
```

---

## Notion — Jackss HQ

Jacopo gestisce tutta la sua vita e i suoi progetti in un unico workspace Notion chiamato **Jackss HQ**. È il suo sistema centrale, non uno strumento secondario. Contiene:

- **Studio personale** — appunti, risorse, percorsi di apprendimento su AI, moda, economia e tutto quello che studia in autonomia.
- **AI & Video Generation** — documentazione, idee, esperimenti e avanzamento sui progetti di automazione (n8n) e generazione creativa (immagini/video AI).
- **Salute e sport** — tracking allenamenti, obiettivi fisici, abitudini.

Quando si fa riferimento a documentazione personale, note di ricerca, o stato di un progetto che non è in questo repo, è probabile che si trovi su Notion / Jackss HQ. Usare il MCP Notion per accedervi se necessario.

---

## Git workflow

- Remote: https://github.com/jacopogrossi-arch/jackss-hq — default branch `master`
- Commit and push after every meaningful unit of work. Stage by filename, not `git add -A`.
- Commit messages: imperative mood, what changed and why.

---

## Segnali dal Daily Log Agent

Il file `claude-signals.md` nella root del repo viene aggiornato automaticamente ogni notte dall'agente `Jackss — Daily Log Processor`, che legge i Daily Log di Notion e rileva nuovi progetti, contatti, decisioni e obiettivi.

**All'inizio di ogni sessione:** leggi `claude-signals.md` se esiste. Per ogni blocco marcato `Da processare`:
1. Estrai le informazioni rilevanti (nuovi progetti, contatti, decisioni, obiettivi)
2. Salva nei file di memoria appropriati in `C:\Users\Jacopo Grossi\.claude\projects\D--ClaudeCodeTest\memory\`
3. Marca il blocco come `Processato` (sostituisci `Da processare` con `Processato`)
4. Salva con Edit

---

## AI Content Automation (n8n-automation/)

### La visione

L'obiettivo finale non è "fare video" — è costruire una macchina che pubblica contenuti sulla nicchia moda maschile quasi in automatico, così Jacopo può concentrarsi su Inverso e sulla community Skool. Il canale è anonimo (no faccia, voiceover AI sintetico): non per timidezza, ma perché un sistema anonimo è scalabile — non dipende da una presenza personale.

Questo progetto è anche un prodotto da vendere: la community Skool "Come costruire un brand di moda con €1.000" mostrerà esattamente questo sistema come esempio reale. Ogni cosa che costruiamo qui è potenzialmente materiale didattico.

### Stato attuale (10/05/2026)

**PIPELINE COMPLETA E FUNZIONANTE** — workflow end-to-end testato con successo.

Schema attivo:

```
Schedule Trigger (ogni 48h)
    ↓
Google Sheets — leggi foglio "Argomenti"
    ↓
Code JS — scegli argomento a caso + costruisci prompt
    ↓
Basic LLM Chain (claude-sonnet-4-6) → script TikTok 60s
    ↓
Code JS — unisci script + argomento + data
    ↓
Google Sheets — append row (Sheet1: data / argomento / script)
    +
HTTP Request — ElevenLabs → voiceover .mp3 (Voice: SAz9YHcvj6GT2YYXdXww)
    ↓
Google Drive — upload audio + rendi pubblico
    ↓
HTTP Request — HeyGen → genera video (Avatar: Adriana_Business_Front_public, 1080×1920)
    ↓
Wait 12 minuti
    ↓
HTTP Request — HeyGen status check → prende video_url
    ↓
Telegram — notifica con link video
```

### Prossimi step

- [ ] Aggiungere B-roll cinematografico con Kling API
- [ ] Aggiungere editing automatico con Shotstack (motion graphics, transizioni, testi)
- [ ] Integrare Buffer → pubblicazione social automatica
- [ ] Valutare avatar personalizzato su HeyGen

### Come collaborare su questo progetto

Jacopo sta imparando n8n e le API mentre costruisce. Non conosce ancora il funzionamento interno dei workflow, ma capisce il "perché" quando lo si spiega bene. Le spiegazioni devono arrivare fino al livello pratico — dove cliccare, cosa copiare, dove incollare. I termini tecnici vanno spiegati al primo utilizzo.

In n8n, le soluzioni visuali (drag-and-drop tra nodi) sono da preferire al codice custom. Quando il codice è necessario, va commentato in italiano. Ogni nuova API si testa prima con un nodo HTTP Request minimale, prima di integrarla nella pipeline. Ogni workflow deve terminare con un nodo Telegram — è la conferma visibile che la macchina ha funzionato.

### Stack

| Tool | Ruolo | Costo |
|------|-------|-------|
| n8n (self-hosted) | Orchestrazione workflow | ~€10/mese VPS |
| Claude API (claude-sonnet-4-6) | Generazione script | Pay per use |
| ElevenLabs | Voiceover sintetico | ~€22/mese |
| HeyGen | Video con avatar AI | ~€29/mese |
| Buffer | Scheduling social | ~€15/mese |
| Google Sheets | Content queue | Gratis |

### Note tecniche importanti

- n8n si avvia con `n8n start` → http://localhost:5678 (NON usare `npx n8n` con Node.js v24)
- Output di Basic LLM Chain → `{{ $json.text }}`
- `argomento` nel secondo Code node: `const argomento = $('Code in JavaScript').first().json.argomento`
- HeyGen: credenziale Header Auth con nome `X-Api-Key` (non OAuth)
- Il file Drive deve essere reso pubblico prima di passare l'URL a HeyGen
- Wait HeyGen: 12 minuti (7 non bastano per video da 60s)
- URI redirect OAuth Google: `http://localhost:5678/rest/oauth2-credential/callback`
- In caso di problemi di caricamento del browser: aprire n8n in modalità incognito

### Monetizzazione

Community Skool "Come costruire un brand di moda con €1.000" — €29-49/mese. Target: 100 iscritti = €2.900-4.900/mese.

---

## AI Image & Video Generation (ai-content-claude/)

### La visione

Questo progetto non è automazione — è un percorso di apprendimento creativo. L'obiettivo è sviluppare un "occhio" per la generazione di immagini e video AI di qualità professionale, applicato al settore moda/lusso. La skill, una volta acquisita, diventa un servizio da offrire a clienti.

> Questo progetto è completamente separato da quello n8n sopra. Non usa workflow automatizzati. Il lavoro è manuale, iterativo, creativo — più vicino alla post-produzione fotografica che alla programmazione.

### Brand di studio

Il sandbox è un'identità visiva luxury Italian fashion: giovane uomo italiano elegante (~25 anni) in Ferrari convertibile anni '80, campagna Toscana, strade con pini. L'aesthetic è old money — dolce vita, Riviera italiana, lusso senza ostentazione.

- Palette: amber `#F5E6C8`, gold `#C9A46A`, deep red `#8B0000`, near-black `#1E1E1E`
- Riferimenti fotografici: campagne Marlboro anni '70, Helmut Newton, Annie Leibovitz
- Riferimenti cinematografici: *Blade Runner 2049*, *Drive* (2011), film italiani anni '80

### Come collaborare su questo progetto

Su questo progetto si ragiona come un direttore della fotografia che dà note — non come un programmatore. La struttura naturale di ogni prompt è:

**SUBJECT & ACTION → SHOT TYPE → LENS → LIGHT → TEXTURE → COMPOSITION → STYLE → EMOTIONAL VISION**

I tool hanno caratteristiche diverse: Gemini/NanoBanana per iterazioni veloci e moodboard; Midjourney per qualità alta; Krea per ritratti fashion realistici; HiggsField per campagne ultra-realistiche; Kling per video (Text-to-Video e Image-to-Video).

### Stato avanzamento (07/05/2026)

- [x] Homework 1: 3 varianti prompt immagine + JSON prompt (Gemini)
- [x] Homework 1.3: Moodboard Pinterest (20-30 reference), keyword estetiche, 3 immagini coerenti
- [x] Homework 1.4: 3 Pinterest board per estetiche diverse, 3 immagini AI con estetica cinematica
- [x] Homework 1.5: Character creation via PromptEngine (text-based + image-based)
- [x] Homework 1.6: Campaign con PromptEngine + MidJourney con OmniReference
- [x] Homework 2: TTV e I2V con Kling (brand Ferrari/Toscana)
- [x] Homework 2.4: Camera movement — 3-4 versioni con movimenti diversi (Static/Push-in/Pan/Tracking)
- [x] Homework 2.5: LipSync con Kling — talking avatar
- [ ] Homework 3 (da assegnare)
- [ ] Risolvere bug reverse-motion in Kling I2V
- [ ] Testare Kling Pro vs standard
- [ ] Esplorare HiggsField per immagini di qualità superiore
- [ ] Costruire "Prompt System" riutilizzabile per questo brand
- [ ] Test griglia lens + lighting (35mm/daylight vs 85mm/tungsten vs 24mm/neon vs 50mm/backlit)
