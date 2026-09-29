# ForestAID — visor de susceptibilidad de incendio forestal en Cataluña

Visor interactivo del mapa diario de susceptibilidad ambiental a incendio
forestal en Cataluña, producto del proyecto **ForestAID** (Trabajo Final de
Bàtxelor en Ciencia de Datos, Universitat Carlemany).

**Ver el mapa:** https://aralrom.github.io/forestaid-visor

## Qué muestra

El mapa **no predice dónde habrá un incendio mañana**. Estima, para cada punto
del territorio, en qué medida sus condiciones ambientales actuales —índice FWI,
temperatura máxima, humedad relativa, viento, precipitación de los cinco días
previos, anomalía de humedad del suelo, NDVI, pendiente y radiación solar— se
parecen a aquellas bajo las que se han propagado los 856 incendios registrados
en Cataluña entre 1986 y 2024. Es una medida de susceptibilidad ambiental a la
propagación, no de probabilidad de ignición.

El modelo es una mezcla bayesiana de dos gaussianas ajustada por MCMC sobre esas
nueve covariables, usando exclusivamente presencias. Cada celda de la rejilla de
1 km recibe una media posterior y una desviación posterior; la segunda es la
medida de incertidumbre.

El visor ofrece tres vistas:

- **Vista municipal** — los 947 términos municipales coloreados por quintil
  según el percentil 90 de las celdas que contienen. Al pulsar sobre un
  municipio se despliegan el nivel asignado, la media y la desviación
  posteriores, y las nueve covariables de la celda que determina ese percentil.
  El círculo superpuesto codifica la incertidumbre mediante el grosor del borde.
- **Rejilla 1 km** — el ráster en el que se basa la agregación municipal.
- **Histórico** — los diez días más recientes, como imágenes de la rejilla, con
  enlace al [archivo](https://aralrom.github.io/forestaid-visor/archivo.html)
  de todos los mapas publicados.

## Fecha de los datos

La portada muestra el último día publicado; la fecha figura en su cabecera. El
archivo conserva los mapas de rejilla de todos los días anteriores desde el 10
de agosto de 2026, cada uno tal como lo produjo la cadena de datos vigente ese
día, sin recalcular a posteriori.

## Estructura

El visor es **estático**: no consulta ningún servicio al abrirse, salvo las
teselas de la capa base. Para que cada actualización diaria solo añada lo nuevo,
los recursos van en ficheros separados:

| Ruta | Contenido |
|---|---|
| `index.html` | Visor del último día |
| `archivo.html` | Índice de todos los mapas publicados |
| `datos/municipios_geom.js` | Geometría simplificada de los 947 municipios (fija) |
| `datos/valores_k2_AAAAMMDD.js` | Valores municipales de cada día |
| `mapas/susceptibilidad_k2_AAAAMMDD.png` | Mapa de la rejilla de 1 km de cada día |
| `mapas/miniaturas/` | Miniaturas de los anteriores |
| `lib/` | Leaflet 1.9.4 |

## Atribuciones y licencias de los datos

El mapa se ha elaborado a partir de las siguientes fuentes, cuyas licencias
exigen el reconocimiento expreso que se reproduce aquí y en el pie del propio
mapa:

- **Precipitación observada:** red **XEMA** del **Servei Meteorològic de
  Catalunya**. Datos actualizados a 06/09/2026.
- **Previsión meteorológica:** modelo **ICON-EU** del **Deutscher Wetterdienst
  (DWD)**. Base de datos del Deutscher Wetterdienst, con elementos propios
  añadidos.
- **ERA5-Land** (Copernicus Climate Change Service) y **CEMS Fire Historical**
  (Copernicus Emergency Management Service), bajo
  [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). *Generated using
  Copernicus Climate Change Service information [2026]*.
- **Perímetros históricos de incendios forestales:** **Departament
  d'Agricultura, Ramaderia, Pesca i Alimentació**, Generalitat de Catalunya,
  bajo [Llicència oberta d'ús d'informació —
  Catalunya](https://web.gencat.cat/ca/generalitat/dades-indicadors/dades-obertes/llicencies).
- **Capa base cartográfica:** © [OpenStreetMap](https://www.openstreetmap.org/copyright)
  contributors, bajo ODbL.
- **Librería de mapas:** [Leaflet](https://leafletjs.com) 1.9.4, BSD-2-Clause,
  incluida en `lib/`.

## Licencia

El **código** del visor se publica bajo licencia [MIT](LICENSE).

La licencia MIT cubre exclusivamente el código de este repositorio. **No se
aplica a los datos de terceros** incorporados o mostrados por el visor —XEMA,
DWD, Copernicus, Generalitat de Catalunya, OpenStreetMap—, que conservan cada
uno su propia licencia, indicada en el apartado anterior. Su reutilización debe
atenerse a esos términos, no a los de la MIT.

## Código y datos del proyecto

El código del sistema completo (descarga de datos, cálculo del FWI de
producción, ajuste del modelo bayesiano y generación diaria del mapa) y el
depósito de datos y modelos ajustados se publicarán por separado. Los enlaces se
añadirán aquí cuando estén disponibles.

## Autoría

Araceli López Romera — Universitat Carlemany.
