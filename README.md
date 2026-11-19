# 👀 Espiadinha

*[English version](README.en.md)*

Compartilhamento de tela P2P para um grupo pequeno de amigos, com voz e chat.
Windows e Linux (as duas versões conversam entre si). Interface em português e inglês (⚙️ → **Idioma**).
**Gratuito.** Este repositório só tem os downloads: o código-fonte é privado.

**⬇️ [Baixar a versão mais nova](https://github.com/ggekkos/espiadinha-releases/releases/latest)**: `Espiadinha_<versão>_x64-setup.exe` (Windows),
`.AppImage` ou `.tar.gz` (Linux). Confira o arquivo com o `SHA256SUMS.txt` (veja abaixo).

> ⚠️ Antes de usar, leia [Segurança e privacidade](#segurança-e-privacidade): o app é feito para amigos que se
> conhecem, depende de um servidor público de terceiros para as pessoas se encontrarem, e quem está na mesma sala
> vê o IP dos outros.

## Como usar
1. Baixe a versão mais nova na página de [Releases](https://github.com/ggekkos/espiadinha-releases/releases/latest):
   `Espiadinha_<versão>_x64-setup.exe` no Windows, `Espiadinha-<versão>-x86_64.AppImage` ou o `.tar.gz` no Linux.
2. Uma pessoa clica em **Criar sala** e manda o código de 6 letras (o botão ✉️ copia um convite pronto).
   Recomendado: preencha uma **senha da sala** antes de criar. Sem a senha certa, o pedido para entrar nem chega.
3. Os outros digitam o código (e a senha, se tiver) e clicam em **Entrar na sala**. Quem criou a sala aceita cada
   pessoa na lateral. Colar o convite inteiro no campo do código preenche o código e a senha.
4. Qualquer pessoa pode clicar em **Compartilhar tela** (se alguém já estiver compartilhando, vira "Assumir a tela").

Na sala:
- 🎤 liga/desliga o microfone (atalho global **Ctrl+Shift+F9**). Passe o mouse no nome de alguém para mudar o volume da voz.
- **Ctrl+Shift+F10** começa/para de compartilhar sem sair do jogo.
- 📍 (ou **Ctrl+clique** no vídeo) aponta algo na tela de quem está compartilhando.
- "Qualidade pra mim" reduz só o que **você** recebe, se a sua internet estiver ruim.
- 👁 esconde a sua prévia enquanto compartilha (economiza GPU; no preset Jogo já começa escondida).
- 🗗 deixa a janela pequena e sempre por cima. 📊 mostra o diagnóstico da conexão. ⚙️ abre as configurações.
- 😀 manda uma reação que sobe na tela. ✏️ desenha por cima do vídeo (some sozinho em alguns segundos).
- 📎 (ou **Ctrl+V** no campo de mensagem, ou arrastar) manda imagens e arquivos (até 500 MB) no chat. O arquivo vai
  direto de quem mandou para quem clicar em "Baixar" (não passa pelo anfitrião) e fica disponível enquanto quem mandou
  estiver na sala.
- 🎬 (ou **Ctrl+Shift+F11**): o primeiro aperto começa a guardar a tela, os seguintes salvam os últimos 30 s
  em MP4 na pasta Downloads.
- ⚙️ → **Aparência**: temas clássicos (Escuro, Claro, Vampiro...) e especiais com efeito animado (Frieren, Noite
  estrelada, Vaga-lumes, Inverno, Primavera, Café lo-fi, Fogueira), cor de destaque, a sua cor e um avatar.
- **Seus temas**: "＋ Criar tema" (ou ✏️ em qualquer tema) abre o editor ao vivo: imagem de fundo (com escurecer,
  desfoque e enquadrar), um personagem num canto (PNG sem fundo), cores (ou "gerar a partir da imagem"),
  vidro nos painéis, cantos, fonte, frase da tela inicial e um efeito (flores, brilhos, pétalas, neve, estrelas,
  vaga-lumes, brasas, bolhas, corações, chuva). Para passar um tema a alguém: 💬 manda no chat da sala (a pessoa
  clica em "Usar") ou 📤 exporta um arquivo `.espiadinha-tema` (quem recebe usa 📂 Importar ou arrasta para a janela).
  As animações param sozinhas enquanto alguém compartilha (dá para mudar em Configurações). ⚙️ → **Voz**: "apertar para falar" (segura uma tecla, ex.: F8) e abaixar o som da tela
  quando alguém fala. Sons de aviso podem ser desligados.

## Windows
O instalador não tem assinatura digital, então o Windows mostra o aviso do SmartScreen ("O Windows protegeu o
computador"). Confira o arquivo com o `SHA256SUMS.txt` e clique em **Mais informações → Executar assim mesmo**.

## Linux
AppImage: `chmod +x Espiadinha-*.AppImage && ./Espiadinha-*.AppImage`.

Ou o `.tar.gz`:
```
tar xzf Espiadinha-<versão>-linux-x64.tar.gz
cd Espiadinha
./instalar.sh        # instala em ~/.local/share/espiadinha e cria o atalho no menu
```
Ou rode direto sem instalar: `./espiadinha.sh`.

- **Som do PC:** usa o `pactl` (pacote `pulseaudio-utils`; funciona com PipeWire também).
- **GPU:** o vídeo usa VA-API quando o driver suporta. Se der problema, desligue em ⚙️ ou abra com `--sem-gpu`.
- **Sandbox:** se o sistema bloquear o sandbox do Chromium, o `instalar.sh` pergunta se pode criar um perfil do
  AppArmor (Ubuntu) ou configurar o `chrome-sandbox` (Debian). É opcional; sem isso o app abre com `--no-sandbox`.

## Segurança e privacidade
O Espiadinha é feito para um grupo pequeno de pessoas que se conhecem. Entenda o que ele faz antes de usar:

**Como as pessoas se encontram.** O app não tem servidor próprio. Para dois PCs se acharem, ele usa o servidor
público e gratuito do [PeerJS](https://peerjs.com) (`0.peerjs.com`), mantido por terceiros, sem garantia de
funcionamento. Esse servidor vê o código da sala, o nome e a versão de quem pede para entrar, os IPs e os horários.
Ele **não** vê o chat, a voz nem a tela: isso vai direto entre os PCs, criptografado pelo próprio WebRTC.
Em Avançado dá para usar um servidor de sinalização seu.

**O que fica protegido:**
- Quem cria a sala só mostra o próprio IP para quem **aceitar**. Quem bate na porta sem ser aceito (ou é recusado)
  não recebe nada. Por isso "Recusar" não avisa a pessoa: ela fica esperando e desiste sozinha.
- Com **senha da sala**, quem não sabe a senha nem aparece na lista de pedidos. A senha não vai em texto puro: vai
  um resumo (hash) dela junto com o código. Use uma senha que não seja óbvia, e mande o convite só para quem vai entrar.
- O anfitrião limita mensagens por pessoa (chat, ping, desenho, imagens, arquivos, temas, troca de tela) e só repassa entre
  membros o que o app usa.
- Tudo que chega de outras pessoas (nomes, chat, imagens, temas) é tratado como texto ou imagem, nunca como código.
  Nomes com caracteres invisíveis são limpos, para ninguém imitar o nome de outra pessoa.
- Imagens no chat só em WebP, JPEG, PNG ou GIF (sem SVG); temas passam por uma validação completa.
- Arquivos: só quem está na sala consegue baixar, o nome chega limpo (sem truques para esconder um `.exe`) e
  programas ou scripts pedem confirmação antes de baixar. Mesmo assim, só abra arquivos de quem você confia.
- Quando a sala troca de anfitrião, quem volta precisa provar que é a mesma pessoa.

**Os riscos que continuam:**
- **Quem está dentro da sala vê o IP dos outros** (a tela e a voz vão direto entre os PCs). Só aceite quem você
  conhece. Para esconder o IP até dos amigos, use uma VPN.
- O anfitrião pode ver e repassar tudo do chat. Quem está na sala pode gravar a tela que você compartilha (o próprio
  app tem clipes): compartilhe só o que você mostraria para essas pessoas.
- Sem "Pedir minha aprovação" e sem senha, qualquer um com o código entra.
- Os instaladores **não têm assinatura digital** (o Windows mostra o aviso do SmartScreen). Baixe só da página
  oficial de [Releases](https://github.com/ggekkos/espiadinha-releases/releases/latest). Outra cópia pode ter sido alterada.
  Para conferir, cada versão tem um `SHA256SUMS.txt`:
  no Windows, `Get-FileHash .\Espiadinha_<versão>_x64-setup.exe` no PowerShell e compare com a linha do arquivo;
  no Linux, `sha256sum -c SHA256SUMS.txt --ignore-missing` na pasta do download.
- No Linux, alguns sistemas (Ubuntu 23.10+, alguns Debian) bloqueiam o sandbox do Chromium, e o app abre com
  `--no-sandbox` (uma camada de proteção a menos). O `instalar.sh` do `.tar.gz` oferece religar o sandbox (precisa
  de sudo), e o app avisa em ⚙️ quando está sem ele. O AppImage não consegue religar (a pasta dele muda a cada vez
  que abre): nesses sistemas, prefira o `.tar.gz`.
- O app é tão seguro quanto o navegador que roda dentro dele: mantenha o Espiadinha atualizado (no Linux ele traz o
  próprio Chromium, que só é atualizado junto com o app).
- O app é fornecido "como está", sem garantias (veja a [licença](LICENSE)).

Achou um problema de segurança? Veja [SECURITY.md](SECURITY.md).

## Como funciona
- A tela vai **direto** do PC de quem compartilha para cada pessoa. A voz é uma malha (cada par se conecta).
- O servidor público gratuito do PeerJS só é usado para o "aperto de mão" inicial (dá para usar um próprio em Avançado).
- Codec escolhido por pessoa: AV1 ou H.264 por GPU quando os dois lados suportam.
- Upload necessário ≈ bitrate do preset × número de espectadores
  (ex.: 3 amigos no "Jogo" = ~24 Mbps; no "Equilibrado" = ~15 Mbps). Dá para pôr um limite em ⚙️.

## Se não conectar
Alguns provedores usam CGNAT e bloqueiam a conexão direta. Aí é preciso um servidor TURN
(ex.: coturn numa VPS), configurado em **Avançado** na tela inicial. Se o servidor público do PeerJS estiver fora
do ar, suba um com `npx peer --port 9000` e configure o mesmo endereço em todos os PCs.

## Problemas, sugestões e segurança
- Bug ou sugestão: abra uma [issue](https://github.com/ggekkos/espiadinha-releases/issues).
- Problema de segurança: **não** abra issue pública; veja o [SECURITY.md](SECURITY.md).

## Licença
Gratuito para baixar, usar e repassar sem alterações; fornecido "como está", sem garantia. Veja [LICENSE](LICENSE).
