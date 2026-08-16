# Currículo por Vaga com IA

Projeto aberto para criar currículos, cartas de apresentação e materiais de
entrevista adaptados a cada vaga, usando IA e uma biblioteca pessoal como fonte
da verdade.

A IA pode reorganizar, destacar, reescrever e traduzir experiências reais. Ela
não deve inventar competências, resultados, empresas, datas ou números.

## O que o projeto gera

Para cada vaga, o fluxo cria uma pasta privada numerada:

```text
vagas/
├── 01 - Desenvolvedor Frontend - Empresa A/
├── 02 - Software Engineer - Empresa B/
└── 03 - Analista de Dados - Empresa C/
```

Cada pasta contém:

```text
requisitos-vaga.md
[cargo] - [Nome] - curriculo.md
[cargo] - [Nome] - resume.md
[cargo] - [Nome] - carta de apresentação.md
[cargo] - [Nome] - cover letter.md
email-candidatura.md
estudo-da-vaga.md
```

## Privacidade

Seus currículos, dados pessoais, PDFs e candidaturas ficam fora do Git por
padrão:

- `base/` guarda sua biblioteca pessoal.
- `vagas/` guarda todas as candidaturas geradas.
- `roteiro-video-apresentacao.md` pode guardar um roteiro pessoal opcional.
- arquivos `.html` de vagas também são ignorados.

O `.gitignore` permite publicar o projeto sem publicar esse conteúdo. Antes de
qualquer `git add`, confirme com:

```bash
git status --short
git check-ignore base/curriculo-pt.md base/resume-en.md base/Profile.pdf
```

Não remova essas regras sem revisar os arquivos que passarão a ser públicos.

## Instalação

### 1. Baixe o projeto

Você pode criar um fork no GitHub ou clonar diretamente:

```bash
git clone https://github.com/MatthewsGoncalves/work-cronogam.git
cd work-cronogam
```

### 2. Crie sua biblioteca de currículos

Copie os modelos anônimos:

```bash
cp modelos/curriculo-pt.exemplo.md base/curriculo-pt.md
cp modelos/resume-en.example.md base/resume-en.md
```

Preencha os dois arquivos apenas com informações verdadeiras. Opcionalmente,
adicione um PDF exportado do LinkedIn em `base/Profile.pdf`.

### 3. Abra a pasta em uma IA com acesso aos arquivos

Use, por exemplo, Cursor, Claude Code, Codex ou outra ferramenta capaz de ler e
escrever arquivos no projeto.

### 4. Envie uma vaga para a IA

Forneça a descrição completa, o HTML ou uma URL pública da vaga e use:

```text
Leia o EXECUTAR.md e execute todo o fluxo para esta vaga.
Use somente informações existentes na minha pasta base.
Crie a próxima pasta numerada em vagas, sem sobrescrever arquivos.

[COLE AQUI A DESCRIÇÃO OU O HTML DA VAGA]
```

A IA deve localizar o maior prefixo existente e usar o próximo número. Se a
última pasta for `09 - ...`, a nova será `10 - ...`. Se não houver nenhuma,
começará por `01 - ...`.

## Prompts úteis

### Criar uma candidatura completa

```text
Siga o EXECUTAR.md do começo ao fim para a vaga abaixo.
Não invente nenhuma informação sobre mim e registre os gaps no estudo da vaga.

[VAGA]
```

### Usar uma vaga salva em arquivo

```text
Siga o EXECUTAR.md usando o arquivo caminho/para/vaga.html.
Crie a próxima pasta numerada dentro de vagas.
```

### Atualizar a biblioteca pessoal

```text
Revise os arquivos base/curriculo-pt.md e base/resume-en.md.
Verifique se possuem conteúdo factual equivalente nos dois idiomas.
Não altere datas, cargos, empresas ou resultados sem me perguntar.
```

### Preparar-se para uma entrevista

```text
Leia a pasta da vaga número 03 e amplie o estudo-da-vaga.md com perguntas
técnicas e comportamentais. Diferencie fatos sobre mim de sugestões de estudo.
```

## Estrutura do projeto

```text
.
├── EXECUTAR.md
├── modelos/
│   ├── curriculo-pt.exemplo.md
│   └── resume-en.example.md
├── base/                  # privada: biblioteca pessoal
├── procedimentos/
│   ├── 1-extrair-vaga-html.md
│   └── 2-adequar-curriculo-vaga.md
└── vagas/                 # privada: 01 - ..., 02 - ..., 03 - ...
```

## Regra de ouro

Toda afirmação factual sobre a pessoa deve existir em `base/`. Quando um
requisito da vaga não estiver comprovado na base:

1. não o inclua no currículo;
2. marque-o como gap em `estudo-da-vaga.md`;
3. sugira uma forma honesta de abordá-lo na entrevista.

## Como o fluxo funciona

1. `EXECUTAR.md` orquestra todo o processo.
2. `procedimentos/1-extrair-vaga-html.md` transforma a vaga em requisitos
   estruturados.
3. `procedimentos/2-adequar-curriculo-vaga.md` cruza os requisitos com a base.
4. A IA cria a próxima pasta numerada e gera os sete documentos.

## Atualizando sua base

Quando adquirir uma experiência ou competência nova, atualize
`base/curriculo-pt.md` e `base/resume-en.md`. As candidaturas anteriores
continuam intactas, enquanto as próximas passam a usar a base atualizada.

## Licença

Distribuído sob a licença MIT.
