# 🎙️ Polish Kick TTS

**Darmowy system Text-to-Speech dla polskich streamerów Kick.com**

---

## 🚀 Użyj TTS

**Link do TTS:** [https://89891383.github.io/Polish-Kick-TTS/tts.html](https://89891383.github.io/Polish-Kick-TTS/tts.html)

---

## 📖 Jak używać

### 1. Wygeneruj link
- Otwórz [link do TTS](https://89891383.github.io/Polish-Kick-TTS/tts.html)
- Wpisz nazwę swojego kanału Kick
- Dostosuj ustawienia
- Skopiuj wygenerowany link

### 2. Dodaj do OBS
- Dodaj **Browser Source** w OBS/Streamlabs
- Wklej skopiowany link
- Ustaw wymiary: **800x600**
- Gotowe! 🎉

### 3. Użycie na czacie
Widzowie piszą wiadomości zaczynające się od `tts`:
```
tts Witam na streamie!
```

---

## ⚙️ Funkcje

- ✅ **5 polskich głosów** (męskie i żeńskie)
- ✅ **Regulacja prędkości** (-3 do +3)
- ✅ **Kontrola głośności** (0-100)
- ✅ **System uprawnień** (Moderator, VIP, OG, Subscriber, Follower)
- ✅ **Filtrowanie linków i emotek**
- ✅ **Komenda !skiptts** dla streamera

---

## 🎤 Dostępne głosy

| Głos | Płeć |
|------|------|
| Zosia | Kobieta (domyślny) |
| Agatka | Kobieta |
| Danota | Kobieta |
| Krzysztof | Mężczyzna |
| Wojciech | Mężczyzna |

---

## 🔗 Parametry URL

### Przykład linku
```
tts.html?channel=twoj_nick&voice=Krzysztof&volume=90&moderator=on&vip=on&og=on&pretext=on
```

### Dostępne parametry

**Wymagane:**
- `channel` - Nazwa kanału Kick.com

**Opcjonalne:**
- `voice` - Głos: `Zosia`, `Agatka`, `Danota`, `Krzysztof`, `Wojciech` (domyślnie: `Zosia`)
- `speed` - Prędkość: `-3` do `3` (domyślnie: `0`)
- `volume` - Głośność: `0` do `100` (domyślnie: `80`)
- `readnick` - Czytaj nick: `on`/`off` (domyślnie: `off`)
- `readlinks` - Czytaj linki: `on`/`off` (domyślnie: `off`)
- `reademotes` - Czytaj emotki: `on`/`off` (domyślnie: `off`)
- `pretext` - Wymagaj "tts": `on`/`off` (domyślnie: `on`)

**Uprawnienia:**
- `anyone=on` - Każdy
- `follower=on` - Obserwujący
- `moderator=on` - Moderatorzy (domyślnie: `on`)
- `og=on` - OG (domyślnie: `on`)
- `subscriber=on` - Subskrybenci
- `vip=on` - VIP (domyślnie: `on`)

---

## 🎮 Komendy

**Dla streamera:**
- `!skiptts` - Pomija aktualnie odtwarzane TTS

---

## 📄 Licencja

MIT License - Projekt darmowy i open-source

---


<div align="center">

**Zrobione z ❤️ dla polskiej społeczności Kick.com**

</div>
