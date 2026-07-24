# Vault

**Leitor de PDF e banda desenhada** — biblioteca local, conta na cloud, sync, TTS offline e leitura sem ruído.

<p align="center">
  <img src="assets/app_icon.png" alt="Vault" width="120" />
</p>

<p align="center">
  <code>hq_reader</code> · v<strong>2.0.1</strong> (+24) · Flutter / Dart&nbsp;3.11
</p>

---

## Visão geral

Vault é um cliente Flutter para ler **PDFs** e **comics** (CBZ / CBR) no dispositivo. Os ficheiros ficam contigo; a cloud guarda progresso, anotações e preferências — nunca os binários.

| Capacidade | Detalhe |
|---|---|
| Formatos | PDF, CBZ/ZIP, CBR/RAR |
| Leitura | Grifos, notas, marcadores, busca, sumário (PDF) |
| Ouvir | TTS offline Piper (Sherpa ONNX) · vozes PT-BR incluídas |
| Conta | Login, sync LWW, refresh JWT, estatísticas |
| Extra | Tradução / dicionário, Discover, social opt-in, multi-idioma |

> **Produto:** sem download de conteúdo pirata no cliente. Discover e social mostram só metadados / rankings.

Backend NestJS: repositório separado **`valt-back`**.

---

## Plataformas

| | Pasta | Binário |
|---|---|---|
| **Windows (PC)** | [`windows/`](windows/) | `hq_reader.exe` |
| **Linux** | [`linux/`](linux/) | `hq_reader` |
| Android · iOS · Web · macOS | presentes no repo | Flutter standard |

Este README foca **Windows** e **Linux**.

---

## Requisitos comuns

- [Flutter](https://docs.flutter.dev/get-started/install) **stable** (testado: **3.41.x** / Dart **3.11.x**)
- SDK Dart `^3.11.1` (ver `pubspec.yaml`)
- Git

```bash
flutter pub get
```

Opcional — apontar para API local:

```bash
flutter run --dart-define=VAULT_BACKEND_URL=http://127.0.0.1:8080
```

---

## Windows (PC)

### Dependências de sistema

- Windows **10 / 11** (x64)
- [Visual Studio 2022](https://visualstudio.microsoft.com/) com workload **Desktop development with C++**
- CMake (incluído no VS)
- Desktop Windows activado no Flutter

```bash
flutter config --enable-windows-desktop
flutter doctor
```

### Correr e build

```bash
# debug
flutter run -d windows

# release
flutter build windows --release
```

Saída típica:

```text
build\windows\x64\runner\Release\
```

Áudio desktop: `media_kit_libs_windows_audio`.

---

## Linux

### Dependências de sistema

Debian / Ubuntu (exemplo):

```bash
sudo apt update
sudo apt install -y \
  clang cmake ninja-build pkg-config \
  libgtk-3-dev \
  liblzma-dev \
  libstdc++-12-dev \
  libmpv-dev mpv \
  libasound2-dev
```

O runner usa **GTK 3** (`linux/CMakeLists.txt` → `gtk+-3.0`).

```bash
flutter config --enable-linux-desktop
flutter doctor
```

### Correr e build

```bash
# debug
flutter run -d linux

# release
flutter build linux --release
```

Bundle típico:

```text
build/linux/x64/release/bundle/
```

Áudio desktop: `media_kit_libs_linux`.

---

## Dependências Dart

Principais pacotes em [`pubspec.yaml`](pubspec.yaml):

| Pacote | Função |
|---|---|
| `pdfrx` | Leitor PDF |
| `archive` · `rar` | CBZ/ZIP e CBR/RAR |
| `file_picker` · `path_provider` · `path` | Ficheiros e paths |
| `sherpa_onnx` | TTS Piper offline |
| `just_audio` · `audio_service` · `audio_session` | Playback |
| `just_audio_media_kit` + libs Windows/Linux | Áudio no desktop |
| `dio` | HTTP |
| `flutter_secure_storage` | Tokens |
| `shared_preferences` | Preferências |
| `sentry_flutter` | Crash reporting (opcional) |
| `share_plus` · `url_launcher` · `package_info_plus` | Share / links / versão |
| `wakelock_plus` | Ecrã ligado na leitura |
| `google_fonts` · `showcaseview` | UI / tutoriais |
| `flutter_localizations` · `intl` | i18n |

Assets TTS: [`assets/tts/`](assets/tts/) (espeak-ng-data + vozes PT-BR Cadu / Faber / Dii).

---

## Configuração

| Variável (`--dart-define`) | Uso |
|---|---|
| `VAULT_BACKEND_URL` | Raiz da API (sem `/v1`) |
| `SENTRY_DSN` | Crash reporting (opcional) |
| `VAULT_CREATOR_USER_ID` | ID do perfil criador (opcional) |

Exemplos:

```bash
flutter run -d windows --dart-define=VAULT_BACKEND_URL=http://127.0.0.1:8080
flutter run -d linux   --dart-define=SENTRY_DSN=https://...
```

Sem override, a URL default está em [`lib/config/vault_backend_config.dart`](lib/config/vault_backend_config.dart).

---

## Estrutura do projecto

```text
lib/
  screens/      # UI — biblioteca, leitores, conta, social, discover…
  services/     # import, sync, TTS, APIs, stores
  models/       # modelos de dados
  widgets/      # componentes
  l10n/         # traduções
  config/       # backend / defines
windows/        # runner desktop Windows
linux/          # runner desktop Linux
assets/         # ícone, atmosfera, TTS
```

---

## Privacidade e segurança

- Tokens em **secure storage**; sync **sem** ficheiros binários
- Social e Discover são **opt-in**
- Sentry sem senhas / tokens em cleartext
- **Não** commits secrets (`SENTRY_DSN`, API keys) no git

---

## Notas

- Versão da app: campo `version` em [`pubspec.yaml`](pubspec.yaml)
- Roadmap interno (se existir no clone): [`PLANOS.md`](PLANOS.md)
- Builds de release: correr **localmente** (`flutter build windows` / `flutter build linux`)

---

<p align="center">
  <sub>Vault · leitura no teu ritmo</sub>
</p>
