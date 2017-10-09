---
title: aaaIntroduction toomicroservices en Azure | Documentos de Microsoft
description: "Información general sobre por qué es importante para el desarrollo de aplicaciones modernas de creación de aplicaciones de nube con un enfoque microservicios y cómo Azure Service Fabric proporciona una plataforma tooachieve esto."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: fae2be85-0ab4-4cd3-9d1f-e0d95fe1959b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell
ms.openlocfilehash: b11920b9105e7575390e8fcf0d1ef6ab3c632978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="why-a-microservices-approach-toobuilding-applications"></a>¿Por qué un microservicios enfocar toobuilding aplicaciones?
La forma en que los desarrolladores de software nos planteamos la factorización de una aplicación en sus distintos componentes no es nueva en absoluto. Es paradigma central de Hola de orientación a objetos y abstracciones de software, creación de componentes. En la actualidad, esta descomposición en factores tiende tootake Hola formada por clases e interfaces entre las bibliotecas compartidas y capas de tecnología. Normalmente, se emplea un enfoque con niveles con un almacén en el back-end, lógica de negocios en el nivel intermedio y una interfaz de usuario (IU) en el front-end. ¿Qué *tiene* cambia a lo largo Hola últimos años es que, como los desarrolladores, estamos creando aplicaciones de nube de hello distribuidas y controlado por business Hola.

cambiantes necesidades del negocio Hola son:

* Un servicio que se compila y se aplica en los clientes de tooreach de escala en regiones geográficas nuevo (por ejemplo).
* Entrega más rápida de características y capacidades toobe toorespond puede toocustomer las demandas de forma ágil.
* Costos de tooreduce de utilización de recursos mejorado.

Todas estas necesidades afectan a la *forma* en que se crean las aplicaciones.

Para obtener más información sobre el enfoque de Hola de toomicroservices de Azure, lea [Microservicios: una revolución de aplicación con la tecnología de nube de hello](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/).

## <a name="monolithic-vs-microservice-design-approach"></a>Enfoque de diseño monolítico en comparación con el de microservicios
Todas las aplicaciones evolucionan con el tiempo. Aplicaciones de éxito evolucionan por ser toopeople útil. Las que fracasan no evolucionan y terminan por entrar en desuso. Hola cuestión es: Cuánto ¿sabe acerca de los requisitos de hoy en día y cuál será en hello futuras? Por ejemplo, supongamos que está creando una aplicación de informes para un departamento. Estás seguro de que la aplicación hello sigue estando ámbito Hola de su empresa y que Hola informes son de corta duración. La elección del enfoque es diferente, por ejemplo, creando un servicio que ofrece vídeo tootens contenido de millones de clientes. 

A veces, obtener algo puerta hello como prueba de concepto es un factor determinante hello, mientras que sabe que aplicación hello puede volver a diseñar más adelante. No tiene mucho sentido volcarse en la ingeniería de algo que no se va a usar nunca. Su saludo habitual ingeniería ventajas y desventajas. En Hola otra parte, cuando las empresas hablar sobre la compilación de hello en la nube, la expectativa de hello es crecimiento y uso. problema de Hello es que el crecimiento y la escala son imprevisibles. Nos gustaría toobe puede tooprototype rápidamente sabiendo también que se encuentran en un toodeal de ruta de acceso con éxito en el futuro. Se trata de enfoque de inicio eficiente de hello: compilar, medir, aprender y recorrer en iteración.

Durante la época de cliente-servidor de hello, se solían toofocus sobre la creación de aplicaciones en capas mediante el uso de tecnologías específicas en cada nivel. término de Hello *monolítico* aplicación ha surgido de estos enfoques. interfaces de Hello tendía toobe entre las capas de Hola y un diseño más estrechamente acoplado se usó entre componentes dentro de cada nivel. Los desarrolladores diseñaban y generaban clases compiladas en bibliotecas y las vinculaban entre sí en algunos archivos ejecutables y DLL. 

Hay ventajas toosuch un enfoque de diseño monolítico. A menudo resulta más sencillo toodesign y tiene más rápida de las llamadas entre componentes, debido a que estas llamadas suelen ser sobre la comunicación entre procesos (IPC). Además, todos los usuarios prueba un solo producto, que suele toobe más personas recursos eficaz. el inconveniente de Hello es que hay un acoplamiento robusto entre las capas en capas, y no se puede escalar los componentes individuales. Si necesita tooperform correcciones o actualizaciones, deberá toowait para que otros usuarios toofinish sus pruebas. Es más difícil toobe agile.

Microservicios solucionar estas desventajas y más estrecha colaboración con hello anterior requisitos empresariales, pero también tienen ventajas y pasivos. Estas son las ventajas de Hola de microservicios que cada uno de ellos normalmente encapsula la funcionalidad empresarial más sencilla, que escale hacia arriba o hacia abajo, hacia la prueba, implementar y administrar de forma independiente. Una ventaja importante de un enfoque de microservicio es que los equipos están determinados más escenarios empresariales que por tecnología, que Hola enfoque en capas anima. En la práctica, los equipos más pequeños desarrollan un microservicio en función de un escenario del cliente y usan las tecnologías que prefieren. 

En otras palabras, organización de hello no necesita que las aplicaciones de microservicio de toostandardize tech toomaintain. Equipos individuales que propios servicios pueden hacer lo que tiene sentido para ellos en función de la experiencia de equipo o cuál es el problema de hello toosolve más adecuado. En la práctica, es preferible tener un conjunto de tecnologías recomendadas, como un almacén NoSQL o un marco de aplicaciones web concretos.

inconveniente Hola de microservicios incluye en la administración de hello mayor número de entidades independientes y trabajar con control de versiones y las implementaciones más complejos. Aumenta el tráfico de red entre hello microservicios, así como las latencias de red correspondiente Hola. Una gran cantidad de servicios granulares comunicándose entre sí no trae nada bueno para el rendimiento. Sin toohelp de herramientas ver estas dependencias, resulta difícil demasiado "ver" sistema completo de Hola. 

Estándares que el enfoque de microservicio Hola funcione por otorgar en cómo toocommunicate y que se va a tolerante a errores de cosas de hello solo se necesita desde un servicio, en lugar de contratos rígidos. Es importante toodefine de diseño por adelantado estos contratos en hello, porque servicios actualización independientemente entre sí. Otra descripción acuñada para el diseño con el enfoque de microservicios es "arquitectura orientada a servicios (SOA) específica".

***En su forma más sencilla, hello microservicios enfoque de diseño es sobre una federación de servicios, con los cambios independientes efectuados tooeach y acordado según los estándares para la comunicación desacoplada.***

Se generan más aplicaciones en la nube, personas descubre que esta descomposición de hello general aplicaciones en servicios independientes, centrada en el escenario es un enfoque mejor a largo plazo.

## <a name="comparison-between-application-development-approaches"></a>Comparación entre los enfoques de desarrollo de aplicaciones
![Desarrollo de aplicaciones de la plataforma Service Fabric][Image1]

1) Las aplicaciones monolíticas contienen funciones específicas del dominio y normalmente se dividen en capas funcionales, como Web, negocios y datos.

2) Para escalar aplicaciones monolíticas, es preciso clonarlas en varios servidores, máquinas virtuales o contenedores.

3) Las aplicaciones de microservicios separan las funciones en servicios más pequeños independientes.

4) Hello microservicios enfoque escalas horizontal mediante la implementación de cada servicio por separado, crear instancias de estos servicios a través de máquinas virtuales o de servidores y contenedores.

Diseñar con un microservicio enfoque no es una panacea para todos los proyectos, pero está alineado más estrechamente con los objetivos de negocio de Hola que se ha descrito anteriormente. A partir de un enfoque monolítico podría ser aceptable si sabe que tenga código de hello oportunidad toorework hello más tarde en un diseño de microservicios. Normalmente, comenzar con una aplicación monolítica y lenta divide en fases, a partir de las áreas funcionales Hola que necesitan toobe más escalable o ágil.

toosummarize, hello microservicio consiste toocompose la aplicación de muchos servicios pequeños. Servicios de Hola se ejecutan en contenedores que se implementan en un clúster de máquinas. Los equipos más pequeños desarrollar un servicio que se centra en un escenario y comprobar de forma independiente, versión, implementación y escalar cada servicio para que toda la aplicación hello puede evolucionar.

## <a name="what-is-a-microservice"></a>¿Qué es un microservicio?
Hay distintas definiciones de microservicios. Si desea buscar Hola Internet, encontrará muchos recursos útiles que proporcionan sus propios puntos de vista y definiciones. Sin embargo, la mayoría de hello siguiendo las características de microservicios ampliamente acordada:

* Encapsulan un escenario de cliente o negocio. ¿Cuál es el problema de Hola que va a resolver?
* Desarrollados por un pequeño equipo de ingenieros.
* Escritos en cualquier lenguaje de programación y usando cualquier marco.
* Constan de código y, opcionalmente, de un estado, ambos de los cuales se controlan para versiones, implementan y escalan de forma independiente.
* Interactúan con otros microservicios a través de protocolos e interfaces bien definidos.
* Tener nombres únicos (URL) usa tooresolve su ubicación.
* Siguen siendo coherentes y están disponibles en presencia de Hola de errores.

Puede resumir estas características en:

***Las aplicaciones de microservicios se componen de servicios pequeños centrados en el cliente, escalables y con control de versiones independiente que se comunican entre sí mediante protocolos estándar con interfaces bien definidas.***

Hemos aprendido primero dos puntos de hello en la sección anterior de Hola y ahora se desarrollan y aclaran Hola a otros usuarios.

### <a name="written-in-any-programming-language-and-use-any-framework"></a>Escritos en cualquier lenguaje de programación y usando cualquier marco
Como los desarrolladores, deberíamos estar libre toochoose un idioma o el marco de trabajo que prefiera, según nuestras necesidades de hello del servicio de Hola o conocimientos. En algunos servicios podrían valor ventajas de rendimiento de Hola de C++ por encima de todo. En otros servicios, facilidad de Hola de desarrollo administrado en C# o Java podría ser más importante. En algunos casos, quizás necesite toouse una biblioteca de socio específico, tecnología de almacenamiento de datos, o medios de exponer Hola tooclients de servicio.

Una vez que haya elegido una tecnología, llega toohello operativa o la administración del ciclo de vida y la escala de servicio de Hola.

### <a name="allows-code-and-state-toobe-independently-versioned-deployed-and-scaled"></a>Permite toobe código y estado de forma independiente con control de versiones, implementar y escalar
Sin embargo decide toowrite su microservicios, código de hello y, opcionalmente, Hola estado debe independientemente implementar, actualizar y escalar. Realmente es una de hello toosolve de problemas sea más difícil, porque se trata de elección de tooyour de tecnologías. Para ajustar la escala, es difícil entender cómo toopartition (o partición) ambos Hola código y estado. Cuando el código de hello y estado usan tecnologías diferentes, lo cual es común hoy en día, los scripts de implementación de Hola para su microservicio deberán toobe toocope pueda con ajuste de escala en ambos. También se trata acerca de la agilidad y flexibilidad, por lo que puede actualizar algunos de hello microservicios sin necesidad de tooupgrade todas ellas a la vez.

Devolver toohello monolítico en comparación con el enfoque de microservicio durante un momento, hello siguiente diagrama muestra las diferencias de hello en estado de toostoring de enfoque de Hola.

#### <a name="state-storage-between-application-styles"></a>Almacenamiento de estado en los distintos estilos de aplicación
![Almacenamiento de estados de la plataforma Service Fabric][Image2]

***método monolítico de Hola Hola izquierda tiene una sola base de datos y las capas de tecnologías específicas.***

***enfoque de microservicios Hello en hello derecho ha toohello microservicio de ámbito de un gráfico de microservicios interconectados donde suele ser estado y se usan varias tecnologías.***

Por lo general en un enfoque monolítico, aplicación hello usa una sola base de datos. ventaja de Hello es que es una ubicación única, lo que resulta fácil toodeploy. Cada componente puede tener una sola tabla toostore su estado. Los equipos tengan toostrictly estado independiente, que es un desafío. Inevitablemente hay temptations tooadd una nueva columna tooan existente tabla de clientes, realice una combinación entre tablas y crear dependencias en la capa de almacenamiento de Hola. Tras esto, no es posible escalar los componentes individuales. 

En el enfoque de microservicios hello, cada servicio administra y almacena su propio estado. Cada servicio es responsable de ajuste de escala en código y estado toomeet juntos hello las peticiones de servicio de Hola. Un inconveniente es que cuando hay una necesidad toocreate vistas o consultas, de los datos de aplicación, deberá tooquery en estado diversos almacenes. Por lo general, esto se resuelve teniendo un microservicio independiente que genera una vista de una colección de microservicios. Si necesita varias consultas ocasionales en datos de hello tooperform, debe considerar cada microservicio escribiendo su servicio almacenamiento de datos tooa datos para el análisis sin conexión.

Control de versiones es la versión de toohello específica implementada de un microservicio así que varias versiones diferentes, implementar y ejecutar en paralelo. Control de versiones describen escenarios de Hola donde una versión más reciente de un microservicio se produce un error durante la actualización y debe tooroll atrás tooan versión anterior. Hello otro escenario para el control de versiones está realizando A/B-estilo pruebas, donde varios usuarios experimentan diferentes versiones del servicio de Hola. Por ejemplo, es común tooupgrade un microservicio para un conjunto específico de la nueva funcionalidad de los clientes tootest antes de distribuirla más ampliamente. Después de la administración del ciclo de vida de microservicios, ahora esto nos lleva toocommunication entre ellos.

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>Interactúan con otros microservicios por medio de protocolos e interfaces bien definidos.
En este tema se necesita poca atención aquí, porque extensa documentación acerca de la arquitectura orientada a servicios que se ha publicado en hello últimos 10 años, describe los patrones de comunicación. Por lo general, comunicación del servicio utiliza un enfoque REST con los protocolos HTTP y TCP y XML o JSON como formato de serialización de Hola. Desde una perspectiva de la interfaz, es sobre la adopción de enfoque de diseño de hello web. No obstante, no hay nada que le impida usar protocolos binarios o sus propios formatos de datos. Prepárese para personas toohave uno sea más difícil utilizando su microservicios si se trata de código abierto disponibles.

### <a name="has-a-unique-name-url-used-tooresolve-its-location"></a>Con un nombre único (URL) usa tooresolve su ubicación
¿Recuerda cómo que seguimos diciendo que el enfoque de microservicio de hello es como hello web? Al igual que hello web, su microservicio necesita toobe direccionable siempre que se está ejecutando. Si piensa en las máquinas y en cuál de ellas se ejecuta un microservicio concreto, las cosas empeoran rápidamente. 

Hola mismo modo que DNS resuelve un equipo determinado de tooa de dirección URL determinado, el microservicio debe toohave un nombre único para que su ubicación actual sea reconocible. Microservicios necesitan nombres direccionables que hacer que sean independientes de infraestructura de Hola que se ejecutan en. Esto implica que hay una interacción entre cómo se implementa el servicio y cómo se detecta, porque es necesario toobe un registro de servicio. De igual forma, cuando se produce un error en un equipo, servicio de registro de hello debe indicar que el servicio de saludo se está ejecutando. 

Esto nos lleva toohello siguiente tema: resistencia y la coherencia.

### <a name="remains-consistent-and-available-in-hello-presence-of-failures"></a>Sigue siendo coherente y está disponible en presencia de Hola de errores
Tratar errores inesperados es uno de hello toosolve de problemas más difícil, especialmente en un sistema distribuido. Gran parte del código de hello que se escribe como a los desarrolladores es controlar las excepciones, y también es donde hello mayor parte del tiempo se invierte en la prueba. problema de Hello es más complicado que escribir código toohandle errores. ¿Qué ocurre cuando se produce un error en la máquina de Hola donde se está ejecutando hello microservicio? No sólo debe toodetect este error de microservicio (un problema de disco duro en su propio), pero también necesita algo toorestart su microservicio. 

Un microservicio toobe resistente toofailures es necesario y reiniciar a menudo en otro equipo por motivos de disponibilidad. Esto también incluye hacia abajo el estado de toohello que se guardó en nombre de microservicio hello, donde hello microservicio puede recuperar este estado de, y si microservicio hello es capaz de toorestart correctamente. En otras palabras, necesita resistencia toobe en proceso hello (Hola reinicios del proceso), así como resistencia en estado de Hola o de datos (ningún dato de hello y pérdida de datos siga siendo coherente).

problema de Hola de resistencia se agrava durante otros escenarios, como cuando se producen errores durante la actualización de la aplicación. Hello microservicio, trabajar con el sistema de implementación de hello, no necesita toorecover. También debe toothen decidir si puede continuar la versión más reciente de toomove toohello hacia delante o en su lugar revertir tooa anterior versión toomaintain un estado coherente. Preguntas frecuentes como si son suficientes máquinas disponible tookeep avanzando y cómo toorecover las versiones anteriores de hello microservicio necesitan toobe considera. Para ello, hello microservicio tooemit mantenimiento información toobe toomake capaz de estas decisiones.

### <a name="reports-health-and-diagnostics"></a>Notifica el estado y diagnósticos
Aunque pueda parecer obvio y a menudo se pase por alto, un microservicio debe informar sobre su mantenimiento y diagnóstico. De lo contrario, hay poca información desde la perspectiva de las operaciones. Establecer correlaciones entre eventos de diagnóstico a través de un conjunto de servicios independientes y afrontar inclinaciones de reloj del equipo resulta difícil toomake sentido del orden de eventos de Hola. Hola da formato igual que interactúen con un microservicio sobre acordado protocolos y los datos, se convierte en una necesidad para la estandarización en cómo almacenan toolog estado y eventos de diagnóstico que en última instancia terminan en un evento de consulta y ver. En un enfoque de microservicios, es fundamental que los diferentes equipos acuerden un único formato de registro. Es necesario toobe un enfoque coherente tooviewing los eventos de diagnóstico en la aplicación hello como un todo.

El estado es diferente de los diagnósticos. Estado trata microservicio Hola reporting sus acciones adecuado de tootake de estado actual. Un buen ejemplo funciona con la disponibilidad de toomaintain de mecanismos de actualización e implementación. Aunque un servicio puede ser incorrecto debido tooa bloqueo del proceso o reinicio del equipo, servicio de hello todavía podría estar operativa. Hola última cosa que necesita es toomake este empeoran realizando una actualización. Hola más recomendable es toodo una investigación en primer lugar o deje tiempo para hello microservicio toorecover. Los eventos de mantenimiento de un microservicio permiten tomar decisiones fundamentadas y, de hecho, ayudan a crear servicios de recuperación automática.

## <a name="service-fabric-as-a-microservices-platform"></a>Service Fabric como plataforma de microservicios
Azure Service Fabric surgido desde una transición por Microsoft de entrega de productos de cuadro, que son normalmente monolíticos en estilo, toodelivering servicios. experiencia de Hola de generar y utilizar servicios de gran tamaño, como la base de datos de SQL Azure y base de datos de Cosmos de Azure, en forma de Service Fabric. plataforma de Hola evolucionado con el tiempo, tal y como se hayan adoptado servicios cada vez más. Lo que es importante, Service Fabric tenía toorun no solo en Azure, sino también en las implementaciones de Windows Server independiente.

***objetivo de Hola de Service Fabric es toosolve problemas de disco duro de Hola de compilar y ejecutar un servicio y utilizar recursos de la infraestructura de forma eficaz, para que los equipos pueden resolver problemas empresariales con un enfoque de microservicios.***

Service Fabric proporciona tres toohelp áreas generales al crear aplicaciones que utilizan un enfoque de microservicios:

* Una plataforma que proporciona toodeploy de servicios del sistema, actualizar, detectar y reiniciar servicios de errores, detectar los servicios, enrutar los mensajes, administrar el estado y supervisar el estado. Estos servicios del sistema en vigor permiten muchas de las características de Hola de microservicios descrito anteriormente.
* Procesa ejecutándose en contenedores o como de las aplicaciones de toodeploy de capacidad. Service Fabric es un organizador de contenedores y proceso.
* API de programación productivas, toohelp compilar aplicaciones como microservicios: [principal de ASP.NET, Reliable Actors y servicios de confianza](service-fabric-choose-framework.md). Puede elegir cualquier código toobuild su microservicio. Pero estas API realizar trabajo hello más sencillo, y que se integran con la plataforma de hello en un nivel más profundo. Por ejemplo, con ellas es posible obtener información de estado y de diagnóstico, o se puede aprovechar la alta disponibilidad integrada.

***Service Fabric es independiente de la forma en que cree el servicio y permite usar cualquier tecnología. Sin embargo, proporcionan las API de programación integradas que hacen que sea más fácil microservicios toobuild.***

### <a name="migrating-existing-applications-tooservice-fabric"></a>Migrar existente de las aplicaciones tooService tejido
Un tejido de enfoque clave tooService es tooreuse código existente, que, a continuación, se y modernizado con microservicios nuevo. Existen cinco fases tooapplication modernización, y puede iniciar y detener en cualquiera de las fases de Hola. Las fases son:

1) Adopción de una aplicación monolítica tradicional
2) Elevación y MAYÚS - Use contenedores o código de invitado ejecutables toohost existente de Service Fabric.
3) Modernización: se agregan nuevos microservicios con código existente en contenedores. 
4) Innovar - interrumpir Hola monolítico microservicios puramente según las necesidades del.
5) Se transforma en microservicios - transformación Hola de monolíticas aplicaciones existentes o crear nuevas aplicaciones virgen.

![TooMicroservices de migración][Image3]

Es importante tooemphasis nuevo, que puede **iniciar y detener en cualquiera de estas fases**, no nos vemos obligados toomoved toohello siguiente fase. Veamos ahora ejemplos de cada una de las fases.

**Levantar y mover** : se levantar el gran número de compañías y desplazar las aplicaciones existentes de monolíticas en contenedores toofor dos razones;

- Reducción de costes ya sea debido tooconsolidation y eliminación de las aplicaciones existentes de hardware o de ejecución en una mayor densidad. 
- Contrato de implementación coherente entre el desarrollo y las operaciones.

Reducción de costos es comprensibles y dentro de Microsoft está siendo gran número de aplicaciones existentes en contenedores simplemente toomillions de dólares. Implementación coherente es más difícil tooevaluate, pero igualmente importante. Dice que los desarrolladores todavía pueden ser libre toochoose Hola tecnología que se adapte usarlas, sin embargo, las operaciones de hello sólo aceptará un toodeploy de manera única y administrar estas aplicaciones. Fin a las operaciones de Hola de tener toodeal con la complejidad de Hola de las muchas tecnologías diferentes o forzar a los desarrolladores tooonly elegir algunas excepciones. Básicamente, cada aplicación se convierte en un contenedor de imágenes de implementación independientes.

Muchas organizaciones se detienen aquí. Ya tienen ventajas Hola de contenedores y Service Fabric proporciona la experiencia de administración completa de Hola de implementación, actualizaciones, control de versiones, reversiones, etcetera de supervisión de estado.

**Modernización** -es Hola adición de nuevos servicios junto con el código existente en contenedores. Si va toowrite nuevo código, es mejor toodecide tootake pequeños pasos hacia abajo de la ruta de acceso de hello microservicios. Esto podría ser agregar un nuevo punto de conexión de la API de REST o una nueva lógica de negocios. De esta manera, primero en viaje Hola de microservicios nueva creación y prácticas de desarrollo y su implementación.

**¿Innovar** -recordar esas original cambiantes necesidades empresariales en el inicio de Hola de este artículo, que imponen enfoque de hello microservicios? En este Hola de fase es decisión, se encuentran estas ocurra toomy la aplicación actual y si es así, necesito toostart dividir monolito Hola o innovación. Un ejemplo sería una base de datos que se convierte en un cuello de botella de procesamiento porque se usa como cola de flujo de trabajo. Como el número de Hola de flujo de trabajo solicita aumentar Hola trabajo toobe necesidades distribuida para la escala. Por lo tanto de esa determinada aplicación Hola que no se ajuste de escala, o si necesita tooupdate más con frecuencia, este comando dividen un microservicio e innovación. 

**Transformación en microservicios**: aquí es dónde la aplicación se compone de (o descompone en) microservicios. tooreach aquí, ha realizado el viaje de microservicios Hola. Puede iniciar aquí, pero toodo esto sin un toohelp de plataforma microservicios es una importante inversión. 

### <a name="are-microservices-right-for-my-application"></a>¿Son los microservicios adecuados para mi aplicación?
Es posible. ¿Qué experimentamos era que como toobuild para la nube de Hola por razones comerciales que empieza en más equipos de Microsoft, muchos de ellos producidas ventajas de Hola de adoptar un enfoque similar a microservicio. Por ejemplo, Bing lleva años desarrollando microservicios para búsqueda. Para otros equipos, era nuevo enfoque de microservicios Hola. Los equipos encontraron que había problemas de disco duro toosolve fuera de sus áreas centrales de seguridad de. Se trata de por qué Service Fabric ganado fuerza como tecnología de Hola de elección para compilar servicios.

objetivo de Hola de Service Fabric es tooreduce complejidades de hello de la creación de aplicaciones con un enfoque de microservicio, para que no tenga toogo a través como rediseña muchas costosa. Empiece poco a poco, escalar cuando sea necesario, dejar de utilizar servicios, agregar otros nuevos y evolucionan con cliente uso es el enfoque de Hola. También sabemos que muchos otros problemas todavía hay toobe resuelve toomake microservicios sea más accesible para la mayoría de los desarrolladores. Contenedores y modelo de programación de actor Hola son ejemplos de pequeños pasos en esa dirección, y se está seguro de que las innovaciones más surgirán toomake esto sea más fácil.
 
<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Pasos siguientes
* [Información general sobre la terminología de Service Fabric](service-fabric-technical-overview.md)
* [Microservicios: Una revolución de aplicación con la tecnología de nube de Hola](https://azure.microsoft.com/en-us/blog/microservices-an-application-revolution-powered-by-the-cloud/)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png
