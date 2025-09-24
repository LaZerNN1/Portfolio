# 🛡️ Honeypot i Azure med Microsoft Sentinel

Dette prosjektet setter opp en enkel **honeypot** i Azure. Den logger mislykkede RDP-innlogginger, henter angripernes IP-adresser, slår de opp mot en geolocation-API og visualiserer dataene i **Microsoft Sentinel**.

---

## 🚀 Steg-for-steg

<table>
  <tr>
    <td width="60%">
      <h3>1. Opprett VM og aktiver RDP</h3>
      <ul>
        <li>Lag en Windows Server VM i Azure</li>
        <li>Åpne RDP-port (3389) i nettverksinnstillingene</li>
        <li>Koble VM-en til Log Analytics Workspace og legg til Microsoft Sentinel</li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/881f910ec430089b777159e9f57a9cb9.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>2. Konfigurer VM som honeypot</h3>
      <ul>
        <li>Logg inn via RDP</li>
        <li><b>Slå av Windows-brannmuren</b> for å gjøre maskinen sårbar</li>
        <li>Sjekk at Event Viewer logger mislykkede innlogginger (Event ID 4625)</li>
        <li>Angripere vil nå automatisk prøve å brute-force innlogging</li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/f0eb16b68518abfcdedb856f5d0c79e9.png" width="400">
      <img src="https://gyazo.com/72fe2d28b028783abcf267414839fbd1.png" width="400">
      <img src="https://i.gyazo.com/ecc3498e6478478ddb39306f1be96278.jpg" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>3. Kjør PowerShell-script for å hente geodata</h3>
      <ul>
        <li>Last ned PowerShell-script og lagre som .ps fil</li>
        <li>Kjør PowerShell-script</li>
        <li>Slå opp IP-adresser mot geolocation.io eller tilsvarende API</li>
        <li>Lagre resultatene (tid, IP, land, latitude, longitude) i <code>failed_rdp.log</code></li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/4eae5be60211e29d38a2c02cc28c7aa1.png" width="400">
      <img src="https://gyazo.com/b82a18d39888d3ac908e3f97e2a5fb46.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>4. Opprett Custom Log i Log Analytics</h3>
      <ul>
        <li>Gå til Log Analytics Workspace i Azure-portalen</li>
        <li>Lag en Custom Log som peker til <code>failed_rdp.log</code></li>
        <li>Importer dataene til Azure</li>
        <li>Opprett Custom Fields for IP, latitude, longitude og country (KQL spørring)</li>
      </ul>
    </td>
    <td>
      <img src="https://i.gyazo.com/69b11e9c70563b6d6f8d975736d15ac3.png" width="400">
      <img src="https://i.gyazo.com/46464b2d1a5e9868767289d1df34ae89.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>5. Visualiser på kart i Microsoft Sentinel</h3>
      <ul>
        <li>Lag en Workbook i Sentinel</li>
        <li>Kjør KQL-spørringer for å hente ut latitude og longitude</li>
        <li>Plott forsøkene på kart</li>
        <li>Se hvor i verden angrepene kommer fra 🌍</li>
      </ul>
    </td>
    <td>
      <img src="https://i.gyazo.com/2e64fc9b2427d9a97d70dcc226f85d11.png" width="400">
      <img src="https://i.gyazo.com/dc79d4f696f44960f4801f9aa3ca8827.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>6. Overvåk angrepene</h3>
      <ul>
        <li>Kontinuerlig overvåkning av bruteforce-forsøk</li>
        <li>Bruk Sentinel til å analysere og lage alarmer</li>
        <li>Gir innsikt i hvor angripere kommer fra og mønstre i angrepene</li>
      </ul>
    </td>
    <td>
      <img src="https://i.gyazo.com/fb9d9778d54e82211ada7e051e905d09.png" width="400">
    </td>
  </tr>
</table>

---

## 📌 Referanse
- 🎥 [SIEM Tutorial for Beginners | Azure Sentinel Tutorial MAP with LIVE CYBER ATTACKS! (Josh Madakor)](https://www.youtube.com/watch?v=RoZeVbbZ0o0)
- 🎥 [SIEM Tutorial | Azure Sentinel Tutorial | MAP with LIVE CYBER ATTACKS! (Anastasia Kuznetsova)](https://www.youtube.com/watch?v=02RE3B2uIvw)
