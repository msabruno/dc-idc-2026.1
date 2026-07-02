# Guia: como enviar sua postagem usando Fork e Pull Request

Este guia explica, passo a passo, como contribuir com o repositório da disciplina do jeito
correto. O erro mais comum é fazer as alterações **apenas no seu computador** e achar que a
entrega foi feita. Não foi. Enquanto você não **enviar (push)** as alterações e **abrir um
Pull Request**, ninguém consegue ver o seu trabalho.

> **Este guia é do semestre 2026.1.** Você vai trabalhar no repositório `dc-idc-2026.1`, e não
> no repositório principal do site (`dc-idc`). Cada semestre tem seu próprio repositório de
> conteúdo — não faça fork do repositório errado.

Leia a seção de conceitos e depois siga **um** dos dois caminhos: pelo navegador (mais simples,
bom para arquivos pequenos) ou pela linha de comando (necessário para o áudio, que pode passar
de 25 MB).

---

## 1. Os conceitos em uma frase cada

- **Repositório original (upstream):** o repositório do semestre, `emanueles/dc-idc-2026.1`.
  Você **não** tem permissão para alterá-lo diretamente.
- **Fork:** uma cópia do repositório original feita **na sua conta** do GitHub. É nela que
  vocês trabalham.
- **Clone:** trazer o repositório da nuvem (GitHub) para o seu computador, para editar os
  arquivos localmente.
- **Commit:** registrar um conjunto de alterações, com uma mensagem que descreve o que mudou.
  Um commit fica só no seu computador até você fazer o push.
- **Push:** enviar os commits do seu computador para o seu fork no GitHub.
- **Pull Request (PR):** o pedido formal de "por favor, incorpore as minhas alterações no
  repositório original". **É este o passo que conta como entrega.**

O fluxo completo é sempre:

```
Fork  →  (editar)  →  Commit  →  Push  →  Pull Request
```

Se qualquer um dos últimos três passos faltar, a entrega não chegou ao destino.

---

## 2. Passo comum: fazer o fork (uma vez por equipe)

1. Acesse o repositório original: `https://github.com/emanueles/dc-idc-2026.1`
2. Clique no botão **Fork**, no canto superior direito.
3. Confirme a criação do fork. Agora existe uma cópia em `github.com/SEU-USUARIO/dc-idc-2026.1`.

> Apenas **uma pessoa** da equipe precisa fazer o fork. As outras podem ser adicionadas como
> colaboradoras desse fork (em *Settings → Collaborators*) ou contribuir por outros meios
> combinados pela equipe.

Depois do fork, siga um dos dois caminhos abaixo.

---

## 3. Caminho A — pelo navegador (arquivos até 25 MB)

Bom para textos, imagens e o `README`. **Não serve** para o áudio se ele passar de 25 MB — e,
mesmo abaixo disso, o site do GitHub **não** ativa o Git LFS automaticamente ao fazer upload
pelo navegador. Isso não é problema para arquivos pequenos (ficam como blob normal do Git), mas
é por isso que arquivos grandes precisam ir pelo Caminho B.

1. Entre no **seu fork** (`github.com/SEU-USUARIO/dc-idc-2026.1`), e não no repositório original.
2. Para editar um arquivo existente: abra o arquivo e clique no ícone de **lápis** (Edit).
3. Para adicionar um arquivo (imagem da capa, por exemplo): clique em **Add file → Upload files**
   e arraste os arquivos.
4. Ao terminar cada mudança, role até **Commit changes**, escreva uma mensagem curta e clara
   (ex.: "Adiciona capa do podcast em 1024x1024") e confirme.
5. Quando **todas** as alterações estiverem no seu fork, abra o Pull Request (seção 5).

---

## 4. Caminho B — pela linha de comando (necessário para o áudio, até 100 MB)

Use se o `.mp3` passar de 25 MB, ou se preferir trabalhar no terminal.

**4.1. Instalar o Git LFS (uma vez por computador)**

Este repositório versiona áudio e vídeo (`.mp3`, `.mp4`, `.mpeg`, `.mpg`, `.wav`, `.mov`) usando
[Git LFS](https://git-lfs.com/), configurado no `.gitattributes` que já vem no repositório. Você
**precisa instalar o Git LFS antes de clonar ou adicionar qualquer arquivo de áudio/vídeo** —
sem isso, o Git trata o arquivo como um blob normal, gigante, e o push acaba falhando ou
excedendo os limites do GitHub.

Instale o Git LFS uma vez por computador (não por equipe nem por repositório):

- **macOS** (com [Homebrew](https://brew.sh/)): `brew install git-lfs`
- **Windows**: baixe o instalador em [git-lfs.com](https://git-lfs.com/) — se você já tem o
  "Git for Windows" instalado, o Git LFS provavelmente já vem junto; confira com `git lfs version`.
- **Linux** (Debian/Ubuntu): `sudo apt install git-lfs`

Depois de instalar, rode **uma única vez** (vale para todos os repositórios no seu computador):

```bash
git lfs install
```

Se você já tinha clonado o repositório **antes** de instalar o Git LFS, os arquivos de
áudio/vídeo provavelmente baixaram como "ponteiros" (arquivos de texto de ~130 bytes, não o
áudio de verdade). Para corrigir, depois de rodar `git lfs install`:

```bash
git lfs pull
```

**Como saber se um arquivo é o áudio de verdade ou só um ponteiro:** abra o arquivo num player;
se não tocar, ou o tamanho estiver muito menor que o esperado, é ponteiro. Para confirmar pelo
terminal:

```bash
head -c 200 equipeXX/seu-arquivo.mp3
```

Se aparecer algo como `version https://git-lfs.github.com/spec/v1`, é ponteiro — rode
`git lfs install && git lfs pull`.

**4.2. Clonar o seu fork para o computador**

```bash
git clone https://github.com/SEU-USUARIO/dc-idc-2026.1.git
cd dc-idc-2026.1
```

**4.3. Editar e adicionar os arquivos**

A pasta da sua equipe já existe na **raiz** deste repositório (`equipeXX/`, com um `index.md`
de template dentro) — não crie uma pasta nova, só edite o que já está lá (veja o `README.md`
deste repositório para o passo a passo do conteúdo). Coloque a imagem da capa e o arquivo de
áudio na mesma pasta, e não esqueça de tirar o `draft: true` do preâmbulo quando terminar.

Como o `.gitattributes` já está configurado, basta usar `git add` normalmente — o Git LFS entra
em ação sozinho para os arquivos de áudio/vídeo, desde que você tenha rodado `git lfs install`
(passo 4.1). Você pode conferir o que vai ser versionado como LFS antes de commitar:

```bash
git lfs status
```

Arquivos de áudio/vídeo devem aparecer na lista como "Git LFS objects to be committed".

**4.4. Registrar as alterações (commit)**

```bash
git add .
git commit -m "Adiciona postagem: texto, capa e áudio do podcast"
```

Você pode fazer vários commits, um para cada etapa. Mensagens descritivas ajudam na nota.

**4.5. Enviar para o seu fork (push)**

```bash
git push origin master
```

> Confira o nome da branch principal do seu fork antes de rodar o comando (`git branch`). A
> branch padrão deste repositório é `master`; se o seu fork usar `main`, troque na linha acima.

Se o push demorar bastante mais que o normal ou mostrar linhas como
`Uploading LFS objects: 100% (1/1), 32 MB | ...`, é o Git LFS enviando o áudio — é esperado,
só espere terminar.

**4.6. Conferir**

Abra `github.com/SEU-USUARIO/dc-idc-2026.1` no navegador. Os arquivos e as mensagens de commit
devem estar lá. Se estiverem, o push funcionou. Agora falta o Pull Request.

---

## 5. Passo final e obrigatório: abrir o Pull Request

Este é o passo que a turma anterior esqueceu. **Sem ele, a atividade não foi entregue.**

1. Vá até o **seu fork** no GitHub.
2. Clique na aba **Pull requests** e depois em **New pull request**.
3. Confirme que a comparação está assim:
   - **base repository:** `emanueles/dc-idc-2026.1`  → **base:** `master`
   - **head repository:** `SEU-USUARIO/dc-idc-2026.1` → **compare:** `master`

   Ou seja: as suas alterações (head) indo **para** o repositório do semestre (base).
4. Clique em **Create pull request**.
5. Escreva um **título** (ex.: "Postagem — Equipe [nome/nomes]") e uma **descrição** com o
   nome dos integrantes e um resumo do que foi enviado.
6. Clique em **Create pull request** novamente para confirmar.

Pronto. Se aparecer a página do PR com o seu título e a lista de commits, a entrega chegou.

---

## 6. Como saber se deu certo

A entrega está correta se **todas** as afirmações abaixo forem verdadeiras:

- [ ] Existe um fork em `github.com/SEU-USUARIO/dc-idc-2026.1`.
- [ ] Os arquivos (texto, capa e áudio) aparecem **no fork**, no site do GitHub — não só no seu
      computador.
- [ ] Existe um Pull Request **aberto para** `emanueles/dc-idc-2026.1`.
- [ ] O PR tem título e descrição com o nome da equipe.

Se você só vê as alterações no seu computador (VS Code, pasta local) mas não no site do GitHub,
faltou o **push**. Se vê no seu fork no GitHub mas não há Pull Request, faltou o **passo 5**.

---

## 7. Problemas comuns

- **"Fiz tudo, mas o professor não vê nada."** Você provavelmente parou no commit local. Rode
  `git push` e depois abra o Pull Request.
- **"Meu arquivo de áudio foi recusado."** Acima de 25 MB, use a linha de comando (Caminho B).
  O limite pelo terminal é 100 MB — mas, com o Git LFS ativado corretamente (passo 4.1), você
  não deve nem chegar perto desse limite.
- **"O push falhou com uma mensagem sobre arquivo maior que 100 MB", mesmo usando o Caminho B.**
  Sinal de que o Git LFS não estava instalado/ativado quando você rodou `git add` — o arquivo
  foi adicionado como blob normal, não como ponteiro LFS. Corrija assim:
  ```bash
  git lfs install
  git rm --cached equipeXX/seu-arquivo.mp3
  git add equipeXX/seu-arquivo.mp3
  git commit -m "Corrige rastreamento do áudio via Git LFS"
  git push origin master
  ```
- **"Baixei o repositório e o áudio não toca" / "o arquivo de áudio tem uns 130 bytes".** Você
  clonou antes de instalar o Git LFS, então recebeu o ponteiro em vez do arquivo real. Rode
  `git lfs install` e depois `git lfs pull`.
- **"Abri o Pull Request no repositório errado."** Confira se você não abriu o fork/PR em
  `emanueles/dc-idc` (o hub do site) por engano — o repositório certo deste semestre é
  `emanueles/dc-idc-2026.1`. Feche o PR errado e abra um novo garantindo que a **base** é
  `emanueles/dc-idc-2026.1`.
- **"Aparece 'conflito' no Pull Request."** Avise a equipe e o professor; normalmente resolve-se
  atualizando o fork antes de reenviar.