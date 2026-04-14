# Taller #2
# Análisis de requisitos: Sistema de Gestión para Panadería
#1. Contexto del proyecto
#2. Roles y usuarios
#3. Requisitos

## 1. Módulo 1: El Maestro Panadero

### HU-01: CRUD de Ingredientes Base (Prioridad: M)

Como administrador del sistema, quiero registrar ingredientes con sus atributos (precio/g, % de merma, % de agua, % de grasa), para corresponder a las recetas.

**Criterios SMART:** El sistema debe permitir crear, leer, actualizar y eliminar ingredientes y almacenando el “Valor por kilo” para compras.

### HU-02: Creación de Sub-recetas (Prioridad: M)

Como panadero, quiero agrupar ingredientes en mezclas intermedias (ej. masa madre, almíbar), para su integración modular en las diferentes recetas (Quiere decir esto que recetas más grandes pueden componerse de subrecetas).

**Criterios SMART:** Una sub-receta debe guardarse como una entidad independiente que pueda ser consultada e insertada en múltiples recetas finales en menos de 3 clics(?).

### HU-03: Composición de Receta Final (Prioridad: M)

Como desarrollador de productos, quiero armar una receta final combinando ingredientes y sub-recetas, para modelar productos complejos como una medialuna.

**Criterios SMART:** La interfaz debe soportar al menos un nivel de anidación (Receta → Sub-receta ) sin errores de guardado en la base de datos relacional.

### HU-04: Cálculo de Porcentaje Panadero (Prioridad: M)

Como panadero, quiero que el sistema exprese los ingredientes como un porcentaje relativo al peso total de la harina (siendo esta 100 %), para estandarizar fórmulas.

**Criterios SMART:** Al guardar una receta, la vista de detalle debe mostrar una columna calculada de % panadero con precisión de un decimal.

### HU-05: Cálculo de Hidratación Total (Prioridad: M)

Como maestro pastelero, quiero que el sistema sume el agua directa más el agua aportada por otros ingredientes (leche, huevos), para conocer la hidratación real de la masa.

**Criterios SMART:** El cálculo debe ejecutarse en el backend basándose en el atributo “% Hidratación” de cada ingrediente y mostrarse en la cabecera de la receta.

### HU-06: Versionado Inmutable (Prioridad: S)

Como desarrollador de productos, quiero crear varias versiones a partir de recetas (o subrecetas) existentes sin sobrescribir la original, para innovar sin romper los productos que ya están en producción.

**Criterios SMART:** Al editar una receta “En producción”, el sistema debe forzar la creación de un nuevo registro (V2) en la base de datos, manteniendo la V1 intacta.

### HU-07: Selección Explícita de Versiones (Prioridad: S)

Como panadero, quiero elegir conscientemente qué versión de una sub-receta usar dentro de mi receta final, para mantener control absoluto de la fórmula.

**Criterios SMART:** El selector de sub-recetas debe mostrar un menú desplegable indicando claramente, por ejemplo: Masa Base Hojaldre “V1” o “V2”.

## 2. Módulo 2: El Planificador (Escalado y Costeo)

### HU-08: Escalado por Objetivo Final (Prioridad: M)

Como panadero, quiero especificar una cantidad objetivo (ej. unidades o kg de masa), para que el sistema calcule las proporciones sin hacer reglas de tres manuales.

**Criterios SMART:** El algoritmo debe escalar todos los componentes de la receta al instante con 0 % de error matemático, se deberá implementar un tratamiento estadístico coherente.

### HU-09: Desglose de Órdenes de Producción (Prioridad: M)

Como jefe de producción, quiero que el programa genere una lista plana de cantidades absolutas, para saber exactamente cuánto pesar de cada cosa en el taller.

**Criterios SMART:** El sistema debe “desarmar” la jerarquía de sub-recetas y mostrar el peso total en gramos o kilos para la orden específica.

### HU-10: Aplicación de Merma al Costo (Prioridad: S)

Como administrador, quiero que el cálculo de costo incluya el porcentaje de pérdida o
evaporación, para tener un costo real y no ideal.

**Criterios SMART:** La fórmula de costeo final debe incrementar el costo del ingrediente
basándose en el valor de su atributo “Merma ( %)”

### HU-11: Proveedores (Prioridad: C)

Como administrador, quiero asignar un proveedor o instancia de precio manualmente a un ingrediente dado para poder comparar las opciones posibles.

**Criterios SMART:** El usuario ingresa el nombre, precio y proveedores de un ingrediente, lo anterior se convierte en un registro con los atributos variables precio y proveedor.

### HU-12: Costeo Dinámico (Prioridad: S)

Como administrador, quiero que la receta calcule su costo sumando el valor de sus ingredientes y la merma al costo según el proveedor seleccionado y la cantidad individualmente calculada de cada ingrediente, para evaluar la rentabilidad según el criterio del panadero.

**Criterios SMART:** El costo total de la receta debe actualizarse inmediatamente si el atributo “Precio relativo” o “Valor por kilo” de un ingrediente base es modificado.

## 3. Módulo 3: El Compañero de Taller (UI de Producción)

### HU-13: Modo Taller Optimizado (Prioridad: C)

Como panadero en producción, quiero poder modificar las relaciones de tamaño de los componentes de la interfaz, para tener autonomía y control de las herramientas más precisas en mi flujo de trabajo para cada momento.

**Criterios SMART:** La vista “Modo Taller” debe ocultar los menús de navegación y mostrar tipografía de al menos 18px para facilitar la lectura.

### HU-14: Checklist Interactivo de Pasos (Prioridad: S)

Como panadero en producción, quiero un botón para marcar pasos o ingredientes como completados, para evitar saltar procesos.

**Criterios SMART:** La interfaz debe mostrar un checkbox por cada ingrediente desglosado y cambiar su estado visual (ej. tachado/color atenuado) al hacer click.

### HU-15: Registro Manual de producciones (Prioridad: S)

Como panadero, quiero que se generen reportes de producción de datos relevantes para tener trazabilidad histórica relacionada a las horas de producción, calidad y cantidad producida.

**Criterios SMART:** El sistema debe guardar un registro (“Lote”) que contenga la fecha, el ID de la receta, la versión utilizada y las notas de temperatura registradas en la HU-14.

## 4. Módulo 4: Simulación y Trazabilidad Básica

### HU-16: Simulador de Modificación Rápida (Prioridad: S)

Como desarrollador de productos, quiero alterar temporalmente la cantidad de un ingrediente en una vista de prueba, para ver el recálculo inmediato de hidratación.

**Criterios SMART:** La vista de simulación debe recalcular métricas sin afectar ni guardar cambios en la base de datos oficial hasta que el usuario decida crear una nueva versión.

### HU-17: Ajustes según condiciones (Prioridad: M)

Como administrador, quiero poder hacer reajustes geográficos y de condiciones ambientales (Temperatura, humedad...) relevantes en la producción, según la receta, para precisar el máximo control teniendo en cuenta todas las influencias.

**Criterios SMART:** El sistema debe guardar un registro de cada pedido y sus condiciones cada vez que sea realizado uno, para ser consultado a futuro.

### HU-18: Registro automático de condiciones ambientales (Prioridad: S)

Como administrador, quiero poder hacer reajustes geográficos y de condiciones ambientales (Temperatura, humedad...) relevantes en la producción, según la receta, para precisar el máximo control teniendo en cuenta todas las influencias.

**Criterios SMART:** El sistema debe guardar un registro de cada pedido y sus condiciones cada vez que sea realizado uno, para ser consultado a futuro.
