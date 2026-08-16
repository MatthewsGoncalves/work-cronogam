# Biblioteca privada de vagas

Cada candidatura gerada fica nesta pasta e é ignorada pelo Git.

As pastas seguem uma sequência numérica:

```text
01 - Desenvolvedor Frontend - Empresa A
02 - Software Engineer - Empresa B
03 - Analista de Dados - Empresa C
```

Ao criar uma vaga:

1. Liste as pastas existentes.
2. Localize o maior prefixo numérico.
3. Use o próximo número, sempre com pelo menos dois dígitos.
4. Nunca reutilize um número nem sobrescreva uma pasta existente.

Se não houver nenhuma vaga numerada, comece por `01`.

