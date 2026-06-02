# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## O que é este repositório

Não é um projeto de software. É um sistema pessoal de **geração diária de ideias de conteúdo** para um criador multifacetado — desenvolvedor de software, mas também praticante de jiu-jitsu, frequentador de academia, pai de família, estudante de inglês, interessado em ciência (física/biologia/química), mundo militar/policial e automotivação. O objetivo é documentar a jornada real (profissional e pessoal) para construir audiência. Não há build, testes, lint ou dependências — todo o trabalho é gerar e versionar texto em Markdown.

Tudo (instruções, conteúdo e respostas) é escrito em **português brasileiro**.

## Arquivos

- `prompt.md` — A especificação completa do sistema: persona, perfil/interesses do usuário, filosofia, categorias permitidas, regras das ideias, formato exato de saída e o passo de versionamento automático. É a fonte da verdade; siga-o literalmente.
- `history.md` — Estado persistente. Registro de todos os temas já sugeridos, usado para evitar repetição. Cada entrada tem `Data: / Tema: / Categoria:` seguida de um bloco `Observações:` com `- Otimista:` e `- Pessimista:` (ver `prompt.md` como fonte da verdade do formato). Para dedup/balanceamento, lê-se só a **janela recente (90 dias)**; ao passar de ~200 entradas, as antigas migram para `history-archive.md` (commit separado).

## Fluxo principal (rodar uma vez por dia)

O gerador roda **uma única vez por dia**, no início do dia, e produz **6 vídeos de uma só vez** (não 3 execuções). Os blocos Manhã/Tarde/Noite são só os períodos de publicação. Ao gerar conteúdo:

0. **Idempotência:** descubra a data com `date +%F` e cheque se o `history.md` já tem entrada de hoje; se tiver, não gere de novo automaticamente — avise e pergunte antes.
1. **Leia `history.md` primeiro** e analise todos os temas já sugeridos.
2. **Não repita** temas anteriores nem reformule a mesma ideia — busque ângulos novos e **varie entre as áreas** (não concentre tudo em programação; misture técnico e pessoal).
3. Cada ideia deve ser **genuinamente interessante** e render um vídeo vertical (9:16, multi-plataforma) de **no máximo 30 segundos** (~70–90 palavras), com **tom provocativo/questionador** — gancho que abre com opinião forte, contra-senso ou pergunta incômoda (ver `prompt.md`).
4. Gere a resposta no formato exato de `prompt.md`: 6 vídeos em Manhã/Tarde/Noite (2 cada), cada um com `Tema / Categoria / Formato / Gancho / Roteiro resumido / CTA / Observações (Otimista e Pessimista)`, seguidos da **Justificativa**.
5. Sinta-se livre para introduzir temas/categorias novos quando forem realmente interessantes e alinhados ao perfil.
6. **Para cada tema, gere um bloco `Observações:`** com uma possível resposta em pelo menos 2 perspectivas (Otimista e Pessimista; cética quando couber) — substancial e honesta, com trade-offs reais. Serve pra o usuário comparar com a visão dele e ter munição em temas que não domina. Vai tanto no vídeo quanto gravado no `history.md`.

## Versionamento automático (sem copiar/colar manual)

Após gerar os 6 vídeos, **não peça ao usuário para copiar nada**. Você mesmo deve:

1. **Anexar ao final** de `history.md` as 6 novas entradas no formato exato do arquivo (Data/Tema/Categoria + bloco Observações com Otimista/Pessimista; data via `date +%F` em ISO). Apenas append — não reordene nem reescreva entradas existentes. Antes, rode `git pull --rebase origin main`.
2. `git add -A`
3. `git commit -m "conteúdo: ideias de <data>"`
4. `git push`

O remote é `origin` (`github.com:zevitagem/content-ideas.git`), branch `main`. O repositório já está configurado com `core.sshCommand` apontando para a chave `~/.ssh/id_ed25519_nanicas`, então `git push` autentica sozinho — não é preciso configurar SSH a cada execução. Ainda assim, o push pode falhar por rede ou rejeição do remote (non-fast-forward); nesse caso, reporte o erro e **não** use `--force`.
