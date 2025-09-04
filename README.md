
# Obtener más de 5000 elementos de una lista de SharePoint con Power Automate

## Problema
Por defecto, el conector de SharePoint en Power Automate tiene un límite de 5000 elementos al usar la acción **"Get items"**. Esto puede ser un obstáculo cuando se necesita procesar listas grandes.

## Soluciones

### 1. Usar Paginación
- Activa la opción de **paginación** en la acción "Get items".
- Establece el **límite de elementos por página** (por ejemplo, 5000 o menos).
- Power Automate procesará múltiples páginas automáticamente.

### 2. Filtrar por Rangos
- Divide la consulta en rangos usando filtros como `ID`, `Created`, `Modified`, etc.
- Ejemplo: Obtener elementos con `ID` entre 1 y 5000, luego entre 5001 y 10000, etc.
- Esto requiere múltiples acciones "Get items" con condiciones específicas.

### 3. Usar la API REST de SharePoint
- Utiliza la acción **"Send an HTTP request to SharePoint"**.
- Permite consultas más avanzadas y control sobre la paginación.
- Ejemplo de URL:
  
_api/web/lists/getbytitle('NombreDeLaLista')/items?$top=5000

### 4. Aplicar Select y Filter Array
- Después de obtener los datos, usa **"Select"** para transformar los elementos.
- Usa **"Filter array"** para filtrar los datos según criterios personalizados.

## Recomendaciones
- Siempre prueba con un subconjunto de datos antes de escalar.
- Considera el impacto en el rendimiento y el tiempo de ejecución.
- Usa **variables** o **arrays** para almacenar resultados intermedios.

## Recursos útiles
- Documentación oficial de Power Automate
- Comunidad de Power Users
- Blogs técnicos sobre SharePoint y Power Platform
