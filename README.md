# GeoRoute Animator 3D Madeira v1.2

PWA Android com MapLibre GL JS, relevo 3D derivado do ficheiro `Madeira_5m_OTIMIZADO(1).tif` EPSG:5016, rotas OSRM, geocodificação Nominatim e edifícios OpenStreetMap (Overpass).

## Publicação

1. Extrair o ZIP.
2. Carregar o **conteúdo** da pasta `georoute-animator` (incluindo a pasta `terrain`) na raiz de um repositório GitHub Pages.
3. Ativar Settings > Pages > Deploy from branch > main > /(root).
4. Abrir o URL HTTPS no Chrome Android e escolher Adicionar ao ecrã principal.

## Ortofotografia real 2023

**Não incluída**: o ficheiro fornecido é um raster de elevação, não um mosaico RGB. Em Controlos 3D, inserir URL HTTPS de mosaicos XYZ `{z}/{x}/{y}` de um serviço autorizado e com CORS. Se o serviço original for WMS/WMTS noutro esquema, é necessário adaptá-lo ou preparar XYZ previamente. Atribuir créditos ao fornecedor. OSM continua disponível como base.

## Limitações

- Tiles de terreno pré-gerados apenas em zoom 9 a 11, com amostragem do MDT original. A precisão do raster de 5 m não se mantém neste zoom. MapLibre amplia o último nível para zooms superiores.
- Edifícios OSM são solicitados por área limitada no ecrã; alturas podem ser estimadas a partir dos pisos ou assumir 6 m. A disponibilidade e os limites do Overpass variam.
- Rotas OSRM/Nominatim requerem internet e têm limites de utilização; não usar estes endpoints públicos em produção de elevado tráfego.
- Exportação vídeo é um renderizador estilizado 2D e **não** inclui o mapa 3D ou a ortofotografia. Para exportação 3D é necessário um renderizador dedicado e garantir CORS/licenciamento dos mosaicos.
- A app não foi validada num telemóvel Android físico.


## v1.3 — Exportação
- **Gravar mapa 3D**: captura diretamente o canvas WebGL do MapLibre e grava com MediaRecorder. A extensão MP4 só é utilizada se o navegador suportar o codec; nos restantes casos, WebM.
- **Exportar mapa PNG**: captura a vista 3D atual como imagem.
- **GeoJSON**: exporta a geometria da rota para QGIS e outros SIG.
- A gravação inclui apenas o canvas do mapa, não os controlos HTML. Requer fontes cartográficas com CORS adequado; a captura não é garantida em todos os Android.
- Para MP4 garantido em todos os dispositivos seria necessária conversão adicional (por exemplo FFmpeg num servidor).

## v1.4 — Estrutura GitHub Pages
Os mosaicos do relevo têm de estar em `terrain/{z}/{x}/{y}.png`.
Não coloque os PNG diretamente na raiz: por exemplo `terrain/9/232/206.png`.
A publicação requer o diretório completo `terrain/` e os ficheiros `index.html`, `app.js`, `style.css`, `sw.js`, `manifest.webmanifest`, `icon.svg` na raiz.
O formato MP4 só é produzido quando suportado pelo navegador; WebM é o formato alternativo.
