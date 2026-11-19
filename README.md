# Tutorial: criação dos Livros Digitais novos do SAE

Tutorial web navegável para ensinar, na prática, o fluxo de criação dos livros digitais (LD) novos do SAE, do PDF do professor até o pagamento das freelas.

Nasceu da proposta de treinamento "ponta a ponta" feita pela supervisão: quem é nova no time precisa conseguir seguir os passos, aplicar em um projeto real e entregar um capítulo concluído até **11/12**.

## Para quem é

- Pessoas novas no time que vão produzir capítulos.
- Quem apoia, planeja ou defende as entregas e precisa conhecer o trabalho a fundo.
- O time, como material vivo: cada pessoa pode corrigir e complementar os passos.

## O que o tutorial cobre

O fluxo de **livros novos**, que o time faz internamente. O aproveitamento é terceirizado e fica fora do escopo.

São 13 passos, em 4 fases:

| Fase | Passos | O que acontece |
|---|---|---|
| Preparação | 1 a 3 | Baixar o PDF do professor no Assets, dividir por disciplina e subir no Drive |
| Produção | 4 a 8 | Reservar o capítulo na planilha, gerar o HTML no DIA LD e guardar HTML e imagens na pasta da disciplina |
| Validação | 9 a 11 | Conferir PDF e HTML lado a lado, passar pelo cotejo e aplicar os ajustes |
| Publicação e pagamento | 12 e 13 | Subir no Bigodão, registrar o link na planilha e liberar o pagamento |

Além dos passos, a página tem: **Visão geral**, **Acessos e ferramentas**, **Plano de encontros** (sugestão de 4 encontros, um por fase) e **Glossário**.

Cada passo traz: ferramenta usada, acesso necessário, caminho de pastas quando existe, o que fazer, itens para conferir antes de seguir, pontos de atenção e links diretos.

Projeto de exemplo usado ao longo do texto: um capítulo de **Geografia, 5º ano**, de um volume novo (V2), usando o HTML do V1 como referência.

## Estrutura da pasta

```
.
├── index.html      # a página inteira: estilos, conteúdo e script
├── digi.png        # Digi, o robô guia, usado na visão geral
├── sae-logo.png    # logo da SAE Digital, usada no menu lateral
└── README.md
```

Não há build, dependências nem servidor. É HTML, CSS e JavaScript puros. A única coisa carregada de fora são as fontes do Google Fonts.

## Como rodar localmente

Abrir o `index.html` direto no navegador funciona. Se preferir um servidor local:

```bash
python3 -m http.server 8000
# abrir http://localhost:8000
```

## Como publicar no GitHub Pages

1. Suba os arquivos na raiz de um repositório.
2. Em **Settings > Pages**, escolha a branch `main` e a pasta `/ (root)`.
3. Aguarde a publicação. O endereço fica no formato `https://<usuario>.github.io/<repositorio>/`.

Atenção: em contas gratuitas, o Pages de um repositório público é público. Veja a seção de segurança abaixo.

## Como editar o conteúdo

Todo o conteúdo está no bloco `<script>` do `index.html`, em estruturas de dados no começo do arquivo. Não é preciso mexer na lógica da página para editar texto.

| Estrutura | O que controla |
|---|---|
| `PHASES` | As 4 fases: nome, intervalo de passos, cor e resumo |
| `STEPS` | Os 13 passos |
| `TOOLS` | Tabela da página "Acessos e ferramentas": nome, para quê, passos e link |
| `GLOSS` | Glossário |
| `MEETINGS` | Plano de encontros |

Campos de cada item de `STEPS`:

| Campo | Uso |
|---|---|
| `n` | Número do passo |
| `phase` | Fase a que pertence (1 a 4) |
| `title`, `lead` | Título e frase de abertura |
| `tool`, `access` | Ferramenta e acesso necessário (aparecem no topo do passo) |
| `links` | Botões de link, no formato `[["Texto", "https://..."]]` |
| `path`, `doPath` | Caminho de pastas ou telas, mostrado em etiquetas |
| `doList` | Lista "O que fazer". Aceita HTML simples (`<b>`, `<span class='ui'>`, `<a>`) |
| `check` | Itens de "Confira antes de seguir" (viram caixas de marcar) |
| `attn` | "Pontos de atenção" |
| `todo` | Aviso tracejado "A completar" para pendências |
| `cred` | Quando `true`, mostra o bloco de acesso do Bigodão (sem usuário e senha) |

Para adicionar um passo, inclua um novo objeto em `STEPS` com os campos acima. O menu, a numeração, o progresso e a navegação entre passos são gerados a partir da lista.

Ao mudar a ordem ou a quantidade de passos, revise também: o texto das fases em `PHASES`, a coluna "Passos" em `TOOLS`, o `MEETINGS` e as referências cruzadas no texto (por exemplo, "o passo 8 cuida disso" no passo 7).

## Como a página funciona

- **Navegação:** um passo por vez, com menu lateral, botões anterior e próximo e atalho de continuar de onde parou. Os endereços usam o hash da URL (`#visao-geral`, `#acessos`, `#encontros`, `#passo-1` a `#passo-13`, `#glossario`), então cada passo pode ser enviado por link.
- **Progresso:** salvo no `localStorage` do navegador, na chave `tutorial-ld-v1`. É individual por navegador e aparelho e não sincroniza entre pessoas. Se o navegador bloquear o armazenamento, a página avisa no menu.
- **Tema:** segue o claro ou escuro do sistema. As cores ficam em variáveis CSS no começo do arquivo (`:root`).
- **Acessibilidade:** link para pular ao conteúdo, foco enviado ao conteúdo a cada troca de passo, título da aba que muda por passo, menu que fecha com a tecla Esc, contraste revisado nos dois temas e respeito a `prefers-reduced-motion`.
- **Celular:** o menu vira uma gaveta aberta pelo botão "Menu".

## Segurança dos dados

- **Não coloque logins, senhas ou tokens neste repositório.** O login do Bigodão é enviado pelo Slack ou passado durante o encontro, e a página apenas informa isso.
- A página mostra links internos (Assets, Bigodão, planilha de pagamentos) e descreve o fluxo de trabalho. Se o repositório for público, isso fica visível a qualquer pessoa com o endereço. Confirme com o time se é aceitável antes de publicar, ou use um repositório privado com a hospedagem adequada.

## Links usados no tutorial

- Assets: https://arco-dam.eos.woodwing.cloud/app/#/ssoOIDCLogin
- Divisor de PDF: https://divisor-pdf.netlify.app/
- Biblioteca de códigos do LD: https://luizsb.github.io/Biblioteca_LD/
- Bigodão: https://bigodao.sae.digital/livro-digital/chapters
- Planilha de pagamentos (GOPP - DIGITAL - Solicitações de Pagamento): https://docs.google.com/spreadsheets/d/1ghghzTj_Ybm2mTqaAm_2YeJcfODaSWPTyiln_kNNYsM/edit?usp=sharing

## Pendências conhecidas

Marcadas como "A completar" na própria página:

- [ ] Passo 5: como abrir o DIA LD, com link, e o que a pessoa deve ver quando estiver pronto.
- [ ] Passo 10: quem faz o cotejo e como o capítulo é encaminhado.
- [ ] Passo 11: o que fazer com ajustes do cotejo que não fazem sentido.
- [ ] Links do DIA LD, da pasta do Drive e da planilha de controle do volume na página "Acessos e ferramentas".
- [ ] Seção de problemas comuns por passo ("Se der ruim").
- [ ] Página de pré-requisitos (o que a pessoa precisa saber antes de começar).
- [ ] Prints das ferramentas nos passos.
- [ ] Datas reais do plano de encontros.

## Trabalhando em dupla

O Git não faz edição simultânea em tempo real. Para evitar conflitos:

1. Dê `git pull` antes de começar a editar.
2. Trabalhe em uma branch por assunto (por exemplo, `passo-10-cotejo`) e abra um pull request.
3. Combine quem mexe em qual passo, já que todo o conteúdo está num arquivo só.
4. Faça commits pequenos e com mensagem que diga o que mudou (por exemplo, "Passo 5: adiciona link do DIA LD").

## Créditos e uso das marcas

O logo da SAE Digital e o personagem Digi são materiais da marca, usados aqui como apoio interno ao treinamento do time.
