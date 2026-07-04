# Controle Fácil — Gestão de Ficha Técnica (Sushi)

App web mobile-first para controlar **custo, margem e preço** de um delivery de sushi/temaki.
Nasceu da planilha `ficha-tecnica-original.xlsx` e virou um aplicativo instalável (PWA).

**🔗 App no ar:** https://koraxia-korp.github.io/controle-facil/

O app já vem **populado com todos os dados da planilha**: 25 produtos, 9 combos/barcas,
25 insumos, 7 funcionários (dois cenários) e 8 contas fixas de operação.
O deploy é automático via GitHub Actions (`.github/workflows/deploy-pages.yml`) a cada push.

## Arquivos

| Arquivo | O que é |
|---|---|
| `index.html` | O aplicativo completo (self-contained: HTML + CSS + JS) |
| `design-system.html` | Guia de estilo / design system (tokens, componentes, regras) |
| `manifest.json` | Manifesto PWA (nome, ícone, cores) |
| `sw.js` | Service worker (funciona offline após o 1º acesso) |
| `icon.svg` | Ícone do app |
| `ficha-tecnica-original.xlsx` | Planilha de origem (referência) |

## O que o app faz

- **Painel** — margem média, custo fixo do mês, ponto de equilíbrio por dia e vendas de hoje.
- **Cardápio** — cadastro de produtos com ingredientes em gramas, categorias, duplicar e **preço-alvo por margem**.
- **Combos & Barcas** — montados a partir dos produtos; custo calculado ao vivo.
- **Insumos** — despensa editável + simulador de preço em tempo real.
- **Custos** — folha de pagamento e contas fixas por cenário (Mês cheio / Semana) com dias de trabalho.
- **Vendas do dia** — faturamento, lucro, CMV% e ticket médio.
- Tema **Escuro/Claro**, **backup** (exportar/importar) e **instalação** na tela inicial.

O motor de custo é `custo = Σ(gramas × preço_por_grama)` — reproduz a planilha original.

## Como usar

1. Abra o `index.html` no navegador (celular ou computador).
2. Comece com os dados de exemplo (sushi) ou importe sua planilha em CSV pela aba de importação.
3. Os dados ficam salvos **no próprio navegador do aparelho** (localStorage).
4. Faça backup de vez em quando: **⚙︎ Ajustes → Exportar backup** (gera `sushi-backup.json`).

## Como publicar (para instalar como app de verdade)

O PWA (instalar na tela inicial + offline) precisa ser servido por **HTTPS**. Opções gratuitas:

- **Netlify Drop** — arraste esta pasta em https://app.netlify.com/drop
- **Vercel** — `vercel` na pasta, ou conecte um repositório
- **GitHub Pages** — suba os arquivos e ative Pages nas configurações do repositório

Teste local rápido (não instala como PWA, mas roda):

```bash
# Python
python3 -m http.server 8080
# ou Node
npx serve .
```

Depois acesse `http://localhost:8080`.

## Dados & privacidade

Nenhum dado sai do aparelho. Tudo é local (localStorage) + o arquivo de backup que você exportar.
Para sincronizar entre aparelhos automaticamente, seria preciso adicionar um serviço de nuvem (passo futuro).
