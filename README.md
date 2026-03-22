# 🐳 Docker Home Server Konfiguráció

Ez a mappa (`content`) tartalmazza az otthoni szerveremhez használt Docker Compose konfigurációs (`.yaml`) fájlokat. A szolgáltatások külön fájlokba vannak szedve a könnyebb kezelhetőség, átláthatóság és skálázhatóság érdekében.

## 📑 Tartalomjegyzék
1. [Tartalmazott Szolgáltatások](#-tartalmazott-szolgáltatások)
2. [Általános Telepítés és Frissítés](#-általános-telepítés-és-frissítés)
3. [Részletes Beállítási Útmutatók (Wiki)](#-részletes-beállítási-útmutatók-wiki)
4. [Támogatás](#-támogatás-support)

---

## 📦 Tartalmazott Szolgáltatások

Kattints a fájlnevekre a pontos konfigurációk (YAML kódok) megtekintéséhez:

* **[calibre.yaml](content/calibre.yaml)**: E-könyv szerver (Calibre / Calibre-Web) a digitális könyvtár kezeléséhez.
* **[compose.yaml](content/compose.yaml)**: Alapértelmezett / központi docker-compose fájl.
* **[influxdb-grafana.yaml](content/influxdb-grafana.yaml)**: InfluxDB adatbázis és Grafana vizualizációs platform.
* **[nginx-revproxy.yaml](content/nginx-revproxy.yaml)**: Nginx Proxy Manager a biztonságos (HTTPS) kiajánláshoz.
* **[pihole.yaml](content/pihole.yaml)**: Hálózati szintű reklámblokkoló és privát DNS szerver.
* **[plex.yaml](content/plex.yaml)**: Médiaszerver a filmek, sorozatok és zenék streameléséhez.
* **[portainer-agent.yaml](content/portainer-agent.yaml)**: Portainer Agent a Docker környezet távoli kezeléséhez.
* **[qbittorrent.yaml](content/qbittorrent.yaml)**: qBittorrent webes felülettel rendelkező letöltőkliens.

---

## 🚀 Általános Telepítés és Frissítés

Mivel a szolgáltatások külön `.yaml` fájlokban vannak, az indításukhoz és frissítésükhöz meg kell adni a `-f` (fájl) paramétert a Docker Compose parancsban.

### Indítás (Deploy)
1. Lépj be a fájlokat tartalmazó könyvtárba:
   ```bash
   cd /útvonal/a/content/mappához
   ````

2.  Indítsd el a kiválasztott szolgáltatást (pl. Plex) a háttérben:
    ```bash
    docker compose -f plex.yaml up -d
    ```

### Frissítés (Update)

1.  Töltsd le a legújabb image-et az adott szolgáltatáshoz:
    ```bash
    docker compose -f plex.yaml pull
    ```
2.  Indítsd újra a konténert (a beállításaid és adataid megmaradnak):
    ```bash
    docker compose -f plex.yaml up -d
    ```
3.  Opcionálisan töröld a régi, már nem használt image-eket a helyfelszabadításhoz:
    ```bash
    docker image prune -f
    ```

-----

## 📖 Részletes Beállítási Útmutatók (Wiki)

Egyes szolgáltatások hálózati szintű, komplexebb beállításokat igényelnek. Ezekhez részletes, lépésről-lépésre leírások készültek a Wikiben. Kattints a linkekre a megtekintésükhöz:

  * 🛡️ **[Pi-hole Belső DNS beállítása Cloudflare alapon](https://github.com/berbekarp/Docker/wiki/Pi%E2%80%90hole)**
  * 🌐 **[Nginx Proxy Manager & Cloudflare SSL beállítása](https://github.com/berbekarp/Docker/wiki/Nginx-Proxy-Manager)**
  * 🔔 **[Watchtower és Diun beállítása (Docker konténer figyelők)](https://github.com/berbekarp/Docker/wiki/Watchtower-Duin)**

----

## ☕ Támogatás (Support)

Ha hasznosnak találod ezeket a Home Assistant kártyákat és dashboardokat, és szeretnéd megköszönni a fejlesztésükbe és dokumentálásukba fektetett időt, egy virtuális kávéval megteheted! Bármilyen apró támogatást hatalmas köszönettel fogadok. 🙏

[![Revolut](https://img.shields.io/badge/Revolut-Support-black?style=for-the-badge&logo=revolut)](https://revolut.me/berbekarp)

**Revolut azonosító:** `@berbekarp`  