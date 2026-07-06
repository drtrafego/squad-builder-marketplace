# Squad Builder, a skill que monta agentes

Skill para Claude Code que constrói **squads de agentes de IA completos de forma autônoma**: você diz o problema, ela projeta a arquitetura, cria os agentes especialistas, define o fluxo e monta toda a infraestrutura. Sem você pedir peça por peça.

Criado por [@gastaomatos](https://instagram.com/gastaomatos).

## Como instalar

No Claude Code, rode:

```
/plugin marketplace add drtrafego/squad-builder-marketplace
/plugin install squad-builder
```

Reinicie o Claude Code se a skill não aparecer de imediato.

Também dá pra baixar a skill direto em ZIP: [squad-builder-marketplace (main.zip)](https://github.com/drtrafego/squad-builder-marketplace/archive/refs/heads/main.zip)

## Como usar

Dentro do Claude Code, chame a skill e descreva o que o squad precisa resolver. Ela faz poucas perguntas (objetivo, entrada e saída, subtarefas) e constrói o time completo.

Exemplos de squads que dá pra montar: produção de anúncios (copy, arte, render, gestor), construção de ofertas, atendimento, pesquisa, criação de conteúdo.

## O que vem dentro

```
squad-builder-marketplace/
├── .claude-plugin/
│   └── marketplace.json          # define este marketplace
├── plugins/
│   └── squad-builder/
│       ├── .claude-plugin/
│       │   └── plugin.json        # define o plugin
│       └── skills/
│           └── mestre-squad-builder/
│               └── SKILL.md       # a skill em si
└── README.md
```

## Publicar (para o autor)

1. Suba esta pasta num repositório público no GitHub (ex: `drtrafego/squad-builder-marketplace`).
2. Compartilhe os dois comandos de instalação acima com quem for usar.
3. Para atualizar a skill, edite o `SKILL.md`, faça commit e os usuários recebem na próxima atualização.
