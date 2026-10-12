# Planejamento do repositório privado de artes

## Escopo

Este repositório é somente uma biblioteca privada de imagens, emotes, GIFs e banners. Ele não contém o bot nem a lógica do projeto principal.

O projeto consumidor está em:

```text
C:\Users\vinic\Desktop\Vinicius Vicentim\Projects\GM Core
```

O que será entregue ao projeto principal:

- o arquivo `assets.json` (ou sua leitura direta no GitHub);
- acesso de leitura ao repositório privado;
- um token guardado no ambiente do projeto principal;
- a regra para baixar cada arte usando o campo `api_url`.

## Estrutura deste repositório

```text
pastas atuais de artes/
assets.json
doc/
taks/
README.md
```

As pastas existentes serão mantidas nesta primeira versão para evitar renomear ou quebrar referências. A organização poderá ser refinada em outro commit.

## Como funciona o JSON

Cada item contém `id`, `name`, `category`, `path`, `extension`, `size_bytes`, `api_url` e `raw_url`.

Os campos `owner`, `repository` e `branch` ficam no início do JSON. Antes de publicar, `SEU_USUARIO` e `SEU_REPOSITORIO` serão substituídos pelos valores reais.

## Atenção aos links privados

Os links existem no catálogo, mas exigem autenticação. O GM Core deve chamar `api_url` com um token de leitura do GitHub e solicitar o conteúdo do arquivo. Um link privado colocado diretamente em um embed do Discord não leva a credencial junto.

O token nunca deve entrar neste repositório. Ele deve ficar no `.env` local/ambiente de execução do GM Core, e somente nomes de variáveis podem ser documentados no `.env.example`.

## Fluxo de atualização

1. Colocar ou substituir a arte em uma das pastas.
2. Adicionar, editar ou remover a entrada correspondente em `assets.json`.
3. Conferir se o caminho e os links estão corretos.
4. Fazer commit e push no repositório privado.
5. O GM Core passa a consumir a nova versão do catálogo.

## Contrato para o GM Core

O projeto principal deve receber estes valores:

```text
GITHUB_ASSETS_OWNER=...
GITHUB_ASSETS_REPOSITORY=...
GITHUB_ASSETS_BRANCH=main
GITHUB_ASSETS_TOKEN=...  # somente no ambiente, nunca no Git
```

A integração deve localizar o item pelo `id`, usar seu `api_url`, autenticar na API do GitHub e ler o conteúdo retornado. A implementação dessa integração será feita separadamente no GM Core.

Veja o desenho em [fluxograma.md](fluxograma.md) ou [fluxograma.svg](fluxograma.svg). As pendências estão em [../taks/README.md](../taks/README.md).
