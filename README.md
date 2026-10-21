# vib-lab

Meus projetos de vibe coding e creative coding: experimentos em HTML, Canvas, SVG e Web Audio, cada um numa pasta própria.

**Galeria:** https://marcosxfelipe.github.io/vib-lab/

## Estrutura

```
vib-lab/
├── index.html        galeria, gerada a partir do projects.json
├── projects.json     lista de projetos
├── _template/        ponto de partida para um projeto novo
├── projects/
│   └── AAAA-nome/
│       ├── index.html
│       ├── thumb.png
│       └── README.md   o que é, prompt inicial, aprendizados
└── shared/           só quando algo se repetir em 3+ projetos
```

## Adicionar um projeto novo

1. Copie `_template/` para `projects/AAAA-nome-do-projeto/`.
2. Substitua o `index.html` pelo seu projeto e preencha o `README.md`.
3. Adicione uma `thumb.png` (por volta de 1200×750).
4. Inclua uma entrada no `projects.json`:

```json
{
  "slug": "2026-nome-do-projeto",
  "title": "Nome do projeto",
  "date": "2026-10",
  "description": "Uma frase sobre o projeto.",
  "tags": ["canvas", "audio"],
  "status": "rascunho"
}
```

Status possíveis: `rascunho`, `funcionando`, `arquivado`.

## Princípios

- Cada projeto é autocontido. É melhor copiar uma função do que criar dependência cedo.
- Guarde o prompt de partida no README do projeto.
- Se um projeto crescer (build, dependências, uso diário), ele vai para um repositório próprio e a galeria só aponta para lá.
