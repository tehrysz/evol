# Evol

Site interativo sobre a história geológica da Terra, do Hadeano ao Cenozoico.

O Evol é um projeto de extensão do componente curricular de Paleontologia, produzido pelos alunos do 7º período do curso de Ciências Biológicas da PUC-Campinas e orientado pelo Prof. Dr. Rafael Farias.

## Conteúdo

- **Início**: relógio geológico e linha do tempo proporcional dos quatro éons.
- **Éons**: Hadeano, Arqueano, Proterozoico e Fanerozoico, cada um com texto, dados rápidos, índice da página e linha do tempo lateral.
- **Eras do Fanerozoico**: Paleozoico, Mesozoico e Cenozoico.
- **Galeria**: registros das aulas práticas (rochas, minerais e fósseis), com visualização ampliada.
- **Referências**: fontes consultadas, em formato ABNT.

## Tecnologias

- React 19
- Vite 7
- CSS puro, sem frameworks de interface

## Como executar

Requer Node.js 20.19 ou superior.

```bash
npm install
npm run dev       # ambiente de desenvolvimento
npm run build     # build de produção em dist/
npm run preview   # servidor local para conferir o build
```

O build usa caminhos relativos (`base: './'`) e a navegação é feita por hash (`#hadeano`, `#galeria`…), então o conteúdo de `dist/` pode ser publicado em qualquer hospedagem estática, inclusive em subpastas, como o GitHub Pages, sem configuração de servidor.

### Publicação no GitHub Pages

O workflow `.github/workflows/deploy.yml` faz o build e publica a cada push na branch `main`. Para ativar: em *Settings → Pages*, escolha **GitHub Actions** como fonte. O workflow usa `npm ci`, então o `package-lock.json` (gerado por `npm install`) precisa estar commitado.

## Estrutura

```
public/gallery/        fotografias da galeria
src/
  app/routes.js        páginas, cores, intervalos de tempo e formatação de idades
  content/             textos de cada página, da galeria e das referências
  components/          cabeçalho, rodapé, ticker, caixas laterais e lightbox
  pages/               Home, páginas de éons/eras, Galeria e Referências
  heroes/              estrutura comum das heroes e a arte de cada página
  hooks/               rota por hash, tema, parallax, revelação e progresso de leitura
  styles/              base.css · heroes.css · motion.css · embedded.css
  assets/              ilustrações das heroes
```

## Detalhes de implementação

- **Heroes**: todas usam o mesmo componente (`HeroShell`) e as mesmas dimensões, definidas pelas variáveis `--hero-h` e `--dino-w` em `heroes.css`. Cada página fornece só a sua composição em `src/heroes/art/`.
- **Tema**: claro e escuro, seguindo a preferência do sistema e persistido pelo botão do cabeçalho.
- **Acessibilidade**: link para pular ao conteúdo, navegação por teclado, anúncio da página atual para leitores de tela e respeito a `prefers-reduced-motion`.
- **Conteúdo**: para alterar textos, edite os arquivos de `src/content/`; para incluir fotos na galeria, adicione a imagem em `public/gallery/` e o registro em `src/content/gallery.js`. Um registro com `views` (lista de `label`, `file`, `alt`, `text`) vira um único cartão com botões para alternar entre as vistas, como o límulo (dorsal/ventral).
