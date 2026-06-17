# -Neon-Colapse-METABLOOM-
1. Visão Geral do Sistema
O sistema consiste na modelagem orientada a objetos de um jogo eletrônico interativo. A arquitetura central conecta o gerenciador principal do jogo às entidades controladas pelo usuário (Jogador) e aos sistemas de controle de fluxo de gameplay, como o ecossistema de missões e gerenciamento de combates.

2. Descrição Detalhada das Classes e Arquitetura
2.1. Núcleo do Jogo (Core)
Jogo: É a classe que centraliza a execução do programa. Ela possui associações diretas com as três grandes frentes do sistema: o Jogador, o controlador de combates (Combate) e o sistema de gerenciamento de missões (Missao). Contém atributos e métodos para iniciar, pausar e encerrar o ciclo principal da aplicação.

2.2. Entidades Reativas e Atributos de Combate
Jogador: Representa a conta ou o perfil do usuário no jogo. Ele possui uma relação de composição/associação com a entidade ativa no mapa: o Personagem.

Personagem: É o elemento central das mecânicas. Ele armazena os atributos principais de RPG (como vida, energia, inteligencia, agilidade, defesa e pontos_de_vida). Possui métodos essenciais como atacar(), defender(), usar_item(), e receber_dano().

Especializações de Personagem (Herança):

Hacker: Especialista com foco em inteligência e mecânicas específicas de invasão/técnicas digitais.

Atirador: Personagem voltado para dano à distância e agilidade.

Mutante: Classe com atributos modificados de resistência física ou habilidades biológicas.

Mercenario: Classe balanceada focada em combate direto e ganho de recursos.

2.3. Sistema de Inventário e Customização
Inventario: Associado diretamente ao Personagem, armazena os pertences coletados ao longo do jogo. Ele contém uma agregação de itens.

Item: Classe abstrata ou base para os objetos do jogo. Divide-se em três especializações por herança:

Consumivel: Itens que concedem bônus temporários ou cura e desaparecem após o uso (ex: poções, kits médicos).

Equipamento: Itens de modificação estética ou proteção que alteram os status do personagem de forma passiva.

Arma: Itens de ataque que modificam diretamente o poder ofensivo e os métodos de dano do portador.

2.4. Ciclo de Combate e Desafios
Combate: Gerencia os turnos, ordem de ataque e fluxo de interações hostis entre o Personagem e os inimigos presentes na sessão.

Inimigo: Classe base para os oponentes do jogo. Assim como o personagem principal, possui atributos de combate, mas com comportamento automatizado. Divide-se em subclasses como:

Chefe (Bosses com mais vida e padrões complexos).

InimigoPadrao, DroneDeDefesa, SoldadoCorporativo.

2.5. Missões e Progressão
Missao: Estrutura que dita os objetivos que o jogador deve cumprir para progredir na história e ganhar recompensas. Cada missão é composta por um ou mais Objetivos, que validam se as condições de vitória do cenário foram atingidas.

3. Mapeamento das Relações (Conceitos POO Utilizados)
Herança (Generalização/Especialização): Demonstrada nitidamente na ramificação das classes derivadas de Personagem (Hacker, Atirador, etc.), de Item (Consumivel, Arma, Equipamento) e de Inimigo.

Associação e Composição: O Jogo coordena as partes independentes, enquanto o Personagem detém a propriedade conceitual de seu Inventario.

Polimorfismo: Métodos como atacar() ou usar_habilidade() são herdados da classe mãe, permitindo que cada subclasse execute comportamentos totalmente distintos dependendo de sua especialização.
