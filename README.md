# Neon Collapse

## 1. Visão Geral do Sistema
O Neon Collapse é uma modelagem arquitetural baseada em Programação Orientada a Objetos (POO) para um jogo eletrônico interativo de RPG focado em turnos e testes de habilidade. 

A arquitetura central conecta o gerenciador principal do jogo às entidades controladas pelo usuário e aos subsistemas de controle de fluxo de gameplay, tais como o ecossistema de missões, gerenciamento de combates e testes dinâmicos de dados.

---

## 2. Arquitetura e Descrição das Classes

### 2.1. Núcleo do Jogo (Core)
* **Jogo**: Centraliza a execução do programa. Possui associações diretas com as três grandes frentes do sistema: o Jogador, o controlador de combates (Combate) e o sistema de gerenciamento de missões (Missao). Contém atributos e métodos para iniciar, avançar fases e encerrar o ciclo principal da aplicação.
* **Dado**: Componente utilitário essencial do sistema que define as faces do dado (padrão de 6 faces) e encapsula a lógica de sorteio matemático.
* **TesteHabilidade**: Modela a mecânica central do sistema. Instancia 3 dados, executa a soma dos valores e valida o sucesso contra o Nível de Habilidade (NH) do personagem.

### 2.2. Entidades Reativas e Atributos de RPG
* **Jogador**: Representa a conta ou o perfil do usuário na sessão, monitorando sua pontuação global e o controle sobre as ações do personagem.
* **Personagem (Classe Abstrata)**: O elemento central das mecânicas. Armazena os atributos principais de RPG (Força, Inteligência, Saúde e Pontos de Vida) além dos Níveis de Habilidade específicos (nh_fisico e nh_mental).

#### Especializações de Personagem (Herança)
| Classe | Foco Principal | Habilidades / Atributos Extras |
| :--- | :--- | :--- |
| **Hacker** | Invasão e Técnicas Digitais | nivel_hack, firewall, invadir_sistema(), hackear_drone() |
| **Mercenário** | Combate Corporal e Resistência | armadura, nivel_raiva, golpe_brutal(), esquivar() |
| **Mutante** | Atributos Equilibrados e Regeneração | tipo_mutacao, energia_mutante, ativar_mutacao(), regenerar() |

---

### 2.3. Sistema de Inventário e Customização
* **Inventario**: Associado diretamente ao Personagem, gerencia os pertences coletados com controle rígido de capacidade máxima.
* **Item (Classe Abstrata)**: Classe base que define propriedades de peso e descrição. Divide-se em três especializações:
    * **Kit Médico**: Itens de cura imediata que restauram pontos de vida.
    * **Implante Neural**: Modificadores temporários que ampliam os atributos mentais.
    * **Arma**: Modificadores ofensivos que ampliam o poder de dano para o próximo ataque.

---

### 2.4. Ciclo de Combate e Desafios
* **Combate**: Gerencia os turnos, ordem de ação e o fluxo de interações hostis baseadas na fórmula: Dano = Força do Atacante - Defesa do Defensor (com dano mínimo de 1 ponto por acerto).
* **Inimigo (Classe Abstrata)**: Classe base automatizada para os oponentes do jogo. Suas ramificações incluem:
    * `DronePatrulha`: Fraco, age de forma rápida e em grupo.
    * `SoldadoCorporativo`: Força média, equipado com proteção de armadura.
    * `CiborgueDeElite`: Chefe de fase com alto balanço de força e inteligência.
    * `NEXUS`: Chefe final (entidade digital), imune a ataques convencionais e vulnerável apenas a hacks e ataques mentais.

---

### 2.5. Missões e Progressão
* **Missao**: Estrutura sequencial de objetivos necessários para progredir pelas fases da megacidade de Neo-Brasília.
* **Objetivo**: Subunidades de validação atômica que determinam as condições de vitória ou conclusão de uma missão específica.

---

## 3. Mapeamento das Relações (Conceitos POO Utilizados)

O projeto utiliza os pilares clássicos da Programação Orientada a Objetos para garantir escalabilidade e organização:

* **Herança (Generalização/Especialização):** Demonstrada nitidamente na ramificação das classes derivadas de Personagem (Hacker, Atirador, Mutante, Mercenario), de Item (Consumivel, Arma, Equipamento) e de Inimigo.
* **Associação e Composição:** O Jogo coordena as partes independentes, enquanto o Personagem detém a propriedade conceitual e o ciclo de vida de seu Inventario.
* **Polimorfismo:** Métodos como atacar() ou usar_item() são herdados da classe mãe, permitindo que cada subclasse execute comportamentos totalmente distintos dependendo de sua especialização.
* **Agregação:** O Inventario armazena e gerencia instâncias da classe Item, permitindo que os objetos existam de maneira independente do contêiner.
* **Dependência:** O Personagem estabelece uma relação de dependência pontual com a classe TesteHabilidade, acionando-a apenas sob demanda para resolver ações de risco no cenário.

---
