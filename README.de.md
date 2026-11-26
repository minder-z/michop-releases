<p align="center"><img src="assets/banner.png" alt="传声筒 MicHop" width="760"></p>
<p align="center"><a href="README.md">简体中文</a> · <a href="README.zh-Hant.md">繁體中文</a> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.es.md">Español</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pt.md">Português</a> · <a href="README.ru.md">Русский</a></p>

<p align="center">
  <b>Leih das Mikrofon dieses Macs einem anderen Mac.</b><br>
  Als Audio oder als Text – im lokalen Netzwerk oder über Tailscale.<br>
  <sub>Lend your Mac's microphone to another Mac — as live audio or as text, over LAN or Tailscale.</sub>
</p>

---

## Wozu ist das gut?

Ich arbeite normalerweise an einem MacBook und verbinde mich per Fernsteuerungssoftware (UU Remote, Sunlogin, ToDesk usw.) mit einem Mac mini, um dort zu arbeiten – etwa um Claude Code Code schreiben zu lassen, Videos zu schneiden oder Websites zu pflegen.

Das Problem: **Der Mac mini hat kein Mikrofon, und die Fernsteuerungssoftware überträgt das Mikrofon des MacBooks nicht.** In der Remote-Sitzung ist deshalb keine Spracheingabe möglich.

Genau das löst MicHop. Auf jedem der beiden Computer wird eine App installiert:

- **Der Computer, in den du sprichst** (z. B. das MacBook): „MicHop“ installieren
- **Der Computer, der die Arbeit macht** (z. B. der Mac mini): „MicHop Receiver“ installieren

### Zwei Übertragungsarten, jederzeit im Hauptfenster umschaltbar

```
MacBook (spricht)                            Mac mini (arbeitet)

Mikrofon ── 🔊 Audio senden ──────────►  Virtuelles Mikrofon (integriertes MicHop Audio)
                                      → Diktat / WeChat Input Method / Sprachmodus von Claude Code

Diktat ──── 📝 Text senden ───────────►  An der Cursorposition eingefügt, optional mit automatischem Return

              über lokales Netzwerk oder Tailscale
```

**🔊 Audio senden: Der Mac mini „hört“ dich direkt**

Der Ton vom Mikrofon des MacBooks wird in Echtzeit an den Mac mini übertragen und wird dort zum Mikrofon des Mac mini. Jede App auf dem Mac mini, die ein Mikrofon braucht, kann es nutzen – etwa das Systemdiktat, die Spracheingabe von WeChat Input Method oder der Sprachmodus von Claude Code.

- Der Receiver bringt sein eigenes virtuelles Audiogerät **MicHop Audio** mit. Beim ersten Senden von Audio wird die Installation angeboten (einmal das Administratorpasswort eingeben); ein separater Download ist nicht nötig. Wer bereits [BlackHole](https://github.com/ExistentialAudio/BlackHole) installiert hat, kann es weiter verwenden.
- Mit integrierter Echounterdrückung – kein Echo, selbst wenn du per Fernsteuerungssoftware verbunden bist.
- Die Fn-Taste kommt über Fernsteuerungssoftware nicht an. Ändere daher das Tastenkürzel für die Spracheingabe in eine Kombination aus Sondertasten, z. B. Ctrl + Option. [Details siehe unten](#tipp-die-fn-taste-kommt-bei-fernzugriff-nicht-an-also-tastenkürzel-ändern).

**📝 Text senden: Erkennung auf dem MacBook, die Wörter werden übertragen**

Drücke auf dem MacBook ⌃⌥Leertaste (Ctrl + Option + Leertaste) und wandle deine Sprache mit dem Systemdiktat in Text um. Der Text wird an den Mac mini gesendet und automatisch an der Cursorposition eingefügt; auf Wunsch wird auch automatisch Return gedrückt, sodass er direkt an Claude abgeschickt wird.

- Auf dem Mac mini musst du weder einen Audiotreiber installieren noch Audio einrichten – die einfachste und stabilste Variante.
- Das ist der Standardmodus der App.

| | 🔊 Audio senden | 📝 Text senden |
|---|---|---|
| Wo wird die Sprache erkannt? | Mac mini (mit eigenem Diktat oder eigener Eingabemethode) | MacBook (mit dem Systemdiktat) |
| Was der Mac mini braucht | Receiver + integriertes virtuelles Audiogerät (wird bei der ersten Nutzung installiert) | Nur den Receiver |
| Geeignet für | Eingabemethode, Diktat oder Claude-Sprachmodus des Mac mini nutzen | Einfach Gesprochenes als Text eingeben |

### So verbinden sich die beiden Computer

- **Im selben lokalen Netzwerk**: Einfach die lokale IP-Adresse des Mac mini eintragen.
- **An verschiedenen Orten**: Installiere [Tailscale](https://tailscale.com) auf beiden Computern, um ein virtuelles lokales Netzwerk zu bilden, und trage die **Tailscale-IP** des Mac mini ein (beginnt mit 100). **Audio und Text können beide über Tailscale laufen** – zu Hause wie unterwegs.
- Das Fenster des Receivers zeigt lokale IP, Tailscale-IP und Code an; neben jedem Wert gibt es eine Kopieren-Schaltfläche.

### Weitere Merkmale

- **Kein Cloud-Dienst beteiligt**: Audio und Text gehen direkt zwischen deinen beiden Computern hin und her – über das lokale Netzwerk oder durch den verschlüsselten Tunnel von Tailscale.
- **Unabhängig von der Fernsteuerungssoftware**: Funktioniert zusammen mit UU Remote, Sunlogin, ToDesk und der Bildschirmfreigabe.
- **Automatische Updates**: Aktualisiert sich selbst, sobald eine neue Version erscheint, ohne dass du Berechtigungen neu erteilen musst.
- **Mehrsprachig**: Die Oberfläche unterstützt 简体中文, 繁體中文, English, 日本語, 한국어, Español, Français, Deutsch, Português und Русский. Standard ist Chinesisch; umschalten lässt sich die Sprache unter „Einstellungen… → Allgemein → Sprache / Language“.

## Download und Installation

Herunterladen unter [Releases](../../releases/latest):

| Datei | Auf welchem Computer | Menüleistensymbol |
|---|---|---|
| `MicHop.zip` (MicHop) | Der Computer, in den du sprichst, z. B. MacBook | Abgerundetes Quadrat wie das App-Symbol |
| `MicHop-Receiver.zip` (MicHop Receiver) | Der Computer, der arbeitet, z. B. Mac mini | Ebenso |

Die Farbe des Menüleistensymbols zeigt den Status: **Grau** = nicht verbunden, **Grün** = verbunden, **Rot** = es wird gerade übertragen (Sprechen / Audio empfangen).

> **Bei beiden Apps steht das Hauptfenster im Mittelpunkt**: Ein Klick auf das Dock-Symbol öffnet das Hauptfenster. Oben zeigen zwei Felder den Status: „Verbindung“ (grau / blau) und „Audio“ (grau / rot), und die üblichen Aktionen erledigst du direkt im Fenster; Sprache, automatische Updates usw. findest du unter „Einstellungen…“ (⌘,). Das Menüleistensymbol und der Rechtsklick auf das Dock-Symbol bieten nur noch die wichtigsten Einträge. Wenn die Kamera-Notch des MacBook das Menüleistensymbol verdeckt, nimm einfach das Dock-Symbol.

Erfordert macOS 13 oder neuer; läuft sowohl auf Macs mit Apple Chip als auch auf Intel-Macs.

> **Beim ersten Öffnen erscheint „Entwickler kann nicht überprüft werden“**: Das liegt daran, dass die App nicht die kostenpflichtige Notarisierung durch Apple durchlaufen hat. Öffne Systemeinstellungen → Datenschutz & Sicherheit und klicke unten auf der Seite auf „Dennoch öffnen“. Alternativ kannst du im Terminal diesen Befehl ausführen, um die Quarantäne aufzuheben, und die App danach öffnen:
> ```bash
> xattr -dr com.apple.quarantine "/Applications/MicHop Receiver.app"
> ```

### 1. Der arbeitende Computer (Receiver)

1. Entpacke `MicHop-Receiver.zip`, ziehe „MicHop Receiver“ in den Ordner „Programme“ und öffne die App.
2. Aktiviere wie angezeigt die Berechtigung für **Bedienungshilfen**: Systemeinstellungen → Datenschutz & Sicherheit → Bedienungshilfen → „MicHop Receiver“ einschalten. Die App braucht diese Berechtigung, um für dich ⌘V zu drücken.
   - Wenn gefragt wird, ob das Programm eingehende Netzwerkverbindungen akzeptieren soll, klicke auf **Erlauben**.
3. Klicke im Dock auf das Symbol von „MicHop Receiver“. Im Hauptfenster siehst du:
   - **Verbindungsdaten**: die lokale Adresse dieses Macs, die Tailscale-Adresse und den Code, jeweils mit einer Kopieren-Schaltfläche daneben.
   - **Einrichtung**: Die Zeile „Bedienungshilfen-Zugriff“ sollte ein grünes Häkchen zeigen. Bei Einträgen mit gelber Warnung steht rechts direkt eine Schaltfläche, die das Problem behebt.
4. „Beim Anmelden öffnen“ ist standardmäßig aktiviert; bei Bedarf lässt sich das unter „Einstellungen… → Allgemein“ abschalten.

### 2. Der Computer, in den du sprichst (Sender)

1. Entpacke `MicHop.zip`, ziehe „MicHop“ in den Ordner „Programme“ und öffne die App.
2. Beim ersten Öffnen erscheint das Einstellungsfenster: Trage **Adresse** und **Code** des Receivers ein, klicke auf „Verbindung testen“ und, sobald das grüne „Verbunden – einsatzbereit“ erscheint, auf „Speichern“.
   - Im Fenster des Receivers lässt sich jeder Wert über die Kopieren-Schaltfläche neben Adresse bzw. Code einzeln kopieren.
   - Du kannst im Receiver auch auf „Alles kopieren“ klicken und den gesamten Text ins Feld „Empfängeradresse“ einfügen. Der Sender sucht sich die Adresse automatisch heraus (eine Tailscale-Adresse wird bevorzugt) und füllt auch den Code aus.
   - Wenn gefragt wird, ob das Suchen nach Geräten im lokalen Netzwerk erlaubt werden soll, klicke auf **Erlauben**.
3. Stelle sicher, dass das Systemdiktat aktiviert ist: Systemeinstellungen → Tastatur → Diktat.
4. Sobald oben im Hauptfenster „Mit Empfänger verbunden“ steht, kann es losgehen. Um Adresse oder Code später zu ändern, klicke im Hauptfenster im Bereich „Empfänger“ auf „Ändern …“ oder drücke ⌘,.

## Benutzung

1. Klicke zuerst in der Remote-Sitzung in ein Eingabefeld auf dem arbeitenden Computer, z. B. in Claude Code.
2. Drücke **⌃⌥Leertaste (Ctrl + Option + Leertaste)**. Unten auf dem Bildschirm erscheint ein kleines Fenster, und das Diktat startet automatisch. Falls es nicht von selbst startet, drücke einmal Fn.
3. Sprich und drücke danach **Return** – der Text erscheint auf dem anderen Computer.

| Taste | Funktion |
|---|---|
| Return / nochmals ⌃⌥Leertaste | Senden |
| Shift + Return | Zeilenumbruch |
| Esc | Abbrechen |

Oben im kleinen Fenster steht, an welchen Computer der Text geht. Links unten gibt es die Option „Nach dem Senden Return drücken“, die standardmäßig aktiviert ist – der Text wird dann direkt an Claude abgeschickt. Wenn du ihn erst prüfen und dann selbst abschicken möchtest, deaktiviere die Option (derselbe Schalter steht auch unter „Optionen“ im Hauptfenster).

Falls die Fernsteuerungssoftware diese Tastenkombination abfängt und das kleine Fenster nicht erscheint, klicke im Hauptfenster auf die große Schaltfläche „Sprechen“ oder im Menü des Menüleistensymbols auf „Sprechen“.

> **Die Tastenkürzel lassen sich ändern**: Klicke unter „Einstellungen… → Kurzbefehle“ auf die Schaltfläche und drücke dann die neue Tastenkombination. ⌃⌥Leertaste ist auf manchen Macs bereits durch den Systemkurzbefehl „Nächste Quelle im Eingabemenü auswählen“ belegt – ein Druck wechselt dann die Eingabequelle. In diesem Fall zeigt die App einen orangefarbenen Hinweis: Schalte diesen Eintrag unter Systemeinstellungen → Tastatur → Tastaturkurzbefehle → Eingabequellen aus oder lege in MicHop eine andere Tastenkombination fest.

## Zwei Übertragungsmodi

Umschalten im Hauptfenster unter „Senden als“ per Klick auf die Karte „Text“ oder „Audio“; auch im Menü des Menüleistensymbols lässt sich umschalten. **Standard ist „Text senden“.**

| | Text senden (Standard) | Audio senden |
|---|---|---|
| Wo wird erkannt? | Auf diesem Mac per Systemdiktat in Text umgewandelt | Auf dem anderen Computer, mit dessen eigenem Diktat oder dem Sprachmodus von Claude Code |
| Funktion von ⌃⌥Leertaste | Öffnet das kleine Diktatfenster | Startet oder stoppt „Immer an“ |
| ⌃⌥ halten | — | Sendet nur, solange die Tasten gehalten werden; Loslassen stoppt |
| Große Schaltfläche im Hauptfenster | „Sprechen“ | „Audio starten“ / „Audio stoppen“ |
| Was die Gegenseite braucht | Nur den Receiver | Den Receiver plus das integrierte virtuelle Audiogerät |

## Modus „Audio senden“

Diesen Modus verwendest du, wenn der arbeitende Computer **deine Stimme direkt hören** soll – etwa um dort den Sprachmodus von Claude Code oder das eigene Diktat zu nutzen.

```
MacBook-Mikrofon ──Audio──► Receiver ──► Virtuelles Audiogerät MicHop Audio ──► jede App auf diesem Mac, die „aufs Mikrofon hört“
```

**Vorbereitung auf dem Receiver-Computer:**

1. Installiere das integrierte virtuelle Audiogerät **MicHop Audio**: Wenn der Sender zum ersten Mal Audio schickt, zeigt der Receiver einen Hinweis – klicke auf „Installieren“. Alternativ klickst du im Receiver unter „Einstellungen… → Virtuelles Audiogerät“ auf „Installieren“. Das System fragt einmal nach dem Administratorpasswort; nach der Installation setzt der Systemton für ein, zwei Sekunden aus.
2. Stelle danach wie angezeigt das **Systemeingabegerät** auf MicHop Audio um (im Hauptfenster gibt es dafür unter „Einrichtung“ auch die Schaltfläche „Ändern“).
3. Lass das **Ausgabegerät** des Systems auf den Lautsprechern (oder dem Audiogerät der Fernsteuerungssoftware). MicHop Audio lässt sich gar nicht als Systemausgang auswählen, sodass kein Systemton hineingemischt wird.

> **Schon BlackHole installiert?** Das funktioniert weiterhin: Wähle unter „Einrichtung → Ausgabe auf“ das gewünschte Audiogerät. Möchtest du auf das integrierte umsteigen, klicke neben „Zum integrierten virtuellen Gerät wechseln“ auf „Installieren“. Achte bei BlackHole darauf, es nicht als Systemausgang zu wählen; ist es doch falsch eingestellt, erscheint unter „Einrichtung“ eine Warnung bei „Systemausgang“ – ein Klick auf „Zu Lautsprechern wechseln“ genügt.

> **Warum gibt es ein Echo?** Viele Fernsteuerungsprogramme (z. B. UU Remote) nehmen den Ton des ferngesteuerten Computers über Apples Bildschirmaufnahme-Framework auf. Dabei wird **der Ton aller Apps** auf diesem Computer aufgezeichnet – ganz gleich, auf welchem Audiogerät er abgespielt wird. Wenn MicHop deine Stimme in das virtuelle Audiogerät abspielt, wird sie also mit aufgenommen, an deinen Computer zurückgeschickt, über die Lautsprecher wiedergegeben und vom Mikrofon erneut aufgefangen.
>
> Deshalb ist beim Sender die **„Echounterdrückung“** standardmäßig aktiviert (im Hauptfenster unter „Optionen“ abschaltbar). Sie nutzt Apples Sprachverarbeitung – dieselbe wie bei FaceTime: Der zurückkommende Ton wird vom Mikrofonsignal abgezogen, andere Geräusche werden gedämpft, während du sprichst, und nebenbei wird Rauschen reduziert. Mit Kopfhörern funktioniert es am besten.

**Benutzung:**

Wähle im Hauptfenster unter „Senden als“ die Karte „Audio“. Der Sender verbindet sich dann mit dem Receiver (beim ersten Mal wird die Mikrofonberechtigung angefragt), „Verbindung“ wird blau und das Menüleistensymbol grün. Danach hast du jederzeit zwei Möglichkeiten zu sprechen:

1. **Immer an**: Drücke einmal **⌃⌥Leertaste** (oder klicke auf „Audio starten“) – das Mikrofon bleibt eingeschaltet; ein weiterer Druck stoppt.
2. **Halten zum Sprechen**: **Halte Ctrl + Option gedrückt, während du sprichst – loslassen stoppt.** Das Mikrofon ist nur eingeschaltet, solange du die Tasten hältst; im Hauptfenster wird „Audio“ rot, und auch das Menüleistensymbol wird rot. Nach dem Loslassen wird das Mikrofon ausgeschaltet, und die Lautstärke dieses Macs wird auch nicht abgesenkt. Beim ersten Mal wird die Berechtigung für Bedienungshilfen angefragt, mit der diese Tastenkombination erkannt wird; fehlt sie, weist dich der Bereich „Optionen“ im Hauptfenster darauf hin – klicke dann auf „Aktivieren …“.
3. Die gehaltene Tastenkombination wird von der Fernsteuerungssoftware auch an den arbeitenden Computer weitergegeben. Wenn du dort das Sprach-Tastenkürzel für Diktat oder Eingabemethode ebenfalls auf Ctrl + Option legst (siehe [Tipp unten](#tipp-die-fn-taste-kommt-bei-fernzugriff-nicht-an-also-tastenkürzel-ändern)), **erledigt ein einziger Druck beides: Audio senden und dort das Diktat starten**.
4. Beide Tastenkürzel lassen sich unter „Einstellungen… → Kurzbefehle“ ändern.

> Solange du die Tasten hältst, schaltet MicHop diesen Mac kurz stumm, damit der vom Fernzugriffsprogramm zurückgeschickte Ton nicht ins Mikrofon gelangt und ein Echo erzeugt; etwa 1 Sekunde nach dem Loslassen ist der Ton wieder da. (Der Modus „Immer an“ nutzt stattdessen Apples Echounterdrückung.)

### Tipp: Die Fn-Taste kommt bei Fernzugriff nicht an, also Tastenkürzel ändern

Wenn du über Fernsteuerungssoftware wie UU Remote, Sunlogin oder ToDesk verbunden bist, **kommt ein Druck auf die Fn-Taste deines Macs beim ferngesteuerten Computer nicht an**. Egal ob dort das Systemdiktat oder die Spracheingabe von WeChat Input Method genutzt wird – sie lässt sich so nicht auslösen. Dafür gibt es zwei Gründe: Die Fn-Taste wird zuerst von deinem eigenen Mac abgefangen (der dann sein eigenes Diktat startet); und selbst wenn die Fernsteuerungssoftware sie weiterreicht, ist sie auf der Gegenseite nur ein „simulierter Tastendruck“, den System und Eingabemethoden meist ignorieren.

Die Lösung: Ändere auf dem **ferngesteuerten Computer** (z. B. dem Mac mini) das Tastenkürzel für die Spracheingabe:

- **Systemdiktat**: Systemeinstellungen → Tastatur → Diktat → Kurzbefehl → „Anpassen“.
- **WeChat Input Method**: In den Einstellungen von WeChat Input Method das Tastenkürzel für die Spracheingabe ändern.

Empfohlen ist eine **Kombination aus Sondertasten**, etwa **linke Ctrl + Option** oder Ctrl mit einer anderen Sondertaste (Option, Shift, Command).

**Verwende nicht Ctrl mit einer Zahlen- oder Buchstabentaste** (z. B. Ctrl+D). Für die Spracheingabe hält man die Taste meist gedrückt, während man spricht – und hältst du eine Buchstaben- oder Zahlentaste gedrückt, wird das Zeichen immer wieder eingegeben, was sehr lästig ist. Eine reine Sondertasten-Kombination erzeugt beim Gedrückthalten keine Zeichen.

Dieser Trick wird zusammen mit dem Modus „Audio senden“ verwendet: Stelle das Eingabegerät des ferngesteuerten Computers auf MicHop Audio, halte in der Remote-Sitzung das neue Tastenkürzel gedrückt und sprich – schon diktiert der ferngesteuerte Computer direkt.

## Nicht im selben Netzwerk? Tailscale verwenden

1. Installiere [Tailscale](https://tailscale.com) auf beiden Computern und melde dich mit demselben Konto an.
2. Im Hauptfenster des Receivers steht unter „Verbindungsdaten“ in der Zeile „Tailscale“ die Adresse 100.x.x.x; trage sie in den Einstellungen des Senders ein. Du kannst auch den in Tailscale angezeigten Gerätenamen verwenden.
3. Wird „nicht gefunden“ angezeigt, prüfe zuerst, ob Tailscale auf dem Receiver-Computer verbunden ist, und klicke dann in dieser Zeile auf die Aktualisieren-Schaltfläche, um erneut zu suchen. Klappt es immer noch nicht, trage im Receiver unter „Einstellungen… → Tailscale → Manuelle Adresse“ die Adresse ein, die im Tailscale-Menü angezeigt wird.

Die Tailscale-Adresse funktioniert zu Hause wie unterwegs; sind beide Computer im selben lokalen Netzwerk, wird automatisch direkt verbunden.

## Sicherheit

- Jeder Receiver hat einen zufälligen 6-stelligen Code; Anfragen mit falschem Code werden grundsätzlich abgelehnt. Im Hauptfenster des Receivers kannst du in der Zeile „Code“ auf „Neu“ klicken (danach muss der Code im Sender neu eingetragen werden).
- Der Receiver lauscht auf den beiden TCP-Ports **8765** (Text) und **8766** (Audio); die Übertragung ist unverschlüsselt. Nutze ihn nur im Heimnetzwerk oder über Tailscale und gib diese Ports nicht ins öffentliche Internet frei.
- Beim Einfügen wird die Zwischenablage kurzzeitig mitbenutzt; nach etwa 1 Sekunde wird ihr ursprünglicher Inhalt wiederhergestellt.

## Häufige Fragen

- **Keine Verbindung**: Prüfe, ob beide Computer im selben Netzwerk sind oder beide mit Tailscale verbunden sind. Die lokale IP-Adresse kann sich ändern – am besten vergibst du dem Receiver im Router eine feste IP oder verwendest direkt die Tailscale-Adresse.
- **Meldung, dass die Bedienungshilfen-Berechtigung fehlt**: Nach einem Neukompilieren oder Update der App kann macOS die bisherige Berechtigung ungültig machen. Entferne zuerst den alten Eintrag aus der Liste der Bedienungshilfen und füge ihn dann neu hinzu.

## Automatische Updates

Beide Apps prüfen selbstständig auf GitHub, ob es neue Versionen gibt: einmal 30 Sekunden nach dem Start, danach alle 6 Stunden. Wird eine neue Version gefunden, wird sie automatisch heruntergeladen, ersetzt und neu gestartet.

- Die aktuelle Versionsnummer steht links unten im Hauptfenster; unter „Einstellungen… → Allgemein“ kannst du mit „Nach Updates suchen“ sofort prüfen.
- Wenn du keine automatische Installation möchtest, schalte unter „Einstellungen… → Allgemein“ die Option „Updates automatisch installieren“ aus. Bei einer neuen Version erscheint dann in den Einstellungen die Schaltfläche „Auf x.y.z aktualisieren“ (derselbe Eintrag auch im Menü der Menüleiste), und aktualisiert wird erst nach einem Klick darauf.
- Keine Unterbrechung während der Nutzung: Der Sender aktualisiert sich nicht, solange das Diktatfenster offen ist; der Receiver nicht während der Audioübertragung oder innerhalb von 1 Minute nach dem Empfang von Text.
- Sicherheit: Eine neue Version muss mit **demselben Zertifikat** signiert sein wie die aktuelle, sonst wird die Installation verweigert.
- Nach dem Update bleiben Berechtigungen wie Bedienungshilfen und Mikrofon erhalten und müssen nicht neu erteilt werden.

## License

[MIT](LICENSE)
