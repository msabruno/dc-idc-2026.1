# Postagens — Disciplina de Divulgação Científica (2026.1)

Este repositório reúne as postagens das equipes do semestre **2026.1** da disciplina de
Introdução à Divulgação Científica. Ele é importado automaticamente pelo site principal
([`emanueles/dc-idc`](https://github.com/emanueles/dc-idc)) — você não precisa mexer no site,
só na sua postagem.

A lista de equipes está em [`EQUIPES.md`](EQUIPES.md), neste mesmo repositório.

## O que fazer

**A pasta da sua equipe já existe neste repositório** (`equipe01/` até `equipe16/`, na raiz),
com um `index.md` de template dentro. **Não crie uma pasta nova** — isso evita erro de nome
(maiúscula/minúscula, número errado etc.). Só edite o que já está lá:

1. Faça um fork **deste** repositório (`emanueles/dc-idc-2026.1`) para o seu usuário no GitHub.
2. Abra a pasta `equipeXX/` correspondente ao número da sua equipe (veja
   [`EQUIPES.md`](EQUIPES.md)) e edite o `index.md` que já está lá. O preâmbulo já vem com o
   `slug` no formato certo — só troque o resto:

   ```
   ---
   title: Título do Post                     # <- Altere o título
   description: Breve descrição da postagem  # <- Altere a descrição
   slug: equipeXX-temaprincipal              # <- Só troque "temaprincipal", mantenha o prefixo
   date: 2026-01-01 00:00:00+0000            # <- Coloque a data do dia que inseriu o conteúdo
   image: cover.jpg                          # <- Nome do arquivo de imagem com a capa (adicione à pasta)
   categories:
       - Post                                # <- Deixe como está
   tags:
       - Tema do Vídeo                       # <- Altere para o tema do vídeo
       - Tema do Podcast                     # <- Altere para o tema do episódio. Se for igual ao de cima, remova essa linha
   weight: 1                                 # <- Deixe como está
   draft: true                               # <- IMPORTANTE: troque para false (ou apague a linha) quando terminar
   ---
   ```

3. Adicione os links do vídeo no YouTube e do episódio do podcast, além da imagem de capa e do
   áudio (mp3) na mesma pasta.
4. **Antes de abrir o Pull Request, confira se tirou o `draft: true`** — enquanto ele estiver
   lá, a postagem não aparece no site publicado.
5. Commit, push para o seu fork e abra um Pull Request **para `emanueles/dc-idc-2026.1`**
   (não para `emanueles/dc-idc`).

> **Áudio/vídeo:** este repositório usa Git LFS (veja `.gitattributes`). Ainda assim, prefira
> exportar o podcast em mono e taxa de bits moderada (96–128 kbps).

## Guia completo (fork, commit, push, Pull Request)

Passo a passo detalhado, com os dois caminhos (navegador ou linha de comando) e como resolver
problemas comuns:
[`guia-pull-request.md`](https://github.com/emanueles/dc-idc/blob/master/guia-pull-request.md)
(no repositório do site — os comandos lá já usam este repositório, `dc-idc-2026.1`, como
exemplo).

**O Pull Request é o que conta como entrega.** Commits que ficam só no seu computador não
chegam até o professor.