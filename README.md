# Pairing: trabajar con agentes de IA con más estructura

En esta sesión vamos a trabajar juntos sobre una tarea real, desde la definición del problema hasta un primer incremento probado. La idea es practicar un proceso que podamos repetir después, con pasos pequeños y tiempo para revisar lo que propone el agente.

No buscamos memorizar las skills, sino practicar cómo dirigir el trabajo con IA.

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

Antes de pasar al siguiente paso, revisamos el resultado. Si aparece algo que cambia el alcance o contradice una hipótesis, volvemos al paso que corresponda.

### 0. Frame the problem - Human driven

Con las cinco preguntas, acordamos el problema, el alcance, las restricciones y los criterios de éxito. Este paso lo hacemos sin agente.

Antes de seguir, deberíamos poder explicar qué queremos resolver y qué hemos decidido dejar fuera.

### 1. Plan

Usamos `/peer-plan` para investigar el código y poner a prueba las hipótesis iniciales. Le pedimos al agente que busque evidencia y cuestione nuestras decisiones, también las que parecen obvias.

Mi peer revisa las propuestas y decide cuáles acepta, cuáles rechaza y qué necesita comprobar mejor. Si cambia un límite, dejamos anotado qué hemos aprendido para cambiarlo.

Podemos pasar al siguiente paso cuando tengamos un enfoque que él pueda explicar, con las dudas pendientes a la vista.

### 2. Spec

Definimos los comportamientos esperados y los contratos que debemos respetar. Necesitamos suficiente detalle para comprobar después si la implementación hace lo acordado.

La especificación debería ayudarnos a escribir los tests y a revisar el resultado, sin tener que adivinar qué queríamos decir.

### 3. Tickets

Dividimos el trabajo en incrementos pequeños. Cada ticket debe decir qué cambia y cómo vamos a comprobarlo.

Elegimos un primer incremento que podamos implementar y revisar durante la sesión. El resto puede esperar.

### 4. Implement

Pasamos a `/peer-implement` la ruta del ticket elegido. Esta skill se apoya en `/peer-tdd` para construir un comportamiento cada vez:

1. Escribimos un test para el comportamiento esperado y comprobamos que falla por el motivo correcto.
2. Implementamos lo mínimo para que pase.
3. Repetimos con el siguiente comportamiento del ticket, comprobando los tests durante el trabajo y la suite completa al terminar.

Después usamos `/peer-code-review` para revisar el código y las decisiones del agente frente a la especificación. Dejamos la refactorización para esta fase de revisión y comprobamos que los tests siguen pasando. Que los tests pasen es parte de la comprobación; también tenemos que entender el cambio y confirmar que respeta los límites acordados.

## Cómo repartimos los 60 minutos

| Tiempo | Bloque | Qué hacemos |
| --- | --- | --- |
| 0-5 min | El principio | Explicamos qué vamos a practicar y qué decisiones queremos mantener en nuestras manos. |
| 5-15 min | Frame the problem | Mi peer explica la tarea y responde a las cinco preguntas. Acordamos alcance y criterios de éxito, sin agente. |
| 15-30 min | Research + grilling | Usamos `/peer-plan` para investigar y cuestionar las hipótesis. Él valida o rechaza las propuestas con la evidencia delante. |
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

## Referencia de skills

Para la sesión, podemos copiar el contenido del `SKILL.md` que necesitemos y pegarlo en el agente. No hace falta configurar un plugin. Los nombres con `/` identifican cada skill; usarlos como comandos requiere que estén instaladas en el agente.

El prefijo `peer-` distingue estas skills de las que ya tenga el agente. Es una convención de nombres, sin plugin ni configuración adicional.

### Workflow

```text
0. Frame the problem   Human driven, sin skill ni agente
          |
          v
1. Plan               /peer-plan
          |
          v
2. Spec               /peer-spec
          |
          v
3. Tickets            /peer-tickets
          |
          v
4. Implement          /peer-implement, un ticket cada vez
                      |
                      +-- /peer-tdd: test que falla -> codigo minimo
                      |
                      +-- /peer-code-review: revisar el cambio
```

### Qué hace cada skill

| Skill | Cuándo usarla | Qué hace |
| --- | --- | --- |
| [`/peer-plan`](skills/peer-plan/SKILL.md) | Después de definir el problema entre nosotros. | Investiga el código y cuestiona las hipótesis por rondas. Las decisiones las tomamos nosotros. Termina cuando confirmamos que compartimos el mismo enfoque. |
| [`/peer-spec`](skills/peer-spec/SKILL.md) | Cuando el enfoque está acordado. | Sintetiza la conversación sin abrir otra entrevista. Guarda comportamientos, contratos, decisiones y dudas en `.idea/<feature-slug>/spec.md`. |
| [`/peer-tickets`](skills/peer-tickets/SKILL.md) | Con una spec lista para descomponer. | Propone incrementos pequeños con criterios de aceptación y dependencias. Tras nuestra aprobación, escribe un Markdown por ticket en `.idea/<feature-slug>/tickets/`. |
| [`/peer-implement`](skills/peer-implement/SKILL.md) | Cuando elegimos un ticket para construir. | Lee el ticket local, usa `peer-tdd`, ejecuta comprobaciones, pide una revisión con `peer-code-review` y hace commit en la rama actual. Si el ticket no está claro, pregunta antes de empezar. |
| [`/peer-tdd`](skills/peer-tdd/SKILL.md) | Durante la implementación. | Trabaja un comportamiento cada vez: test que falla y código mínimo para hacerlo pasar. Acuerda con nosotros las interfaces que se van a probar y sigue las convenciones de testing del proyecto. |
| [`/peer-code-review`](skills/peer-code-review/SKILL.md) | Al revisar el incremento. | Busca bugs, fallos de seguridad y problemas concretos de estructura o rendimiento. Puede revisar cambios sin commit, un commit, una comparación con otra rama o una MR de GitLab. |

### Archivos de trabajo

La spec y los tickets comparten el mismo `feature-slug`. Por ejemplo:

```text
.idea/
  cart-checkout/
    spec.md
    tickets/
      01-confirm-checkout.md
      02-handle-payment-failure.md
```

Al pasar a tickets, damos la ruta de la spec. Al implementar, damos la ruta de un ticket concreto. Así evitamos que el agente tenga que elegir el trabajo por nosotros.

## Instalación en Claude Code

La opción más simple para tener los comandos disponibles es copiar las carpetas a `~/.claude/skills/`. No necesitamos un plugin. Las skills quedarán disponibles en tus proyectos, solo para tu usuario.

Clona este repositorio si aún no lo tienes:

```bash
git clone https://github.com/nobuti/mini.git
cd mini
```

Desde la raíz de este repositorio:

```bash
mkdir -p ~/.claude/skills
cp -R skills/peer-* ~/.claude/skills/
```

Si ya tienes carpetas con esos nombres en el destino, revísalas antes de copiar: el comando puede sobrescribir sus archivos.

Abre Claude Code en el proyecto donde vayas a trabajar. Si ya estaba abierto, reinicia la sesión. Escribe `/peer-` para comprobar que aparecen las seis skills. Después de definir el problema entre nosotros, empieza con `/peer-plan`.

Para una sesión puntual, también podemos seguir copiando y pegando el contenido de cada `SKILL.md`, sin instalar nada. En ese caso, los comandos no se registran y tendremos que aportar las instrucciones de las skills de apoyo cuando hagan falta.
