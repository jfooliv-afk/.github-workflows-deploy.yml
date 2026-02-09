

name: Deploy to Lovable

on:
  push:
    branches: [ "main" ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout código
        uses: actions/checkout@v3

      - name: Configurar Node.js
        uses: actions/setup-node@v3
        with:
          node-version: "18"

      - name: Instalar dependências
        run: npm install

      - name: Rodar lint
        run: npm run lint

      - name: Rodar testes
        run: npm test

      - name: Instalar CLI do Lovable
        run: npm install -g lovable

      - name: Deploy para Lovable
        run: npx lovable deploy --token ${{ secrets.LOVABLE_TOKEN }}
