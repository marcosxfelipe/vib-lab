# Hand Animator

**Status:** funcionando · **Início:** abril 2026

Ferramenta no navegador para animar uma mão desenhada em vetor (estilo poligonal, amarelo sobre laranja). A versão atual segue a lógica do plugin Joysticks 'n Sliders do After Effects: um joystick 2D mistura três poses desenhadas à mão (frente, apontando e lateral), e sliders curvam cada dedo por cima da pose. Tem timeline com keyframes por trilha e exporta frames SVG ou vídeo.

Os desenhos da mão foram feitos no Figma e estão embutidos em cada arquivo, então nenhuma versão depende de arquivos externos.

## Ideia de partida

Animar minhas próprias ilustrações da mão (três poses de referência) direto no navegador, com controle manual parecido com um rig do After Effects, em vez de animar quadro a quadro.

## Como usar

- **Joystick de pose:** arraste para misturar frente, apontando e lateral. Os percentuais embaixo mostram o peso de cada pose.
- **Hand in space:** posição, escala e rotação da mão. Também dá para arrastar a mão direto no palco.
- **Finger curl:** arraste a barra de cada dedo para curvar; clique para abrir as juntas individuais (MCP, PIP, DIP) e a abertura lateral.
- **Timeline:** escolha a trilha (pose, posição ou dedos) e clique em **+ KF**. Cada trilha tem keyframes independentes. A timeline pode ser recolhida e redimensionada.
- **Exportar:** "SVG Frames" gera um .zip com um SVG por frame; "Video" grava um .webm.

## Versões

| Arquivo | O que mudou |
|---|---|
| [`versoes/v1-ossos-selecionaveis.html`](versoes/v1-ossos-selecionaveis.html) | Primeira versão: clicar num osso e girá-lo, com keyframes e exportação. |
| [`versoes/v2-hierarquia-de-ossos.html`](versoes/v2-hierarquia-de-ossos.html) | Hierarquia real de ossos (o dedo acompanha a junta de baixo) e controles simplificados por dedo. |
| [`versoes/v3-poses-de-referencia.html`](versoes/v3-poses-de-referencia.html) | Painel com as três poses de referência, abertura dos dedos e escolha de FPS para exportar. |
| [`versoes/v4-controle-por-gestos.html`](versoes/v4-controle-por-gestos.html) | Experimento com câmera: MediaPipe rastreia a mão e controla o rig por gestos. Abandonado por dar pouco controle manual. |
| [`versoes/v5-anatomia-mediapipe.html`](versoes/v5-anatomia-mediapipe.html) | De volta ao controle manual, com a nomenclatura anatômica do MediaPipe (CMC→MCP→IP, MCP→PIP→DIP) e curvatura em cascata. |
| [`versoes/v6-rotacao-3d.html`](versoes/v6-rotacao-3d.html) | Rotação 3D com perspectiva CSS (pitch, yaw, roll e profundidade) e fundo laranja fixo no palco. |
| _(v7 não guardada)_ | Timeline com keyframes por trilha, recolhível e redimensionável. |
| [`index.html`](index.html) | **Atual (v8).** Mistura das três poses por joystick, no estilo Joysticks 'n Sliders, com curvatura dos dedos por cima. |

## Aprendizados

- Rastrear a mão pela câmera parecia mágico, mas tirava o controle fino que animação precisa.
- Os nomes das camadas no Figma viram `id` no SVG exportado (marcando "Include IDs", com nomes em minúsculas e hífens).
- O fundo laranja precisa ser CSS do palco, não um path dentro do grupo da mão, senão ele gira e escala junto.
- A mistura de poses é um cross-dissolve de opacidade entre desenhos completos, como o Joysticks 'n Sliders faz por padrão.

## Próximo passo possível

Morph ponto a ponto entre as poses, em vez de cross-dissolve. Para isso, as três poses precisam ser redesenhadas no Figma com o mesmo número de paths e a mesma ordem de pontos.
