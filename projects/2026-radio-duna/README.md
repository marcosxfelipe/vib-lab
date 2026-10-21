# Rádio Duna

**Status:** funcionando · **Início:** julho 2026

Camada de motion design que reage ao áudio, pensada para o site de uma rádio fictícia. Grãos poligonais atravessam a página como areia sobre dunas. O vento acelera com o volume da música, cada batida troca a cor da areia, e o cursor prende os grãos ao passar. A camada fica por cima do conteúdo sem bloquear cliques.

Feito num único HTML, só com Web Audio API e Canvas 2D, sem bibliotecas.

## Ideia de partida

Uma camada de formas poligonais fluindo como grãos de areia sobre dunas, reagindo à música, por cima do conteúdo da página sem impedir a interação, e respondendo ao cursor, que acumula grãos pelo caminho.

## Como usar

- **Play demo signal**: toca uma batida sintética de 125 bpm.
- **Load a track**: carrega um arquivo de áudio do seu computador.
- **Use microphone**: usa o microfone como fonte.
- **Capture a tab**: captura o áudio de outra aba (só em Chrome e Edge; marque "compartilhar áudio da aba").
- **Dune layer**: liga e desliga o efeito.
- Clicar e segurar junta os grãos em vez de girá-los em volta do cursor.

## Versões

| Arquivo | O que mudou |
|---|---|
| [`versoes/v1-inicial.html`](versoes/v1-inicial.html) | Primeira versão: analyser, campo de ruído, grãos e cursor, com paleta de areia. |
| [`versoes/v2-cores-e-autogain.html`](versoes/v2-cores-e-autogain.html) | Reação mais forte ao áudio: autogain por faixa de frequência, detecção de batida, vento proporcional ao volume e cores `#6476FE → #00FF00 → #E4FA00`. |
| [`versoes/v3-captura-de-aba.html`](versoes/v3-captura-de-aba.html) | Correção do eco do microfone e captura de áudio de outra aba. |
| [`versoes/v4-sink-silencioso.html`](versoes/v4-sink-silencioso.html) | Correção do microfone e da aba que não moviam os grãos (sink silencioso e referência ao node). |
| [`index.html`](index.html) | **Atual.** O vento muda de direção a cada 60 s, e as dunas e a borda de entrada dos grãos giram junto. |

## Aprendizados

- `smoothingTimeConstant` alto (0.82) achatava os picos; 0.62 deixa as batidas visíveis.
- Músicas normais raramente passam de 25% da escala, então cada faixa precisa de autogain com decaimento lento.
- Um analyser só recebe dados se o ramo chegar ao `destination`. A solução foi `analyser → gain(0) → destination`: o ramo continua sendo processado sem som e sem eco.
- `MediaStreamSourceNode` precisa ficar guardado numa variável, senão o Chrome descarta o node e o analyser para em silêncio.
- O microfone e a aba capturada nunca devem ir para a saída de som, ou o áudio volta para o microfone.

## Parâmetros que valem guardar

- Analyser: `smoothingTimeConstant 0.62`, `minDecibels -85`, `maxDecibels -12`
- Autogain: decaimento `0.9985`
- Batida: limiar `média × 1.9`, intervalo mínimo de 130 ms
- Vento: `WIND_PERIOD = 60`, `WIND_STEP = 0.45` (±26°), `WIND_LIMIT = 0.88` (±50°), suavização `0.0012`
- Rastro: fade entre `0.022` e `0.105`, conforme a velocidade do vento
- 560 grãos, suavização da cor `0.30`
