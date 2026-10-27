# Pairing: trabajar con agentes de IA con más estructura

En esta sesión vamos a trabajar juntos sobre una tarea real, desde la definición del problema hasta un primer incremento probado. La idea es practicar un proceso que podamos repetir después, con pasos pequeños y tiempo para revisar lo que propone el agente.

No buscamos aprender cuatro skills, sino practicar cómo dirigir el trabajo con IA.

## Antes de abrir el agente

La primera conversación es entre nosotros. Antes de invocar una sola skill, te pediré que respondas a estas cinco preguntas:

1. ¿Qué problema estamos resolviendo y para quién?
2. ¿Qué está dentro y fuera del scope?
3. ¿Qué restricciones debemos respetar? Arquitectura, convenciones, compatibilidad, seguridad, etc.
4. ¿Qué decisiones técnicas debemos tomar nosotros?
5. ¿Cómo sabremos que hemos terminado?

No hace falta escribir un documento. Cinco minutos de conversación y unas notas son suficientes para empezar. Lo importante es que el problema lo hayas definido tú.

También quiero que lleguemos a la investigación con unas hipótesis propias sobre los límites del cambio: qué creemos que hay que tocar, qué debería quedar fuera y por qué.

Podemos equivocarnos. El agente puede encontrar algo que nos haga revisar esos límites. Pero quiero que ese cambio venga de contrastar nuestras hipótesis con evidencia, en lugar de aceptar los límites que proponga la IA sin más.

## El proceso

### 0. Frame the problem - HUMAN LEAD

Con las cinco preguntas, acordamos el problema, el alcance, las restricciones y los criterios de éxito. Este paso lo hacemos sin agente.

Antes de seguir, deberíamos poder explicar qué queremos resolver y qué hemos decidido dejar fuera.

### 1. Plan

Usamos `plan` para investigar el código y poner a prueba las hipótesis iniciales. Le pedimos al agente que busque evidencia y cuestione nuestras decisiones, también las que parecen obvias.

Mi peer revisa las propuestas y decide cuáles acepta, cuáles rechaza y qué necesita comprobar mejor. Si cambia un límite, dejamos anotado qué hemos aprendido para cambiarlo.

Podemos pasar al siguiente paso cuando tengamos un enfoque que él pueda explicar, con las dudas pendientes a la vista.

### 2. Spec

Definimos los comportamientos esperados y los contratos que debemos respetar. Necesitamos suficiente detalle para comprobar después si la implementación hace lo acordado.

La especificación debería ayudarnos a escribir los tests y a revisar el resultado, sin tener que adivinar qué queríamos decir.

### 3. Tickets

Dividimos el trabajo en incrementos pequeños. Cada ticket debe decir qué cambia y cómo vamos a comprobarlo.

Elegimos un primer incremento que podamos implementar y revisar durante la sesión. El resto puede esperar.

### 4. Implement

Construimos ese incremento con TDD:

1. Escribimos un test para el comportamiento esperado y comprobamos que falla por el motivo correcto.
2. Implementamos lo mínimo para que pase.
3. Refactorizamos y comprobamos que los tests siguen pasando.

Revisamos el código y las decisiones del agente frente a la especificación. Que los tests pasen es parte de la comprobación; también tenemos que entender el cambio y confirmar que respeta los límites acordados.

## Cómo repartimos los 60 minutos

| Tiempo | Bloque | Qué hacemos |
| --- | --- | --- |
| 0-5 min | El principio | Explicamos qué vamos a practicar y qué decisiones queremos mantener en nuestras manos. |
| 5-15 min | Frame the problem | Mi peer explica la tarea y responde a las cinco preguntas. Acordamos alcance y criterios de éxito, sin agente. |
| 15-30 min | Research + grilling | Usamos `plan` para investigar y cuestionar las hipótesis. Él valida o rechaza las propuestas con la evidencia delante. |
| 30-40 min | Spec + tickets | Definimos comportamientos verificables y dividimos el trabajo en incrementos pequeños. |
| 40-55 min | Implementación | Implementamos el primer incremento con TDD y revisamos las decisiones y el resultado del agente. |
| 55-60 min | Reflexión | Hablamos sobre qué ha decidido él, qué ha delegado y qué haría diferente. |

Este reparto es una guía. Si una duda necesita más tiempo, prefiero reducir el incremento antes que correr para completar todos los pasos. No necesitamos terminar toda la tarea en una hora.

## Los últimos cinco minutos

Quiero cerrar con tres preguntas:

- ¿Qué decisiones has tomado tú?
- ¿Cuáles has delegado al agente?
- ¿Qué harías diferente la próxima vez?

Con esas respuestas podremos ver qué partes del proceso le han ayudado y cuáles conviene ajustar para la siguiente sesión.
