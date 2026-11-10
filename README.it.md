# Wallbox WEB – add-on per Home Assistant (non ufficiale)

🇬🇧 [English](README.md)

[![Aggiungi il repository a Home Assistant](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2FFilpin011%2Fha-wallbox-web-addon)

> **Progetto indipendente e non ufficiale.** Non affiliato, approvato, sponsorizzato né supportato da
> SCAME PARRE S.p.A. Nasce da uno studio di come l'app e le wallbox comunicano sulla rete locale
> (interoperabilità), non usa loghi Scame. Software fornito senza garanzia: lo usi a tuo rischio. Gli interventi
> elettrici vanno eseguiti secondo le norme da un installatore qualificato. Leggi [DISCLAIMER.md](DISCLAIMER.md).

Questo repository contiene l'add-on **Wallbox WEB** per Home Assistant OS / Supervised: la web app per
configurare e monitorare le wallbox compatibili nella rete di casa, direttamente nella barra laterale di Home
Assistant.

| Add-on | Descrizione |
|---|---|
| [Wallbox WEB](wallbox_web) | Web app nella barra laterale (accesso automatico con l'utente Home Assistant), colonnine trovate da sole sulla rete dell'host, integrazione Home Assistant rilevata automaticamente. |

## Installazione

1. Premi il pulsante qui sopra (oppure *Impostazioni › Componenti aggiuntivi › Raccolta di componenti
   aggiuntivi › ⋮ › Repository* e incolla `https://github.com/Filpin011/ha-wallbox-web-addon`).
2. Installa **Wallbox WEB**, attiva *Mostra nella barra laterale* e *Watchdog*, avvia.
3. Apri **Wallbox** nella barra laterale. La documentazione completa è nella scheda *Documentazione*
   dell'add-on ([wallbox_web/DOCS.md](wallbox_web/DOCS.md)).

Requisiti: Home Assistant OS o Supervised, processore **amd64** o **aarch64** (es. Raspberry Pi 4/5 a 64 bit,
Home Assistant Green/Yellow, mini PC).

Le opzioni dell'add-on seguono la lingua di Home Assistant (**inglese** di default, **italiano** disponibile); la
scheda *Documentazione* è in inglese con una sezione in italiano in fondo.

Note per i manutentori (struttura del repository, immagine, rilasci): [README in inglese](README.md#for-maintainers).

Licenza: [MIT](LICENSE) per i file di questo repository. L'immagine del container contiene l'applicazione Wallbox
WEB, distribuita come immagine compilata secondo i propri termini (vedi [LICENSE](LICENSE) e
[DISCLAIMER.md](DISCLAIMER.md)).
