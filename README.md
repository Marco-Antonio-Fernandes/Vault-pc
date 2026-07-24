<p align="center">
  <img src="assets/app_icon.png" alt="Vault" width="140" />
</p>

<h1 align="center">Vault</h1>

<p align="center">
  <strong>O teu espaço para ler PDFs e banda desenhada</strong><br/>
  No PC ou no Linux — com a biblioteca no teu dispositivo e a progresso a acompanhar-te.
</p>

<p align="center">
  <img alt="versão" src="https://img.shields.io/badge/versão-2.0.1-6B4F3A?style=for-the-badge" />
  <img alt="Windows" src="https://img.shields.io/badge/Windows-PC-0078D4?style=for-the-badge&logo=windows&logoColor=white" />
  <img alt="Linux" src="https://img.shields.io/badge/Linux-Desktop-FCC624?style=for-the-badge&logo=linux&logoColor=black" />
  <img alt="Flutter" src="https://img.shields.io/badge/feito_com-Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white" />
</p>

---

## O que é o Vault?

Imagina uma **estante digital só tua**: importas os teus ficheiros, organizas a biblioteca, retomas a leitura onde paraste e — se quiseres — ouves o texto em voz alta.

Os livros e comics **ficam no teu computador**. A conta online serve para sincronizar progresso, anotações e preferências entre dispositivos — **sem enviar os ficheiros** para a cloud.

<br/>

<table>
  <tr>
    <td width="50%" valign="top">

### Ler com conforto
- PDFs e comics (CBZ, CBR)
- Marcadores, notas e grifos
- Busca no texto e sumário
- Temas e modo mãos-livres

    </td>
    <td width="50%" valign="top">

### Ouvir e acompanhar
- Vozes em português (incluídas)
- Timer de sono para pausar sozinho
- Estatísticas da tua leitura
- Tradução rápida de palavras

    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">

### A tua biblioteca
- Capas e pastas / estantes
- Progresso guardado
- Sync opcional com conta
- Funciona também offline

    </td>
    <td width="50%" valign="top">

### Comunidade (se quiseres)
- Perfil e estante pública *opt-in*
- Discover com tendências
- Só metadados — sem downloads
- Controlo total da privacidade

    </td>
  </tr>
</table>

> **Nota:** o Vault **não** descarrega conteúdo de sites de pirataria. Tu trazes os teus próprios ficheiros.

---

## Para quem é?

| Queres… | Vault ajuda assim |
|---|---|
| Ler HQs e PDFs no PC | Abre, importa, lê em ecrã inteiro |
| Continuar noutro dispositivo | Conta + sync de progresso e notas |
| Ouvir enquanto fazes outra coisa | Modo voz com timer de sono |
| Ver quanto lês | Ecrã “A minha leitura” com metas e streak |
| Manter tudo privado | Social desligado por defeito |

---

## Versões de secretária

<p align="center">

| | **Windows** | **Linux** |
|:---:|:---:|:---:|
| **Para** | PC com Windows 10 ou 11 | Desktop Linux (Ubuntu e afins) |
| **App** | `hq_reader.exe` | `hq_reader` |
| **Ideal para** | Uso diário no portátil / secretária | Quem prefere ambiente Linux |

</p>

Também existem builds para telemóvel e web no mesmo projecto — mas o foco deste guia é **PC Windows** e **Linux**.

---

## Como começar (passo a passo)

### 1. Preparar o ambiente

Precisas do [Flutter](https://docs.flutter.dev/get-started/install) instalado (versão estável recente).

No terminal, dentro da pasta do projecto:

```bash
flutter pub get
```

Isto descarrega tudo o que a app precisa para correr.

---

### 2. No Windows

**O que instalar uma vez:**

1. Visual Studio 2022 com a opção **Desenvolvimento para ambiente de trabalho com C++**
2. Activar o suporte Windows no Flutter:

```bash
flutter config --enable-windows-desktop
flutter doctor
```

O `flutter doctor` deve ficar sem erros vermelhos nos pontos de Windows.

**Abrir a app:**

```bash
flutter run -d windows
```

**Gerar versão final (instalável / pasta Release):**

```bash
flutter build windows --release
```

A pasta pronta fica em `build\windows\x64\runner\Release\`.

---

### 3. No Linux

**O que instalar uma vez** (exemplo Ubuntu / Debian):

```bash
sudo apt update
sudo apt install -y \
  clang cmake ninja-build pkg-config \
  libgtk-3-dev liblzma-dev \
  libmpv-dev mpv libasound2-dev
```

Depois:

```bash
flutter config --enable-linux-desktop
flutter doctor
```

**Abrir a app:**

```bash
flutter run -d linux
```

**Gerar versão final:**

```bash
flutter build linux --release
```

A pasta pronta fica em `build/linux/x64/release/bundle/`.

---

## O que a app usa por baixo (em linguagem simples)

Não precisas de memorizar isto para usar — só se fores desenvolver ou empacotar.

| Área | Em poucas palavras |
|---|---|
| Interface | Flutter — uma base, várias plataformas |
| Abrir PDFs | Motor de leitura PDF integrado |
| Comics | Suporte a pastas ZIP (CBZ) e RAR (CBR) |
| Voz | TTS offline (não depende da internet para falar) |
| Conta e sync | Liga a um servidor Vault (backend à parte) |
| Preferências | Guardadas no dispositivo de forma segura |

Vozes em português já vêm empacotadas; podes gerir / acrescentar vozes dentro da app.

---

## Ligar a um servidor (opcional)

Por defeito a app aponta para o servidor configurado no projecto.

Se estiveres a desenvolver com API local:

```bash
flutter run -d windows --dart-define=VAULT_BACKEND_URL=http://127.0.0.1:8080
```

(O mesmo funciona com `-d linux`.)

---

## Privacidade, em resumo

```text
  Ficheiros  ──►  ficam no teu PC / Linux
  Progresso  ──►  pode sincronizar (com login)
  Anotações  ──►  podem sincronizar
  Estante pública  ──►  só se activares
```

Não commits palavras-passe, tokens ou chaves de serviços no Git.

---

<p align="center">
  <br/>
  <strong>Vault</strong><br/>
  <em>Lê no teu ritmo. A estante é tua.</em>
  <br/><br/>
  <sub>Versão 2.0.1 · nome interno <code>hq_reader</code></sub>
</p>
