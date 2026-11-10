# Wallbox WEB – add-on documentation

> **Unofficial project.** Not affiliated with, endorsed or supported by SCAME PARRE S.p.A. No warranty: use it at
> your own risk. Details in [DISCLAIMER.md](https://github.com/Filpin011/ha-wallbox-web-addon/blob/main/DISCLAIMER.md).
> *Italiano: [in fondo alla pagina](#italiano).*

Wallbox WEB is the web app to configure and monitor compatible wallboxes on your home network: status, start and
stop charging, schedules, power management, history, costs and charge curves. With this add-on it runs inside
Home Assistant OS:

- the app is in the **sidebar** (*Wallbox* entry) and recognises you with your Home Assistant user, no second
  login;
- stations are **discovered automatically** (the add-on uses the host network and receives their UDP
  announcements);
- the Home Assistant **Wallbox WEB integration** is **discovered automatically** (no URL or token to copy).

## Installation

1. Add the repository to Home Assistant:

   [![Add the repository to Home Assistant](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2FFilpin011%2Fha-wallbox-web-addon)

   or *Settings › Add-ons › Add-on store › ⋮ › Repositories* and paste
   `https://github.com/Filpin011/ha-wallbox-web-addon`.
2. Install **Wallbox WEB**, enable *Show in sidebar* and *Watchdog*, then **Start**.
3. Open **Wallbox** in the sidebar: you are already signed in with your user. Accept the notice and add the station
   as in the app.
4. *Settings › Devices & services*: **"New device discovered: Wallbox WEB"** appears → **Add** (requires the
   [Wallbox WEB integration](https://github.com/Filpin011/ha-wallbox-web) installed from HACS).

## Access and users

| From | How you sign in |
|---|---|
| Home Assistant sidebar (also remotely, e.g. Home Assistant Cloud) | automatically, with your Home Assistant user |
| `http://<Home Assistant IP>:8423` on your home network (e.g. the phone as an app) | the app's login (e-mail/password or passkey) |

- Every Home Assistant user who opens the app gets their own account in the app (same name). With the option
  *Home Assistant administrators are app administrators* (default) Home Assistant administrators are also app
  administrators, other users are normal users. The sidebar entry is visible to administrators only.
- These accounts have no password: they only work from the sidebar. In *Account*, *Change password* and *Add
  passkey* are not needed for them.
- **First start:** the **add-on log** shows the initial password of the `root` user (box *"Wallbox WEB – first
  login"*). It is only needed for direct access on port 8423: sign in with `root` and that password and complete
  the setup (e-mail + new password). Lost it? Turn on *Reset the administrator password*, restart, read the new
  password in the log and **turn the option off again**.

## Options

| Option | Meaning |
|---|---|
| Log level | `info` normal, `debug` for troubleshooting (also logs the traffic to the station). |
| Address of the web app | Direct access address, if different from `http://<IP>:8423` (e.g. your https domain). |
| Other addresses | Further addresses you use for direct access, comma separated. |
| Stations outside this network | `ip` or `ip:port` of stations on another subnet or over VPN. |
| Home Assistant administrators are app administrators | see *Access and users*. |
| Reset the administrator password | new `root` password in the log at the next start (then turn it off). |

The option labels follow your Home Assistant language (English, or Italian when Home Assistant is in Italian).

**Network** (*Network* tab): port **8423** is the direct access and the one used by the integration. You can change
it; if you disable it only the sidebar remains and the integration is not set up automatically.

## Data and backups

Users, sessions, tokens, saved stations, costs and charge curves are in the add-on's `/data` and are included in
**Home Assistant backups**. The backup is *cold*: the add-on stops for a few seconds during the backup (charge
recording resumes right after). The cache of downloaded firmware is excluded.

## Home Assistant add-on or self-hosted server?

Use **one server** per station: if Wallbox WEB already runs on your server (Coolify/Docker), do not also start the
add-on for the same station (that would be two connections). The add-on is the simplest choice with Home Assistant
OS: no reverse proxy, working station discovery, backups included.

## Dashboard

With the integration set up, add the [Wallbox WEB card](https://github.com/Filpin011/wallbox-web-card) (HACS) or
use the built-in Home Assistant cards
([examples](https://github.com/Filpin011/ha-wallbox-web#use-the-built-in-home-assistant-cards)).

## Known issues

- **The station does not appear:** it must be on the same network as Home Assistant (UDP announcements on port
  4023). Otherwise add it by hand in the app or with the option *Stations outside this network*.
- **"The ingress path changed: restart the Wallbox WEB add-on."** – restart the add-on (only happens after a
  reinstall).
- **Changing port 8423** requires restarting the add-on.

---

## Italiano

Wallbox WEB è la web app per configurare e monitorare le wallbox compatibili nella rete di casa: stato, avvio e
stop della ricarica, programmazioni, gestione della potenza, storico, costi e curve di ricarica. Con questo
add-on gira dentro Home Assistant OS:

- l'app è nella **barra laterale** (voce *Wallbox*) e ti riconosce con il tuo utente Home Assistant, senza un
  secondo login;
- le colonnine vengono **trovate da sole** (l'add-on usa la rete dell'host e riceve i loro annunci UDP);
- l'integrazione **Wallbox WEB** di Home Assistant viene **rilevata automaticamente** (nessun URL o token da
  copiare).

> **Progetto non ufficiale.** Non affiliato, approvato né supportato da SCAME PARRE S.p.A. Nessuna garanzia:
> lo usi a tuo rischio. Dettagli in [DISCLAIMER.md](https://github.com/Filpin011/ha-wallbox-web-addon/blob/main/DISCLAIMER.md).

### Installazione

1. Aggiungi il repository a Home Assistant con il pulsante in alto, oppure *Impostazioni › Componenti aggiuntivi ›
   Raccolta di componenti aggiuntivi › ⋮ › Repository* e incolla `https://github.com/Filpin011/ha-wallbox-web-addon`.
2. Installa **Wallbox WEB**, attiva *Mostra nella barra laterale* e *Watchdog*, poi **Avvia**.
3. Apri **Wallbox** nella barra laterale: entri già con il tuo utente. Accetta l'informativa e aggiungi la
   colonnina come nell'app.
4. *Impostazioni › Dispositivi e servizi*: compare **"Nuovo dispositivo trovato: Wallbox WEB"** → **Aggiungi**
   (serve l'integrazione Wallbox WEB installata da HACS).

### Accesso e utenti

| Da dove | Come entri |
|---|---|
| Barra laterale di Home Assistant (anche da remoto, es. Home Assistant Cloud) | automaticamente, con il tuo utente Home Assistant |
| `http://<IP di Home Assistant>:8423` nella rete di casa (es. il telefono come app) | login dell'app (e-mail/password o passkey) |

- Ogni utente Home Assistant che apre l'app ottiene un proprio account nell'app (stesso nome). Con l'opzione
  *Amministratori di Home Assistant = amministratori dell'app* (predefinita) gli amministratori di Home Assistant
  sono amministratori anche nell'app, gli altri utenti normali. La voce nella barra laterale è visibile solo agli
  amministratori.
- Questi account non hanno password: funzionano solo dalla barra laterale. In *Account* le voci *Cambia
  password* e *Aggiungi passkey* non servono per loro.
- **Primo avvio:** nel **log dell'add-on** trovi la password iniziale dell'utente `root` (riquadro *"Wallbox WEB –
  first login"*). Serve solo per l'accesso diretto sulla porta 8423: entra con `root` e quella password e completa
  la configurazione (e-mail + nuova password). Persa? Attiva *Reimposta la password dell'amministratore*,
  riavvia, leggi la nuova password nel log e **disattiva di nuovo l'opzione**.

### Opzioni

| Opzione | Significato |
|---|---|
| Livello di log | `info` normale, `debug` per la diagnosi (registra anche il traffico verso la colonnina). |
| Indirizzo della web app | Indirizzo dell'accesso diretto, se diverso da `http://<IP>:8423` (es. il tuo dominio https). |
| Altri indirizzi | Altri indirizzi da cui accedi direttamente, separati da virgola. |
| Colonnine fuori da questa rete | `ip` o `ip:porta` di colonnine su un'altra sottorete o in VPN. |
| Amministratori di Home Assistant = amministratori dell'app | vedi *Accesso e utenti*. |
| Reimposta la password dell'amministratore | nuova password di `root` nel log al prossimo avvio (poi disattivala). |

Con Home Assistant in italiano le opzioni sono mostrate in italiano.

**Rete** (scheda *Rete*): la porta **8423** è l'accesso diretto e quella usata dall'integrazione. Puoi cambiarla;
se la disattivi resta solo la barra laterale e l'integrazione non viene configurata da sola.

### Dati e backup

Utenti, sessioni, token, colonnine salvate, costi e curve di ricarica sono in `/data` dell'add-on e finiscono
nei **backup di Home Assistant**. Il backup è *a freddo*: l'add-on si ferma qualche secondo durante il backup
(le registrazioni delle ricariche riprendono subito dopo). La cache dei firmware scaricati è esclusa.

### Home Assistant o server self-hosted?

Usa **un solo server** per colonnina: se Wallbox WEB gira già sul tuo server (Coolify/Docker), non avviare anche
l'add-on sulla stessa colonnina (sarebbero due connessioni). L'add-on è la scelta più semplice se hai Home
Assistant OS: niente reverse proxy, discovery delle colonnine funzionante, backup inclusi.

### Dashboard

Con l'integrazione configurata aggiungi la [card Wallbox WEB](https://github.com/Filpin011/wallbox-web-card) (HACS)
oppure usa le card integrate di Home Assistant
([esempi](https://github.com/Filpin011/ha-wallbox-web/blob/main/README.it.md#usare-le-card-integrate-di-home-assistant)).

### Problemi noti

- **La colonnina non compare:** deve essere nella stessa rete di Home Assistant (annunci UDP sulla porta 4023).
  Altrimenti aggiungila a mano nell'app o con l'opzione *Colonnine fuori da questa rete*.
- **"The ingress path changed: restart the Wallbox WEB add-on."** – riavvia l'add-on (succede solo dopo una
  reinstallazione).
- **Cambiare la porta 8423** richiede il riavvio dell'add-on.
