---
title: 'aaaAzure DMZ ejemplo: crear una red Perimetral Simple con NSG | Documentos de Microsoft'
description: "Creación de una red perimetral con grupos de seguridad de red"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a>Ejemplo 1: Crear una red perimetral simple mediante NSG con una plantilla de Azure Resource Manager
[Devolver toohello página de prácticas recomendadas de seguridad límite][HOME]

> [!div class="op_single_selector"]
> * [Plantilla de Resource Manager](virtual-networks-dmz-nsg.md)
> * [Clásico: PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

En este ejemplo se crea una red perimetral primitiva con cuatro servidores Windows y grupos de seguridad de red. En este ejemplo se describe cada uno de hello plantilla relevante secciones tooprovide una comprensión más profunda de cada paso. También hay un tooprovide de sección de escenario de tráfico obtener información detallada sobre paso a paso cómo se realiza el tráfico a través de niveles de Hola de defensa en hello red Perimetral. Por último, en la sección de referencias de hello es toobuild de código y las instrucciones de la plantilla completa de Hola este entorno tootest y experimentar con diferentes escenarios. 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

![Red perimetral de entrada con grupo de seguridad de red][1]

## <a name="environment-description"></a>Descripción del entorno
En este ejemplo, una suscripción contiene Hola recursos siguientes:

* Un único grupo de recursos
* Una red virtual con dos subredes (FrontEnd y BackEnd)
* Un grupo de seguridad de red que está aplicada tooboth subredes
* Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")
* Dos servidores Windows que representan servidores back-end de aplicaciones ("AppVM01", "AppVM02")
* Un servidor Windows que representa un servidor DNS ("DNS01")
* Una dirección IP pública asociada con el servidor de web de aplicación Hola

En la sección de referencias de hello, hay una plantilla de Azure Resource Manager tooan de vínculo que se basa el entorno de hello descrita en este ejemplo. Hola de crear las máquinas virtuales y redes virtuales, aunque se realiza mediante la plantilla de ejemplo de Hola, se describen detalladamente en este documento. 

**toobuild este entorno** (las instrucciones detalladas están en la sección de referencias de Hola de este documento);

1. Implementar Hola plantilla del Administrador de recursos de Azure en: [plantillas de inicio rápido de Azure][Template]
2. Instalar la aplicación de ejemplo de Hola en: [Script de aplicación de ejemplo][SampleApp]

>[!NOTE]
>servidores de back-end de tooRDP tooany en este caso, el servidor IIS de Hola se utiliza como un "cuadro salto". Primer servidor RDP toohello IIS y, a continuación, desde el servidor de hello IIS Server RDP toohello back-end. Asimismo, una IP pública se puede asociar con cada servidor NIC para facilitar la conexión RDP.
> 
>

Hello secciones siguientes proporcionan una descripción detallada de hello grupo de seguridad de red y su funcionamiento en este ejemplo recorriendo líneas claves de hello plantilla del Administrador de recursos de Azure.

## <a name="network-security-groups-nsg"></a>Grupos de seguridad de red (NSG)
En este ejemplo, se crea un grupo de seguridad de red y se cargan después seis reglas. 

>[!TIP]
>Por lo general, debe crear primero las reglas específicas de "Permitir" y, a continuación, Hola reglas más genéricas de "Denegar" última. Hola tenga asignada la prioridad determina qué reglas se evalúan primero. Una vez que el tráfico se encuentra la regla específica de tooapply tooa, no se evalúa ninguna otra regla. Se pueden aplicar reglas NSG en la vista en hello dirección entrante o saliente (desde la perspectiva de Hola de subred de hello).
>
>

Mediante declaración, se regeneran Hola siguiendo las reglas para el tráfico entrante:

1. Se permite el tráfico DNS interno (puerto 53)
2. Se permite el tráfico RDP (puerto 3389) de hello Internet tooany VM
3. Se permite el tráfico HTTP (puerto 80) del servidor de hello Internet tooweb (IIS01)
4. Se permite cualquier tráfico (todos los puertos) del IIS01 tooAppVM1
5. Todo (todos los puertos) el tráfico de hello Internet toohello se deniega todo red virtual (tanto en las subredes)
6. Se deniega todo (todos los puertos) el tráfico de subred de back-end de hello front-end subred toohello

Con estas subredes de enlazado tooeach reglas, si una solicitud HTTP es entrante desde el servidor web de hello Internet toohello, ambas reglas 3 (permitir) y 5 (denegar) aplicaría, pero dado que la regla 3 tiene mayor prioridad solo aplicaría y regla 5 podría no entran en juego. Por lo tanto solicitud HTTP de hello podría permitirse a toohello servidor de web. Si ese mismo tráfico estaba intentando server DNS01 de tooreach hello, regla 5 (Deny) sería Hola primera hello y tooapply el tráfico no estarían permitido a toopass toohello server. Regla 6 (Deny) bloques de subred de front-end de Hola de hablar de subred de back-end de toohello (excepto el tráfico permitido en las reglas 1 y 4), este conjunto de reglas protege la red de back-end de hello en caso de que una aplicación atacante pone en peligro hello web en hello front-end, el atacante de hello sería ha limitado toohello acceso back-end "protegido" red (solo tooresources expuesta en el servidor de hello AppVM01).

Hay una regla de salida predeterminada que permite el tráfico de salida toohello internet. En este ejemplo, permitimos el tráfico saliente y no modificamos las reglas de salida. tooapply tootraffic de directiva de seguridad en ambas direcciones, enrutamiento de definido por usuario es obligatorio y se explora en "Ejemplo 3" en hello [página de prácticas recomendadas de seguridad límite][HOME].

Cada regla se explica con más detalle a continuación:

1. Un recurso de grupo de seguridad de red debe ser toohold instancias Hola reglas:

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. la primera regla en este ejemplo de Hola permite el tráfico DNS entre todos los servidores DNS de toohello redes internas de subred de back-end de Hola. regla de Hello tiene algunos parámetros importantes:
  * "destinationAddressPrefix" - reglas pueden usar un tipo especial de prefijo de dirección denominado "Etiqueta predeterminada", estas etiquetas son identificadores proporcionados por el sistema que permiten una tooaddress fácilmente una categoría mayor de prefijos de dirección. Esta regla usa Hola etiqueta predeterminado "Internet" toosignify cualquiera de las direcciones fuera Hola red virtual. Otras etiquetas de prefijo son VirtualNetwork y AzureLoadBalancer.
  * "Direction" indica en qué dirección del flujo de tráfico esta entrada surte efecto. dirección de Hello es desde la perspectiva de Hola de subred de Hola o una máquina Virtual (en función de donde está enlazado este GSN). Por lo tanto si dirección es "Inbound" y está accediendo al tráfico de subred de Hola, Hola regla se aplicará y tráfico que sale de la subred de hello no se verían afectado por esta regla.
  * "Priority" establece el orden de hello en el que se evalúa un flujo de tráfico. Hola inferior Hola número Hola Hola prioridad. Cuando una regla aplica tooa flujo de tráfico específico, no se procesa ninguna otra regla. Por tanto, si una regla con prioridad 1 permite el tráfico y una regla con prioridad 2 deniega el tráfico y ambas reglas aplican tootraffic, ¿se permite el tráfico de hello tooflow (puesto regla 1 no tenía una prioridad más alta entra en vigor y no se aplica ninguna otra regla).
  * "Access" indica si se bloquea ("Deny") o se permite ("Allow") el tráfico al que afecta esta regla.

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. Esta regla permite tooflow de tráfico RDP de hello internet toohello el puerto RDP en cualquier servidor de hello enlazado subred. 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. Esta regla permite que servidor de web de hello toohit de tráfico de internet entrante. Esta regla no cambia el comportamiento de enrutamiento Hola. regla de Hello solo permite el tráfico destinado a IIS01 toopass. Por lo tanto si el tráfico de Internet Hola tenía el servidor de web de hello como su destino de esta regla se permitirlo y detener el procesamiento de más reglas. (En la regla de hello con prioridad 140 todos los demás tráfico entrante de internet se bloquea). Si sólo está procesando el tráfico HTTP, esta regla podría ser más restringido tooonly Permitir destino puerto 80.

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. Esta regla permite toopass de tráfico desde el servidor de hello IIS01 toohello AppVM01 server, una regla posterior bloquea todo el tráfico de otros tooBackend front-end. tooimprove esta regla, si se conoce el puerto de Hola que debe agregarse. Por ejemplo, si el servidor IIS de hello está alcanzando solo SQL Server en AppVM01, intervalo de puertos de destino de hello debe cambiarse de "*" (Any) too1433 (Hola puerto de SQL) lo que permite una menor superficie expuesta a ataques entrantes en AppVM01 debe alguna vez verse comprometida la aplicación web de Hola.

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. Esta regla deniega el tráfico de los servidores de tooany de internet de hello en red Hola. Con las reglas de hello en prioridad 110 y 120, el efecto de hello es tooallow solo internet tráfico toohello firewall de entrada y puertos RDP en servidores y todo lo demás bloquea. Esta regla es la regla de notificaciones de "error" tooblock todos los flujos inesperados.

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. regla de final de Hello deniega el tráfico de subred de back-end de hello front-end subred toohello. Puesto que esta regla es una regla de sola entrada, se permite el tráfico inverso (de hello back-end toohello front-end).

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a>Escenarios de tráfico
#### <a name="allowed-internet-tooweb-server"></a>(*Permitido*) servidor de Internet tooweb
1. Un usuario de internet solicita una página HTTP desde la dirección IP pública de Hola de hello que NIC asociada con hello IIS01 NIC
2. dirección IP pública de Hello pasa tráfico toohello red virtual hacia IIS01 (servidor web de hello)
3. La subred front-end comienza el procesamiento de las reglas de entrada:
  1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
  2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
  3. Aplicar NSG regla 3 (tooIIS01 Internet), el tráfico es el procesamiento de reglas permitidas, detenga
4. Tráfico alcanza el dirección IP interna del servidor web de hello IIS01 (10.0.1.5)
5. Iis01 escucha el tráfico de web, recibe esta solicitud y comienza a procesar la solicitud de Hola
6. Iis01 pide Hola SQL Server en AppVM01 información
7. No hay reglas de salida en la subred front-end, se permite el tráfico.
8. subred de back-end de Hello comienza el procesamiento de la regla de entrada:
  1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
  2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
  3. Regla de NSG 3 (tooFirewall Internet) no se aplica, mover toonext regla
  4. Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga
9. AppVM01 recibe Hola consulta SQL y responde
10. Dado que no hay ninguna regla de salida en la subred de back-end de hello, se permite la respuesta de Hola
11. La subred front-end comienza el procesamiento de las reglas de entrada:
  1. No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola
  2. Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.
12. servidor IIS de Hello recibe la respuesta SQL de Hola y completa respuesta HTTP de Hola y envía toohello solicitante
13. Dado que no hay ninguna regla de salida en la subred de front-end de hello, se permite la respuesta de Hola y Hola usuario de Internet recibe hello web página solicitada.

#### <a name="allowed-rdp-tooiis-server"></a>(*Permitido*) servidor de tooIIS RDP
1. Un administrador del servidor en internet solicita un tooIIS01 de sesión RDP en la dirección IP pública de Hola de hello que NIC asociada con hello NIC IIS01 (se puede encontrar esta dirección IP pública a través de hello Portal o PowerShell)
2. dirección IP pública de Hello pasa tráfico toohello red virtual hacia IIS01 (servidor web de hello)
3. La subred front-end comienza el procesamiento de las reglas de entrada:
  1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
  2. Se aplica la regla 2 (RDP) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.
4. No hay reglas de salida, se aplican las reglas predeterminadas y se permite el tráfico de retorno.
5. La sesión RDP está habilitada.
6. Mensajes de iis01 Hola nombre de usuario y contraseña

>[!NOTE]
>servidores de back-end de tooRDP tooany en este caso, el servidor IIS de Hola se utiliza como un "cuadro salto". Primer servidor RDP toohello IIS y, a continuación, desde el servidor de hello IIS Server RDP toohello back-end.
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*Permitido*) Búsqueda de DNS del servidor web en el servidor DNS
1. Web necesidades de servidor, IIS01, fuente de distribución de datos en www.data.gov, pero necesita tooresolve Hola dirección.
2. Hola configuración de red para las listas de red virtual de hello DNS01 (10.0.2.4 de subred de back-end de hello) como servidor DNS principal de hello, IIS01 envía Hola DNS solicitud tooDNS01
3. No hay reglas de salida en la subred front-end, se permite el tráfico.
4. La subred back-end comienza el procesamiento de las reglas de entrada:
  * Se aplica la regla 1 (DNS) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.
5. Servidor DNS recibe la solicitud de Hola
6. Servidor DNS no tiene dirección de hello en caché y pide un servidor DNS raíz en hello internet
7. No hay reglas de salida en la subred back-end, se permite el tráfico.
8. Se responde el servidor DNS de Internet, ya que esta sesión se ha iniciado internamente, se permite la respuesta de Hola
9. Servidor DNS almacena en caché la respuesta de Hola y responde tooIIS01 de espera de solicitud inicial toohello
10. No hay reglas de salida en la subred back-end, se permite el tráfico.
11. La subred front-end comienza el procesamiento de las reglas de entrada:
  1. No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola
  2. Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico por lo que se permite el tráfico de Hola
12. Iis01 recibe respuesta hello DNS01

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*Permitido*) Archivo de acceso del servidor web en AppVM01
1. IIS01 solicita un archivo en AppVM01
2. No hay reglas de salida en la subred front-end, se permite el tráfico.
3. subred de back-end de Hello comienza el procesamiento de la regla de entrada:
  1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
  2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
  3. Regla de NSG 3 (tooIIS01 Internet) no se aplica, mover toonext regla
  4. Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga
4. AppVM01 recibe la solicitud de Hola y responde con el archivo (suponiendo que se autoriza el acceso)
5. Dado que no hay ninguna regla de salida en la subred de back-end de hello, se permite la respuesta de Hola
6. La subred front-end comienza el procesamiento de las reglas de entrada:
  1. No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola
  2. Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.
7. servidor IIS de Hello recibe el archivo hello

#### <a name="denied-rdp-toobackend"></a>(*Denegado*) toobackend RDP
1. Un usuario de internet intenta tooRDP tooserver AppVM01
2. Dado que no hay ninguna dirección IP pública asociada a esta NIC de servidores, este tráfico nunca escribiría Hola red virtual y no llegar a servidor hello
3. Sin embargo, si se habilitó una dirección IP pública por algún motivo, la regla de NSG 2 (RDP) permitiría este tráfico.

>[!NOTE]
>servidores de back-end de tooRDP tooany en este caso, el servidor IIS de Hola se utiliza como un "cuadro salto". Primer servidor RDP toohello IIS y, a continuación, desde el servidor de hello IIS Server RDP toohello back-end.
>
>

#### <a name="denied-web-toobackend-server"></a>(*Denegado*) servidor de Web toobackend
1. Un usuario de internet trata de un archivo en AppVM01 tooaccess
2. Dado que no hay ninguna dirección IP pública asociada a esta NIC de servidores, este tráfico nunca escribiría Hola red virtual y no llegar a servidor hello
3. Si ha habilitado una dirección IP pública por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Denegado*) Búsqueda de DNS web en el servidor DNS
1. Un usuario de internet intenta toolook un registro de DNS interna en DNS01
2. Dado que no hay ninguna dirección IP pública asociada a esta NIC de servidores, este tráfico nunca escribiría Hola red virtual y no llegar a servidor hello
3. Si ha habilitado una dirección IP pública por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico (Nota: 1 de la regla (DNS) no aplicaría porque Hola solicita la dirección de origen es Hola internet y de la regla 1 solo se aplica toohello red virtual local como origen de hello)

#### <a name="denied-sql-access-on-hello-web-server"></a>(*Denegado*) el acceso a SQL en el servidor web de Hola
1. Un usuario de Internet solicita datos SQL de IIS01
2. Dado que no hay ninguna dirección IP pública asociada a esta NIC de servidores, este tráfico nunca escribiría Hola red virtual y no llegar a servidor hello
3. Si ha habilitado una dirección IP pública por algún motivo, subred de front-end de hello comienza el procesamiento de la regla de entrada:
  1. 1 de la regla de NSG (DNS) no se aplica, mover toonext regla
  2. 2 de la regla de NSG (RDP) no se aplica, mover toonext regla
  3. Aplicar NSG regla 3 (tooIIS01 Internet), el tráfico es el procesamiento de reglas permitidas, detenga
4. Tráfico alcanza el dirección IP interna de hello IIS01 (10.0.1.5)
5. Iis01 no está escuchando en el puerto 1433, por lo que no hay ninguna solicitud de toohello de respuesta

## <a name="conclusion"></a>Conclusión
En este ejemplo es una forma relativamente simple y sencillo de aislar la subred de back-end de Hola de tráfico entrante.

Puede encontrar más ejemplos y una descripción general de los límites de seguridad de red [aquí][HOME].

## <a name="references"></a>Referencias
### <a name="azure-resource-manager-template"></a>Plantilla del Administrador de recursos de Azure
Este ejemplo usa una plantilla predefinida de administrador de recursos de Azure en un repositorio de GitHub mantenido por Microsoft y abra toohello Comunidad. Esta plantilla puede implementarse sin desviarse para extraerla de GitHub, o descarga y modifica toofit sus necesidades. 

plantilla principal de Hello es en el archivo hello denominado "azuredeploy.json." Esta plantilla puede enviarse a través de PowerShell o CLI (con el archivo de asociados "azuredeploy.parameters.json" hello) toodeploy esta plantilla. Opino que hello más fácil es forma toouse Hola botón "Implementar tooAzure" en la página de README.md hello en GitHub.

plantilla de hello toodeploy que se basa en este ejemplo de GitHub y Hola portal de Azure, siga estos pasos:

1. Desde un explorador, navegue toohello [plantilla][Template]
2. Haga clic en botón de "Implementar tooAzure" hello (u Hola "Visualizar" botón toosee una representación gráfica de esta plantilla)
3. Escriba Hola cuenta de almacenamiento, el nombre de usuario y la contraseña en la hoja de parámetros de hello, a continuación, haga clic en **Aceptar**
5. Cree un grupo de recursos para esta implementación (puede usar uno existente, pero se recomienda una nueva contraseña para obtener los mejores resultados).
6. Si es necesario, cambiar la configuración de suscripción y la ubicación de hello para la red virtual.
7. Haga clic en **revisar los términos legales**, lea los términos de Hola y haga clic en **compra** tooagree.
8. Haga clic en **crear** implementación de hello toobegin de esta plantilla.
9. Una vez finalizada correctamente la implementación hello, navegue toohello que creará el grupo de recursos para esta implementación toosee Hola los recursos configurados dentro.

>[!NOTE]
>Esta plantilla permite a solo servidor RDP toohello IIS01 (Buscar Hola IP pública para IIS01 en hello Portal). servidores de back-end de tooRDP tooany en este caso, el servidor IIS de Hola se utiliza como un "cuadro salto". Primer servidor RDP toohello IIS y, a continuación, desde el servidor de hello IIS Server RDP toohello back-end.
>
>

tooremove esta implementación, Hola eliminar grupo de recursos y todos los recursos secundarios también se eliminarán.

#### <a name="sample-application-scripts"></a>Scripts de aplicación de ejemplo
Una vez que la plantilla de Hola se ejecuta correctamente, puede configurar hello web y servidor de aplicaciones con una tooallow de aplicación web simple pruebas con esta configuración de red Perimetral. tooinstall una aplicación de ejemplo para este y otros ejemplos de la red Perimetral, se aplicó en hello siguiente vínculo: [Script de aplicación de ejemplo][SampleApp]

## <a name="next-steps"></a>Pasos siguientes

* Implementar este ejemplo
* Compilar la aplicación de ejemplo de Hola
* Probar los flujos de tráfico distintos a través de esta red perimetral

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Red perimetral de entrada con grupo de seguridad de red"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md