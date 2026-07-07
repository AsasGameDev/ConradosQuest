# **CONRADO'S QUEST**
[`TDD`](https://asasgamedev.github.io/ConradosQuest/Documents/TDD) | [`GDD`](https://asasgamedev.github.io/ConradosQuest/) | [`Complete GDD`](https://asasgamedev.github.io/ConradosQuest/Documents/GDD)

# **Techincal Design Document**

#  **Visão Geral do Jogo**

* **`Engine`:** Unity 6(6000.3.7f1)  
* **`Render`:** URP  
* **`Plataforma`:** PC, Web  
* **`Design Patterns`:** Observer(desacoplagem), State Machines(IAs, movimentação), Factory(Criação dos ambientes.).  
* **`Tempo de projeto`:** 3 Meses.  
* **`Sistemas`:** Movimentação, Combate, IA inimigos, Diálogo,Inventário,Criação de Mapas, Criação de texturas, gerenciamento de cenas, save serializado, UI.

# **Pacotes da Unity**

- **`Cinemachine`** - Movimento das Cameras  
- **`URP`** - Render das imagens  
- **`UI Toolkit`** - UIs de editor e Jogo

# **Sistemas**
   1. ## **Movimentação**
   Movimentação 3D, onde o personagem é sempre visto em topDown, tem guardado uma direção e itera por essa direção a cada Fixed Update. tem um sensor para delimitar o pé, e em que tipo de piso está, o personagem poderá ter diferentes tipos de movimento dependendo dos terrenos, como voar, nadar e escavar.
   
   2. ## **Combate**
   Combate com foco em movimentação, sem complexidade, o personagem poderá se mover com uma esquiva / rolamento, que irá puxar ele por alguns metros, poderá defender e atacar tanto de forma corpo-a-corpo quanto a distância, os danos serão sempre calculados de forma simples, a vida do inimigo menos a o valor da arma atual, todo ataque terá uma janela de ripostar, alguns marcados para não permitir, alguns ataques podem ser marcados como indefensáveis, todos os ataques tem de ter telemetria clara da área de dano.
   
   3. ## **IA dos Inimigos**
   Sistema que deve através de classes específicas, fazer a movimentação e o sistema de definição do funcionamento de um inimigo em jogo, usando State Machines finitas para entender a melhor forma de atacar, ele deve incluir definições mais complexas para os padrões de ataques dos subchefes, e Chefes.
   
   4. ## **Diálogo**
   Sistema editável para exibição de um diálogo textual,deve ser editável por scriptable objects, e guardados no sistema, devem ser exibidos na ferramenta de UI, seja qual for, o sistema deve contar com uma possibilidade de opções, e múltiplas ações para cada resposta dada.  
   
   5. ## **Inventário**
   O inventário deve guardar todos os itens de um personagem, serializado suas quantidades para o sistema de Save/Load, ele conta com itens capazes de dar buffs no ataque, na defesa, recuperar parte da vida, ou a vida toda, aumentar a quantidade de tempo transformado. Aqui também ficam guardados os itens chave da história, os que liberam novas transformações e abrem ou fecham possibilidades para o jogador.

   6. ## **Editor de Mapas** 
   Ferramenta interna funcional em runtime para criação de mapas, ela deve permitir que o usuário escolha um elemento (paleta de Tileset) crie uma fase, e salve essa fase em uma textura de 50x50 casas, que então poderá ser usada para outros elementos, essa ferramenta deve incluir um criador procedural, um aleatorizador, e a possibilidade de parametrização da criação no geral, lembrando da utilização de Compute Shader para processamento em jogo da geração procedural.

   7. ## **Parser Textura Mapa**
   O parser de textura deverá pegar as imagens criadas pelo editor de mapas, e transformá-las em leveis completos, fazendo a conversão de cores para objetos 3D reais, assim podendo guardar múltiplos mapas no acesso simples de um textura 50x50,usando instanciamento por GPU, aglutinação de texturas, e objetos separados em camadas de detalhes apenas, necessário salientar a modularidade, e o sistema Low poly da modelagem.

   8. ## **Gerenciamento de Cena**
   Sistema responsável por pegar os parsers das texturas, e colocá-las de forma coerente dentro do mapa, lidar com o Load / Unload dessas cenas, de forma a economizar processamento, manter fácil a navegação do personagem por todo o mapa.  
   Também é responsável pelo instanciamento dos inimigos, itens, e salas secretas, mantendo a funcionalidade do andar por completo, estruturalmente cada andar deverá ser uma nova cena.

   9. ## **Save/Load**
   Sistema responsável por parsear wrappers em arquivos Json, encriptá-los e guardá-los, bem como recuperar suas informações para devolver ao player quando necessário,usando sistemas diferentes para cada plataforma (persistent data path no PC e Local Save WebGL). 

---

### **Asas GameDev**
<a href="https://www.linkedin.com/in/thadeu-moscatelli-2559061b0/" target="_blank">
  <img src="https://img.icons8.com/color/48/linkedin.png" alt="LinkedIn" width="24" height="24">
</a>
&nbsp;
<a href="https://wa.me/5515997329328" target="_blank">
  <img src="https://api.iconify.design/logos/whatsapp-icon.svg" alt="WhatsApp" width="20" height="20">
</a>