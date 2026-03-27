# ProyectoHackatonBosch
Implementación de un Dashboard para la visualización de los datos procesados por el LLM 

## Analisis Hecho 
Vamos a diseñar un dashboard que permita visualizar y analizar los logs de la aplicación. El corazón del análisis será un LLM, que procesará los logs en base a un prompt (aún por definir) y devolverá información estructurada para alimentar las vistas del dashboard.

### Flujo de Interacción del Usuario

1. El usuario selecciona los parámetros de entrada.
2. Al hacer clic en el botón de ejecución, se dispara un proceso que:
    
    - Corre la aplicación con esos parámetros.
        
    - Genera los logs correspondientes.
        
    - Envía los logs al LLM para su análisis.
        
    - Recibe el resultado procesado.
3. El dashboard se actualiza con la nueva información, mostrando las tablas, los análisis y las justificaciones.
    

---

### Estructura del Dashboard

#### 1. Sección Superior: Controles de Entrada

- **Dropdown "Número de Pedimento":**  
    Lista desplegable que contiene todos los números de pedimento disponibles.  
    _Consideración:_ Debe incluir un buscador interno, ya que podrían haber miles de opciones. No puede ser un scroll infinito.
    
- **Radio Buttons "Tipo de Operación":**  
    Dos opciones mutuamente excluyentes: _Exportación_ e _Importación_. Sirven para filtrar los logs antes del análisis.
    
- **Botón de Acción Principal:**  
    Nombre tentativo: _"Analizar con LLM"_ o _"Ejecutar Análisis"_.  
    Debe ser un botón claramente visible, con buen contraste y feedback de estado (carga, éxito, error).  
    Al presionarlo, se ejecuta el flujo completo: correr la app, procesar logs con LLM, y mostrar los resultados en el dashboard.
    

---

#### 2. Sección Principal: Visualización de Tablas

_(Se muestran una debajo de la otra, con jerarquía clara)_

- **Tabla Stage:**  
    Muestra información del "stage" del proceso.  
    _Fuente de datos:_ CSV ya existente, solo se extrae y se presenta de forma limpia y ordenada.
    
- **Tabla System:**  
    Muestra información del "sistema".  
    _Fuente de datos:_ Misma lógica que Stage, solo presentación visual.
    
- **Tabla Convenio:**  
    Esta es la tabla dinámica que se genera tras ejecutar el análisis.  
    _Característica especial:_ Resaltado de cambios a nivel de celda mediante codificación de colores:
    
    - Verde: cambios menores
        
    - Amarillo: cambios moderados
        
    - Rojo: cambios severos
        

---

#### 3. Sección de Detalles: Descripción y Justificación

- **Descripción de cambios:**  
    Explicación detallada, en lenguaje natural, de qué cambios identificó el LLM en el análisis.  
    _Fuente:_ Proviene directamente del análisis generado por el LLM.
    
- **Justificación del análisis:**  
    Espacio donde se explica el "por qué" de los cambios. Contexto adicional, criterios usados por el LLM, o advertencias relevantes.
    
- **Información relevante para el usuario:**  
    Cualquier otro dato crítico que el LLM considere necesario incluir para entender el análisis (alertas, recomendaciones, etc.).
    

---

#### 4. Sección Inferior: Proceso de Análisis del LLM

- **Pensamiento del LLM:**  
    Área que simula el razonamiento paso a paso del modelo.  
    _Formato:_ Similar a una transcripción o flujo de pensamiento donde se explica cómo llegó a las conclusiones.  
    _Objetivo:_ Dar transparencia al proceso y ayudar al usuario a confiar en los resultados.
    

---

### Consideraciones de UI/UX

- **Claridad visual:**  
    Diseño limpio, con suficiente espacio entre secciones. La información más relevante debe estar a simple vista.
    
- **Paleta de colores:**  
    Coherente, profesional, con colores de acento para elementos interactivos (botones, estados). Los colores de severidad (verde, amarillo, rojo) deben usarse exclusivamente para los cambios en la tabla Convenio.
    
- **Interactividad:**  
    Elementos como dropdowns, radios y botones deben ser claramente identificables como interactivos. El cursor debe cambiar al pasar sobre ellos.
    
- **Jerarquía visual:**  
    Guiar al usuario de arriba hacia abajo: primero controles, luego tablas, luego descripciones, finalmente el razonamiento del LLM.
    
- **Estados de carga:**  
    Incluir espacio para mensajes de "Cargando...", "Procesando análisis...", o errores. El botón de ejecución debe mostrar un estado de carga para evitar acciones duplicadas.

# Prompt Utilizado
(A este prompt le falta especificar el como se devolvera el analisis del LLM, esto es necesario para alimentar las secciones como el dropdown, la seccion de analisis interpretativo y Proceso de Razonamiento del LLM)

---
Como diseñador de UI/UX xperto y desarrollador frontend experimentado, crea un diseño detallado para un dashboard interactivo en Figma. siguiendo la estructura y funcionalidades, el objetivo es visualizar y analizar logs de una aplicacion, con especial enfasis en la interpretacion de un LLM.
**Contexto:** La aplicacion genera logs por defecto, estos logs seran procesados por un LLM utilizando un prompt especifico (aun no definido), la respuesta del LLM alimentara el dashboard.

**Estructura del Dashboard:**
1. *Seccion Superior: Controles de Entrada*
   1. Dropdown "Numero de Pedimento" : Un campo de seleccion desplegable que lista todos los numeros de pedimento disponibles (ojo, tambien debe poder buscarlos porque si son 10000 numeros, no puede ser que deslice hasta encontrar el que busca).
   2. Radio Buttons "Tipo de operacion": Dos opciones exclusivas, "exportation" e "importation", para filtrar los logs.
   3. Boton "Ejecutar Motor de Conciliacion": (Dale un nombre mas UI), Un boton claramente visible que, al hacer clic, correra la app con los datos de entrada (Pedimento y si es exportacion o importacion), se generaran los logs, se mandaran al LLM y se hara el analisis, que este lo regresara procesado y listo para presentarce.
2. *Seccion Principal Visualizacion de Tablas (por debajo de los controles)*
   1. Tabla Stage: Presenta datos relevantes del "stage" del proceso (cvs ya establecido, solo extraer el contenido y mostrarlo de forma visualmente atractiva).
   2. Tabla System: Muestra informacion referente al "sistema" (igual que Stage).
   3. Tabla Convenio: Esta tabla es la que se genera cuando se corre la aplicacion, en esta, con el analisis que hizo el LLM, se debe destacar los cambios con una codificacion de colores a nivel de celda.  cada celda que haya experimentado cambio se colorearasegun la severidad de dicho cambio (ejemplo, verde para cambios menores, amarillo para moderados, rojo para severos).
3. *Seccion de Detalles: Descripcion y Justificacion (por debajo de las tablas)*
   1. Descripcion de cambios: Un area de texto enriquecido que proporciona una explicacion detallada de los cambios identificados por el LLM de acuerdo al analisis que realizo (esto se va a obtener del analisis de los logs que hizo el LLM y se regresara junto con todo lo demas en una especie de archivo que se usara para alimentar este dashboard, es decir, tanto la app que contiene los csv y el LLM se encargaran de proporcionar la informacion, aqui solo se meten los inputs y se corre el codigo con el boton, y se muestra la info generada en el proceso). 
   2. Justificacion del analisis: Un espacio para la explicacion del "por que" de los cambios y la informacion adicional relevante que el usuario debe conocer.
   3. informacion relevante para el usuario: cualquier otro dato critico que el LLM considere fundamental para la comprension del analisis.
4. *Seccion "Proceso de Analisis del LLM"*: (en la parte inferior del dashboard)
   1. Pensamiento del LLM: Un area que simule el "razonamiento" del LLM, debe mostrar un desglose paso a paso del proceso de analisis que llevo a las conclusiones presentadas, por ejemplo, que una transcripcion o un fluje de pensamiento explique como el LLM llego a ese analisis, similar a como un humano explicaria su proceso de resolucion de un problema

Consideraciones del diseño UI/UX:
El diseño debe ser limpio, intuitivo y facil de navegar 
Utiliza una paleta de colores coherente y profesional
Asegurate de que los elementos interactivos sean claramente identificables 
La jerarquia visual debe guiar al usuario a traves de la informacion mas importante
Considerar el espacio para posibles mensajes de carga o estado

**Resultado Esperado**
Un diseño visualmente atractivo y funcional que sirva como base para la implementacion en figma, presentando la interaccion entre el usuario, la aplicacion, el LLM y la visualizacion de datos. El enfasis debe estar en la claridad de la informacion y la usabilidad para el usuario final.
