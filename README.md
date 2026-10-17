<div align="center">

# 💊 Dosia

**Ferramentas rápidas para a enfermagem — consulta de medicamentos, calculadoras de dose e guia de leis, direto no celular, no plantão.**

🌐 **[saudedosia.com.br](https://saudedosia.com.br)**

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![React](https://img.shields.io/badge/React-20232A?logo=react&logoColor=61DAFB)
![esbuild](https://img.shields.io/badge/esbuild-FFCF00?logo=esbuild&logoColor=black)
![WordPress](https://img.shields.io/badge/WordPress-21759B?logo=wordpress&logoColor=white)

</div>

---

## Sobre o projeto

O **Dosia** nasceu de uma dor real de quem trabalha em UPA e hospital: no meio do plantão, descobrir se dois medicamentos podem correr na mesma via, como diluir uma ampola ou quantos mL aspirar para uma criança de 12 kg exige abrir bula, manual de diluição e calculadora ao mesmo tempo.

O Dosia junta tudo isso num só lugar, **sem instalar nada**, com **fontes citadas** e uma regra de ouro: **quando não há registro, o sistema avisa em vez de supor.**

> ⚠️ **Aviso:** conteúdo de apoio para profissionais de saúde. Não substitui prescrição, bula ou protocolo institucional. Confirme sempre com a farmácia da sua instituição antes de administrar.

## Funcionalidades

### 🔎 Consulta de medicamentos
- **253+ medicamentos** organizados em **32 classes terapêuticas**
- Busca por **nome genérico ou comercial**
- Ficha completa: indicação, contraindicações, efeitos colaterais, vias de administração, diluente, diluição mínima e tempo de infusão
- **Farmacologia avançada** (mecanismo de ação, Vd, ligação proteica, metabolização CYP, eliminação)
- **Tempo de ação**: início, pico e duração
- **157 pares de compatibilidade**, separando **"em Y"** de **"mesma seringa"**, com alertas de cautela
- Passo a passo de administração e alertas de monitorização por classe

### 🧮 Calculadora de medicação
Gotejamento (gotas e microgotas/min), dose por regra de três, insulina, bomba de infusão, porcentagem, conversor de unidades, reconstituição, rediluição pediátrica, canetas emagrecedoras, vias e seringas, checklist de segurança e histórico de cálculos (salvo no navegador).

### 👶 Calculadora pediátrica
- **Quanto aspirar?** — volume a partir da dose prescrita e da apresentação (pronta, pó ou %)
- Medicamentos pediátricos comuns com faixa de dose (mg/kg) e dose máxima
- Dose por peso (mg, mcg, UI, mEq / kg, por dose ou por dia)
- **Emergência (PALS)** com doses limitadas ao máximo
- **Infusão contínua** (dose → mL/h e mL/h → dose)
- **Soro de manutenção** — regra de Holliday-Segar (100/50/20) com conversão para bomba, micro e macrogotas
- **Peso estimado pela idade** (fórmulas APLS)

### ⚖️ Leis, deveres e anotações
Quem faz o quê na equipe, deveres e proibições do Código de Ética, direitos, piso salarial e jornada, papel do Cofen/Coren, infrações e penalidades e linha do tempo das resoluções recentes — com busca, filtros por categoria e links para as fontes oficiais.

## Tecnologias e decisões técnicas

| Decisão | Por quê |
|---|---|
| **Páginas estáticas autossuficientes** (HTML + CSS + JS inline) | Rodam embutidas em qualquer CMS (WordPress/Elementor, Blogger) sem backend e sem dependência de CDN |
| **React** na consulta e na calculadora de medicação | Interface com muitos estados (busca, filtros, fichas, compatibilidade) |
| **JavaScript puro** na calculadora pediátrica e nas leis | Páginas leves, carregamento instantâneo no celular |
| **Bundle com esbuild + gzip/base64** | Reduz ~970 KB de código e dados para ~370 KB embutidos na página |
| **Base de dados curada à mão** | Cada medicamento e cada par de compatibilidade tem fonte real (bula Anvisa, manuais hospitalares) |
| **Mobile-first** | O uso principal é no celular, durante o plantão |
| **`localStorage`** | Histórico de cálculos sem precisar de conta ou servidor |

## Estrutura do repositório

```
dosia/
├── index.html                          # Início + Consulta de medicamentos
├── assets/
│   ├── consulta.bundle.js              # App da consulta (React + base de dados, gerado com esbuild)
│   └── dosia-logo.webp
├── calculadora-de-medicacao/
│   ├── index.html                      # Página com menu
│   └── app.html                        # Calculadora (React)
├── calculadora-pediatrica/
│   └── index.html
├── leis-e-deveres-da-enfermagem/
│   └── index.html
├── docs/
│   ├── ARQUITETURA.md
│   └── FONTES.md
├── .nojekyll
├── .gitignore
├── LICENSE
└── README.md
```

## Como rodar localmente

Não precisa instalar nada. Clone e sirva a pasta com qualquer servidor estático:

```bash
git clone https://github.com/josias1999/dosia.git
cd dosia
python -m http.server 8000
# abra http://localhost:8000
```

Ou ative o **GitHub Pages** (Settings → Pages → Branch `main` / root) para ter uma demo online.

## Fontes de dados

- Bulas aprovadas pela **Anvisa** (Bulário Eletrônico)
- Manuais de diluição hospitalares (Palmas, Joinville, Sorocaba)
- Guia de Incompatibilidades — CIM-HUJM/EBSERH, Guia Farmacêutico Hospital São Camilo
- **AHA PALS**, fórmulas **APLS**, regra de **Holliday-Segar**
- Lei 7.498/86, Decreto 94.406/87, Código de Ética (Res. Cofen 564/2017)

Lista detalhada em [`docs/FONTES.md`](docs/FONTES.md).

## Roadmap

- [x] Consulta com farmacologia avançada e tempo de ação
- [x] Calculadora de medicação e calculadora pediátrica
- [x] Guia de leis e deveres da enfermagem
- [ ] Curadoria completa dos pares de compatibilidade dos novos medicamentos
- [ ] Separar a base de dados em JSON e migrar o build para Vite
- [ ] PWA (funcionar offline)
- [ ] Testes automatizados das fórmulas das calculadoras

## Autor

**Josias Carvalho**
[GitHub](https://github.com/josias1999) · [LinkedIn](https://www.linkedin.com/in/josias-carvalho99)

## Licença

Código sob licença **MIT** — veja [LICENSE](LICENSE). O conteúdo clínico é informativo e não substitui avaliação profissional.
