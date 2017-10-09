---
title: "aaaDeploy el conjunto de IoT de Azure conectado puerta de enlace de fábrica | Documentos de Microsoft"
description: "Cómo toodeploy una puerta de enlace de Windows o Linux toohello de conectividad de tooenable había conectado fábrica preconfigurado solución."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>Implementar una puerta de enlace de Windows o Linux para la solución de fábrica preconfigurado Hola conectado

Hello requiere software toodeploy una puerta de enlace para la solución de fábrica preconfigurado Hola conectado tiene dos componentes:

* Hola *OPC Proxy* establece un concentrador de conexión tooIoT. Hola *OPC Proxy* , a continuación, espera a que los mensajes de comando y control de hello integrado OPC explorador que se ejecuta en el portal de solución de hello generador conectado.
* Hola *Publisher OPC* se conecta a servidores de agente de usuario de OPC tooexisting locales y reenvía los mensajes de telemetría de ellos tooIoT concentrador.

Ambos componentes son de código abierto y están disponibles como código fuente en GitHub y como contenedores de Docker:

| GitHub | DockerHub |
| ------ | --------- |
| [OPC Publisher][lnk-publisher-github] | [OPC Publisher][lnk-publisher-docker] |
| [OPC Proxy][lnk-proxy-github] | [OPC Proxy][lnk-proxy-docker] |

Ninguna dirección IP de orientados al público o agujeros en firewall de puerta de enlace de hello son necesarios para alguno de los componentes. Hola OPC Proxy y el publicador de OPC utilizan solo los puertos de salida 8883, 5671 y 443.

Hello pasos en este artículo muestra cómo toodeploy una puerta de enlace con Docker en cualquier [Windows](#windows-deployment) o [Linux](#linux-deployment). puerta de enlace de Hello habilita la solución de conectividad toohello conectado fábrica preconfigurado.

> [!NOTE]
> software de puerta de enlace de Hola que se ejecuta en el contenedor de Docker de hello es [Azure IoT borde].

## <a name="windows-deployment"></a>Implementación de Windows

> [!NOTE]
> Si todavía no tiene un dispositivo de puerta de enlace, Microsoft le recomienda comprar una puerta de enlace comercial con uno de nuestros asociados. Visite hello [catálogo de dispositivos de IoT de Azure] para obtener una lista de dispositivos de puerta de enlace compatibles con hello conectado solución de fábrica. Siga las instrucciones de Hola que vienen con hello tooset de dispositivo de puerta de enlace de Hola. O bien, usar hello después de configurar una de las puertas de enlace existentes de toomanually de instrucciones.

### <a name="install-docker"></a>Instalación de Docker

Instale [Docker para Windows] en el dispositivo de puerta de enlace Windows. Durante la instalación de Docker de Windows, seleccione una unidad en el tooshare de máquina de host con Docker. Hola siguiente captura de pantalla muestra comparten unidad Hola D en el sistema de Windows:

![Instalación de Docker][img-install-docker]

A continuación, cree una carpeta denominada **docker** en la raíz de Hola de hello unidad compartida.
También puede realizar este paso después de instalar docker desde hello **configuración** menú.

### <a name="configure-hello-gateway"></a>Configurar la puerta de enlace de Hola

1. Necesita hello **iothubowner** cadena de conexión de su conjunto de IoT de Azure conectado implementación de puerta de enlace de fábrica implementación toocomplete Hola. Hola [portal de Azure], navegue tooyour centro de IoT en grupo de recursos de hello crearon al implementar soluciones de fábrica de hello conectado. Haga clic en **directivas de acceso compartido** tooaccess hello **iothubowner** cadena de conexión:

    ![Buscar la cadena de conexión de centro de IoT Hola][img-hub-connection]

    Hola copia **cadena de conexión: clave principal** valor.

1. Configurar la puerta de enlace de hello para el centro de IoT mediante la ejecución de los módulos de puerta de enlace de hello dos **una vez** desde un símbolo del sistema con:

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  es Hola nombre toogive tooyour OPC UA publicador en formato de hello **publisher.&lt; el nombre de dominio completo&gt;**. Por ejemplo, si se llama a la red de fábrica **myfactorynetwork.com**, hello **ApplicationName** valor es **publisher.myfactorynetwork.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  es hello **iothubowner** cadena de conexión copió en el paso anterior de Hola. Esta cadena de conexión solo se utiliza en este paso, no la necesite en hello pasos:

    Usa Hola asignado D:\\carpeta docker (hello `-v` argumento) toopersist posterior Hola dos certificados X.509 que utilizar los módulos de puerta de enlace de Hola.

### <a name="run-hello-gateway"></a>Ejecutar la puerta de enlace de Hola

1. Reinicie la puerta de enlace de hello mediante Hola siguientes comandos:

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Por motivos de seguridad, los certificados X.509 Hola dos se conservan en hello D:\\carpeta docker contienen la clave privada de Hola. Limitar las credenciales de acceso toothis carpeta toohello (normalmente **administradores**) utilizar el contenedor de Docker de toorun Hola. Hola contextual D:\\carpeta docker, elija **propiedades**, a continuación, **seguridad**y, a continuación, **editar**. Conceda a los **administradores** el control total y quite a todos los demás:

    ![Recurso compartido de conceder permisos tooDocker][img-docker-share]

1. Compruebe la conectividad de la red. Desde un símbolo del sistema, escriba el comando de hello `ping publisher.<your fully qualified domain name>` tooping la puerta de enlace. Si se puede alcanzar el destino de hello, agregue la dirección IP de Hola y el nombre de archivo de hosts toohello de puerta de enlace en la puerta de enlace. archivo de hosts de Hola se encuentra en hello **Windows\\System32\\controladores\\etcetera** carpeta.

1. A continuación, intente tooconnect toohello publicador con un cliente local de OPC UA con puerta de enlace de Hola. Hola es la dirección URL de extremo de OPC UA `opc.tcp://publisher.<your fully qualified domain name>:62222`. Si no tiene un cliente OPC UA, puede descargar un [cliente OPC UA de código abierto] y úselo.

1. Cuando haya completado correctamente estas pruebas locales, busque toohello **conectar su propio servidor de agente de usuario de OPC** página del portal de solución de hello generador conectado. Escriba la dirección URL del extremo de publicador de hello (`tcp://publisher.<your fully qualified domain name>:62222`) y haga clic en **conectar**. Recibirá una advertencia de certificado; luego, haga clic en **Proceed** (Continuar). A continuación se produce un error que Hola publicador no confía en hello cliente de agente de usuario Web. tooresolve este error, Hola copia **cliente de agente de usuario Web** certificado de hello **D:\\docker\\certificados rechazó\\certificados** carpeta toohello **D:\\docker\\aplicaciones de agente de usuario\\certificados** carpeta en la puerta de enlace de Hola. No es necesario toorestart de puerta de enlace de Hola. Repita este paso. Ahora puede conectarse toohello puerta de enlace de nube de Hola y está listo tooadd toohello solución de OPC UA servidores.

### <a name="add-your-opc-ua-servers"></a>Incorporación de los servidores OPC UA

1. Examinar toohello **conectar su propio servidor de agente de usuario de OPC** página del portal de solución de hello generador conectado. Siga los mismos pasos de hello anterior sección tooestablish confianza entre Hola portal generador conectado y Hola servidor OPC UA de Hola. Este paso establece una confianza mutua de certificados de Hola de hello conectado hello servidor OPC UA y portal de fábrica y crea una conexión.

1. Examinar el árbol de nodos de OPC UA del servidor OPC UA hello, haga clic en los nodos OPC hello y seleccione **publicar**. Para publicación de toowork de esta manera, Hola servidor OPC UA y Hola publicador debe ser en hello misma red. En otras palabras, si Hola completo nombre de dominio del publicador de hello es **publisher.mydomain.com** , a continuación, nombre de dominio completo de Hola de hello OPC UA servidor debe ser, por ejemplo, **myopcuaserver.mydomain.com**. Si el programa de instalación es diferente, puede agregar manualmente los nodos toohello publishesnodes.json archivo encontrado en archivos hello **D:\\docker** carpeta. Hello publishesnodes.json archivo se genera automáticamente en hello primero correcta de publicación de un nodo de OPC.

1. Ahora los flujos de telemetría de dispositivo de puerta de enlace de Hola. Puede ver telemetría Hola Hola **Factory Locations** ver del portal de fábrica conectado hello en **nuevo generador**.

## <a name="linux-deployment"></a>Implementación de Linux

> [!NOTE]
> Si todavía no tiene un dispositivo de puerta de enlace, Microsoft le recomienda comprar una puerta de enlace comercial con uno de nuestros asociados. Visite hello [catálogo de dispositivos de IoT de Azure] para obtener una lista de dispositivos de puerta de enlace compatibles con hello conectado solución de fábrica. Siga las instrucciones de Hola que vienen con hello tooset de dispositivo de puerta de enlace de Hola. O bien, usar hello después de configurar una de las puertas de enlace existentes de toomanually de instrucciones.

[Instale Docker] en el dispositivo de puerta de enlace Linux.

### <a name="configure-hello-gateway"></a>Configurar la puerta de enlace de Hola

1. Necesita hello **iothubowner** cadena de conexión de su conjunto de IoT de Azure conectado implementación de puerta de enlace de fábrica implementación toocomplete Hola. Hola [portal de Azure], navegue tooyour centro de IoT en grupo de recursos de hello crearon al implementar soluciones de fábrica de hello conectado. Haga clic en **directivas de acceso compartido** tooaccess hello **iothubowner** cadena de conexión:

    ![Buscar la cadena de conexión de centro de IoT Hola][img-hub-connection]

    Hola copia **cadena de conexión: clave principal** valor.

1. Configurar la puerta de enlace de hello para el centro de IoT mediante la ejecución de los módulos de puerta de enlace de hello dos **una vez** desde un shell con:

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  es nombre Hola de hello puerta de enlace de OPC UA aplicación Hola crea en formato de hello **publisher.&lt; el nombre de dominio completo&gt;**. Por ejemplo, **publisher.microsoft.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  es hello **iothubowner** cadena de conexión copió en el paso anterior de Hola. Esta cadena de conexión solo se utiliza en este paso, no la necesite en hello pasos:

    Usar hello **/ compartido** carpeta (hello `-v` argumento) toopersist posterior Hola dos certificados X.509 que utilizar los módulos de puerta de enlace de Hola.

### <a name="run-hello-gateway"></a>Ejecutar la puerta de enlace de Hola

1. Reinicie la puerta de enlace de hello mediante Hola siguientes comandos:

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Por motivos de seguridad, los certificados X.509 Hola dos se conservan en hello **/ compartido** carpeta contienen la clave privada de Hola. Límite toothis carpeta toohello las credenciales de acceso usar toorun Hola contenedor Docker. permisos de hello tooset para **raíz** únicamente, use hello `chmod` shell de comandos en carpeta Hola.

1. Compruebe la conectividad de la red. Desde un shell, escriba el comando de hello `ping publisher.<your fully qualified domain name>` tooping la puerta de enlace. Si se puede alcanzar el destino de hello, agregue la dirección IP de Hola y el nombre de archivo de hosts tooyour de puerta de enlace en la puerta de enlace. archivo de hosts de Hola se encuentra en hello **/etcetera** carpeta.

1. A continuación, intente tooconnect toohello publicador con un cliente local de OPC UA con puerta de enlace de Hola. Hola es la dirección URL de extremo de OPC UA `opc.tcp://publisher.<your fully qualified domain name>:62222`. Si no tiene un cliente OPC UA, puede descargar un [cliente OPC UA de código abierto] y úselo.

1. Cuando haya completado correctamente estas pruebas locales, busque toohello **conectar su propio servidor de agente de usuario de OPC** página del portal de solución de hello generador conectado. Escriba la dirección URL del extremo de publicador de hello (`tcp://publisher.<your fully qualified domain name>:62222`) y haga clic en **conectar**. Recibirá una advertencia de certificado; luego, haga clic en **Proceed** (Continuar). A continuación se produce un error que Hola publicador no confía en hello cliente de agente de usuario Web. tooresolve este error, Hola copia **cliente de agente de usuario Web** certificado de hello **/compartido/rechazado certificados/certificados** carpeta toohello **/shared/UA aplicaciones/certificados** carpeta de puerta de enlace de Hola. No es necesario toorestart de puerta de enlace de Hola. Repita este paso. Ahora puede conectarse toohello puerta de enlace de nube de Hola y está listo tooadd toohello solución de OPC UA servidores.

### <a name="add-your-opc-ua-servers"></a>Incorporación de los servidores OPC UA

1. Examinar toohello **conectar su propio servidor de agente de usuario de OPC** página del portal de solución de hello generador conectado. Siga los mismos pasos de hello anterior sección tooestablish confianza entre Hola portal generador conectado y Hola servidor OPC UA de Hola. Este paso establece una confianza mutua de certificados de Hola de hello conectado hello servidor OPC UA y portal de fábrica y crea una conexión.

1. Examinar el árbol de nodos de OPC UA del servidor OPC UA hello, haga clic en los nodos OPC hello y seleccione **publicar**. Para publicación de toowork de esta manera, Hola servidor OPC UA y Hola publicador debe ser en hello misma red. En otras palabras, si Hola completo nombre de dominio del publicador de hello es **publisher.mydomain.com** , a continuación, nombre de dominio completo de Hola de hello OPC UA servidor debe ser, por ejemplo, **myopcuaserver.mydomain.com**. Si el programa de instalación es diferente, puede agregar manualmente los nodos toohello publishesnodes.json archivo encontrado en archivos hello **/ compartido** carpeta. Hola publishesnodes.json se genera automáticamente en hello primero correcta de publicación de un nodo de OPC.

1. Ahora los flujos de telemetría de dispositivo de puerta de enlace de Hola. Puede ver telemetría Hola Hola **Factory Locations** ver del portal de fábrica conectado hello en **nuevo generador**.

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de arquitectura de Hola de fábrica conectado Hola preconfigurado solución, vea [conectado fábrica preconfigurado tutorial de la solución][lnk-walkthrough].

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Docker para Windows]: https://www.docker.com/docker-windows
[catálogo de dispositivos de IoT de Azure]: https://catalog.azureiotsuite.com/?q=opc
[portal de Azure]: http://portal.azure.com/
[cliente OPC UA de código abierto]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[Instale Docker]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT borde]: https://github.com/Azure/iot-edge

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy