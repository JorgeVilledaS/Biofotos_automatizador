# Selector de fotos de especies forestales

Herramienta sencilla para armar guías de especies: a partir de una lista de nombres científicos, busca fotos con licencia abierta, permite elegir la mejor de cada especie y genera un documento Word listo para imprimir, con el crédito de cada foto.

Pensada originalmente para una guía de especies forestales autóctonas de Guatemala, pero sirve para cualquier lista de especies.

## Qué hace

- Carga especies una por una o desde un archivo `.txt`.
- Actualiza el nombre al aceptado actual usando [GBIF](https://www.gbif.org/) (útil con listas antiguas, donde hay sinónimos).
- Busca fotos en [iNaturalist](https://www.inaturalist.org/) (observaciones de "grado de investigación", solo licencias abiertas).
- Muestra las candidatas para que elijas la que más te guste.
- Guarda el progreso automáticamente, así se puede retomar otro día.
- Genera un `.docx` con la foto, el nombre científico y el crédito del autor.

## Requisitos

- Python 3.9 o superior

```bash
python -m pip install streamlit requests pandas python-docx
```

## Uso

1. Crea un archivo `especies.txt` con una especie por línea:

   ```
   Ceiba pentandra
   Swietenia macrophylla
   Cedrela odorata
   ```

2. Ejecuta la aplicación:

   ```bash
   python -m streamlit run app.py
   ```

3. En el navegador:
   - **Barra lateral**: escribe una especie o sube el `.txt`.
   - **Pestaña "Elegir fotos"**: haz clic en **Elegir esta** sobre la mejor foto, o en **Ninguna sirve** para buscarla a mano después.
   - **Pestaña "Documento para imprimir"**: elige el formato (1 foto grande por página, o 4 por página) y descarga el `.docx`. Desde Word o LibreOffice se imprime o se exporta a PDF.

## Archivos que genera

| Archivo | Contenido |
|---|---|
| `elegidas.csv` | Foto elegida por especie, con autor, licencia y enlace a la observación. Sirve como registro para los créditos. |

Opcionalmente, si ya tienes un `fotos.csv` con candidatas (columnas `original, aceptado, match, url, licencia, autor, obs`), la aplicación lo usa en lugar de consultar iNaturalist.

## Configuración

Desde la barra lateral se puede ajustar:

- **Candidatas por especie** (3 a 12).
- **place_id**: filtra las fotos por lugar en iNaturalist. El valor por defecto (`6728`) debe verificarse en iNaturalist; usa `0` para buscar en todo el mundo.
- **Respaldo mundial**: si una especie no tiene fotos en ese lugar, busca en cualquier parte. Esas fotos pueden no ser de ejemplares de la región.
- **Licencias permitidas**: `cc0`, `cc-by`, `cc-by-sa`.

## Sobre las licencias de las fotos

Cada foto pertenece a su autor y tiene su propia licencia. Si vas a publicar o distribuir el documento:

- Incluye siempre el crédito del autor (el documento ya lo agrega como pie de foto).
- Las licencias `cc-by-sa` exigen compartir el material derivado con la misma licencia. Si eso es un problema, deja marcadas solo `cc0` y `cc-by`.
- Revisa los términos de uso de iNaturalist y de cada licencia.

## Limitaciones

- La identificación de las fotos depende de la comunidad de iNaturalist. Conviene que una persona con conocimiento biológico revise la selección final.
- Algunas especies, sobre todo las poco observadas, pueden no tener fotos. Quedan anotadas como "Ninguna sirve" para buscarlas por otra vía.
- Este proyecto no está afiliado a iNaturalist ni a GBIF; solo usa sus APIs públicas.

## Licencia

Agrega aquí la licencia del código que prefieras (por ejemplo MIT).
