# <a name="internet-of-things-security-architecture"></a>Arquitectura de seguridad de Internet de las cosas
Al diseñar un sistema, es importante toounderstand las amenazas potenciales de hello toothat sistema y agregar las defensas adecuadas según corresponda, como sistema de hello está diseñado y está diseñado. Es especialmente importante toodesign Hola producto desde el principio de hello teniendo en cuenta la seguridad debido a que comprender cómo un atacante podría ser capaz de toocompromise un sistema de ayuda a asegurarse de que las mitigaciones adecuadas están en vigor desde el principio de Hola. 

## <a name="security-starts-with-a-threat-model"></a>La seguridad comienza con un modelo de riesgos
Microsoft tiempo ha utilizado el modelos de amenazas para sus productos y realizó disponible públicamente del proceso de modelado de amenazas de la compañía de Hola. Hello experiencia de la empresa que presenta la modelización Hola inesperados ventajas más allá de hello inmediata de comprender de qué amenazas son Hola relativas a la mayoría. Por ejemplo, también crea una vía en una mesa redonda con otros usuarios fuera de equipo de desarrollo de hello, lo cual puede conducir toonew ideas y mejoras en el producto de Hola.

objetivo de Hello del modelado de amenazas es toounderstand cómo un atacante podría ser capaz de toocompromise un sistema y, a continuación, asegúrese de que las mitigaciones adecuadas están en vigor. Modelado de amenazas fuerza las mitigaciones tooconsider de equipo de diseño de hello tal y como se ha diseñado el sistema de hello en lugar de después de implementar un sistema. Este hecho es muy importante, porque la retroadaptados tooa infinidad de defensas de seguridad de dispositivos en el campo de hello es factible, es propensa a errores y dejará los clientes en peligro.

Muchos equipos de desarrollo es un excelente trabajo capturar requisitos funcionales hello para el sistema de Hola que benefician a los clientes. Sin embargo, la identificación de formas no son evidentes que alguien puede hacer un mal uso sistema hello es más complejo. El modelado de riesgos puede ayudar a los equipos de desarrollo a conocer lo que podría hacer un atacante, y por qué. Modelado de amenazas es un proceso estructurado que crea un debate sobre seguridad de hello las decisiones de diseño en el sistema de hello, así como el diseño de toohello cambios realizados por el camino de Hola que afectar a la seguridad. Aunque un modelo de amenazas es simplemente un documento, esta documentación también representa una forma ideal de continuidad tooensure de conocimiento, retención de lecciones aprendidas y ayuda nuevo equipo incorporar rápidamente. Por último, un resultado del modelado de amenazas es tooenable tooconsider otros aspectos de seguridad, por ejemplo, ¿qué compromisos de seguridad que se va tooprovide tooyour clientes. Estos compromisos, junto con el modelado de riesgos, controlarán su solución de Internet de las cosas e informarán sobre la misma.

### <a name="when-toothreat-model"></a>Cuando el modelo de toothreat
[Modelado de amenazas](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) ofertas Hola valor más grande si se incorpora en la fase de diseño de Hola. Cuando está diseñando, tendrá Hola mayor flexibilidad toomake cambios tooeliminate amenazas. Lo que elimina las amenazas por cuestiones de diseño es el resultado deseado de Hola. Este método es mucho más fácil que agregar mitigaciones, probarlas y asegurarse de que siempre están actualizadas; además, su eliminación no siempre es posible. Resulta más difícil tooeliminate amenazas como un producto pasa a ser más maduran y a su vez en última instancia necesitará más trabajo y compensaciones mucho más difíciles que el modelo desde el principio en el desarrollo de Hola de amenazas.

### <a name="what-toothreat-model"></a>¿Qué modelo toothreat
Debe subproceso solución Hola de modelo como un conjunto y también se centran en hello siguientes áreas:

* características de seguridad y privacidad de Hola
* características de Hello cuyos errores están relacionados con la seguridad
* características de Hola que tocan un límite de confianza 

### <a name="who-threat-models"></a>Quién debe crear modelos de riesgos
El modelado de riesgos es un proceso como cualquier otro.  Es un documento de modelo de amenaza de buena idea tootreat hello como cualquier otro componente de solución de Hola y validarla. Muchos equipos de desarrollo es un excelente trabajo capturar requisitos funcionales hello para el sistema de Hola que benefician a los clientes. Sin embargo, la identificación de formas no son evidentes que alguien puede hacer un mal uso sistema hello es más complejo. El modelado de riesgos puede ayudar a los equipos de desarrollo a conocer lo que podría hacer un atacante, y por qué.

### <a name="how-toothreat-model"></a>¿Cómo toothreat modelo
proceso de modelado de amenazas de Hola se componen de cuatro pasos. Hola pasos son:

* Aplicación hello modelo
* Enumerar las amenazas
* Mitigar las amenazas
* Validar las mitigaciones Hola

#### <a name="hello-process-steps"></a>pasos del proceso de Hola
Tres reglas generales tookeep en cuenta al crear un modelo de amenazas:

1. Cree un diagrama de la arquitectura de referencia. 
2. Inicie la búsqueda en anchura. Obtener una visión general y comprender el sistema de Hola como un todo, antes de entrar en profundidad.  Esto permite garantizar que se inmersión en hello derecho vuelve a realizar.
3. Unidad de proceso de hello, no permita que el proceso de hello unidad se. Si se detecta un problema en la fase de modelado de Hola y desea tooexplore lo, vaya para él.  No cree que necesita toofollow ciegamente estos pasos.  

#### <a name="threats"></a>Amenazas
Hola cuatro núcleos elementos de un modelo de amenazas son:

* Procesos (servicios web, servicios Win32, demonios * nix, etc.). Tenga en cuenta que algunas entidades complejas (por ejemplo, sensores y puertas de enlace de campo) se pueden resumir como procesos cuando no es posible explorar estas áreas en profundidad.
* Almacenes de datos (todos los lugares donde se almacenan los datos, como un archivo de configuración o una base de datos)
* Flujo de datos (que mueven datos entre los otros elementos de la aplicación hello)
* Las entidades externas (todo lo que interactúa con el sistema de hello, pero no está bajo control de Hola de aplicación hello, algunos ejemplos son los usuarios y las fuentes de satélite)

Todos los elementos en el diagrama de arquitectura de hello son las amenazas de toovarious de asunto; se usará la tecla de acceso de hello STRIDE. Lectura [de modelado de amenazas nuevo, STRIDE](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) tooknow más información acerca de los elementos del intervalo de saludo.

Diferentes elementos del diagrama de aplicaciones de hello son amenazas STRIDE toocertain asunto:

* Los procesos son tooSTRIDE de asunto
* Flujos de datos están tooTID de asunto
* Almacenes de datos son tooTID de asunto y a veces R, si los almacenes de datos de hello son archivos de registro.
* Las entidades externas son tooSRD de asunto

## <a name="security-in-iot"></a>Seguridad de IoT
Dispositivos conectados de propósito especial tienen un número importante de posibles áreas de superficie de interacción y patrones de interacción, todos ellos deben tener en cuenta tooprovide un marco para proteger el acceso digital toothose dispositivos. término de Hola "digital access" es usado aquí toodistinguish de las operaciones que se llevan a cabo a través de la interacción directa de dispositivos donde se proporciona seguridad de acceso a través del control de acceso físico. Por ejemplo, colocar dispositivo hello en una sala con un bloqueo en puerta de Hola. Mientras no se puede denegar el acceso físico con el software y hardware, se pueden tomar medidas tooprevent acceso físico de los principales toosystem interferencias. 

A medida que exploramos patrones de interacción de hello, veremos "control de dispositivo" y "datos del dispositivo" con Hola de mismo nivel de atención. "Control de dispositivo" se puede clasificar como cualquier información que se proporciona tooa dispositivo por cualquier entidad con el objetivo de Hola de cambiar o influir en su comportamiento hacia su estado u Hola de su entorno. "Datos del dispositivo" se pueden clasificar como cualquier información que un dispositivo emite tooany otra parte sobre su estado y Hola observadas el estado de su entorno.

En orden toooptimize recomendaciones de seguridad, se recomienda que una arquitectura típica de IoT dividirse en varias zonas/de componente como parte del ejercicio de modelado de amenazas de Hola. Dichas zonas se describen con detalle en esta sección e incluyen:

* Dispositivo,
* Puerta de enlace de campo,
* Puertas de enlace en la nube y
* Servicios.

Las zonas son amplias forma toosegment una solución; cada zona a menudo tiene sus propios requisitos de datos y la autenticación y autorización. Las zonas también pueden ser tooisolation usado dañar y restringir el impacto de Hola de zonas de confianza baja en zonas de confianza superior.

Cada zona se separa con un límite de confianza, que se indica como Hola decimal con punto de la línea roja en el siguiente diagrama de Hola. Representa una transición de datos o información de un origen tooanother. Durante esta transición, Hola datos/información podría estar sujeto tooSpoofing, alteración de datos, rechazo, divulgación de información, denegación de servicio y elevación de privilegios (intervalo).

![Zonas de seguridad de IoT](media/iot-security-architecture/iot-security-architecture-fig1.png) 

Hello componentes representados en cada límite también están sometido tooSTRIDE, lo que permite una completa 360 vista de solución de Hola de modelado de amenazas. Hola las siguientes secciones se elaboran en cada uno de los componentes de Hola y preocupaciones concretas de seguridad y las soluciones que deben colocarse en su lugar.

secciones de Hola que sigue tratarán los componentes estándar que normalmente se encuentran en estas zonas.

### <a name="hello-device-zone"></a>Hola zona del dispositivo
entorno del dispositivo Hello es espacio físico inmediata de hello alrededor de dispositivo de Hola donde el acceso físico o digital de peer-to-peer "red local" tener acceso a toohello dispositivo es factible. Se supone que una "red local" toobe una red que es distinta y aislada: pero potencialmente conectados de Internet pública demasiado: Hola e incluye cualquier tecnología inalámbrica de corto alcance que permite la comunicación punto a punto de dispositivos. Lo hace *no* incluyen cualquier tecnología de virtualización de red creando ilusión de Hola de dicha red local y también incluye redes de operador público que requieren cualquier toocommunicate dos dispositivos a través del espacio de red pública Si se hubieran relación de comunicación tooenter punto a punto.

### <a name="hello-field-gateway-zone"></a>Hola zona de puerta de enlace de campo
Una puerta de enlace de campo es un dispositivo (o aparato) o un software de equipo servidor de uso general que actúa como habilitador de comunicaciones y, potencialmente, como sistema de control de dispositivos y centro de procesamiento de datos de dispositivos. zona de puerta de enlace de campo de Hola Hola campo puerta de enlace y todos los dispositivos que están acoplados tooit. Como se indica el nombre de hello, puertas de enlace de campo actuar instalaciones de procesamiento de datos dedicado exterior, suelen ser ubicación enlazados, es potencialmente intrusiones toophysical de asunto y habrá limitado redundancia operativa. Todos los toosay que suele ser una puerta de enlace de campo algo uno puede táctil y sabotear al saber cuál es su función. 

Una puerta de enlace de campo se diferencia de un enrutador de tráfico en que tiene un rol activo en la administración del acceso y del flujo de información, lo que significa que es una entidad y terminal de sesión o de conexión de red dirigidos a aplicaciones. Por el contrario, los dispositivos NAT o los firewalls no son aptos como puertas de enlace de campo, porque no son terminales de sesión o de conexión explícitos, sino que enrutan (o bloquean) las conexiones o sesiones que se realizan a través de ellos. puerta de enlace de campo de Hello tiene dos áreas de superficie. Uno enfrenta a dispositivos de hello tooit adjunto y representa Hola dentro de la zona de hello, y Hola otro enfrenta a todas las partes externas y se borde Hola de zona de Hola.   

### <a name="hello-cloud-gateway-zone"></a>zona de puerta de enlace de Hello en la nube
Puerta de enlace de nube es un sistema que permite la comunicación remota de y toodevices o campo puertas de enlace de varios sitios a través del espacio de la red pública, normalmente hacia una basada en la nube datos y control sistema de análisis, una federación de estos sistemas. En algunos casos, una puerta de enlace de nube puede facilitar inmediatamente dispositivos toospecial con fines de acceso de los terminales como tabletas o teléfonos. En el contexto de hello descrito aquí, la "nube" está pensado toorefer tooa dedicado procesamiento de datos de sistema que no está enlazado toohello mismo sitio como Hola adjunta dispositivos o puertas de enlace de campo. También en una zona en la nube, impiden el acceso físico destino medidas operativas y no es necesariamente expuesto tooa infraestructura de "nube pública".  

Posiblemente se puede asignar una puerta de enlace de nube en una red virtualización superposición tooinsulate Hola nube puerta de enlace y todos sus dispositivos conectados o puertas de enlace de campo desde cualquier otro tráfico de red. Hola nube puerta de enlace es ni un sistema de control de dispositivo ni un procesamiento o dispositivo de almacenamiento de datos del dispositivo; las instalaciones de la interfaz con la puerta de enlace de hello en la nube. zona de puerta de enlace de nube de Hola Hola nube puerta de enlace junto con todas las puertas de enlace de campo y dispositivos, directa o indirectamente acoplados tooit. borde de Hola de zona de hello es un área expuesta distinto donde todas las entidades externas se comunican a través de.

### <a name="hello-services-zone"></a>zona de servicios de Hola
En este contexto, un "servicio" se define como cualquier componente de software o módulo que interactúa con dispositivos a través de una puerta de enlace de campo o en la nube para la recopilación y análisis de datos, así como para el comando y control.  Los servicios son mediadores. Actúan en su identidad hacia las puertas de enlace y otros subsistemas, almacenan y analizan los datos, forma autónoma problema comandos toodevices en función de información sobre los datos o las programaciones y exponer información y controlar funciones tooauthorized los usuarios finales.

### <a name="information-devices-vs-special-purpose-devices"></a>Dispositivos de información frente a dispositivos especiales
Los equipos, los teléfonos y las tabletas son principalmente dispositivos de información interactivos. Los teléfonos y las tabletas están optimizados explícitamente para maximizar la duración de la batería. Si es posible desactiven parcialmente cuando no inmediatamente interactuar con una persona, o cuando no proporciona servicios como reproducir música o guiar a su propietario ubicación determinada tooa. Desde una perspectiva de los sistemas, estos dispositivos de tecnología de la información actúan principalmente como servidores proxy hacia las personas. Son “accionadores de personas” que sugieren acciones y “sensores de personas” que recopilan datos de entrada. 

Dispositivos con fines especiales, de líneas de producción de temperatura simple sensores toocomplex generador con miles de componentes dentro de ellos, son diferentes. Estos dispositivos son un ámbito mucho más en su finalidad e incluso si proporciona alguna interfaz de usuario, que son en gran medida con ámbito toointerfacing con o integrarse en activos de Hola mundo físico. Miden e informan acerca de las circunstancias medioambientales de informes, giran válvulas, controlar servodirecciones, hacen que suenen alarmas y encienden luces, entre otras muchas tareas. Ayudan a toodo de trabajo para el que un dispositivo de información es demasiado genérico, demasiado caro, demasiado grande o demasiado complicado. propósito concreto Hola dicta inmediatamente su diseño técnico como presupuesto disponible de monetario Hola bien para su producción y la operación de duración programada. combinación de Hola de estos dos factores claves restringe Hola operativa asignación de energía, espacio físico y, por tanto, el almacenamiento disponible, proceso disponibles y capacidades de seguridad.  

Si tiene algún valor "va incorrecto" con dispositivos controlables automatizados o remotos, por ejemplo, defectos físicos o toowillful de defectos de lógica de control no autorizado intrusiones y la manipulación. puede destruir una gran cantidad de producción de Hello, edificios pueden ser saqueados o grabados hacia abajo y personas pueden herido o incluso chip. Indudablemente, este tipo de daño es totalmente distinto del que produce alguien que agota el límite de una tarjeta de crédito robada. mover Hello barra de seguridad para los dispositivos que hacer las cosas, y también para los datos de sensor que finalmente resultados en comandos que provoquen toomove cosas, debe ser mayor que en cualquier escenario de banca o de comercio electrónico. 

### <a name="device-control-and-device-data-interactions"></a>Control de dispositivos e interacciones con datos de dispositivos
Dispositivos conectados de propósito especial tienen un número importante de posibles áreas de superficie de interacción y patrones de interacción, todos ellos deben tener en cuenta tooprovide un marco para proteger el acceso digital toothose dispositivos. término de Hola "digital access" es usado aquí toodistinguish de las operaciones que se llevan a cabo a través de la interacción directa de dispositivos donde se proporciona seguridad de acceso a través del control de acceso físico. Por ejemplo, colocar dispositivo hello en una sala con un bloqueo en puerta de Hola. Mientras no se puede denegar el acceso físico con el software y hardware, se pueden tomar medidas tooprevent acceso físico de los principales toosystem interferencias. 

A medida que exploramos patrones de interacción de hello, veremos "control de dispositivo" y "datos del dispositivo" con Hola de mismo nivel de atención durante el modelado de amenazas. "Control de dispositivo" se puede clasificar como cualquier información que se proporciona tooa dispositivo por cualquier entidad con el objetivo de Hola de cambiar o influir en su comportamiento hacia su estado u Hola de su entorno. "Datos del dispositivo" se pueden clasificar como cualquier información que un dispositivo emite tooany otra parte sobre su estado y Hola observadas el estado de su entorno. 

## <a name="threat-modeling-hello-azure-iot-reference-architecture"></a>Arquitectura de referencia de hello IoT de Azure de modelado de amenazas
Microsoft usa framework Hola descrita anteriormente para IoT de Azure de modelado de amenazas de toodo. En la siguiente sección de Hola, por tanto, usamos ejemplo concreto de Hola de toodemonstrate de arquitectura de referencia de IoT de Azure cómo identifica toothink acerca de modelado de amenazas de IoT y cómo tooaddress Hola amenazas. En este caso, se han identificado cuatro áreas principales de atención:

* Dispositivos y orígenes de datos,
* Transporte de datos,
* Dispositivo y procesamiento de eventos
* Presentación

![Modelado de riesgos para IoT de Azure](media/iot-security-architecture/iot-security-architecture-fig2.png) 

diagrama de Hello siguiente proporciona una vista simplificada de arquitectura de IoT de Microsoft mediante un modelo de diagrama de flujo de datos que se usa por hello herramienta de modelado de amenazas de Microsoft:

![Modelado de riesgos para IoT de Azure mediante la herramienta de modelado de riesgos de MS](media/iot-security-architecture/iot-security-architecture-fig3.png)

Es importante toonote que Hola arquitectura separa las capacidades de dispositivo y la puerta de enlace de Hola. Esto permite Hola usuario tooleverage dispositivos de puerta de enlace que son más seguros: es capaces de comunicarse con hello en la nube puerta de enlace mediante protocolos seguros, lo que normalmente requiere mayor sobrecarga de procesamiento que un dispositivo nativo - como un termostato - pudo proporcionar por sí mismo. En la zona de los servicios de Azure de hello, suponemos que Hola que puerta de enlace de nube se representa mediante Hola servicio del centro de IoT de Azure.

### <a name="device-and-data-sourcesdata-transport"></a>Dispositivo y orígenes de datos o transporte de datos
Esta sección explora la arquitectura de hello descrita anteriormente a través de la lente de hello del modelado de amenazas y ofrezca una visión general de cómo nos dirigimos a algunos de los problemas inherentes de Hola. Nos centraremos en elementos básicos de Hola de un modelo de amenazas:

* Procesos (las que están bajo nuestro control y los elementos externos)
* Comunicación (denominado también flujos de datos)
* Almacenamiento (denominado también almacenes de datos)

#### <a name="processes"></a>Procesos
En cada una de las categorías de hello descritos en hello arquitectura de IoT de Azure, intentamos toomitigate existe un número de amenazas diferentes en distintas fases de hello datos o información en: proceso, la comunicación y el almacenamiento. A continuación se ofrece una visión general de hello más comunes se encargan de la categoría de "proceso" Hola, seguido de una descripción general de cómo se puede mitigar mejor: 

**Suplantación de identidad (S)**: un atacante puede extraer el material de clave criptográfica de un dispositivo, ya sea a nivel de software o hardware de hello y obtener acceso posteriormente sistema Hola con otro dispositivo físico o virtual con identidad Hola de Hola Hola de dispositivo se ha tomado el material de clave de. Un buen ejemplo son los mandos a distancia que pueden encender cualquier televisor y que son herramientas populares para gastar bromas.

**Denegación de servicio (D)**: un dispositivo se puede representar como incapaz de funcionar o comunicarse al interferir con frecuencias de radio o cortar hilos. Por ejemplo, una cámara de vigilancia cuya alimentación o conexión de red se han interrumpido intencionadamente cubriendo no notificarán datos.

**Manipulación (T)**: un atacante puede reemplazar parcial o totalmente software Hola que se ejecuta en el dispositivo de hello, permitiendo potencialmente Hola reemplazar software tooleverage Hola original identidad de dispositivo de hello si hello material de clave u Hola criptográfico funciones que contiene material clave eran programa ilícito toohello disponible. Por ejemplo, un atacante puede aprovechar extraído toointercept material clave y suprimir los datos del dispositivo de hello en la ruta de comunicación de Hola y reemplazarlo con datos falsos que se autentican con material de clave de hello robada.

**Divulgación de información (I)**: si Hola dispositivo está ejecutando software manipulado, dicho software manipulado puede provocar pérdidas de partes de toounauthorized de datos. Por ejemplo, un atacante puede aprovechar extraído clave material tooinject propio en ruta de acceso de hello comunicación entre dispositivos de hello y una puerta de enlace de controlador o un campo o puerta de enlace toosiphon la información en la nube.

**Elevación de privilegios (E)**: un dispositivo que realiza la función específica puede ser forzada toodo algo más. Por ejemplo, una válvula de tooopen programado mitad forma puede inducir a tooopen Hola a todos forma.

| **Componente** | **Amenaza** | **Mitigación** | **Riesgo** | **Implementación** |
| --- | --- | --- | --- | --- |
| Dispositivo |S |Asignación de identidad toohello dispositivo y la autenticación de dispositivo de Hola |Reemplace el dispositivo o parte de un dispositivo Hola con cualquier otro dispositivo. ¿Cómo sabemos que estamos hablando toohello de dispositivo correcto? |Autenticación de dispositivo de hello, mediante seguridad de capa de transporte (TLS) o IPSec. La infraestructura debe admitir el uso de una clave precompartida (PSK) en los dispositivos que no pueden controlar la criptografía asimétrica completa. Aprovechamiento de Azure AD, [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt) |
| TRID |Dispositivo de toohello de mecanismos a prueba de manipulaciones se aplican por ejemplo, ya que las claves de tooextract tooimpossible muy complicada y otro material criptográfico de dispositivo de Hola. |riesgo de Hello es si un usuario es la alteración dispositivo hello (interferencias física). ¿Cómo tenemos la certeza de que el dispositivo no se ha alterado? |mitigación de Hello más eficaz es una capacidad de módulo (TPM) de plataforma segura que permite almacenar claves de circuitos de tipo on-chip especial de qué hello no se puede leer las claves, pero solo pueden utilizarse para las operaciones criptográficas que utilizan clave Hola pero nunca revelar la clave de Hola . Cifrado de memoria del dispositivo de Hola. Administración de claves para el dispositivo de Hola. Firma de código de hello. | |
| E |Tener el control de acceso del dispositivo de Hola. Esquema de autorización. |Si el dispositivo de hello permite para acciones individuales toobe realizar basándose en los comandos de un origen externo, o incluso puesto en peligro los sensores, permitirá ataque hello tooperform operaciones no es accesible en caso contrario. |Con el esquema de autorización para el dispositivo de Hola | |
| Puerta de enlace de campo |S |Autenticar tooCloud de puerta de enlace de campo de hello puerta de enlace (cert según, PSK, notificación según,...) |Si alguien puede suplantar la identidad de la puerta de enlace de campo, puede presentarse como cualquier dispositivo. |TLS RSA/PSK, IPSec, [RFC 4279](https://tools.ietf.org/html/rfc4279). Hola a todos los mismo almacenamiento de claves y problemas de atestación de dispositivos en general: mejor de los casos es usar TPM. Extensión de 6LowPAN para IPSec toosupport inalámbrica Sensor de redes (WSN). |
| TRID |¿Protege Hola puerta de enlace de campo de la alteración (TPM)? |Ataques que engañan a la puerta de enlace de nube de hello pensando en comunica toofield de suplantación puerta de enlace podría provocar la divulgación de información y a la alteración de datos |Cifrado de memoria, TPM y autenticación. | |
| E |Mecanismo de control de acceso de una puerta de enlace de campo | | | |

Estos son algunos ejemplos de las amenazas de esta categoría:

Suplantación de identidad: Un atacante puede extraer material de clave criptográfica de un dispositivo, ya sea en el nivel de software o hardware de Hola y posteriormente acceso sistema Hola con otro dispositivo físico o virtual con identidad Hola Hola dispositivo Hola del material de clave se ha toma.

**Denegación de servicio**: un dispositivo se puede representar como incapaz de funcionar o comunicarse al interferir con frecuencias de radio o cortar hilos. Por ejemplo, una cámara de vigilancia cuya alimentación o conexión de red se han interrumpido intencionadamente cubriendo no notificarán datos.

**Manipulación**: un atacante puede reemplazar parcial o totalmente software Hola que se ejecuta en el dispositivo de hello, permitiendo potencialmente Hola reemplazar software tooleverage Hola original identidad de dispositivo de hello si hello material de clave u Hola criptográfico funciones que contiene material clave eran programa ilícito toohello disponible.

**Manipulación**: una cámara de vigilancia que muestra una imagen del espectro visible de un pasillo vacío puede dirigirse a una fotografía de dicho pasillo. Un detector de humo o de incendios puede saltar si hay alguien debajo con un mechero encendido. En cualquier caso, puede ser dispositivo Hola técnicamente plena confianza hacia el sistema de hello, pero le informará sobre información manipulado.

**Manipulación**: un atacante puede aprovechar extraído toointercept material clave y suprimir los datos del dispositivo de hello en la ruta de comunicación de Hola y reemplazarlo con datos falsos que se autentican con material de clave de hello robado.

**Manipulación**: un atacante puede reemplazar total o parcialmente software Hola que se ejecuta en el dispositivo de hello, permitiendo potencialmente Hola reemplazar software tooleverage Hola original identidad de dispositivo de hello si hello material de clave u Hola criptográfico funciones que contiene material clave eran programa ilícito toohello disponible.

**Divulgación de información**: si Hola dispositivo está ejecutando software manipulado, dicho software manipulado puede provocar pérdidas de partes de toounauthorized de datos.

**Divulgación de información**: un atacante puede aprovechar extraído clave material tooinject propio en ruta de acceso de hello comunicación entre dispositivos de hello y una puerta de enlace de controlador o un campo o puerta de enlace toosiphon la información en la nube.

**Denegación de servicio**: Hola dispositivo se ha desactivado o se convierten en un modo donde la comunicación no es posible (que es intencional en muchas máquinas industriales).

**Manipulación**: dispositivo Hola puede ser toooperate ha vuelto a configurar en un estado desconocido toohello controlar sistema (fuera de los parámetros de calibrado conocidos) y, por tanto, proporcionan datos que se pueden interpretar erróneamente

**Elevación de privilegios**: un dispositivo que realiza la función específica puede ser forzada toodo algo más. Por ejemplo, una válvula de tooopen programado mitad forma puede inducir a tooopen Hola a todos forma.

**Denegación de servicio**: dispositivo Hola se puede convertir en un estado que no sea posible la comunicación.

**Manipulación**: dispositivo Hola puede ser toooperate ha vuelto a configurar en un estado desconocido toohello controlan sistema (fuera de los parámetros de calibrado conocidos) y, por tanto, proporcionan datos que se pueden interpretar.

**Suplantación de identidad, alteración de datos/repudio**: si no están protegidos (que rara vez es Hola sucede con los controles remotos de consumidor) un atacante puede manipular el estado de saludo de un dispositivo de forma anónima. Un buen ejemplo son los mandos a distancia que pueden encender cualquier televisor y que son herramientas populares para gastar bromas.

#### <a name="communication"></a>Comunicación
Las amenazas existentes en ta ruta de acceso de comunicación entre los dispositivos, los dispositivos y las puertas de enlace de campo, y los dispositivos y la puerta de enlace en la nube. tabla Hola siguiente tiene alguna orientación todo sockets abiertos en hello dispositivo/VPN:

| **Componente** | **Amenaza** | **Mitigación** | **Riesgo** | **Implementación** |
| --- | --- | --- | --- | --- |
| Centro de IoT de dispositivo |TID |(D) Tráfico TLS (PSK/RSA) tooencrypt Hola |Interceptaciones o interferir comunicación Hola entre dispositivos de Hola y puerta de enlace de Hola |Seguridad de nivel de protocolo de Hola. Con protocolos personalizados, necesitamos toofigure más información sobre cómo tooprotect ellos. En la mayoría de los casos, la comunicación de hello tiene lugar de hello dispositivo toohello centro de IoT (dispositivo inicia la conexión de hello). |
| Dispositivo Dispositivo |TID |(D) Tráfico TLS (PSK/RSA) tooencrypt Hola. |Lectura de los datos en tránsito entre dispositivos. Manipulación de datos de Hola. Sobrecarga de dispositivo de hello con las nuevas conexiones |Seguridad de nivel de protocolo de hello (MQTT/AMQP o HTTP/CoAP. Con protocolos personalizados, necesitamos toofigure más información sobre cómo tooprotect ellos. mitigación de Hola para hello amenaza de denegación es toopeer dispositivos a través de una puerta de enlace en la nube o un campo y pídale que solo actúan como clientes hacia la red de Hola. una conexión directa entre equipos del mismo nivel Hola después negociada de puerta de enlace de Hola Hola emparejamiento penada |
| Entidad externa Dispositivo |TID |Emparejamiento segura de dispositivo de Hola entidades externas toohello |Dispositivo de toohello de conexión de interceptación Hola. Comunicación de hello interfiere con dispositivo Hola |Emparejamiento de forma segura toohello dispositivo LE NFC/Bluetooth de Hola entidades externas. Control panel operativa hello de dispositivo de hello (física) |
| Puerta de enlace de campo Puerta de enlace en la nube |TID |Tráfico TLS (PSK/RSA) tooencrypt Hola. |Interceptaciones o interferir comunicación Hola entre dispositivos de Hola y puerta de enlace de Hola |Seguridad de nivel de protocolo de hello (MQTT/AMQP o HTTP/CoAP). Con protocolos personalizados, necesitamos toofigure más información sobre cómo tooprotect ellos. |
| Puerta de enlace en la nube de dispositivo |TID |Tráfico TLS (PSK/RSA) tooencrypt Hola. |Interceptaciones o interferir comunicación Hola entre dispositivos de Hola y puerta de enlace de Hola |Seguridad de nivel de protocolo de hello (MQTT/AMQP o HTTP/CoAP). Con protocolos personalizados, necesitamos toofigure más información sobre cómo tooprotect ellos. |

Estos son algunos ejemplos de las amenazas de esta categoría:

**Denegación de servicio**: restringidos dispositivos suelen ser bajo la amenaza de denegación cuando realizan escuchas para las conexiones entrantes o datagramas no solicitados en una red, porque un atacante puede abrir muchas conexiones en paralelo y no darles servicio o de servicio ellos muy lenta, o hello dispositivo puede estar congestiona con tráfico no solicitado. En ambos casos, el dispositivo de hello puede eficazmente quedar inoperativo en red Hola.

**Suplantación de identidad, la divulgación de información**: dispositivos restringidos y especial a menudo tienen funciones de seguridad de uno para todos como protección de PIN o contraseña, o se basan totalmente en red Hola fiable, lo que significa que van a conceder acceso tooinformation cuando un dispositivo está en hello misma red y esa red a menudo sólo está protegida por una clave compartida. Eso significa que cuando Hola compartido toodevice secreto o la red se revela, es posible toocontrol Hola dispositivo u observar los datos emitidos desde dispositivo Hola.  

**Suplantación de identidad**: un atacante puede interceptar o invalidar parcialmente Hola difusión y engaño Hola originador (man en medio de hello)

**Manipulación**: un atacante puede interceptar o parcialmente invalidar Hola difusión y enviar información falsa 

**Divulgación de información:** un atacante puede interceptar una difusión y obtener información sin autorización **denegación de servicio:** un atacante puede atasco Hola señal de difusión y denegar la distribución de información

#### <a name="storage"></a>Storage
Cada puerta de enlace de dispositivo y el campo tiene algún tipo de almacenamiento (temporal para los datos de hello puesta en cola, el almacenamiento de imágenes de sistema operativo (SO)).

| **Componente** | **Amenaza** | **Mitigación** | **Riesgo** | **Implementación** |
| --- | --- | --- | --- | --- |
| Almacenamiento del dispositivo |TRID |Cifrado de almacenamiento, registros de Hola de firma |Leer datos desde el almacenamiento de hello (datos PII), manipulación de datos de telemetría. Manipulación de datos de control de comandos en cola o en la memoria caché. Manipule los paquetes de actualización de configuración o el firmware mientras almacenado en caché o en la cola local puede provocar componentes tooOS y/o el sistema está en peligro |Cifrado, código de autenticación de mensajes (MAC) o firma digital. Donde sea posible, control de acceso seguro a través de listas de control de acceso (ACL) a los recursos o permisos. |
| Imagen de sistema operativo de dispositivo |TRID | |Manipule SO / reemplazo de componentes de hello SO |Partición de sistema operativo de solo lectura, imagen de sistema operativo firmada, cifrado |
| Almacenamiento de puerta de enlace de campo (datos de hello puesta en cola) |TRID |Cifrado de almacenamiento, registros de Hola de firma |Leer datos desde el almacenamiento de hello (datos PII), manipulación de datos de telemetría, manipule en cola o datos de control de comandos almacenados en caché. Manipular paquetes de actualización de la configuración o el firmware (destinados a dispositivos o puerta de enlace de campo) mientras se almacena en caché o en la cola local puede provocar componentes tooOS y/o el sistema está en peligro |BitLocker |
| Imagen de sistema operativo de puerta de enlace de campo |TRID | |Manipule SO / reemplazo de componentes de hello SO |Partición de sistema operativo de solo lectura, imagen de sistema operativo firmada, cifrado |

### <a name="device-and-event-processingcloud-gateway-zone"></a>Zona de procesamiento de dispositivos y eventos o de puerta de enlace en la nube
Una puerta de enlace de nube es sistema que permite la comunicación remota de y toodevices o campo puertas de enlace de varios sitios a través del espacio de la red pública, normalmente hacia una basada en la nube datos y control sistema de análisis, una federación de estos sistemas. En algunos casos, una puerta de enlace de nube puede facilitar inmediatamente dispositivos toospecial con fines de acceso de los terminales como tabletas o teléfonos. En el contexto de hello descrito aquí, la "nube" está pensado toorefer tooa dedicado procesamiento de datos de sistema que no está enlazado toohello mismo sitio como Hola adjunta dispositivos o puertas de enlace de campo y donde medidas operativas evitar el acceso físico de destino pero no es necesariamente tooa "pública" infraestructura de la nube.  Posiblemente se puede asignar una puerta de enlace de nube en una red virtualización superposición tooinsulate Hola nube puerta de enlace y todos sus dispositivos conectados o puertas de enlace de campo desde cualquier otro tráfico de red. Hola nube puerta de enlace es ni un sistema de control de dispositivo ni un procesamiento o dispositivo de almacenamiento de datos del dispositivo; las instalaciones de la interfaz con la puerta de enlace de hello en la nube. zona de puerta de enlace de nube de Hola Hola nube puerta de enlace junto con todas las puertas de enlace de campo y dispositivos, directa o indirectamente acoplados tooit.

Puerta de enlace de nube es principalmente personalizado parte integrada de software que se ejecuta como un servicio con la puerta de enlace de extremos expuestos toowhich campo y dispositivos se conectan. Por lo tanto, debe diseñarse pensando en la seguridad. Siga el proceso de [SDL](http://www.microsoft.com/sdl) para diseñar y compilar este servicio. 

#### <a name="services-zone"></a>Zona de servicios
Un sistema de control (o controlador) es una solución de software que se comunica con un dispositivo, o una puerta de enlace de campo o la puerta de enlace de nube a fin de Hola de controlar uno o varios dispositivos o toocollect o almacén o analizar datos de dispositivo de presentación, o con fines de control posteriores. Sistemas de control son las únicas entidades de hello en el ámbito de Hola de esta explicación que inmediatamente puede facilitar la interacción con personas. excepción de Hello son superficies de control físicas intermedias en dispositivos, como un conmutador que permite que una persona tooturn Hola dispositivo desactivado o cambiar otras propiedades, y para el que no hay ningún equivalente funcional que se puede acceder digitalmente. 

Superficies de control físicas intermedias son aquellos donde ningún tipo de que rigen la lógica restringe la función hello de superficie de control físico de hello tal que una función equivalente se puede iniciar de forma remota o entrada entra en conflicto con la entrada remoto puede ser evitado: este tipo cursan superficies de control son sistema de control local tooa conceptualmente adjunto que aprovecha Hola misma funcionalidad subyacente que cualquier otro sistema de control remoto que Hola dispositivo puede ser tooin adjunto paralelas. Principales amenazas toohello la informática en nube puede ser leído en [en la nube seguridad Alliance (CSA)](https://cloudsecurityalliance.org/research/top-threats/) página.

## <a name="additional-resources"></a>Recursos adicionales
Toohello siguientes artículos para obtener más información, consulte:

* [SDL Threat Modeling Tool](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx) (Herramienta de modelado de amenazas SDL)
* [Microsoft Azure IoT reference architecture available](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/) (Arquitectura de referencia de IoT de Microsoft Azure disponible)

