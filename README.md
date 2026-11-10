# Wallbox WEB – Home Assistant add-on (unofficial)

🇮🇹 [Italiano](README.it.md)

[![Add the repository to Home Assistant](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2FFilpin011%2Fha-wallbox-web-addon)

> **Independent, unofficial project.** Not affiliated with, endorsed, sponsored or supported by SCAME PARRE S.p.A.
> It comes from a study of how the app and the wallboxes communicate on the local network (interoperability) and
> uses no Scame logos. Software provided without warranty: use it at your own risk. Electrical work must be done
> by a qualified installer according to local regulations. Read [DISCLAIMER.md](DISCLAIMER.md).

This repository contains the **Wallbox WEB** add-on for Home Assistant OS / Supervised: the web app to configure
and monitor compatible wallboxes on your home network, right in the Home Assistant sidebar.

| Add-on | Description |
|---|---|
| [Wallbox WEB](wallbox_web) | Web app in the sidebar (automatic sign-in with your Home Assistant user), stations discovered automatically on the host network, Home Assistant integration discovered automatically. |

The add-on's options follow your Home Assistant language (**English** by default, **Italian** available); the
*Documentation* tab is in English with an Italian section at the end.

## Installation

1. Press the button above (or *Settings › Add-ons › Add-on store › ⋮ › Repositories* and paste
   `https://github.com/Filpin011/ha-wallbox-web-addon`).
2. Install **Wallbox WEB**, enable *Show in sidebar* and *Watchdog*, start it.
3. Open **Wallbox** in the sidebar. The full documentation is in the add-on's *Documentation* tab
   ([wallbox_web/DOCS.md](wallbox_web/DOCS.md)).
4. Optional: install the [Wallbox WEB integration](https://github.com/Filpin011/ha-wallbox-web) (HACS) – Home
   Assistant then offers it under *Settings › Devices & services › Discovered* – and the
   [dashboard card](https://github.com/Filpin011/wallbox-web-card).

Requirements: Home Assistant OS or Supervised, **amd64** or **aarch64** processor (e.g. 64-bit Raspberry Pi 4/5,
Home Assistant Green/Yellow, mini PC).

## Troubleshooting

See *Known issues* in the add-on's *Documentation* tab ([wallbox_web/DOCS.md](wallbox_web/DOCS.md#known-issues)).
For bugs, open an issue with the add-on log (Settings › Add-ons › Wallbox WEB › *Log*); never paste tokens or
passwords.

---

## For maintainers

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
