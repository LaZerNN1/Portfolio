# 🛡️ Enkel SOC i Azure med Microsoft Sentinel

Dette prosjektet bygger videre på honeypot-oppsettet. Målet er å sette opp en enkel **Security Operations Center (SOC)** ved å bruke eksisterende VM, Log Analytics Workspace (LAW) og Microsoft Sentinel fra honeypot-prosjektet. Prosessen inkluderer å koble til data fra VM, definere Data Collection Rules, lage enkle deteksjonsregler og bruke informasjon fra honeypot-loggene.

---

## 🚀 Steg-for-steg

<table>
  <tr>
    <td width="60%">
      <h3>1. Forutsetninger: eksisterende VM, LAW og Sentinel</h3>
      <ul>
        <li>Vi gjenbruker VM-en, Log Analytics Workspace (LAW) og Microsoft Sentinel fra honeypot-prosjektet</li>
        <li>Sørg for at VM-en fortsatt samler inn logger og er tilkoblet LAW</li>
        <li>Sentinel må være aktivert og tilknyttet riktig LAW</li>
      </ul>
    </td>
    <td>
      <img src="https://i.gyazo.com/82ef36498ce8d6d7e2cb98a75dcfc871.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>2. Sett opp Data Connector mellom VM og LAW</h3>
      <ul>
        <li>Installer en agent (Log Analytics agent eller Azure Monitor Agent) på VM-en</li>
        <li>Opprett en <strong>Data Connector</strong> for å sende <em>Windows Security Events</em> fra VM til LAW</li>
        <li>Bekreft i Azure Monitor at data flyter inn i LAW</li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/8969e2771efe663c791832f40d2ad859.png" width="400">
      <img src="https://i.gyazo.com/0130f05c9fe7f09b629afa268d615b3e.png" width="400">
      <img src="https://i.gyazo.com/2c2c65449e58748b7fb76b0ccd3f714e.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>3. Lag Data Collection Rule (DCR)</h3>
      <ul>
        <li>Opprett en <em>Data Collection Rule</em> som definerer hvilke logger som skal hentes</li>
        <li>I dette prosjektet: hent <strong>alle Windows Security Events</strong> (f.eks. Event IDs 4624, 4625, 4648 osv.)</li>
        <li>DCR peker til din LAW, og sørger for at alle nødvendige logger sendes dit</li>
      </ul>
    </td>
    <td>
      <img src="https://i.gyazo.com/0eb4081522fdc103f5e8e39ae6b67d07.png" width="400">
      <img src="https://i.gyazo.com/287a0db86b8ced390f9f9026dffe8bad.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>4. Analyser data i Sentinel og lag en enkel deteksjonsregel</h3>
      <ul>
        <li>Når data er i LAW, blir de automatisk tilgjengelig i Sentinel</li>
        <li>Lag en enkel <em>Analytics Rule</em> som oppretter en alert ved <strong>successful local sign-in</strong></li>
        <li>Test regelen ved å utføre en lokal pålogging og se at en alert genereres</li>
      </ul>
    </td>
    <td>
      <img src="https://i.gyazo.com/81b01c7cf23ad0dac8fb2b6cb127f2ae.png" width="400">
      <img src="https://gyazo.com/d87c40b4bc862fe5a5897a6a1489bf11.png" width="400">
      <img src="https://gyazo.com/ebf25d9f3d06efae4657d67b869979a9.png" width="400">
      <img src="https://gyazo.com/06dc23a8a9c7020fbfc6419300a18d09.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>5. Koble inn honeypot-data</h3>
      <ul>
        <li>Berik Sentinel-regler med informasjon fra honeypotens <code>failed_rdp.log</code></li>
        <li>Eksempel: dersom en bruker feiler innloggingen mer en 5 ganger → høyprioritets alert</li>
        <li>Denne krysskoblingen gir en mer realistisk SOC-funksjon</li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/b89f0060675780f4c303ea141ea7c4ca.png" width="400">
    </td>
  </tr>
</table>

---

## 📌 Referanse
- 🎥 [you NEED this cyber security project on your resume (Mad Hat)](https://www.youtube.com/watch?v=IJUkGuirTGQ)
