# PROCEDIMENTO — Adequação de Currículo por Vaga

> **Para a IA que vai executar isto (Claude, Gemini ou outro modelo):**
> Este é um procedimento determinístico. Siga os passos na ordem. A regra mais
> importante é a **REGRA DE OURO**: você NÃO pode inventar, exagerar ou supor
> nada que não esteja na base crua do candidato. Adaptar = reordenar, destacar,
> reescrever e traduzir fatos que JÁ EXISTEM. Nada além disso.

---

## 0. Objetivo

Pegar a **base crua** do candidato (currículo completo já existente) e gerar um
currículo **sob medida para UMA vaga específica**, com linguagem atrativa e de
fácil reconhecimento por modelos de IA / sistemas ATS. Além do currículo, gerar
um segundo arquivo de **estudo da vaga**, para o candidato se preparar caso seja
chamado para entrevista.

---

## 1. Arquivos de entrada (a base crua)

Sempre ler estes arquivos antes de qualquer coisa (todos na pasta `base/`):

- `base/curriculo-pt.md` — base completa em português
- `base/resume-en.md` — base completa em inglês
- `base/Profile.pdf` — fonte complementar opcional exportada do LinkedIn

**Toda informação factual sai daqui.** Se algo não está nesses arquivos, não entra
no currículo gerado.

---

## 2. Entradas que o candidato fornece no momento

Antes de executar, o candidato (ou quem aciona a IA) deve informar:

1. **Descrição da vaga** (texto completo, colado ou em arquivo). Quanto mais
   completo, melhor a adequação.
2. **Nome da empresa**.

Se a descrição da vaga não foi fornecida, **pare e peça** — não tente adivinhar a
vaga.

---

## 3. REGRA DE OURO — Não inventar (LEIA COM ATENÇÃO)

✅ **Permitido:**
- Reordenar experiências/skills para colocar o mais relevante para a vaga no topo.
- Destacar (negrito) tecnologias e resultados que a vaga pede E que o candidato tem.
- Reescrever bullets com verbos de ação mais fortes, **mantendo o fato intacto**.
- Reescrever o resumo/summary para falar diretamente com a vaga, usando só fatos reais.
- Traduzir entre PT e ING (a base existe nas duas línguas).
- Usar palavras-chave da vaga **somente** quando o candidato realmente tem aquela
  experiência comprovável na base.

❌ **Proibido:**
- Adicionar tecnologia, ferramenta, empresa, certificação ou número que não está na base.
- Inflar tempo de experiência, cargos ou resultados.
- Inventar métricas (%, valores, quantidades) que não existem no original.
- Atribuir ao candidato uma skill que a vaga pede mas ele não tem.
- Mudar datas, nomes de empresas, cargos ou formação.

> **Teste mental antes de escrever qualquer frase:** "Consigo apontar exatamente
> onde isto está na base crua?" Se a resposta for não, **não escreva**.

### 3.1 Lacunas (o que fazer quando a vaga pede algo que o candidato não tem)
- **Não preencha com mentira.** Deixe de fora do currículo.
- Registre a lacuna no arquivo de estudo da vaga (passo 6), na seção "Gaps e como abordar".

---

## 4. Como deixar o currículo "atrativo para IA / ATS"

Otimização para reconhecimento por modelos de IA e parsers ATS — **sem encher de
buzzword vazia**:

- **Cabeçalho limpo** com nome, título alinhado à vaga (ex.: usar o mesmo nome do
  cargo da vaga, desde que verdadeiro para o perfil) e contatos.
- **Markdown semântico**: use `#`, `##`, `###` e listas `-`. Evite tabelas
  complexas, colunas ou ASCII art (ATS lê mal).
- **Palavras-chave exatas da vaga** (nomes de tecnologias, frameworks,
  metodologias) escritas igual à vaga — mas só as que o candidato realmente tem.
  Ex.: se a vaga diz "Next.js" e a base diz "Next.js", mantenha "Next.js".
- **Seção de Competências/Skills no topo**, em texto plano e escaneável, com os
  termos que dão match com a vaga primeiro.
- **Bullets orientados a resultado**: verbo de ação + o que fez + impacto (só
  impacto que existe na base).
- **Texto em primeira pessoa implícita** (sem "Eu"), frases diretas e curtas.
- **Sem imagens, sem ícones decorativos pesados** que atrapalhem parsing (emojis
  de contato simples no cabeçalho são aceitáveis).
- **Densidade de palavras-chave natural** — distribua os termos ao longo do
  resumo e dos bullets, não amontoe.

---

## 5. Estrutura de saída (pasta + arquivos)

Criar **uma pasta dentro de `vagas/`** com o próximo número disponível. Liste as
pastas existentes, encontre o maior prefixo e some 1. Use pelo menos dois
dígitos. A pasta não recebe sufixo de idioma, pois contém PT e EN:

```
vagas/[NN] - [vaga] - [nome da empresa]
```

Exemplos:
- `vagas/01 - Desenvolvedor Frontend - Empresa A`
- `vagas/02 - Software Engineer - Empresa B`

Dentro da pasta, criar os arquivos abaixo. **Currículo e carta são sempre gerados
em PT e EN.** O `requisitos-vaga.md` entra quando o fluxo parte do HTML.

```
vagas/[NN] - [vaga] - [nome da empresa]/
├── [cargo] - [Nome] - curriculo.md             # currículo adaptado — português
├── [cargo] - [Nome] - resume.md                # currículo adaptado — inglês
├── [cargo] - [Nome] - carta de apresentação.md # carta — português
├── [cargo] - [Nome] - cover letter.md          # carta — inglês
├── email-candidatura.md                        # mensagem de e-mail (EN + PT-BR no mesmo arquivo)
└── estudo-da-vaga.md                           # o que a vaga pedia, para preparação (PT)
```

> **Padrão de nome de currículo e carta:** `[cargo] - [Nome] - [tipo]`. O `[tipo]` é:
> `curriculo` (PT) / `resume` (EN) e `carta de apresentação` (PT) / `cover letter` (EN).
>
> As versões PT e EN devem ter **conteúdo factual equivalente** — mesma adaptação,
> apenas em idiomas diferentes (PT vem da `base/curriculo-pt.md`, EN da `base/resume-en.md`).

> Nunca reutilize um número nem sobrescreva uma adaptação anterior. Se a vaga já
> existir, crie uma nova entrada com o próximo número da sequência.

---

## 6. Conteúdo de `estudo-da-vaga.md`

Documento para o candidato estudar caso seja chamado. Estrutura:

```markdown
# Estudo da Vaga — [Cargo] @ [Empresa]

> ## 🚨 ALERTA: VAGA PRESENCIAL   ← incluir SOMENTE se a vaga for presencial ou híbrida com presença obrigatória
> Esta vaga é **presencial** em **[local]** ([modelo: presencial / híbrido X dias]).
> Horário: **[horário, se informado]**.
> **Antes de aplicar, confirme** disponibilidade real de estar nesse local/horário —
> compare com a localização do candidato na base. Se não for viável, sinalize antes
> de seguir com a candidatura.

## Resumo da vaga
(2-4 linhas: o que a empresa busca, em palavras simples)

## Requisitos obrigatórios (must-have)
- [requisito] → ✅ tenho (onde: experiência X) / ⚠️ parcial / ❌ não tenho

## Requisitos desejáveis (nice-to-have)
- [requisito] → status

## Match do meu perfil (pontos fortes a destacar na entrevista)
- ...

## Gaps e como abordar
- [o que não tenho] → como compensar honestamente (projeto correlato, vontade de aprender, base teórica)

## Tecnologias/temas para revisar antes da entrevista
- [tech] → tópicos-chave a estudar

## Possíveis perguntas técnicas
- ...

## Perguntas que EU posso fazer ao entrevistador
- ...

## Sobre a empresa (se a descrição trouxer contexto)
- (apenas o que estiver na descrição da vaga — não inventar dados da empresa)
```

> **Regra do alerta de presencial:** se a vaga for **presencial** (ou híbrida com
> dias obrigatórios no local), inclua o bloco `🚨 ALERTA: VAGA PRESENCIAL` como
> primeira coisa do arquivo, logo após o título — com local, modelo e horário. Se a
> vaga for **remota**, **não** inclua o bloco. Confronte o local da vaga com a
> localização do candidato na base e peça confirmação de disponibilidade.

Na seção de match/gaps, mapeie cada requisito da vaga contra a base crua de forma
honesta. Esse arquivo PODE conter análise e sugestões (é material de estudo), mas
**os fatos sobre o candidato continuam vindo só da base**.

---

## 6.1 Conteúdo de `carta-apresentacao.md`

Carta de apresentação (cover letter) curta e personalizada para a vaga. Regras:

- **3 a 4 parágrafos**, no máximo ~250–300 palavras. Direta e profissional.
- Conecta os **pontos fortes reais** do candidato (da base) às **necessidades da
  vaga** e ao contexto da empresa.
- **REGRA DE OURO vale aqui também:** não prometer skills que o candidato não tem,
  não inventar entusiasmo por tecnologias que ele nunca usou. Sobre os gaps, no
  máximo demonstrar disposição genuína de aprender — sem afirmar experiência falsa.
- Gerar uma versão em português e outra em inglês, com conteúdo factual
  equivalente. Usar tom humano, profissional e sem clichês vazios.

Estrutura sugerida:

```markdown
# Carta de Apresentação — [Cargo] @ [Empresa]

[Local], [data]

Prezada equipe da [Empresa],   ← ou nome do recrutador, se conhecido

**Parágrafo 1 — abertura:** quem sou, a vaga a que me candidato e um gancho de
encaixe (1 ponto forte central que conversa com a vaga).

**Parágrafo 2 — prova:** 2–3 conquistas/experiências reais da base que comprovam
o encaixe com as responsabilidades e requisitos da vaga.

**Parágrafo 3 — empresa:** por que esta empresa/produto faz sentido para mim
(usar só contexto real da vaga; se houver gap relevante, mostrar disposição de
aprender de forma honesta).

**Parágrafo 4 — fechamento:** agradecimento, disponibilidade e convite à conversa.

Atenciosamente,
[Nome]
[contato]
```

---

## 6.2 Conteúdo de `email-candidatura.md`

Mensagem **curta** de e-mail para enviar a candidatura (acompanha currículo e carta
em anexo). Regras:

- **Bem mais curta que a carta** — 1 abertura + 2–4 frases + fechamento.
- **Inglês e PT-BR no MESMO arquivo**, separados por uma divisória `---`.
- Cada versão traz uma **linha de assunto sugerida**.
- Tom profissional, direto e cordial. Só fatos da base; nada inventado.
- Mencionar que currículo e carta de apresentação seguem em anexo.

Formato:

```markdown
# E-mail de Candidatura — [Cargo] @ [Empresa]

## 🇧🇷 Português (PT-BR)

**Assunto:** Candidatura — [Cargo] | [Nome]

Olá, [equipe/nome],

(1–2 frases: a que vaga me candidato + 1 gancho de encaixe real.)
(1–2 frases: principal ponto forte para a vaga.)
Em anexo envio meu currículo e carta de apresentação. Fico à disposição.

Atenciosamente,
[Nome]
[contato]

---

## 🇬🇧 English

**Subject:** Application — [Role] | [Name]

Hi [team/name],

(same message, in English)

Best regards,
[Name]
[contact]
```

---

## 7. Passo a passo da execução

1. **Ler** `base/curriculo-pt.md`, `base/resume-en.md` e, se existir,
   `base/Profile.pdf` por completo.
2. **Ler** a descrição da vaga fornecida. Extrair: cargo, must-haves, nice-to-haves,
   tecnologias, responsabilidades, palavras-chave.
3. **Mapear** cada requisito da vaga ↔ evidência na base crua (tabela mental).
4. **Criar a pasta** com o nome no formato do passo 5 (sem sufixo de idioma).
5. **Gerar currículo PT (`[cargo] - [Nome] - curriculo.md`) e EN (`[cargo] - [Nome] - resume.md`)** (mesma adaptação, duas línguas):
   - Reescrever o resumo mirando a vaga (só fatos reais).
   - Reordenar skills e experiências por relevância à vaga.
   - Destacar matches; aplicar otimização de IA/ATS.
   - Revisar contra a REGRA DE OURO: cada linha tem origem na base?
6. **Gerar carta PT (`[cargo] - [Nome] - carta de apresentação.md`) e EN (`[cargo] - [Nome] - cover letter.md`)** conforme passo 6.1.
7. **Gerar `email-candidatura.md`** conforme passo 6.2 (EN + PT-BR no mesmo arquivo).
8. **Gerar `estudo-da-vaga.md`** conforme passo 6.
9. **Relatar ao candidato**: caminho da pasta, principais matches destacados e os
   gaps encontrados (para ele saber onde está vulnerável).

---

## 8. Checklist final antes de entregar

- [ ] Nenhuma tecnologia/skill/número que não esteja na base foi adicionada.
- [ ] Datas, empresas, cargos e formação idênticos à base.
- [ ] Palavras-chave da vaga presentes só onde há experiência real.
- [ ] Markdown limpo e parseável (sem tabelas complexas no currículo).
- [ ] Pasta nomeada no formato `[NN] - [vaga] - [nome da empresa]`, usando o próximo número disponível e sem sufixo de idioma.
- [ ] Currículo e carta nomeados como `[cargo] - [Nome] - [tipo]` (curriculo/resume, carta de apresentação/cover letter).
- [ ] Arquivos criados: currículo PT + EN, carta PT + EN, `email-candidatura.md` e `estudo-da-vaga.md`.
- [ ] Currículo e carta gerados em PT e EN, com conteúdo factual equivalente.
- [ ] E-mail de candidatura tem EN e PT-BR no mesmo arquivo, com assunto sugerido.
- [ ] Carta de apresentação usa só fatos da base e não promete skills inexistentes.
- [ ] Gaps documentados no arquivo de estudo, não escondidos.
```
