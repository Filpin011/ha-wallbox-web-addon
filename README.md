# Wallbox WEB – add-on per Home Assistant (non ufficiale)

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

---

## English

**Independent, unofficial project** – not affiliated with, endorsed, sponsored or supported by SCAME PARRE S.p.A.
It is based on a study of how the app and the wallboxes communicate on the local network (interoperability) and
uses no Scame logos. No warranty, use at your own risk; electrical work must be done by a qualified installer
according to local regulations. See [DISCLAIMER.md](DISCLAIMER.md).

This repository provides the **Wallbox WEB** add-on for Home Assistant OS / Supervised: the web app for
compatible wallboxes on your network, in the Home Assistant sidebar, with automatic sign-in of Home Assistant
users, station discovery on the host network and automatic discovery of the Wallbox WEB integration. Click the
button above to add the repository, install **Wallbox WEB**, enable *Show in sidebar* and *Watchdog*, start it.
Supported architectures: amd64, aarch64.

---

## Per i manutentori / For maintainers

How this repository works and why (compared with large add-on projects):

| Topic | Choice | Reference projects |
|---|---|---|
| Layout | one repository, one folder per add-on (`wallbox_web/`), `repository.yaml` at the root. A beta channel, if ever needed, is a second folder (`wallbox_web_beta/`, same image with a `beta` tag) | folders per channel: [esphome/home-assistant-addon](https://github.com/esphome/home-assistant-addon) (`esphome`, `esphome-beta`, `esphome-dev`), [music-assistant/home-assistant-addon](https://github.com/music-assistant/home-assistant-addon), [frigate-hass-addons](https://github.com/blakeblackshear/frigate-hass-addons), [hassio-zigbee2mqtt](https://github.com/zigbee2mqtt/hassio-zigbee2mqtt) (`-edge`); separate repositories per channel: [hassio-addons/repository-beta](https://github.com/hassio-addons/repository-beta) / [-edge](https://github.com/hassio-addons/repository-edge) |
| Image | **prebuilt multi-arch image** `ghcr.io/filpin011/wallbox-web-addon` (amd64 + aarch64 in one manifest, no `{arch}`), tag = `version`; nothing is built on the device | same pattern as ESPHome (`ghcr.io/esphome/esphome-hassio`), Frigate (`ghcr.io/blakeblackshear/frigate`) and [home-assistant/apps-example](https://github.com/home-assistant/apps-example) |
| Build | the image is built by the (private) application repository with plain `docker buildx` (one native Next.js build, `npm ci` per architecture) – not `home-assistant/builder`, which targets add-ons built from a Home Assistant base image | [contributors.home-assistant.io › Publishing](https://contributors.home-assistant.io/apps/guides/publishing/) |
| Base image / init | Node.js image without s6-overlay → `init: true` (Docker's tini is PID 1). The Home Assistant base images with s6-overlay need `init: false` instead | [configuration reference](https://contributors.home-assistant.io/apps/reference/configuration/) |
| Labels | `io.hass.type=app`, `io.hass.version`, `io.hass.arch` (per architecture), OCI `source` = this repository, description with the disclaimer | [Dockerfile guide](https://contributors.home-assistant.io/apps/guides/dockerfile/) |
| AppArmor | `apparmor: true` with the Supervisor's default profile. A custom `apparmor.txt` (as in apps-example) will be added after profiling the add-on in complain mode on a real system – a wrong profile breaks the add-on | [security guide](https://contributors.home-assistant.io/apps/guides/security/) |
| Releases | fully automatic: the application's release workflow pushes the image, then commits the new `version` + changelog entry here and tags `v<version>`; the linter below checks that the image of the configured version exists | Frigate / ESPHome pin a fixed `version` that a bump workflow updates |
| CI | [frenck/action-addon-linter](https://github.com/frenck/action-addon-linter) (renamed *action-app-linter*) on every push / PR + weekly; image existence check | used by apps-example and ESPHome |
| Dependencies | Dependabot for GitHub Actions (weekly, grouped). Renovate is equally common (apps-example, hassio-addons) | |
| Branch protection | protect `main`: require the *Lint* checks; allow the release bot (fine-grained token of the maintainer) to push | |

The add-on's own documentation for users is [wallbox_web/DOCS.md](wallbox_web/DOCS.md); translations of the
options are in [wallbox_web/translations](wallbox_web/translations).

License: [MIT](LICENSE) for the files of this repository. The container image contains the Wallbox WEB application,
distributed as a compiled image under its own terms (see [LICENSE](LICENSE) and [DISCLAIMER.md](DISCLAIMER.md)).
