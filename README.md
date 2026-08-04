# Análisis RENABAP — Área Metropolitana de Tucumán (2018–2023)

## Descripción

Análisis geoespacial y sociohabitacional de los barrios populares del Área Metropolitana de Tucumán (AMT) a partir del Registro Nacional de Barrios Populares (RENABAP), comparando los relevamientos de 2018, 2022 y 2023.

Este proyecto forma parte de una investigación doctoral sobre el impacto territorial de las políticas de integración socio-urbana derivadas de la Ley N° 27.453 en barrios populares del noroeste argentino (CONICET – FAU UNT). El análisis se desarrolla en Python como reformulación de trabajos previos realizados en entorno de planilla de cálculo, con el objetivo de mejorar la trazabilidad, reproducibilidad y capacidad de visualización de los resultados.

---

## Pregunta de investigación

¿Cuáles son las condiciones sociohabitacionales de los barrios populares del AMT registrados en RENABAP, cómo se distribuyen espacialmente y qué cambios se registran entre 2018 y 2023 en términos de accesibilidad de servicios básicos?

---

## Área de estudio

Área Metropolitana de Tucumán (AMT) conformada por el municipio de San Miguel de Tucumán y localidades contiguas de múltiples municipalidades y comunas rurales. El recorte geográfico no es posible a través de selección de atributos, se realiza un filtrado de polígonos barriales mediante la selección espacial en QGIS 3.34, utilizando una capa de delimitación del AMT como área de referencia. Los subconjuntos resultantes se incluyen directamente en el repositorio como capas de trabajo validadas.

| Área de estudio | Área Metropolitana de Tucumán |

| Fuente 2018 | RENABAP – TECHO | datos.techo.org
| Fuente 2022 | RENABAP – datos oficiales de la Secretaría de Integración Sociourbana| datos.gob.ar
| Fuente 2023 | RENABAP – datos oficiales de la Secretaría de Integración Sociourbana | datos.gob.ar

| Barrios AMT 2018 | subconjunto de 144 registros nacionales | 
| Barrios AMT 2022 | subconjunto de 170 registros nacionales |
| Barrios AMT 2023 | subconjunto de 209 registros nacionales |
| Formato de entrada | Shapefile (.shp) y GeoPackage (.gpkg) |
| CRS | WGS84 / EPSG:4326 |

---

## Objetivos

### Objetivo general
Caracterizar las condiciones sociohabitacionales de los barrios populares del AMT registrados en RENABAP en base a los relevamientos de 2018, 2022 y 2023.

### Objetivos específicos

1. **Caracterización sociohabitacional:** describir la distribución de los barrios populares del AMT según tipo de asentamiento (villa / asentamiento), acceso a servicios básicos (energía eléctrica, agua corriente, efluentes cloacales, cocina, calefacción) y situación dominial, para cada corte temporal disponible.

2. **Distribución espacial:** analizar los patrones de localización de los barrios populares en el AMT, su concentración territorial y relación con la estructura urbana metropolitana.

3. **Análisis diacrónico 2018–2023:** comparar relevamientos para identificar barrios nuevos incorporados al registro, cambios en la clasificación, y variaciones en los indicadores de acceso a servicios.

4. **Visualización:** producir cartografía temática y visualizaciones estadísticas que comuniquen los resultados de forma clara para audiencias técnicas y de política pública.

---

### Pipeline de análisis

```
Capas RENABAP 2018 (.shp) 2022 (.shp) y 2023 (.gpkg)
        │
        ├── Selección espacial previa en QGIS 3.34 (delimitación AMT)
        │
        ▼
01_carga_limpieza.ipynb
   - Carga de capas con geopandas
   - Armonización de nombres de campos entre versiones
   - Verificación de geometrías y CRS
   - Clasificación de categorías de servicios
        │
        ▼
02_caracterizacion.ipynb
   - Distribución por tipo de barrio (villa / asentamiento)
   - Acceso a servicios básicos: energía eléctrica, agua corriente, efluentes cloacales, cocina, calefacción
   - Situación dominial
   - Distribución por década de creación
        │
        ▼
03_analisis_espacial.ipynb
   - Mapas de distribución general en el AMT
   - Mapas temáticos por indicador
   - Densidad y concentración territorial
        │
        ▼
04_comparacion_temporal.ipynb
   - Join por id_renabap
   - Barrios nuevos incorporados al registro
   - Cambios en clasificación y en acceso a servicios
   - Visualización de variaciones
        │
        ▼
05_visualizaciones.ipynb
   - Figuras para comunicación de resultados
   - Mapas exportables
```

### Tratamiento de variables categóricas de servicios

Las variables de acceso a servicios (energía eléctrica, agua corriente, efluentes cloacales, cocina, calefacción) son cadenas de texto descriptivas en el dataset original. Se construye una clasificación binaria auxiliar (acceso formal / acceso precario o sin acceso) para facilitar el análisis comparativo, conservando la variable original en todas las capas. El criterio de clasificación se documenta explícitamente en el notebook de limpieza.

---

## Estructura del repositorio

```
renabap-amt/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── data/
│   ├── raw/                        # Capas originales descargadas 
│   └── processed/│                 # Subconjuntos AMT — selección espacial QGIS
│
├── notebooks/
│   ├── 01_carga_limpieza.ipynb
│   ├── 02_caracterizacion.ipynb
│   ├── 03_analisis_espacial.ipynb
│   ├── 04_comparacion_temporal.ipynb
│   └── 05_visualizaciones.ipynb
│
├── outputs/
│   ├── figuras/                    # Visualizaciones exportadas
│   └── mapas/                      # Cartografía temática exportada
│
└── src/
    └── utils.py                    # Funciones reutilizables (clasificación, paletas, etc.)
```

---

## Limitaciones conocidas

- El RENABAP registra barrios populares tal como fueron relevados y validados en cada corte. Los cambios entre ediciones pueden reflejar tanto transformaciones territoriales reales como mejoras en la cobertura del relevamiento.

---

## 🔗 Proyectos relacionados

- [gee-cobertura-amt](https://github.com/Camilamop/gee-cobertura-amt) — Clasificación de cobertura del suelo en el AMT (Google Earth Engine)

---

## Autora

**Camila Agustina Mopty**  
Arquitecta | Analista de Datos Geoespaciales | Becaria Doctoral CONICET  
CETyHaP – FAU – Universidad Nacional de Tucumán  
[LinkedIn](https://www.linkedin.com/in/camila-mopty) · [GitHub](https://github.com/Camilamop) · camilamopty@gmail.com

*Investigación doctoral financiada por CONICET*
---

## Licencia

MIT License — ver [LICENSE](LICENSE) para detalles.
