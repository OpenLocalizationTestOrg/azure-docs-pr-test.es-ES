# <a name="internet-of-things-security-best-practices"></a>Procedimientos recomendados de seguridad de Internet de las cosas
toosecure una infraestructura de Internet de las cosas (IoT) requiere una estrategia de seguridad en profundidad rigurosa. Esta estrategia requiere toosecure datos en la nube de hello, proteger la integridad de los datos mientras están en tránsito en Hola internet pública y aprovisionar dispositivos de forma segura. Cada capa genera mayor garantía de seguridad en hello toda la infraestructura.

## <a name="secure-an-iot-infrastructure"></a>Protección de una infraestructura de IoT
Esta estrategia de seguridad en profundidad se pueden desarrollar y ejecuta con participación activa de varios jugadores relacionados con la fabricación de hello, desarrollo e implementación de dispositivos de IoT y la infraestructura. A continuación verá una descripción de alto nivel de estos participantes.  

* **Fabricante del hardware IoT/integrador**: normalmente, son los fabricantes de Hola de hardware IoT implementarse, integradores ensamblar el hardware de diversos fabricantes o proveedores proporcionar hardware para ver una implementación de IoT fabricada o bien, integrado con otros proveedores.
* **Programador de soluciones de IoT**: desarrollo de Hola de una solución de IoT se suele realizar mediante un programador de soluciones. Este desarrollador puede formar parte de un equipo interno o ejercer como integrador de sistemas especializado en esta actividad. Hola IoT programador de soluciones puede desarrollar diversos componentes de solución de IoT Hola desde el principio, integrar varios componentes estándar o de código abierto o adoptar soluciones preconfiguradas con adaptación menor.
* **Implementador de la solución de IoT**: después de IoT una solución se ha desarrollado, necesita toobe implementado en el campo de Hola. Esto implica la implementación de hardware, interconexión de dispositivos y la implementación de soluciones de nube de Hola o dispositivos de hardware.
* **Operador de solución de IoT**: después de implementa la solución de IoT hello, requiere supervisión, mantenimiento y las actualizaciones de operaciones a largo plazo. Esto puede hacerse mediante un equipo interno que comprende los especialistas de tecnología de información, las operaciones de hardware y los equipos de mantenimiento y especialistas de dominio que supervisar el funcionamiento correcto de Hola de toda la infraestructura de IoT.

Hola secciones siguientes proporcionan recomendaciones para cada uno de estos toohelp reproductores desarrollaran, implementación y operan una infraestructura segura de IoT.

## <a name="iot-hardware-manufacturerintegrator"></a>Integrador/fabricante de hardware IoT
siguiente Hola es hello las recomendaciones para los fabricantes de hardware de IoT e integradores de hardware.

* **Definir el ámbito de los requisitos de hardware toominimum**: diseño de hardware de hello debe incluir características de hello mínimo necesarios para el funcionamiento de hardware de Hola y nada más. Un ejemplo es puertos USB de tooinclude solo si es necesario para el funcionamiento de hello de dispositivo de Hola. Estas características adicionales de abrir el dispositivo de Hola de vectores de ataque no deseados que debería evitarse.
* **Asegúrese de hardware a prueba de manipulaciones**: compilar en mecanismos toodetect manipulaciones físicas, como la apertura de la cubierta del dispositivo de Hola o quitar una parte del dispositivo de Hola. Estas señales de alterar puede ser parte de hello datos flujo cargado toohello en la nube, que se avisa a los operadores de estos eventos.
* **Basarse en hardware seguro**: si COGS lo permite, cree características de seguridad como el almacenamiento seguro y cifrado, o la funcionalidad de arranque basada en el Módulo de plataforma segura (TPM). Estos dispositivos de la marca de características más seguras y ayudar a proteger Hola toda la infraestructura de IoT.
* **Proteger las actualizaciones**: las actualizaciones de Firmware durante la vigencia de hello de dispositivo de hello son inevitables. Creación de dispositivos con las rutas de acceso seguros para las actualizaciones y garantía criptográfica de versiones de firmware permitirá Hola dispositivo toobe segura durante y después de las actualizaciones.

## <a name="iot-solution-developer"></a>Desarrollador de soluciones de IoT
siguiente Hola es hello las recomendaciones para los programadores de soluciones de IoT:

* **Siga la metodología de desarrollo de software seguro**: desarrollo de software seguro requiere el terreno pensar acerca de la seguridad, desde el comienzo de hello del proyecto de hello todos implementación de hello forma tooits, prueba e implementación. Opciones de Hola de plataformas, lenguajes y herramientas están influenciadas con esta metodología. Hola ciclo de vida de desarrollo de seguridad de Microsoft proporciona un método paso a paso toobuilding un software seguro.
* **Seleccione software de código abierto con cuidado**: software de código abierto ofrece la oportunidad tooquickly desarrollar soluciones. Elegir el software de código abierto, considere la posibilidad de nivel de actividad de Hola de comunidad de Hola para cada componente de código abierto. Una comunidad activa garantiza la compatibilidad con el software; se detectarán problemas, a los que se hará frente. La otra opción es que no se admita software de código abierto complejo e inactivo, y así lo más probable es que no se detecten problemas.
* **Integrar con cuidado**: existen muchos errores de seguridad de software en límite de Hola de bibliotecas y API. La funcionalidad que no puede ser necesaria para la implementación actual de hello todavía podría estar disponible a través de un nivel de API. tooensure seguridad general, realizar toocheck seguro de que todas las interfaces de componentes se integra de brechas de seguridad.      

## <a name="iot-solution-deployer"></a>Implementador de soluciones de IoT
siguiente Hola es prácticas recomendadas para los implementadores de la solución de IoT:

* **Implementar hardware de forma segura**: implementaciones de IoT podrían requerir que toobe de hardware implementado en ubicaciones no seguras, como se muestra en los espacios públicos o configuraciones regionales supervisadas. En estas situaciones, asegúrese de que la implementación de hardware es inviolable toohello máxima medida. Si USB u otros puertos están disponibles en hardware de hello, asegúrese de que se tratarán en forma segura. Muchos vectores de ataques pueden usarlos como punto de entrada.
* **Mantener las claves de autenticación seguros**: durante la implementación, cada dispositivo requiere que los identificadores de dispositivo y asociados de claves de autenticación generadas por el servicio en la nube Hola. Mantener estas claves físicamente segura incluso después de la implementación de Hola. Puede utilizarse cualquier tecla comprometido por un dispositivo malintencionado toomasquerade como un dispositivo existente.

## <a name="iot-solution-operator"></a>Operador de soluciones de IoT
siguiente Hola es prácticas recomendadas de Hola para operadores de solución de IoT:

* **Mantener el sistema hello toodate**: asegúrese de que todos los controladores de dispositivos y sistemas operativos de dispositivos son versiones más recientes de toohello actualizado. Si activa las actualizaciones automáticas en Windows 10 (IoT u otras SKU), Microsoft la mantiene una toodate, con lo que se proporciona un sistema operativo seguro para los dispositivos de IoT. Mantener otros sistemas operativos (por ejemplo, Linux) seguridad toodate ayuda a garantiza que también estén protegidos frente a ataques malintencionados.
* **Proteger frente a actividades malintencionadas**: si se permite el sistema operativo de hello, instale las características más recientes de antivirus y antimalware hello en cada sistema operativo del dispositivo. Esto puede ayudar a mitigar las amenazas más externas. Puede proteger los sistemas operativos más modernos contra amenazas realizando los pasos adecuados.
* **Auditar con frecuencia**: infraestructura de auditoría IoT para problemas relacionados con la seguridad es clave al responder a incidentes de toosecurity. Mayoría de sistemas operativos proporcionan el registro de eventos integrados que se debe revisa con frecuencia toomake seguro que no se ha producido ninguna infracción de seguridad. Información de auditoría puede enviarse como un servicio de nube de toohello de flujo de telemetría independiente donde se pueden analizar.
* **Proteger físicamente la infraestructura de IoT de Hola**: Hola peor ataques de seguridad en la infraestructura de IoT se inician mediante el acceso físico toodevices. Una práctica de seguridad importante es tooprotect contra el uso malintencionado de los puertos USB y otro acceso físico. Las infracciones de una toouncovering clave que pudieran haberse producido es el registro de acceso física, por ejemplo, uso de puerto USB. Una vez más, Windows 10 (IoT y el resto de SKU) habilita el registro detallado de estos eventos.
* **Proteger las credenciales de nube**: credenciales de autenticación de nube usadas para configurar y usar una implementación de IoT son posiblemente acceso de toogain de manera más fácil de Hola y poner en peligro un sistema de IoT. Proteger las credenciales de hello cambiando la contraseña de hello con frecuencia y abstenerse de utilizar estas credenciales en equipos públicos.

Las funcionalidades de los distintos dispositivos IoT varían. Algunos dispositivos pueden ser equipos que ejecutan sistemas operativos de escritorio comunes, y otros pueden estar ejecutando sistemas operativos muy ligeros. prácticas recomendadas de seguridad Hola descritas anteriormente podrían ser dispositivos toothese aplicables en distintos grados. Si se proporciona, deben seguir prácticas recomendadas adicionales de seguridad e implementación de fabricantes de Hola de estos dispositivos.

Puede que algunos dispositivos heredados y limitados no se hayan diseñado de forma específica para la implementación de IoT. Estos dispositivos podrían no tienen datos de tooencrypt de capacidad de hello, conecte con hello Internet o proporcionar auditoría avanzada. En estos casos, una puerta de enlace de campo moderno y segura puede agregar datos de dispositivos heredados y proporcionar seguridad de hello necesario para conectar estos dispositivos a través de Internet de Hola. Las puertas de enlace de campo pueden proporcionar una autenticación segura, la negociación de sesiones cifradas, recibo de comandos de la nube de Hola y muchas otras características de seguridad.
