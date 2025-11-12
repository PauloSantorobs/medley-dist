# Medley Dist – GitHub Pages (docs)

Este repositório já contém o site estático em `docs/`, pronto para ser publicado no GitHub Pages usando a opção "Deploy from a branch".

## Publicar pelo GitHub Pages (docs/)
- Faça push deste repositório para o GitHub.
- Acesse `Settings` → `Pages` no repositório.
- Em `Source`, selecione `Deploy from a branch`.
- Em `Branch`, escolha `main` e a pasta `/docs`.
- Salve. Em alguns minutos a página ficará disponível.

## Importante: base do site
Os arquivos HTML em `docs/` usam a tag `<base href="/medley-dist/">`. Isso presume que o nome do repositório seja `medley-dist` e que o site seja acessado em:

```
https://<seu-usuario>.github.io/medley-dist/
```

Se o repositório tiver outro nome, ajuste a base na sua build (ex.: `--base-href` no Angular) para corresponder ao nome do repositório, ou renomeie o repositório para `medley-dist`.

## O que já foi preparado
- Adicionado `docs/.nojekyll` para evitar processamento Jekyll e servir os arquivos como estão.
- Estrutura já está em `docs/` com `index.html` e ativos necessários.

## (Opcional) Publicar via GitHub Actions
Caso prefira publicar via Actions (em vez de `Deploy from a branch`), habilite `Settings` → `Pages` usando `GitHub Actions` como origem e adicione um workflow como o exemplo abaixo:

```
# .github/workflows/pages.yml
name: Deploy static content to Pages
on:
  push:
    branches: ["main"]
permissions:
  contents: read
  pages: write
  id-token: write
concurrency:
  group: "pages"
  cancel-in-progress: true
jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: docs
      - id: deployment
        uses: actions/deploy-pages@v4
```

## (Opcional) Domínio personalizado
- Se for usar domínio próprio, adicione um arquivo `CNAME` dentro de `docs/` com o domínio (ex.: `www.seudominio.com`).
- Configure o DNS de acordo com a documentação do GitHub Pages.

## Suporte
Se quiser, posso criar o workflow acima automaticamente e/ou ajustar a base de acordo com o nome do seu repositório.
