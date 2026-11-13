# Seu Jarvis seguro: INTELECTO v2 e caixa-do-agente

**🇧🇷 Português · 🇺🇸 [English](https://inematds.github.io/intelecto-v2-curso/en/) · 🇪🇸 [Español](https://inematds.github.io/intelecto-v2-curso/es/)**

Curso aberto e gratuito do INEMA.CLUB (formato INEMA Learning v7.2), em 9 aulas: **https://inematds.github.io/intelecto-v2-curso/**

Você monta um assistente de IA só seu, que roda no seu computador, lembra de você e só faz o perigoso com o seu OK;
aprende como deixar agentes de programação trabalharem numa cópia do projeto, sem as suas senhas, aplicando só o que
revisou; e monta a versão do seu jeito na mercearia, que gera o `meu-assistente.md` para o agente construir.

- Projeto: https://github.com/inematds/intelecto-v2 · guia: https://inematds.github.io/intelecto-v2/guia/
- Kit da caixa: https://github.com/inematds/caixa-do-agente · guia: https://inematds.github.io/caixa-do-agente/guia/
- Versão anterior do curso (v1): https://inematds.github.io/intelecto-curso/

## Como o curso é feito
Conteúdo em `conteudo/<pt|en|es>/` (JSON) → `python3 gerar.py [--lang en|es]` gera o HTML estático →
`python3 validar.py --links` + `conferir-tela.cjs` são o portão. Não edite o HTML gerado à mão.
