<p align="center"><img src="assets/banner.png" alt="传声筒 MicHop" width="760"></p>
<p align="center"><a href="README.md">简体中文</a> · <a href="README.zh-Hant.md">繁體中文</a> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.es.md">Español</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pt.md">Português</a> · <a href="README.ru.md">Русский</a></p>

<p align="center">
  <b>Presta el micrófono de este Mac a otro Mac.</b><br>
  Hablas en este y el otro se comporta como si tuviera un micrófono conectado; funciona por red local o por Tailscale.<br>
  <sub>Lend your Mac's microphone to another Mac — live, over LAN or Tailscale.</sub>
</p>

---

## ¿Para qué sirve?

Normalmente trabajo en un MacBook y me conecto a un Mac mini con un programa de escritorio remoto (UU Remote, Sunlogin, ToDesk, etc.) para hacer cosas allí: que Claude Code escriba código, editar vídeos, mantener sitios web…

El problema es que **el Mac mini no tiene micrófono y el programa de escritorio remoto tampoco transmite el del MacBook**, así que dentro del escritorio remoto no se puede usar la entrada de voz.

MicHop resuelve justo eso. Se instala una app en cada equipo:

- **El equipo en el que hablas** (por ejemplo, el MacBook): instala «MicHop»
- **El equipo en el que trabajas** (por ejemplo, el Mac mini): instala «MicHop Receiver»

```
MacBook (hablas)                             Mac mini (trabajas)

Micrófono ── 🔊 audio ──────────────►  Micrófono virtual (MicHop Audio integrado)
                                      → Dictado / WeChat Input Method / modo de voz de Claude Code

              por red local o por Tailscale
```

El sonido del micrófono del MacBook llega en tiempo real al Mac mini y se convierte en su micrófono. Cualquier app del Mac mini que necesite micrófono puede usarlo: el Dictado del sistema, la entrada de voz de WeChat Input Method, el modo de voz de Claude Code, etc.

- El receptor incluye el dispositivo de audio virtual **MicHop Audio**: la primera vez que lo abres te propone instalarlo (pide la contraseña de administrador una sola vez) y no hay que descargar nada más. Si ya tenías [BlackHole](https://github.com/ExistentialAudio/BlackHole) instalado, puedes seguir usándolo.
- Dos formas de hablar, disponibles en todo momento: pulsa **⌃⌥M** una vez para enviar sin parar y otra vez para detener; o **mantén pulsado ⌃⌥** mientras hablas y suelta para parar.
- Incluye cancelación de eco, así que no hay eco aunque estés conectado con un programa de escritorio remoto.
- La tecla Fn no pasa a través del escritorio remoto: acuérdate de cambiar en el Mac mini el atajo de la entrada de voz por una combinación de teclas modificadoras, como Ctrl + Option. [Más detalles abajo](#truco-en-conexiones-remotas-la-tecla-fn-no-llega-cambia-el-atajo).

### Cómo conectar los dos equipos

- **En la misma red local**: basta con introducir la IP local del Mac mini.
- **Si no están juntos**: instala [Tailscale](https://tailscale.com) en los dos para crear una red virtual e introduce la **IP de Tailscale** del Mac mini (empieza por 100). Funciona igual en casa que fuera.
- La ventana del receptor muestra la IP local, la IP de Tailscale y el código, cada uno con su botón de copiar.

### Otras características

- **Sin servicios en la nube**: el audio viaja directamente entre tus dos equipos, por la red local o por el túnel cifrado de Tailscale.
- **Independiente del escritorio remoto**: funciona con UU Remote, Sunlogin, ToDesk o Compartir pantalla.
- **Actualizaciones automáticas**: se actualiza solo cuando hay una versión nueva y no tienes que volver a conceder los permisos.
- **Varios idiomas**: la interfaz está disponible en 简体中文, 繁體中文, English, 日本語, 한국어, Español, Français, Deutsch, Português y Русский. El idioma predeterminado es el chino; cámbialo en «Ajustes… → General → Idioma / Language».

## Descarga e instalación

Descarga los archivos desde [Releases](../../releases/latest):

| Archivo | En qué equipo se instala | Icono de la barra de menús |
|---|---|---|
| `MicHop.zip` (MicHop) | El equipo en el que hablas, por ejemplo el MacBook | Dos micrófonos, igual que el icono de la app |
| `MicHop-Receiver.zip` (MicHop Receiver) | El equipo en el que trabajas, por ejemplo el Mac mini | Igual que el anterior |

El color del icono de la barra de menús indica el estado: **gris** = sin conexión, **verde** = conectado, **rojo** = enviando audio.

> **Las dos apps giran en torno a su ventana principal**: al hacer clic en el icono del Dock se abre la ventana principal, que muestra arriba dos bloques de estado: «Conexión» (gris / azul) y «Audio» (gris / rojo). Las acciones habituales están en la ventana; los atajos, el idioma, las actualizaciones automáticas y demás están en «Ajustes…» (⌘,). El icono de la barra de menús y el menú contextual del icono del Dock solo conservan las opciones más usadas. Si la cámara (la muesca) del MacBook tapa el icono de la barra de menús, usa el icono del Dock.

Requiere macOS 13 o posterior; funciona tanto en Mac con chip de Apple como con Intel.

> **Si al abrirla por primera vez aparece «no se puede verificar el desarrollador»**: es porque la app no ha pasado por la notarización de pago de Apple. Abre Ajustes del Sistema → Privacidad y seguridad y, al final de la página, haz clic en «Abrir igualmente». También puedes ejecutar este comando en Terminal para quitar la cuarentena y después abrirla:
> ```bash
> xattr -dr com.apple.quarantine "/Applications/MicHop Receiver.app"
> ```

### 1. El equipo en el que trabajas (receptor)

1. Descomprime `MicHop-Receiver.zip`, arrastra «MicHop Receiver» a la carpeta Aplicaciones y ábrelo.
   - Si aparece un aviso preguntando si quieres permitir conexiones de red entrantes, haz clic en **Permitir**.
2. La primera vez te propondrá instalar el dispositivo de audio virtual integrado **MicHop Audio**: haz clic en «Instalar» e introduce la contraseña de administrador. Durante la instalación, el audio del sistema se corta un par de segundos. También puedes instalarlo más adelante en «Ajustes… → Dispositivo de audio virtual».
3. Cuando termine, sigue las indicaciones para poner **MicHop Audio como dispositivo de entrada del sistema** (en «Preparación», en la ventana principal, también tienes el botón «Cambiar»). Deja como **salida** del sistema los altavoces (o el dispositivo de audio del programa de escritorio remoto). MicHop Audio no se puede elegir como salida del sistema, así que el sonido del sistema no se mezcla.
4. En la ventana principal verás:
   - **Datos de conexión**: la dirección local de este Mac, la dirección de Tailscale y el código, cada uno con su botón de copiar.
   - **Preparación**: cuando el dispositivo de audio virtual y la entrada del sistema tienen una marca verde, todo está listo. Si algún elemento muestra un aviso amarillo, a su derecha aparece directamente un botón para solucionarlo.
5. De forma predeterminada se abre al iniciar sesión; si no lo quieres, desactívalo en «Ajustes… → General».

> **¿Ya tenías BlackHole?** Sigue funcionando: elige el dispositivo que prefieras en «Preparación → Reproducir en». Si quieres pasarte al integrado, haz clic en «Instalar», junto a «Puedes usar el dispositivo virtual integrado». Con BlackHole, ten cuidado de no seleccionarlo como salida del sistema; si te equivocas, en «Preparación» aparecerá el aviso «Salida del sistema» y bastará con hacer clic en «Cambiar a altavoces».

### 2. El equipo en el que hablas (emisor)

1. Descomprime `MicHop.zip`, arrastra «MicHop» a la carpeta Aplicaciones y ábrelo.
2. La primera vez se abre la ventana de ajustes: introduce la **dirección** y el **código** del receptor, haz clic en «Probar conexión» y, cuando veas en verde «Conectado: listo para usar», haz clic en «Guardar».
   - En la ventana del receptor, los botones de copiar junto a la dirección y al código copian cada dato por separado.
   - También puedes hacer clic en «Copiar todo» en el receptor y pegar el bloque entero en el campo «Dirección». El emisor extrae la dirección automáticamente (si hay una dirección de Tailscale, la usa con prioridad) y rellena también el código.
   - Si aparece un aviso para permitir que la app busque dispositivos en tu red local, haz clic en **Permitir**.
3. La primera vez pedirá permiso para usar el **micrófono**: permítelo. También pedirá el permiso de **Accesibilidad** (sirve para detectar cuándo mantienes pulsado ⌃⌥); sigue las indicaciones: Ajustes del Sistema → Privacidad y seguridad → Accesibilidad → activa «MicHop».
4. Al abrir la app se conecta al receptor. Cuando «Conexión» se ponga azul en la ventana principal y el icono de la barra de menús se ponga verde, ya puedes usarla. Para cambiar más adelante la dirección o el código, haz clic en «Cambiar…» en el apartado «Receptor» de la ventana principal, o pulsa ⌘,.

## Cómo se usa

Primero, en el escritorio remoto, haz clic en el lugar del equipo de trabajo donde quieras usar la voz: el modo de voz de Claude Code, el Dictado del sistema o el método de entrada. A partir de ahí tienes dos formas de hablar, siempre disponibles:

1. **Envío continuo**: pulsa **⌃⌥M (Ctrl + Option + M)** una vez, o haz clic en «Iniciar audio» en la ventana principal, y el micrófono queda abierto; vuelve a pulsar para detenerlo.
2. **Mantener para hablar**: **mantén pulsado Ctrl + Option mientras hablas y suelta para parar**. El micrófono solo se abre mientras mantienes las teclas.

Mientras se envía audio, «Audio» en la ventana principal y el icono de la barra de menús se ponen en rojo; en el receptor, «Audio» también se pone en rojo.

- El programa de escritorio remoto también transmite esa combinación de teclas al equipo de trabajo. Si allí configuras también Ctrl + Option como atajo de voz del Dictado o del método de entrada (consulta [el truco de abajo](#truco-en-conexiones-remotas-la-tecla-fn-no-llega-cambia-el-atajo)), **con una sola pulsación envías el audio y a la vez empieza el dictado al otro lado**.
- Mientras mantienes las teclas para hablar, MicHop silencia temporalmente este Mac, para que el sonido del otro equipo no vuelva a través del escritorio remoto, entre otra vez por el micrófono y forme eco; el sonido vuelve solo aproximadamente 1 segundo después de soltar. (El envío continuo usa la cancelación de eco de Apple).

> **Puedes cambiar los atajos**: en «Ajustes… → Atajos», haz clic en el botón y pulsa la nueva combinación. «Empezar a hablar» admite cualquier combinación que incluya ⌃, ⌥ o ⌘; «Mantener para hablar» necesita una combinación de dos o más de ⌃ ⌥ ⇧ ⌘. Si la combinación elegida ya la usa el sistema (por ejemplo, en muchos Mac ⌃⌥Espacio es «Seleccionar la siguiente fuente del menú Entrada»), la app muestra un aviso naranja: desactiva ese atajo en Ajustes del Sistema → Teclado → Atajos de teclado o elige otra combinación.

> **¿Por qué hay eco?** Muchos programas de escritorio remoto (por ejemplo, UU Remote) capturan el sonido del equipo controlado con el framework de grabación de pantalla de Apple, que graba **el sonido de todas las apps** de ese equipo, sin importar en qué dispositivo de audio se reproduzca. Cuando MicHop reproduce tu voz en el dispositivo de audio virtual, también se graba, vuelve a tu equipo, sale por los altavoces y el micrófono la vuelve a captar.
>
> Por eso el emisor tiene activada de forma predeterminada la **cancelación de eco** (puedes desactivarla en «Opciones», en la ventana principal). Usa el procesamiento de voz de Apple, el mismo que usa FaceTime: resta del micrófono el sonido que vuelve, baja los demás sonidos mientras hablas y, de paso, reduce el ruido. Con auriculares funciona mejor.

### Truco: en conexiones remotas la tecla Fn no llega, cambia el atajo

Cuando te conectas con programas de escritorio remoto como UU Remote, Sunlogin o ToDesk, **la tecla Fn que pulsas en tu equipo no llega al equipo controlado**. No activa nada allí, ni el Dictado del sistema ni la entrada de voz de WeChat Input Method. Hay dos motivos: tu propio equipo intercepta primero la tecla Fn (y empieza a dictar en local), y aunque el programa de escritorio remoto la transmitiera, en el equipo controlado solo sería una «pulsación simulada», que el sistema y los métodos de entrada no suelen reconocer.

La solución: cambia el atajo de la entrada de voz en el **equipo controlado** (por ejemplo, el Mac mini):

- **Dictado del sistema**: Ajustes del Sistema → Teclado → Dictado → Atajo → «Personalizar».
- **WeChat Input Method**: cambia el atajo de la entrada de voz en los ajustes de WeChat Input Method.

Se recomienda una **combinación de teclas modificadoras**, como **Ctrl + Option de la izquierda**, o Ctrl con otra tecla modificadora (Option, Shift, Command).

**No uses Ctrl con una tecla de número o de letra** (por ejemplo, Ctrl+D). La entrada de voz suele requerir mantener la tecla pulsada mientras hablas, y si mantienes una letra o un número, ese carácter se escribe una y otra vez, lo que resulta muy incómodo. Una combinación solo de teclas modificadoras no escribe ningún carácter aunque la mantengas.

Pon MicHop Audio como dispositivo de entrada del equipo controlado, mantén pulsado el nuevo atajo en el escritorio remoto mientras hablas, y el equipo controlado dictará directamente.

## ¿No están en la misma red? Usa Tailscale

1. Instala [Tailscale](https://tailscale.com) en los dos equipos e inicia sesión con la misma cuenta.
2. En la ventana principal del receptor, la fila «Tailscale» de «Datos de conexión» muestra 100.x.x.x: introduce esa dirección en los ajustes del emisor. También vale el nombre del equipo que muestra Tailscale.
3. Si aparece «No encontrado», comprueba primero que Tailscale está conectado en el equipo receptor y luego haz clic en el botón de actualizar de esa fila para volver a detectarlo. Si aun así no lo detecta, introduce la dirección que aparece en el menú de Tailscale en «Ajustes… → Tailscale → Dirección manual» del receptor.

La dirección de Tailscale funciona tanto en casa como fuera, y cuando los dos equipos están en la misma red local se conecta directamente de forma automática.

## Seguridad

- Cada receptor tiene un código aleatorio de 6 dígitos y rechaza cualquier conexión con un código incorrecto. Puedes cambiarlo haciendo clic en «Nuevo» en la fila «Código» de la ventana principal del receptor (después tendrás que volver a introducirlo en el emisor).
- El receptor solo escucha en un puerto: TCP **8766** (audio). Por ahora la transmisión no está cifrada. Úsalo solo en tu red doméstica o dentro de Tailscale y no expongas ese puerto a internet.

## Preguntas frecuentes

- **No se conecta**: comprueba que los dos equipos están en la misma red o que ambos están conectados a Tailscale. La IP local puede cambiar, así que conviene asignar una IP fija al receptor en el router o usar directamente la dirección de Tailscale.
- **El receptor dice que no puede abrir el puerto**: normalmente es porque un receptor anterior no se cerró del todo y sigue ocupando el puerto; el receptor lo cierra automáticamente. Si lo ocupa otro programa, el aviso indica su nombre, y el receptor se iniciará solo en cuanto quede libre.
- **Mantener pulsado ⌃⌥ no hace nada**: el emisor necesita el permiso de **Accesibilidad**. Después de recompilar o actualizar la app, macOS a veces invalida el permiso anterior: elimina primero la entrada antigua de la lista de Accesibilidad y vuelve a añadirla.

## Actualizaciones automáticas

Las dos apps buscan versiones nuevas en GitHub por su cuenta: una vez 30 segundos después de abrirse y luego cada 6 horas. Si encuentran una versión nueva, la descargan, la sustituyen y se vuelven a abrir automáticamente.

- La versión actual se ve en la esquina inferior izquierda de la ventana principal; en «Ajustes… → General» puedes hacer clic en «Buscar actualizaciones» para comprobarlo al momento.
- Si no quieres que se instalen solas, desactiva «Instalar actualizaciones automáticamente» en «Ajustes… → General». A partir de entonces, cuando haya una versión nueva aparecerá el botón «Actualizar a x.y.z» en los ajustes, y la misma opción en el menú de la barra de menús; solo se actualiza cuando haces clic.
- No te interrumpe mientras la usas: no se actualiza mientras se está enviando audio.
- Seguridad: la versión nueva debe estar firmada con **el mismo certificado** que la actual; si no, se rechaza la instalación.
- Tras actualizar se conservan los permisos de Accesibilidad, Micrófono, etc., y no hay que volver a concederlos.

## License

[MIT](LICENSE)
