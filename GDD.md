# ColdLine.C — Game Design Document

**Versao:** 1.0
**Data:** 24/10/2026
**Genero:** Acao top-down
**Plataforma:** Navegador (desktop)
**Tecnologias:** TypeScript, HTML5 Canvas, CSS
**Referencia principal:** Hotline Miami

---

## Sumario

1. [Ficha tecnica](#1-ficha-tecnica)
2. [Visao geral e pilares](#2-visao-geral-e-pilares)
3. [Historia e ambientacao](#3-historia-e-ambientacao)
4. [Personagem principal](#4-personagem-principal)
5. [Gameplay loop](#5-gameplay-loop)
6. [Mecanicas detalhadas](#6-mecanicas-detalhadas)
7. [IA dos inimigos](#7-ia-dos-inimigos)
8. [Controles](#8-controles)
9. [Nivel do prototipo](#9-nivel-do-prototipo)
10. [Direcao de arte](#10-direcao-de-arte)
11. [Audio](#11-audio)
12. [Arquitetura tecnica](#12-arquitetura-tecnica)
13. [Escopo, riscos e proximos passos](#13-escopo-riscos-e-proximos-passos)

---

## 1. Ficha tecnica

| Item | Descricao |
| --- | --- |
| Titulo | ColdLine.C |
| Genero | Acao top-down |
| Perspectiva | Vista superior (top-down) |
| Plataforma | Navegador desktop |
| Tecnologias | TypeScript + HTML5 Canvas + CSS |
| Inspiracao | Hotline Miami |
| Publico-alvo | Jogadores de acao rapida e fãs de pixel art |
| Classificacao indicativa | 16 anos (violencia estilizada) |
| Modo | Um jogador |
| Escopo desta versao | Prototipo de um nivel |

---

## 2. Visao geral e pilares

**ColdLine.C** e um jogo de acao em vista superior no qual o jogador controla um policial decidido a limpar as ruas de sua cidade, prendendo e neutralizando criminosos. O combate e rapido, o inimigo e perigoso e o jogador tambem cai com poucos golpes, o que valoriza planejamento e execucao precisa.

### Pilares de design

1. **Combate letal e rapido** — o jogador e forte, mas vulneravel. Cada erro custa caro.
2. **Planejamento antes da acao** — observar a sala, escolher a rota e a arma certa.
3. **Estetica pixel art com clima neon** — visual inspirado em Hotline Miami e synthwave.
4. **Progressao por dominio** — fases curtas e rejogaveis; o jogador melhora com pratica.

---

## 3. Historia e ambientacao

O protagonista e um policial experiente de ColdLine, uma cidade fictícia tomada por faccoes criminosas. Apos anos vendo criminosos sairem impunes, ele decide agir fora do sistema: entrar nos esconderijos, atordoar os suspeitos e desmontar as operacoes uma por uma.

- **Tom:** sombrio, tenso e estilizado; violencia tratada de forma arcade.
- **Cenario:** becos, armazens, bares e predios abandonados com iluminacao neon.
- **Narrativa:** apresentada em textos curtos entre fases (sem cutscenes no prototipo).

---

## 4. Personagem principal

| Atributo | Valor |
| --- | --- |
| Nome | O Policial (ColdLine) |
| Motivacao | Limpar a cidade da criminalidade |
| Vida | Baixa (2 a 3 golpes) |
| Velocidade | Media; corrida com penalidade de ruido |
| Armas iniciais | Soco, cacetete, mata-leao |
| Armas obtidas | Armas dos inimigos derrubados |
| Limitacao | Sem cura; sem armadura |

---

## 5. Gameplay loop

```
[Inicio da fase]
       |
       v
[Observar e planejar rota]
       |
       v
[Entrar na area e atordoar o primeiro inimigo]
       |
       v
[Pegar a arma derrubada / trocar de arma]
       |
       v
[Eliminar ou prender os demais inimigos]
       |
       v
[Concluir objetivo da fase]
       |
       v
[Pontuacao + proxima fase]
```

---

## 6. Mecanicas detalhadas

### 6.1 Movimento e colisao

- Movimento em 8 direcoes (WASD ou setas).
- Colisao com paredes, moveis e inimigos.
- Corrida (Shift) aumenta velocidade e o raio de deteccao dos inimigos.

### 6.2 Ataques corpo a corpo

| Ataque | Alcance | Efeito | Observacao |
| --- | --- | --- | --- |
| Soco | Curto | Atordoa | Rapido, sem custo |
| Cacetete | Medio | Atordoa ou neutraliza | Arma inicial do policial |
| Mata-leao | Muito curto | Neutraliza silenciosamente | Exige estar pelas costas |
| Arma de fogo (inimigo) | Longo | Dano alto | Municao limitada |

### 6.3 Atordoar versus neutralizar

- **Atordoado:** o inimigo cai e pode ser algemado (objetivo de "prender") ou finalizado.
- **Neutralizado:** o inimigo sai de combate permanentemente.
- O jogador escolhe entre prender (mais pontos) e neutralizar (mais rapido).

### 6.4 Armas no chao

- Inimigos derrubados deixam sua arma no chao.
- O jogador pega a arma com **E** e a substitui pela atual.
- Armas de fogo possuem municao e podem ser descartadas ao esvaziar.
- Armas corpo a corpo nao possuem municao.

### 6.5 Condicoes de vitoria e derrota

- **Vitoria:** concluir o objetivo da fase (ex.: neutralizar/prender todos os alvos).
- **Derrota:** vida do jogador chegar a zero.
- **Reinicio:** reinicio instantaneo da fase com **R**.

---

## 7. IA dos inimigos

| Estado | Comportamento |
| --- | --- |
| Patrulha | Anda por pontos fixos predefinidos |
| Suspeita | Investiga ruido ou visao parcial do jogador |
| Alerta | Persegue o jogador e chama reforcos |
| Ataque | Ataca corpo a corpo ou atira a distancia |
| Atordoado | Fica imovel e vulneravel |
| Fora de combate | Neutralizado ou preso |

Regras iniciais:
- Deteccao por cone de visao e por ruido (corrida, tiros, portas).
- Inimigos nao enxergam atraves de paredes.
- Tempo de reacao configuravel para balancear a dificuldade.

---

## 8. Controles

| Acao | Tecla |
| --- | --- |
| Mover | W A S D |
| Correr | Shift |
| Mirar | Mouse |
| Atacar | Botao esquerdo do mouse |
| Interagir / pegar arma | E |
| Reiniciar fase | R |
| Pausar | Esc |

---

## 9. Nivel do prototipo

**Nome:** Armazem da Docas
**Objetivo:** neutralizar ou prender 5 criminosos e sair pela porta leste.

```
+-----------------------------------+
|  ENTRADA        CAIXAS      SAIDA |
|  [P]   . . . .  [XX]  . .  [E]    |
|  . . . . . . .  [XX]  . .  .      |
|  [1]  . . [2] . . . . [3]  .      |
|  . . . . . . . . . . . .  .       |
|  [4]  . . . . [5] . . . . .       |
|  . . . . . . . . . . . .  .       |
+-----------------------------------+
P = jogador | 1..5 = inimigos | XX = caixas | E = saida
```

- **Inimigos:** 5, com armas variadas (2 corpo a corpo, 2 com pistola, 1 com cacetete).
- **Armas no cenario:** 1 cacetete extra e 1 pistola com municao limitada.
- **Duracao estimada:** 2 a 4 minutos por tentativa.
- **Visao futura:** novas fases (beco, bar, predio) com layouts e objetivos proprios.

---

## 10. Direcao de arte

- **Estilo:** pixel art top-down, inspirado em Hotline Miami.
- **Resolucao base:** 320 x 180, escalada em multiples inteiros para manter os pixels nitidos.
- **Tiles:** 16 x 16 pixels.
- **Paleta:** tons escuros de azul e roxo com destaques neon (rosa, ciano, amarelo).
- **Animacoes:** 4 direcoes, 4 a 6 frames por acao (andar, atacar, atordoado).
- **Interface:** HUD minimalista com vida, arma atual e objetivo.

---

## 11. Audio

- **Trilha:** synthwave/arcade em loop por fase.
- **Efeitos:** soco, cacetete, tiro, passos, alarme, conclusao de fase.
- **Prototipo:** sons e musicas gratuitos ou placeholders, com licenca compativel.
- **Regra:** volume separado para musica e efeitos.

---

## 12. Arquitetura tecnica

### 12.1 Stack

- **TypeScript** para logica e tipagem.
- **HTML5 Canvas** para renderizacao 2D.
- **CSS** para layout da pagina e HUD.
- **Vite** como servidor de desenvolvimento e build.

### 12.2 Estrutura de pastas proposta

```
coldline.c/
|-- index.html
|-- package.json
|-- tsconfig.json
|-- src/
|   |-- main.ts
|   |-- engine/
|   |   |-- loop.ts
|   |   |-- input.ts
|   |   |-- renderer.ts
|   |   `-- collision.ts
|   |-- entities/
|   |   |-- player.ts
|   |   |-- enemy.ts
|   |   `-- weapon.ts
|   |-- systems/
|   |   |-- combat.ts
|   |   |-- ai.ts
|   |   `-- level.ts
|   `-- levels/
|       `-- warehouse.ts
`-- assets/
    |-- sprites/
    |-- tiles/
    `-- audio/
```

### 12.3 Loop de jogo

1. Ler entrada do teclado e mouse.
2. Atualizar entidades com base no delta time.
3. Resolver colisoes.
4. Atualizar IA e estado de combate.
5. Renderizar o cenario, entidades e HUD no Canvas.
6. Repetir via `requestAnimationFrame`.

---

## 13. Escopo, riscos e proximos passos

### Escopo do prototipo

- Uma fase jogavel: Armazem da Docas.
- Movimento, tres ataques corpo a corpo e coleta de armas.
- IA basica com patrulha, alerta e ataque.
- HUD com vida, arma e objetivo.
- Arte pixel art provisoria e audio placeholder.

### Fora do escopo (visao futura)

- Multiplos niveis e progressao.
- Narrativa entre fases.
- Ranking de pontuacao.
- Editor de fases.
- Suporte a controle e mobile.

### Riscos

| Risco | Impacto | Mitigacao |
| --- | --- | --- |
| Arte pixel art demorada | Alto | Usar assets provisorios e refinar depois |
| IA complexa demais | Medio | Comecar com 2 estados e evoluir |
| Tempo de desenvolvimento | Medio | Entregar o prototipo de 1 nivel primeiro |
| Balanceamento de dificuldade | Medio | Ajustar tempos e dano por testes |

### Proximos passos

1. Configurar o projeto com TypeScript, Vite e Canvas.
2. Implementar movimento e colisao do jogador.
3. Implementar ataques e coleta de armas.
4. Implementar IA e condicoes de vitoria/derrota.
5. Montar o nivel Armazem da Docas.
6. Aplicar arte e audio.
7. Testar, balancear e publicar no navegador.
