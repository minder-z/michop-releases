<p align="center"><img src="assets/banner.png" alt="传声筒 MicHop" width="760"></p>
<p align="center"><a href="README.md">简体中文</a> · <a href="README.zh-Hant.md">繁體中文</a> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.es.md">Español</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pt.md">Português</a> · <a href="README.ru.md">Русский</a></p>

<p align="center">
  <b>Empreste o microfone deste Mac para outro Mac.</b><br>
  Você fala aqui e o outro Mac ganha um microfone — pela rede local ou pelo Tailscale.<br>
  <sub>Lend your Mac's microphone to another Mac — live, over LAN or Tailscale.</sub>
</p>

---

## Para que serve

No dia a dia eu trabalho num MacBook e uso um app de acesso remoto (UU Remote, Sunlogin, ToDesk etc.) para me conectar a um Mac mini, onde o trabalho de verdade acontece: deixar o Claude Code escrever código, editar vídeos, cuidar de sites.

O problema: **o Mac mini não tem microfone, e o app de acesso remoto não repassa o microfone do MacBook**. Por isso, dentro da área de trabalho remota não dá para usar entrada por voz.

É isso que o MicHop resolve. Cada computador recebe um app:

- **O computador em que você fala** (por exemplo, o MacBook): instale o “MicHop”
- **O computador que faz o trabalho** (por exemplo, o Mac mini): instale o “MicHop Receiver”

```
MacBook (você fala)                          Mac mini (faz o trabalho)

Microfone ──── 🔊 Áudio ──────────────►  Microfone virtual (MicHop Audio embutido)
                                      → Ditado / método de entrada do WeChat / modo de voz do Claude Code

              pela rede local ou pelo Tailscale
```

O som do microfone do MacBook chega ao Mac mini em tempo real e passa a funcionar como o microfone do Mac mini. Qualquer app do Mac mini que precise de microfone pode usá-lo: o Ditado do macOS, a entrada por voz do método de entrada do WeChat, o modo de voz do Claude Code e assim por diante.

- O Receiver já vem com o dispositivo de áudio virtual **MicHop Audio**. Na primeira vez que você o abre, ele oferece a instalação (é preciso digitar a senha de administrador uma vez); não há nada para baixar à parte. Quem já tem o [BlackHole](https://github.com/ExistentialAudio/BlackHole) instalado pode continuar usando.
- Dois jeitos de falar, sempre disponíveis: pressione **⌃⌥M** uma vez para enviar sem parar e de novo para parar; ou **mantenha ⌃⌥ pressionadas** enquanto fala e solte para parar.
- Cancelamento de eco embutido: nada de eco, mesmo conectado por um app de acesso remoto.
- A tecla Fn não passa pelos apps de acesso remoto. Por isso, troque no Mac mini o atalho da entrada por voz por uma combinação de teclas modificadoras, como Ctrl + Option. [Veja os detalhes abaixo](#dica-a-tecla-fn-não-chega-pela-conexão-remota-então-troque-o-atalho).

### Como conectar os dois computadores

- **Na mesma rede local**: basta digitar o IP local do Mac mini.
- **Em lugares diferentes**: instale o [Tailscale](https://tailscale.com) nos dois computadores para criar uma rede local virtual e digite o **IP do Tailscale** do Mac mini (começa com 100). Funciona igual em casa ou fora.
- A janela do Receiver mostra o IP local, o IP do Tailscale e o código, cada um com um botão de copiar ao lado.

### Outros destaques

- **Nenhum serviço na nuvem no meio do caminho**: o som vai direto entre os seus dois computadores, pela rede local ou pelo túnel criptografado do Tailscale.
- **Independente do app de acesso remoto**: funciona com UU Remote, Sunlogin, ToDesk e o Compartilhamento de Tela.
- **Atualização automática**: quando sai uma versão nova, o app se atualiza sozinho, sem precisar autorizar as permissões de novo.
- **Vários idiomas**: a interface está disponível em 简体中文, 繁體中文, English, 日本語, 한국어, Español, Français, Deutsch, Português e Русский. O padrão é chinês; para mudar, vá em “Ajustes… → Geral → Idioma / Language”.

## Download e instalação

Baixe em [Releases](../../releases/latest):

| Arquivo | Em qual computador instalar | Ícone na barra de menus |
|---|---|---|
| `MicHop.zip` (MicHop) | O computador em que você fala, por exemplo o MacBook | Dois microfones, igual ao ícone do app |
| `MicHop-Receiver.zip` (MicHop Receiver) | O computador que faz o trabalho, por exemplo o Mac mini | Igual |

A cor do ícone na barra de menus indica o estado: **cinza** = desconectado, **verde** = conectado, **vermelho** = enviando áudio.

> **Nos dois apps, tudo gira em torno da janela principal**: clique no ícone do Dock para abri-la. No topo há duas áreas de estado, “Conexão” (cinza/azul) e “Áudio” (cinza/vermelho), e as ações do dia a dia ficam na própria janela. Atalhos, idioma, atualização automática etc. ficam em “Ajustes…” (⌘,). O ícone da barra de menus e o menu de contexto do ícone do Dock trazem só as opções mais usadas. Se o entalhe da câmera do MacBook esconder o ícone da barra de menus, use o ícone do Dock.

Requer macOS 13 ou posterior e funciona tanto em Macs com chip da Apple quanto em Macs com processador Intel.

> **Na primeira abertura aparece o aviso de que o desenvolvedor não pode ser verificado**: isso acontece porque o app não passou pela notarização paga da Apple. Abra Ajustes do Sistema → Privacidade e Segurança e, na parte de baixo da página, clique em “Abrir Mesmo Assim”. Outra opção é rodar este comando no Terminal para remover a quarentena e depois abrir o app:
> ```bash
> xattr -dr com.apple.quarantine "/Applications/MicHop Receiver.app"
> ```

### 1. O computador que faz o trabalho (Receiver)

1. Descompacte o `MicHop-Receiver.zip`, arraste o “MicHop Receiver” para a pasta “Aplicativos” e abra-o.
   - Se aparecer a pergunta se o app pode aceitar conexões de rede de entrada, clique em **Permitir**.
2. Na primeira abertura, o app oferece instalar o dispositivo de áudio virtual embutido **MicHop Audio**: clique em “Instalar” e digite a senha de administrador uma vez. Ao terminar, o som do sistema falha por um ou dois segundos. Você também pode instalar depois, em “Ajustes… → Dispositivo de áudio virtual”.
3. Depois de instalar, siga a indicação e mude o **dispositivo de entrada do sistema** para MicHop Audio (a área “Preparação” da janela principal também tem um botão “Corrigir” para isso). O dispositivo de **saída** do sistema pode continuar nos alto-falantes (ou no dispositivo de áudio do app de acesso remoto). O próprio MicHop Audio não pode ser escolhido como saída do sistema, então o som do sistema não se mistura ao seu.
4. Na janela principal você vê:
   - **Dados de conexão**: o endereço local, o endereço do Tailscale e o código deste Mac, cada um com um botão de copiar ao lado.
   - **Preparação**: quando o dispositivo de áudio virtual e a entrada do sistema estão com o visto verde, está tudo pronto. Os itens com aviso amarelo mostram à direita um botão para corrigir.
5. Por padrão, o Receiver abre sozinho ao iniciar sessão. Se não quiser isso, desative em “Ajustes… → Geral”.

> **Já tinha o BlackHole instalado?** Ele continua funcionando: em “Preparação → Tocar em”, escolha o dispositivo de áudio que quiser usar. Para trocar pelo embutido, clique em “Instalar”, ao lado de “Você pode usar o dispositivo virtual embutido”. Com o BlackHole, cuidado para não escolhê-lo como saída do sistema; se isso acontecer, aparece em “Preparação” um aviso de “Saída do sistema”, e basta clicar em “Voltar aos alto-falantes”.

### 2. O computador em que você fala (emissor)

1. Descompacte o `MicHop.zip`, arraste o “MicHop” para a pasta “Aplicativos” e abra-o.
2. Na primeira abertura aparece a janela de configuração: digite o **endereço** e o **código** do Receiver, clique em “Testar conexão” e, quando aparecer em verde “Conectado — pronto para usar”, clique em “Salvar”.
   - Na janela do Receiver, os botões de copiar ao lado do endereço e do código copiam cada item separadamente.
   - Você também pode clicar em “Copiar tudo” no Receiver e colar o bloco inteiro no campo “Endereço”. O emissor escolhe o endereço sozinho (dando preferência ao do Tailscale, se houver) e preenche o código automaticamente.
   - Se aparecer o pedido para encontrar dispositivos na rede local, clique em **Permitir**.
3. Na primeira vez, o app pede acesso ao **Microfone**: clique em Permitir. Ele também pede acesso à **Acessibilidade** (para detectar quando você mantém ⌃⌥ pressionadas); siga as instruções: Ajustes do Sistema → Privacidade e Segurança → Acessibilidade → ative o “MicHop”.
4. Assim que o app abre, ele se conecta ao Receiver. Quando “Conexão” fica azul na janela principal e o ícone da barra de menus fica verde, já pode usar. Para mudar o endereço ou o código depois, clique em “Alterar…” na área “Receptor” da janela principal, ou pressione ⌘,.

## Como usar

Primeiro, na área de trabalho remota, clique no ponto do outro computador onde você quer usar a voz: o modo de voz do Claude Code, o Ditado ou um método de entrada. Depois, os dois jeitos de falar ficam disponíveis a qualquer momento:

1. **Envio contínuo**: pressione **⌃⌥M (Ctrl + Option + M)** uma vez, ou clique em “Iniciar áudio” na janela principal, e o microfone fica aberto; pressione de novo para parar.
2. **Segurar para falar**: **mantenha Ctrl + Option pressionadas enquanto fala e solte para parar**. O microfone só fica aberto enquanto as teclas estão pressionadas.

Durante o envio, “Áudio” na janela principal e o ícone da barra de menus ficam vermelhos; do lado do Receiver, “Áudio” também fica vermelho.

- As teclas que você segura também são repassadas pelo app de acesso remoto ao outro computador. Se lá você também definir Ctrl + Option como atalho de voz do Ditado ou do método de entrada (veja a [dica abaixo](#dica-a-tecla-fn-não-chega-pela-conexão-remota-então-troque-o-atalho)), **um único toque já começa a enviar o áudio e faz o outro lado começar a ditar**.
- Enquanto você segura as teclas, o MicHop silencia temporariamente este Mac. Assim o som do outro computador, devolvido pelo app de acesso remoto, não é captado pelo microfone e não vira eco. Cerca de 1 segundo depois de soltar, o som volta. (No envio contínuo, quem cuida disso é o cancelamento de eco da Apple.)

> **Os atalhos podem ser alterados**: em “Ajustes… → Atalhos”, clique em um botão e pressione a nova combinação. “Começar a falar” aceita qualquer combinação com ⌃, ⌥ ou ⌘; “Segurar para falar” precisa de duas ou mais teclas entre ⌃ ⌥ ⇧ ⌘. Se a combinação escolhida já estiver em uso pelo sistema (em muitos Macs, ⌃⌥Espaço é “Selecionar a próxima fonte no menu Entrada”), o app mostra um aviso em laranja: desative esse item em Ajustes do Sistema → Teclado → Atalhos de Teclado ou escolha outra combinação.

> **Por que aparece eco?** Muitos apps de acesso remoto (como o UU Remote) captam o som do Mac controlado usando o framework de gravação de tela da Apple, que grava **o som de todos os apps daquele computador**, não importa em qual dispositivo de áudio ele toque. Quando o MicHop toca a sua voz no dispositivo de áudio virtual, ela é gravada junto, enviada de volta ao seu computador, sai pelos alto-falantes e é captada de novo pelo microfone.
>
> Por isso o **cancelamento de eco** vem ativado por padrão no emissor (dá para desativar em “Opções”, na janela principal). Ele usa o processamento de voz da Apple, o mesmo do FaceTime: subtrai do microfone o som que volta, abaixa os outros sons enquanto você fala e ainda reduz o ruído. Com fones de ouvido, o resultado é ainda melhor.

### Dica: a tecla Fn não chega pela conexão remota, então troque o atalho

Quando você se conecta por apps como UU Remote, Sunlogin ou ToDesk, **a tecla Fn pressionada no seu Mac não chega ao Mac controlado**. Nem o Ditado do macOS nem a entrada por voz do método de entrada do WeChat são acionados. Há dois motivos: o seu próprio Mac intercepta a tecla Fn antes (e começa ele mesmo a ditar); e, mesmo que o app de acesso remoto a repasse, no Mac controlado ela é só uma “tecla simulada”, que o sistema e os métodos de entrada normalmente ignoram.

A solução é trocar o atalho da entrada por voz no **Mac controlado** (por exemplo, o Mac mini):

- **Ditado do macOS**: Ajustes do Sistema → Teclado → Ditado → Atalho → “Personalizar”.
- **Método de entrada do WeChat**: nos ajustes do método de entrada do WeChat, altere o atalho da entrada por voz.

O ideal é usar uma **combinação de teclas modificadoras**, como **Ctrl esquerdo + Option**, ou Ctrl com outra tecla modificadora (Option, Shift, Command).

**Não use Ctrl com número ou letra** (como Ctrl+D). Na entrada por voz normalmente você mantém as teclas pressionadas, e uma letra ou número segurado é digitado sem parar, o que atrapalha bastante. Uma combinação só de teclas modificadoras não digita nada enquanto é mantida.

Com o dispositivo de entrada do Mac controlado definido como MicHop Audio, segure o novo atalho na área de trabalho remota e fale: o Mac controlado já começa a ditar.

## Não estão na mesma rede? Use o Tailscale

1. Instale o [Tailscale](https://tailscale.com) nos dois computadores e entre com a mesma conta.
2. Na janela principal do Receiver, em “Dados de conexão”, a linha “Tailscale” mostra um endereço 100.x.x.x. Digite-o nos ajustes do emissor. Também dá para usar o nome da máquina que aparece no Tailscale.
3. Se aparecer “Não encontrado”, confirme primeiro que o Tailscale está conectado no Mac do Receiver e clique no botão de atualizar dessa linha para detectar de novo. Se mesmo assim não for detectado, vá em “Ajustes… → Tailscale → Endereço manual” no Receiver e digite o endereço que aparece no menu do Tailscale.

O endereço do Tailscale funciona em casa ou fora, e quando os dois estão na mesma rede local, a conexão passa a ser direta automaticamente.

## Segurança

- Cada Receiver tem um código aleatório de 6 dígitos, e conexões com o código errado são sempre recusadas. Na janela principal do Receiver, clique em “Novo” na linha “Código” para gerar outro (depois, digite-o de novo no emissor).
- O Receiver escuta uma única porta: TCP **8766** (áudio). A transmissão ainda não é criptografada. Use apenas na rede de casa ou pelo Tailscale e não exponha essa porta à internet.

## Perguntas frequentes

- **Não conecta**: confirme que os dois computadores estão na mesma rede ou que ambos estão conectados ao Tailscale. O IP local pode mudar; vale definir um IP fixo para o Receiver no roteador ou usar direto o endereço do Tailscale.
- **O Receiver avisa que não consegue abrir a porta**: geralmente um Receiver antigo não foi encerrado direito e ainda ocupa a porta; o Receiver encerra esse processo sozinho. Se for outro programa, o aviso mostra o nome dele, e o Receiver inicia sozinho assim que a porta for liberada.
- **Segurar ⌃⌥ não faz nada**: o emissor precisa de acesso à **Acessibilidade**. Depois de recompilar ou atualizar o app, o macOS às vezes invalida a autorização anterior. Nesse caso, remova o item antigo da lista de Acessibilidade e adicione o app de novo.

## Atualização automática

Os dois apps verificam sozinhos se há versões novas no GitHub: uma vez 30 segundos depois de abrir e, a partir daí, a cada 6 horas. Quando encontram uma versão nova, baixam, substituem e reabrem automaticamente.

- O número da versão atual aparece no canto inferior esquerdo da janela principal; em “Ajustes… → Geral”, clique em “Verificar atualizações” para verificar na hora.
- Se não quiser instalação automática, desative “Instalar atualizações automaticamente” em “Ajustes… → Geral”. A partir daí, quando sair uma versão nova, os ajustes mostram o botão “Atualizar para x.y.z”, e o menu da barra de menus ganha a mesma opção; a atualização só acontece quando você clica.
- Sem interrupções: enquanto o áudio está sendo enviado, nada é atualizado.
- Segurança: a versão nova precisa ser assinada com o **mesmo certificado** da versão atual; caso contrário, a instalação é recusada.
- Depois da atualização, permissões como Acessibilidade e Microfone continuam valendo, sem precisar autorizar de novo.

## License

[MIT](LICENSE)
