# Correção do curso INTELECTO v2 — 13/11/2026

Escopo: apenas `/home/nmaldaner/projetos/intelecto-v2-curso`. Li a skill v7.2, `ESQUEMA.md`, `LICOES.md`, `CLAUDE.md`, o código e os guias do INTELECTO v2 e da caixa-do-agente antes das edições. Não fiz commit, push, publicação, tradução ou chamada de API paga. O HTML foi regenerado dos JSON.

## Defeitos do parecer

| # | O que mudou ou limite | Onde |
|---|---|---|
| 1 | A abertura fala com “você” sobre o medo de apagar arquivos e expor senhas, depois apresenta INTELECTO e caixa. Retirei a promessa de agente sempre sem rede/senhas e troquei 68/18 por resultados compreensíveis. Mantive os nomes no título. | `conteudo/pt/curso.json` |
| 2 | A prática principal agora usa o `~/intelecto-v2` da aula 1, monta `intelecto-v2-testes` com `docker build -t intelecto-v2-testes caixa/` e executa `./caixa.sh ~/intelecto-v2 --imagem intelecto-v2-testes -- python3 -m pytest -q -p no:cacheprovider`. `~/meu-projeto` ficou opcional. | aula 7 |
| 3 | O bloco de aplicação usa `patch -p1` com o caminho absoluto do patch revisado. A aula explica que `--aplicar` inicia outra rodada e pergunta antes de copiar o resultado novo. | aula 7 |
| 4 | Acrescentei o comando de Claude Code na caixa com `--rede --env ANTHROPIC_API_KEY`. A aula explica que `.env`, `.pem` e `~/.ssh` ficam fora, o original não muda sem aplicação, há tetos de recursos e, com rede, o agente pode enviar o conteúdo da cópia. O comando é identificado como exemplo, não foi executado. | aula 7 |
| 5 | A aula 2 traz o instalador Linux oficial do Ollama, o aplicativo de macOS em ollama.com, tabela máquina→modelo e a ressalva sobre llama3.2 no corpo antes do quiz. Os tamanhos vieram dos manifestos locais: 2.019.392.628 bytes e 23.938.333.115 bytes; não estimei RAM. **Limite:** `ollama list` e `ollama show` foram tentados, mas o sandbox bloqueou a conexão local, então os números não são apresentados como saída desses comandos. | aula 2 |
| 6 | A aula 1 usa `cd ~ && git clone ... && cd intelecto-v2`, com `git` nos pré-requisitos Linux/macOS. A aula 2 só entra com `cd ~/intelecto-v2` e remete à aula 1 se faltar o clone. | aulas 1 e 2 |
| 7 | As sete respostas do `configurar` estão descritas uma a uma; a aula informa que ele lista modelos já instalados e sugere um. | aula 2 |
| 8 | O painel traz a saída **completa** obtida de `verificar` no ensaio isolado. Somente o caminho temporário foi normalizado para `~/.intelecto2`, com aviso explícito; o provedor do ensaio foi `mock`. | aula 2 |
| 9 | `MEMORY.md` é apresentado como importação única da primeira execução; fatos posteriores entram por “lembre que…” na conversa. Incluí Ctrl+O, Enter, Ctrl+X para salvar no nano. | aula 3 |
| 10 | As aulas 4 e 8 mostram linhas JSON reais de `auditoria -n 20` e explicam `comando`, `classe`, `rodou` e `decisao`. | aulas 4 e 8 |
| 11 | A prática usa `[na caixa, saída 0]`, `rode: ls /trabalho` e `rode: pwd` → `/trabalho` como prova conferível. Incluí link oficial de instalação do Docker, `sudo usermod -aG docker $USER`, novo login e `docker run --rm hello-world`. A saída da caixa está **rotulada como exemplo esperado**, pois o Docker não pôde ser executado aqui. | aula 6 |
| 12 | `mkdir -p ~/.config/systemd/user` vem antes do `cp` do serviço. | aula 8 |
| 13 | A aula diz que `auditar.py` lê Claude Code, Codex e DeepSeek Harness instalados e que uma nota baixa sem eles é normal. Explica harness e sandbox. | aula 7 |
| 14 | Há passo a passo de `@BotFather`, `/newbot`, nome, token secreto, `/id`, campo `telegram_donos` e a mensagem real que cita `config.json`. A prática pede `rode: echo teste > nota.txt`, que exige aprovação. | aula 5 |
| 15 | Expliquei os termos na primeira ocorrência útil: container Docker, patch, memória SQLite/FTS5, Fernet, OpenRouter, executor, systemd, journalctl, sandbox, harness, pytest, @BotFather, token, id e “saída 0”. | aulas 1–8 |
| 16 | Conferi os quizzes contra o texto anterior. Corrigi especialmente a pergunta da aula 7 que dependia da nota 7,5 sem mostrá-la antes. O validador passou com 3 perguntas por aula. | aulas 1–8 |
| 17 | Substituí as fotos das aulas 1, 2 e 8 por imagens `image_gen` da assinatura: dono impede o acesso do assistente, mão encaixa o modelo local, dona lê o registro antes de ligar o assistente. Luz neutra, sem texto/logos; figuras 2 e 8 foram refeitas para humanoide realista. | `assets/img/hero/{jarvis-seguro,instalar-conversar,seu-jarvis}.jpg` |

Para a tabela da aula 2, `gerar.py` passou a emitir uma tabela HTML como bloco, sem envolvê-la em `<p>`. Os arquivos gerados estão em `index.html` e `aulas/*/index.html`. Registrei em `CLAUDE.md` e `FALHAS.md` a falha do meu script de edição: inseri uma seção e depois acessei o quiz por índice antigo; corrigi localizando a seção pelo tipo.

## Comandos executados e saídas observadas

### Ollama e tamanhos

Executei `ollama list; ollama show llama3.2; ollama show qwen3.6:35b-a3b`. Os três comandos devolveram a mesma falha de conexão; trecho literal:

```text
Error: Head "http://127.0.0.1:11434/": dial tcp 127.0.0.1:11434: socket: operation not permitted
```

Li os manifestos instalados em `~/.ollama/models/manifests/registry.ollama.ai/library/` por script Python local. A soma dos tamanhos de camadas impressa foi:

```text
llama3.2/latest: total 2019392628
qwen3.6/35b-a3b: total 23938333115
```

São tamanhos dos arquivos descritos nos manifestos locais, não medições de RAM nem a saída de `ollama show`.

### INTELECTO em estado isolado

Usei `INTELECTO_HOME=/tmp/intelecto-curso-demo.dqwv9S`, `PYTHONDONTWRITEBYTECODE=1` e executei `python3 -m intelecto configurar --nao-interativo --provedor mock --modelo mock --nome Teste`; em seguida, uma conversa por pipe com pedidos de memória e comando, `python3 -m intelecto auditoria -n 20`, `python3 -m intelecto verificar` e `python3 -m intelecto demo`. A aprovação por pipe foi recusada literalmente:

```text
[aprovação] 'echo x > y.txt' precisa de OK (substituição de comando ou redirecionamento para arquivo); entrada não é um terminal → recusado
```

O `verificar` imprimiu, por inteiro:

```text
[OK] Python 3.12.3 (precisa 3.10+)
[OK] SQLite com FTS5 (memória)
[OK] config em /tmp/intelecto-curso-demo.dqwv9S/config.json
[INFO] cofre: fernet (Fernet)
tudo certo
```

As linhas de auditoria copiadas nas aulas 4 e 8 vieram dessa execução:

```json
{"ts": "2026-11-13T03:37:49+00:00", "tipo": "comando", "comando": "echo x > y.txt", "classe": "aprovar", "rodou": false, "decisao": "o dono não aprovou"}
{"ts": "2026-11-13T03:38:00+00:00", "tipo": "comando", "comando": "ls", "classe": "livre", "rodou": true, "decisao": "livre (só leitura)"}
```

`python3 -m intelecto demo` terminou com este bloco real, usado na aula 1:

```text
Auditoria desta demonstração:
  livre     rodou=True  ls  (livre (só leitura))
  aprovar   rodou=False echo teste > nota.txt  (o dono não aprovou)
  bloqueado rodou=False rm -rf /  (bloqueado: apagar pasta do sistema ou a pasta pessoal)
```

### Docker, auditor e patch

`docker version` imprimiu o cliente `Version: 28.5.1` e falhou ao acessar o daemon:

```text
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.51/version": dial unix /var/run/docker.sock: connect: operation not permitted
```

Por esse limite, não executei `docker run --rm hello-world`, `docker build`, `caixa.sh` nem `bash testes/teste.sh`. Os resumos `67 passed, 1 skipped` e `TUDO OK (18/18)` presentes na aula 7 são resultados **documentados nas fontes**, não saídas obtidas nesta sessão. O comando de agente de nuvem também é exemplo; não carreguei chave nem usei API.

Executei `python3 /home/nmaldaner/projetos/caixa-do-agente/auditar.py /home/nmaldaner/projetos/intelecto-v2` em leitura. Trecho da saída real:

```text
Harness encontrados: Claude Code, Codex
[FALTA] Caixa (sandbox): Claude Code sandbox=desligado; Codex sandbox_mode=danger-full-access
NOTA DO HARNESS: 7.5/10  (o modelo não entra na conta)
```

Testei `patch -p1` somente em um projeto descartável em `/tmp`, com um patch criado ali:

```text
patching file prova.txt
depois
```

Não apliquei nenhum patch aos repositórios fonte. Um parser HTML local confirmou `tabelas HTML na aula 2: 1`.

### Imagens

As imagens finais foram geradas pelo `image_gen` da assinatura e salvas em `assets/img/hero/` como JPG 1536×1024. Prompts finais: (1) dono segura chave e impede humanoide de tocar na pasta; (2) humanoide adulto realista observa uma mão encaixar um módulo de modelo local no laptop; (8) dona confere folha de auditoria antes de acionar interruptor ao lado de humanoide realista. Todos pediram luz natural neutra, fotografia editorial, sem texto, marca ou logotipo.

### Portão final

Comando executado depois das edições de conteúdo e imagens:

```text
$ python3 gerar.py && python3 validar.py
8 aulas + index geradas (pt, motor 7.14.23), 0 erros
OK: 8 aulas + index
```

Não executei `--links` nem `conferir-tela`, conforme solicitado.
