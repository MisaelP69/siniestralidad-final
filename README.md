# Intersecciones y tramos viales críticos — app Streamlit

App multipágina de apoyo a la tesis (SPF con datos abiertos):

- **app.py** (página principal, "Análisis"): sube un CSV de accidentes con las
  9 columnas del registro de Acacías (o usa los datos generados en la otra
  página), elige la ciudad, y la app descarga la red vial de OSM, geocodifica
  con el parser de nomenclatura colombiana, construye características,
  entrena con validación cruzada espacial y muestra métricas, tablas de
  inspección/prevención y tres mapas interactivos.
- **pages/1_Generador_de_datos.py** ("Generador"): genera accidentes
  simulados parametrizables para cualquier ciudad (barrios y vías reales
  consultados a OSM; hotspots; mezcla de gravedad; % rural; semilla) con el
  mismo esquema del CSV original, descargables o enviados directamente a la
  página de análisis.

## Ejecutar en local

```bash
pip install -r requirements.txt
streamlit run app.py
```

## Desplegar en Streamlit Community Cloud (gratis, con link compartible)

1. Sube esta carpeta a un repositorio público de GitHub (app.py en la raíz,
   la carpeta pages/ y requirements.txt).
2. Entra a https://share.streamlit.io e inicia sesión con GitHub.
3. **Create app** → "Deploy a public app from GitHub" → elige el repositorio,
   rama `main` y **Main file path: `app.py`** → **Deploy**.
4. En ~3 minutos queda pública en `https://<nombre>.streamlit.app` — ese es
   el link para compartir.

Notas de rendimiento: la primera ejecución de cada ciudad descarga la red de
OSM (1–5 min; queda en caché); en ciudades grandes usa la opción "Centro
urbano" con radio. Si la app se suspende por inactividad, el primer visitante
la despierta en ~1 min.
