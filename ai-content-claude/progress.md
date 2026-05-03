# Progress Log — AI Image & Video Generation

## Stato generale (03/05/2026)

Corso di generazione immagini e video AI. Progetto di studio: **luxury Italian fashion brand** (Ferrari, Toscana, old money aesthetic).

---

## Completato

### Homework 1 — Image Prompting (Gemini)
- [x] Brief creativo del brand definito
- [x] Guida al prompting professionale (SHOT + LENS + LIGHT + TEXTURE + COMPOSITION + STYLE) studiata
- [x] 3 varianti prompt immagine generate con Gemini:
  - V1: camera sinistra, wide angle 16–24mm
  - V2: camera destra, wide angle (speculare)
  - V3: camera sinistra, 85mm portrait (più intima)
- [x] JSON prompt creato in 2 versioni: 3D stylized + fotorealistica con negative_prompt
- [x] Risultati salvati su Notion (pagina "risultato" → Homework 1)

### Homework 2 — Video Generation (Kling)
- [x] TTV prompt scritto e video generato (tracking shot Ferrari → close-up → car away)
- [x] I2V prompt scritto usando frame di Homework 1 come immagine di partenza
- [x] Bug identificato: Ferrari va in reverse in alcuni output I2V → workaround da testare
- [x] Video I2V salvato su Google Drive

---

## In corso / Prossimi step

- [ ] **Homework 3** (da assegnare)
- [ ] Risolvere bug reverse-motion in Kling I2V
- [ ] Testare Kling Pro vs standard
- [ ] Esplorare HiggsField per immagini di qualità superiore rispetto a Gemini
- [ ] Costruire un "Prompt System" riutilizzabile per questo brand (Advanced Option A, HW1)
- [ ] Test griglia lens + lighting (Advanced Option B, HW1): 35mm/daylight vs 85mm/tungsten vs 24mm/neon vs 50mm/backlit

---

## Fonte dati Notion

Pagina principale: [AI CONTENT CLAUDE](https://www.notion.so/34f30837a9e680abb434cd560867fb56)
- Platform Cheat Sheet
- Primo Homework + risultati
- Secondo Homework + risultati
- Guida prompt
- Prompt JSON esempi
