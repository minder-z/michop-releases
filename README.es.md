<p align="center"><img src="assets/banner.png" alt="传声筒 MicHop" width="760"></p>
<p align="center"><a href="README.md">简体中文</a> · <a href="README.zh-Hant.md">繁體中文</a> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.es.md">Español</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pt.md">Português</a> · <a href="README.ru.md">Русский</a></p>

<p align="center">
  <b>Presta el micrófono de este Mac a otro Mac.</b><br>
  Puedes enviar audio o texto, por red local o por Tailscale.<br>
  <sub>Lend your Mac's microphone to another Mac — as live audio or as text, over LAN or Tailscale.</sub>
</p>

---

## ¿Para qué sirve?

Normalmente trabajo en un MacBook y uso software de escritorio remoto (UU Remote, Sunlogin, ToDesk, etc.) para conectarme a un Mac mini y trabajar allí: por ejemplo, que Claude Code escriba código, editar vídeos o mantener sitios web.

El problema: **el Mac mini no tiene micrófono, y el software de escritorio remoto no transmite el micrófono del MacBook**, así que no puedes usar la entrada de voz dentro del escritorio remoto.

MicHop resuelve justo eso. Se instala una app en cada ordenador:

- **El ordenador en el que hablas** (por ejemplo, el MacBook): instala «MicHop»
- **El ordenador que hace el trabajo** (por ejemplo, el Mac mini): instala «MicHop Receiver»

### Dos formas de enviar, intercambiables en cualquier momento desde la ventana principal

```
MacBook (hablas)                             Mac mini (trabaja)

Micrófono ── 🔊 Enviar audio ─────────►  Micrófono virtual (MicHop Audio integrado)
                                      → Dictado / WeChat Input Method / modo de voz de Claude Code

Dictado ──── 📝 Enviar texto ─────────►  Se pega donde está el cursor, con Retorno automático opcional

              por red local o Tailscale
```

**🔊 Enviar audio: el Mac mini te «oye» directamente**

El sonido del micrófono del MacBook se transmite en tiempo real al Mac mini y se convierte en el micrófono del Mac mini. Cualquier app del Mac mini que necesite micrófono puede usarlo, como el Dictado del sistema, la entrada de voz de WeChat Input Method o el modo de voz de Claude Code.

- El Receiver incluye su propio dispositivo de audio virtual, **MicHop Audio**: la primera vez que envíes audio te pedirá instalarlo (hay que introducir una vez la contraseña de administrador), sin descargar nada más. Si ya tenías instalado [BlackHole](https://github.com/ExistentialAudio/BlackHole), puedes seguir usándolo.
- Incluye cancelación de eco, así que no hay eco aunque estés conectado mediante software de escritorio remoto.
- La tecla Fn no llega a través del software de escritorio remoto, así que cambia el atajo de la entrada de voz a una combinación de teclas modificadoras, como Ctrl + Opción. [Más detalles abajo](#truco-la-tecla-fn-no-llega-por-conexión-remota-cambia-el-atajo).

**📝 Enviar texto: se reconoce en el MacBook y se envían las palabras**

En el MacBook, pulsa ⌃⌥Espacio (Ctrl + Opción + Espacio) y usa el Dictado del sistema para convertir lo que dices en texto. El texto se envía al Mac mini y se pega automáticamente donde está el cursor; incluso puede pulsar Retorno automáticamente para enviárselo directamente a Claude.

- No hace falta instalar ningún controlador de audio ni configurar el audio en el Mac mini: es la opción más sencilla y estable.
- Es el modo predeterminado de la app.

| | 🔊 Enviar audio | 📝 Enviar texto |
|---|---|---|
| Dónde se reconoce la voz | Mac mini (con su propio dictado o método de entrada) | MacBook (con el Dictado del sistema) |
| Qué necesita el Mac mini | Receiver + su dispositivo de audio virtual integrado (se instala la primera vez) | Solo el Receiver |
| Ideal para | Usar el método de entrada, el dictado o el modo de voz de Claude del Mac mini | Simplemente convertir lo que dices en texto escrito |

### Cómo se conectan los dos ordenadores

- **En la misma red local**: basta con introducir la IP local del Mac mini.
- **En lugares distintos**: instala [Tailscale](https://tailscale.com) en ambos ordenadores para formar una red local virtual e introduce la **IP de Tailscale** del Mac mini (empieza por 100). **Tanto el audio como el texto pueden ir por Tailscale**, así que funciona igual en casa que fuera.
- La ventana del Receiver muestra la IP local, la IP de Tailscale y el código, cada uno con su propio botón de copiar.

### Otras características

- **Sin pasar por ningún servicio en la nube**: el audio y el texto viajan directamente entre tus dos ordenadores, por la red local o por el túnel cifrado de Tailscale.
- **Independiente del software de escritorio remoto**: funciona junto con UU Remote, Sunlogin, ToDesk y Compartir Pantalla.
- **Actualizaciones automáticas**: se actualiza sola cuando hay una versión nueva, sin tener que volver a conceder permisos.
- **Multilingüe**: la interfaz está disponible en 简体中文, 繁體中文, English, 日本語, 한국어, Español, Français, Deutsch, Português y Русский. El idioma predeterminado es el chino; se cambia en «Ajustes… → General → Idioma / Language».

## Descarga e instalación

Descárgalo desde [Releases](../../releases/latest):

| Archivo | En qué ordenador | Icono en la barra de menús |
|---|---|---|
| `MicHop.zip` (MicHop) | El ordenador en el que hablas, p. ej. MacBook | Un cuadrado redondeado, igual que el icono de la app |
| `MicHop-Receiver.zip` (MicHop Receiver) | El ordenador que hace el trabajo, p. ej. Mac mini | Igual que el anterior |

El color del icono de la barra de menús indica el estado: **gris** = sin conexión, **verde** = conectado, **rojo** = enviando (hablando / recibiendo audio).

> **Ambas apps giran en torno a su ventana principal**: haz clic en el icono del Dock para abrirla. En la parte superior, el estado se muestra en dos bloques: «Conexión» (gris / azul) y «Audio» (gris / rojo); las acciones habituales están en la propia ventana; el idioma, las actualizaciones automáticas y demás están en «Ajustes…» (⌘,). El icono de la barra de menús y el clic derecho en el icono del Dock solo conservan las opciones más usadas. Si la cámara (notch) del MacBook tapa el icono de la barra de menús, usa el icono del Dock.

Requiere macOS 13 o posterior; funciona tanto en Mac con chip de Apple como con Intel.

> **Al abrirla por primera vez aparece «No se puede verificar el desarrollador»**: se debe a que la app no ha pasado por la notarización de pago de Apple. Abre Ajustes del Sistema → Privacidad y seguridad y haz clic en «Abrir igualmente» en la parte inferior de la página. También puedes ejecutar este comando en Terminal para quitar la cuarentena y luego abrirla:
> ```bash
> xattr -dr com.apple.quarantine "/Applications/MicHop Receiver.app"
> ```

### 1. El ordenador que trabaja (Receiver)

1. Descomprime `MicHop-Receiver.zip`, arrastra «MicHop Receiver» a «Aplicaciones» y ábrela.
2. Sigue las indicaciones para activar el permiso de **Accesibilidad**: Ajustes del Sistema → Privacidad y seguridad → Accesibilidad → activa «MicHop Receiver». Necesita este permiso para pulsar ⌘V por ti.
   - Si aparece «¿Quieres que la aplicación acepte conexiones de red entrantes?», haz clic en **Permitir**.
3. Haz clic en el icono de «MicHop Receiver» en el Dock; en la ventana principal verás:
   - **Datos de conexión**: la dirección local de este Mac, la dirección de Tailscale y el código, cada uno con su botón de copiar.
   - **Preparación**: la fila «Permiso de accesibilidad» debería mostrar una marca verde. Si alguna fila tiene un aviso amarillo, a su derecha aparece directamente un botón para solucionarlo.
4. «Abrir al iniciar sesión» está activado por defecto; si no lo necesitas, puedes desactivarlo en «Ajustes… → General».

### 2. El ordenador en el que hablas (emisor)

1. Descomprime `MicHop.zip`, arrastra «MicHop» a «Aplicaciones» y ábrela.
2. La primera vez se abre la ventana de ajustes: introduce la **dirección** y el **código** del Receiver, haz clic en «Probar conexión» y, cuando veas en verde «Conectado: listo para usar», haz clic en «Guardar».
   - En la ventana del Receiver, los botones de copiar junto a la dirección y al código permiten copiar cada dato por separado.
   - También puedes hacer clic en «Copiar todo» en el Receiver y pegarlo entero en el campo «Dirección del receptor». El emisor extrae la dirección automáticamente (si hay dirección de Tailscale, la usa con prioridad) y también rellena el código.
   - Si aparece «Permitir buscar dispositivos en la red local», haz clic en **Permitir**.
3. Comprueba que el Dictado del sistema esté activado: Ajustes del Sistema → Teclado → Dictado.
4. Cuando la parte superior de la ventana principal muestre «Conectado al receptor», ya puedes usarlo. Si más adelante quieres cambiar la dirección o el código, haz clic en «Cambiar…» en la sección «Receptor» de la ventana principal, o pulsa ⌘,.

## Cómo se usa

1. Primero, en el escritorio remoto, haz clic en un campo de texto del ordenador que trabaja, por ejemplo en Claude Code.
2. Pulsa **⌃⌥Espacio (Ctrl + Opción + Espacio)**: aparecerá una pequeña ventana en la parte inferior de la pantalla y el dictado empezará automáticamente. Si el dictado no empieza solo, pulsa Fn una vez.
3. Habla y, al terminar, pulsa **Retorno**: el texto aparecerá en el otro ordenador.

| Tecla | Función |
|---|---|
| Retorno / ⌃⌥Espacio otra vez | Enviar |
| Mayúsculas + Retorno | Salto de línea |
| Esc | Cancelar |

En la parte superior de la pequeña ventana se indica a qué ordenador se enviará el texto. Abajo a la izquierda está la opción «Pulsar Intro tras enviar», marcada por defecto, de modo que el texto se envía directamente a Claude. Si prefieres revisarlo antes de enviarlo a mano, desmárcala (el mismo interruptor está también en «Opciones» de la ventana principal).

Si el software de escritorio remoto se queda con esta combinación y la ventanita no aparece, haz clic en el botón grande «Hablar» de la ventana principal, o en el icono de la barra de menús → «Hablar».

> **Los atajos se pueden cambiar**: en «Ajustes… → Atajos», haz clic en el botón y pulsa la nueva combinación. En algunos Mac, ⌃⌥Espacio ya lo usa el atajo del sistema «Seleccionar la siguiente fuente del menú Entrada», y al pulsarlo cambia la fuente de entrada. En ese caso la app muestra un aviso naranja: desactiva esa opción en Ajustes del Sistema → Teclado → Atajos de teclado → Fuentes de entrada, o elige otra combinación en MicHop.

## Dos modos de envío

Se cambia en la sección «Enviar como» de la ventana principal, haciendo clic en la tarjeta «Texto» o «Audio»; también desde el menú del icono de la barra de menús. **El modo predeterminado es Enviar texto.**

| | Enviar texto (predeterminado) | Enviar audio |
|---|---|---|
| Dónde se reconoce | En este Mac, con el Dictado del sistema | En el otro ordenador, con su propio dictado o el modo de voz de Claude Code |
| Qué hace ⌃⌥Espacio | Abre la ventanita de dictado | Inicia o detiene el modo «Siempre activo» |
| Mantener ⌃⌥ | — | Envía mientras lo mantienes y para al soltar |
| Botón grande de la ventana principal | «Hablar» | «Iniciar audio» / «Detener audio» |
| Qué necesita el otro Mac | Solo el Receiver | El Receiver y su dispositivo de audio virtual integrado |

## Modo Enviar audio

Usa este modo cuando quieras que el ordenador que trabaja **oiga tu voz directamente**, por ejemplo para usar el modo de voz de Claude Code en ese ordenador o su propio dictado.

```
Micrófono del MacBook ──audio──► Receiver ──► Dispositivo de audio virtual MicHop Audio ──► cualquier app de ese Mac que «escuche el micrófono»
```

**Antes, en el ordenador del Receiver:**

1. Instala el dispositivo de audio virtual integrado, **MicHop Audio**: la primera vez que el emisor envíe audio, el Receiver mostrará un aviso; haz clic en «Instalar». También puedes hacer clic en «Instalar» en «Ajustes… → Dispositivo de audio virtual» del Receiver. El sistema pedirá una vez la contraseña de administrador y, al terminar, el sonido del sistema se cortará un par de segundos.
2. Cuando esté instalado, sigue el aviso para poner la **entrada del sistema** en MicHop Audio (en «Preparación», en la ventana principal, también tienes el botón «Cambiar»).
3. Deja el dispositivo de **salida** del sistema en los altavoces (o en el dispositivo de audio del software de escritorio remoto). MicHop Audio no se puede elegir como salida del sistema, así que el sonido del sistema no se mezcla con tu voz.

> **¿Ya tenías BlackHole?** Sigue funcionando: elige el dispositivo que quieras en «Preparación → Reproducir en». Si quieres pasarte al integrado, haz clic en «Instalar» junto a «Puedes usar el dispositivo virtual integrado». Si usas BlackHole, ten cuidado de no elegirlo como salida del sistema; si te equivocas, aparecerá un aviso de «Salida del sistema» en «Preparación»: basta con hacer clic en «Cambiar a altavoces».

> **¿Por qué hay eco?** Muchas apps de escritorio remoto (UU Remote, por ejemplo) capturan el sonido del ordenador remoto con el framework de grabación de pantalla de Apple, que graba **el sonido de todas las apps** de ese ordenador, sin importar en qué dispositivo de audio se reproduzca. Cuando MicHop reproduce tu voz en el dispositivo de audio virtual, también se graba, vuelve a tu ordenador, suena por los altavoces y el micrófono la vuelve a captar.
>
> Por eso el emisor tiene la **«Cancelación de eco»** activada por defecto (se puede desactivar en «Opciones» de la ventana principal). Usa el procesamiento de voz de Apple, el mismo que usa FaceTime: resta del micrófono el sonido que vuelve, baja los demás sonidos mientras hablas y, de paso, reduce el ruido. Con auriculares funciona mejor.

**Cómo se usa:**

En la sección «Enviar como» de la ventana principal, elige «Audio»: el emisor se conectará al Receiver (la primera vez pedirá permiso para usar el micrófono), «Conexión» se pondrá azul y el icono de la barra de menús, verde. A partir de ahí tienes dos formas de hablar, disponibles en todo momento:

1. **Siempre activo**: pulsa una vez **⌃⌥Espacio** (o haz clic en «Iniciar audio») y el micrófono queda encendido; vuelve a pulsarlo para detenerlo.
2. **Mantener para hablar**: **mantén pulsado Ctrl + Opción mientras hablas y suelta para parar**. El micrófono solo se activa mientras mantienes pulsadas las teclas: «Audio» se pone rojo en la ventana principal y el icono de la barra de menús también; al soltar, el micrófono se apaga y el volumen de este Mac tampoco se baja. La primera vez pedirá el permiso de Accesibilidad, que usa para detectar esta combinación de teclas; si no está concedido, «Opciones» de la ventana principal te avisará: haz clic en «Activar…».
3. El software de escritorio remoto también transmite la combinación que mantienes pulsada al ordenador que trabaja. Si en ese ordenador configuras también Ctrl + Opción como atajo de voz del dictado o del método de entrada (consulta [el truco de abajo](#truco-la-tecla-fn-no-llega-por-conexión-remota-cambia-el-atajo)), **con una sola pulsación envías el audio y a la vez haces que allí empiece el dictado**.
4. Ambos atajos se pueden cambiar en «Ajustes… → Atajos».

> Mientras mantienes las teclas, MicHop silencia temporalmente este Mac para que el sonido que devuelve la app de escritorio remoto no llegue al micrófono y cause eco; el sonido vuelve aproximadamente 1 segundo después de soltar. (El modo Siempre activo usa la cancelación de eco de Apple).

### Truco: la tecla Fn no llega por conexión remota, cambia el atajo

Cuando te conectas con software de escritorio remoto como UU Remote, Sunlogin o ToDesk, **pulsar Fn en tu Mac no llega al ordenador remoto**. Da igual que en el remoto uses el Dictado del sistema o la entrada de voz de WeChat Input Method: no se activa. Hay dos motivos: tu Mac intercepta primero la tecla Fn (y empieza su propio dictado); y aunque el software remoto la transmitiera, en el ordenador remoto es solo una «pulsación simulada», que el sistema y los métodos de entrada normalmente no reconocen.

La solución: en el **ordenador remoto** (por ejemplo, el Mac mini), cambia el atajo de la entrada de voz:

- **Dictado del sistema**: Ajustes del Sistema → Teclado → Dictado → Función rápida → «Personalizar».
- **WeChat Input Method**: cambia el atajo de entrada de voz en los ajustes de WeChat Input Method.

Se recomienda una **combinación de teclas modificadoras**, como **Ctrl izquierda + Opción**, o Ctrl con otra tecla modificadora (Opción, Mayúsculas, Comando).

**No uses Ctrl con una tecla de número o letra** (como Ctrl+D). La entrada de voz suele requerir mantener la tecla pulsada mientras hablas, y al mantener pulsada una letra o un número ese carácter se repite una y otra vez, lo cual es muy incómodo. Una combinación solo de modificadoras no escribe ningún carácter al mantenerla pulsada.

Este truco se combina con el modo «Enviar audio»: configura MicHop Audio como dispositivo de entrada del ordenador remoto, mantén pulsado el nuevo atajo en el escritorio remoto mientras hablas y el ordenador remoto podrá dictar directamente.

## ¿No estáis en la misma red? Usa Tailscale

1. Instala [Tailscale](https://tailscale.com) en ambos ordenadores e inicia sesión con la misma cuenta.
2. En la ventana principal del Receiver, la fila «Tailscale» de «Datos de conexión» mostrará 100.x.x.x; introdúcela en los ajustes del emisor. También puedes usar el nombre de la máquina que aparece en Tailscale.
3. Si aparece «no detectada», comprueba primero que Tailscale esté conectado en el ordenador del Receiver y haz clic en el botón de actualizar de esa fila para volver a detectarla. Si aun así no se detecta, ve a «Ajustes… → Tailscale → Dirección manual» en el Receiver y escribe la dirección que muestra el menú de Tailscale.

La dirección de Tailscale funciona tanto en casa como fuera; cuando ambos ordenadores están en la misma red local, se conecta directamente de forma automática.

## Seguridad

- Cada Receiver tiene un código aleatorio de 6 dígitos, y se rechaza cualquier solicitud con un código incorrecto. Puedes cambiarlo haciendo clic en «Nuevo» en la fila «Código» de la ventana principal del Receiver (después tendrás que volver a introducirlo en el emisor).
- El Receiver escucha en dos puertos TCP, **8765** (texto) y **8766** (audio), y la transmisión no está cifrada. Úsalo solo en la red local de casa o a través de Tailscale, y no expongas estos puertos a Internet.
- Al pegar se toma prestado el portapapeles temporalmente; su contenido original se restaura al cabo de aproximadamente 1 segundo.

## Preguntas frecuentes

- **No se conecta**: comprueba que ambos ordenadores estén en la misma red o que ambos estén conectados a Tailscale. La IP local puede cambiar, así que conviene asignar una IP fija al Receiver en el router, o usar directamente la dirección de Tailscale.
- **Dice que el permiso de Accesibilidad no está activado**: tras recompilar o actualizar la app, macOS puede invalidar la autorización anterior. Elimina primero la entrada antigua de la lista de Accesibilidad y vuelve a añadirla.

## Actualizaciones automáticas

Ambas apps buscan versiones nuevas en GitHub por su cuenta: una vez 30 segundos después de abrirse y, a partir de ahí, cada 6 horas. Si encuentran una versión nueva, la descargan, la sustituyen y se vuelven a abrir automáticamente.

- El número de versión actual se ve abajo a la izquierda de la ventana principal; en «Ajustes… → General» puedes hacer clic en «Buscar actualizaciones» para comprobarlo al momento.
- Si no quieres que se instalen automáticamente, desactiva «Instalar actualizaciones automáticamente» en «Ajustes… → General». A partir de entonces, cuando haya una versión nueva, aparecerá en los ajustes un botón «Actualizar a x.y.z» (y la misma opción en el menú de la barra de menús), y solo se actualizará cuando hagas clic.
- No te interrumpe mientras la usas: el emisor no se actualiza mientras la ventanita de dictado está abierta; el Receiver tampoco se actualiza mientras recibe audio ni si ha recibido texto en el último minuto.
- Seguridad: la versión nueva debe estar firmada con **el mismo certificado** que la actual; de lo contrario, se rechaza la instalación.
- Tras actualizar, se conservan los permisos de Accesibilidad, micrófono, etc.; no hace falta volver a concederlos.

## License

[MIT](LICENSE)
