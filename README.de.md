<p align="center"><img src="assets/banner.png" alt="传声筒 MicHop" width="760"></p>
<p align="center"><a href="README.md">简体中文</a> · <a href="README.zh-Hant.md">繁體中文</a> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.es.md">Español</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pt.md">Português</a> · <a href="README.ru.md">Русский</a></p>

<p align="center">
  <b>Leih das Mikrofon dieses Macs einfach einem anderen Mac.</b><br>
  Du sprichst hier, und der andere Mac hat plötzlich ein Mikrofon – im lokalen Netzwerk oder über Tailscale.<br>
  <sub>Lend your Mac's microphone to another Mac — live and encrypted, over LAN or Tailscale.</sub>
</p>

---

## Wozu ist das gut?

Ich arbeite meist am MacBook und verbinde mich per Fernsteuerungs-App (UU Remote, Sunlogin, ToDesk usw.) mit einem Mac mini, auf dem die eigentliche Arbeit läuft – etwa Claude Code beim Programmieren, Videoschnitt oder die Pflege von Websites.

Das Problem: **Der Mac mini hat kein Mikrofon, und die Fernsteuerungs-App reicht das Mikrofon des MacBooks nicht weiter.** In der Remote-Sitzung ist Spracheingabe deshalb nicht möglich.

Genau hier setzt MicHop an. Auf jeden der beiden Computer kommt eine App:

- **Der Computer, an dem du sprichst** (z. B. das MacBook): „MicHop“
- **Der Computer, auf dem gearbeitet wird** (z. B. der Mac mini): „MicHop Receiver“

```
MacBook (du sprichst)                        Mac mini (hier wird gearbeitet)

Mikrofon ──── 🔊 Audio ───────────────►  Virtuelles Mikrofon (integriertes MicHop Audio)
                                      → Diktat / WeChat-Eingabemethode / Sprachmodus von Claude Code

              über das lokale Netzwerk oder Tailscale
```

Der Ton vom Mikrofon des MacBooks wird in Echtzeit an den Mac mini übertragen und dient dort als Mikrofon. Jede App auf dem Mac mini, die ein Mikrofon braucht, kann es nutzen – etwa das Diktat von macOS, die Spracheingabe der WeChat-Eingabemethode oder der Sprachmodus von Claude Code.

- Der Receiver bringt mit **MicHop Audio** ein eigenes virtuelles Audiogerät mit. Beim ersten Öffnen wird dir die Installation angeboten (einmal das Administratorpasswort eingeben); ein separater Download ist nicht nötig. Wer bereits [BlackHole](https://github.com/ExistentialAudio/BlackHole) installiert hat, kann es weiter verwenden.
- Zwei Arten zu sprechen, beide jederzeit verfügbar: Drück einmal **⌃⌥M**, um durchgehend zu senden, und noch einmal, um zu stoppen. Oder **halte ⌃⌥** gedrückt, während du sprichst – loslassen beendet die Übertragung.
- Mit integrierter Echounterdrückung, sodass es auch über eine Fernsteuerungs-App kein Echo gibt.
- Die Fn-Taste kommt über Fernsteuerungs-Apps nicht an. Stell deshalb auf dem Mac mini den Kurzbefehl für die Spracheingabe auf eine Kombination aus Sondertasten um, z. B. Ctrl + Option – [mehr dazu unten](#tipp-wenn-die-fn-taste-bei-fernzugriff-nicht-ankommt-nimm-einen-anderen-kurzbefehl).

### So verbindest du die beiden Computer

- **Im selben lokalen Netzwerk**: Trag einfach die lokale IP-Adresse des Mac mini ein.
- **An verschiedenen Orten**: Installiere [Tailscale](https://tailscale.com) auf beiden Computern, um ein virtuelles lokales Netzwerk aufzubauen, und trag die **Tailscale-IP** des Mac mini ein (beginnt mit 100). Das funktioniert zu Hause genauso wie unterwegs.
- Das Fenster des Receivers zeigt die lokale IP, die Tailscale-IP und den Code an, jeweils mit einer Kopiertaste daneben.

### Weitere Merkmale

- **Keine Cloud dazwischen**: Der Ton geht direkt zwischen deinen beiden Computern hin und her, durchgehend verschlüsselt – über das lokale Netzwerk oder über Tailscale.
- **Unabhängig von der Fernsteuerungs-App**: Funktioniert mit UU Remote, Sunlogin, ToDesk und der Bildschirmfreigabe.
- **Automatische Updates**: Neue Versionen werden von selbst installiert, ohne dass du Berechtigungen neu erteilen musst.
- **Mehrsprachig**: Die Oberfläche gibt es auf 简体中文, 繁體中文, English, 日本語, 한국어, Español, Français, Deutsch, Português und Русский. Standard ist Chinesisch; umstellen kannst du unter „Einstellungen… → Allgemein → Sprache / Language“.

## Download und Installation

Lade die Dateien unter [Releases](../../releases/latest) herunter:

| Datei | Auf welchem Computer | Symbol in der Menüleiste |
|---|---|---|
| `MicHop.zip` (MicHop) | Der Computer, an dem du sprichst, z. B. das MacBook | Zwei Mikrofone, wie das App-Symbol |
| `MicHop-Receiver.zip` (MicHop Receiver) | Der Computer, auf dem gearbeitet wird, z. B. der Mac mini | Ebenso |

Die Farbe des Menüleistensymbols zeigt den Status: **Grau** = nicht verbunden, **Grün** = verbunden, **Rot** = Audio wird gesendet.

> **Bei beiden Apps dreht sich alles um das Hauptfenster**: Ein Klick auf das Dock-Symbol öffnet es. Oben siehst du zwei Statusbereiche, „Verbindung“ (grau/blau) und „Audio“ (grau/rot), und alle wichtigen Aktionen findest du im Fenster selbst. Kurzbefehle, Sprache, automatische Updates usw. liegen unter „Einstellungen…“ (⌘,). Das Menüleistensymbol und das Kontextmenü des Dock-Symbols enthalten nur die häufigsten Befehle. Verdeckt die Kamera-Notch deines MacBooks das Menüleistensymbol, nimm einfach das Dock-Symbol.

Voraussetzung ist macOS 13 oder neuer; Macs mit Apple Chip und mit Intel-Prozessor werden beide unterstützt.

> **Beim ersten Öffnen erscheint die Meldung, dass der Entwickler nicht verifiziert werden kann**: Das liegt daran, dass die App nicht kostenpflichtig von Apple notariell beglaubigt wurde. Öffne Systemeinstellungen → Datenschutz & Sicherheit und klick unten auf der Seite auf „Dennoch öffnen“. Alternativ kannst du die Quarantäne im Terminal mit diesem Befehl aufheben und die App danach öffnen:
> ```bash
> xattr -dr com.apple.quarantine "/Applications/MicHop Receiver.app"
> ```

### 1. Der Computer, auf dem gearbeitet wird (Receiver)

1. Entpacke `MicHop-Receiver.zip`, zieh „MicHop Receiver“ in den Ordner „Programme“ und öffne die App.
   - Wenn gefragt wird, ob eingehende Netzwerkverbindungen akzeptiert werden sollen, klick auf **Erlauben**.
2. Beim ersten Öffnen wird dir angeboten, das integrierte virtuelle Audiogerät **MicHop Audio** zu installieren: Klick auf „Installieren“ und gib einmal das Administratorpasswort ein. Nach der Installation setzt der Systemton für ein, zwei Sekunden aus. Du kannst das auch später unter „Einstellungen… → Virtuelles Audiogerät“ nachholen.
3. Stell danach wie angezeigt das **Eingabegerät des Systems** auf MicHop Audio um (im Bereich „Einrichtung“ des Hauptfensters gibt es dafür auch die Taste „Ändern“). Das **Ausgabegerät** des Systems bleibt einfach bei den Lautsprechern (oder dem Audiogerät der Fernsteuerungs-App). MicHop Audio selbst lässt sich nicht als Systemausgang wählen, sodass sich kein Systemton daruntermischt.
4. Im Hauptfenster siehst du:
   - **Verbindungsdaten**: die lokale Adresse, die Tailscale-Adresse und den Code dieses Macs, jeweils mit einer Kopiertaste daneben.
   - **Einrichtung**: Haben virtuelles Audiogerät und Systemeingang ein grünes Häkchen, ist alles bereit. Bei Punkten mit gelber Warnung steht rechts gleich eine Taste zum Beheben.
5. Der Receiver startet standardmäßig automatisch beim Anmelden. Wenn du das nicht möchtest, schalte es unter „Einstellungen… → Allgemein“ aus.

> **Du hast schon BlackHole installiert?** Das funktioniert weiterhin: Wähl unter „Einrichtung → Ausgabe auf“ das gewünschte Audiogerät. Möchtest du zum integrierten wechseln, klick neben „Zum integrierten virtuellen Gerät wechseln“ auf „Installieren“. Achte bei BlackHole darauf, es nicht als Systemausgang auszuwählen. Passiert das doch, erscheint unter „Einrichtung“ eine Warnung zum „Systemausgang“ – ein Klick auf „Zu Lautsprechern wechseln“ genügt.

### 2. Der Computer, an dem du sprichst (Sender)

1. Entpacke `MicHop.zip`, zieh „MicHop“ in den Ordner „Programme“ und öffne die App.
2. Beim ersten Öffnen erscheint das Einrichtungsfenster: Trag **Adresse** und **Code** des Receivers ein und klick auf „Verbindung testen“. Sobald das grüne „Verbunden – einsatzbereit“ erscheint, klick auf „Speichern“.
   - Im Fenster des Receivers kannst du Adresse und Code über die Kopiertasten daneben einzeln kopieren.
   - Oder du klickst im Receiver auf „Alles kopieren“ und fügst den ganzen Block ins Feld „Adresse“ ein. Der Sender sucht sich die Adresse automatisch heraus (eine Tailscale-Adresse hat Vorrang) und füllt auch den Code aus.
   - Wenn gefragt wird, ob die App Geräte in deinem lokalen Netzwerk finden darf, klick auf **Erlauben**.
3. Beim ersten Start fragt die App nach dem Zugriff auf das **Mikrofon** – klick auf „Erlauben“. Außerdem braucht sie Zugriff auf die **Bedienungshilfen** (damit sie erkennt, wann du ⌃⌥ gedrückt hältst). Folge den Hinweisen: Systemeinstellungen → Datenschutz & Sicherheit → Bedienungshilfen → „MicHop“ aktivieren.
4. Sobald die App geöffnet ist, verbindet sie sich mit dem Receiver. Wird „Verbindung“ im Hauptfenster blau und das Menüleistensymbol grün, kann es losgehen. Adresse oder Code änderst du später über „Ändern …“ im Bereich „Empfänger“ des Hauptfensters oder mit ⌘,.

## So benutzt du es

Klick in der Remote-Sitzung zuerst auf dem anderen Computer dorthin, wo du per Sprache eingeben willst – etwa in den Sprachmodus von Claude Code, das Diktat oder eine Eingabemethode. Danach stehen dir jederzeit beide Arten zu sprechen zur Verfügung:

1. **Durchgehend senden**: Drück einmal **⌃⌥M (Ctrl + Option + M)** oder klick im Hauptfenster auf „Audio starten“. Das Mikrofon bleibt offen, bis du die Tasten noch einmal drückst.
2. **Halten zum Sprechen**: **Halte Ctrl + Option gedrückt, während du sprichst, und lass los, wenn du fertig bist.** Das Mikrofon ist nur offen, solange du die Tasten hältst.

Während gesendet wird, werden „Audio“ im Hauptfenster und das Menüleistensymbol rot; auch „Audio“ auf der Seite des Receivers wird rot.

- Die gehaltenen Tasten reicht die Fernsteuerungs-App auch an den anderen Computer weiter. Legst du dort den Kurzbefehl für Diktat oder Spracheingabe ebenfalls auf Ctrl + Option (siehe den [Tipp weiter unten](#tipp-wenn-die-fn-taste-bei-fernzugriff-nicht-ankommt-nimm-einen-anderen-kurzbefehl)), **startest du mit einem einzigen Tastendruck die Übertragung und gleichzeitig das Diktat drüben**.
- Während du die Tasten hältst, schaltet MicHop diesen Mac vorübergehend stumm. So kann der Ton des anderen Computers, den die Fernsteuerungs-App zurückschickt, nicht vom Mikrofon aufgenommen werden und als Echo zurückkommen. Etwa eine Sekunde nach dem Loslassen ist der Ton wieder da. (Beim durchgehenden Senden kommt die Echounterdrückung von Apple zum Einsatz.)

> **Die Kurzbefehle lassen sich ändern**: Klick unter „Einstellungen… → Kurzbefehle“ auf eine Taste und drück dann die neue Kombination. Für „Sprechen starten“ eignet sich jede Kombination mit ⌃, ⌥ oder ⌘; „Halten zum Sprechen“ braucht mindestens zwei der Tasten ⌃ ⌥ ⇧ ⌘. Ist die gewählte Kombination schon vom System belegt (⌃⌥Leertaste etwa ist auf vielen Macs „Nächste Quelle im Eingabemenü auswählen“), zeigt die App einen orangefarbenen Hinweis an. Deaktiviere den Eintrag dann unter Systemeinstellungen → Tastatur → Tastaturkurzbefehle oder nimm eine andere Kombination.

> **Woher kommt das Echo?** Viele Fernsteuerungs-Apps (z. B. UU Remote) greifen den Ton auf dem gesteuerten Mac über Apples Framework für Bildschirmaufnahmen ab. Dabei wird **alles aufgenommen, was irgendeine App auf diesem Computer abspielt** – ganz egal, auf welchem Audiogerät. Spielt MicHop deine Stimme in das virtuelle Audiogerät, wird sie also mit aufgenommen, an deinen Computer zurückgeschickt, über die Lautsprecher wiedergegeben und vom Mikrofon erneut eingefangen.
>
> Deshalb ist die **Echounterdrückung** im Sender standardmäßig aktiv (abschaltbar unter „Optionen“ im Hauptfenster). Sie nutzt Apples Sprachverarbeitung, dieselbe wie bei FaceTime: Der zurückkommende Ton wird aus dem Mikrofonsignal herausgerechnet, andere Geräusche werden leiser gestellt, während du sprichst, und nebenbei wird das Rauschen reduziert. Am besten klappt es mit Kopfhörern.

### Tipp: Wenn die Fn-Taste bei Fernzugriff nicht ankommt, nimm einen anderen Kurzbefehl

Bist du über eine Fernsteuerungs-App wie UU Remote, Sunlogin oder ToDesk verbunden, **kommt die Fn-Taste, die du an deinem Mac drückst, auf dem gesteuerten Mac nicht an**. Weder das Diktat von macOS noch die Spracheingabe der WeChat-Eingabemethode lassen sich so auslösen. Dafür gibt es zwei Gründe: Dein eigener Mac fängt die Fn-Taste zuerst ab (und startet selbst das Diktat). Und selbst wenn die Fernsteuerungs-App sie weiterreicht, ist sie auf dem gesteuerten Mac nur ein „simulierter Tastendruck“, den System und Eingabemethoden meist ignorieren.

Die Lösung: Ändere auf dem **gesteuerten Mac** (z. B. dem Mac mini) den Kurzbefehl für die Spracheingabe:

- **Diktat von macOS**: Systemeinstellungen → Tastatur → Diktat → Kurzbefehl → „Anpassen …“.
- **WeChat-Eingabemethode**: Ändere in den Einstellungen der WeChat-Eingabemethode den Kurzbefehl für die Spracheingabe.

Am besten eignet sich eine **Kombination aus Sondertasten**, etwa **linke Ctrl-Taste + Option** oder Ctrl mit einer anderen Sondertaste (Option, Shift, Command).

**Nimm nicht Ctrl plus eine Ziffer oder einen Buchstaben** (z. B. Ctrl+D). Für die Spracheingabe hältst du die Tasten meist gedrückt, und eine gehaltene Buchstaben- oder Zifferntaste tippt das Zeichen immer wieder – das ist mühsam. Eine reine Kombination aus Sondertasten erzeugt beim Halten kein Zeichen.

Stell das Eingabegerät des gesteuerten Macs auf MicHop Audio, halte in der Remote-Sitzung den neuen Kurzbefehl gedrückt und sprich – schon diktiert der gesteuerte Mac direkt.

## Den Ton des Mac mini zurückholen (virtueller Lautsprecher)

Das integrierte virtuelle Audiogerät des Receivers enthält außerdem einen **virtuellen Lautsprecher, MicHop Speaker** (ab 1.6.0). Er ist ein eigenes Gerät, getrennt von MicHop Audio, über das dein Mikrofonton läuft – die beiden Tonspuren vermischen sich also nicht.

Schalte im Receiver unter „Einstellungen… → Virtuelles Audiogerät“ die Option „Ton dieses Macs an MicHop Speaker senden“ ein:

- Die Systemausgabe des Mac mini wechselt auf MicHop Speaker, **die eigenen Lautsprecher bleiben stumm** – im Raum ertönt also nicht plötzlich etwas;
- Fernsteuerungs- oder Bildschirmaufnahme-Apps, bei denen man ein Audiogerät auswählt (etwa manche Versionen von Sunlogin und ToDesk oder OBS), können MicHop Speaker als Tonquelle nehmen und so den Ton des Mac mini zu dir zurückholen;
- Die Lautstärketasten der Tastatur funktionieren darauf ganz normal, und der aufgenommene Ton folgt der Lautstärke;
- Schaltest du die Option aus, beendest den Receiver oder deinstallierst das virtuelle Audiogerät, wechselt die Systemausgabe automatisch zurück auf das vorherige Gerät.

> Fernsteuerungs-Apps wie UU Remote, die den Ton über die Bildschirmaufnahme von macOS abgreifen, hören ihn unabhängig davon, auf welchem Gerät er ausgegeben wird. Für sie liegt der Hauptvorteil des virtuellen Lautsprechers darin, dass die Lautsprecher des Mac mini stumm bleiben, während du ihn aus der Ferne trotzdem hörst.

Die letzte Zeile unter „Einrichtung“ im Hauptfenster des Receivers, „Ton dieses Macs“, zeigt an, wohin der Ton dieses Computers gerade ausgegeben wird.

## Nicht im selben Netzwerk? Nimm Tailscale

1. Installiere [Tailscale](https://tailscale.com) auf beiden Computern und melde dich jeweils mit demselben Account an.
2. Im Hauptfenster des Receivers steht unter „Verbindungsdaten“ in der Zeile „Tailscale“ eine Adresse im Format 100.x.x.x. Trag sie in den Einstellungen des Senders ein. Alternativ geht auch der Gerätename, den Tailscale anzeigt.
3. Steht dort „Nicht gefunden“, prüf zuerst, ob Tailscale auf dem Receiver-Mac verbunden ist, und klick dann in dieser Zeile auf die Aktualisieren-Taste, um erneut zu suchen. Wird die Adresse trotzdem nicht erkannt, trag sie im Receiver unter „Einstellungen… → Tailscale → Manuelle Adresse“ von Hand ein, so wie sie im Tailscale-Menü steht.

Die Tailscale-Adresse funktioniert zu Hause wie unterwegs; seid ihr im selben lokalen Netzwerk, verbindet Tailscale die beiden Geräte automatisch direkt.

## Sicherheit

- **Der Ton ist durchgehend verschlüsselt**: Bei jeder Verbindung findet zuerst ein Schlüsselaustausch statt (X25519), danach wird jedes Stück Audio mit ChaCha20-Poly1305 verschlüsselt. Das schützt vor Leuten im selben Netzwerk, die mithören oder Pakete mitschneiden: Sie hören nicht, was du sagst, und kommen auch nicht an den Code. Der Code selbst wird nie übers Netz geschickt.
- Jeder Receiver hat einen zufälligen 6-stelligen Code; Verbindungen mit falschem Code werden immer abgelehnt. Nach 5 Fehlversuchen in Folge nimmt der Receiver 30 Sekunden lang keine neuen Verbindungen an, und das Hauptfenster meldet „Jemand probiert Codes aus“. Einen neuen Code erzeugst du im Hauptfenster des Receivers in der Zeile „Code“ mit „Neu“ (danach musst du ihn im Sender neu eintragen).
- **Wogegen es nicht schützt**: gegen jemanden, der die Verbindung aktiv kapert und sich als Receiver ausgibt. Ein 6-stelliger Code hat nur eine Million Möglichkeiten; wer einmal einen Handshake abgefangen hat, kann ihn offline durchprobieren. Nutze MicHop daher nur im Heimnetz oder über Tailscale und gib den Port des Receivers (TCP **8766**) nicht ins Internet frei.
- Sender und Receiver müssen beide Version 1.6.0 oder neuer sein. Ist eine Seite zu alt, weist die andere darauf hin, dass sie aktualisiert werden muss.

## Häufige Fragen

- **Keine Verbindung**: Prüf, ob beide Computer im selben Netzwerk sind oder beide mit Tailscale verbunden sind. Die lokale IP kann sich ändern; vergib dem Receiver im Router am besten eine feste IP oder nimm gleich die Tailscale-Adresse.
- **Der Receiver meldet, dass der Port nicht geöffnet werden kann**: Meist hat sich ein alter Receiver nicht sauber beendet und belegt den Port noch – der Receiver beendet ihn dann automatisch. Belegt eine andere App den Port, nennt der Hinweis ihren Namen; sobald der Port frei ist, startet der Receiver von selbst.
- **Halten von ⌃⌥ bewirkt nichts**: Der Sender braucht Zugriff auf die **Bedienungshilfen**. Nach einem Neukompilieren oder Update der App macht macOS die bisherige Freigabe manchmal ungültig. Entferne dann den alten Eintrag aus der Liste unter „Bedienungshilfen“ und füge die App neu hinzu.

## Automatische Updates

Beide Apps suchen selbst auf GitHub nach neuen Versionen: einmal 30 Sekunden nach dem Start und danach alle 6 Stunden. Gibt es eine neue Version, wird sie automatisch geladen, ersetzt und neu geöffnet.

- Die aktuelle Versionsnummer steht unten links im Hauptfenster; unter „Einstellungen… → Allgemein“ kannst du mit „Nach Updates suchen“ sofort prüfen.
- Möchtest du nicht automatisch installieren, schalte unter „Einstellungen… → Allgemein“ die Option „Updates automatisch installieren“ aus. Bei einer neuen Version erscheint dann in den Einstellungen die Taste „Auf x.y.z aktualisieren“ und derselbe Eintrag auch im Menü der Menüleiste – aktualisiert wird erst, wenn du darauf klickst.
- Kein Update mittendrin: Während Audio gesendet wird, wird nicht aktualisiert.
- Sicherheit: Die neue Version muss mit **demselben Zertifikat** signiert sein wie die aktuelle, sonst wird die Installation abgelehnt.
- Nach dem Update bleiben Berechtigungen wie Bedienungshilfen und Mikrofon erhalten; du musst nichts neu freigeben.

## License

[MIT](LICENSE)
