# TDVProjeto1

## Grupo
Filipe Araújo 25981

Pedro Rodrigues 25982

## Estrutura
O projeto possui 13 classes:

* PlatformerGame.cs (classe principal)
* VirtualGamePad.cs
* TouchCollectionExtensions.cs
* Tile.cs
* RectangleExtensions.cs
* Player.cs
* Level.cs
* Gem.cs
* Enemy.cs
* Circle.cs
* AnimationPlayer.cs
* Animation.cs
* Accelerometer.cs

## Funcionamento

O próximo nível é carregado. Os métodos importantes são PlatformerGame.LoadContent e PlatformerGame.LoadNextLevel.

O jogo é actualizado utilizando PlatformerGame.Update e Level.Update. Se o jogador estiver morto ou se o tempo acabar, os inputs são ignorados e o jogo fica num estado de pausa. Se o jogador tiver chegado ao final (exit), o tempo restante é convertido em pontos. Se ainda houver tempo e o jogador não tiver chegado ao local final, o tempo restante é diminuído e todos os objectos do nível são actualizados (personagem do jogador, inimigos, pedras preciosas, etc.) utilizando os seus métodos Update. Neste momento, também é verificado se o jogador chegou à final e se caiu da borda do ecrã.

O ecrã de jogo é desenhado utilizando o método PlatformerGame.Draw. Este método, por sua vez, chama Level.Draw e PlatformerGame.DrawHud.
O método Level.Draw é responsável por desenhar os tiles, a personagem do jogador, as pedras preciosas e os inimigos, através de chamadas ao método Draw de cada um dos objectos de jogo mencionados anteriormente.

## Aprofundamento de cada classe:
### PlatformerGame.cs

Este é a classe principal do jogo

O método LoadContent será chamado uma vez por jogo e é o local que carrega todo o conteúdo.

O método Update permite que o jogo execute a lógica como atualizar o mundo, verificação de colisões, recolha de dados e reprodução de áudio

O método HandleInput trata do controlo do teclado, como por exemplo, saber se alguma tecla esta a ser clicada ou não.

O método Draw desenha o jogo desde do fundo até ao primeiro plano.

O método DrawHud desenha o HUD, onde está incluido, por exemplo, o tempo de jogo e a pontuação.

### Player.cs

Classe responsável pelo personagem do jogo. Nesta classe trata-se do movimento do jogador (horizontal, vertical, se está no ar, etc.), da hitbox, das animações do personagem, das físicas (ex: cair, saltar)

O método HandleCollisions detecta e resolve todas as colisões entre o jogador e a vizinhança. Quando é detectada uma colisão, o jogador é afastado ao longo de um eixo para evitar a sobreposição. Existe alguma lógica especial para o eixo Y para lidar com plataformas que se comportam de forma diferente dependendo da direção do movimento.

O método DoJump calcula a velocidade Y para saltar e anima em conformidade.
Durante a acentuação de um salto, a velocidade Y é completamente anulada por uma curva de potência. Durante a descida, a gravidade toma conta. A velocidade do salto é controlada pelo campo jumpTime que mede o tempo na acentuação do salto actual.

O método GetInput obtém os comandos de movimento horizontal e de salto do jogador a partir dos inputs.

O método LoadContent carrega o sprite sheet e os sons do personagem.

### Enemy.cs

Classe responsável pelo inimigo presente no nível 2

O método LoadContent carrega o sprite sheet e os sons do iniimgo.

O método Draw desenha o inimigo.

O método Update é responsáel pelo movimento do inimigo, que caminha para trás e para a frente ao longo de uma plataforma, esperando em cada extremidade.
