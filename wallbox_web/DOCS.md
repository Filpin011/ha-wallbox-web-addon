# Wallbox WEB – documentazione dell'add-on

> **Progetto non ufficiale.** Non affiliato, approvato né supportato da SCAME PARRE S.p.A. Nessuna garanzia:
> lo usi a tuo rischio. Dettagli in [DISCLAIMER.md](https://github.com/Filpin011/ha-wallbox-web-addon/blob/main/DISCLAIMER.md).
> *Unofficial project, not affiliated with SCAME PARRE S.p.A., no warranty – English summary at the end.*

Wallbox WEB è la web app per configurare e monitorare le wallbox compatibili nella rete di casa: stato, avvio e
stop della ricarica, programmazioni, gestione della potenza, storico, costi e curve di ricarica. Con questo
add-on gira dentro Home Assistant OS:

- l'app è nella **barra laterale** (voce *Wallbox*) e ti riconosce con il tuo utente Home Assistant, senza un
  secondo login;
- le colonnine vengono **trovate da sole** (l'add-on usa la rete dell'host e riceve i loro annunci UDP);
- l'integrazione **Wallbox WEB** di Home Assistant viene **rilevata automaticamente** (nessun URL o token da
  copiare).

## Installazione

1. Aggiungi il repository a Home Assistant:

   [![Aggiungi il repository a Home Assistant](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2FFilpin011%2Fha-wallbox-web-addon)

   oppure *Impostazioni › Componenti aggiuntivi › Raccolta di componenti aggiuntivi › ⋮ › Repository* e incolla
   `https://github.com/Filpin011/ha-wallbox-web-addon`.
2. Installa **Wallbox WEB**, attiva *Mostra nella barra laterale* e *Watchdog*, poi **Avvia**.
3. Apri **Wallbox** nella barra laterale: entri già con il tuo utente. Accetta l'informativa e aggiungi la
   colonnina come nell'app.
4. *Impostazioni › Dispositivi e servizi*: compare **"Nuovo dispositivo trovato: Wallbox WEB"** → **Configura**
   (serve l'integrazione Wallbox WEB installata da HACS).

## Accesso e utenti

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

## Opzioni

| Opzione | Significato |
|---|---|
| Livello di log | `info` normale, `debug` per la diagnosi (registra anche il traffico verso la colonnina). |
| Indirizzo della web app | Indirizzo dell'accesso diretto, se diverso da `http://<IP>:8423` (es. il tuo dominio https). |
| Altri indirizzi | Altri indirizzi da cui accedi direttamente, separati da virgola. |
| Colonnine fuori da questa rete | `ip` o `ip:porta` di colonnine su un'altra sottorete o in VPN. |
| Amministratori di Home Assistant = amministratori dell'app | vedi *Accesso e utenti*. |
| Reimposta la password dell'amministratore | nuova password di `root` nel log al prossimo avvio (poi disattivala). |

**Rete** (scheda *Rete*): la porta **8423** è l'accesso diretto e quella usata dall'integrazione. Puoi cambiarla;
se la disattivi resta solo la barra laterale e l'integrazione non viene configurata da sola.

## Dati e backup

Utenti, sessioni, token, colonnine salvate, costi e curve di ricarica sono in `/data` dell'add-on e finiscono
nei **backup di Home Assistant**. Il backup è *a freddo*: l'add-on si ferma qualche secondo durante il backup
(le registrazioni delle ricariche riprendono subito dopo). La cache dei firmware scaricati è esclusa.

## Home Assistant o server self-hosted?

Usa **un solo server** per colonnina: se Wallbox WEB gira già sul tuo server (Coolify/Docker), non avviare anche
l'add-on sulla stessa colonnina (sarebbero due connessioni). L'add-on è la scelta più semplice se hai Home
Assistant OS: niente reverse proxy, discovery delle colonnine funzionante, backup inclusi.

## Problemi noti

- **La colonnina non compare:** deve essere nella stessa rete di Home Assistant (annunci UDP sulla porta 4023).
  Altrimenti aggiungila a mano nell'app o con l'opzione *Colonnine fuori da questa rete*.
- **"The ingress path changed: restart the Wallbox WEB add-on."** – riavvia l'add-on (succede solo dopo una
  reinstallazione).
- **Cambiare la porta 8423** richiede il riavvio dell'add-on.

---

## English summary

Wallbox WEB runs inside Home Assistant OS: the app is in the **sidebar** (you are signed in with your Home
Assistant user; Home Assistant administrators are app administrators), stations are **discovered
automatically** on the host network, and the **Wallbox WEB integration** is offered automatically
(*Settings › Devices & services › Discovered*). Direct access with the app's own login:
`http://<Home Assistant IP>:8423`. The first-run password of `root` is printed in the add-on log. Data lives in
the add-on's `/data` and is included in Home Assistant backups (cold backup). Run only one Wallbox WEB server per
station. Unofficial project, not affiliated with SCAME PARRE S.p.A., no warranty – see
[DISCLAIMER.md](https://github.com/Filpin011/ha-wallbox-web-addon/blob/main/DISCLAIMER.md).
