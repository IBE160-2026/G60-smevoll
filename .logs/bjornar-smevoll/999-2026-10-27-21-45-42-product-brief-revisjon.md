# Product brief-revisjon

## 2026-10-27 kl. 21:45 — Bjørnar Smevoll

### Oppgave
Oppdatere product brief for FocusApp etter faglærerens tilbakemelding (`tilbakemelding-product-brief.md`, 2026-10-06): avklare plattform, lage testbare suksesskriterier og beskrive by- og streak-reglene konkret. I samme økt: git pull, flytting av `FocusApp`-mappen inn i repoet og oppsett av Claude Code-statuslinje.

### Plan
- `git pull` hentet commit `2891b2b` (tilbakemeldingen, `CLAUDE.md`, sesjonslogg-skillen).
- Gikk gjennom tilbakemeldingen og oppdaterte briefen med `bmad-product-brief` (oppdateringsmodus, coaching-vei): plattform → suksesskriterier → byen, streaks og lagring → konkurrenter og personvern → utkast.
- Polerte språk og struktur med `bmad-review` (lensene structure og prose).
- Alle beslutninger er logget i `.docs/planning-artifacts/briefs/brief-FocusApp-2026-09-15/.memlog.md`.

### Resultat
- `brief.md` er skrevet om (ukommittert). Hovedbeslutninger:
  - **Plattform:** Chrome-utvidelse (Manifest V3), med én egen fane for tidtaker og by. «Web» i den gamle briefen betydde «nettside, ikke mobilapp».
  - **Blokkering:** advarselsvindu over siden innen 1 sekund, med 10 sekunders nedtelling. Blir brukeren på siden, eller lukker vinduet, avbrytes økten og gir null fremgang. Utenfor økt skjer ingenting. Standard blokkeringsliste som brukeren kan redigere.
  - **By:** fokusminutter er eneste enhet. 5 byggtyper med ulik byggetid; brukeren velger selv, og kan ikke bytte bygg underveis.
  - **Streak:** én fullført økt per kalenderdag, nullstilles ellers. Vises bare som et tall.
  - **Lagring:** kun lokalt. Nettleserhistorikk lagres eller sendes aldri.
  - **Konkurrenter:** StayFocusd, LeechBlock og Forest-utvidelsen er nevnt. Forskjellen er 10-sekundersvinduet, byen og at appen er lett.
  - **Suksesskriterier:** 12 testbare kriterier. De langsiktige målene er flyttet til Vision.
- `.memlog.md` er opprettet i brief-mappen (36 oppføringer).
- `FocusApp/` er flyttet fra `E:\Skole\IBE160\` inn i repoet (ukommittert, untracked). `_bmad` og `.claude` der er identiske kopier. `.docs` har i tillegg et PRD-utkast og brainstorming fra 2026-09-15.
- Statuslinje (utenfor repoet): `~/.claude/statusline.ps1` og `statusLine` i `~/.claude/settings.json`. Viser modell, sti, branch, kontekst og 5t/7d-grenser med tid til nullstilling. Skriptet er ikke testet av Claude, fordi testkjøringen ble blokkert.

### Åpne punkter
- Lag en teknisk prototype (en minimal utvidelse med advarselsvindu på ett blokkert nettsted) før PRD-en, og avgjør der om advarselen skal ha lyd.
- Dokumenter hvorfor planleggingsdokumentene ble fjernet i commit `3cdb256`, som faglæreren ba om.
- Bestem hva som skal skje med `FocusApp/`: slett duplikatene `_bmad` og `.claude`, og avgjør om PRD-utkastet og brainstormingen skal beholdes.
- Neste BMAD-steg etter prototypen: PRD (`bmad-prd`).
