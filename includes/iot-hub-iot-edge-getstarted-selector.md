> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

Este artículo ofrece un tutorial detallado de hello [código de ejemplo de Hola a todos] [ lnk-helloworld-sample] componentes fundamentales de hello tooillustrate de hello [Azure IoT borde] [ lnk-iot-edge] arquitectura. Hello ejemplo utiliza hello borde de IoT de Azure toobuild una puerta de enlace simple que registra cada cinco segundos de un archivo de tooa de mensaje "¡hello world".

En este tutorial, se describen los siguientes procedimientos:

* **Hola arquitectura de ejemplo del mundo**: describe cómo [conceptos arquitectónicos de borde de IoT de Azure] [ lnk-edge-concepts] toohello ejemplo de Hola a todos y cómo encajan los componentes de Hola se aplican.
* **¿Cómo toobuild Hola ejemplo**: ejemplo de Hola Hola a toobuild necesarios pasos.
* **¿Cómo toorun Hola ejemplo**: ejemplo de Hola Hola a toorun necesarios pasos. 
* **La salida típica**: muestra un ejemplo de Hola tooexpect de salida al ejecutar el ejemplo de Hola.
* **Fragmentos de código**: una colección de tooshow de fragmentos de código cómo implementa el ejemplo hello World Hola principales componentes de puerta de enlace de IoT borde.


## <a name="hello-world-sample-architecture"></a>Arquitectura de ejemplo Hello World
ejemplo de Hola mundo Hola ilustra los conceptos de Hola que se describe en la sección anterior de Hola. ejemplo de Hola mundo Hola implementa una puerta de enlace de IoT perimetral que tiene una canalización consta de dos módulos de IoT borde:

* Hola *Hola a todos* módulo crea un mensaje cada cinco segundos y le pasa el módulo de registrador toohello.
* Hola *registrador* mensajes de saludo de escrituras de módulo que recibe el archivo tooa.

![Arquitectura del ejemplo Hola mundo creada con Azure IoT Edge][4]

Como se describe en la sección anterior de hello, Hola mundo Hola módulo no pasa los mensajes directamente módulo de registrador toohello cada cinco segundos. En su lugar, publica a un agente de toohello mensajes cada cinco segundos.

módulo de registrador Hola recibe el mensaje de bienvenida desde el agente de Hola y actúa sobre ella, escribir el contenido de hello del archivo de tooa de mensaje de Hola.

módulo de registrador Hola sólo consume mensajes desde el agente de hello, nunca publica nuevo agente de toohello de mensajes.

![Cómo Hola broker enruta los mensajes entre los módulos en el borde de IoT de Azure][5]

Hello ilustración anterior muestra hello arquitectura de ejemplo de Hola mundo Hola y rutas de acceso relativas de hello toohello archivos de código fuente que implementan diferentes partes de ejemplo de Hola Hola [repositorio][lnk-iot-edge]. Explorar el código de hello por su cuenta o usar fragmentos de código de hello siguiente como guía.

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md