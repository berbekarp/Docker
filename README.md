# 🐳 Docker Home Server Konfiguráció

Ez a mappa (`content`) tartalmazza az otthoni szerveremhez használt Docker Compose konfigurációs (`.yaml`) fájlokat. A szolgáltatások külön fájlokba vannak szedve a könnyebb kezelhetőség, átláthatóság és skálázhatóság érdekében.

## 📦 Tartalmazott Szolgáltatások (Stackek)

Az alábbi konténerek telepítési leírásai találhatók meg a mappában:

* **`calibre.yaml`**: E-könyv szerver (Calibre / Calibre-Web) a digitális könyvtár kezeléséhez és böngészéséhez.
* **`compose.yaml`**: Alapértelmezett / központi docker-compose fájl (általános hálózatok, vagy alap szolgáltatások definiálásához).
* **`influxdb-grafana.yaml`**: InfluxDB idősoros adatbázis és Grafana vizualizációs platform (kiváló a Home Assistant adatok hosszú távú tárolására és gyönyörű grafikonok készítésére).
* **`nginx-revproxy.yaml`**: Nginx Reverse Proxy (pl. Nginx Proxy Manager) a szolgáltatások biztonságos, HTTPS (SSL) alapon történő kiajánlásához az internet felé.
* **`pihole.yaml`**: Hálózati szintű reklámblokkoló és privát DNS szerver (Pi-hole).
* **`plex.yaml`**: Médiaszerver a filmek, sorozatok és zenék streameléséhez bármilyen eszközre.
* **`portainer-agent.yaml`**: Portainer Agent, amely lehetővé teszi a Docker környezet távoli, grafikus felületen történő kezelését egy központi Portainer példányból.
* **`qbittorrent.yaml`**: qBittorrent webes felülettel rendelkező letöltőkliens.

---

## 🚀 Telepítés (Deploy)

Mivel a szolgáltatások külön `.yaml` fájlokban vannak, az indításukhoz meg kell adni a `-f` (fájl) paramétert a Docker Compose parancsban.

1. Lépj be a fájlokat tartalmazó könyvtárba:
   ```bash
   cd /útvonal/a/content/mappához
   ````

2.  Indíts el egy adott szolgáltatást a háttérben (`-d` flag):
    ```bash
    docker compose -f fajlnev.yaml up -d
    ```

**Példa a Plex szerver elindítására:**

```bash
docker compose -f plex.yaml up -d
```

*(Tipp: Ha van olyan szolgáltatás, ami függ egy másiktól – pl. minden a reverse proxyn keresztül megy –, érdemes először az `nginx-revproxy.yaml`-t elindítani).*

-----

## 🔄 Frissítés (Update)

A konténerek (image-ek) frissítése nagyon egyszerű, és szolgáltatásonként külön is elvégezhető az alábbi lépésekkel:

1.  Lépj be a fájlokat tartalmazó könyvtárba:

    ```bash
    cd /útvonal/a/content/mappához
    ```

2.  Töltsd le a legújabb Docker image-et az adott szolgáltatáshoz:

    ```bash
    docker compose -f fajlnev.yaml pull
    ```

3.  Indítsd újra a konténert (a Docker automatikusan újraalkotja az új image alapján, az adataid a volume-okban megmaradnak):

    ```bash
    docker compose -f fajlnev.yaml up -d
    ```

4.  **(Opcionális)** Töröld a régi, már nem használt image-eket, hogy helyet szabadíts fel a szerveren:

    ```bash
    docker image prune -f
    ```

**Példa a Pi-hole teljes frissítésére:**

```bash
docker compose -f pihole.yaml pull
docker compose -f pihole.yaml up -d
docker image prune -f
```

---
## ☕ Támogatás (Support)

Ha hasznosnak találod ezeket a konfigurációkat és leírásokat, egy virtuális kávéval megteheted, hogy támogatod a további munkámat! Bármilyen apró támogatást hatalmas köszönettel fogadok. 🙏

[![Revolut](https://img.shields.io/badge/Revolut-Support-black?style=for-the-badge&logo=revolut)](https://revolut.me/berbekarp)

**Revolut azonosító:** `@berbekarp`  