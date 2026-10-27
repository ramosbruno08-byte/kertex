# Kartex

Um jogo de corrida de karts arcade para 2 jogadores locais, com uma mecânica única e caótica!

## Índice

- [Sobre o Jogo](#sobre-o-jogo)
- [Conceito Geral](#conceito-geral)
- [Regras Fundamentais](#regras-fundamentais)
- [Mecânicas de Gameplay](#mecânicas-de-gameplay)
- [Elementos Visuais e UI](#elementos-visuais-e-ui)
- [MVP (Versão Jogável Mínima)](#mvp-versão-jogável-mínima)
- [Tecnologias Sugeridas](#tecnologias-sugeridas)
- [Controles](#controles)
- [Próximos Passos](#próximos-passos)

## Sobre o Jogo

**Kartex** é um jogo de corrida arcade 2D com perspectiva em 3/4 superior levemente inclinada para as costas do kart. O grande diferencial é a punição por batida traseira: ao colidir com o kart da frente, o kart que estiver atrás irá dar duas voltas completas (720°) no mesmo lugar antes de voltar exatamente à posição e rotação em que estava antes da colisão.

## Conceito Geral

| Item | Definição |
| :-- | :-- |
| **Nome** | Kartex |
| **Gênero** | Corrida Arcade de Karts 2D |
| **Plataforma** | Digital (PC) |
| **Modo de Jogo** | 2 Jogadores Locais (Mesmo Dispositivo) |
| **Perspectiva** | 3/4 superior, levemente inclinado para as costas do kart |
| **Tema** | Corrida de Karts |
| **Objetivo** | Completar o número de voltas selecionadas e ser o primeiro a cruzar a linha de chegada |
| **Duração** | Sem limite de tempo, a corrida acaba apenas ao fim da última volta |

## Regras Fundamentais

| Regra | Descrição |
| :-- | :-- |
| **Seleção de Voltas** | Antes da partida, os jogadores poderão selecionar entre 3 a 7 voltas. A corrida só irá acabar ao completar todas elas. |
| **Vitória** | O primeiro jogador a completar todas as voltas e cruzar a linha de chegada será o vencedor, sendo exibido na tela de vitória. |
| **Batida Traseira** | Caso o kart que estiver atrás colida com o traseiro do kart da frente, será aplicada a penalidade de giro. |
| **Penalidade (Giro)** | O kart traseiro irá dar 2 voltas completas (720°) no mesmo lugar. Durante esse tempo, ele ficará completamente travado, não podendo acelerar. Ao completar os 720°, ele irá voltar para a posição e rotação exata que possuía antes da colisão. |
| **Colisões Laterais** | Colisões laterais irão apenas empurrar o kart levemente e tirar ele do seu curso anterior, sem aplicar a penalidade de giro. |
| **Colisões Frontais** | Não irão aplicar a penalidade de giro. Irá ter apenas o empurrão causado pela colisão física entre os karts. |
| **Largada** | Ambos os karts iniciam na linha de largada ao mesmo tempo. O contador de voltas só irá começar a contar após a primeira passagem válida pela linha de largada/chegada. |

## Mecânicas de Gameplay

| Mecânica | Sugestão de Implementação |
| :-- | :-- |
| **Movimentação** | Acelerar, frear/recuar e virar. Movimentação arcade, ágil e fácil de controlar, ao invés de física extremamente realista. |
| **Sistema de Voltas** | Utilizar um `Area2D` na linha de largada/chegada. Toda vez que o kart passar por ela no sentido correto da pista, será contabilizado +1 volta. Será necessário adicionar uma checagem para impedir a contagem dupla caso ele passe devagar ou em sentido inverso. |
| **Detecção de Batida Traseira** | Comparar a direção e o ponto de contato entre os karts. Caso o contato aconteça na traseira do kart da frente e o kart de trás esteja vindo em direção a ela, a penalidade será ativada. |
| **Estado de Giro** | Criar dois estados para o kart (`Normal` e `Girando`). Ao entrar em `Girando`, salvar a `posição` e `rotação` exatas do kart, travar completamente seu movimento e aceleração, rotacionar o sprite em 720° a uma velocidade constante no mesmo lugar e, ao finalizar, retornar ele para a posição e rotação salvas anteriormente. |
| **Empurrão Lateral e Frontal** | Em colisões laterais ou frontais, ao invés de aplicar a penalidade, será aplicado um impulso perpendicular ou na direção oposta ao curso do kart. A força desse impulso deve ser baixa, apenas o suficiente para empurrá-lo e tirá-lo levemente do seu curso, sem arremessá-lo pela pista. |
| **Câmera** | Tela única, mostrando ambos os karts simultaneamente. Caso eles se afastem um do outro, utilizar um zoom dinâmico para sempre manter os dois visíveis na tela. |

## Elementos Visuais e UI

| Elemento | Sugestão |
| :-- | :-- |
| **Perspectiva** | 3/4 superior, levemente inclinado para as costas do kart. |
| **Karts** | Dois karts com cores distintas (Ex: Vermelho e Azul) para fácil identificação. |
| **Pista** | Circuito fechado com bordas sólidas, impedindo que os karts saiam da área jogável. Curvas são recomendadas para incentivar as batidas traseiras. |
| **Menu Pré-Partida** | Menu simples para selecionar a quantidade de voltas (entre 3 e 7) com botões de incremento e decremento, junto ao botão "Iniciar Partida". |
| **HUD** | Exibir o contador de voltas para ambos os jogadores (Ex: "Voltas: 1/5"). |
| **Tela de Vitória** | Ao completar a última volta e cruzar a linha de chegada, exibir "Jogador [Cor] Venceu!" com a opção de reiniciar a partida ou voltar para o menu de seleção de voltas. |
| **Arte** | Pixel Art simples e legível. Priorizar a silhueta dos karts e das bordas da pista, facilitando a leitura das colisões. |

## MVP (Versão Jogável Mínima)

| Ordem | Tarefa | Prioridade |
| :-- | :-- | :-- |
| **1** | Movimentação dos dois karts (Acelerar, Frear/Recuar e Virar) | Crítica |
| **2** | Colisão entre karts e colisão com as bordas da pista | Crítica |
| **3** | Detecção de batida traseira + Estado "Girando" (720°, travado, salvar e voltar para posição/rotação anterior) | Crítica |
| **4** | Sistema de voltas (Gatilho da linha de chegada, seleção entre 3-7 e contagem válida) | Crítica |
| **5** | Condição de vitória (Completar todas as voltas e cruzar a chegada) + Tela de Vitória | Crítica |
| **6** | Empurrão em colisões laterais e frontais | Importante |
| **7** | Menu de seleção de voltas e HUD de voltas | Importante |
| **8** | Câmera em tela única com zoom dinâmico e polimento da animação de giro | Opcional |

## Tecnologias Sugeridas

| Ferramenta | Motivo |
| :-- | :-- |
| **[Godot Engine](https://godotengine.org/)** | Altamente recomendado. Possui `CharacterBody2D/RigidBody2D`, `Area2D`, máquina de estados, zoom de câmera e suporte nativo a 2 jogadores locais. Perfeito para esse projeto. |
| **[LÖVE2D](https://love2d.org/)** | Ótimo caso queira programar tudo do zero com Lua. Extremamente leve e ótimo para aprender a lógica por trás do jogo. |
| **[Raylib](https://www.raylib.com/)** | Ótimo para controlar cada detalhe, porém irá exigir mais código manual para colisões, estados e UI. |

## Controles

| Jogador | Acelerar | Frear/Recuar | Virar |
| :-- | :-- | :-- | :-- |
| **Jogador 1** | W | S | A / D |
| **Jogador 2** | Seta Cima | Seta Baixo | Seta Esquerda / Seta Direita |

## Próximos Passos

1. **Protótipo em papel** - Criar um protótipo em papel da pista oval e simular a penalidade dos 720° manualmente para validar a regra.
2. **Movimentação e pista** - Criar a pista e movimentação dos karts no motor escolhido.
3. **Mecânica única** - Implementar a detecção de batida traseira e o sistema de estados (`Normal`/`Girando`), testando com diversos ângulos para garantir que a posição e rotação sejam salvas e restauradas corretamente.
4. **Sistema de corridas** - Implementar o sistema de voltas, seleção de 3 a 7 voltas e a condição de vitória.
5. **Testes e balanceamento** - Testar com partidas reais (entre duas pessoas) e balancear a força do empurrão das colisões laterais, assim ajustando o caos da corrida ao seu agrado!                                         http://localhost:8766/index.html?v=195
