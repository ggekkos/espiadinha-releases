# 👀 Espiadinha

*[Versão em português](README.md)*

P2P screen sharing for a small group of friends, with voice and chat.
Windows and Linux (both versions talk to each other). Interface in English and Portuguese (⚙️ → **Language**).
**Free.** This repository only holds the downloads: the source code is private.

**⬇️ [Download the latest version](https://github.com/ggekkos/espiadinha-releases/releases/latest)**: `Espiadinha_<version>_x64-setup.exe` (Windows),
`.AppImage` or `.tar.gz` (Linux). Check the file with `SHA256SUMS.txt` (see below).

> ⚠️ Before using it, read [Security and privacy](#security-and-privacy): the app is made for friends who know each
> other, relies on a third-party public server for people to find each other, and everyone in the same room can see
> the others' IP addresses.

## How to use
1. Download the latest version from the [Releases](https://github.com/ggekkos/espiadinha-releases/releases/latest) page:
   `Espiadinha_<version>_x64-setup.exe` on Windows, `Espiadinha-<version>-x86_64.AppImage` or the `.tar.gz` on Linux.
2. One person clicks **Create room** and sends the 6-character code (the ✉️ button copies a ready-made invite).
   Recommended: fill in a **room password** before creating it. Without the right password, the request to join
   never even arrives.
3. The others type the code (and the password, if any) and click **Join room**. The room creator accepts each person
   on the side panel. Pasting the whole invite into the code field fills in the code and the password.
4. Anyone can click **Share screen** (if someone is already sharing, it becomes "Take over the screen").

In the room:
- 🎤 turns the microphone on/off (global shortcut **Ctrl+Shift+F9**). Hover someone's name to change their voice volume.
- **Ctrl+Shift+F10** starts/stops sharing without leaving your game.
- 📍 (or **Ctrl+click** on the video) points at something on the sharer's screen. ✏️ draws over the video (fades by itself).
- "Quality for me" lowers only what **you** receive, if your internet is bad.
- 🗗 makes the window small and always on top. 📊 shows connection diagnostics. ⚙️ opens settings.
- 😀 sends a reaction. 📎 (or **Ctrl+V**, or drag and drop) sends images and files
  (up to 1 GB) in the chat. Files go straight from the sender to whoever clicks "Download" (not through the host)
  and stay available while the sender is in the room.
- 🎬 (or **Ctrl+Shift+F11**): the first press starts keeping the screen, the next ones save the last 30 s as MP4 in
  your Downloads folder.
- ⚙️ → **Appearance**: classic and animated themes, accent color, your color and an avatar. You can create your own
  themes (background image, a character in a corner, colors, effects) and send them in the chat or as a
  `.espiadinha-tema` file.
- 🐾 **Pet:** the paw button on the home screen opens a 16×16 pixel-art editor (up to 10 animations of 8 frames, with
  selection, rotate and flip). The pet strolls around the home screen and, in the room, shows up in a corner while
  nobody is sharing. Click it to pet it, feed it, play ball and do tricks; drag it and let go while moving to throw it
  (each pet's "physics" sets how much it flies and bounces). The ball stays until you double-click it.

## Windows
The installer isn't digitally signed, so Windows shows the SmartScreen warning ("Windows protected your PC"). Check
the file against `SHA256SUMS.txt`, then click **More info → Run anyway**.

## Linux
AppImage: `chmod +x Espiadinha-*.AppImage && ./Espiadinha-*.AppImage`.

Or the `.tar.gz`:
```
tar xzf Espiadinha-<version>-linux-x64.tar.gz
cd Espiadinha
./instalar.sh        # installs into ~/.local/share/espiadinha and adds a menu shortcut
```
Or run it directly without installing: `./espiadinha.sh`.

- **PC audio:** uses `pactl` (package `pulseaudio-utils`; also works with PipeWire).
- **GPU:** video uses VA-API when the driver supports it. If it causes trouble, turn it off in ⚙️ or start with `--sem-gpu`.
- **Sandbox:** if the system blocks the Chromium sandbox, `instalar.sh` asks whether it may create an AppArmor
  profile (Ubuntu) or set up `chrome-sandbox` (Debian). It's optional; without it the app starts with `--no-sandbox`.

## Security and privacy
Espiadinha is made for a small group of people who know each other. Understand what it does before using it:

**How people find each other.** The app has no server of its own. For two PCs to find each other it uses the free
public [PeerJS](https://peerjs.com) server (`0.peerjs.com`), run by third parties with no uptime guarantee. That
server sees the room code, the name and version of whoever asks to join, IP addresses and times. It does **not** see
the chat, voice or screen: those go straight between the PCs, encrypted by WebRTC itself. You can use your own
signaling server in Advanced.

**What is protected:**
- The room creator only reveals their own IP to people they **accept**. Someone knocking who isn't accepted (or is
  declined) receives nothing. That's why "Decline" doesn't notify the person: they keep waiting and give up on their own.
- With a **room password**, people who don't know it don't even show up in the request list. The password isn't sent
  in plain text: a hash of it is sent together with the code. Use a password that isn't obvious, and send the invite
  only to people who will join.
- The host rate-limits each person (chat, ping, drawing, images, files, themes, screen takeover) and only relays between
  members what the app actually uses.
- Everything that comes from other people (names, chat, images, themes) is treated as text or image, never as code.
  Names with invisible characters are cleaned, so nobody can imitate someone else's name.
- Chat images only in WebP, JPEG, PNG or GIF (no SVG); themes go through full validation.
- Files: only people in the room can download them, names arrive cleaned (no tricks to hide an `.exe`) and programs
  or scripts ask for confirmation before downloading. Still, only open files from people you trust.
- When the room changes host, whoever comes back must prove they're the same person.

**Remaining risks:**
- **Everyone in the room sees the others' IP addresses** (screen and voice go straight between the PCs). Only accept
  people you know. To hide your IP even from friends, use a VPN.
- The host can see and relay the whole chat. People in the room can record the screen you share (the app itself has
  clips): only share what you would show to those people.
- Without "Ask for my approval" and without a password, anyone with the code gets in.
- The installers are **not digitally signed** (Windows shows the SmartScreen warning). Only download from the
  official [Releases](https://github.com/ggekkos/espiadinha-releases/releases/latest) page. Other copies may have been altered.
  To check, every release has a `SHA256SUMS.txt`: on Windows, run `Get-FileHash .\Espiadinha_<version>_x64-setup.exe`
  in PowerShell and compare it with the file's line; on Linux, `sha256sum -c SHA256SUMS.txt --ignore-missing` in the
  download folder.
- On Linux, some systems (Ubuntu 23.10+, some Debian) block the Chromium sandbox, and the app starts with
  `--no-sandbox` (one less layer of protection). The `.tar.gz`'s `instalar.sh` offers to turn the sandbox back on
  (needs sudo), and the app warns you in ⚙️ when it's running without it. The AppImage can't (its folder changes every
  time it starts): on those systems, prefer the `.tar.gz`.
- The app is only as safe as the browser inside it: keep Espiadinha up to date (on Linux it ships its own Chromium,
  which only updates together with the app).
- The app is provided "as is", without warranty (see the [license](LICENSE)).

Found a security problem? See [SECURITY.md](SECURITY.md).

## If it doesn't connect
Some ISPs use CGNAT and block direct connections. Then you need a TURN server (e.g. coturn on a VPS), set in
**Advanced** on the home screen. If the public PeerJS server is down, run one with `npx peer --port 9000` and set
the same address on every PC.

## Problems, suggestions and security
- Bug or suggestion: open an [issue](https://github.com/ggekkos/espiadinha-releases/issues).
- Security problem: **don't** open a public issue; see [SECURITY.md](SECURITY.md).

## License
Free to download, use and pass on unmodified; provided "as is", without warranty. See [LICENSE](LICENSE).
