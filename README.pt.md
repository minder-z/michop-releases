<p align="center"><img src="assets/banner.png" alt="传声筒 MicHop" width="760"></p>
<p align="center"><a href="README.md">简体中文</a> · <a href="README.zh-Hant.md">繁體中文</a> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.es.md">Español</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pt.md">Português</a> · <a href="README.ru.md">Русский</a></p>

<p align="center">
  <b>Empreste o microfone deste Mac para outro Mac.</b><br>
  Envie como áudio ou como texto, pela rede local ou pelo Tailscale.<br>
  <sub>Lend your Mac's microphone to another Mac — as live audio or as text, over LAN or Tailscale.</sub>
</p>

---

## Para que serve

Eu costumo trabalhar num MacBook e uso um software de acesso remoto (UU Remote, Sunlogin, ToDesk etc.) para me conectar a um Mac mini e trabalhar nele — por exemplo, pedir ao Claude Code para escrever código, editar vídeos ou cuidar de sites.

O problema: **o Mac mini não tem microfone, e o software de acesso remoto não transmite o microfone do MacBook**. Por isso, não dá para usar entrada por voz dentro da área de trabalho remota.

O MicHop resolve exatamente isso. Instale um app em cada computador:

- **O computador em que você fala** (por exemplo, o MacBook): instale o "MicHop"
- **O computador que faz o trabalho** (por exemplo, o Mac mini): instale o "MicHop Receiver"

### Dois jeitos de enviar, alternáveis a qualquer momento na janela principal

```
MacBook (você fala)                          Mac mini (trabalha)

Microfone ── 🔊 Enviar áudio ─────────►  Microfone virtual (MicHop Audio, embutido)
                                      → Ditado / WeChat Input Method / modo de voz do Claude Code

Ditado ───── 📝 Enviar texto ─────────►  Colado onde está o cursor, com Return automático opcional

              pela rede local ou pelo Tailscale
```

**🔊 Enviar áudio: o Mac mini "ouve" você diretamente**

O som do microfone do MacBook é transmitido em tempo real para o Mac mini e passa a ser o microfone do Mac mini. Qualquer app do Mac mini que precise de microfone pode usá-lo, como o Ditado do sistema, a entrada por voz do WeChat Input Method ou o modo de voz do Claude Code.

- O Receiver já traz seu próprio dispositivo de áudio virtual, o **MicHop Audio**. Na primeira vez que você enviar áudio, ele oferece a instalação (é preciso digitar a senha de administrador uma vez); não há nada para baixar à parte. Quem já instalou o [BlackHole](https://github.com/ExistentialAudio/BlackHole) pode continuar usando.
- Tem cancelamento de eco integrado, então não há eco mesmo conectado por software de acesso remoto.
- A tecla Fn não passa pelo software de acesso remoto; lembre-se de trocar o atalho da entrada por voz por uma combinação de teclas modificadoras, como Ctrl + Option. [Veja mais abaixo](#dica-a-tecla-fn-não-passa-pela-conexão-remota-troque-o-atalho).

**📝 Enviar texto: reconhece no MacBook e envia as palavras**

No MacBook, pressione ⌃⌥Espaço (Ctrl + Option + Espaço) e use o Ditado do sistema para transformar sua fala em texto. O texto é enviado ao Mac mini e colado automaticamente onde está o cursor; ele também pode pressionar Return automaticamente para enviar direto ao Claude.

- Não é preciso instalar driver de áudio nem configurar áudio no Mac mini — é a opção mais prática e mais estável.
- É o modo padrão do app.

| | 🔊 Enviar áudio | 📝 Enviar texto |
|---|---|---|
| Em qual computador a fala é reconhecida | Mac mini (com o próprio ditado ou método de entrada) | MacBook (com o Ditado do sistema) |
| O que o Mac mini precisa | Receiver + o dispositivo de áudio virtual embutido (instalado no primeiro uso) | Só o Receiver |
| Ideal para | Usar o método de entrada, o ditado ou o modo de voz do Claude no Mac mini | Só transformar o que você fala em texto digitado |

### Como conectar os dois computadores

- **Na mesma rede local**: basta informar o IP local do Mac mini.
- **Em lugares diferentes**: instale o [Tailscale](https://tailscale.com) nos dois computadores para formar uma rede local virtual e informe o **IP do Tailscale** do Mac mini (começa com 100). **Tanto o áudio quanto o texto podem passar pelo Tailscale**, então funciona igual em casa ou fora.
- A janela do Receiver mostra o IP local, o IP do Tailscale e o código, cada um com um botão de copiar ao lado.

### Outros destaques

- **Nenhum serviço de nuvem no caminho**: o áudio e o texto vão direto entre os seus dois computadores, pela rede local ou pelo túnel criptografado do Tailscale.
- **Independente do software de acesso remoto**: funciona junto com UU Remote, Sunlogin, ToDesk e Compartilhamento de Tela.
- **Atualização automática**: atualiza sozinho quando sai uma versão nova, sem precisar conceder as permissões de novo.
- **Multilíngue**: a interface está disponível em 简体中文, 繁體中文, English, 日本語, 한국어, Español, Français, Deutsch, Português e Русский. O padrão é chinês; troque o idioma em "Ajustes… → Geral → Idioma / Language".

## Download e instalação

Baixe em [Releases](../../releases/latest):

| Arquivo | Em qual computador | Ícone na barra de menus |
|---|---|---|
| `MicHop.zip` (MicHop) | O computador em que você fala, ex.: MacBook | Um quadrado de cantos arredondados, igual ao ícone do app |
| `MicHop-Receiver.zip` (MicHop Receiver) | O computador que trabalha, ex.: Mac mini | Igual ao de cima |

A cor do ícone na barra de menus indica o estado: **cinza** = não conectado, **verde** = conectado, **vermelho** = transmitindo (falando / recebendo áudio).

> **Nos dois apps, tudo gira em torno da janela principal**: clique no ícone do Dock para abrir a janela principal. No topo, dois blocos mostram o estado: "Conexão" (cinza / azul) e "Áudio" (cinza / vermelho), e as ações do dia a dia ficam na própria janela; idioma, atualização automática e afins ficam em "Ajustes…" (⌘,). O ícone da barra de menus e o clique com o botão direito no ícone do Dock mantêm só os itens mais usados. Quando o notch da câmera do MacBook esconder o ícone da barra de menus, use o ícone do Dock.

Requer macOS 13 ou posterior; funciona em Macs com Apple Silicon e com Intel.

> **Na primeira abertura aparece "não é possível verificar o desenvolvedor"**: isso acontece porque o app não passou pela notarização paga da Apple. Abra Ajustes do Sistema → Privacidade e Segurança e clique em "Abrir Mesmo Assim" na parte de baixo da página. Você também pode executar este comando no Terminal para remover a quarentena e depois abrir o app:
> ```bash
> xattr -dr com.apple.quarantine "/Applications/MicHop Receiver.app"
> ```

### 1. O computador que trabalha (Receiver)

1. Descompacte `MicHop-Receiver.zip`, arraste o "MicHop Receiver" para "Aplicativos" e abra-o.
2. Siga as instruções para ativar a permissão de **Acessibilidade**: Ajustes do Sistema → Privacidade e Segurança → Acessibilidade → ative o "MicHop Receiver". Ele precisa dessa permissão para pressionar ⌘V por você.
   - Se aparecer "Deseja que o aplicativo aceite conexões de rede de entrada?", clique em **Permitir**.
3. Clique no ícone do "MicHop Receiver" no Dock. Na janela principal você vê:
   - **Dados de conexão**: o endereço local deste Mac, o endereço do Tailscale e o código, cada um com um botão de copiar ao lado.
   - **Preparação**: a linha "Permissão de acessibilidade" deve mostrar um visto verde. Itens com aviso amarelo trazem, à direita, um botão que resolve o problema.
4. "Abrir ao iniciar sessão" vem ativado por padrão; se não precisar disso, desative em "Ajustes… → Geral".

### 2. O computador em que você fala (emissor)

1. Descompacte `MicHop.zip`, arraste o "MicHop" para "Aplicativos" e abra-o.
2. Na primeira vez, abre-se a janela de ajustes: informe o **endereço** e o **código** do Receiver, clique em "Testar conexão" e, quando aparecer em verde "Conectado — pronto para usar", clique em "Salvar".
   - Na janela do Receiver, os botões de copiar ao lado dos endereços e do código copiam cada valor separadamente.
   - Você também pode clicar em "Copiar tudo" no Receiver e colar o bloco inteiro no campo "Endereço do receptor". O emissor encontra o endereço automaticamente (dando preferência ao endereço do Tailscale, se houver) e também preenche o código.
   - Se aparecer "Permitir encontrar dispositivos na rede local", clique em **Permitir**.
3. Confirme que o Ditado do sistema está ativado: Ajustes do Sistema → Teclado → Ditado.
4. Quando o topo da janela principal mostrar "Conectado ao receptor", está tudo pronto. Para mudar o endereço ou o código depois, clique em "Alterar…" na seção "Receptor" da janela principal, ou pressione ⌘,.

## Como usar

1. Primeiro, na área de trabalho remota, clique num campo de texto do computador que trabalha, por exemplo no Claude Code.
2. Pressione **⌃⌥Espaço (Ctrl + Option + Espaço)**: uma janelinha aparece na parte de baixo da tela e o ditado começa automaticamente. Se o ditado não começar sozinho, pressione Fn uma vez.
3. Fale e, ao terminar, pressione **Return**: o texto aparece no outro computador.

| Tecla | Função |
|---|---|
| Return / ⌃⌥Espaço de novo | Enviar |
| Shift + Return | Nova linha |
| Esc | Cancelar |

O topo da janelinha mostra para qual computador o texto vai. No canto inferior esquerdo fica a opção "Pressionar Enter após enviar", marcada por padrão, para que o texto seja enviado direto ao Claude. Se preferir revisar antes de enviar manualmente, desmarque (a mesma opção também está em "Opções" na janela principal).

Se o software de acesso remoto capturar essa combinação de teclas e a janelinha não aparecer, clique no botão grande "Falar" na janela principal, ou no ícone da barra de menus → "Falar".

> **Os atalhos podem ser alterados**: em "Ajustes… → Atalhos", clique no botão e pressione a nova combinação de teclas. Em alguns Macs, o ⌃⌥Espaço já está ocupado pelo atalho do sistema "Selecionar a próxima fonte no menu Entrada", e pressioná-lo troca a fonte de entrada. Nesse caso, o app mostra um aviso laranja: desative esse item em Ajustes do Sistema → Teclado → Atalhos de Teclado → Fontes de Entrada, ou escolha outra combinação no MicHop.

## Dois modos de envio

Alterne na janela principal, em "Enviar como", clicando no cartão "Texto" ou "Áudio"; o menu do ícone da barra de menus também permite trocar. **O padrão é Enviar texto.**

| | Enviar texto (padrão) | Enviar áudio |
|---|---|---|
| Onde a fala é reconhecida | Neste Mac, pelo Ditado do sistema | No outro computador, pelo próprio ditado ou pelo modo de voz do Claude Code |
| O que o ⌃⌥Espaço faz | Abre a janelinha de ditado | Inicia ou para o modo "Sempre ativo" |
| Segurar ⌃⌥ | — | Envia só enquanto segura; para ao soltar |
| Botão grande na janela principal | "Falar" | "Iniciar áudio" / "Parar áudio" |
| O que o outro lado precisa | Só o Receiver | O Receiver e o dispositivo de áudio virtual embutido |

## Modo Enviar áudio

Use este modo quando quiser que o computador que trabalha **ouça sua voz diretamente**, por exemplo para usar o modo de voz do Claude Code nesse computador ou o próprio ditado dele.

```
Microfone do MacBook ──áudio──► Receiver ──► Dispositivo de áudio virtual MicHop Audio ──► qualquer app desse Mac que "escute o microfone"
```

**Antes, no computador do Receiver:**

1. Instale o dispositivo de áudio virtual embutido, o **MicHop Audio**: na primeira vez que o emissor enviar áudio, o Receiver mostra um aviso; clique em "Instalar". Você também pode clicar em "Instalar" em "Ajustes… → Dispositivo de áudio virtual" no Receiver. O sistema pede a senha de administrador uma vez e, ao terminar, o som do sistema é interrompido por um ou dois segundos.
2. Depois de instalado, siga o aviso e mude o **dispositivo de entrada do sistema** para MicHop Audio (em "Preparação", na janela principal, também há o botão "Corrigir").
3. Mantenha o dispositivo de **saída** do sistema nos alto-falantes (ou no dispositivo de áudio do software de acesso remoto). O próprio MicHop Audio não pode ser escolhido como saída do sistema, então o som do sistema não se mistura.

> **Já instalou o BlackHole antes?** Ele continua funcionando: em "Preparação → Tocar em", escolha o dispositivo que preferir. Para trocar pelo embutido, clique em "Instalar" ao lado de "Você pode usar o dispositivo virtual embutido". Se usar o BlackHole, cuidado para não escolhê-lo como saída do sistema; se escolher errado, aparecerá em "Preparação" um aviso de "Saída do sistema", e basta clicar em "Voltar aos alto-falantes".

> **Por que há eco?** Muitos softwares de acesso remoto (como o UU Remote) capturam o som do computador controlado usando o framework de gravação de tela da Apple, que grava **o som de todos os apps** desse computador, não importa em qual dispositivo de áudio ele toque. Quando o MicHop toca sua voz no dispositivo de áudio virtual, ela também é gravada, volta para o seu computador, sai pelos alto-falantes e é captada de novo pelo microfone.
>
> Por isso o emissor vem com o **"Cancelamento de eco"** ativado por padrão (dá para desativar em "Opções" na janela principal). Ele usa o processamento de voz da Apple, o mesmo do FaceTime: subtrai do microfone o som que volta, abaixa os outros sons enquanto você fala e, de quebra, reduz o ruído. Com fones de ouvido o resultado é melhor.

**Como usar:**

Na janela principal, em "Enviar como", escolha "Áudio": o emissor se conecta ao Receiver (na primeira vez, será pedida a permissão do microfone), "Conexão" fica azul e o ícone da barra de menus fica verde. A partir daí, há duas formas de falar, sempre disponíveis:

1. **Sempre ativo**: pressione **⌃⌥Espaço** uma vez (ou clique em "Iniciar áudio") e o microfone fica ligado; pressione de novo para parar.
2. **Segurar para falar**: **segure Ctrl + Option enquanto fala e solte para parar**. O microfone só fica ligado enquanto você segura as teclas: "Áudio" fica vermelho na janela principal e o ícone da barra de menus também; ao soltar, o microfone desliga e o volume deste Mac também não é abaixado. Na primeira vez, será pedida a permissão de Acessibilidade, usada para detectar essa combinação de teclas; se ela não estiver ativada, "Opções" na janela principal avisa, e basta clicar em "Ativar…".
3. O software de acesso remoto também repassa a combinação que você segura para o computador que trabalha. Se nesse computador você também definir Ctrl + Option como atalho de voz do ditado ou do método de entrada (veja [a dica abaixo](#dica-a-tecla-fn-não-passa-pela-conexão-remota-troque-o-atalho)), **um único toque já envia o áudio e faz o ditado começar do outro lado**.
4. Os dois atalhos podem ser alterados em "Ajustes… → Atalhos".

> Enquanto você segura as teclas, o MicHop silencia este Mac temporariamente, para que o som devolvido pelo app de acesso remoto não chegue ao microfone e cause eco; o som volta cerca de 1 segundo depois de soltar. (O modo Sempre ativo usa o cancelamento de eco da Apple.)

### Dica: a tecla Fn não passa pela conexão remota, troque o atalho

Quando você está conectado por um software de acesso remoto como UU Remote, Sunlogin ou ToDesk, **pressionar Fn no seu Mac não chega ao computador controlado**. Seja o Ditado do sistema ou a entrada por voz do WeChat Input Method no computador controlado, nada é acionado. Há dois motivos: a tecla Fn é interceptada primeiro pelo seu Mac (que inicia o próprio ditado); e, mesmo que o software remoto a repasse, do outro lado ela é só um "toque de tecla simulado", que o sistema e os métodos de entrada normalmente ignoram.

A solução: no **computador controlado** (por exemplo, o Mac mini), troque o atalho da entrada por voz:

- **Ditado do sistema**: Ajustes do Sistema → Teclado → Ditado → Atalho → "Personalizar".
- **WeChat Input Method**: altere o atalho da entrada por voz nos ajustes do WeChat Input Method.

Recomendamos uma **combinação de teclas modificadoras**, como **Ctrl esquerdo + Option**, ou Ctrl com outra tecla modificadora (Option, Shift, Command).

**Não use Ctrl com uma tecla de número ou letra** (como Ctrl+D). A entrada por voz normalmente exige segurar a tecla enquanto você fala, e segurar uma letra ou número faz o caractere se repetir sem parar, o que é muito incômodo. Uma combinação só de modificadoras não digita nenhum caractere quando mantida pressionada.

Este truque funciona junto com o modo "Enviar áudio": defina o MicHop Audio como dispositivo de entrada do computador controlado, segure o novo atalho na área de trabalho remota enquanto fala, e o computador controlado consegue fazer o ditado diretamente.

## Não estão na mesma rede? Use o Tailscale

1. Instale o [Tailscale](https://tailscale.com) nos dois computadores e entre na mesma conta.
2. Na janela principal do Receiver, em "Dados de conexão", a linha "Tailscale" mostra 100.x.x.x; informe esse endereço nos ajustes do emissor. Também dá para usar o nome da máquina exibido no Tailscale.
3. Se aparecer "não detectado", confirme primeiro que o Tailscale está conectado no computador do Receiver e clique no botão de atualizar dessa linha para detectar de novo. Se ainda assim não for detectado, vá em "Ajustes… → Tailscale → Endereço manual" no Receiver e digite o endereço mostrado no menu do Tailscale.

O endereço do Tailscale funciona em casa e fora; quando os dois computadores estão na mesma rede local, a conexão direta é feita automaticamente.

## Segurança

- Cada Receiver tem um código aleatório de 6 dígitos, e qualquer solicitação com código errado é recusada. Na janela principal do Receiver, clique em "Novo" na linha "Código" (depois disso, é preciso informar o código de novo no emissor).
- O Receiver escuta em duas portas TCP, **8765** (texto) e **8766** (áudio), e a transmissão não é criptografada. Use apenas na rede local de casa ou pelo Tailscale, e não exponha essas portas à internet.
- Ao colar, a área de transferência é usada temporariamente, e o conteúdo original é restaurado após cerca de 1 segundo.

## Perguntas frequentes

- **Não conecta**: confirme que os dois computadores estão na mesma rede, ou que ambos estão conectados ao Tailscale. O IP local pode mudar; recomendamos definir um IP fixo para o Receiver no roteador, ou usar direto o endereço do Tailscale.
- **Aviso de que a permissão de Acessibilidade não está ativada**: depois de recompilar ou atualizar o app, o macOS pode invalidar a autorização anterior. Remova primeiro o item antigo da lista de Acessibilidade e depois adicione-o de novo.

## Atualização automática

Os dois apps verificam sozinhos se há versões novas no GitHub: uma vez 30 segundos após abrir e, depois, a cada 6 horas. Ao encontrar uma versão nova, eles baixam, substituem e reabrem automaticamente.

- O número da versão atual aparece no canto inferior esquerdo da janela principal; em "Ajustes… → Geral" você pode clicar em "Verificar atualizações" para checar na hora.
- Se não quiser instalação automática, desative "Instalar atualizações automaticamente" em "Ajustes… → Geral". A partir daí, quando houver uma versão nova, os ajustes mostrarão o botão "Atualizar para x.y.z" (o mesmo item aparece também no menu da barra de menus), e a atualização só acontece quando você clicar.
- Não interrompe você durante o uso: o emissor não atualiza enquanto a janelinha de ditado está aberta; o Receiver também não atualiza durante o envio de áudio, nem se tiver recebido texto no último minuto.
- Segurança: a versão nova precisa ser assinada com **o mesmo certificado** da versão atual; caso contrário, a instalação é recusada.
- Depois da atualização, as permissões de Acessibilidade, microfone etc. são mantidas; não é preciso concedê-las de novo.

## License

[MIT](LICENSE)
