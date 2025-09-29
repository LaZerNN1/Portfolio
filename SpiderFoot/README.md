# 🕷️ SpiderFoot — OSINT Undersøkelse

Dette prosjektet demonstrerer bruk av **SpiderFoot** for Open Source Intelligence (OSINT). SpiderFoot er et automatiseringsverktøy skrevet i Python som samler, korrelerer og visualiserer data fra åpne kilder.
---

## 🔍 Hva er OSINT?
**OSINT (Open Source Intelligence)** handler om innsamling og analyse av informasjon fra offentlig tilgjengelige kilder: nettsider, DNS, sosiale medier, offentlige registre, lekkasjer og mye mer. OSINT brukes til etterretning, trusselvurdering og undersøkelser.

---

## ✅ Prosjekt — steg-for-steg

<table>
  <tr>
    <td width="60%">
      <h3>Steg 1 — Oppsett av Virtuell Maskin (Kali Linux)</h3>
      <ul>
        <li>Last ned og installer VirtualBox (Oracle)</li>
        <li>Last ned Kali Linux ISO fra offisiell kilde</li>
        <li>Opprett VM i VirtualBox og tildel RAM/lagring</li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/8a76bb38d4fb83c6d18ffda526ed60d2.png" width="400">
      <img src="https://gyazo.com/413484cd9004b99f1324be57f42ff177.png" width="400">
      <img src="https://gyazo.com/3db5e53dc02b3760b419626cdf292deb.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>Steg 2 — Oppdatering og installasjon av SpiderFoot</h3>
      <ul>
        <li>Åpne terminal i Kali</li>
        <li>Oppdater systemet:
          <pre><code>sudo apt update && sudo apt upgrade -y</code></pre>
        </li>
        <li>Sjekk om SpiderFoot er installert:
          <pre><code>spiderfoot -h</code></pre>
        </li>
        <li>Hvis nødvendig, installer fra GitHub:
          <pre><code>git clone https://github.com/smicallef/spiderfoot.git
cd spiderfoot
pip3 install -r requirements.txt</code></pre>
        </li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/ad63ee6b303b71a2d864b9f1158f6031.png" width="400">
      <img src="https://gyazo.com/2d9c4fe424747ba1ad138a8609e86df6.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>Steg 3 — Kjøre og bruke SpiderFoot</h3>
      <ul>
        <li>Start SpiderFoot (web UI):
          <pre><code>python3 ./sf.py -l 127.0.0.1:5001
# eller
spiderfoot</code></pre>
        </li>
        <li>Åpne nettleser: <code>http://127.0.0.1:5001</code></li>
        <li>Opprett ny scan: velg måltype (domene, IP, e-post osv.) og moduler</li>
        <li>Start skanningen, følg progresjon og analyser resultater</li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/b59fe7d70a57c68b38b3696000b18d90.png" width="400">
      <img src="https://gyazo.com/54f0e7a2c1dc16d4aa850ed3fbca27d7.png" width="400">
      <img src="https://gyazo.com/05f2267499f75ed94e5bd443c32efc65.png" width="400">
      <img src="https://gyazo.com/200020ed5f8aa8fabbb71f9d9dbb929a.png" width="400">
    </td>
  </tr>
</table>
