# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## O que é este repositório

Não é um projeto de software. É um sistema pessoal de **geração diária de ideias de conteúdo** para um criador multifacetado — desenvolvedor de software, mas também praticante de jiu-jitsu, frequentador de academia, pai de família, estudante de inglês, interessado em ciência (física/biologia/química), mundo militar/policial e automotivação. O objetivo é documentar a jornada real (profissional e pessoal) para construir audiência. Não há build, testes, lint ou dependências — todo o trabalho é gerar e versionar texto em Markdown.

Tudo (instruções, conteúdo e respostas) é escrito em **português brasileiro**.

## Arquivos

- `prompt.md` — A especificação completa do sistema: persona, perfil/interesses do usuário, filosofia, categorias permitidas, regras das ideias, formato exato de saída e o passo de versionamento automático. É a fonte da verdade; siga-o literalmente.
- `history.md` — Estado persistente. Registro de todos os temas já sugeridos, usado para evitar repetição. Cada entrada tem `Data: / Tema: / Categoria:`.

## Fluxo principal (rodar uma vez por dia)

O gerador roda **uma única vez por dia**, no início do dia, e produz **6 vídeos de uma só vez** (não 3 execuções). Os blocos Manhã/Tarde/Noite são só os períodos de publicação. Ao gerar conteúdo:

1. **Leia `history.md` primeiro** e analise todos os temas já sugeridos.
2. **Não repita** temas anteriores nem reformule a mesma ideia — busque ângulos novos e **varie entre as áreas** (não concentre tudo em programação; misture técnico e pessoal).
3. Cada ideia deve ser **genuinamente interessante** e render um vídeo de **no máximo 30 segundos**.
4. Gere a resposta no formato exato de `prompt.md`: 6 vídeos em Manhã/Tarde/Noite (2 cada), cada um com `Tema / Categoria / Formato / Gancho / Roteiro resumido / CTA`, seguidos da **Justificativa**.
5. Sinta-se livre para introduzir temas/categorias novos quando forem realmente interessantes e alinhados ao perfil.

## Versionamento automático (sem copiar/colar manual)

Após gerar os 6 vídeos, **não peça ao usuário para copiar nada**. Você mesmo deve:

1. **Anexar ao final** de `history.md` as 6 novas entradas no formato `Data: / Tema: / Categoria:` (use a data atual do ambiente; não reordene nem reescreva entradas existentes).
2. `git add -A`
3. `git commit -m "conteúdo: ideias de <data>"`
4. `git push`

O remote é `origin` (`github.com:zevitagem/content-ideas.git`), branch `main`. O repositório já está configurado com `core.sshCommand` apontando para a chave `~/.ssh/id_ed25519_nanicas`, então `git push` autentica sozinho — não é preciso configurar SSH a cada execução.
