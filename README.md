# Curso 26/27. Práctica 1. Interfaces gráficas para aplicaciones de escritorio

![Image of the assigment](social-image.png)

_Repositorio dedicado al desarrollo de la primera práctica de equipo
de IPM_

Este repositorio contiene todo el material necesario para comenzar el
desarrollo de la práctica.


En este trabajo práctico, el estudiante diseñará e implementará una
aplicación de escritorio con su correspondiente _IGU_, _interfaz
gráfica de usuaria_.

Este documento:

  - describe el trabajo a realizar
  
  - establece los roles a desempeñar por parte de los miembros del equipo
  
  - describe los resultados (entragables) de la práctica
  
  - proporciona las rúbricas necesarias para la autoevaluación
  
  - proporciona indicaciones y sugerencias para validar el trabajo realizado


> :warning: ¡Importantísimo! Si no te familiarizas con el contenido
> de este repositorio (el README, el enunciado, los roles, etc.), no
> podremos calificarte, y la puntuación será de **cero**. Tómate un
> tiempo para leerlo todo con calma.


> ⚠️ Evaluación ⚠️ Este documento incluye atributos de calidad, rúbricas
> y una lista de los errores más comunes. Usalos para autoevaluar tu
> trabajo y corregir las deficiencias antes de la revisión del
> profesor. La valoración de tu trabajo será pobre si presenta alguna
> de las deficiencias que ya están descritas en este documento.


---


# Equipo de trabajo

El equipo de trabajo está formado por tres personas. Cada persona
desempeñara un role individual durante el desarrollo de la práctica.

La descripción de cada role y sus requisitos de asignación se
encuentran en el fichero [roles.md](roles.md).

Una vez asignados los roles de cada miembro del equipo, debéis cubrir
el fichero [AUTHORS](AUTHORS) siguiendo el formato de ejemplo del
propio fichero.


---


# Presentación de la aplicación (IPMDownloader)

En esta práctica el aspecto clave de la aplicación es la interfaz
gráfica de usuaria en un entorno de escritorio.

_IPMDownloader_ es una aplicación de escritorio que permite gestionar
la simulación o descarga real desde un servidor de múltiples archivos
de manera simultánea, garantizando una experiencia de usuario fluida y
sin bloqueos.


# Objetivos de aprendizaje

En el desarrollo de software profesional, la construcción de
interfaces gráficas de usuario (GUI) requiere una separación estricta
entre la lógica de negocio y la presentación. Asimismo, las
aplicaciones modernas deben ser globales (soportar múltiples idiomas y
formatos) y altamente reactivas.

Al finalizar este trabajo práctico, el estudiante habrá demostrado ser
capaz de:

  - realizar una __programación dirigida por eventos__.
  
  - realizar un buen diseño orientado a objetos de la interfaz.
  
  - __separar la vista y el modelo__ desde el diseño de la
    arquitectura de la aplicación hasta la implementación.
  
  - entender la necesidad (el por qué) de la __programación concurrente__
    para evitar el bloqueo de la interfaz.
	
  - evitar el bloqueo de la interfaz usando una programación
    concurrente.

  - __internacionalizar__ la interfaz.


## Mini-proyecto

La práctica abarca el desarrollo completo de una aplicación. Esto incluye:

  - QA.
  
    Pruebas, documentación, planificación, seguimiento, control de versiones.
	
  - Análisis de requisitos.
  
  - Análisis y diseño del software.
  
  - Implementación.
  
  
---

# Descripción: Gestor de descargas multihilo internacionalizado (IPMDownloader)

Este es un trabajo clásico que demuestra de forma muy visual la
utilidad de los hilos de ejecución.

- **¿En qué consiste?** Una interfaz donde el usuario introduce, desde
  un fichero de texto, varias URLs de archivos grandes (pueden ser
  imágenes pesadas o archivos simulados) para su descarga. La aplicación
  muestra una lista con el progreso de cada descarga mediante barras de
  progreso individuales.

- **Cómo cubre los objetivos:**

  * **Programación dirigida por eventos:** La librería gráfica elegida
    impone la programación dirigida por eventos para manejar las
    acciones de la usuaria.
  
  * **Diseño Orientado a Objetos:** La librería gráfica elegida
    promueve el diseño orientado a objetos.

  * **Arquitectura de la aplicación:** La arquitectura diseñada debe
    separar la interfaz del manejo de las descargas y su estado.
  
  * **Concurrencia:** Cada descarga debe ejecutarse en un hilo
    distinto al que maneja la interfaz. Los estudiantes aprenden el
    peligro de modificar componentes gráficos directamente desde un
    hilo secundario y la necesidad de usar mecanismos de
    comunicación/coordinación con la interfaz.
  
  * **i18n:** Traducción de textos ("Descargando", "Pausado",
    "Error"), unidades de medida (KB/s, MB/s) y fechas.


## División en tareas

De cada a la evaluación continua, la práctica se divide en tres tareas.


  - __Tarea 1__
  
    * Hito 1: Arquitectura Base y Diseño de la Interfaz.
	
    * Hito 2: Desarrollo de la Arquitectura y Lógica dirigida por eventos.
	
	
	**Nota:** En este hito, durante las descargas de archivos grandes
    es posible que la interfaz **se congele**.  Esto no se considera
    un fallo hasta la siguiente etapa. Puedes aprovechar esta
    circustancia para experimentar el problema real en tu propio
    código antes de resolverlo en el siguiente hito.

  - __Tarea 2__
  
    * Hito 3: Concurrencia y Sincronización con el Main Loop.
	
  - __Tarea 3__
  
    * Hito 4: Internacionalización (i18n) y Localización (l10n).
  
  
---


## Requisitos tecnológicos

1. El lenguaje de programación es _python_.
  
   Se debe usar una [versión de
   python](https://devguide.python.org/versions/) que no vaya a
   alcanzar el _fin de vida_ (_end-of-life_) antes de que finalize el
   curso.
   
2. Las librerías a emplear son: la librería estándar de python, GTK4
   y, opcionalmente, adwaita.
   
3. El control de versiones ser realiza con _git_.

4. Se guardará una copia completa del repositorio en _github_. Los
   docentes tendrán acceso a dicho repositorio.

5. No se permite usar herramientas como _blueprint_, _glade_ o _gazpacho_.
   En general, cualquier herramienta que implique el uso de la clase
   `GTk.Builder` en tiempo de ejecución.


## Requisitos Funcionales (RF)

La interfaz de la aplicación deberá contar con los siguientes componentes:

- __RF-1:__ Adición.

  Un formulario con un campo de texto para introducir la URL/Nombre
  del archivo y un botón para "Descargar".

- __RF-2:__ Lista de Descargas.

  Una sección princial que muestre de forma dinámica cada descarga
  añadida. Por cada una debe mostrar:
  
  * Nombre del archivo / URL.
  
  * Barra de progreso (_Progress Bar_) en porcentaje (0% a 100%).
  
  * Etiqueta de texto con el estado actual. Ej: Esperando,
    Descargando, Completado, Cancelado, Error.
	
	Cuando este disponible y corresponda, junto con cada etiqueta se
    mostrará: tamaño del archivo, velocidad de descarga, fecha y hora
    de finalización de la descarga.
  
  * Botón individual de __Cancelar / Detener / Pausar__.
  
  
- __RF-4:__ Estadísticas Generales.

   Muestra el número total de descargas activas y completadas.

La interfaz está internacionalizada:

- __RF-4:__ El idioma de la interfaz se configura mediante las
  _variables de entorno_ del sistema.


---


## Requisitos Técnicos y Restricciones (Atributos de Calidad)

- __A. Separación de Responsabilidades (Modelo-Vista)__

  * __Restricción:__ Queda estrictamente prohibido programar lógica de
    negocio, bucles de simulación o accesos a datos dentro de los
    escuchadores de eventos (*Listeners/Handlers*) de los botones.
  
  * __Evidencia:__ Las clases del **Modelo** no deben importar,
    heredar ni hacer referencia a ninguna librería gráfica, ni los
    módulos de la aplicación que implementan la interfaz. El modelo
    debe ser 100% aislable.


- __B. Concurrencia y Reactividad (Multithreading)__

  * __Restricción:__ El hilo principal de la interfaz gráfica
    (**EDT**, __Event Dispatch Thread__, o __MainThread__) debe
    dedicarse *únicamente* a la librería gráfica y a capturar eventos
    del usuario.
  
  * __Comportamiento esperado:__ Cada descarga añadida debe ejecutarse
    en un hilo secundario independiente (ya sea un hilo por descarga,
    un pool de hilos, ...). Durante una descarga pesada, el usuario
    debe poder arrastrar la ventana, redimensionarla y pulsar los
    botones de cancelación sin experimentar *lag* o congelación de la
    pantalla ("No responde").
  
  * __Seguridad de Hilos (Thread-Safety):__ Las actualizaciones de las
    barras de progreso y textos de la interfaz deben notificarse al
    MainThread utilizando los mecanismos seguros de la librería gráfica.
  
  * __Cierre Seguro:__ Al cerrar la ventana principal de la
    aplicación, todos los hilos de fondo activos deben finalizar de
    manera inmediata y limpia (evitar hilos "zombi" en el sistema), y
    la aplicación terminar ordenadamente.
	

- __C. Internacionalización (i18n)__

  * __Restricción:__ No debe existir ninguna cadena de texto (String)
    literal visible para el usuario final que no esté
    internacionalizada en el código fuente de la vista.
  
  * __Manejo de Recursos:__ Todos los textos deben estar _localizados_
    en archivos externos.
  
  * __Localización de Datos:__ El formateo de números (separadores de
    miles/decimales) y las fechas deben respetar el estándar cultural
    del idioma seleccionado.


---


## Documentación técnica

1. _Diseño de la interfaz de usuaria_. El estudiante tiene que seguir
   las mismas pautas que siguió en la práctica individual.

2. _Diseño arquitectónico de la aplicación_. El estudiante tiene
   libertad para seleccionar el patrón de su preferencia, pero es
   obligatoria la separación entre modelo y vista (interfaz). Algunos
   ejemplos clásicos serían: _Model-View-Controller_ (MVC) y
   _Model-View_Presenter_ (MVP).
   
3. _Diseño software_. El estudiante tiene que usar obligatoriamente el
   lenguaje UML para documentar el diseño. No se permite usar ningún
   otro lenguaje de diagramado.
   
4. _Concurrencia_. Breve explicación de la estrategia de
   sincronización de threads.

5. _UX_: Breve explicación de la estrategia del _user journey_ cuando
   se interrumpe la conexión con el servidor.
   
   
## Entregables

Todos los recursos entregables deben encontrarse en el repositorio
designado. El repositorio debe estar convenientemente estructurado y
contener:

  - Código fuente completo. Proyecto limpio y compilable/ejecutable
    sin errores.

  - Ficheros de _l10n_. Al menos dos idiomas.

  - Documentación técnica. Documentación descrita en el apartado
    anterior.


## Evaluación

* **Diseño Orientado a Objetos y Arquitectura (30%):** Modularidad de
  la vista, encapsulamiento y correcto desacoplamiento del Modelo.

* **Gestión Concurrente y Sincronización (30%):** Fluidez de la
  interfaz ante estrés de carga y ausencia de excepciones por hilos
  cruzados.

* **Internacionalización y Localización (20%):** Cambio de idioma
  correcto, ausencia de textos nativos ocultos, formato de datos
  correcto.

* **Funcionalidad y Usabilidad (20%):** Cumplimiento de los flujos de
  la aplicación y manejo de errores (ej. control de URLs inválidas).


---

# 🎯 Rúbricas Genéricas

1. __Patrón Arquitectónico (Separación de responsabilidades):__

  Es obligatorio implementar un patrón arquitectónico que separe el
  modelo de la vista.
  
  _Tip:_ se pueden realizar pruebas unitarias del modelo sin ejecutar la interfaz.
  
  Prohibido tener lógica de negocio (modelo) dentro de los escuchas de
  eventos (*listeners* o *handlers*).


2. __Diseño Orientado a Objetos:__

  El diseño de los componentes de la interfaz respetan los principios _SOLID_.
  
  _Consejo:_ Un error habitual es usar la especialización (y la herencia) en
  lugar de la composición, rompiendo el principio _Liskov
  substitution_.
  

3. __Hilos (Threads):__ 

  La interfaz debe responder y permanecer fluida en todo momento
  mientras ocurren las tareas pesadas (descargas).
  
  _Tip_: en todo momento es posible mover o cerrar la ventana y hacer
  clic en otros botones.
  
  Es obligatorio usar las herramientas nativas de la librería gráfica
  para sincronizar el hilo de fondo con el _hilo de despacho de
  eventos_ o _hilo principal_.


4. __Ficheros de Recursos (i18n):__

  Todo el texto traducido debe cargarse desde archivos externos.
  
  El cambio de idioma debe hacerse mediante las variables de entorno
  del sistema.



## Errores típicos

A continuación se detallan algunos errores típicos que se comenten de
forma recurrente divididos por los objetivos de la práctica:


1. __Errores en Separación de Capas (Modelo-Vista)__

El síndrome del _"Botón Inteligente"_ es el error rey en este nivel.

- __Lógica de negocio dentro del Listener:__ El estudiante programa la
  descarga de datos, el cálculo matemático o el acceso a la base de
  datos directamente dentro del método manejador de la activación del
  botón.

- __Importaciones cruzadas:__ La/s clase/s Modelo termina importando
  librerías de la interfaz. Esto rompe por completo la separación
  entre modelo y vista.

- __La Vista almacena el estado:__ Guarda los datos de la aplicación
  dentro de un componente visual. Por ejemplo, leer el saldo de una
  cuenta directamente del estado de la vista haciendo
  `float(label_saldo.get_text())` en lugar de consultar al Modelo.
  

2. __Errores en Concurrencia (Bloqueo y Sincronización)__

La gestión de hilos en entornos de interfaz gráfica combianda con la
programación dirigida por eventos plantea un esquema distinto al de la
programación sencuencial.

- __Congelar la interfaz (The Frozen UI):__ Ejecutan la tarea pesada
  (el bucle de la descarga o el filtro de imagen) en el mismo hilo de
  la interfaz (EDT \- *Event Dispatch Thread*). La ventana no responde
  y el entorno de escritorio termina por mostar el mensaje de "La
  aplicación no responde".
  
  _Warning:_ Es habitual que este problema se deba a una programación
  incorrecta de los threads.

- __Modificar la Vista desde un hilo secundario (Crash por
  Thread-Safety):__ Intentar acciones como, por ejemplo,
  `label.set_text(...)` directamente desde un hilo que no es el hilo
  de manejo de eventos, _EDT_, es un fallo habitual cuando comenzamos
  a trabajar con librerías gráficas.

  En frameworks estrictos (como JavaFX, .NET o Android), esto lanza
  una excepción inmediata de violación de acceso de hilos. En otros
  (como Gtk+), provoca comportamientos erráticos, parpadeos,
  corrupción visual aleatoria o el "crash" de la aplicación.
  

- __Hilos huérfanos (Zombies):__ Si la usuaria cierra la ventana
   principal de la aplicación mientras hay tareas en segundo plano,
   los hilos de fondo siguen corriendo infinitamente en la memoria de
   la computadora y la aplicación no termina. 
   
   _Tip:_ Para evitar el error, configurar los threads correctamente
   y/o implementar un método de parada segura.
   

3. __Errores en Diseño Orientado a Objetos (POO)__

Suelen originarse por una mala comprensión del paradigma de
orientación a objetos, a veces debido a la influencia del paradigma
procedural.

- __La clase "Monolito":__ Una sola clase gigantesca llamada
  `VentanaPrincipal`, o un nombre similar, que contiene más de 1.500
  líneas de código, donde se declaran absolutamente todos los botones,
  paneles, layouts, lógica de negocio y variables globales. No se
  modulariza la interfaz en componentes.
  
  _Nota:_ Este es el antipatrón que se conoce como _Blob_ o _Clase
  Dios_.


- __Abuso de variables estáticas:__ Para comunicar la ventana A con la
  ventana B, recurren a hacer las variables globales o estáticas. Esto
  destruye el encapsulamiento y los principios de diseño.


- __Herencia innecesaria:__ Heredar de componentes de la librería
  gráfica para implementar componentes específicos de la interfaz en
  lugar de usar composición o, simplemente, configurar sus
  propiedades.


4. __Errores en Internacionalización (i18n)__

La internacionalización no suele recibir la atención que merece,
provocando que se realizen desarrollos de calidad sub-estándar.


- __Textos "Hardcodeados" mixtos:__ Se traducen los botones
  principales, pero los mensajes de error, los títulos de las ventanas
  de diálogo o los formatos de los números y fechas se quedan en el
  idioma nativo del código.

- __Formateo manual de datos:__ Concatenar strings para las fechas
  (ej. dia \+ "/" \+ mes \+ "/" \+ año). Olvidan que en otros países
  el orden cambia (MM/DD/AAAA) o que los separadores de miles y
  decimales varían (puntos por comas).
  
  _Tip:_ Las librerías de nuestro lenguaje de programación tienen
  funciones y métodos para realizar el formateo correctamente.

- __Corte de texto en la interfaz (Layouts rígidos):__ El diseño y/o
  la implementación de la interfaz son rígidos y no se adaptan a las
  distintas longuitudes del texto. La interfaz debe adaptarse ya que
  los textos que contiene varían en longuitud según el idioma de los
  mismos. Por ejemplo, tomando únicamente idiomas occidentales:
  español "Salir", inglés ("Exit") o alemán ("Ausloggen").


# 📊 Rúbrica detallada de evaluación


## ⚠️ Pauta de conversión para la nota final ⚠️

Para obtener el aprobado de la práctica, es __requisito
indispensable__ que el estudiante obtenga al menos el 50% de los
puntos en el __Hito 3 (Concurrencia)__. Una aplicación que congela la
interfaz se considera un software no funcional en el ámbito de la
ingeniería informática.



## 📌 Hito 1: Arquitectura Base y Diseño de la Interfaz (Peso: 15% / Máx: 1.5 pts)

  - **Excelente (1.3 \- 1.5 pts):** La interfaz está completamente
    descrita. El modelo está encapsulado en clases de Python puras sin
    ninguna importación de gi.repository.Gtk o los módulos de la
    vista. Existen pruebas unitarias o de consola que demuestran que
    el modelo funciona de forma aislada.

  - **Aceptable (0.8 \- 1.2 pts):** El modelo y la vista están
    separados, pero el modelo contiene variables globales innecesarias
    que dificultan su aislamiento.

  - **Insuficiente (0.0 \- 0.7 pts):** El modelo realiza importaciones
    de componentes de GTK o de los módulos de la vista, o la interfaz
    no se despliega en absoluto.

  - __⚠️ Penalización Directa (-0.5 pts):__ Uso de herencia innecesaria
    (ej. crear subclases de Gtk.Button solo para cambiarles el texto).
	

## 📌 Hito 2: Lógica Dirigida por Eventos (Peso: 20% / Máx: 2.0 pts)

  - **Excelente (1.7 \- 2.0 pts):** Los controladores capturan los
    eventos, y usan los objetos del modelo. No hay lógica de negocio
    dentro de las funciones *callback* de las señales de GTK.
  
  - **Aceptable (1.0 \- 1.6 pts):** La comunicación funciona, pero los
    componentes visuales almacenan el estado de la aplicación (ej. se
    consulta el progreso leyendo el string de un Gtk.Label en lugar de
    preguntar al objeto del modelo).
  
  - **Insuficiente (0.0 \- 0.9 pts):** El "síndrome del botón
    inteligente": la lógica del modelo está escrita de forma
    procedimental dentro del manejador del botón de la interfaz.

## 📌 Hito 3: Concurrencia y Sincronización con el Main Loop (Peso: 35% / Máx: 3.5 pts)

  - **Excelente (3.0 \- 3.5 pts):** Pasa limpiamente el test de estrés
    (ventana móvil en círculos sin congelación). Las descargas no
    corren en el thread principal. Las modificaciones visuales se
    delegan de forma estricta al hilo principal mediante
    `GLib.idle_add()`. El botón de cancelar responde al instante y los
    hilos mueren limpiamente al cerrar la ventana.
  
  - **Aceptable (1.8 \- 2.9 pts):** La interfaz no se congela, pero se
    aprecian parpadeos visuales o micro-bloqueos debido a que el hilo
    secundario pasa bloques de código demasiado grandes a
    `GLib.idle_add()`, saturando el *Main Loop*.
  
  - **Fallo Crítico (0.0 pts en este bloque):** Se produce cualquiera
    de las siguientes situaciones:
  
    * El sistema muestra el mensaje "No responde" o la interfaz se
      congela.
	
    * El hilo secundario modifica directamente un componente GTK
      (ej. `label.set_text()` sin pasar por `GLib.idle_add()`),
      provocando excepciones o comportamientos erráticos.
	
    * Al cerrar la ventana, el proceso de Python sigue activo (hilos
      zombi).

  - **Robustez ante fallos de red (+0.5 pts):** El código captura de
    forma limpia las excepciones de red en el Modelo y la usuaria
    recibe el _feedback_ adecuado.
  

  - **Falta de control de excepciones (Penalización de \-0.5 pts):**
    El programa aborta su ejecución ante una excepción de red o de
    otro tipo.

## 📌 Hito 4: Internacionalización (i18n) y Localización (l10n) (Peso: 20% / Máx: 2.0 pts)

  - **Excelente (1.7 \- 2.0 pts):** El 100% de los strings visibles
    (incluyendo diálogos de error, la barra de estado, etc.) se traducen
    "al vuelo" usando GNU gettext y la convención \_(). El módulo
    locale adapta dinámicamente los separadores decimales/millares y
    el formato de fecha exacto de la región. El diseño es elástico y
    los textos largos no se cortan.
  
  - **Aceptable (1.0 \- 1.6 pts):** Las traducciones de los botones
    principales funcionan, pero los mensajes de error o los títulos de
    las ventanas siguen *hardcodeados* en el idioma original. Los
    números se muestran como strings crudos sin formato regional.
  
  - **Insuficiente (0.0 \- 0.9 pts):** El estudiante usó condicionales
    if idioma \== "en": manuales en el código para cambiar los textos
    o concatenó las fechas de forma rígida (dia \+ "/" \+ mes).


## 📑 Memoria Técnica y Buenas Prácticas (Peso: 10% / Máx: 1.0 pt)**

  - **Evaluación (0.0 \- 1.0 pt):** Justificación clara del patrón
    arquitectónico mediante un diagrama de clases simplificado. Estilo
    de código conforme a las directrices de **PEP 8**. El repositorio
    está limpio de archivos temporales de compilación (ej. exclusión
    correcta de carpetas \_\_pycache\_\_ o archivos .po sin compilar
    mediante un .gitignore adecuado).
  

---

# Pruebas exploratorias

A continuación se describe una batería de _pruebas técnicas y
funcionales_ que ayuda a validar la ausencia de los errores descritos.
Cada pruebas está asociada a una puntuación o penalización directa.


_Warning:_ Esta batería supone un mínimo de pruebas a realizar para
validar la calidad de la aplicación. Es posible y recomendable
realizar más pruebas.


## Bloque 1: Pruebas de Concurrencia y Reactividad (30% de la nota)

  - __🔴 Prueba 1.1: El test del estrés y ventana congelada (The Frozen UI Test)__

	* **Objetivo:** Verificar que las descargas pesadas corren en
      hilos de fondo y no bloquean el Hilo de Despacho de Eventos
      (EDT).
	
	* **Procedimiento:**
	  1. Iniciar la aplicación.
	  2. Añadir 3 descargas simultáneas de archivos pesados (o
         simulaciones de más de 10 segundos).
	  3. Mientras las barras de progreso avanzan,arrastrar la
         ventana en círculos de forma rápida por la pantalla.
	  4. Maximizar y minimizar la ventana repetidas veces.
	  
    * **Resultado esperado (Apto):** La ventana se mueve de forma
      suave, se redimensiona instantáneamente y el sistema operativo
      no muestra el mensaje de "No responde". Las barras de progreso
      siguen actualizándose visualmente mientras se mueve la ventana.

    * **Fallo crítico (0 puntos en concurrencia):** La ventana se
      congela, se vuelve blanca de forma intermitente, el cursor
      muestra el icono de carga del sistema operativo, el renderizado
      se pausa por completo hasta que termina la descarga, o el
      sistema muestra el mensaje de "No responde".


  - __🔴 Prueba 1.2: El test de la cancelación reactiva__

    * **Objetivo:** Comprobar la comunicación asíncrona bidireccional
      y la respuesta a eventos durante tareas pesadas.
	
	* **Procedimiento:**
      1. Iniciar una descarga pesada.
      2. Cuando el progreso vaya por el 30%, pulsar el botón
         individual de "Cancelar".
		 
    * **Resultado esperado (Apto):** El estado de esa fila cambia
      inmediatamente a "Cancelado", la barra de progreso se detiene
      por completo y las *demás* descargas activas continúan su
      ejecución sin inmutarse.
	
    * **Fallo:** El botón de cancelar no responde al hacer clic, o
      responde únicamente cuando la descarga ya ha llegado al 100%
      (síntoma de que el evento de clic se quedó encolado detrás de la
      tarea pesada).
	  

  - __🔴 Prueba 1.3: Inspección de Hilos Activos (El test del "Zombi")__

    * **Objetivo:** Garantizar el cierre seguro de los flujos de ejecución.
	
    * **Procedimiento:**
      1. Abrir el monitor de procesos del sistema operativo
         (P.e.: Administrador de tareas en Windows, Monitor de Actividad en
         macOS, o htop/ps en Linux) o el inspector de hilos del IDE
         (Eclipse/IntelliJ/VS Code).
      2. Iniciar 2 descargas largas en la aplicación.
      3. Cerrar la aplicación pulsando la "X" de la ventana principal.
      4. Observar el monitor de procesos o la consola del IDE.
	  
    * **Resultado esperado (Apto):** El proceso del programa finaliza
      inmediatamente.
	
    * **Fallo (Penalización severa):** La ventana de la interfaz
      desaparece, pero el proceso sigue vivo en segundo plano
      consumiendo CPU, debido a que los hilos de fondo quedaron en
      bucles infinitos no interrumpidos.
	  

  - __🔴 Prueba 1.4: El test del Servidor Apagado (Connection Refused Test)__

    * **Objetivo:** Verificar que la aplicación gestiona correctamente
      las excepciones de red asíncronas y no colapsa (*crash*) si el
      endpoint no está disponible.
	
    * **Procedimiento:**
      1. Asegurarse de que el servidor simulado **está completamente
         apagado**.
      2. Iniciar la aplicación.
      3. Introducir un nombre de archivo válido y pulsar el botón
         **"Añadir a la cola"**.
		 
    * **Resultado esperado (Apto):** La aplicación añade las filas a
      la lista normalmente, pero tras un breve instante (intento de
      conexión), el estado de la descarga cambia automáticamente a
      **"Error"** (o su traducción correspondiente según el idioma
      activo) y el botón de cancelar se deshabilita. La interfaz
      gráfica sigue respondiendo perfectamente.
	
    * **Fallo crítico (Penalización severa):** La aplicación se cierra
      inesperadamente arrojando una excepción, o la ventana se queda
      congelada intentando conectar (seguramente debido a que se
      ejecutó el intento de conexión en el hilo principal).
	  

  - __🔴 Prueba 1.5: El test de la caida del servidor o la red__

    * **Objetivo:** Verificar que la aplicación gestiona correctamente
      las excepciones de red asíncronas y no colapsa (*crash*) si el
      endpoint dejar de estar disponible.

    * **Procedimiento:**
      1. Asegurarse de que el servidor simulado **está operativo**.
      2. Iniciar la aplicación.
      3. Iniciar varias descargas.
      4. Apagar abruptamente el servidor.
  
    * **Resultado esperado (Apto):** Tras un breve instante (timeout de
      la conexión), el estado de la descarga cambia automáticamente a
      **"Error"** (o su traducción correspondiente según el idioma
      activo) y el botón de cancelar sigue habilitado. La interfaz
      gráfica sigue respondiendo perfectamente, permitiendo al usuario
      intentar añadir más descargas, cancelar las actuales, o finalizar
      la aplicación.

    * **Fallo crítico (Penalización severa):** La aplicación se cierra
      inesperadamente arrojando una excepción, o la ventana se queda
      congelada indefinidamente esperando recibir datos de la conexión
      (debido probablemente a que se ejecutó el intento de conexión en
      el hilo principal).


## Bloque 2: Pruebas de Arquitectura y Separación de Capas (30% de la nota)

  - __🔴 Prueba 2.1: El test del "Modo Texto" (Desacoplamiento)__

    * **Objetivo:** Demostrar empíricamente la independencia del
      Modelo respecto a la Vista.
	  
    * **Procedimiento (Inspección de código):**
      1. Ir al directorio del código fuente que contiene las clases
         del **Modelo**.
      2. Buscar palabras clave del framework gráfico (ej. en Java:
         import javax.swing, import javafx, JButton, JLabel).
	  3. Ejecutar el modelo desde consola o pruebas unitarias sin
         instanciar ni una sola clase de la interfaz gráfica.
      4. *Opcional*: Intentar crear una clase Main alternativa en
         consola que instancie el modelo y ejecute una simulación de
         descarga imprimiendo el progreso con un simple `print`.
	  
    * **Resultado esperado (Apto):** El modelo compila perfectamente
      sin necesidad de que exista la interfaz gráfica. No hay
      dependencias visuales.
	
    * **Fallo (0 puntos en arquitectura):** Las clases de lógica
      matemática o de negocio contienen referencias a etiquetas de la
      interfaz para poder escribir el progreso de la descarga.
	  

## Bloque 3: Pruebas de Internacionalización y Diseño Elástico (20% de la nota)

  - __🔴 Prueba 3.1: El test del "Idioma Klingon / Fantasía"__

    * **Objetivo:** Asegurar que el 100% de las cadenas visibles pasan
      por el sistema de ficheros de recursos (i18n).
	
    * **Procedimiento:**
      1. Buscar el archivo de traducciones de un texto secundario.
      2. Modificar temporalmente todas sus traducciones por palabras
         aleatorias legibles (ej. cambiar "Download" por "KLINGON\_1",
         "Cancel" por "KLINGON\_2", o directamente por palabras en
         idioma Klingon).
      3. Iniciar la aplicación con la configuración cambiada al idioma
         del perfil que hemos modificado.
      4. Provocar un error a propósito (ej. introducir una URL inválida).
  
    * **Resultado esperado (Apto):** Absolutamente toda la interfaz
      gráfica cambia a los textos modificados, incluyendo los títulos
      de las ventanas emergentes y diálogos, los mensajes de error,
      etc.
	  
	* **Fallo:** Quedan textos "olvidados" en el idioma original del
      código porque fueron programados directamente como literales
      (hardcoded).
	  

  - __🔴 Prueba 3.2: El test de la "Palabra Larga" (Diseño Elástico)__

    * **Objetivo:** Comprobar que el diseño de la interfaz se adapta
      al tamaño dinámico de los textos traducidos.
	  
    * **Procedimiento:**
      1. Modificar un archivo de localización e introducir traducciones
         extremadamente largas (ej. cambiar el texto de un botón de
         "Añadir" por
         "Adicionar\_Elemento\_A\_La\_Cola\_De\_Descargas\_Activas").
	  2. Cambiar la configuración a ese idioma.
	  
    * **Resultado esperado (Apto):** Los *Layout Managers*
      (manejadores de distribución espacial) reajustan el tamaño de
      los botones automáticamente o habilitan barras de
      desplazamiento. El texto es visible.
	
    * **Fallo:** El texto aparece cortado (ej. "Adicionar\_Ele..."),
      se superpone con otros componentes visuales o rompe por completo
      la estética de la ventana haciendo desaparecer otros elementos.


## 📅 Bloque 4: Pruebas de Localización de Fechas y Números (l10n)

  - __🔴 Prueba 3.3: El test del "Cambio de Localidad" (Locale Test)__

    * **Objetivo:** Verificar que la aplicación adapta automáticamente
      el formato de los datos numéricos y cronológicos según la región
      e idioma seleccionados (sin concatenaciones manuales de texto).
	
    * **Procedimiento:**
      1. Iniciar una descarga pesada o simulación que muestre la
         **velocidad de descarga** (ej. 1.543,21 KB/s o 1,543.21 KB/s)
         y el **tamaño total** del archivo.
      2. Esperar a que la descarga termine con éxito para que la
         aplicación registre y muestre la **fecha y hora de
         finalización**.
      3. Repetir el procedimiento con varias configuraciones de
         idioma. Ej. de **Español de España es\_ES** a **Inglés de
         Estados Unidos en\_US**.
		 
    * **Resultado esperado (Apto):**
      * **Separadores numéricos:** Por ejemplo, en español, la
        velocidad debe mostrarse con coma decimal y punto de millar
        (ej: 2.450,75 KB/s). Sin embargo en inglés, debe representarse
        usando punto decimal y coma de millar (ej: 2,450.75 KB/s).
	  
      * **Formato de fecha y hora:** De forma análoga, en español, la
        fecha debe seguir el orden europeo _Día/Mes/Año_ (ej:
        19/08/2026 18:30) o formato largo. Mientras que en inglés de
        estados unidos, la fecha se representa como Mes/Día/Año (ej:
        08/19/2026 06:30 PM).
	  
    * **Fallo crítico (Penalización en l10n):** Los números y fechas
      se muestran siempre en el mismo formato. Seguramente porque el
      alumno usó concatenaciones manuales del tipo dia \+ "/" \+ mes o
      convirtió los números a texto usando un simple
      Double.toString(velocidad).
	  

  - __🔴 Prueba 3.4: El test de las Unidades de Medida y Plurales__

    * **Objetivo:** Comprobar que las unidades de almacenamiento
      cambian de escala correctamente y que los textos auxiliares
      respetan las reglas de pluralización de cada idioma.
	
    * **Procedimiento:**
      1. Agregar un archivo muy pequeño (ej. 500 bytes) y otro muy
         grande (ej. 2.5 GB).
      2. Observar cómo la interfaz renderiza las unidades de tamaño y
         los mensajes de la barra de estado inferior (ej: "1 descarga
         activa" vs "2 descargas activas").
      3. Repetir el procedimiento con varias configuraciones de idioma.
	  
    * **Resultado esperado (Apto):** Los textos cambian correctamente
      su pluralización en base al contador (Español: 1 descarga / 2
      descargas; Inglés: 1 download / 2 downloads). Las unidades se
      formatean con la unidad más adecuada según el estándar del
      framework internacionalizado (ej: 500 B, 2.5 GB).
	  
    * **Fallo:** Aparecen errores de concordancia de número (ej: 1
      downloads o tamaños de archivo mostrados siempre en bytes crudos
      como 2500000000 Bytes porque no se aplicó una clase formateadora
      de tamaño de almacenamiento).


---



# Apoyo Técnico para Python y GTK 4

_Tip 💡:_ Recuerda que Gtk4 que es el estándar nativo para entornos de
escritorio como GNOME.


Para cumplir con los requisitos de arquitectura, concurrencia e
internacionalización exigidos en este trabajo práctico utilizando
__python__ y la librería __GTK 4__, se debe hacer uso de _gobject
introspection__ (los *bindings* oficiales de Python para la biblioteca
GObject) y las herramientas estándar del sistema operativo.


## Framework de Interfaz Gráfica: GTK 4

  - **Instalación base:** Los estudiantes deberán instalar `gi`
    (_g_object _i_ntrospection). Generalmente requiere dependencias
    del sistema como libgirepository1.0-dev en sistemas basados en
    Debian/Ubuntu.

##  Concurrencia Segura y Reactividad (Evitar el bloqueo del Main Loop)

En GTK, el hilo principal ejecuta el *Main Loop* que dibuja la
pantalla y captura los eventos de la usuaria. Cualquier tarea pesada
que se ejecute en hilo, congelará la aplicación por completo.

Para solucionarlo en GTK 4, la estrategia combina la librería estándar
threading de Python con funciones específicas de **GLib**.

  1. **El Hilo de Fondo:** La tarea pesada debe ejecutarse dentro de
     un hilo estándar de Python (threading.Thread).

  2. **Prohibición de Modificación Directa:** Está estrictamente
     prohibido llamar a funciones como `label.set\_text()` o
     `progress\_bar.set\_fraction()` desde dentro de ese hilo
     secundario. Romperá la interfaz de forma errática.

  3. **Comunicación Segura con GLib.idle\_add:** Para actualizar la
     interfaz, el hilo de fondo debe delegar la función de
     actualización al hilo principal usando `GLib.idle\_add()`. Esta
     función encola una tarea para que el *Main Loop* la ejecute de
     forma segura en cuanto esté libre.

```python
import threading
from gi.repository import GLib

# 1. Función que ejecuta en el hilo principal
def actualizar_gui_progreso(porcentaje, label_componente):
    label_componente.set_text(f"{porcentaje}%")
    return False # Retornar False para que GLib no repita la llamada

# 2. Función que ejecuta el hilo secundario
def tarea_descarga_pesada(label_componente):
    for i in range(101):
        # ... simulación de descarga o E/S ... (llamada al modelo)
        # Se envía la actualización de forma segura al Main Loop de GTK
        GLib.idle_add(actualizar_gui_progreso, i, label_componente)
```


## Internacionalización (i18n) mediante GNU gettext

A diferencia de otras librerías, que tiene sus propias herramientas,
GTK utiliza el estándar de la industria en sistemas Unix: __GNU
gettext__. También es la herramienta más utilizada en el software
libre.


**Flujo de trabajo:**

  1. __Importación del gettext:__ Por convención la función de
     traducción principal se renombra como `\_`:

```python
from gettext import gettext as _
```

  2. __Encapsulamiento en el código:__ Todas las cadenas de texto del
     código Python deben envolverse en la función de traducción:
   
```python
    boton.set_label(_("Añadir a la cola"))
```

3. __Extracción de textos:__ Los estudiantes utilizarán la herramienta
   de consola `xgettext` para escanear sus archivos `.py` y generar un
   archivo plantilla `.pot` (ej. `messages.pot`).

4. __Traducción:__ A partir de la plantilla, crean los archivos de
   traducción `.po` (ej. `en.po` para inglés) y los editan convenientemente.

5. __Compilación:__ Los archivos `.po` deben compilarse a archivos
   binarios `.mo` usando `msgfmt`. Estos archivos se guardan en una
   estructura de carpetas específica (ej:
   `locale/en/LC\_MESSAGES/downloader.mo`).

6. __Inicialización en GTK:__ Al arrancar la aplicación se configura
   el dominio de traducción:

```python
    gettext.bindtextdomain('downloader', 'path/to/locale')
    gettext.textdomain('downloader')
```


## Localización (l10n) de Fechas y Números

Para dar formato regional a la velocidad (puntos/comas decimales) y a
la fecha de finalización en un entorno GTK puro, debemos utilizar el
módulo nativo `locale` de Python, el cual se sincroniza
perfectamente con la configuración regional del sistema.

**Ejemplo de uso con locale:**

```python
import locale
from datetime import datetime

# Establecer la configuración regional según el idioma configurado en el sistema.
locale.setlocale(locale.LC_ALL, '')

# Formatear números con millares y decimales de forma regional
# Resultado en en_US: "1,543.21" | Resultado en es_ES: "1.543,21"
velocidad_texto = locale.format_string("%.2f", 1543.21, grouping=True)

# Formatear la fecha según el estándar cultural de la región seleccionada
# Resultado en en_US: "08/19/2026" | Resultado en es_ES: "19/08/2026"
fecha_texto = datetime.now().strftime(locale.nl_langinfo(locale.D_FMT))
```

_Tip 💡:_ Si has programado algo como `if (idioma \== "en")` para
cambiar el formato de los datos, no es correcto.
apartado.



## 💡 Entorno de corrección

Para evaluar el código en tu equipo de desarrollo:

  - Compilar los archivos .po

```
$ msgfmt locale/en/LC\_MESSAGES/downloader.po \-o locale/en/LC\_MESSAGES/downloader.mo
```

  - Prepara dos terminales:

    1. **Terminal 1 (Servidor):** Ejecutas el servidor.

    2. **Terminal 2 (Cliente):** Ejecutas la aplicación.


    De esta forma puedes:
	
	- En mitad de la ejecución hacer _Ctrl+C_ para apagar el servidor.
	
	- Relanzar el servidor después de apagarlo.
	
	- Ejecutar la aplicación sin lanzar el servidor.


