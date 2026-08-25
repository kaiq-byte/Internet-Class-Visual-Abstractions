# Abstrações Visuais

Animações interativas que tentam tornar visíveis conceitos de sistemas e redes que normalmente só existem como texto ou diagrama estático — coisas como "o que é um socket", "como um pacote é roteado até o destino", etc.

Cada visualização é um arquivo HTML autocontido, pensado para ser aberto direto no navegador ou hospedado via GitHub Pages.

## ⚠️ Aviso importante

> **Todas as animações deste repositório foram geradas com o auxílio de uma IA (Claude, da Anthropic)** e têm **finalidade puramente didática**.
>
> Elas são **abstrações simplificadas**, não simulações fiéis ou tecnicamente rigorosas do comportamento real de sistemas operacionais, redes ou protocolos. Diversos detalhes reais são **deliberadamente omitidos** para focar numa única ideia central de cada vez.
>
> **Não use este material como referência técnica definitiva.** Ele serve para construir intuição inicial sobre um conceito — para profundidade e precisão, consulte documentação oficial, RFCs, código-fonte de referência ou livros especializados da área (ex.: *TCP/IP Illustrated*, *Unix Network Programming*, *Computer Networking: A Top-Down Approach*, a documentação do kernel Linux).

Cada visualização traz também suas próprias notas de simplificação, específicas do que foi deixado de fora naquele caso particular.

## Conteúdo atual

| Visualização | Descrição | Simplificações principais |
|---|---|---|
| [`pacote-socket-processo.html`](./pacote-socket-processo.html) | Mostra por que "pacote → processo" é enganoso: entre os dois sempre existe um socket (`struct sock` no kernel). Três abas: (1) pacote chegando e sendo casado com a tabela de sockets pela 5-tupla, (2) processo lendo do socket via `read()`, (3) processo escrevendo e o kernel montando o pacote de saída via `write()`. | Sem segmentação/reassembly de TCP, sem buffers de anel/DMA/IRQ/softirqs, sem three-way handshake, sem `accept()` criando socket novo, sem controle de congestionamento. |
| [`netmap.html`](./netmap.html) | Simulador de roteamento: uma rede fictícia com clientes, roteadores, ISPs, um backbone e um servidor de aplicação. Sorteia origem e destino e anima o pacote percorrendo o caminho (BFS) até o destino — em dois modos: **envio direto** (ponto a ponto) e **envio via servidor** (requisição/processamento/resposta). | Topologia e caminhos são fictícios e simplificados (BFS simples, não roteamento real como BGP/OSPF), sem latência/perda de pacotes realista, sem representar camadas de protocolo (IP, TCP, DNS) dentro da animação. |

## Como visualizar

**Localmente:** baixe o arquivo `.html` desejado e abra no navegador (duplo clique ou `Ctrl+O`). Não precisa de servidor, build ou instalação — é HTML/CSS/JS puro (o `netmap.html` carrega fontes do Google Fonts via CDN; o restante é 100% offline).

**Online (GitHub Pages):** depois de publicado, cada arquivo fica acessível em:
```
https://SEU_USUARIO.github.io/NOME_DO_REPO/pacote-socket-processo.html
https://SEU_USUARIO.github.io/NOME_DO_REPO/netmap.html
```

## Estrutura do repositório

```
.
├── README.md
├── pacote-socket-processo.html
├── netmap.html
└── (novas visualizações aqui, um .html por conceito)
```

## Adicionando novas visualizações

Ao adicionar uma nova animação:
1. Um arquivo `.html` autocontido (CSS e JS inline, evitando dependências externas sempre que possível).
2. Uma linha nova na tabela de conteúdo acima, incluindo as principais simplificações feitas.
3. De preferência, um aviso interno (banner ou nota) no próprio arquivo, explicando o que foi deixado de fora especificamente naquela visualização.

## Licença

[MIT](https://choosealicense.com/licenses/mit/) — livre para usar, copiar, modificar e distribuir, mantendo o aviso de copyright.
