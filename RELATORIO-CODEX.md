# Correção do curso INTELECTO v2 — rodada 4 — 13/11/2026

Escopo: somente `/home/nmaldaner/projetos/intelecto-v2-curso`. Reli a skill v7.2 (`SKILL.md`, `references/ESQUEMA.md`, `references/LICOES.md`), o `CLAUDE.md` e o relatório anterior. Consultei o README, as seções `#funciona` e `#mercearia` do guia, a página da mercearia, os cinco `exemplos/*.md` e seus JPGs no INTELECTO v2, além do README e do funcionamento descrito da caixa-do-agente. Editei os JSON em `conteudo/pt/`, gerei a foto em `assets/img/hero/mercearia.jpg` e regenerei o HTML. Não fiz Git, publicação, Telegram, tradução nem chamada de API paga. Docker não foi executado neste sandbox.

## Novo conteúdo pedido pelo dono

| Pedido | O que mudou | Onde |
|---|---|---|
| Aula 9, mercearia | Criei “Monte o seu: a mercearia e o meu-assistente.md” com diagrama escolher → baixar .md → entregar ao agente; legenda ✅/🟡/➕; 144 ingredientes de 12 projetos em 8 corredores; cinco exemplos e seus totais conferidos nos arquivos `.md`. | `conteudo/pt/aulas/09-mercearia.json` |
| Conteúdo do arquivo | Expliquei que ✅ cita o arquivo existente, 🟡 mostra o que falta e ➕ indica a peça em que acrescentar. As regras finais cobrem um item por vez, teste em `tests/`, `python3 -m pytest -q`, trava preservada, segredos no cofre, testes sem API real, tabela do README atualizada e “pronto” só com saída dos testes. | Aula 9, diagrama e passos |
| Entrega e práticas | Incluí a cópia do exemplo do README, o pedido para Claude Code/Codex, uma prática de leitura sem agente nem custo e uma prática opcional para **um** item ➕. A segunda exige testes passando em número maior que antes e conferência do código feito pelo agente; informa uso da assinatura ou créditos. A caixa com patch revisado aparece como caminho mais seguro. | Aula 9, código, texto e práticas |
| Quiz e fontes | Três perguntas sobre ➕, um item por vez com teste e arquivo de um ✅; links para a mercearia, os cinco exemplos `.md` e a caixa-do-agente. | Aula 9, quiz e links |
| Imagem | Criei fotografia editorial 1536×1024 de carrinho com cartões em branco apontando para uma folha, com humanoide genérico ao lado, luz neutra e sem texto. Usei `image_gen` pela assinatura e salvei como JPG. | `assets/img/hero/mercearia.jpg` |
| Funcionamento interno | Acrescentei seis passos curtos: canal → “lembre que” direto para a memória → contexto → cérebro → ferramenta pela trava → resposta e auditoria. | `conteudo/pt/aulas/01-jarvis-seguro.json`, seção “O caminho de uma mensagem” |
| Contagem | Atualizei o topo para 9 aulas, o número visível e a descrição da sequência; o gerador inclui a aula 9 pela ordem dos arquivos JSON. | `conteudo/pt/curso.json` e HTML gerado |

Os totais lidos nos exemplos foram: Jarvis 12 (✅5, 🟡3, ➕4); Atendente 12 (✅2, 🟡2, ➕8); Programador 12 (✅4, 🟡0, ➕8); Local e privado 10 (✅5, 🟡1, ➕4); Casa com voz 12 (✅2, 🟡0, ➕10). No Jarvis, o item ✅ Telegram cita `intelecto/canais/telegram.py`.

## Sete defeitos do terceiro revisor

| # | Correção | Onde |
|---|---|---|
| 1 | Ubuntu tem bloco copiável com `sudo apt install -y docker.io`, `sudo usermod -aG docker $USER`, instrução para sair e entrar de novo e `docker run --rm hello-world`; o manual oficial ficou nos links extras. macOS aponta para Docker Desktop. | Aula 6, código e links |
| 2 | Separei “Ubuntu · instalar Docker” de “macOS · instalar Docker Desktop”, sem rótulo misto. | Aula 6, código |
| 3 | A abertura da aula 7 diz que precisa do Docker da aula 6 e que só as aulas 6–7 o pedem. | Aula 7, lead e código |
| 4 | Adicionei bloco opcional com o comando do README da caixa para Claude Code; está rotulado “não executado neste curso”, informa a chave e o envio da cópia pela rede e explica `--rede`, `--env`, `npx`, `-p` e `--dangerously-skip-permissions`. A promessa do topo agora diz “aprende como deixar agentes trabalharem numa cópia”. | Aula 7, código e seção “O que faz o exemplo opcional”; `curso.json` |
| 5 | Mostrei o diff real **completo**, inclusive a linha `diff -ruN`, os cabeçalhos datados e `+teste`; expliquei que 1969 em `antes/nota.txt` é normal para arquivo novo. | Aula 7, aba do patch e passo “Patch” |
| 6 | O comando copiável começa em `cd ~ && ~/caixa-do-agente/caixa.sh ...`; a saída real começa em `▶ 1/3 CRIAR`, sem `./caixa.sh` na aba. O texto explica que o patch é salvo em `~`, de onde o comando rodou. | Aula 7, código e aba de saída |
| 7 | Expliquei as três políticas em ambas as aulas: `perigosos` é padrão; `sempre` pergunta antes de **qualquer** comando, inclusive `ls` e `cat`; `nunca` deixa leitura conhecida rodar e recusa o que precisaria de aprovação. Bloqueados não rodam em nenhuma. Conferi a semântica em `intelecto/seguranca/aprovacao.py`. | Aulas 2 e 4, passos; aula 4, resumo |

## Sugestões incorporadas

| Sugestão | O que mudou | Onde |
|---|---|---|
| Abertura | Completei o risco: erro ou texto malicioso escondido num site pode levar a IA a apagar uma pasta ou enviar senha para fora. O topo usa “caixa”; notas sobre macOS e Windows ficaram em “Para quem é”. | `curso.json`, `inicio` |
| Aula 1 | A demo diz o texto “meu nome é Ana e moro em Curitiba”. Se Python for anterior a 3.10, o aluno recebe a orientação “use Ubuntu 22.04 ou mais novo”. | Aula 1, passos |
| Aula 2 | Acrescentei `sudo apt install -y python3-cryptography` como opção Ubuntu para Fernet e expliquei a falha `externally-managed-environment` do pip no Ubuntu 24.04. Tornei os distratores do quiz 2 plausíveis. | Aula 2, passos, código e quiz |
| Aula 5 | Instrução para abrir o bot pelo link `t.me/nome_bot` enviado por @BotFather; `/sim` e `/nao` expiram após 120 segundos, conforme `intelecto/canais/telegram.py`. | Aula 5, passos e prática |
| Aula 7 | Bloco copiável `rsync --version` e `patch --version`, ferramentas esperadas no Ubuntu. | Aula 7, código |
| Aula 8 | `cat servico/intelecto-telegram.service` vem antes do `cp`, para conferir `WorkingDirectory` e `ExecStart`. | Aula 8, código |

## Comandos executados e saídas observadas

Conferência dos cinco exemplos: li as linhas `**Total: …**` e as entradas `**No INTELECTO v2**` dos arquivos `exemplos/*.md`. Também conferi os cinco JPGs locais: todos são JPEG 1400×788. Para a nova imagem, a conversão do PNG gerado para JPG informou `(1536, 1024)`; `file assets/img/hero/mercearia.jpg` confirmou `1536x1024`.

Primeiro portão, antes de dividir o parágrafo da aula 7:

```text
$ python3 gerar.py && python3 validar.py
9 aulas + index geradas (pt, motor 7.14.23), 0 erros
FALHOU:
 - caixa-projeto: parágrafo com mais de 75 palavras
```

A menor correção foi separar a explicação do patch em dois parágrafos; registrei a falha em `FALHAS.md`. Após ajustar também os ícones da aula 9 para chaves existentes no motor, acrescentar o pedido de um único item ➕ e os links dos cinco exemplos, rodei o portão final:

```text
$ python3 gerar.py && python3 validar.py
9 aulas + index geradas (pt, motor 7.14.23), 0 erros
OK: 9 aulas + index
```

Não executei `validar.py --links` nem `conferir-tela`, conforme o portão desta rodada. As saídas de Docker mostradas na aula 7 são as capturas reais fornecidas pelo pedido e pela rodada 3; não são execução nova neste sandbox. O exemplo opcional que invoca Claude Code na caixa foi documentado, não executado.
