<p align="center"><img src="assets/banner.png" alt="传声筒 MicHop" width="760"></p>
<p align="center"><a href="README.md">简体中文</a> · <a href="README.zh-Hant.md">繁體中文</a> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.es.md">Español</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pt.md">Português</a> · <a href="README.ru.md">Русский</a></p>

<p align="center">
  <b>Lend this Mac's microphone to another Mac.</b><br>
  Send it as live audio or as text, over your LAN or Tailscale.
</p>

---

## What it's for

I usually work on a MacBook and use remote desktop software (UU Remote, Sunlogin, ToDesk, etc.) to connect to a Mac mini and get things done there, like having Claude Code write code, editing videos, or maintaining websites.

The problem: **the Mac mini has no microphone, and the remote desktop software doesn't forward the MacBook's microphone**, so you can't use voice input inside the remote desktop.

MicHop solves exactly that. Install one app on each computer:

- **The computer you talk into** (e.g. the MacBook): install "MicHop"
- **The computer doing the work** (e.g. the Mac mini): install "MicHop Receiver"

### Two ways to send, switchable anytime from the main window

```
MacBook (talking)                            Mac mini (working)

Microphone ── 🔊 Send Audio ──────────►  Virtual microphone (built-in MicHop Audio)
                                      → System Dictation / WeChat Input Method / Claude Code voice mode

Dictation  ── 📝 Send Text ───────────►  Pasted at the cursor, with optional auto-Return

              over LAN or Tailscale
```

**🔊 Send Audio: the Mac mini "hears" you directly**

The sound from the MacBook's microphone is streamed to the Mac mini in real time and becomes the Mac mini's microphone. Any app on the Mac mini that needs a microphone can use it, such as System Dictation, voice input in WeChat Input Method, or Claude Code's voice mode.

- The Receiver comes with its own virtual audio device, **MicHop Audio**. You're prompted to install it the first time audio is sent (it asks for an administrator password once); nothing else to download. If you already have [BlackHole](https://github.com/ExistentialAudio/BlackHole) installed, you can keep using it.
- Built-in echo cancellation, so there's no echo even while connected through remote desktop software.
- The Fn key doesn't get through remote desktop software, so remember to change your voice input shortcut to a modifier-key combo such as Ctrl + Option. [See below](#tip-the-fn-key-doesnt-pass-through-remote-connections-so-change-the-shortcut).

**📝 Send Text: recognize on the MacBook, send the words over**

On the MacBook, press ⌃⌥Space (Ctrl + Option + Space) and use System Dictation to turn your speech into text. The text is sent to the Mac mini and automatically pasted at the cursor, optionally followed by Return so it's submitted straight to Claude.

- No audio driver or audio setup needed on the Mac mini — the simplest and most reliable option.
- This is the app's default mode.

| | 🔊 Send Audio | 📝 Send Text |
|---|---|---|
| Where speech is recognized | Mac mini (its own dictation or input method) | MacBook (System Dictation) |
| What the Mac mini needs | Receiver + its built-in virtual audio device (installed on first use) | Just the Receiver |
| Best for | Using the Mac mini's input method, dictation, or Claude voice mode | Simply turning what you say into typed text |

### How the two computers connect

- **On the same LAN**: just enter the Mac mini's LAN IP.
- **Not in the same place**: install [Tailscale](https://tailscale.com) on both computers to form a virtual LAN, then enter the Mac mini's **Tailscale IP** (starts with 100). **Both audio and text can go over Tailscale**, so it works the same at home or on the road.
- The Receiver's window lists the LAN IP, Tailscale IP, and passcode, each with its own copy button.

### Other highlights

- **No cloud services involved**: audio and text travel directly between your own two computers, over the LAN or through Tailscale's encrypted tunnel.
- **Independent of your remote desktop software**: works alongside UU Remote, Sunlogin, ToDesk, and Screen Sharing.
- **Automatic updates**: upgrades itself when a new version is available, without needing to re-grant permissions.
- **Multilingual**: the interface supports 简体中文, 繁體中文, English, 日本語, 한국어, Español, Français, Deutsch, Português, and Русский. Chinese is the default; switch languages under "Settings… → General → Language".

## Download and install

Download from [Releases](../../releases/latest):

| File | Which computer | Menu bar icon |
|---|---|---|
| `MicHop.zip` (MicHop) | The computer you talk into, e.g. MacBook | A rounded square, same as the app icon |
| `MicHop-Receiver.zip` (MicHop Receiver) | The computer doing the work, e.g. Mac mini | Same as above |

The menu bar icon's color shows the status: **grey** = not connected, **green** = connected, **red** = sending (speaking / receiving audio).

> **Both apps are built around a main window**: click the Dock icon to open it. The top of the window shows the status in two tiles, "Connection" (grey / blue) and "Audio" (grey / red), and the everyday controls are all right there in the window; language, automatic updates, and similar options live in "Settings…" (⌘,). The menu bar icon and the Dock icon's right-click menu keep only the most-used items. When the MacBook camera notch hides the menu bar icon, just use the Dock icon.

Requires macOS 13 or later; works on both Apple silicon and Intel Macs.

> **"Developer cannot be verified" on first launch**: this is because the app hasn't gone through Apple's paid notarization. Open System Settings → Privacy & Security, and click "Open Anyway" near the bottom of the page. Alternatively, run this command in Terminal to remove the quarantine flag, then open the app:
> ```bash
> xattr -dr com.apple.quarantine "/Applications/MicHop Receiver.app"
> ```

### 1. The working computer (Receiver)

1. Unzip `MicHop-Receiver.zip`, drag "MicHop Receiver" into "Applications", and open it.
2. Follow the prompt to grant **Accessibility** permission: System Settings → Privacy & Security → Accessibility → turn on "MicHop Receiver". It needs this permission to press ⌘V for you.
   - If asked "Do you want the application to accept incoming network connections?", click **Allow**.
3. Click the "MicHop Receiver" icon in the Dock. The main window shows:
   - **Connection Info**: this Mac's LAN address, Tailscale address, and passcode, each with its own copy button.
   - **Setup**: the "Accessibility Permission" row should show a green checkmark. Any item with a yellow warning has a fix button right next to it.
4. "Launch at Login" is on by default; you can turn it off under "Settings… → General" if you don't need it.

### 2. The talking computer (Sender)

1. Unzip `MicHop.zip`, drag "MicHop" into "Applications", and open it.
2. The first time you open it, a settings window appears: enter the Receiver's **address** and **passcode**, click "Test Connection", and once you see the green "Connected — ready to go", click "Save".
   - In the Receiver's window, the copy buttons next to the address and passcode let you copy each one separately.
   - You can also click "Copy All" on the Receiver and paste the whole thing into the "Receiver Address" field. The Sender picks out the address automatically (preferring the Tailscale address if there is one) and fills in the passcode too.
   - If asked to "allow finding devices on your local network", click **Allow**.
3. Make sure System Dictation is turned on: System Settings → Keyboard → Dictation.
4. Once the top of the main window shows "Connected to receiver", you're ready to go. To change the address or passcode later, click "Change…" in the "Receiver" section of the main window, or press ⌘,.

## How to use

1. In the remote desktop, first click into a text field on the working computer, such as Claude Code.
2. Press **⌃⌥Space (Ctrl + Option + Space)**. A small window pops up at the bottom of the screen and dictation starts automatically. If dictation doesn't start on its own, press Fn once.
3. Speak, then press **Return** when you're done. The text appears on the other computer.

| Key | Action |
|---|---|
| Return / ⌃⌥Space again | Send |
| Shift + Return | New line |
| Esc | Cancel |

The top of the small window shows which computer the text will be sent to. In the lower-left corner there's a "Press Return after sending" option, checked by default, so the text is submitted straight to Claude. If you'd rather review it before submitting manually, uncheck it (the same switch is also under "Options" in the main window).

If the remote desktop software swallows this key combo and the small window doesn't appear, click the big "Speak" button in the main window, or the menu bar icon → "Speak".

> **You can change the shortcuts**: in "Settings… → Shortcuts", click the button, then press the new key combo. On some Macs, ⌃⌥Space is already taken by the system shortcut "Select next source in Input menu", so pressing it switches input sources instead. When that happens, the app shows an orange notice: either turn that item off in System Settings → Keyboard → Keyboard Shortcuts → Input Sources, or pick a different combo in MicHop.

## Two transfer modes

Switch by clicking the "Text" or "Audio" card under "Send As" in the main window; you can also switch from the menu bar icon's menu. **The default is Text.**

| | Send Text (default) | Send Audio |
|---|---|---|
| Where speech is recognized | On this Mac, via System Dictation | On the other computer, via its own dictation or Claude Code voice mode |
| What ⌃⌥Space does | Opens the dictation window | Starts or stops "Always On" sending |
| Holding ⌃⌥ | — | Sends only while held, stops when released |
| Big button in the main window | "Speak" | "Start Audio" / "Stop Audio" |
| What the other Mac needs | Just the Receiver | The Receiver plus its built-in virtual audio device |

## Send Audio mode

Use this mode when you want the working computer to **hear your voice directly**, for example to use Claude Code's voice mode on that computer, or its own dictation.

```
MacBook mic ──audio──► Receiver ──► MicHop Audio virtual device ──► any app on that Mac that "listens to the mic"
```

**First, on the Receiver computer:**

1. Install the built-in virtual audio device **MicHop Audio**: the first time the Sender sends audio, the Receiver shows a prompt; click "Install". You can also click "Install" under "Settings… → Virtual Audio Device" on the Receiver. macOS asks for an administrator password once, and system sound cuts out for a second or two after installation.
2. Once installed, follow the prompt to set the **system input device** to MicHop Audio (there's also a "Fix" button under "Setup" in the main window).
3. Keep the system **output** device set to the speakers (or the remote desktop software's audio device). MicHop Audio can't be chosen as the system output at all, so system sound never gets mixed in.

> **Already have BlackHole?** It still works: choose the device you want under "Setup → Play Into". To switch to the built-in one, click "Install" next to "You can switch to the built-in virtual device". When using BlackHole, be careful not to select it as the system output. If you do, a "System Output" warning appears under "Setup"; just click "Switch to Speakers".

> **Why is there an echo?** Many remote desktop apps (UU Remote, for example) capture the remote computer's sound using Apple's screen recording framework, which records **the sound of every app** on that computer, no matter which audio device it plays to. When MicHop plays your voice into the virtual audio device, that gets recorded too, sent back to your computer, played through your speakers, and picked up again by your microphone.
>
> That's why the Sender has **"Echo Cancellation"** on by default (you can turn it off under "Options" in the main window). It uses Apple's voice processing — the same one FaceTime uses: it subtracts the returning sound from the microphone signal, ducks other sounds while you're speaking, and reduces noise as a bonus. Headphones give the best results.

**How to use:**

In the main window under "Send As", choose "Audio", and the Sender connects to the Receiver (the first time, it will ask for microphone permission); "Connection" turns blue and the menu bar icon turns green. From then on, two ways to talk are always available:

1. **Always On**: press **⌃⌥Space** once (or click "Start Audio"), and the microphone stays on; press it again to stop.
2. **Hold to talk**: **hold Ctrl + Option while you talk, and release to stop**. The microphone is only on while you hold the keys; the "Audio" tile in the main window turns red, and so does the menu bar icon. Once you release, the microphone turns off and this Mac's volume isn't lowered either. The first time, it will ask for Accessibility permission, which it uses to detect this key combo; if it hasn't been granted, "Options" in the main window will point it out, and you can click "Turn On…".
3. The remote desktop software also passes the held key combo on to the working computer. If you set the dictation or input method voice shortcut on that computer to Ctrl + Option as well (see [the tip below](#tip-the-fn-key-doesnt-pass-through-remote-connections-so-change-the-shortcut)), **a single press both sends your audio and starts dictation over there**.
4. Both shortcuts can be changed under "Settings… → Shortcuts".

> While you hold the keys, MicHop temporarily mutes this Mac, so sound sent back by the remote-desktop app can't reach the microphone and cause an echo; sound returns about 1 second after you let go. (Always On mode uses Apple's echo cancellation instead.)

### Tip: the Fn key doesn't pass through remote connections, so change the shortcut

When connected through remote desktop software like UU Remote, Sunlogin, or ToDesk, **pressing Fn on your local Mac doesn't reach the remote computer**. Whether the remote side uses System Dictation or WeChat Input Method's voice input, it won't be triggered. There are two reasons: the Fn key is intercepted by your local Mac first (which starts its own dictation); and even if the remote software does forward it, on the remote side it's only a "simulated keypress", which the system and input methods usually ignore.

The fix: on the **remote computer** (e.g. the Mac mini), change the voice input shortcut:

- **System Dictation**: System Settings → Keyboard → Dictation → Shortcut → "Customize".
- **WeChat Input Method**: change the voice input shortcut in WeChat Input Method's settings.

A **modifier-key combo** is recommended, such as **left Ctrl + Option**, or Ctrl plus another modifier (Option, Shift, Command).

**Don't use Ctrl plus a number or letter key** (e.g. Ctrl+D). Voice input usually means holding the key down while you talk, and holding a letter or number key makes that character repeat, which is very annoying. Holding a pure modifier combo doesn't type any characters.

This trick pairs with "Send Audio" mode: set the remote computer's input device to MicHop Audio, hold the new shortcut in the remote desktop while you speak, and the remote computer can dictate directly.

## Not on the same network? Use Tailscale

1. Install [Tailscale](https://tailscale.com) on both computers and sign in to the same account.
2. In the Receiver's main window, the "Tailscale" row under "Connection Info" shows 100.x.x.x; enter that in the Sender's settings. You can also enter the machine name shown in Tailscale.
3. If it says "Not found", first make sure Tailscale is connected on the Receiver computer, then click the refresh button on that row to detect it again. If it still can't be detected, go to the Receiver's "Settings… → Tailscale → Manual Address" and type in the address shown in the Tailscale menu.

The Tailscale address works both at home and away; when both computers are on the same LAN, it connects directly automatically.

## Security

- Each Receiver has a random 6-digit passcode, and any request with the wrong passcode is rejected. You can click "New" on the "Passcode" row in the Receiver's main window (after that, re-enter the new passcode on the Sender).
- The Receiver listens on two TCP ports, **8765** (text) and **8766** (audio), and the traffic is not encrypted. Use it only on your home LAN or over Tailscale, and don't expose these ports to the public internet.
- Pasting temporarily borrows the clipboard; its original contents are restored after about 1 second.

## FAQ

- **Can't connect**: make sure both computers are on the same network, or both are connected to Tailscale. LAN IPs can change, so consider giving the Receiver a fixed IP in your router, or just use the Tailscale address.
- **Says Accessibility permission isn't granted**: after the app is rebuilt or updated, macOS may invalidate the previous authorization. Remove the old entry from the Accessibility list first, then add it again.

## Automatic updates

Both apps check GitHub for new versions on their own: once 30 seconds after launch, then every 6 hours. When a new version is found, it's downloaded, swapped in, and relaunched automatically.

- The current version number is shown in the lower-left corner of the main window; click "Check for Updates" under "Settings… → General" to check right away.
- If you don't want automatic installation, turn off "Install Updates Automatically" under "Settings… → General". From then on, when a new version is available, an "Update to x.y.z" button appears in Settings and the same item appears in the menu bar menu; it only updates when you click it.
- It won't interrupt you mid-use: the Sender doesn't update while the dictation window is open; the Receiver doesn't update while receiving audio, or within 1 minute of receiving text.
- Safety: a new version must be signed with **the same certificate** as the current version, or installation is refused.
- After an upgrade, Accessibility, microphone, and other permissions are kept; no need to re-grant them.

## License

[MIT](LICENSE)
