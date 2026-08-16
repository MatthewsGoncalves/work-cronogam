# PROCEDIMENTO — Extração de Requisitos da Vaga a partir do HTML

> **Para a IA que vai executar isto (Claude, Gemini ou outro modelo):**
> Este procedimento recebe o **código HTML cru** de uma página de vaga (LinkedIn,
> Gupy, site da empresa, etc.) e produz um `.md` limpo e estruturado com os
> requisitos da vaga. Esse `.md` é a **entrada** do procedimento
> `procedimentos/2-adequar-curriculo-vaga.md`.
>
> **REGRA DE OURO:** extraia SOMENTE o que está no HTML. Não invente requisitos,
> não complete com "o que costuma ser pedido", não suponha tecnologias. Se um
> campo não existe no HTML, marque como `não informado`.

---

## 0. Objetivo

Transformar o HTML bruto e poluído de uma página de vaga em um documento `.md`
limpo, contendo cargo, empresa, responsabilidades, requisitos obrigatórios,
desejáveis, tecnologias, benefícios e demais dados — pronto para ser usado na
adaptação do currículo.

---

## 1. Entrada

O candidato fornece **uma** das opções:

- O **código HTML** colado (ou caminho de um arquivo `.html` salvo da página), OU
- A **URL** da vaga (a IA tenta buscar; se a página exigir login ou bloquear
  scraping — ex.: LinkedIn retorna HTTP 999 — peça o HTML colado).

Também deve informar (se souber): **nome da empresa** e **idioma desejado** do
documento de saída (`pt` ou `ing`). Se não informar, detecte o idioma a partir do
próprio texto da vaga.

---

## 2. Como limpar o HTML

O HTML vem cheio de ruído. Descarte:

- Tags de estrutura/estilo: `<script>`, `<style>`, `<svg>`, `<nav>`, `<header>`,
  `<footer>` que não fazem parte do anúncio.
- Menus, banners, "vagas relacionadas", botões de candidatura, cookies, rodapé
  do site, links de compartilhamento.
- Atributos, classes e IDs — interessa o **texto** e a **hierarquia** (títulos,
  listas, parágrafos).

Mantenha e priorize:

- O bloco principal da descrição da vaga (geralmente dentro de `<article>`,
  `<main>`, ou um container com "job description" / "descrição").
- Listas `<ul>/<li>` — normalmente são requisitos e responsabilidades.
- Títulos `<h1>..<h4>` — delimitam seções (Requisitos, Responsabilidades, etc.).

> Se o HTML estiver truncado ou claramente incompleto (faltando a seção de
> requisitos), **avise o candidato** e peça o HTML completo antes de gerar.

---

## 3. O que extrair (campos-alvo)

Procure no texto os seguintes campos. Se não encontrar, use `não informado`:

| Campo | Onde costuma aparecer |
|---|---|
| Cargo / título da vaga | `<h1>`, topo do anúncio |
| Empresa | cabeçalho, logo, "sobre a empresa" |
| Local / modelo (remoto/híbrido/presencial) | perto do título |
| Senioridade (júnior/pleno/sênior) | título ou requisitos |
| Tipo de contrato (CLT/PJ/estágio) | detalhes da vaga |
| Faixa salarial / benefícios | seção de benefícios |
| Responsabilidades / o que vai fazer | lista após "responsabilidades" |
| Requisitos obrigatórios (must-have) | lista após "requisitos"/"qualificações" |
| Requisitos desejáveis (nice-to-have) | "diferenciais", "será um plus" |
| Tecnologias / ferramentas | espalhadas no texto |
| Idiomas exigidos | requisitos |
| Sobre a empresa / cultura | seção institucional |

### 3.1 Separar must-have de nice-to-have
- "Obrigatório", "imprescindível", "necessário", "você precisa ter" → **must-have**.
- "Diferencial", "desejável", "será um plus", "bônus", "gostaríamos" → **nice-to-have**.
- Em dúvida, classifique como must-have e marque `(classificação incerta)`.

---

## 4. Estrutura de saída

Gerar **um** arquivo `.md`. Nome sugerido:

```
vaga-[empresa]-[cargo].md
```

Conteúdo no formato:

```markdown
# Vaga — [Cargo] @ [Empresa]

- **Empresa:** ...
- **Local / Modelo:** ... (remoto / híbrido / presencial)
- **Senioridade:** ...
- **Contrato:** ...
- **Salário / Benefícios:** ...
- **Fonte:** [URL ou "HTML colado em AAAA-MM-DD"]

## Resumo da vaga
(2-4 linhas, em texto plano, do que a vaga busca — só com base no anúncio)

## Responsabilidades
- ...

## Requisitos obrigatórios (must-have)
- ...

## Requisitos desejáveis (nice-to-have)
- ...

## Tecnologias e ferramentas citadas
- ... (lista plana de termos exatos como aparecem no anúncio — útil para ATS)

## Idiomas
- ...

## Sobre a empresa / cultura
- ... (só o que o anúncio trouxer)

## Palavras-chave para o currículo
- (todos os termos técnicos e de domínio relevantes, escritos exatamente como na vaga)
```

> A seção **"Palavras-chave para o currículo"** é a ponte para o outro
> procedimento: lista os termos que o currículo adaptado deve conter — desde que,
> no momento da adaptação, o candidato realmente possua aquela experiência.

---

## 5. Passo a passo da execução

1. **Receber** o HTML (colado, arquivo ou URL).
2. Se for URL, **tentar buscar**; se bloquear/exigir login, pedir o HTML colado.
3. **Limpar** o HTML conforme passo 2 (remover ruído, manter texto e hierarquia).
4. **Extrair** os campos do passo 3, separando must-have de nice-to-have.
5. **Detectar idioma** (ou usar o solicitado) e escrever a saída nesse idioma.
6. **Gerar** o `.md` no formato do passo 4.
7. **Relatar** ao candidato: cargo, empresa e quaisquer campos que ficaram como
   `não informado` (para ele decidir se complementa manualmente).

---

## 6. Encadeamento com o outro procedimento

Fluxo completo de ponta a ponta:

```
HTML da vaga
   │
   ▼  (procedimentos/1-extrair-vaga-html.md)
vaga-[empresa]-[cargo].md   ← requisitos limpos
   │
   ▼  (procedimentos/2-adequar-curriculo-vaga.md)
vagas/[NN] - [vaga] - [nome da empresa]/
   ├── [cargo] - [Nome] - curriculo.md
   ├── [cargo] - [Nome] - resume.md
   ├── [cargo] - [Nome] - carta de apresentação.md
   ├── [cargo] - [Nome] - cover letter.md
   ├── email-candidatura.md
   └── estudo-da-vaga.md
```

Depois de gerar o `.md` de requisitos, ofereça ao candidato executar o
`procedimentos/2-adequar-curriculo-vaga.md` usando este arquivo como descrição da vaga.

---

## 7. Checklist final antes de entregar

- [ ] Nenhum requisito inventado — tudo veio do HTML.
- [ ] Campos ausentes marcados como `não informado` (não preenchidos por suposição).
- [ ] Must-have e nice-to-have separados corretamente.
- [ ] Tecnologias escritas exatamente como no anúncio (importante para ATS).
- [ ] Seção "Palavras-chave para o currículo" preenchida.
- [ ] Fonte (URL ou data do HTML) registrada.
- [ ] Saída no idioma correto.
```
