# Skills Mestre, o marketplace do @gastaomatos

Cinco skills para Claude Code que constroem sistemas completos de forma autônoma: você diz o problema, a skill projeta, constrói e valida. Sem pedir peça por peça.

Criado por [@gastaomatos](https://instagram.com/gastaomatos).

## As skills

| Plugin | Skill | O que constrói |
|---|---|---|
| `squad-builder` | mestre-squad-builder | Squads de agentes de IA completos: orquestrador, especialistas, skills e infraestrutura |
| `lp-builder` | mestre-lp | Landing pages de alta conversão com movimento e 3D, calibrando o nível de efeito (1 a 4) antes de codar |
| `oferta-builder` | mestre-oferta | Oferta irrecusável pelo método Hormozi em 13 etapas sequenciais, com plano navegável em HTML |
| `conteudo-builder` | mestre-conteudo | Fábrica de carrosséis animados pra Instagram: copy, cards HTML com GSAP e render em vídeo |
| `mcp-builder` | mestre-mcp | Servidores MCP em TypeScript que conectam a IA em qualquer API externa |

## Como instalar

No Claude Code, rode:

```
/plugin marketplace add drtrafego/squad-builder-marketplace
/plugin install squad-builder
```

Troque `squad-builder` pelo plugin que quiser (`lp-builder`, `oferta-builder`, `conteudo-builder`, `mcp-builder`) ou instale todos. Reinicie o Claude Code se a skill não aparecer de imediato.

Também dá pra baixar tudo em ZIP: [squad-builder-marketplace (main.zip)](https://github.com/drtrafego/squad-builder-marketplace/archive/refs/heads/main.zip)

## Como usar

Dentro do Claude Code, descreva o que você quer construir. A skill certa entra sozinha, faz poucas perguntas (máximo 2 por vez) e constrói o sistema completo, com validação no final.

Exemplos:
- "Monta um squad pra produzir anúncios do meu restaurante" (squad-builder)
- "Preciso de uma LP pra minha mentoria, público executivo" (lp-builder)
- "Sei muito de confeitaria mas não sei o que vender" (oferta-builder)
- "Quero postar carrossel todo dia sem virar refém de designer" (conteudo-builder)
- "Quero que o Claude opere minha conta de anúncios de verdade" (mcp-builder)

## O que vem dentro

```
squad-builder-marketplace/
├── .claude-plugin/
│   └── marketplace.json           define este marketplace
├── plugins/
│   ├── squad-builder/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/mestre-squad-builder/SKILL.md
│   ├── lp-builder/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/mestre-lp/SKILL.md
│   ├── oferta-builder/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/mestre-oferta/SKILL.md
│   ├── conteudo-builder/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/mestre-conteudo/SKILL.md
│   └── mcp-builder/
│       ├── .claude-plugin/plugin.json
│       └── skills/mestre-mcp/SKILL.md
└── README.md
```

## Publicar (para o autor)

1. Edite o `SKILL.md` da skill que quiser evoluir, suba a versão no `plugin.json` correspondente
2. Commit e push: quem instalou recebe na próxima atualização de plugins
3. Pra distribuir uma skill avulsa como arquivo, zipe a pasta da skill (ex: `mestre-lp/SKILL.md`) com extensão `.skill`
