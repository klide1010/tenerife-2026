# Tenerife 2026

PWA travel planner per Tenerife · 15–19 ottobre 2026 · Andrea & Michela, ospiti di Davide.
Replica in salsa canaria di [islanda-2026](https://github.com/klide1010/islanda-2026).

## File

- `tenerife_2026.html` — l'app completa (HTML + CSS + JS in un file solo)
- `manifest.webmanifest`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` — PWA installabile
- `icon.svg` — sorgente dell'icona

## Tab

| Tab | Cosa c'è |
|-----|----------|
| Piano | Programma di Davide blocco per blocco + **slot liberi** tratteggiati da colmare. Ogni slot ha un campo note salvato sul telefono. |
| Liberi | Ore libere vs ore con Davide, per giorno e totali, con barra 08:00–23:30. |
| Spese | Solo EUR. Importi «da inserire» si compilano toccandoli; spunte pagato/da pagare; voci custom. |
| Meteo | Open-Meteo sulla località del giorno (costa sud, Teide, costa ovest). Fallback medie di ottobre. |
| Info | Voli FR2830/FR2831 (G8WW6E), Lella's Home, casa di Davide, cose da prenotare, info pratiche. |

## Come colmare uno slot libero

In `tenerife_2026.html`, array `GIORNI` → `blocchi`. Uno slot libero è:

```js
{ id: 'd1-pom', ora: '15:30', fine: '19:00', tipo: 'libero', titolo: 'Pomeriggio libero', desc: '…' }
```

Per riempirlo cambia `tipo` in `'noi'`, aggiorna `titolo`/`desc` e, se serve, aggiungi `places: [{ label, q }]` per il link Maps.
Se l'attività occupa solo una parte dello slot, spezza il blocco in due (uno `noi` e uno `libero` con il residuo).

## Convenzioni

- `stima: true` → Davide non ha dato un orario preciso ("mattina", "sera"): nell'app compare «~».
- `book: true` → da prenotare. `flex: true` → "senza programma rigido" (domenica).
- `DAY_START` / `DAY_END` → finestra della giornata usata per il calcolo del tempo libero.

## Deploy

File statici: basta copiarli su un hosting qualsiasi (GitHub Pages, Cloudflare Pages, cartella del tema WordPress come per Islanda). Nessun proxy PHP: Tenerife non ha bisogno di feed strade/allerte.
