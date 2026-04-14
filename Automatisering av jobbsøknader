# 🤖Automatisering av LinkedIn-jobbsøknader
En automatisert arbeidsflyt bygget med n8n som henter LinkedIn-stillingsannonser, rangerer dem mot CV-en din ved hjelp av AI, filtrerer bort duplikater, genererer personlige søknadsbrev og lagrer alt i en Notion-database.

---

## 📋 Oversikt

Dette prosjektet automatiserer jobbsøkerprosessen ved å:
1. Hente stillingsannonser fra LinkedIn
2. Rangere hver jobb opp mot CV-en din ved hjelp av Claude AI
3. Filtrere bort jobber med lav relevans og duplikater
4. Generere et personlig søknadsbrev for hver relevant jobb
5. Lagre jobb + søknadsbrev i en Notion-database og Google Docs

---

## 🛠️ Teknologistack

- **n8n** – Automatisering av arbeidsflyt (selvhostet via Docker)
- **Apify** – LinkedIn-jobbskraper
- **Claude AI (Anthropic)** – Jobbrangering og generering av søknadsbrev
- **Notion** – Database for jobbsøknader
- **Google Docs** – Lagring av søknadsbrev
- **Google Drive** – Lagring av CV

---

## 🏗️ Arkitektur

```
LinkedIn URLs
     ↓
Apify LinkedIn Scraper
     ↓
Fetch CV from Google Drive
     ↓
Claude AI – Ranger jobb 1–10 basert på CV-match
     ↓
Code Node – Parse JSON output
     ↓
Filter – Behold jobber med rangering 6 og opp
     ↓
Remove Duplicates – Sjekk mot Notion-database
     ↓
Claude AI – Generer personlig søknadsbrev
     ↓
Google Docs – Lagre søknadsbrev
     ↓
Notion – Lagre jobb + lenke til søknadsbrev
```

---

## ⚙️ Oppsett

### Forutsetninger

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Notion-konto
- Google-konto
- Anthropic API-nøkkel
- Apify-konto

### 1. Kjør n8n med Docker

```powershell
docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n n8nio/n8n
```

Åpne http://localhost:5678 i nettleseren din.

### 2. Sett opp legitimasjon i n8n

| Service | Auth Type | Notes |
|---|---|---|
| Anthropic | API Key | Fra console.anthropic.com |
| Google Docs | OAuth2 | Koble til Google-konto |
| Google Drive | OAuth2 | Samme Google-konto |
| Notion | Internal Integration Token | Fra notion.so/my-integrations |
| Apify | API Key | Fra apify.com |

### 3. Sett opp Notion-database

Opprett en database kalt Stillingsannonser med følgende felt:

| Felt | Type |
|---|---|
| Tittel | Tittel |
| Bedrift | Tekst |
| Stillingstype | Tekst |
| Sted | Tekst |
| Status | Tekst |
| Publiseringsdato | Dato |
| Søknadsfrist | Dato |
| Annonse URL | URL |
| Rangering | Tall |
| Notater | Tekst |

Koble n8n-integrasjonen til databasen via Settings → Connections i Notion.

---

## 🔄 Gjennomgang av arbeidsflyt

### Node 1 – Ulike URL fra LinkedIn
Legg manuelt inn én eller flere LinkedIn-søke-URL-er som skal skrapes.

### Node 2 – Henter LinkedIn-jobber (Apify)
Bruker Apify sin LinkedIn Jobs Scraper til å hente opptil 50 stillingsannonser per URL. Returnerer felt som `title`, `companyName`, `descriptionText`, `location`, `link`, `postedAt`.

### Node 3 – CV (Google Drive)
Henter CV-en din fra Google Drive for bruk i AI-rangering.

### Node 4 – Rangerer jobben (Claude AI)
Sender jobbinformasjon + CV til Claude med følgende promptstruktur:
- Hvem du er og hva du ser etter
- Innholdet i CV-en
- Jobbtittel, selskap og beskrivelse
- Instruksjoner om å svare i ren JSON med:: `Selskap`, `Rolle`, `Rangering` (1-10), `Grunnlag`

### Node 5 – Lager dedikerte JSON felt (Kode-node)
Fjerner markdown-kodeblokker og parser ren JSON:
```javascript
return $input.all().map(item => {
  const text = item.json.content[0].text;
  const cleaned = text.replace(/```json|```/g, '').trim();
  const parsed = JSON.parse(cleaned);
  parsed.Rangering = Number(parsed.Rangering);
  return { json: parsed };
});
```

### Node 6 – Filtrerer jobben ut i fra rangering (Filter)
Beholder kun jobber der `Rangering >= 6`.

### Node 7 – Sjekker duplikater (Notion Get Many)
Søker i Notion-databasen for å sjekke om jobben allerede finnes basert på `Tittel` AND `Bedrift`. Hindrer duplikater mellom kjøringer.

### Node 8 – Lager søknad (Claude AI)
Genererer et personlig søknadsbrev på norsk basert på:
- Stillingsbeskrivelse
- CV-en din
- Selskap og rolle

### Node 9 – Google Docs
Oppretter et nytt dokument med tittelen `Søknad - [Rolle] - [Selskap]` med generert tekst.

### Node 10 – Notion Create
Lagrer jobben i Notion-databasen med alle relevante felt, inkludert lenke til søknadsbrevet.

---

## 🚀 Slik kjører du

1. Åpne n8n på `localhost:5678`
2. Lim inn én eller flere LinkedIn-søke-URL-er i trigger-noden
3. Klikk **Execute Workflow**
4. Nye relevante jobber dukker opp i Notion-databasen med ferdige søknadsbrev i Google Docs

---

## 📁 Prosjektstruktur

```
n8n-job-automation/
├── README.md
└── workflow.json        # Eksportert fra n8n (File → Download)
```

For å eksportere workflow: Gå til n8n → åpne workflow → ⋮ meny → Download

---
