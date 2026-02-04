# Besvarelse av refleksjonsspørsmål - DATA1500 Oppgavesett 1.3

Skriv dine svar på refleksjonsspørsmålene fra hver oppgave her.

---

## Oppgave 1: Docker-oppsett og PostgreSQL-tilkobling

### Spørsmål 1: Hva er fordelen med å bruke Docker i stedet for å installere PostgreSQL direkte på maskinen?

**Ditt svar:**

Å bruke docker sørger for at man ikke trenger et konsistent miljø eller samme maskin for å åpne applikasjoner, siden Docker-containeren inneholder miljøet (OS, biblioteker, kode) som trengs for å kjøre den. Det gjør at PostgresSQL blir enklere å innstallere og mer tilgjengelig for bruk av f.eks. studenter med ulikt miljø.
---

### Spørsmål 2: Hva betyr "persistent volum" i docker-compose.yml? Hvorfor er det viktig?

**Ditt svar:**

'persistent volum' vil si at dataen blir lagret i sti, eller 'volum'. Det lagres lokalt, utenfor containeren og er viktig for å unngå at dataen går tapt når containeren stoppes/slettes/restartes.
---

### Spørsmål 3: Hva skjer når du kjører `docker-compose down`? Mister du dataene?

**Ditt svar:**

docker-compose down stopper containeren, men sletter ikke dataene siden de lagres i volum.
---

### Spørsmål 4: Forklar hva som skjer når du kjører `docker-compose up -d` første gang vs. andre gang.

**Ditt svar:**

Første gang man starter opp containeren er det flere ting som må lastes inn, som image, containeren og volum opprettes. Andre gang eksisterer disse tingene allerede, så containeren starter raskere.
---

### Spørsmål 5: Hvordan ville du delt docker-compose.yml-filen med en annen student? Hvilke sikkerhetshensyn må du ta?

**Ditt svar:**

Man bør ta hensyn til at det er sårbar informasjon i klartekst, som brukernavn og passord. Det kan f.eks. lagres i en egen fil som ikke deles, eller sendes separat hvis man skal jobbe på samme bruker for å unngå at hele databasen kan bli tilgjengelig for feil person (tilgangskontroll)
---

## Oppgave 2: SQL-spørringer og databaseskjema

### Spørsmål 1: Hva er forskjellen mellom INNER JOIN og LEFT JOIN? Når bruker du hver av dem?

**Ditt svar:**

Joins kobler sammen 2 tabeller når man skal hente ut informasjon. Forskjellen er at inner join gir resultater der det er en match i både tabell 1 og tabell 2, og utelater dermed data når en rad ikke eksisterer i den andre. Left join viser alt fra tabell 1, men kun de radene i tabell 2 som samsvarer. 
---

### Spørsmål 2: Hvorfor bruker vi fremmednøkler? Hva skjer hvis du prøver å slette et program som har studenter?

**Ditt svar:**

Fremmednøkler brukes for å koble 2 tabeller sammenhengende tabeller i en database. Det brukes bl.a. i joins. Hvis man prøver å slette et program som har studenter vil databaseprogrammet stoppe brukeren siden kolonnen har en avhengighet til studenter-tabellen. Da må isåfall fremmenøklene i studenter slettes, før progrmamet kan slettes.
---

### Spørsmål 3: Forklar hva `GROUP BY` gjør og hvorfor det er nødvendig når du bruker aggregatfunksjoner.

**Ditt svar:**

GROUP BY grupperer resultater ut ifra en kolonne. Det er nødvendig når man bruker aggregatfunksjoner fordi man vil utføre beregninger på grupperte datasett, f.eks. når man teller opp antall studenter i hvert emne. Da vil antallet være gruppert i forhold til emnene.
---

### Spørsmål 4: Hva er en indeks og hvorfor er den viktig for ytelse?

**Ditt svar:**

En indeks er en peker som indikerer hvor en rad ligger, noe som kan minne om en innholdsfortengelse i en bok. Det er viktig for ytelse, spesielt i store databaser fordi det øker hastigheten det tar å finne/hente ut data. F.eks. når man gjør et søk. Det kan være når man leter etter en student i databasen, eller ønsker å filtrere innholdet i databasen.
---

### Spørsmål 5: Hvordan ville du optimalisert en spørring som er veldig treg?

**Ditt svar:**

En måte å optimalisere treg spørring er ved å bruke indekser og unngått select *
---

## Oppgave 3: Brukeradministrasjon og GRANT

### Spørsmål 1: Hva er prinsippet om minste rettighet? Hvorfor er det viktig?

**Ditt svar:**

Prinsippet om minste rettighet er at brukere kun har tilgang til det de trenger for å utføre oppgavene sine. Det er viktig for tilgangskontroll, siden man setter grenser og får kontroll på hvem som kan gjøre hva. Det reduserer muligheten for feil, f.eks. oppdateringer/sletting av data, eller uautorisert tilgang.
---

### Spørsmål 2: Hva er forskjellen mellom en bruker og en rolle i PostgreSQL?

**Ditt svar:**

En bruker er en individuell person med innlogging, mens en rolle er hvilke rettigheter denne personen/brukeren har på databasen. Flere brukere kan ha samme rolle (f.eks. student), og de vil ha de samme rettighetene (f.eks. å kunne oppdatere en rad i en tabell).
---

### Spørsmål 3: Hvorfor er det bedre å bruke roller enn å gi rettigheter direkte til brukere?

**Ditt svar:**

Når man tilskriver roller rettigheter, lagres de i den rollen. Dermed kan man gjenbruke dette for hver bruker som har samme rolle i systemet. Det sparer tid ved å motvirke redundant arbeid da man ikke trenger å grante de samme rettighetene til brukerne i flere omganger. Man kan også tilskrive en hel gruppe den samme rollen, noe som også er en fordel.
---

### Spørsmål 4: Hva skjer hvis du gir en bruker `DROP` rettighet? Hvilke sikkerhetsproblemer kan det skape?

**Ditt svar:**

DROP sletter dataen, tabellstrukturen og rettighetene som er definert for tabellen. Da vil brukeren ha makten til å la data gå tapt permanent, noe som er et stort risikoproblem dersom det skjer feilaktig.
---

### Spørsmål 5: Hvordan ville du implementert at en student bare kan se sine egne karakterer, ikke andres?

**Ditt svar:**

Enten ved å opprette et view, da får de sin egen personlige kopi av tabellen med kun kolonnene og radene som er relevant for dem, eller implementert RLS slik at de kun ser sine egne rader. 
---

## Notater og observasjoner

Bruk denne delen til å dokumentere interessante funn, problemer du møtte, eller andre observasjoner:

[Skriv dine notater her]


## Oppgave 4: Brukeradministrasjon og GRANT

1. **Hva er Row-Level Security og hvorfor er det viktig?**
   - Row-Level Security (RLS) er at man begrenser brukernes tilgang til kun deres rad, ved å sjekke hvilke rader som oppfyller en bestemt betingelse (hvor raden = bruker)

2. **Hva er forskjellen mellom RLS og kolonnebegrenset tilgang?**
   - Forskjellen er at CLS begrenser brukeres tilgang til antall synlige kolonner, f.eks. at hver bruker kun ser kolonnene for karakter, brukerID og emneID, men utelater navn. Brukerne vil kunne se alle rader, men kjenner kun til sin egen rad. RLS begrenser synlighet ved å utelate rader som ikke er relevante for brukeren.

3. **Hvordan ville du implementert at en student bare kan se karakterer for sitt eget program?**
   - Ved å bruke RLS, slik at kun deres rad i databasen er synlig.

4. **Hva er sikkerhetsproblemene ved å bruke views i stedet for RLS?**
   - Svar her...

5. **Hvordan ville du testet at RLS-policyer fungerer korrekt?**
   - Svar her...

---

## Referanser

- PostgreSQL dokumentasjon: https://www.postgresql.org/docs/
- Docker dokumentasjon: https://docs.docker.com/

