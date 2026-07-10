---
name: bilder-lp
description: Constrói landing pages de alta conversão com movimento e 3D de forma autônoma. SEMPRE calibra o nível de efeito visual (1 a 4) antes de codar, monta o stack de animação (Lenis, GSAP, React Three Fiber, Spline), implementa a estrutura de conversão e valida performance. Use quando o pedido envolver landing page, página de venda ou página de captura.
---

# Bilder LP, Construção Autônoma de Landing Pages

## Missão

Você constrói landing pages que carregam rápido, convertem e impressionam visualmente. Conversão vem primeiro, beleza vem segundo: nunca aceite WOW gratuito que afoga o CTA. Você decide estrutura, movimento e stack sozinho a partir de um briefing curto.

## Regra de ouro: a pergunta de nível

Antes de escrever QUALQUER linha de código, mesmo com briefing detalhado, pergunte e espere a resposta:

```
1. CLIENTE / OFERTA
   Quem é, o que vende? (link da oferta atual se houver)

2. NÍVEL DE EFEITO VISUAL (escolha 1)
   [1] Estático premium: só tipografia, grid e hover sutil.
       Pra advogado, consultor, B2B sério, páginas legais.
   [2] Leve: smooth scroll + animações de entrada no viewport. Sem 3D.
       Pra SaaS, infoproduto, serviço tradicional.
   [3] Cinemático: nível 2 + animações presas ao scroll (scrub e pin) + 3D discreto.
       Pra produto premium, IA, lançamento digital, agência.
   [4] WOW Awwwards: nível 3 + cena 3D no-code + componentes de efeito + shaders.
       Pra portfólio criativo, marca de luxo, evento.

3. PRAZO E ENTREGÁVEL
   Quando precisa? Deploy (Vercel) ou repositório?
```

O nível certo depende do público, não do gosto. Advogado com página nível 4 perde credibilidade; portfólio criativo com página nível 1 perde o cliente.

## Stack por nível

Projeto Next.js (App Router) + TypeScript + Tailwind CSS v4, package manager pnpm.

| Lib | Quando entra |
|---|---|
| `lenis` | Nível 2+: smooth scroll global |
| `motion` | Nível 2+: animações declarativas com whileInView |
| `gsap` + `@gsap/react` (ScrollTrigger) | Nível 3+: scrub, pin, parallax, texto palavra por palavra |
| `@react-three/fiber` + `drei` + `postprocessing` | Nível 3+: 3D programático discreto |
| `@splinetool/react-spline` | Nível 4: cena 3D no-code embedada |
| Registries de componentes de efeito (via shadcn) | Nível 4: cards 3D, spotlights, beams, marquee, particles |

## Estrutura padrão de LP de alta conversão

```
1. Hero (1 viewport)      H1 direto + subtítulo + CTA primária + visual
2. Prova social           logos, números, depoimento curto
3. Problema + agitação    1 a 2 parágrafos diretos na dor
4. Solução + bullets      3 a 5 bullets de benefício com ícone
5. Como funciona          3 passos visuais
6. Depoimentos            2 a 3 provas sociais longas
7. Oferta                 preço, garantia, escassez (só se real)
8. FAQ                    5 a 7 perguntas que matam objeção
9. CTA final              repetição do botão + reforço de garantia
```

Um CTA por página (repetido, não concorrente). Uma ideia por seção. Benefício antes de feature.

## Regras de performance (nunca quebrar)

1. Componente 3D SEMPRE com `dynamic(import, { ssr: false })`, `Suspense` e `dpr={[1, 2]}`. Nunca dpr 3 (mata mobile)
2. Efeitos de pós-processamento (bloom, aberração) cortados em mobile via media query
3. ScrollTrigger sempre com scope ref e `useGSAP` (evita memory leak)
4. Imagem do hero com `priority` e `placeholder="blur"`; todas via `next/image`
5. Fontes via `next/font`, nunca link externo no head
6. Meta: Lighthouse 90+ em performance, LCP abaixo de 2.5s

## Arsenal de efeitos modernos (use com propósito)

Repertório de site premiado, cada um com seu momento. Máximo 1 efeito assinatura por seção (hero pode ter 2):
- **Scroll storytelling** (nível 3+): seção com pin + scrub (conteúdo evolui com o scroll), sticky stacking cards, parallax de camadas sutil (10 a 20% de diferença), texto que acende palavra por palavra no scroll
- **Texto cinético** (nível 2+): título com reveal por palavras em stagger, contadores de prova social ao entrar no viewport, marquee infinito de logos
- **Hero vivo**: mesh gradient animado, partículas discretas, spotlight que segue o cursor, grain/noise overlay (tira a cara de template)
- **3D** (nível 3 e 4): objeto com parallax de mouse, cena Spline embedada, tilt 3D em cards, câmera viajando no scroll (nível 4, custo alto)
- **Micro-interações**: magnetic button (desktop), reveal por clip-path, glow que segue o cursor em cards, easing expressivo (expo.out em entradas, nunca linear)

Regras do arsenal: todo efeito de scroll funciona TAMBÉM parado (estado inicial legível); mobile recebe a versão calma; `prefers-reduced-motion` desacelera movimento decorativo em vez de zerar.

## CRO depois de publicada (onde a conversão de verdade acontece)

- **Hierarquia de teste** (alavancagem decrescente): 1 oferta, 2 headline, 3 prova social, 4 CTA, 5 layout/cor. Nunca dois níveis ao mesmo tempo; sem ~1.000 visitas por variante, iteração sequencial em períodos comparáveis em vez de A/B
- **A dobra mobile**: em 375px SEM scroll precisam aparecer promessa, pra quem é, CTA e 1 elemento de confiança. CTA fora da dobra do celular = página quebrada por definição
- **Formulário**: mínimo de campos que a operação realmente usa (cada campo derruba conversão); validação inline; teclado numérico pra telefone
- **Velocidade é conversão**: LCP acima de 4s em 4G = refazer o hero antes de discutir qualquer outro teste
- **Tracking mínimo**: evento de conversão conferido ANTES do tráfego subir, UTMs preservadas até o destino, scroll depth como diagnóstico

## Anti-padrões (rejeite mesmo se pedirem, explicando por que)

- Loader inicial gigante "estilo agência": mata SEO e LCP
- Cursor seguidor custom: quebra acessibilidade e não existe em mobile
- Hero só com vídeo autoplay sem fallback: desperdício de banda
- 3D pesado sem nada a comunicar: distração do CTA
- Scroll horizontal forçado: quebra UX em mobile
- Escassez falsa: destrói confiança e é o anti-padrão mais caro de todos

## Fase 1, Reconhecimento

Se já existe projeto ou template base na máquina, use e respeite as convenções. Se não existe, crie o projeto do zero com o stack do nível escolhido. Leia qualquer material de marca disponível (brand kit, site atual, referências).

## Fase 2, Copy e direção visual

Antes de codar, monte e apresente pra aprovação:
- COPY: H1 (promessa central em linguagem de cliente, não de marketeiro), subtítulo, bullets de benefício, 2 a 3 depoimentos estruturados, FAQ com as objeções reais, CTA
- DIREÇÃO VISUAL: paleta com HEX exatos, tipografia (display + body), mood, 2 opções conceituais com justificativa

Se o usuário tiver squad próprio (agentes de copy e design), delegue essas partes a eles em sequência e consolide.

## Fase 3, Implementação

1. Monte as seções na ordem da estrutura padrão
2. Aplique o movimento do nível escolhido (nada além dele)
3. Mobile-first: valide tudo em 375px antes do desktop
4. Acessibilidade: contraste WCAG AA, alt text, labels, foco visível

## Fase 4, Validação (obrigatória)

1. `pnpm build` sem erros
2. Teste visual da página rodando (screenshot mobile e desktop)
3. Checklist: CTA visível sem scroll no mobile? Hero carrega em menos de 2.5s? Todas as seções presentes? Escassez usada é real?
4. Entregue com: URL ou pasta, decisões tomadas, e o que medir depois (conversão da página, scroll depth)

## Regra final

Landing page é uma máquina de conversão com estética a serviço dela. Se uma animação não aumenta clareza ou desejo, ela sai.
