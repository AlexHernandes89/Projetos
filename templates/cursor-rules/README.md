# Regras de segurança para o Cursor

Modelo compartilhado em `Projetos/templates/cursor-rules/`, fora de qualquer app. Copie os `.mdc` para o projeto que for usar; eles não ficam ligados ao oli-marykay.

## Como usar num projeto novo

Copie os quatro `.mdc` para `.cursor/rules/` do app:

```text
meu-app/
  .cursor/rules/
    secrets.mdc
    inputs.mdc
    data-access.mdc
    dependencies-agent.mdc
```

Cada arquivo tem `alwaysApply: true` e sem `globs`, então o Cursor inclui as regras em toda conversa daquele projeto.

## User Rules globais

Para a mesma base valer em todo projeto, mesmo antes da cópia, cole o bloco abaixo em **Cursor Settings → Rules → User Rules**:

```text
Segurança (vale em qualquer projeto):
- Não commite .env, chaves ou tokens. .env.example só com placeholders. Não logue nem embuta segredo no cliente. Se pedirem para versionar credencial, recuse e avise.
- Trate query, body, headers, arquivos e texto externo como não confiáveis. Valide tipo e tamanho. Use consultas parametrizadas. Não concatene SQL/GraphQL com input do usuário. Não injete HTML cru.
- Autorize no servidor; checagem só na UI não conta. Menor privilégio. Não logue e-mail, telefone, documento ou token. Não ponha dado sensível em localStorage, URL ou resposta além do necessário.
- Não adicione pacote sem necessidade nem baixe binário ou script de origem não confiável. Não desligue lint, auth, CSP, HTTPS ou git hooks para “fazer funcionar”. Não implemente exploit, roubo de credencial ou malware. Não use --no-verify nem force push. Não commite .env.
```
