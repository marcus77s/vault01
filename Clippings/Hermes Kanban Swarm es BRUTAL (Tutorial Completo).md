---
title: "Hermes Kanban Swarm es BRUTAL (Tutorial Completo)"
source: "https://www.youtube.com/watch?v=_sNppItjUZY&t=639s"
author:
  - "[[Alejandro Pardo | IA Automatización]]"
published: 2026-06-06
created: 2026-06-06
description: "📚 PLANTILLAS Y RECURSOS GRATIS (Comunidad Skool): https://www.skool.com/savesyncai-9500/aboutSuscríbete para más tutoriales: https://youtube.com/channel/alejandropardolA?sub_confirmation=1🔗 RECU"
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=_sNppItjUZY)

📚 PLANTILLAS Y RECURSOS GRATIS (Comunidad Skool): https://www.skool.com/savesyncai-9500/about  
  
Suscríbete para más tutoriales: https://youtube.com/channel/alejandropardolA?sub\_confirmation=1  
  
🔗 RECURSO MENCIONADO:  
→ Hermes Agent (Nous Research): https://github.com/NousResearch/hermes-agent  
  
El Kanban Swarm es la nueva forma de Hermes Agent de poner varios agentes de IA a trabajar en equipo, en paralelo y coordinándose solos. En este vídeo te enseño qué es, cómo funciona por dentro a nivel de arquitectura (el dispatcher, las dependencias, la base de datos, cómo evita que dos agentes choquen), en qué se diferencia de un agente trabajando solo, y te muestro un sistema real funcionando que monté yo mismo, sin trampa ni cartón.  
  
#hermesagent #kanban #agentesia #multiagente #inteligenciaartificial #automatizacionIA #ClaudeCode #openclaw #nousresearch #claude #codex #hermes

## Transcript

**0:00** · Si has trabajado con agentes de IA, seguro que te has dado cuenta de un problema bastante importante. Cuando quieres crear un proyecto muy grande o complejo, normalmente un solo agente no es capaz. Se atasca, se olvida de lo que está haciendo o incluso te dice que ya ha terminado cuando no es verdad.

**0:16** · Normalmente para resolver esto tienes que montar tú algo por tu cuenta. Pues bien, hace unos días Hermes, el agente de No Research, que ya cuenta con más de 180,000 estrellas en GitHub, cogió su tablero de tareas, su canvan, y lo convirtió en un sistema donde varios agentes trabajan en equipo en paralelo y se coordinan solos sin pisarse. Ellos lo han llamado Canban Swarm. Así que si te quedas hasta el final de este vídeo, vas a entender perfectamente cómo funciona por dentro, para qué sirve de verdad y cómo puedes crear tú tus propios proyectos desde este nuevo sistema.

**0:47** · Y antes de empezar, recuerda que tienes mi comunidad school totalmente gratuita, donde voy subiendo todos los recursos y plantillas de todos mis vídeos y donde además tienes cursos completos, tanto de N8N, agentes de voz, JavaScript, servidores y Hermes y OpenCloud. Además, hemos abierto hace poco una bolsa de proyectos donde cualquiera vais a poder colaborar entre vosotros, tanto para la gente que tiene proyectos pero no sabe desarrollarlos como para la gente que sabe desarrollarlos pero no tiene proyectos para así formar una sinergia muy bonita.

**1:18** · Te dejo el link en la descripción de este vídeo por si quieres unirte. Así que vamos al lío. Bien, para entender qué es Canban Swarm de Hermes, primero tenemos que entender qué es Canban a secas. Can lo inventó Toyota en 1947, en concreto un ingeniero llamado Taichi Ono. La palabra en japonés es esta de aquí que significa tablón o cartel. La idea era tener un tablón donde ahí apuntando todas las tareas que hay que hacer. Por ejemplo, aquí tenemos la columna de qué tareas hay que hacer, las que se están haciendo y las que ya se han hecho.

**1:48** · Tú aquí vas a poder tener las columnas que tú quieras, las cuales van avanzando de izquierda a derecha. Esto funcionaba muy bien para que así los trabajadores supieran en todo momento qué hay que hacer y organizarse mejor.

**1:59** · Entonces, esto al principio se popularizó específicamente para las fábricas de los coches. Con los años esto se empezó a hacer muy popular, sobre todo en el mundo software. Seguro que has oído hablar de herramientas como Trello, Gira o Linear, que al final son canvans para que los equipos de programadores se organicen mejor.

**2:15** · Entonces, lo que ha hecho Hermes ha sido esta misma idea, pero en vez de que los trabajadores sean los que van apuntando las tareas y organizándose, son los propios agentes de IA los que van a empezar a crear tareas y a completarlas. Además, tú también vas a poder estar involucrado en ello. Bueno, entonces, ¿cómo llegó el can? Bueno, todo comenzó en esta versión de aquí, la 013, el 7 de mayo, llamada Tenacity, Tenacidad. Básicamente esta versión solucionaba un problema que llevaban ya arrastrando los agentes de hace tiempo, que era que no eran capaces de completar las tareas.

**2:45** · De hecho, el lema de esta versión es Hermes ahora termina lo que empieza. Entonces, ¿cómo lo consiguieron? Pues bueno, introdujeron diferentes novedades, como podemos ver aquí. Una fue el Multient Canban, que fue el inicio del Canban. De hecho, Can ya venía de antes, pero no funcionaba muy bien y lo acabaron quitando. Y aquí ya lo volvieron a introducir, pero mucho más profesional. Básicamente era un tablero donde por un lado los trabajadores, como he dicho antes, eran agentes de IA. Cada uno tenía un proceso independiente con su propia identidad y por otro lado metieron una automatización que es muy importante que ellos llamaron el dispatcher.

**3:18** · Básicamente tenéis que verlo como si fuera un gerente que va a gestionar el canvan. Es un código que se ejecuta cada 60 segundos y de lo que se encarga es de repartir las tareas en los agentes que haya, moverla las tareas de columna en columna y revisar de que ningún agente se quede colgado. ¿Cómo hace esto? Pues bueno, tiene tres herramientas principales. Una sería el hertit, que básicamente es como el latío de un corazón, el cual cada worker o cada agente va a enviar cada 30 segundos un aviso para que el dispatcher pueda ver que ese agente sigue vivo, ¿no?

**3:50** · Entonces, si un agente, por lo que sea, deja de mandar esas señales cada 30 segundos, ahí es cuando el dispatcher va a utilizar recline, que lo que va a hacer es quitar la tarea de la gente que le ha dejado de dar señal y mandársela a otro. Y por último tiene el retri, que lo que va a hacer es que cuando un agente empiece a fallar, pues el dispatcher pueda ejecutarlo para que vuelva a intentar la tarea con un número limitado de veces. Es decir, que cuando falle ese número delimitado de veces, lo que va a hacer ya es bloquear la tarea para que ya tú, por ejemplo, manualmente puedas ver qué está pasando, ¿no?

**4:21** · Por eso digo que es como un gerente, es el que gestiona todo el canvan, pero no es ningún agente de IA, es una automatización y además todo esto se va guardando en tiempo real en una base de datos que es SQL Lite, que luego veremos más en profundidad. Y luego, además, en esa versión también metieron dos novedades nuevas. Una era lo de Barra goal, que esto lo puedes poner tú en el chat y es para darle un objetivo a un agente para que no se desvíe y pueda acabar la tarea, que era su principal problema.

**4:48** · Y luego también mejoraron los checkpoints para que la gente pues guardara el estado de la sesión y luego pudiera recuperarlo, ¿no? Pero bueno, lo que nos interesa en este vídeo de hoy es el canvan, ¿no? Entonces, la 013, para que os hagáis una idea, es cuando lo introdujeron ya de manera profesional.

**5:03** · La limitación de esta versión, de este multient canban, es que cuando tú ejecutabas una tarea, cuando tú mandabas una tarea a los agentes, tú eras el encargado como de organizar la tarea, ¿no? De dividir, si era una tarea muy grande, dividirla en trozos pequeñitos y saber a qué agente va cada tarea. Eras tú el encargado. Y entonces aquí es cuando llega la versión 015 llamada Velocity hace relativamente poco, el 28 de mayo. Y se llama Velocity porque el objetivo de esta versión era bajar los tiempos de una forma bestial. Para que veáis un poco lo que hicieron.

**5:33** · Aquí os he dejado una tabla con alguna de las cosas que consiguieron reducir, ¿no? Por ejemplo, el Colstar, que básicamente es el arranque frío, lo que tarda Hermes en encenderse, pues pasó de 700 milisegundos a 258, reduciéndolo en un 63%.

**5:49** · Luego las llamadas internas que hace por conversación bajaron casi la mitad, un menos 47%.

**5:56** · Luego el session search, es decir, la búsqueda en memoria, lo que le permite a la gente saber lo que he hablado contigo en conversaciones anteriores, pasó de 90 segundos a 20 milisegundos, es decir, 4500 veces más rápido. Y luego el RAN IENT EN, que es el archivo principal de la gente, lo refactorizaron de 16,000 líneas de código a 3,800, es decir, un -76%.

**6:19** · que esto realmente no no lo hace más rápido en sí, pero sí que permite que el código sea más sano y que haya menos sitios donde esconderse los bugs. Y una cosa que os recomiendo es que, bueno, creo que ahora cuando estoy grabando este vídeo ya está la 15.2, pero bueno, como mínimo utilizar la 15.1, ya que hay un bug del dashboard y con la 15.1 pues lo arregla. Pero bueno, como os he dicho, este vídeo va sobre el canvan. Yo esto lo hago para poneros en contexto.

**6:43** · Entonces, con esto lo que hicieron fue automatizar algunos procesos que antiguamente tú tenías que hacer a mano, ¿no? Por ejemplo, tenemos el comando Hermescan Bansual, que lo que permite es montar el equipo directamente. Antes cada tarjeta y cada enlace tenías que hacerlo tú manualmente. Luego está la autodescomposición, que esto está muy bien, que es como he dicho antes, tú mandabas una tarea y tú tenías que, si era una tarea muy grande, partirla en trozos pequeños y saber qué tarea pequeña tiene que ir a cada agente, ¿no?

**7:11** · Como organizar tú el canvan. Ahora con el la autodescomposición, que ahora veremos cómo se activa, ahora puedes crear una tarea más genérica o dar una idea en un apartado llamado trije. Lo puedes crear tú o lo puede crear un agente con el que tú te comuniques por Telegram o por el dashboard. Entonces va a haber un agente orquestador, el cual se va a encargar de partir esa tarea o esa idea genérica en subtareas. Y en base a los agentes que tú hayas creado, los subagentes, cada agente tendrá una descripción, pues él sabrá qué tarea mandarle a cada agente.

**7:42** · Luego también te permite él utilizar diferentes modelos para cada tarea. Por ejemplo, si quieres a lo mejor una tarea muy simple, puedes utilizar un modelo mini o nano. Y si quieres, a lo mejor, para una tarea más compleja, pues puedes utilizar un 4.8 o el 5.5. Y por último, puedes crear chrons para que se ejecuten esas tareas de forma periódica a una hora en concreto, ¿no? Pero bueno, antes de profundizar bien en lo que es la arquitectura de Canban Swarm, quiero que entendáis primero qué significa esto de Swarm, ¿no?

**8:10** · De enjambre, porque esto no es ningún invento de Hermes, esto es una arquitectura para que varios agentes trabajen juntos que se lleva utilizando desde 2024. Entonces, aquí os he puesto varias arquitecturas para trabajar con múltiples agentes. Una sería el swarm puro, que ahora explicaremos, luego el orquestador y lo que utiliza Hermes con Canvan Swarm, que realmente es una forma híbrida, no es un swarm puro.

**8:31** · Entonces, el swarm puro se llama enjambre porque tenéis que verlo como si fuera un enjambre de abejas, donde la abeja reina no es la que trabaja ni da órdenes, sino que son las abejas obreras las que se encargan de pasarse las tareas de una a otra. Esto lo popularizó Open EI con un framework llamado literalmente Swarm, que fue hace 2 años en 2024.

**8:51** · Y luego Lchain también sacó su propia versión llamada Langraph Swarm, que de hecho yo hablé de esto hace como 5 meses en un vídeo y como he dicho antes, esto sirve para que los agentes trabajen entre ellos sin necesidad de un orquestador.

**9:06** · Esto tiene sus ventajas y sus desventajas. La ventaja es que no tiene que pasar todo por un agente y es mucho más barato. La desventaja es que si tienes muchos agentes, piensa que cada abeja obrera tiene que saber cuál es el rol de las demás. Si tú tienes 10, cada una tiene que saber lo que hacen las otras 10 para que cada una pueda delegárselo a las demás. Entonces, el ejemplo que te ponen en LC Chain es, imagínate que tú tienes eh dos agentes, uno que es el experto en reservar vuelos y otro que es el experto en reservar hoteles. Entonces el usuario dice, "Oye, pues resérvame un vuelo."

**9:37** · Pues se activa el agente de vuelo y pues habla con él y le reserva el vuelo. En el momento que el cliente le pide una tarea que no tiene nada que ver con él, es decir, resérvame un hotel, pues el agente de aviones sabe que él no tiene nada que ver con hoteles y hace un handof tool traspasándole la tarea al siguiente, al agente de hoteles, y al agente de hoteles pues se encarga de reservar el hotel. Bien, pues esto es un swarm, un enjambre de agentes. Luego tenemos la arquitectura del orquestador.

**10:07** · Hay muchas más, eh, pero como no quiero que se haga muy largo este vídeo, pues he puesto estas dos. Entonces, el orquestador, que seguramente ya todos lo conocéis, pues tenemos un agente que puede ser el jefe o el orquestador, que él sabe que tiene un montón de subagentes que son expertos en cada tarea. Y cuando un usuario venga y le haga una consulta, pues él va a tener que orquestar, decidir pues a qué agente tiene que mandarle esa tarea y ya la gente se encargará.

**10:32** · Y cuando acabe el subagente de la tarea, pues la respuesta que dé se la vuelve a enviar al jefe y el jefe es el que responde al usuario final. En este caso, los workers no saben lo que hacen los demás. Son simples trabajadores que hacen lo que le manda el jefe y ya está. Entonces, cada una tiene sus ventajas y sus desventajas. Tú tienes que decidir cuándo utilizar cada una.

**10:50** · Y luego vendría Hermes con el canvan, Hermes Swarm, que ellos lo llaman Swarm, pero realmente lo llaman Swar un poco también por marketing, pero no es un swarm puro como el que hemos visto antes, pero tampoco es un orquestador porque el orquestador ya verás como se desentiende, es más un planificador.

**11:06** · Entonces, ¿cómo funciona? Bueno, pues todos tienen una pizarra o un tablero compartido que es básicamente el canvan.

**11:11** · Entonces, cuando un usuario llega, el planificador, como hemos dicho antes, va a partir la tarea en subtareas. Este planificador va a ver qué trabajadores tiene disponibles, ¿no? En base a la descripción de cada uno. Con esto creará un plan de tareas y lo que va a hacer es subirlas a la pizarra, no se las va a enviar directamente a los trabajadores.

**11:31** · Y aquí luego tenemos al gerente que hemos dicho antes, que es el dispatcher.

**11:34** · Y aquí es donde se va a encargar él de gestionar las tareas. se las enviará a cada trabajador, estará pendiente de que ninguno se quede bloqueado o falle, si falla, pues lo volverá a reintentar y luego, pues también se encargará de mover las tareas de columna en columna.

**11:48** · Entonces, como veis, no es un SW puro porque estos agentes no se pueden comunicar entre ellos tampoco. No puede enviarle este una tarea a otro, como mucho puede subir la tarea y ya veremos si el dispatcher se la encarga al siguiente, pero entre ellos no se pueden enviar tareas. Y tampoco es un orquestador porque no pasa todo por él, él solamente planifica al principio y ya se desentiende, ya solamente deja en la pizarra las tareas. Entonces es una mezcla entre uno y otro, por eso he dicho que es como híbrido. Bien, ahora vamos a lo importante, ¿no? El que hace especial a este canvan respecto a otras formas de coordinar agentes.

**12:17** · Bueno, lo primero, como he dicho antes, todo se va a guardar en una base de datos llamada SQL Lite, en concreto aquí. SQL Lite básicamente es una base datos, pero que está metida entera en un archivo de tu disco o si tienes Hermes en un VPS, pues en un VPS, ¿no? Entonces, aquí se guarda absolutamente todo. Se reparte en cinco tablas. La primera sería task, que lo que va a hacer es guardar cada tarea en una fila de tu tabla.

**12:44** · Luego tenemos links, muy importante, que la tabla se llama task links, que lo que va a hacer es que cuando una tarea dependa de varios agentes, o sea, es decir, la dependencia de padre e hijo, pues esa relación se va a guardar en una fila en esta tabla. Luego comments, cada comentario o cada traspaso que se haga, pues se guarda en una nueva fila en esta tabla de aquí. Luego tenemos la tabla task events.

**13:07** · Aquí se guarda cualquier cambio de estado que haya cuando se manda un latido con el Herbit, cuando se bloquea, cuando se completa una tarea, cuando se archiva, cuando se queda pendiente. Cualquier cambio de estado se guarda aquí. Y por último, la tabla task runs, que aquí se va a guardar cualquier intento de ejecución, tanto los logs como el código de salida y un pequeño resumen. Esto también lo vamos a poder ver desde el dashboard. Ahora veremos.

**13:32** · Entonces, lo importante de esto es que esta base datos es un archivo aparte.

**13:36** · independiente de tus conversaciones. Es decir, el historial de tu chat se guarda en un sitio aparte que el de tu tablero.

**13:42** · Esto permite que aunque tú borres tus conversaciones, apagues el servidor o pierdas la conexión, tú no vas a perder el canvan, ¿no? No vas a perder el tablero. Es, por decirlo así, como un checkpoint, se te va a quedar todo guardado para cuando vuelvas a ejecutarlo, pues siga. Entonces, ya sabemos dónde se guarda todo, ¿no?

**13:59** · Ahora, ¿cómo puedes comunicarte con ese tablero? Bueno, pues hay diferentes formas. Por un lado, los agentes se van a comunicar, como hemos visto antes, con las herramientas llamadas canvan barra baja y lo que sea. Pues aquí tienen un montón de herramientas. Canban show para que puedan mirar ellos la tarea que tienen. Canban complete para que ellos puedan completar la tarea una vez que ya crean que está acabada. Canban block para que puedan bloquearla si ven que no son capaces de hacerla y que intervenga un humano. El canbang bit, que es lo que he dicho antes, para que puedan ejecutar cada 30 segundos.

**14:28** · Lo del canvan comment, para que puedan guardar aquí lo de los comentarios.

**14:33** · Entonces, ellos van a tener múltiples herramientas para poder comunicarse con ese tablero. Lo único, como he dicho antes, que no se puede ni listar ni desbloquear tareas de otros agentes, ¿no? Solo van a poder hacerlo con sus propias tareas. Y luego pues los humanos, o sea, es decir que vas a poder comunicarte de tres maneras, una desde la terminal poniendo Hermes Canban y lo que sea, luego desde el chat, ya sea desde Telegram, Discord o el desktop que han sacado hace poco que pronto haré un vídeo con barra canvan y lo que sea.

**15:03** · Luego desde el propio dashboard que vais a ver ahora. Entonces, aquí tenemos el propio dashboard de Hermes agent. Si no sabes cómo montarlo, hace dos vídeos hice un tutorial de cómo montar Hermes y donde te dejo mi comunidad school totalmente gratuita, dos cheats sheats para que puedas levantar este dashboard como yo. Tienes el link en la descripción de este vídeo por si te quieres unir. Entonces, vamos a ver un poco qué es lo que tiene. Primero, como veis, tenemos las diferentes columnas que hemos hablado antes.

**15:26** · Entonces, lo primero es esta columna de aquí que se llama triaje, que es donde vas a subir tú cualquier idea que tengas o tú o tu agente, eh, o cualquier tarea genérica, la vas a poner aquí, ¿no? vas a dar el más y vas a crear tú la tarea. Entonces, una vez esté aquí, la va a revisar el agente orquestador que hemos visto antes, el planificador, y va a dividirlo en subtareas de forma automática, porque tenemos el orquestation auto. Entonces, con eso lo que va a hacer es enviarlas a la columna todo. ¿Dónde va a estar esperando las dependencias?

**15:57** · Que ahora veremos qué es eso. Entonces, cuando una tarea ya tiene todo listo para empezar, la manda el dispatcher a ready. Luego también tenemos esta de aquí de schédule que hemos visto antes que era para pues tareas que quieras que se ejecuten de forma periódica a una hora en concreto, ¿no? Los crons. Entonces de ready pasa a in progress. Aquí es cuando ya un agente o un subagente ha cogido la tarea y la está trabajando, ¿no? Pues vas a ver que se va a poner aquí como esta se va a poner aquí y va a estar en progreso. Y luego de progress puede ir a dos caminos.

**16:28** · Si todo ha ido bien, pues el propio agente, como hemos visto antes, con la herramienta, la marcará como hecha. Y si no, pues puede mandarla a bloqueada. Hay dos formas de que se bloquee. Una era que el propio agente la mande a bloquear con la herramienta de blocket y otra es que el dispatchet vea que está fallando, lo haya reintentado hasta llegar al límite de veces de reintento y la haya bloqueado él. Y luego, una vez hayan acabado las tareas, si quieres limpiar ya tu canvan, puedes hacer aquí darle archiv archivarla o mandarla a la papelera, ¿no? Para eliminarla.

**16:59** · Entonces, ves que tú en todo momento eh los agentes van a empezar a trabajar, pero tú puedes estar revisando aquí cómo va todo. Puedes eh ver si se ha bloqueado algo, el por qué.

**17:08** · Normalmente si lo bloquean también si lo hace la gente es porque necesita revisión humana. Entonces tienes que estar tú pendiente de cómo van trabajando, ¿no? Bien, entonces una vez explicada la teoría, ¿cómo podréis vosotros empezar a trabajar aquí en Canban y crear vuestras tareas? No, mira, lo primero que tenéis que entender es que aquí vais a tener una cosa llamada board, que son como unas pizarras donde vais a poder organizaros vuestros diferentes proyectos, ¿no?

**17:30** · Tenéis una que sería por defecto, pero luego vais a poder dándole aquí a new board y dándole a este botón de aquí vais a poder vosotros mismos crear vuestro propio board. Yo en este caso tengo aquí dos, uno para desarrollos en general y otro de radar de contenido guía. Como yo me dedico a esto, pues para estar siempre a la última de noticias de inteligencia artificial.

**17:49** · Entonces, una vez ya tenéis vuestro board o cogéis el por defecto, lo que tenéis que hacer es crear agentes. Si nos vamos aquí a Orquestation Settings, lo primero que vais a ver es que os pide un orchestator profile. En Hermes, los profiles son vuestros agentes de IA, así como lo llaman, ¿no? Entonces, aquí vosotros vais a poder crear los agentes que queráis. Esto es muy importante porque luego este orquestador va a necesitar eh agentes o subagentes para realizar la tarea, ¿no?

**18:13** · Entonces, si vosotros tenéis ya una idea de lo que queréis hacer más o menos o tenéis algún cliente o lo que sea, lo primero sería crearle un Board y una vez creado un Board, empezáis a crear los agentes que creáis que necesitáis, ¿no? Imaginaos para una página web, por ejemplo, pues podéis crear un agente para el backend, otro agente para el frontend, un agente para tema de seguridad, etcétera, ¿no?

**18:35** · Entonces, eso se hace desde aquí, desde profiles, y vais creando los diferentes agentes y le dais una descripción. Si os fijáis, aquí, por ejemplo, tenemos arquitecto software y aquí tenemos una descripción que le podemos dar nosotros manualmente o le dais a auto y la autogenera un un modelo de IA, ¿no?

**18:53** · Entonces, una vez ya tengáis vuestros agentes creados, cuando escribáis aquí una tarea, ya el orquestador va a ver todos los agentes que hay con sus descripciones y va a empezar a asignar subtareas, ¿no? Entonces, lo primero sería iros a triaje. Podéis hacerlo tanto de aquí manualmente como pedírselo a vuestro agente de Telegram. Eso lo puede hacer también él. Entonces, aquí tenéis que entender varias cosas.

**19:12** · Primero, esto es la tarea, ¿no? Aquí tú puedes poner una idea, una tarea, lo que tú quieras. Luego, esto de aquí es como el nivel de prioridad. De momento vamos a dejarlo en cero, no nos importa. Aquí es por si queréis poner skills manualmente. Si no, no pasa nada porque ya los agentes de Hermes suelen tener como 127 skills y ellos saben bien escoger cuándo necesitan cada una, no es que vean todas de golpe como en Open Cloud, por ejemplo. Luego, esto es super importante. Aquí veis que os aparecen tres pestañas: Scratch, Work y Dear.

**19:44** · Bien, esto es la carpeta donde la gente va a trabajar. Scratch es como una carpeta temporal. En cuanto acabe la tarea se elimina. Por lo tanto, si hay algo que necesitas guardarlo para después o para luego tú verlo, pues no te conviene. Ahora, para subtareas, por ejemplo, que como estas de aquí, pues eh la gente seguramente las ponga como Scratch. Luego, Wort es una copia aislada de un repositorio de Geek. Esto a lo mejor requiere un poquito más de conocimiento, pero básicamente es para cuando quieres crear varias tareas de código a la vez, pues que no se pisen unas entre otras, ¿no?

**20:11** · Y por último tendríamos esta opción de aquí, que es la más importante de todas, que se llama DI. Esto es para que tú pongas una dirección de una carpeta tuya que hayas creado, donde quieras que se guarde la tarea o el resultado de la tarea. Pero para esto vas a necesitar crear tú manualmente una carpeta. Puedes hacerlo desde la terminal o le puedes pedir a tu agente, en este caso de Telegram, que te cree la carpeta.

**20:34** · Por ejemplo, le puedes decir, "Créame una carpeta vacía en el servidor que vaya a usar como Workspace persistente para un talero de Canban en una ruta que tenga sentido y a la que el usuario Hermes, que es el usuario que yo le di, tenga permisos de escritura.

**20:49** · Cuando la tenga creada, dime la ruta exacta y comprueba que se puede escribir en ella." Y una vez hecho esto, pues como veis aquí, por hecho ruta exacta para tal y aquí te da la ruta, ¿no?

**20:58** · Entonces tú copias esta ruta y la pegarías aquí y ya está. Y aquí luego cuando acabe la tarea, el agente orquestador ve dónde tiene que guardar esa tarea final, ¿no?

**21:08** · O ese resultado. Y luego tendríamos este apartado de aquí, que eso es también muy importante, que es lo que he comentado antes de las dependencias. Esto es muy sencillo. Es básicamente que hay tareas que requieren de otras tareas para poder realizarse. Imagínate si tú tienes una subtarea, que es publicar un artículo, pero ese artículo todavía no ha sido escrito, pues esa tarea depende de la otra tarea que es escribir un artículo, ¿no? Entonces, tú aquí puedes seleccionar manualmente si esta tarea requiere de algún padre o si no, pues no pasa nada.

**21:36** · Tú pones esto aquí y luego el agente con las subtareas él se encargará de organizarlo. Por ejemplo, estas tareas que veis aquí que está en todo, están esperando dependencias. Si nos vamos aquí radar dashboard, vais a ver aquí abajo que los padres que tiene, es decir, que depende de estas tareas son estas tres y que a su vez hay cuatro tareas que son sus hijos. decir que estas cuatro tareas están esperando a que esta tarea en concreto acabe. Y todo esto lo ha construido el agente orquestador. Y ya que estamos aquí voy a explicaros algunas cosas que pueden ser interesantes, ¿no?

**22:07** · Aquí, por ejemplo, vais a ver el estatus, que está en este caso en todo, a qué agente ha sido asignado. En este caso, el agente orquestador ha asignado esta tarea a la gente de backend. Luego en Wordspace, aquí como veis pone dir, es decir que se va a guardar esta tarea en la carpeta desarrollo y luego creado por el orquestador. Luego aquí tenéis los botones por si queréis mover vosotros manualmente las tareas de columna en columna. Aquí por si queréis que os notifique cuando se haya acabado la tarea, por ejemplo, en Telegram.

**22:33** · Luego una pequeña descripción, implementar flujo de draft por canal y publicación aprobada manualmente. Aquí los padres que hemos dicho antes. Y bueno, aquí pues puedes subir algún documento, puedes incluso tú manualmente añadir algún comentario, o sea, que está muy bien, ¿no? Entonces, yo aquí, por ejemplo, creé la tarea que yo necesitaba, bueno, pues muchos agentes que estuvieran investigando tanto de LinkedIn, X, YouTube, Redit, un montón de plataformas investigaran siempre las últimas novedades. Y hay varios agentes en paralelo trabajando.

**23:04** · Y luego hay un agente que es como el que filtra qué contenido me interesa a mí en base a mis gustos o a mi canal de YouTube. Y luego una vez hecho esto, a mí me van a consultar con una lista cuáles son las noticias más relevantes y de ahí yo puedo decir, "Bueno, pues yo quiero publicar esto en LinkedIn y habrá una gente que se encarga de publicarlo en LinkedIn o yo quiero esto para un vídeo de YouTube, etcétera, ¿no? Y luego, además, todo esto se va a guardar en un dashboard donde yo voy a ir viendo las métricas, que funciona, que no funciona, y puedo ir retroalimentando a los agentes. ¿Vale? Ahora fijaos en esta tarea de aquí que pone bloqueada, ¿no?

**23:36** · Esto lo he dejado aquí durante varios días porque quiero enseñarlo en el vídeo porque creo que es muy importante, ¿no?

**23:41** · Porque esto va a hacer entender muy bien cómo funciona el canv, ¿no? Si nos metemos aquí pone que el estatus es blocked, que la tarea ha sido asignada por el de frontend desarrollando lo que sería la fase dos del dashboard.

**23:54** · Entonces, la meta es implementar un dashboard MVP humano para Alejandro, ¿no? Los padres que tiene son estos. Y si nos vamos abajo dice que esta eh acción ya requiere de una revisión manual por mí. Es decir, la tarea ha sido completada correctamente, pero esto es lo que se conoce como el human in the loop. a pesar de que está bien, me lo bloquea y la gente ha utilizado la herramienta de Blocked que he enseñado antes para que yo mismo la revise manualmente y si está bien, pues me iré aquí arriba y le daré a desbloquear o a complete, por ejemplo.

**24:27** · Y si no, pues puedo yo aquí manualmente escribir algún comentario, pues yo quiero que modifiques x cosa. Y le doy a comment.

**24:37** · Entonces, fijaos aquí, ¿no? Dice, "La revisión requiere lo de hand off y aquí te dice los archivos que han sido modificados. Y aquí te deja los comandos para que puedas tú arrancar el dashboard y verlo, ¿no? Ahora sí, por lo que sea no quieres tocar la terminal, lo mismo de siempre, tú puedes pedirle a una gente que lo haga. Y nada, esto es un poco todo. Así es como podrías trabajar con el canvam de Hermes. Yo creo que es una herramienta bastante poderosa si consigues aprender a utilizarla bien. Lo que habéis visto en este vídeo al final es un ejemplo personal mío que me sirve a mí, pero con esto prácticamente podríais montar cualquier idea que se os ocurra.

**25:08** · Por ejemplo, podríais montar un sistema que os vigile a varios clientes que tengáis a la vez y os prepare borradores de respuesta para que vosotros lo tengáis que aprobar. Eso, por ejemplo, es vendible a una empresa.

**25:19** · O podríais crear una fábrica de contenido donde tú sueltas una idea y hay agentes que investigan, otros que pueden crear el guion, otros estructuran la idea y eso le puede servir muchísimo a un montón de empresas pequeñas con el tema de marketing, que a lo mejor no se lo pueden permitir, o incluso para vuestro uso personal, agentes que estén investigando todos los días vuestro correo o lo organicen o que estén buscando ofertas de trabajo. Hay mil cosas que seguro que vosotros tenéis muchísimas ideas, que con esto podríais construir algo bastante potente. Así que nada, vamos a meterle caña a esta herramienta que la veo muy poderosa.

**25:51** · Cualquier duda que tengáis o cualquier idea me lo podéis poner en los comentarios o en la comunidad school que trataré de responderos lo antes posible.

**25:58** · Nada, como siempre, si os ha gustado este vídeo os ha aportado algo de valor, os agradecería un like y una suscripción, que a mí me ayuda muchísimo a seguir trayendo este tipo de contenido.