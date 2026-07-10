# Bilder, as skills que constroem por você

Cinco skills para Claude Code criadas por [@gastaomatos](https://instagram.com/gastaomatos). Cada uma constrói um sistema completo de forma autônoma: você diz o problema, ela projeta, constrói e valida. Sem pedir peça por peça.

## As skills

| Plugin | O que constrói |
|---|---|
| `bilder-squad` | Squads de agentes de IA completos: orquestrador, especialistas, skills e infraestrutura |
| `bilder-lp` | Landing pages de alta conversão com movimento e 3D, calibrando o nível de efeito (1 a 4) antes de codar |
| `bilder-oferta` | Oferta irrecusável pelo método Hormozi em 13 etapas sequenciais, com plano navegável em HTML |
| `bilder-conteudo` | Fábrica de carrosséis animados pra Instagram: copy, cards HTML com GSAP e render em vídeo |
| `bilder-mcp` | Servidores MCP em TypeScript que conectam a IA em qualquer API externa |

## Como instalar

No Claude Code, rode:

```
/plugin marketplace add drtrafego/squad-builder-marketplace
/plugin install bilder-squad
```

Troque `bilder-squad` pelo plugin que quiser (`bilder-lp`, `bilder-oferta`, `bilder-conteudo`, `bilder-mcp`) ou instale todos. Reinicie o Claude Code se a skill não aparecer de imediato.

Também dá pra baixar tudo em ZIP: [squad-builder-marketplace (main.zip)](https://github.com/drtrafego/squad-builder-marketplace/archive/refs/heads/main.zip)

## Como usar

Dentro do Claude Code, descreva o que você quer construir. A skill certa entra sozinha, faz poucas perguntas (máximo 2 por vez) e constrói o sistema completo, com validação no final.

Exemplos:
- "Monta um squad pra produzir anúncios do meu restaurante" (bilder-squad)
- "Preciso de uma LP pra minha mentoria, público executivo" (bilder-lp)
- "Sei muito de confeitaria mas não sei o que vender" (bilder-oferta)
- "Quero postar carrossel todo dia sem virar refém de designer" (bilder-conteudo)
- "Quero que o Claude opere minha conta de anúncios de verdade" (bilder-mcp)

## O que vem dentro

```
squad-builder-marketplace/
├── .claude-plugin/
│   └── marketplace.json           define este marketplace
├── plugins/
│   ├── bilder-squad/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/bilder-squad/SKILL.md
│   ├── bilder-lp/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/bilder-lp/SKILL.md
│   ├── bilder-oferta/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/bilder-oferta/SKILL.md
│   ├── bilder-conteudo/
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/bilder-conteudo/SKILL.md
│   └── bilder-mcp/
│       ├── .claude-plugin/plugin.json
│       └── skills/bilder-mcp/SKILL.md
└── README.md
```

## Nota de migração

As skills se chamavam `squad-builder`, `lp-builder`, `oferta-builder`, `conteudo-builder` e `mcp-builder` até 10/07/2026. Quem instalou `squad-builder` antes: desinstale e instale `bilder-squad` pra continuar recebendo atualizações.

## Publicar (para o autor)

1. Edite o `SKILL.md` da skill que quiser evoluir, suba a versão no `plugin.json` correspondente
2. Commit e push: quem instalou recebe na próxima atualização de plugins
3. Pra distribuir uma skill avulsa como arquivo, zipe a pasta da skill (ex: `bilder-lp/SKILL.md`) com extensão `.skill`
