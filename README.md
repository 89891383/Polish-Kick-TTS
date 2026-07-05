<div align="center">

<img src="https://kick.com/img/kick-logo.svg" width="72" alt="Kick" />

<br><br>

# 🎙️ Polish Kick TTS

**Najlepszy darmowy Text-to-Speech dla polskich streamerów Kick.com**

<br>

[![Generator TTS](https://img.shields.io/badge/▶_GENERATOR_TTS-53FC18?style=for-the-badge&labelColor=18181b)](https://89891383.github.io/Polish-Kick-TTS/tts.html)
[![47 Głosów](https://img.shields.io/badge/47_GŁOSÓW-53FC18?style=flat-square&labelColor=18181b)](https://89891383.github.io/Polish-Kick-TTS/tts.html)
[![Darmowy](https://img.shields.io/badge/0_zł-DARMOWY-53FC18?style=flat-square&labelColor=18181b)](https://89891383.github.io/Polish-Kick-TTS/tts.html)
[![OBS Ready](https://img.shields.io/badge/OBS-READY-53FC18?style=flat-square&labelColor=18181b)](https://89891383.github.io/Polish-Kick-TTS/tts.html)

<br>

### 👉 [https://89891383.github.io/Polish-Kick-TTS/tts.html](https://89891383.github.io/Polish-Kick-TTS/tts.html)

```
https://89891383.github.io/Polish-Kick-TTS/tts.html
```

<sub>Wklej link Kick lub nick → skopiuj URL → dodaj jako Browser Source w OBS</sub>

</div>

---

<br>

## 📖 Instrukcja

<table>
<tr>
<td width="60" align="center"><h2>1</h2></td>
<td>

### Wygeneruj link

Otwórz **[generator TTS](https://89891383.github.io/Polish-Kick-TTS/tts.html)** → wpisz nick lub wklej `https://kick.com/twoj_nick` → ustaw głos, filtry i uprawnienia → **Kopiuj link** (aktualizuje się na żywo)

</td>
</tr>
<tr>
<td align="center"><h2>2</h2></td>
<td>

### Dodaj do OBS

**Sources → Browser Source** → wklej link → rozmiar **800×600** → ✅ *Refresh browser when scene becomes active*

</td>
</tr>
<tr>
<td align="center"><h2>3</h2></td>
<td>

### Gotowe

Widzowie piszą na czacie:

```
!tts Witam na streamie!
```

Broadcaster: `!skiptts` — przerywa aktualne TTS i przechodzi do następnej wiadomości w kolejce

</td>
</tr>
</table>

<br>

---

## ⚙️ Funkcje

<div align="center">

| 🎤 Głosy | ⚡ Live URL | 🔗 Kick parser | 🔊 Auto OBS | 📋 FIFO | 🤖 Anti-bot |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 47 PL | ✅ | ✅ | ✅ | ✅ | ✅ |

</div>

<br>

| Funkcja | Opis |
|---------|------|
| **47 polskich głosów** | Oddcast · Microsoft · StreamElements · Google Cloud |
| **Google Chirp3 HD** | 30 głosów HD + Wavenet + Standard |
| **Live URL** | Link generuje się automatycznie przy każdej zmianie |
| **Parsowanie Kick** | Wklej `kick.com/nick` — dostaniesz gotowy URL |
| **Auto-start w OBS** | Działa od razu, bez klikania w przeglądarce |
| **Prędkość mowy** | `-3` szybciej → `+3` wolniej *(Oddcast, Microsoft)* |
| **Ton głosu** | `-10` do `+10` *(Oddcast, MS, SE)* · `0.01`–`0.99` *(Google, domyślnie 0.50)* |
| **Anti-spam** | Filtry znaków specjalnych, liczb i powtórzeń liter |
| **CAPS → małe litery** | Wiadomości CAPSLOCK czytane jako małe litery (automatycznie) |
| **Uprawnienia** | Każdy · Follower · Mod · VIP · OG · Sub |
| **!skiptts** | Broadcaster przerywa aktualne TTS — kolejka działa dalej |
| **Filtr botów** | Botrix, Kickbot i inne boty ignorowane |

<br>

---

## 🎤 Silniki i głosy

| Silnik | Głosy | Speed | Pitch |
|--------|:-----:|:-----:|:-----:|
| **Oddcast** | Zosia, Agatka, Danota, Krzysztof, Wojciech | ✅ | Web Audio |
| **Microsoft** | Adam, Paulina | ✅ | Natywny |
| **StreamElements** | Wavenet-A/B, Jacek, Maja, Ewa, Jan | ❌ | Web Audio |
| **Google Cloud** | Chirp3 HD (30), Wavenet-F/G, Standard-F/G | ❌ | Natywny `0.01`–`0.99` |

<br>

<div align="center">

| | **Kobiety** | | **Mężczyźni** | |
|:---:|:---|:---:|:---|:---:|
| ⭐ | Zosia · Agatka · Danota | | Krzysztof · Wojciech | |
| | SE-WavenetA · SE-Maja · SE-Ewa | | Adam · SE-WavenetB · SE-Jacek · SE-Jan | |
| | Sulafat · Zephyr · Leda · Wavenet-F | | Schedar · Charon · Umbriel · Wavenet-G | |

</div>

<sub>Pełna lista 34 głosów Google Cloud (Chirp3 HD + Wavenet + Standard) w generatorze.</sub>

<br>

---

<details>
<summary><h3>🔗 Parametry URL — kliknij aby rozwinąć</h3></summary>

<br>

**Przykład (Oddcast):**

```
https://89891383.github.io/Polish-Kick-TTS/tts.html?channel=adamcy&voice=Zosia&volume=90&moderator=on&vip=on&og=on&pretext=on
```

**Przykład (Google Cloud):**

```
https://89891383.github.io/Polish-Kick-TTS/tts.html?channel=adamcy&voice=pl-PL-Chirp3-HD-Sulafat&pitch=0.35&stripspecial=on&ignorenumbers=on
```

<br>

| Parametr | Domyślnie | Opis |
|----------|:---------:|------|
| `channel` | — | **Wymagane** — nazwa kanału Kick |
| `voice` | `Zosia` | Głos z listy (np. `pl-PL-Chirp3-HD-Schedar`) |
| `speed` | `0` | `-3` do `+3` *(tylko Oddcast, Microsoft)* |
| `pitch` | `0` / `0.50` | Oddcast/MS/SE: `-10` do `+10` · Google: `0.01`–`0.99` |
| `volume` | `80` | Głośność `0`–`100` |
| `readnick` | `off` | Czytaj nick przed wiadomością |
| `readlinks` | `off` | Linki jako słowo „LINK" |
| `reademotes` | `off` | Czytaj nazwy emotek |
| `pretext` | `on` | Wymagaj `!tts` na początku |
| `stripspecial` | `on` | Usuń znaki specjalne (*, ^, ~, # itd.) |
| `ignorenumbers` | `off` | Ignoruj liczby w wiadomości |
| `ignorerepeat` | `off` | Skróć powtórzone litery (heeeeey → hey) |

<br>

**Uprawnienia** — domyślnie włączone: `moderator` · `vip` · `og`

`anyone=on` · `follower=on` · `moderator=on` · `og=on` · `subscriber=on` · `vip=on`

</details>

<br>

---

<div align="center">

<img src="https://kick.com/img/kick-logo.svg" width="36" alt="Kick" />

<br><br>

**Zrobione z ❤️ dla polskiej społeczności Kick.com**

<br>

<sub>MIT License · Darmowy · Open Source</sub>

<br><br>

[![Generator TTS](https://img.shields.io/badge/▶_OTWÓRZ_GENERATOR-53FC18?style=for-the-badge&labelColor=0e0e10)](https://89891383.github.io/Polish-Kick-TTS/tts.html)

</div>
