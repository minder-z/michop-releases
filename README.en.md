<p align="center"><img src="assets/banner.png" alt="传声筒 MicHop" width="760"></p>
<p align="center"><a href="README.md">简体中文</a> · <a href="README.zh-Hant.md">繁體中文</a> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.es.md">Español</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pt.md">Português</a> · <a href="README.ru.md">Русский</a></p>

<p align="center">
  <b>Lend this Mac's microphone to another Mac.</b><br>
  Talk into this one, and the other one hears it as if a mic were plugged in. Works over your LAN or Tailscale.<br>
  <sub>Lend your Mac's microphone to another Mac — live, over LAN or Tailscale.</sub>
</p>

---

## What it's for

I usually work on a MacBook and use remote desktop software (UU Remote, Sunlogin, ToDesk and the like) to get things done on a Mac mini — having Claude Code write code, editing videos, maintaining websites.

The catch: **the Mac mini has no microphone, and remote desktop software doesn't forward the MacBook's microphone**, so voice input doesn't work inside the remote session.

MicHop fixes exactly that. You install one app on each computer:

- **The computer you talk into** (e.g. the MacBook): install "MicHop"
- **The computer you work on** (e.g. the Mac mini): install "MicHop Receiver"

```
MacBook (talking)                            Mac mini (working)

Microphone ── 🔊 audio ───────────►  Virtual mic (built-in MicHop Audio)
                                      → Dictation / WeChat Input / Claude Code voice mode

              over your LAN or Tailscale
```

Audio from the MacBook's microphone streams to the Mac mini in real time and becomes the Mac mini's microphone. Any app on the Mac mini that needs a mic can use it — macOS Dictation, voice input in WeChat Input, Claude Code's voice mode, and so on.

- The receiver comes with its own virtual audio device, **MicHop Audio**, and offers to install it the first time you open it (you'll enter an administrator password once). Nothing else to download. If you already have [BlackHole](https://github.com/ExistentialAudio/BlackHole) installed, you can keep using it.
- Two ways to talk, both always available: press **⌃⌥M** once to keep sending and again to stop, or **hold ⌃⌥** while you speak and let go to stop.
- Built-in echo cancellation, so there's no echo even while a remote desktop session is running.
- The Fn key doesn't make it through remote desktop software, so change the voice-input shortcut on the Mac mini to a modifier-key combo such as Ctrl + Option — [see below](#tip-fn-doesnt-work-over-remote-connections-so-change-the-shortcut).

### How the two computers connect

- **On the same LAN**: just enter the Mac mini's LAN IP.
- **In different places**: install [Tailscale](https://tailscale.com) on both computers to put them on one virtual network, then enter the Mac mini's **Tailscale IP** (it starts with 100). It works the same at home or on the road.
- The receiver's window lists the LAN IP, the Tailscale IP and the passcode, each with its own copy button.

### Other highlights

- **No cloud services involved**: audio goes straight between your own two computers, over your LAN or through Tailscale's encrypted tunnel.
- **Works with any remote desktop tool**: UU Remote, Sunlogin, ToDesk and Screen Sharing all work alongside it.
- **Automatic updates**: new versions install themselves, and you don't have to grant permissions again.
- **Multilingual**: the interface is available in 简体中文, 繁體中文, English, 日本語, 한국어, Español, Français, Deutsch, Português and Русский. It defaults to Simplified Chinese; switch under "Settings… → General → Language".

## Download and install

Download from [Releases](../../releases/latest):

| File | Install on | Menu bar icon |
|---|---|---|
| `MicHop.zip` (MicHop) | The computer you talk into, e.g. a MacBook | Two microphones, same as the app icon |
| `MicHop-Receiver.zip` (MicHop Receiver) | The computer you work on, e.g. a Mac mini | Same as above |

The menu bar icon's color shows the status: **gray** = not connected, **green** = connected, **red** = sending audio.

> **Both apps are built around their main window**: click the Dock icon to bring it up. Across the top, two status areas show "Connection" (gray / blue) and "Audio" (gray / red), and everyday controls live in the window. Shortcuts, language, automatic updates and the like are under "Settings…" (⌘,). The menu bar icon and the Dock icon's right-click menu keep only the most common items. If the MacBook's camera notch hides the menu bar icon, just use the Dock icon.

Requires macOS 13 or later. Runs on both Apple silicon and Intel Macs.

> **"Developer cannot be verified" on first launch**: this happens because the app hasn't been through Apple's paid notarization. Open System Settings → Privacy & Security and click "Open Anyway" near the bottom of the page. Or remove the quarantine flag in Terminal, then open the app:
> ```bash
> xattr -dr com.apple.quarantine "/Applications/MicHop Receiver.app"
> ```

### 1. The computer you work on (receiver)

1. Unzip `MicHop-Receiver.zip`, drag "MicHop Receiver" into Applications, and open it.
   - If you're asked whether to accept incoming network connections, click **Allow**.
2. On first launch it offers to install its built-in virtual audio device, **MicHop Audio**: click "Install" and enter your administrator password once. System audio drops out for a second or two when installation finishes. You can also install it later under "Settings… → Virtual Audio Device".
3. Once it's installed, follow the prompt to set the **system input device** to MicHop Audio (the "Setup" section of the main window also has a "Fix" button). Leave the system **output** device on your speakers (or the remote desktop software's audio device). MicHop Audio itself can't be chosen as the system output, so system sounds never get mixed in.
4. The main window shows:
   - **Connection Info**: this Mac's LAN address, Tailscale address and passcode, each with a copy button.
   - **Setup**: when both the virtual audio device and the system input device show a green check mark, you're ready. Any item with a yellow warning has a fix button right next to it.
5. It launches at login by default; turn that off under "Settings… → General" if you don't want it.

> **Already using BlackHole?** It works as before: choose the device you want under "Setup → Play Into". To switch to the built-in one, click "Install" next to "You can switch to the built-in virtual device". When using BlackHole, be careful not to make it the system output — if you do, a "System Output" warning appears in "Setup"; just click "Switch to Speakers".

### 2. The computer you talk into (sender)

1. Unzip `MicHop.zip`, drag "MicHop" into Applications, and open it.
2. On first launch a setup window appears: enter the receiver's **address** and **passcode**, click "Test Connection", and once you see the green "Connected — ready to go", click "Save".
   - In the receiver's window, the copy buttons next to the address and passcode copy each item separately.
   - Or click "Copy All" on the receiver and paste the whole thing into the "Address" field. The sender picks out the address automatically (preferring the Tailscale address if there is one) and fills in the passcode for you.
   - If you're asked to allow the app to find devices on your local network, click **Allow**.
3. The first time, it asks for **Microphone** access — click Allow. It also asks for **Accessibility** access (used to detect "hold ⌃⌥"); follow the prompt: System Settings → Privacy & Security → Accessibility → turn on "MicHop".
4. Once the app is open, it connects to the receiver. When "Connection" in the main window turns blue and the menu bar icon turns green, you're good to go. To change the address or passcode later, click "Change…" in the "Receiver" row of the main window, or press ⌘,.

## How to use

First, in the remote desktop, click wherever you want to use voice on the working computer — Claude Code's voice mode, Dictation, or an input method. Then either way of talking is available at any time:

1. **Keep sending**: press **⌃⌥M (Ctrl + Option + M)** once, or click "Start Audio" in the main window. The microphone stays on until you press it again.
2. **Hold to send**: **hold Ctrl + Option while you speak, and let go to stop**. The microphone is only on while you hold the keys.

While audio is being sent, "Audio" in the main window and the menu bar icon turn red, and so does "Audio" on the receiver.

- The keys you're holding are also passed through to the working computer by the remote desktop software. If you set the dictation or input-method voice shortcut on that computer to Ctrl + Option as well (see the [tip below](#tip-fn-doesnt-work-over-remote-connections-so-change-the-shortcut)), **a single press both sends your voice and starts dictation over there**.
- While you're holding the keys, MicHop temporarily mutes this Mac, so the other computer's audio — sent back by the remote desktop software — doesn't get picked up by the microphone and turn into echo. Sound comes back about a second after you let go. (Keep-sending mode relies on Apple's echo cancellation instead.)

> **You can change the shortcuts**: in "Settings… → Shortcuts", click a button and press the new key combination. "Start Talking" can be any combination that includes ⌃, ⌥ or ⌘; "Hold to Talk" needs two or more of ⌃ ⌥ ⇧ ⌘. If the combination is already taken by the system (for example, ⌃⌥Space is "Select next source in Input menu" on many Macs), the app shows an orange notice: turn that item off in System Settings → Keyboard → Keyboard Shortcuts, or pick a different combination.

> **Why is there an echo?** Many remote desktop apps (UU Remote, for example) capture the remote computer's audio with Apple's screen-capture framework, which records **sound from every app** on that computer, no matter which audio device it plays to. So when MicHop plays your voice into the virtual audio device, it gets captured too, sent back to your computer, played through your speakers, and picked up again by your microphone.
>
> That's why the sender has **echo cancellation** on by default (you can turn it off under "Options" in the main window). It uses Apple's voice processing — the same one FaceTime uses — to subtract the returning audio from the microphone signal, duck other sounds while you're talking, and reduce noise along the way. Headphones work best.

### Tip: Fn doesn't work over remote connections, so change the shortcut

When you're connected through remote desktop software like UU Remote, Sunlogin or ToDesk, **pressing Fn on your local Mac doesn't reach the remote one**. Whether the remote side uses macOS Dictation or voice input in WeChat Input, Fn won't trigger it. There are two reasons: your local Mac intercepts Fn first (and starts its own dictation), and even if the remote software does forward it, it arrives as a "simulated keypress" that macOS and input methods usually ignore.

The fix: change the voice-input shortcut on the **remote computer** (e.g. the Mac mini):

- **Dictation**: System Settings → Keyboard → Dictation → Shortcut → "Customize".
- **WeChat Input**: change the voice-input shortcut in WeChat Input's settings.

A **modifier-key combination** works best, such as **left Ctrl + Option**, or Ctrl plus another modifier (Option, Shift, Command).

**Don't use Ctrl plus a number or letter key** (e.g. Ctrl+D). Voice input usually means holding the keys while you talk, and holding a letter or number key types that character over and over. A modifiers-only combination doesn't type anything while held.

With the remote computer's input device set to MicHop Audio, hold the new shortcut in the remote desktop and speak — the remote computer will take dictation directly.

## Not on the same network? Use Tailscale

1. Install [Tailscale](https://tailscale.com) on both computers and sign in to the same account.
2. In the receiver's main window, the "Tailscale" row under "Connection Info" shows 100.x.x.x. Enter it in the sender's settings. You can also use the machine name shown in Tailscale.
3. If it says "Not found", make sure Tailscale is connected on the receiver, then click the refresh button on that row to detect it again. If it still can't be detected, go to "Settings… → Tailscale → Manual Address" on the receiver and enter the address shown in the Tailscale menu.

The Tailscale address works both at home and away, and when the two computers are on the same LAN, Tailscale connects them directly.

## Security

- Every receiver has a random 6-digit passcode, and any connection with the wrong passcode is rejected. To get a new one, click "New" on the "Passcode" row of the receiver's main window (you'll then need to enter it again on the sender).
- The receiver listens on a single port: TCP **8766** (audio). The stream isn't encrypted yet, so use it only on your home network or over Tailscale, and don't expose this port to the internet.

## FAQ

- **Can't connect**: make sure both computers are on the same network, or both are connected to Tailscale. LAN IPs can change, so consider giving the receiver a fixed IP in your router, or just use the Tailscale address.
- **The receiver says it can't open the port**: usually an old receiver didn't quit completely and is still holding the port; the receiver ends it automatically. If another app is holding it, the message names that app, and the receiver starts up on its own once the port is freed.
- **Holding ⌃⌥ does nothing**: the sender needs **Accessibility** access. After you rebuild or update the app, macOS sometimes invalidates the existing permission. Remove the old entry from the Accessibility list, then add the app again.

## Automatic updates

Both apps check GitHub for new versions on their own: once 30 seconds after launch, then every 6 hours. When a new version is found, they download it, swap it in, and reopen automatically.

- The current version number is shown in the lower-left corner of the main window; click "Check for Updates" under "Settings… → General" to check right away.
- If you'd rather not install automatically, turn off "Install Updates Automatically" under "Settings… → General". When a new version comes out, an "Update to x.y.z" button appears in Settings and the same item shows up in the menu bar menu; the update only happens when you click it.
- Updates never interrupt you: nothing is updated while audio is being sent.
- Security: a new version must be signed with **the same certificate** as the current one, or it won't be installed.
- After an update, Accessibility, Microphone and other permissions are kept, so there's no need to grant them again.

## License

[MIT](LICENSE)
