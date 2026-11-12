---
name: especies-amenazadas-vedas
description: >-
  Determina y verifica la categoría de amenaza, el comercio regulado (CITES),
  las vedas nacionales o regionales y el endemismo de especies de flora
  registradas en estudios ambientales en Colombia, y cómo tratarlas en el
  inventario, el aprovechamiento y el plan de manejo. Úsela al revisar listas
  de especies, al llenar campos de categoría en tablas o al redactar sobre
  especies sensibles.
license: MIT
---

# Especies amenazadas, CITES y vedas

## Primero: confirme qué está vigente hoy
Los listados de especies amenazadas, los apéndices de CITES y las vedas cambian con el tiempo, y las normas citadas en esta skill pueden quedar desactualizadas. **Antes de cada proyecto, o de cada entrega, busque la versión vigente en las fuentes oficiales** (Ministerio de Ambiente, autoridad ambiental de la jurisdicción, CITES) y anote la norma, su fecha y la fecha de consulta. Los ejemplos de esta skill sirven para saber qué buscar, no como respuesta. Si no puede consultar la fuente oficial, dígalo y marque la categoría como pendiente de verificación.

## Fuentes, en orden
1. **Listado nacional de especies silvestres amenazadas** del Ministerio de Ambiente y Desarrollo Sostenible. Al escribir esta skill era la Resolución 0126 de 2024; confirme si hay una más reciente. Es la que obliga en Colombia.
2. **Apéndices de CITES** (comercio internacional): consulte la lista vigente en el sitio de CITES o Species+.
3. **Lista Roja de la UICN**: referencia global, no reemplaza la categoría nacional.
4. **Vedas**:
   - Nacionales: por ejemplo, la veda de flora no maderable (bromelias, orquídeas, musgos, líquenes y hepáticas) establecida desde la Resolución 0213 de 1977 del INDERENA, y vedas de especies maderables específicas. *Verificar el procedimiento vigente de manejo de especies en veda en el licenciamiento, que cambió con el Decreto 2106 de 2019.*
   - Regionales: las corporaciones autónomas pueden declarar vedas propias (por ejemplo, de cedro). Busque las de la jurisdicción del proyecto.
5. **Endemismo**: Catálogo de Plantas y Líquenes de Colombia.

## Cómo verificar sin repetir trabajo
- Revise la lista completa de especies del proyecto una sola vez contra cada fuente y registre, por especie: categoría, fuente, número de la norma, página o tabla y fecha de consulta.
- Busque por nombre científico aceptado y también por sinónimos; una especie puede aparecer con un nombre antiguo.
- Una determinación solo a género (por ejemplo, *Cedrela* sp.) no se puede descartar: trátela con el criterio de precaución y dígalo.
- Guarde el resultado en una tabla del proyecto, con la fecha de consulta. Dentro del mismo proyecto use esa tabla en lugar de releer la norma completa, pero antes de cada entrega confirme que no haya salido una norma nueva.
- Ejemplo público de la Resolución 0126 de 2024: *Cedrela odorata* (cedro) y *Elaeis oleifera* (nolí) figuran como En Peligro (EN). *Cedrela odorata* además está en el Apéndice II de CITES.

## Tratamiento en el proyecto
- **Inventario:** marque la categoría de cada especie en las tablas y en la base de datos geográfica, con el código de dominio correcto (ver `modelo-datos-anla`).
- **Aprovechamiento:** los individuos de especies amenazadas o en veda no entran en el volumen solicitado sin el trámite específico. Prefiera ajustar el área de intervención para no afectarlos e informe a qué distancia quedan.
- **Plan de manejo:** si hay individuos cerca del área de intervención, proponga medidas proporcionales (señalización, protección durante obras, rescate de plántulas o semillas, seguimiento).
- **Texto:** cite la categoría nacional primero y luego la internacional. No mezcle «veda» con «amenaza»: son figuras distintas con consecuencias distintas.

## Errores frecuentes
- Dejar una especie como «no amenazada» en la tabla aunque el listado vigente la incluye.
- Citar un listado derogado.
- Incluir individuos en veda dentro del volumen de aprovechamiento.
- Afirmar que no hay especies amenazadas sin haber revisado la regeneración ni las epífitas.

## Eficiencia
- Descargue la norma una vez y extraiga su texto a un archivo; busque las especies con un script en lugar de leer el documento completo.
- Cuando el inventario cambie, verifique solo las especies nuevas; cuando cambie la norma, verifique toda la lista contra la versión nueva.
