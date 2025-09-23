# 🛡️ Honeypot i Azure med Microsoft Sentinel

Dette prosjektet setter opp en enkel **honeypot** i Azure. Den logger mislykkede RDP-innlogginger, henter angripernes IP-adresser, slår de opp mot en geolocation-API og visualiserer dataene i **Microsoft Sentinel**.

---

## 1. Opprett VM og aktiver RDP
- Opprett en Windows Server VM i **Azure**.  
- Sørg for at **RDP-port** er åpen i nettverksinnstillingene slik at andre kan prøve å koble til.  
- Koble VM-en til **Log Analytics Workspace** og legg til **Microsoft Sentinel** i arbeidsområdet.

---

## 2. Konfigurer VM som honeypot
- Logg inn på VM-en via RDP.  
- **Slå av Windows-brannmuren** for å gjøre maskinen sårbar.  
- Sjekk at **Event Viewer** logger sikkerhetshendelser, spesielt mislykkede innlogginger (Event ID 4625).  
- Resultatet blir at angripere automatisk vil forsøke å brute-force innlogging.

---

## 3. Kjør PowerShell-script for å hente geodata
- Kjør et PowerShell-script som:
  1. Leser **Event Viewer**-logger (mislykkede RDP-innlogginger).  
  2. Slår opp IP-adressene mot **geolocation.io** eller tilsvarende API.  
  3. Skriver ut resultatene (tid, IP, land, latitude, longitude) til en fil kalt **`failed_rdp.log`**.

---

## 4. Opprett Custom Log i Log Analytics
- Gå til **Log Analytics Workspace** i Azure-portalen.  
- Opprett en **Custom Log** som peker til filen `failed_rdp.log`.  
- Denne importerer de rå dataene inn i Azure.  
- Opprett deretter **Custom Fields** for IP, latitude, longitude og country slik at dataene blir enklere å analysere.

---

## 5. Visualiser på kart i Microsoft Sentinel
- I **Sentinel**, opprett en **Workbook**.  
- Bruk en KQL-spørring for å hente ut latitude og longitude fra custom loggen.  
- Velg **Map**-visualisering og plott punktene etter angrepsforsøk.  
- Hvert angrep vises nå geografisk på kartet.

---

## 6. Overvåk angrepene
- Når honeypoten er satt opp, vil du se kontinuerlige angrep (ofte fra hele verden).  
- Bruk Sentinel til å overvåke, analysere og eventuelt lage alarmer eller playbooks.  
- Dette gir innsikt i **hvor angripere kommer fra** og **hvilke mønstre som finnes**.
