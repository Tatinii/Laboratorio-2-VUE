Integrantes de equipo para Laboratorio 1
-Kriscia Tatiana Del Cid Argueta 
-Ludwin Saúl Vásques Romero

Situación problemática:
La situación problemática en la Universidad Gerardo Barrios (UGB) de San Miguel radica en la dificultad que enfrentan los estudiantes de Ingeniería en Sistemas para gestionar presupuestos destinados a la optimización de sus estaciones de trabajo, lo que suele derivar en gastos impulsivos o decisiones financieras ineficientes que comprometen sus metas a largo plazo. Enfocada en el sector de la Gestión Financiera Estudiantil, esta aplicación de Vue.js resuelve el problema al permitir definir un presupuesto máximo y registrar artículos de hardware de forma dinámica, utilizando variables reactivas y propiedades computadas para calcular el saldo restante en tiempo real. Mediante validaciones estrictas de datos y alertas visuales automáticas ante excedentes, el sistema garantiza una toma de decisiones informada y coherente con la realidad económica del estudiante, asegurando la integridad de los registros y evitando proactivamente el ingreso de montos negativos o campos vacíos en el inventario.

Desarrollo de preguntas:
1. Explique con sus propias palabras qué es Vue.js y cuál es su función dentro de la
página web desarrollada.

Vue.js es un framework del lado del cliente en JavaScript diseñado para extender el HTML y construir 
interfaces de usuario con comportamientos personalizados. Dentro de nuestro simulador financiero para tu 
setup, su función principal es sincronizar el estado interno de los datos con lo que el usuario visualiza 
en pantalla. En lugar de que tú manipules manualmente el DOM para actualizar los cálculos del presupuesto 
o insertar nuevos periféricos, Vue utiliza su motor reactivo para detectar cambios en las variables y 
redibujar automáticamente solo las áreas necesarias de la interfaz, optimizando el rendimiento y 
simplificando la arquitectura.

2. Describa qué variables reactivas utilizó en su aplicación y cuál es la función de
cada una dentro del sistema.

En la arquitectura del sistema, definimos múltiples variables reactivas para el control del estado. 
Utilizamos referencias simples para establecer el tituloApp, definir el presupuestoBase inicial, y 
capturar los valores temporales de nombreArticulo y precioArticulo desde el formulario. Adicionalmente,
 declaramos el arreglo inventarioSetup para preservar el historial de hardware y el booleano 
 errorValidacion para controlar el estado de las alertas. Para escalar esta lógica de manera eficiente, 
 implementamos propiedades computadas como totalInvertido y saldoRestante, las cuales recalculan 
 automáticamente los montos basándose en las variables anteriores, garantizando que la matemática 
 financiera sea siempre precisa y reactiva.

3. Explique la diferencia entre las siguientes directivas utilizadas en su proyecto: v-
bind y v-model

La diferencia técnica entre las directivas empleadas radica en la dirección en la que fluye la 
información. La directiva v-bind establece un enlace unidireccional que permite vincular dinámicamente 
atributos HTML o clases de estilo al estado de nuestra aplicación. Nosotros la aplicamos para teñir el 
texto de rojo únicamente cuando tu saldo restante cae por debajo de cero. En contraste, la directiva 
v-model genera un enlace bidireccional estricto entre los inputs del formulario y los datos de la 
instancia de Vue. Esto significa que, si escribes un precio en la pantalla, la variable en memoria se 
actualiza al instante, y si la lógica de nuestro código reinicia la variable tras un registro exitoso, el 
campo de texto se vacía automáticamente frente al usuario.

4. Mencione al menos un ejemplo de evento utilizado dentro de su aplicación.

La aplicación captura las acciones del usuario a través del manejo de eventos. El ejemplo más crítico en 
nuestro código es la implementación del evento de clic, escrito con la sintaxis abreviada @click, situado 
en el botón principal de "Añadir al Presupuesto". Al ejecutarse, este evento captura el estímulo del 
mouse e invoca de inmediato el método registrarComponente, actuando como el detonador que inicia todo el 
proceso de validación lógica y almacenamiento de datos sin depender de recargas nativas del navegador.

5. Explique para qué utilizó la directiva v-for dentro de su aplicación.

La directiva v-for fue implementada como el motor de iteración de nuestro proyecto, resolviendo el 
problema arquitectónico de renderizar listas dinámicas en el DOM. Su función específica es recorrer el 
arreglo inventarioSetup elemento por elemento, extrayendo las propiedades de nombre y precio de cada 
pieza de hardware para inyectarlas en etiquetas de lista. Este enfoque elimina por completo la 
redundancia de código y permite que tu historial de compras crezca o se reduzca de manera fluida y 
automatizada según los componentes que vayas añadiendo.

6. Describa en qué situación utilizó v-if y qué problema resuelve dentro de su
interfaz.

empleamos la directiva v-if para resolver problemas de experiencia de usuario mediante el renderizado 
condicional, logrando que ciertos bloques del HTML solo existan si se cumple una evaluación lógica. En 
nuestra interfaz, la utilizamos de manera táctica en dos escenarios: primero, para desplegar una alerta 
visual en rojo solo cuando se detectan entradas inválidas, y segundo, para mostrar un texto indicando que 
la lista de inversión está vacía cuando el arreglo aún no contiene hardware. Esto mantiene la pantalla 
limpia y evita mostrar advertencias fuera de contexto

7. Explique cómo se realiza la validación de datos en su aplicación y por qué es
importante validar la información ingresada por el usuario.

la validación de datos se ejecuta interceptando la información antes de guardarla, exigiendo lógicamente 
que el nombre no sea una cadena de texto vacía y asegurando que el precio sea numéricamente mayor a cero. 
Como ingeniero de la UGB, debes entender que validar información es tu primera línea de defensa; asegurar 
la integridad de las entradas evita que el sistema propague valores nulos o precios negativos que 
corromperían los cálculos reactivos, previniendo así un análisis financiero defectuoso que afecte tu 
planificación a largo plazo.