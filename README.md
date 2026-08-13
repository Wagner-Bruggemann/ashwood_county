# Ashwood County

**Ashwood County** é um jogo de sobrevivência e terror rural desenvolvido em **Godot**.

O projeto combina gerenciamento de fazenda, exploração, sobrevivência, construção e horror psicológico em uma região isolada onde eventos estranhos começam a transformar uma rotina aparentemente simples em algo muito maior.

O objetivo do projeto é construir os sistemas do jogo de forma **modular, desacoplada e reutilizável**, permitindo que funcionalidades como inventário, necessidades do personagem, construção, agricultura, combate e IA possam evoluir independentemente.

---

## 🎮 Conceito

O jogador chega a uma propriedade rural localizada em **Ashwood County**.

Durante o dia, a região parece relativamente normal. O jogador precisa administrar recursos, cultivar alimentos, explorar propriedades próximas, melhorar equipamentos e preparar a fazenda.

Quando a noite chega, as regras mudam.

A floresta, as plantações e os locais abandonados escondem fenômenos que não parecem seguir as leis normais do mundo.

Ao longo do jogo, o jogador começa a descobrir que Ashwood County possui uma história muito mais antiga e perturbadora do que aparenta.

---

## 🌾 Principais mecânicas

O projeto pretende incluir:

* Agricultura
* Plantio e colheita
* Criação de animais
* Inventário baseado em grid
* Containers e armazenamento
* Equipamentos
* Sistema de peso
* Crafting
* Construção
* Necessidades do personagem
* Vida
* Fome
* Sede
* Sono
* Sanidade
* Exploração
* Comércio
* NPCs
* Combate
* Armas de fogo
* Ferramentas
* Animais selvagens
* Inimigos
* IA baseada em visão e audição
* Ciclo de dia e noite
* Eventos sobrenaturais
* Exploração de cavernas e locais abandonados
* Progressão narrativa através do ambiente

---

# 🛠 Tecnologia

## Engine

**Godot 4**

## Linguagem

**GDScript**

O projeto prioriza GDScript pela integração direta com a Godot, velocidade de desenvolvimento e facilidade para criação e iteração dos sistemas de gameplay.

---

# 🧱 Filosofia de arquitetura

Ashwood County utiliza uma abordagem baseada em **sistemas modulares**.

A intenção é evitar que toda a lógica do jogo fique diretamente acoplada aos Nodes e cenas da Godot.

Sempre que possível, cada mecânica deve existir como um sistema relativamente independente.

Exemplos:

```text
Inventory
Health
Needs
Farming
Building
Combat
Interaction
Equipment
AI
Time
Trading
```

Cada sistema deve possuir uma responsabilidade clara e depender do menor número possível de outros sistemas.

---

# 🔌 Sistemas plugáveis

Uma das principais metas arquiteturais do projeto é permitir que sistemas possam ser adicionados ou removidos sem exigir grandes alterações no restante do jogo.

Exemplo:

```text
Player
 ├── HealthComponent
 ├── NeedsComponent
 ├── InventoryComponent
 ├── EquipmentComponent
 └── InteractionComponent
```

Um animal poderia utilizar:

```text
Animal
 ├── HealthComponent
 ├── NeedsComponent
 └── AIComponent
```

Enquanto um container poderia possuir apenas:

```text
Chest
 └── InventoryComponent
```

Isso permite reutilizar componentes em diferentes entidades.

---

# 📡 Comunicação entre sistemas

Sistemas devem evitar referências diretas uns aos outros sempre que possível.

A comunicação pode acontecer através de:

```text
Commands
Events
Signals
Resources
Interfaces/Contracts
```

A regra geral é:

### Command

Representa uma intenção.

Exemplo:

```text
MovePlayerCommand
PickUpItemCommand
DropItemCommand
UseItemCommand
PlaceBuildingCommand
AttackCommand
```

Normalmente existe apenas um responsável por executar um Command.

---

### Event

Representa algo que já aconteceu.

Exemplo:

```text
ItemPickedUp
ItemDropped
PlayerDamaged
PlayerDied
BuildingPlaced
CropHarvested
GunFired
SoundEmitted
```

Vários sistemas podem reagir ao mesmo evento.

Exemplo:

```text
GunFired
   │
   ├── AudioSystem
   ├── EnemyHearingSystem
   ├── AnimationSystem
   └── AlertSystem
```

---

# 🧩 Componentes

Componentes devem representar principalmente **dados ou capacidades**.

Exemplos:

```text
HealthComponent
InventoryComponent
EquipmentComponent
NeedsComponent
InteractableComponent
DamageableComponent
VisionComponent
HearingComponent
```

Sempre que possível, componentes não devem concentrar grandes quantidades de regras de negócio.

As regras devem permanecer nos sistemas responsáveis.

---

# ⚙️ Systems

Systems executam as regras do jogo.

Exemplos:

```text
HealthSystem
InventorySystem
InteractionSystem
FarmingSystem
BuildingSystem
CombatSystem
EnemyVisionSystem
EnemyHearingSystem
NeedsSystem
TimeSystem
```

Um sistema deve possuir uma responsabilidade claramente definida.

---

# 🗂 Estrutura inicial

Uma possível organização do projeto:

```text
res://
│
├── assets/
│   ├── audio/
│   ├── materials/
│   ├── models/
│   ├── textures/
│   └── ui/
│
├── scenes/
│   ├── characters/
│   ├── enemies/
│   ├── items/
│   ├── props/
│   ├── buildings/
│   ├── ui/
│   └── world/
│
├── scripts/
│   │
│   ├── core/
│   │   ├── commands/
│   │   ├── events/
│   │   ├── components/
│   │   └── shared/
│   │
│   ├── systems/
│   │   ├── inventory/
│   │   ├── health/
│   │   ├── needs/
│   │   ├── interaction/
│   │   ├── farming/
│   │   ├── building/
│   │   ├── combat/
│   │   └── ai/
│   │
│   ├── actors/
│   │   ├── player/
│   │   ├── enemies/
│   │   ├── animals/
│   │   └── npc/
│   │
│   ├── infrastructure/
│   │   ├── persistence/
│   │   ├── configuration/
│   │   └── events/
│   │
│   └── ui/
│
├── resources/
│   ├── items/
│   ├── crops/
│   ├── buildings/
│   ├── enemies/
│   └── configuration/
│
├── tests/
│
├── project.godot
└── README.md
```

Essa estrutura é apenas uma referência inicial e deverá evoluir junto com o projeto.

---

# 📦 Resources

Dados configuráveis devem utilizar **Godot Resources** sempre que fizer sentido.

Por exemplo:

```text
ItemDefinition
WeaponDefinition
CropDefinition
BuildingDefinition
EnemyDefinition
RecipeDefinition
```

Exemplo conceitual:

```text
ItemDefinition

id
display_name
description
weight
icon
world_scene
stack_size
category
```

Isso permite criar novos conteúdos sem alterar a lógica dos sistemas.

---

# 🎒 Inventário

O inventário será baseado em grid, inspirado em jogos como:

* Resident Evil
* Escape from Tarkov
* Arena Breakout

Itens podem ocupar múltiplas células.

Exemplo:

```text
┌───┬───┬───┬───┐
│   │███│███│   │
├───┼───┼───┼───┤
│   │███│███│   │
├───┼───┼───┼───┤
│   │   │   │   │
└───┴───┴───┴───┘
```

O sistema deverá suportar futuramente:

* rotação de itens;
* diferentes containers;
* mochilas;
* bolsos;
* equipamentos;
* chão;
* baús;
* peso;
* stack;
* transferência de itens;
* inspeção 3D.

---

# 🏗 Construção

O sistema de construção será desenvolvido inicialmente de forma simples.

Fluxo básico:

```text
Selecionar construção
        ↓
Mostrar preview/ghost
        ↓
Escolher posição
        ↓
Validar terreno
        ↓
Confirmar
        ↓
Criar construção
```

Posteriormente o sistema poderá evoluir para construção baseada em materiais e etapas.

---

# 🌱 Agricultura

Fluxo básico:

```text
Preparar solo
    ↓
Plantar
    ↓
Regar
    ↓
Crescimento
    ↓
Colher
```

Culturas devem ser orientadas por configuração através de Resources.

Exemplo:

```text
CropDefinition

id
name
growth_time
water_requirement
harvest_item
harvest_amount
growth_stages
```

---

# 👁 Inteligência artificial

A IA deverá ser baseada em sistemas independentes de percepção.

Inicialmente:

```text
Vision
Hearing
State
Navigation
Combat
```

Exemplo:

```text
Enemy
 │
 ├── VisionComponent
 ├── HearingComponent
 ├── HealthComponent
 └── AIStateComponent
```

Fluxo possível:

```text
SoundEmitted
      ↓
EnemyHearingSystem
      ↓
SoundDetected
      ↓
EnemyAI
      ↓
Investigate
```

Da mesma forma:

```text
Player enters vision cone
        ↓
EnemyVisionSystem
        ↓
TargetDetected
        ↓
EnemyAI
        ↓
Chase
```

---

# 🌙 Dia e noite

O ciclo de tempo é uma parte importante do gameplay.

Durante o dia o foco será principalmente:

```text
Fazenda
Exploração
Coleta
Comércio
Construção
Preparação
```

Durante a noite:

```text
Sobrevivência
Tensão
Eventos
Inimigos
Defesa
Horror
```

A transição entre os dois períodos deverá alterar significativamente o comportamento do mundo.

---

# 💾 Save

O sistema de save deverá armazenar apenas estado relevante do jogo.

Exemplos:

```text
Player state
Inventory
Equipment
World time
Buildings
Containers
Crops
NPC state
Quest state
World events
```

Nodes da Godot não devem ser considerados diretamente o estado persistente do jogo.

---

# 🧪 Testabilidade

Sistemas importantes devem possuir lógica independente da interface sempre que possível.

Isso permitirá testar regras como:

```text
Adicionar item ao inventário
Mover item dentro do grid
Aplicar dano
Consumir alimento
Consumir água
Avançar crescimento de planta
Validar construção
Detectar inimigo
Calcular peso
```

sem precisar carregar todo o mundo do jogo.

---

# 📐 Princípios

O desenvolvimento de Ashwood County deverá seguir algumas regras simples.

### Simplicidade primeiro

Não criar infraestrutura complexa antes que ela seja necessária.

### Composição sobre herança

Preferir:

```text
Player
 + Health
 + Inventory
 + Needs
```

em vez de grandes árvores de herança.

### Baixo acoplamento

Sistemas não devem depender diretamente uns dos outros quando uma mensagem, evento ou contrato resolver o problema.

### Dados separados da lógica

Resources armazenam configurações.

Systems executam regras.

Scenes representam objetos do mundo e sua apresentação.

### Godot como engine, não como arquitetura inteira

Nodes continuam sendo fundamentais para:

```text
Rendering
Physics
Audio
Input
Navigation
Animation
UI
```

mas regras importantes de gameplay devem permanecer organizadas em seus respectivos sistemas.

### Vertical slices

Cada funcionalidade deve ser desenvolvida primeiro na menor versão funcional possível.

Depois ela pode ser expandida.

---

# 🗺 Roadmap inicial

## Fase 1 — Fundação

* [ ] Estrutura base do projeto
* [ ] Player
* [ ] Câmera em primeira pessoa
* [ ] Movimento
* [ ] Interação
* [ ] Sistema de Commands
* [ ] Sistema de Events

## Fase 2 — Itens

* [ ] ItemDefinition
* [ ] Itens no mundo
* [ ] Pickup
* [ ] Drop
* [ ] Inventário
* [ ] Containers

## Fase 3 — Sobrevivência

* [ ] Vida
* [ ] Dano
* [ ] Fome
* [ ] Sede
* [ ] Sono
* [ ] Consumo de itens

## Fase 4 — Fazenda

* [ ] Solo
* [ ] Plantio
* [ ] Crescimento
* [ ] Água
* [ ] Colheita
* [ ] Venda

## Fase 5 — Construção

* [ ] Preview de construção
* [ ] Posicionamento
* [ ] Validação
* [ ] Construção
* [ ] Persistência

## Fase 6 — Mundo

* [ ] Ciclo de dia/noite
* [ ] Clima
* [ ] Exploração
* [ ] Containers do mundo
* [ ] Recursos
* [ ] Animais

## Fase 7 — Horror

* [ ] Primeiro inimigo
* [ ] Visão
* [ ] Audição
* [ ] Investigação
* [ ] Perseguição
* [ ] Eventos noturnos
* [ ] Sanidade
* [ ] Eventos sobrenaturais

## Fase 8 — Narrativa

* [ ] NPCs
* [ ] Diálogos
* [ ] Documentos
* [ ] Locais especiais
* [ ] Eventos narrativos
* [ ] Progressão da história

---

# 🚧 Estado do projeto

**Em desenvolvimento.**

Ashwood County está atualmente em fase inicial de arquitetura, prototipagem e implementação dos sistemas fundamentais.

A prioridade é construir um **vertical slice jogável pequeno** antes de expandir o conteúdo.

O primeiro objetivo é chegar ao seguinte ciclo:

```text
Acordar
   ↓
Cuidar da fazenda
   ↓
Explorar
   ↓
Coletar recursos
   ↓
Voltar para casa
   ↓
Preparar-se
   ↓
Sobreviver à noite
   ↓
Novo dia
```

Se esse ciclo for divertido, os demais sistemas poderão ser adicionados progressivamente.

---

# 📜 Licença

Projeto proprietário.

Código, assets, conceitos, nomes, personagens e demais conteúdos relacionados a **Ashwood County** não podem ser redistribuídos sem autorização.
