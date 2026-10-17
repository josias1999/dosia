# Arquitetura do Dosia

## Visão geral

O Dosia é um conjunto de **4 páginas estáticas** publicadas no WordPress (Elementor, widget "HTML"). Cada página é autossuficiente: traz seu próprio CSS, JavaScript e dados, sem backend e sem chamadas de API.

```
WordPress (saudedosia.com.br)
 ├─ /                                → index.html  (início + consulta)
 ├─ /calculadora-de-medicacao/       → menu + <iframe> com app React
 ├─ /calculadora-pediatrica/         → JavaScript puro
 └─ /leis-e-deveres-da-enfermagem/   → JavaScript puro
```

Todas compartilham o mesmo **menu lateral** (`.dosia-nav`), feito só com CSS (checkbox + label), sem JavaScript.

## Consulta de medicamentos

- Componente React escrito em JSX, com a base de dados inline.
- Compilado com **esbuild** num único bundle minificado (`assets/consulta.bundle.js`, ~970 KB).
- Na versão publicada no WordPress, o bundle é comprimido com **gzip** e codificado em **base64** (~370 KB). Um carregador de poucas linhas descomprime com `DecompressionStream` e executa o código. No repositório o bundle fica descomprimido, para ser legível e versionável.

### Modelo de dados (simplificado)

```js
// medicamento
{
  id: "ceftriaxona",
  category: "Antibióticos",
  generic: "Ceftriaxona sódica",
  brands: ["Rocefin"],
  pharmacology: { formula, mechanism, pharmacokinetics },
  actionTime: { onset, peak, duration },
  indication: "...",
  contraindications: [...],
  sideEffects: [...],
  routes: [{ route: "EV", diluent: "...", minDilution: "...", infusion: "..." }],
  source: "Bula Anvisa ..."
}

// par de compatibilidade / interação
{
  pair: ["sulfato_magnesio", "hidrocortisona"],
  route: "EV",
  contexts: ["solucao", "mesma_seringa"],   // separa via Y de mistura na mesma seringa/soro
  status: "incompativel",
  caution: "...",       // opcional: "compatível, mas a bula não recomenda misturar"
  note: "...",
  source: "Manual Farmacêutico ..."
}
```

Quando não existe par cadastrado, a interface mostra **"Não há registros informando se pode ou não"** — nunca supõe compatibilidade.

## Calculadora de medicação

App React carregado num `<iframe>` (originalmente via `srcdoc`, aqui como `app.html`) para isolar o CSS do tema do WordPress. O histórico de cálculos fica no `localStorage`.

## Calculadora pediátrica e Leis

JavaScript puro, sem framework. Todas as fórmulas rodam no navegador; os resultados aplicam limites de dose máxima e exibem alertas quando o volume é pequeno demais para aspirar com segurança.

## Próximos passos técnicos

- Extrair a base de dados para `data/medicamentos.json`
- Migrar o build para **Vite** e pré-compilar o JSX
- Testes unitários das fórmulas (Vitest)
- PWA com service worker para uso offline
