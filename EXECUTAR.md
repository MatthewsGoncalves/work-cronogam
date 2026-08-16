# EXECUTAR — Gerar Currículo Adaptado a partir do HTML da Vaga

> **Para a IA (Claude, Gemini ou outro modelo):**
> Quando o candidato mandar o **HTML de uma vaga** e disser algo como
> *"siga o EXECUTAR.md"*, execute TODO o fluxo abaixo automaticamente, do começo
> ao fim, sem pedir confirmação a cada passo. Só pare para perguntar se faltar uma
> informação essencial (ex.: HTML/descrição incompleto).
> **O currículo e a carta são SEMPRE gerados em PT e em EN.**
>
> **REGRA DE OURO (vale para tudo):** nunca invente, exagere ou suponha fatos
> sobre o candidato. Toda informação factual vem da pasta `base/`. O que a vaga
> pede e o candidato não tem **não** entra no currículo — vai documentado como gap
> no arquivo de estudo.

---

## O que o candidato fornece

- **HTML da vaga** (colado, arquivo `.html`, ou URL — se a URL bloquear, peça o HTML
  colado). Também aceita a **descrição da vaga em texto** (sem HTML).
- (Opcional) Nome da empresa, se não estiver claro na vaga.

Nada mais é necessário. A base do currículo deve estar em `base/`, e a saída é
**bilíngue (PT + EN) por padrão** — o candidato não precisa escolher idioma.

---

## Estrutura do projeto

```
.
├── EXECUTAR.md                       ← este arquivo (o orquestrador)
├── base/                             ← base crua do candidato (fonte da verdade)
│   ├── curriculo-pt.md
│   ├── resume-en.md
│   └── Profile.pdf                    ← opcional
├── procedimentos/                    ← regras detalhadas de cada etapa
│   ├── 1-extrair-vaga-html.md
│   └── 2-adequar-curriculo-vaga.md
└── vagas/                            ← saída: uma pasta por vaga
```

---

## Fluxo automático (execute em sequência)

### Passo 1 — Extrair os requisitos do HTML
Siga **`procedimentos/1-extrair-vaga-html.md`**.
- Limpe o HTML (remova scripts, menus, banners, ruído).
- Extraia: cargo, empresa, local/modelo, senioridade, contrato, salário/benefícios,
  responsabilidades, requisitos **must-have** e **nice-to-have**, tecnologias,
  idiomas, cultura e palavras-chave.
- Campos ausentes = `não informado` (nunca preencher por suposição).

### Passo 2 — Ler a base crua
Leia **`base/curriculo-pt.md`**, **`base/resume-en.md`** e, se existir,
**`base/Profile.pdf`**.
Use a base PT para gerar as saídas em PT e a base EN para as saídas em EN.

### Passo 3 — Mapear vaga × candidato
Cruze cada requisito da vaga com a evidência real na base. Marque cada um como
✅ tem / ⚠️ parcial / ❌ não tem.

### Passo 4 — Criar a pasta da vaga
Liste as pastas em `vagas/`, encontre o maior prefixo numérico e crie
**`vagas/[NN] - [vaga] - [nome da empresa]/`**. Use o próximo número com pelo
menos dois dígitos. Se não houver nenhuma pasta numerada, comece por `01`.

Exemplos: `vagas/01 - Software Engineer - Empresa A/`,
`vagas/02 - Frontend Developer - Empresa B/`.

Nunca reutilize um número nem sobrescreva uma pasta existente. Se a vaga já
existir, crie uma nova entrada com o próximo número da sequência.

### Passo 5 — Gerar os 7 arquivos dentro da pasta

```
vagas/[NN] - [vaga] - [nome da empresa]/
├── requisitos-vaga.md                          # saída do Passo 1 (requisitos limpos)
├── [cargo] - [Nome] - curriculo.md             # currículo adaptado — português
├── [cargo] - [Nome] - resume.md                # currículo adaptado — inglês
├── [cargo] - [Nome] - carta de apresentação.md # carta — português
├── [cargo] - [Nome] - cover letter.md          # carta — inglês
├── email-candidatura.md                        # mensagem de e-mail (EN + PT-BR no mesmo arquivo)
└── estudo-da-vaga.md                           # preparação para entrevista (match, gaps, perguntas)
```

> **Padrão de nome de currículo e carta:** `[cargo] - [Nome] - [tipo]`, onde o tipo é:
> `curriculo` (PT) / `resume` (EN) para o currículo, e `carta de apresentação` (PT) /
> `cover letter` (EN) para a carta. Ex.: `Frontend Developer - Nome Sobrenome - resume.md`.

- **`requisitos-vaga.md`** → conforme o formato do `procedimentos/1-extrair-vaga-html.md` (idioma da vaga ou PT).
- **`[cargo] - [Nome] - curriculo.md` (PT) e `[cargo] - [Nome] - resume.md` (EN)** →
  conforme `procedimentos/2-adequar-curriculo-vaga.md`: **mesma adaptação nas duas
  línguas** — resumo mirando a vaga, skills e experiências reordenadas por relevância,
  matches destacados, otimizado para IA/ATS (markdown limpo, palavras-chave exatas da
  vaga **só onde há experiência real**, bullets de resultado). Conteúdo factual
  equivalente entre PT e EN.
- **`[cargo] - [Nome] - carta de apresentação.md` (PT) e `[cargo] - [Nome] - cover letter.md` (EN)** →
  conforme `procedimentos/2-adequar-curriculo-vaga.md` (seção 6.1): carta curta (3–4
  parágrafos) conectando os pontos fortes reais do candidato à vaga e à empresa, **nas
  duas línguas**. Só fatos da base; tom profissional e direto.
- **`email-candidatura.md`** → conforme `procedimentos/2-adequar-curriculo-vaga.md`
  (seção 6.2): mensagem curta de e-mail para enviar a candidatura, **em inglês e em
  PT-BR no mesmo arquivo**, separadas por divisória. Com assunto sugerido.
- **`estudo-da-vaga.md`** → conforme `procedimentos/2-adequar-curriculo-vaga.md`
  (seção 6): resumo da vaga, must/nice-have com status, pontos fortes, **gaps e
  como abordar**, temas a revisar, possíveis perguntas técnicas e perguntas a fazer.
  (Pode ser apenas em PT — é material de estudo do candidato.)

### Passo 6 — Relatar
Ao final, informe ao candidato:
- Caminho da pasta criada.
- Principais matches destacados no currículo.
- Gaps encontrados (onde ele está vulnerável e como o estudo orienta a contornar).
- Campos que ficaram como `não informado` (para ele complementar se quiser).

---

## Checklist final (antes de entregar)

- [ ] Requisitos extraídos só do HTML; ausências marcadas como `não informado`.
- [ ] Nenhuma tech/skill/número fora da base entrou no currículo.
- [ ] Datas, empresas, cargos e formação idênticos à base.
- [ ] Palavras-chave da vaga presentes só onde há experiência real.
- [ ] Markdown limpo e parseável (sem tabelas complexas no currículo).
- [ ] Pasta em `vagas/` nomeada como `[NN] - [vaga] - [nome da empresa]`, usando o próximo número disponível e sem sufixo de idioma.
- [ ] Sete arquivos criados (currículo e carta no padrão `[cargo] - [Nome] - [tipo]`): currículo PT (`curriculo`) + EN (`resume`), carta PT (`carta de apresentação`) + EN (`cover letter`), além de `requisitos-vaga.md`, `email-candidatura.md` e `estudo-da-vaga.md`.
- [ ] Currículo e carta gerados em **PT e EN**, com conteúdo factual equivalente.
- [ ] E-mail de candidatura tem versão EN e PT-BR no mesmo arquivo, com assunto sugerido.
- [ ] Carta de apresentação usa só fatos da base e não promete skills que o candidato não tem.
- [ ] Gaps documentados no estudo (não escondidos).
- [ ] Se a vaga for presencial/híbrida com presença obrigatória, o estudo abre com o bloco `🚨 ALERTA: VAGA PRESENCIAL` (local, modelo, horário e checagem de disponibilidade).
```
