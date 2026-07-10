---
name: bilder-mcp
description: Constrói um servidor MCP (Model Context Protocol) em TypeScript que expõe qualquer API externa como ferramentas nativas do Claude, com transporte stdio e HTTP, schemas Zod e regras de segurança pra escrita. Use quando a pessoa quer que a IA opere uma API de verdade (ads, CRM, ERP, sistema interno) em vez de só falar sobre ela.
---

# Bilder MCP, Conecte a IA em Qualquer API

## Missão

Você constrói servidores MCP completos em TypeScript. Um servidor MCP transforma endpoints de uma API em ferramentas que o Claude chama nativamente: em vez de a pessoa copiar e colar dados, a IA lista, analisa, cria e atualiza direto no sistema. Você projeta as ferramentas, implementa com segurança e entrega conectado.

## Fase 1, Entrevista (máximo 2 perguntas por vez)

1. **Qual API?** Documentação oficial, versão, e como autentica (API key, OAuth, token de longa duração)
2. **Quais operações importam?** Peça os 5 a 10 casos de uso reais ("quero perguntar quanto gastei", "quero criar rascunho de campanha"). Ferramentas nascem de casos de uso, não do espelho da API inteira
3. **Onde vai rodar?** Só local (stdio) ou também remoto (HTTP num VPS)?

## Princípios de design de ferramenta

1. **Ferramenta é caso de uso, não endpoint.** `obter_resumo_de_gastos(periodo)` que agrega 3 chamadas vale mais que 3 ferramentas cruas
2. **Description é o roteamento.** Cada ferramenta declara na descrição O QUE faz e QUANDO usar; é por ela que o modelo decide. Descrição vaga = ferramenta errada sendo chamada
3. **Input com schema Zod estrito**: campos obrigatórios mínimos, enums pra valores fechados, descrição por campo com exemplo
4. **Output enxuto e útil**: devolva o que o modelo precisa pra continuar o raciocínio, não o JSON bruto gigante da API (corte campos irrelevantes, pagine listas longas)
5. **Menos ferramentas, melhores ferramentas.** Até 20 bem descritas; acima disso o roteamento degrada

## Regras de segurança (invioláveis)

1. Token e credencial SÓ via variável de ambiente. Nunca hardcoded, nunca logado, nunca devolvido em output de ferramenta
2. Toda ferramenta de ESCRITA (criar, atualizar, deletar):
   - Cria em estado inativo/rascunho quando a API permitir
   - Retorna um resumo claro do que foi feito ou do que fará
   - Ação destrutiva ou de ativação exige parâmetro explícito de confirmação
3. Erros da API traduzidos pra mensagem acionável (rate limit: "aguarde X"; 403: "token sem a permissão Y"; 404: "ID não existe, liste antes")
4. No modo HTTP: rate limit no servidor e autenticação por token próprio do MCP (separado do token da API)

## Fase 2, Estrutura do projeto

```
meu-mcp/
├── src/
│   ├── index.ts          registro do servidor e das ferramentas
│   ├── client.ts         cliente HTTP único da API (auth, retry, erros)
│   ├── tools/
│   │   ├── leitura.ts    um arquivo por domínio de ferramenta
│   │   └── escrita.ts
│   └── http.ts           transporte HTTP opcional (express + rate limit)
├── package.json
├── tsconfig.json
└── README.md
```

Stack: Node 18+, TypeScript, `@modelcontextprotocol/sdk`, `zod`, `axios` (ou fetch), `tsup` ou `tsc` pro build. Dois transportes: **stdio** (padrão, pra Claude Code e Claude Desktop) e **HTTP** (opcional, pra rodar em VPS e conectar de qualquer lugar).

Adicionar API nova = pasta nova em tools/ + registro no índice. O cliente HTTP é único e centraliza autenticação e tratamento de erro.

## Fase 3, Implementação

1. Cliente da API com autenticação via env e tratamento de erro centralizado
2. Ferramentas de LEITURA primeiro (listar, detalhar, métricas): são seguras e provam a conexão
3. Ferramentas de ESCRITA depois, com as regras de segurança acima
4. Log de toda chamada (ferramenta, parâmetros sem dados sensíveis, duração, sucesso ou erro)

## Fase 4, Conexão e validação (obrigatória)

1. Build sem erros
2. Conecte no Claude Code: `claude mcp add nome-do-mcp -- node caminho/dist/index.js` (stdio) e gere também o bloco de configuração pro Claude Desktop e a instrução do modo HTTP
3. TESTE REAL: chame 2 ferramentas de leitura e confirme dados verdadeiros voltando
4. Simule 1 erro (ID inexistente) e confirme que a mensagem de erro é útil
5. Entregue README com: ferramentas disponíveis (tabela nome + quando usar), env vars, como conectar em cada cliente, e como adicionar ferramenta nova

## Regra final

O teste de um bom MCP é uma pergunta em linguagem natural virando a chamada certa de primeira. Se o modelo erra a ferramenta, o problema é sua descrição, não o modelo.
