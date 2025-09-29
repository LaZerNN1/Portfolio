# 🌐 Kompleks hjemmenettverk i Cisco Packet Tracer

Dette prosjektet demonstrerer oppsett og konfigurasjon av et **hjemmenettverk med flere sikkerhetssoner** i Cisco Packet Tracer. Nettverket inkluderer VLAN, DMZ, gjestenettverk, admin-sone og tjenester som DHCP, DNS og Syslog.

---

## 🖥️ Nettverkskomponenter

- **Nettverkssoner**
  - Privat (VLAN 10 → 192.168.10.0/24)
  - Gjestenettverk (VLAN 20 → 192.168.20.0/24)
  - DMZ (VLAN 30 → 192.168.30.0/24)
  - Admin/Syslog (VLAN 40 → 192.168.40.0/24)

- **Maskinvare**
  - Ruter, Switch, Trådløst aksesspunkt
  - Servere (Syslog)
  - Klienter (PC-er)

- **Tjenester**
  - DHCP, Syslog, ACL / Port security

---

## ✅ Steg-for-steg

<table>
  <tr>
    <td width="60%">
      <h3>Fase 1 — Planlegging</h3>
      <ul>
        <li>Skisse av nettverkstopologi og IP-plan</li>
        <li>Definer VLAN: 10 (Privat), 20 (Gjest), 30 (DMZ), 40 (Admin)</li>
        <li>Inventar over nødvendige enheter (ruter, switch, servere, klienter)</li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/7f822f6e3cab1f919cdaa0667d0c286c.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>Fase 2 — Grunnoppsett i Packet Tracer</h3>
      <ul>
        <li>Grunnkonfigurasjon av ruter og switch (hostname, passord)</li>
        <li>Sett opp "router-on-a-stick" for subinterfaces</li>
        <li>Sett opp trunk på switch</li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/de35e70c6c9a5a1cf6ec7f97805c809f.png" width="400">
      <img src="https://gyazo.com/347cc87111d540c8a195c33050b86bd3.png" width="400">
      <img src="https://gyazo.com/ddab2c96e04bd5492e448077b40dba8a.png" width="400">
      <img src="https://i.gyazo.com/e46b59d3628d9f78fe3550eaea37db64.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>Fase 3 — Konfigurasjon av nettverkssoner</h3>
      <ul>
        <li>Opprett VLAN og tildel subnett for hver sone</li>
        <li>Sett opp DHCP-scope for hvert VLAN</li>
        <li>Konfigurer DMZ-server med statisk IP (f.eks. 192.168.30.5/24)</li>
        <li>Implementer ACLs og port security for gjestenettverk og DMZ</li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/69a62477a7e2ee4915fb525ad65b6f7e.png" width="400">
      <img src="https://gyazo.com/5c6be04f8626af187ff7366eef10385c.png" width="400">
      <img src="https://gyazo.com/2566e80ac9940d7408669beb7a06e20b.png" width="400">
      <img src="https://gyazo.com/94a51f1f2267171377a97abe3948ab7d.png" width="400">
      <img src="https://gyazo.com/d6e1c60fbec6fa73fb131e93cb382a8b.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>Fase 4 — Tjenester og logging</h3>
      <ul>
        <li>Installer og konfigurer Syslog-server</li>
        <li>Konfigurer rutere og switch til å sende logs til Syslog</li>
        <li>Verifiser at DHCP fungerer og at klienter får riktige IP-er</li>
      </ul>
    </td>
    <td>
      <img src="https://i.gyazo.com/2b928dd2988151f496197f39c5b3b57c.png" width="400">
      <img src="https://i.gyazo.com/54a5f936cb21ed2b501bbbc31d22f847.png" width="400">
    </td>
  </tr>
</table>

---

<table>
  <tr>
    <td width="60%">
      <h3>Fase 5 — Testing og feilsøking</h3>
      <ul>
        <li>Bekreft at sikkerhetspolicyer fungerer som forventet</li>
        <li>Bruk ping for å teste internkommunikasjon</li>
      </ul>
    </td>
    <td>
      <img src="https://gyazo.com/29b4653194e3bf55f4ecf344a3d294bd.png" width="400">
      <img src="https://gyazo.com/5fb88337a201733a0070387aef782202.png" width="400">
    </td>
  </tr>
</table>

