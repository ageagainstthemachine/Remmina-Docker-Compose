# Remmina in Docker (Compose)

This repository provides a minimal Docker Compose setup for running [Remmina](https://remmina.org/) using the [LinuxServer.io Remmina image](https://docs.linuxserver.io/images/docker-remmina/). It maps a local `./config` folder for persistent settings and exposes a web UI on port `3144`.

---

## Compose file

Please see the compose file [here](docker-compose.yml).

---

## Quick start

1) Clone and enter the repo:
```bash
git clone https://github.com/ageagainstthemachine/Remmina-Docker-Compose.git
cd remmina-docker
````

2. Create the config directory (persisted in `./config`):

```bash
mkdir -p config
```

3. Open `docker-compose.yml` and set at least:

* `CUSTOM_USER` (login user)
* `PASSWORD` (login password)
* `TZ` (e.g., `America/Los_Angeles`)

> Note on PUID/PGID: This compose file sets `PUID=1026` and `PGID=100` by default. You generally do not need to change these unless you know what you're doing. There is more information [here](https://docs.linuxserver.io/images/docker-remmina/#user-group-identifiers).

4. Launch:

```bash
docker compose up -d
```

Then browse to:

```
http://localhost:3144
```

---

## Configuration

**Data directory**

* `./config` on the host is mounted to `/config` in the container (Remmina profiles and preference data persists here).

**Ports**

* Host `3144` → Container `3000` (web UI)

**Environment variables**

| Variable      | Purpose                                    | Default in this repo |
| ------------- | ------------------------------------------ | -------------------- |
| `CUSTOM_USER` | Web UI username                            | (set by you)         |
| `PASSWORD`    | Web UI password                            | (set by you)         |
| `TZ`          | Container timezone                         | (set by you)         |
| `PUID`        | Optional: host user ID for file ownership  | `1026`               |
| `PGID`        | Optional: host group ID for file ownership | `100`                |

---

## Notes on compose versions and commands

* **Modern compose (v2+)**: The `version:` key is optional and can be removed. The recommended command is `docker compose ...` (with a space).
* **Older setups**: You might still use `docker-compose ...` (hyphenated). Keeping `version: "3.9"` preserves compatibility with older environments.
* **File name**: Modern Docker will pick up `compose.yaml`, `compose.yml`, or `docker-compose.yml`. This repo uses `docker-compose.yml`.

---

## Common tasks

Pull updated image and recreate:

```bash
docker compose pull
docker compose up -d
```

Stop and remove the stack:

```bash
docker compose down
```

Remove the stack and the persisted `./config` volume mapping (data loss):

```bash
docker compose down -v
```

---

## Links

* Remmina [website](https://remmina.org/)
* Remmina [source](https://gitlab.com/Remmina/Remmina)
* LinuxServer Remmina image [docs](https://docs.linuxserver.io/images/docker-remmina/)
* Docker Compose [spec](https://compose-spec.io/)
* Docker [install](https://docs.docker.com/get-docker/)
