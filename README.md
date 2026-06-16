# 🎙️ Polish Kick TTS

**Darmowy i nowoczesny system Text-to-Speech dla polskich streamerów Kick.com**

---

## 🚀 Użyj TTS

**Link do Generatora TTS:** [https://89891383.github.io/Polish-Kick-TTS/tts.html](https://89891383.github.io/Polish-Kick-TTS/tts.html)

---

## 📖 Jak używać

### 1. Wygeneruj link
- Otwórz [link do TTS](https://89891383.github.io/Polish-Kick-TTS/tts.html)
- Wpisz nazwę swojego kanału na Kicku
- Dostosuj ustawienia (wybierz jeden z 17 głosów, głośność, uprawnienia)
- Skopiuj wygenerowany link

### 2. Dodaj do OBS
- Dodaj **Źródło przeglądarki (Browser Source)** w OBS / Streamlabs
- Wklej skopiowany link
- Ustaw wymiary: **800x600** (rozmiar nie ma większego znaczenia, źródło będzie niewidoczne)
- Gotowe! 🎉

### 3. Użycie na czacie
Widzowie (posiadający uprawnienia) piszą wiadomości zaczynające się od wykrzyknika i `tts`:
```
!tts Witam na streamie!
```

---

## ⚙️ Funkcje

- ✅ **17 polskich głosów** (Oddcast, Microsoft, Streamlabs/Amazon Polly, StreamElements)
- ✅ **Regulacja prędkości** (-3 do +3 dla głosów Oddcast i Microsoft)
- ✅ **Kontrola głośności** (0-100)
- ✅ **Nowoczesny przedrostek `!tts`**
- ✅ **System uprawnień** (Każdy, Moderator, VIP, OG, Subskrybent, Obserwujący)
- ✅ **Opcjonalne czytanie nicku** ("Nick mówi: ...")
- ✅ **Filtrowanie/czytanie linków i emotek**
- ✅ **Komenda !skiptts** dla streamera do szybkiego pomijania spamu
- ✅ **Automatyczne ignorowanie botów** (Botrix, Kickbot itp.)

---

## 🎤 Dostępne głosy

| Głos | Płeć | Dostawca / Silnik |
|------|------|-------------------|
| Zosia | Kobieta | Oddcast (Domyślny) |
| Agatka | Kobieta | Oddcast |
| Danota | Kobieta | Oddcast |
| Krzysztof | Mężczyzna | Oddcast |
| Wojciech | Mężczyzna | Oddcast |
| Adam | Mężczyzna | Microsoft |
| Ola | Kobieta | Streamlabs (Amazon Polly) |
| Ewa | Kobieta | Streamlabs (Amazon Polly) |
| Maja | Kobieta | Streamlabs (Amazon Polly) |
| Jacek | Mężczyzna | Streamlabs (Amazon Polly) |
| Jan | Mężczyzna | Streamlabs (Amazon Polly) |
| SE-WavenetA | Kobieta | StreamElements |
| SE-WavenetB | Mężczyzna | StreamElements |
| SE-Jacek | Mężczyzna | StreamElements |
| SE-Maja | Kobieta | StreamElements |
| SE-Ewa | Kobieta | StreamElements |
| SE-Jan | Mężczyzna | StreamElements |

---

## 🔗 Parametry URL (Dla zaawansowanych)

Jeśli wolisz edytować link ręcznie, oto dostępne parametry:

### Przykład linku
```
tts.html?channel=twoj_nick&voice=Ola&volume=90&moderator=on&vip=on&og=on&pretext=on
```

### Dostępne parametry

**Wymagane:**
- `channel` - Twoja nazwa kanału Kick.com

**Opcjonalne:**
- `voice` - Nazwa głosu z tabeli powyżej (domyślnie: `Zosia`)
- `speed` - Prędkość: `-3` do `3` (domyślnie: `0`). *Uwaga: działa tylko dla głosów Oddcast i Microsoft.*
- `volume` - Głośność: `0` do `100` (domyślnie: `80`)
- `readnick` - Czytaj nick przed wiadomością: `on`/`off` (domyślnie: `off`)
- `readlinks` - Zamieniaj linki na słowo "LINK": `on`/`off` (domyślnie: `off` - linki są ignorowane)
- `reademotes` - Czytaj nazwy emotek: `on`/`off` (domyślnie: `off` - emotki są ignorowane)
- `pretext` - Wymagaj `!tts` przed wiadomością: `on`/`off` (domyślnie: `on`)

**Uprawnienia (domyślnie włączony Moderator, VIP i OG):**
- `anyone=on` - Każdy
- `follower=on` - Obserwujący
- `moderator=on` - Moderatorzy
- `og=on` - OG
- `subscriber=on` - Subskrybenci
- `vip=on` - VIP

---

## 🎮 Komendy

**Tylko dla Broadcastera (właściciela kanału):**
- `!skiptts` - Natychmiastowo ucina i pomija aktualnie odtwarzaną wiadomość TTS (przydatne przy trollach).

---

## 📄 Licencja

MIT License - Projekt całkowicie darmowy i open-source.

---

**Zrobione z ❤️ dla polskiej społeczności Kick.com**
