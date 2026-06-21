# NowyBot — Kick Viewer (2026)

Lekki bot widzów na Kick.com — terminal dashboard, WebSocket, tryb Stability.  
Bez przeglądarek, działa na słabszym PC. Obsługa **bez proxy** (test) i skali do **30 000** botów.

> **Repozytorium prywatne** — nie udostępniaj proxy, tokenów ani danych logowania.

---

## Funkcje

- **WebSocket** `websockets.kick.com/viewer/v1` — handshake, ping, Pusher
- **Stability mode** — `user_event` co ~30s (`tracking.user.watch.livestream`)
- **Auto-reconnect** + świeży token + **watchdog 95%**
- **HQ token flow** — symulacja wejścia usera (homepage → kanał → API → playback → token)
- **Token pool** — pre-warm tokenów przy starcie (gdy Stability Y)
- **Fast ramp** (`--fast-ramp`) — szybki token bez HQ (duża skala, gorsze retention)
- **Burst start** — stagger 0 domyślnie (wątki startują naraz)
- **Bez proxy** — test lokalny (Kick liczy ~1 widza z IP)
- **Fingerprint Chrome/Firefox** — spójne pary UA + TLS + Client Hints (jak F12)
- **Dashboard Rich** w terminalu — lite mode przy 5000+ botów
- **Opcjonalnie HLS** — streamlink (więcej bandwidthu)
- **Retention HQ** — status pełnego profilu pod utrzymanie średniej widzów

---

## Wymagania

- Python 3.10+
- Windows / Linux
- Proxy HTTP residential (np. [Webshare](https://www.webshare.io/)) — opcjonalne przy teście bez proxy
- Stream **LIVE** na Kick

---

## Instalacja

```powershell
git clone https://github.com/TWOJ_USER/TWOJE_REPO.git
cd TWOJE_REPO

pip install -r requirements.txt
```

Aktualizacja zależności do najnowszych z PyPI:

```powershell
py upgrade_requirements.py
pip install -r requirements.txt --upgrade
```

Skopiuj przykładowy plik proxy (opcjonalnie):

```powershell
copy proxies.example.txt proxies.txt
```

Format proxy: `host:port:user:pass`

---

## Uruchomienie

```powershell
py main.py
```

### Menu interaktywne

**1. Proxy**

| Wybór | Opis |
|-------|------|
| **0** | Bez proxy — lokalne IP, dowolna liczba botów (test) |
| **1** | Plik lokalny (`proxies.txt`) |
| **2** | URL (download link Webshare) + liczba botów |
| **4** | **Bez limitu** — rotacja puli proxy (np. 100 proxy → 5000 connections; Enter = proxy × 50) |

**2. Kanał** — nazwa lub URL `kick.com/nazwa`

**3. Liczba widzów** — dowolna (opcja **4**: connections niezależne od liczby proxy)

**4. Opcje Y/n** (tylko te trzy):

| Pytanie | Domyślnie | Opis |
|---------|-----------|------|
| HLS keepalive | N | Więcej bandwidthu — wyłącza Retention HQ |
| Pusher subscribe | Y | Subskrypcje channel + chatroom |
| Stability mode | Y | `user_event` + auto-reconnect + token pool |

Po Y/n bot pokazuje blok **Retention HQ** (TAK/NIE + powód).

**Włączone domyślnie** (bez pytań): dashboard, watchdog, **burst stagger 0**, token pool (gdy Stability Y).  
**Fast ramp domyślnie NIE** — włącz tylko flagą `--fast-ramp` gdy chcesz szybki start kosztem retention.

### Flagi CLI

```powershell
py main.py --no-proxy
py main.py --total 500 --channel nazwa
py main.py --proxy-file proxies.txt
py main.py --proxy-url "https://..."
py main.py --max-proxy --proxy-url "https://..." --total 5000
py main.py --fast-ramp                    # szybki token (Retention HQ = NIE)
py main.py --token-workers 48             # więcej równoległych requestów tokena
py main.py --stagger 0.5                  # opóźnienie między startem botów (s)
py main.py --no-hls --no-pusher
py main.py --no-watchdog --no-dashboard
py main.py --slow                         # start wsadami (batch 100, delay 30s)
```

---

## Retention HQ — co to jest?

**Retention HQ** to nie osobna opcja w menu — bot **liczy status** z ustawień:

| Warunek | Wymagane |
|---------|----------|
| Stability | Y |
| Pusher | Y |
| HLS | N |
| Fast ramp | NIE (bez `--fast-ramp`) |

### Retention HQ = TAK

- Pełny **HQ token** przy pierwszym połączeniu (symulacja przeglądarki)
- `channel_handshake` co 15s
- `tracking.user.watch.livestream` co ~30s
- `pusher:ping` co 20s + re-subscribe co 3 min
- Auto-reconnect + watchdog
- **Wolniejszy start**, lepsze utrzymanie widza / średniej

### Retention HQ = NIE

Dashboard poda powód, np. `NIE (HLS ON)` lub `NIE (Fast ramp)`.

| Powód | Efekt |
|-------|--------|
| **HLS ON** | Więcej bandwidthu, gorsze retention |
| **`--fast-ramp`** | Szybki token od razu, bez HQ flow |
| **Pusher N** | Brak subskrypcji Pusher na WS |
| **Stability N** | Brak reconnect i token pool — bot umiera po błędzie |

### HQ token vs fast token

| Tryb | HTTP przed tokenem | Kiedy |
|------|-------------------|--------|
| **HQ** | kick.com → kanał → API → playback → token | Pierwszy connect (Retention HQ) |
| **Fast** | kick.com → token | Reconnect, `--fast-ramp`, token z poola |

> **Uwaga:** przy Stability Y token pool może podać **fast token** z pre-warm zanim bot zdąży zrobić HQ — start szybszy, retention trochę słabsze niż „czysty” HQ.

---

## Szybkość startu (Connected na dashboardzie)

**Wątki** odpalają się prawie natychmiast (burst, stagger 0).  
**Connected** rośnie wolniej — limituje **pobieranie tokena HTTP** (token workers + jakość proxy).

| Boty | Token workers (auto) | Szac. ramp-up (dobre proxy) |
|------|------------------------|----------------------------|
| 230 | 16 | ~1–3 min |
| 500 | 24 | ~2–5 min |
| 3000 | 48 | ~5–15 min |

Przy starcie bot wypisuje `Szac. ramp-up: ~X min`.

| Profil | Start | Retention |
|--------|-------|-----------|
| Domyślny (Retention HQ) | Średni | Lepszy |
| `--fast-ramp` | **Szybki** | Gorszy |
| `--token-workers 64` | Szybszy (więcej równoległych tokenów) | — |

Patrz na dashboard: **`Connected X/Y`** — to realna prędkość wejścia.

---

## Fingerprint (UA + TLS + Client Hints)

Każdy bot dostaje **spójną parę** UA + `tls_client` (Chrome 149/150, Firefox 151/152 — czerwiec 2026).

Nagłówki jak prawdziwy Chrome z F12 na Kick:

- `sec-ch-ua`: `"Not)A;Brand";v="24"`
- `sec-ch-ua-full-version` / `sec-ch-ua-full-version-list`
- `sec-ch-ua-arch`, `sec-ch-ua-bitness`, `sec-ch-ua-platform-version`
- `x-app-platform: web`
- `accept-encoding: gzip, deflate, br, zstd`

Bot symuluje widza na `kick.com/kanał` (nie dashboard streamera).

---

## Tryb bez proxy

Wybierz **0** lub `--no-proxy`.

- Dowolna liczba botów (test połączeń, dashboardu)
- Kick **deduplikuje po IP** — ~1 widz na liczniku
- Do realnych widzów na streamie: proxy residential **1:1**

---

## Skala masowa (do 30 000)

| Wymaganie | Uwagi |
|-----------|-------|
| Unikalne proxy | 1:1 = max widzów na Kick; rotacja (opcja 4) = więcej WS, nie więcej IP |
| Stability Y | Utrzymanie średniej |
| HLS N | Oszczędność bandwidth i RAM |
| Retention HQ | Domyślnie TAK (bez `--fast-ramp`) |
| `--fast-ramp` | Tylko gdy liczy się szybkość, nie średnia 30d |
| Jeden PC | Realnie ~2–8k stabilnych wątków |

```powershell
# Szybka skala (retention gorsze):
py main.py --total 3000 --channel NAZWA --proxy-url "LINK" --fast-ramp --no-hls --stagger 0

# Retention (wolniejszy start):
py main.py --total 500 --channel NAZWA --proxy-file proxies.txt
```

---

## Oszczędzanie bandwidth (Webshare)

| Opcja | Zużycie | Zostaw? |
|-------|---------|---------|
| **HLS** | największe | **NIE** przy limicie GB |
| Stability + WS | minimalne | **TAK** |
| Pusher | prawie zero | **TAK** |

---

## Struktura projektu

```
.
├── main.py                  # główny bot (monolit)
├── bezproxy.py              # fork masowy (opcjonalny)
├── upgrade_requirements.py  # odświeża requirements.txt z PyPI
├── requirements.txt
├── proxies.example.txt
├── proxies.txt              # gitignore — nie commituj!
├── bot.log                  # gitignore
├── .gitignore
└── README.md
```

---

## Wgranie na GitHub

### 1. Utwórz repo

GitHub → **New repository** → np. `kick-nowybot` → **Private** → bez README.

### 2. Push

```powershell
cd C:\sciezka\do\projektu

git init
git add .
git commit -m "NowyBot — Kick viewer 2026"
git branch -M main
git remote add origin https://github.com/TWOJ_USER/kick-nowybot.git
git push -u origin main
```

### 3. Czego NIE commitować

- `proxies.txt`, `bot.log`, `__pycache__/`, tokeny, hasła

Są w `.gitignore`.

---

## Show Stopper (średnia 50 widzów / 30 dni)

Achievement liczy **średnią z 30 dni**, nie chwilowy spike.

| Przyczyna spadku | Co robić |
|------------------|----------|
| Brak `user_event` | **Stability: Y** |
| Brak Pusher | **Pusher: Y** |
| HLS włączone | **HLS: N** |
| `livestream_id` nieaktualne | Auto-refresh co 30s (w kodzie) |
| WS umiera | Watchdog 95% + auto-reconnect |
| Bot wyłączony po streamie | Trzymaj bota LIVE podczas streamu |
| Za mało proxy | 1 proxy = 1 widz na Kick |

**Wskazówki:**

1. **Retention HQ = TAK** (domyślnie przy Y/Y/N bez fast ramp)
2. **1 proxy = 1 widz** — rotacja nie zwiększa licznika IP
3. Stream **LIVE**
4. Dashboard: `Kick Viewers (+X)` i `Connected X/Y`

---

## Zależności (06/2026)

| Pakiet | Wersja | Po co |
|--------|--------|-------|
| `tls_client` | 1.0.1 | TLS fingerprint (Chrome 149/150) |
| `websocket-client` | 1.9.0 | połączenie WSS |
| `requests` | 2.34.2 | pobieranie proxy z URL |
| `rich` | 15.0.0 | dashboard terminalowy |
| `streamlink` | 8.4.0 | opcjonalny HLS manifest |

---

## Rozwiązywanie problemów

| Problem | Rozwiązanie |
|---------|-------------|
| `Nie udało się pobrać tokena WS` | Sprawdź proxy, zmniejsz skalę, `--token-workers`, stagger 0.3–1s |
| Mało Connected po długim czasie | Rate-limit proxy; 1:1 residential; bez rotacji ×50 na słabe proxy |
| Średnia spada | Retention HQ TAK, Stability Y, Pusher Y, HLS N |
| Wolny start | Normalne przy HQ; `--fast-ramp` lub `--token-workers 48` |
| Wysokie zużycie GB | HLS = N |
| `botów > proxy` | Mniej botów lub więcej proxy |
| Bez proxy — licznik nie rośnie | Normalne — 1 widz z IP |

---

## Disclaimer

Narzędzie edukacyjne / do testów własnego kanału.  
Użytkowanie może naruszać regulamin Kick.com — odpowiedzialność po stronie użytkownika.