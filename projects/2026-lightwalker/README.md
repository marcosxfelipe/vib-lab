# Lightwalker

**Status:** funcionando · **Início:** novembro 2026

Protótipo de PWA para aprender a desenhar experiências baseadas em mapa. Rotas por Munique a pé, de corrida ou de bike, passando por prédios históricos e pontos de arquitetura. Ao chegar perto de cada parada, o app narra a história do lugar em português. Pensado para quem gosta de fotografia, história, arquitetura e curiosidades.

Feito num único HTML, com mapa vetorial em SVG desenhado à mão, Web Speech API para a narração e Geolocation API para o GPS. Sem bibliotecas.

## Ideia de partida

> Quero aprender a desenhar uma experiência baseada em um mapa. Vamos prototipar uma PWA onde o usuário tem um mapa local, vamos começar com a cidade de Munique. No mapa é possível ver rotas e trilhas passando por locais historicos e predios interessantes. O usuário pode escolher uma das rotas no mapa ou em uma lista. Ao escolher uma trilha o usuário vê os detalhes da rota, pode passa e quais os highlights, a opção de começar a rota fica fixa na tela enquanto passa por scroll os outro elementos. Ao dar play na rota o usuário passa ver uma experiência de mapa guiada, parecido com google maps e waze, é possível ver onde estamos e a rota a seguir, a medida que o usuário avança e se aproxima fisicamente com o proximo ponto do mapa ele escuta uma descrição daquele landmark.

Depois: incluir rotas de bicicleta e corrida, e posicionar o app para quem se interessa por fotografia, história, curiosidades e arquitetura.

## Como usar

- **Mapa e lista**: as rotas aparecem no mapa como linhas de metrô (T1 a T5). Deslizar os cards ou tocar numa linha seleciona a rota.
- **Lista**: tem o filtro de modo (a pé, corrida, bike), que reordena as rotas e marca as que são ideais ou que é melhor evitar.
- **O que você quer ouvir**: História, Arquitetura, Curiosidades e Fotografia montam a narração de cada parada.
- **Detalhes da rota**: estatísticas por modo, horários de luz dourada e hora azul do dia, pontos de foto e paradas. O botão de começar fica fixo embaixo.
- **Navegação**: o mapa gira na direção do movimento, o banner mostra a próxima instrução e a narração toca perto de cada parada. Tocar numa parada repete o áudio.
- **Sem GPS** (ou fora de Munique): entra uma simulação, com pausa e velocidade de 1× a 20×.

## Rotas

| Código | Rota | Tema |
|---|---|---|
| T1 | Coração da Altstadt | História |
| T2 | Eixo Real | Arquitetura |
| T3 | Atenas no Isar | Arte e memória |
| T4 | Isar e Englischer Garten | Fotografia |
| T5 | Grande Volta do Isar | Corrida e bike |

## Aprendizados

- Mapa e lista sincronizados nos dois sentidos dão a sensação de um sistema só: deslizar o card move o mapa, tocar no mapa move o card.
- O filtro de modo funcionou melhor na lista do que no mapa. No mapa, apagar rotas escondia justamente o que a pessoa queria explorar.
- Explorar com norte para cima e navegar com o mapa girando na direção do movimento são dois modelos mentais diferentes; a transição entre eles precisa ser animada.
- A pé, a simulação pausa durante a narração, como alguém parado diante do prédio. Na corrida e na bike, a narração é curta e não para o movimento.
- O texto acompanha o áudio frase por frase, o que ajuda quem está com o som desligado.
- Pontos de foto com um leque de direção e lente sugerida comunicam mais do que um pin.

## Parâmetros que valem guardar

- Velocidade média: a pé `1,25 m/s`, corrida `2,9 m/s` (≈ 5:45/km), bike `4,4 m/s` (≈ 16 km/h)
- Distância que dispara a narração: a pé `25 m`, corrida `45 m`, bike `70 m`; pontos de foto em `1,6×` essa distância
- Zoom da navegação: `1,5` a pé e correndo, `1,1` de bike; posição do usuário a `64%` da altura da tela
- Luz dourada: sol entre o horizonte e `6°`; hora azul: entre o horizonte e `−6°`
- Paleta das rotas inspirada no sistema de Otl Aicher para Munique 1972

## Próximos passos

- Trocar o mapa desenhado à mão por tiles reais (MapLibre + OpenStreetMap).
- Salvar pontos de foto para voltar depois, útil para quem corre ou pedala.
- Áudio gravado em vez de voz sintética.
