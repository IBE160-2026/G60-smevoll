# Tilbakemelding på product brief

| | |
|---|---|
| **Gruppe** | G60 – G60-smevoll |
| **Product brief** | `.docs/planning-artifacts/briefs/brief-FocusApp-2026-09-15/brief.md` (commit `7add91e`) |
| **Tilbakemelding fra** | Faglærer i IBE160 (utarbeidet med KI-støtte) |
| **Dato** | 2026-10-06 |

## Samlet vurdering

- **Bør revideres før dere går videre.** Rett punktene markert «Endre» før dere lager PRD og arkitektur.

Vi har vurdert `brief.md` for «Focus App».

**Det som er bra:**

1. Innsikten bak appen er tydelig og godt formulert. Mobilgrepet er en refleks og ikke et viljestyrkeproblem, så appen skal gripe inn i øyeblikket i stedet for å belønne i etterkant. Det gir en klar kjernefunksjon: overlay og lyd når fokusøkten brytes.
2. Avgrensningen er ryddig. Mobilappen og synkronisering mellom enheter er eksplisitt satt utenfor v1, og ferdighetstreet er merket som strekkmål. Dere er også ærlige om at dette ikke er en teknisk «moat».

**De viktigste endringene:**

1. Kjernefunksjonen lar seg ikke lage som en vanlig nettside. En nettside kan merke at brukeren forlater fanen sin, men den kan ikke se hvilket nettsted brukeren går til, og den kan ikke legge en overlay over andre faner. Det krever en nettleserutvidelse (for eksempel en Chrome-utvidelse). Avklar dette i briefen, siden det endrer både arkitektur, kjøring og testing.
2. Begge suksesskriteriene («time-before-drift trending upward» over uker og «sustained use … over months») kan ikke måles i løpet av emnet. Legg til funksjonelle kriterier som kan bli testtilfeller.
3. Beskriv bylogikken mer konkret: hva en fullført økt gir, hva som skjer ved avbrudd, hvordan streaks regnes og hvor fremdriften lagres. Det er her det meste av appens logikk og testbarhet ligger.

## Vanskelighetsgrad og gjennomførbarhet

### Vurdert vanskelighetsgrad

- **Middels**

**Sammenlignbart med:** 6) To-do-liste med smarte etiketter (enkel) i kjernen, altså en personlig produktivitetsapp med enkel datamodell. Nettleserutvidelse med fanedeteksjon og blokkering, pluss et spillifisert byggesystem, løfter prosjektet til middels. Det er på nivå med 7) Kurs-FAQ-chatbot (middels) i arbeidsmengde, men med en helt annen type teknisk utfordring.

**Begrunnelse:**

| Faktor | Nivå (lav / middels / høy) | Kommentar |
|---|---|---|
| Domenelogikk – hvor mange og hvor kompliserte regler og beregninger må stemme? | middels | Tidtaker for fokus og pause, regler for hva som teller som drift, streaks, bygging av byen og eventuelt opplåsing via ferdighetstre. |
| Datamodell – antall entiteter og relasjoner mellom dem | lav | Økter, innstillinger, blokkeringsliste, streak og bytilstand. |
| Brukere, roller og innlogging | lav | Én bruker. Innlogging er ikke nevnt, og lokal lagring kan være nok i v1. |
| KI-funksjonalitet i appen, f.eks. kall til språkmodell, prompts i koden og håndtering av usikre svar | lav | Ingen KI i appen. Det er greit. Kursets KI-del ligger i hvordan dere styrer utviklingen. |
| Integrasjoner og eksterne tjenester, f.eks. API-er, betaling og e-post | middels | Ingen eksterne tjenester, men nettleserens API-er for utvidelser (tabs, overlay og varsler) med egne regler og tillatelser. |
| Sanntid, samtidighet eller flere brukere som påvirker hverandre | middels | Ingen flerbruker. Utvidelsen må likevel reagere umiddelbart på fanebytter mens tidtakeren går. |
| Filhåndtering, f.eks. opplasting, PDF-lesing og eksport | lav | Ingen. |
| Sikkerhet og personvern | middels | En utvidelse som ser hvilke nettsteder brukeren besøker, er personvernsensitiv. Beskriv at nettleserhistorikk bare brukes lokalt og ikke lagres eller sendes. |

**Hva vanskelighetsgraden betyr for dere:**

- _Middels:_ Et godt balansert valg. Pass på at kjerneflyten blir ferdig og stabil før dere legger til mer. Her er kjerneflyten: start økt → fanebytte til blokkert nettsted fanges → overlay og lyd → økten fullføres → byen vokser.

### Gjennomførbarhet med BMAD og Claude Code

Dere skal planlegge med BMAD (product brief → PRD → arkitektur → epics og stories) og implementere med Claude Code. Vurderingen under tar hensyn til at det må være tid til hele denne flyten, og til testing, retting og README til slutt.

| Spørsmål | Vurdering (OK / risiko / stor risiko) | Kommentar |
|---|---|---|
| **Tid og omfang** – kan v1 realistisk bli ferdig og stabil i løpet av semesteret, med tid til flere iterasjoner? | OK | Omfanget i v1 er rimelig hvis byen holdes enkel og ferdighetstreet blir værende et strekkmål. |
| **BMAD-flyten** – er briefen konkret nok til at PRD, arkitektur og stories kan lages uten store hull, og blir det overkommelig mange stories? | risiko | Plattformvalget (nettside eller utvidelse) og reglene for byen er ikke avklart. Det gir hull i PRD og arkitektur. |
| **Egnet for Claude Code** – bruker løsningen en vanlig, godt dokumentert teknologistakk som Claude Code håndterer godt, eller krever den nisjeteknologi, spesialmaskinvare eller mye manuell konfigurasjon? | risiko | Chrome-utvidelser (Manifest V3) er godt dokumentert, og Claude Code kan lage dem. Testing og feilsøking krever likevel manuell lasting i nettleseren og mer prøving enn en vanlig webapp. |
| **Kontroll på KI-ens arbeid** – kan gruppen selv avgjøre om koden gjør det riktige? Krever domenet kunnskap gruppen ikke har, f.eks. avanserte beregninger eller fagregler, så er det vanskelig å kvalitetssikre. | OK | Dere kan selv enkelt se om blokkeringen slår inn, og om byen vokser riktig. |
| **Testbarhet** – finnes det tydelige regler og forventede resultater som tester kan skrives mot? | risiko | Tidtaker-, streak- og byregler kan enhetstestes når de er definert. Selve blokkeringen må testes manuelt med en dokumentert testplan. |
| **Kjørbar for sensor** – kan appen kjøres lokalt etter README, uten gruppens nøkler, betalte kontoer eller egen infrastruktur? | OK | Ingen nøkler eller kontoer. README må forklare steg for steg hvordan utvidelsen lastes inn i nettleseren (utviklermodus → «Load unpacked»). |
| **Avhengigheter og kostnader** – krever løsningen betalte API-er, f.eks. språkmodeller, og finnes det en plan for kostnad, testmodus eller mock-data? | OK | Ingen betalte tjenester. |

**Konklusjon om gjennomførbarhet:**

- **Gjennomførbart med justert omfang.** Se forslagene under.

**Forslag til justering av omfang eller vanskelighetsgrad:**

1. Velg plattform eksplisitt: en nettleserutvidelse for én nettleser (for eksempel Chrome) med popup for tidtaker og en egen side for byen. Alternativet er en ren nettside som bare merker at brukeren forlater fokusfanen, men da må ideen om å blokkere bestemte nettsteder endres.
2. Hold byen enkel i v1, for eksempel ett nytt bygg per fullførte intervall fra en fast liste, og la ferdighetstreet være trinn 2. Da blir det tid til god testing og et gjennomarbeidet design.

## Hvorfor product brief er viktig for mappen

Product brief er utgangspunktet for PRD, arkitektur, stories og til slutt koden. Del 1 av mappen vurderes blant annet på om sensor kan følge en sporbar vei fra plan til ferdig app. Den vurderes også på om appen gjør det dere har beskrevet, om den er testet, om den er godt designet, og om den kan kjøres etter README. Et uklart, for stort eller for lite brief gjør alt dette vanskeligere senere. Det er mye enklere å rette nå enn sent i semesteret.

## 1. Gjennomgang av briefens deler

| Del av brief | Status | Kommentar |
|---|---|---|
| Executive Summary – er det klart hva appen er, og hvilket problem den løser? | OK | Klart: en fokusapp som griper inn med overlay og lyd i stedet for å belønne passivt, med en by som vokser. |
| The Problem – er problemet konkret, med reelle situasjoner og brukere? | OK | Konkret beskrivelse av hvordan et sekunds distraksjon blir til 30 minutters scrolling, og hvorfor dagens løsninger svikter. |
| The Solution – beskriver løsningen brukeropplevelsen, ikke bare teknologi? | Endre | Brukeropplevelsen er godt beskrevet, men forutsetter noe en vanlig nettside ikke kan gjøre: se og blokkere andre faner. Beskriv løsningen som nettleserutvidelse, eller juster funksjonen. |
| What Makes This Different – er vurderingen ærlig og realistisk? | Juster | Ærlig vurdering. Det finnes likevel kjente utvidelser som blokkerer nettsteder i fokusøkter (for eksempel StayFocusd og LeechBlock). Nevn dem og forklar hva kombinasjonen med byen tilfører. |
| Who This Serves – er primærbrukerne tydelige, og vet vi hva de trenger? | OK | Én tydelig primærbruker: studenter og selvstendige lærende som jobber uten ytre struktur. |
| Success Criteria – kan kriteriene faktisk sjekkes eller testes? | Endre | Begge kriteriene krever måneder med bruk. Legg til kriterier som «når brukeren åpner et nettsted på blokkeringslisten under en aktiv økt, vises overlay og lyd innen ett sekund», «utenfor økt blokkeres ingenting», «et fullført intervall gir ett nytt bygg i byen» og «streaken nullstilles når en dag går uten fullført økt». |
| Scope – er det klart hva som er med i første versjon, og hva som ikke er det? | Juster | Tydelig delt i inne og ute. Legg til plattformvalget (utvidelse og nettleser), og presiser om blokkeringslisten er fast eller kan redigeres av brukeren. |
| Vision – henger visjonen sammen med resten uten å blåse opp omfanget? | OK | Mobilapp, flere bytemaer og deling er tydelig plassert i fremtiden. |

## 2. Utgangspunkt for del 1 av mappen

Punktene følger kriteriene i sensorveiledningen for del 1. Vektene i parentes viser hvor mye hvert kriterium teller i del 1.

| Kriterium i del 1 | Hva briefen bør legge til rette for | Status | Kommentar |
|---|---|---|---|
| **1. Prosess og KI-styring** (30 %) | Brief som er presis nok til at PRD og stories kan bygges direkte på den, slik at krav kan spores fra brief til kode. | Juster | Briefen ligger i BMAD-strukturen. Dere fjernet andre planleggingsdokumenter i siste commit. Dokumenter kort hvorfor, siden slike beslutninger er en del av prosessen sensor ser etter. |
| **2. Funksjonalitet og omfang** (20 %) | Realistisk omfang for gruppen og semesteret: en tydelig kjerneflyt som kan bli ferdig og stabil, og nok innhold til å vise reell funksjonalitet. | OK | Tydelig kjerneflyt og et rimelig omfang, gitt at plattformen avklares. |
| **3. Kvalitetssikring og testing** (15 %) | Suksesskriterier og funksjoner som er konkrete nok til å bli testtilfeller. | Endre | Suksesskriteriene kan ikke bli testtilfeller. Legg til funksjonelle kriterier, og planlegg både enhetstester for logikken og manuell testplan for blokkeringen. |
| **4. Design og brukeropplevelse** (10 %) | Tydelige brukere og brukssituasjoner som designet kan bygges rundt, gjerne med de viktigste skjermbildene eller flytene skissert. | Juster | Byen er en god designmulighet. Skisser overlayen, tidtakeren og byvisningen, og vurder om overlay og lyd kan oppleves som for brå. |
| **5. Kodekvalitet og arkitektur** (10 %) | Teknologivalg som er begrunnet og ikke mer komplekse enn appen trenger. | Endre | Plattformvalget mangler og er avgjørende for arkitekturen. Begrunn valget av utvidelse eller nettside i briefen eller i arkitekturen. |
| **6. README og kjørbarhet** (10 %) | Løsning som andre kan kjøre lokalt uten betalte kontoer, og uten tilgang til gruppens egne tjenester og nøkler. | OK | Ingen betalte tjenester. Planlegg en tydelig installasjonsveiledning for utvidelsen og en ferdig testkonfigurasjon med blokkeringsliste. |
| **7. Ryddighet i repoet** (5 %) | En plan for hvor hemmeligheter, testdata og dokumentasjon skal ligge. | OK | Få hemmeligheter. Hold byggefiler for utvidelsen (for eksempel `dist/`) ute av repoet med `.gitignore`. |

## 3. Neste steg for gruppen

1. Avklar plattformen: undersøk (gjerne med Claude Code) hva en nettside og en Chrome-utvidelse kan gjøre, og oppdater «The Solution» og «Scope» etter valget.
2. Skriv nye, testbare suksesskriterier for blokkering, økter, streaks og byvekst. Flytt de langsiktige målene til visjonen.
3. Beskriv reglene for byen og streaks konkret, og gå så videre til PRD.

Oppdater product brief i repoet når dere har gjort endringene, slik at historikken viser hvordan planen utviklet seg. Det er en del av prosessen sensor ser etter.
