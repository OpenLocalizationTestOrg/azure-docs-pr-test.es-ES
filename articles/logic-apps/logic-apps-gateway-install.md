---
title: puerta de enlace de aaaInstall local datos - Azure Logic Apps | Documentos de Microsoft
description: "Antes de acceder a orígenes de datos de forma local, instalar la puerta de enlace de datos de hello en local para la transferencia de datos rápidamente y cifrado entre los orígenes de datos de forma local y las aplicaciones lógicas"
keywords: "obtener acceso a datos, local, transferencia de datos, cifrado, orígenes de datos"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a>Hola de instalación local puerta de enlace de datos para las aplicaciones lógicas de Azure

Antes de que las aplicaciones lógicas pueden tener acceso a orígenes de datos de forma local, debe instalar y configurar la puerta de enlace de datos de hello en local. puerta de enlace de Hello actúa como un puente que permite el cifrado entre los sistemas locales y las aplicaciones lógicas y transferencia de datos rápidamente. puerta de enlace de Hello transmite datos desde orígenes locales en los canales cifrados a través de hello Azure Service Bus. Todo el tráfico se origina como proteger el tráfico saliente desde el agente de puerta de enlace de Hola. Obtenga más información sobre [cómo funciona la puerta de enlace de datos de hello](#gateway-cloud-service).

puerta de enlace de Hello es compatible con orígenes de datos de las conexiones toothese local:

*   BizTalk Server 2016
*   DB2  
*   Sistema de archivos
*   Informix
*   MQ
*   MySQL
*   Base de datos de Oracle
*   PostgreSQL
*   Servidor de aplicaciones de SAP 
*   Servidor de mensajes de SAP
*   SharePoint
*   SQL Server
*   Teradata

Estos pasos muestra cómo toofirst instalación Hola local puerta de enlace de datos antes de [establecer una conexión entre la puerta de enlace de Hola y las aplicaciones lógicas](./logic-apps-gateway-connection.md). Para obtener más información sobre las conexiones admitidas, consulte [Conectores para Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list). 

Para obtener información acerca de cómo toouse Hola puerta de enlace con otros servicios, vea estos artículos:

*   [Puerta de enlace de datos local de Microsoft Power BI](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Puerta de enlace de datos local de Azure Analysis Services](../analysis-services/analysis-services-gateway.md)
*   [Puerta de enlace de datos local de Microsoft Flow](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Administración de una puerta de enlace de datos local en Microsoft PowerApps](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a>Requisitos

**Mínimos**:

* .NET Framework 4.5
* versión de 64 bits de Windows 7 o Windows Server 2008 R2 (o posterior)

**Recomendaciones**:

* CPU de 8 núcleos
* 8 GB de memoria
* versión de 64 bits de Windows 2012 R2 (o posterior)

**Consideraciones importantes**:

* Hola de instalación local de puerta de enlace de datos solo en un equipo local.
No se puede instalar la puerta de enlace de hello en un controlador de dominio.

   > [!TIP]
   > No tiene puerta de enlace de tooinstall hello en hello mismo equipo que el origen de datos. latencia de toominimize, puede instalar puerta de enlace de hello más próximo como origen de datos de tooyour posible, o en hello mismo equipo, suponiendo que tenga permisos.

* No instale la puerta de enlace de hello en un equipo que se desactiva, deja de toosleep o no se conecta toohello Internet porque no se puede ejecutar la puerta de enlace de hello en esas circunstancias. Además, el rendimiento de la puerta de enlace podría verse afectado en una red inalámbrica.

* Durante la instalación, debe iniciar sesión con una [cuenta profesional o educativa](https://docs.microsoft.com/azure/active-directory/sign-up-organization) que está administrada por Azure Active Directory (Azure AD), no una cuenta de Microsoft. 

  Tiene toouse Hola mismo trabajo o escuela hello más tarde en Azure de cuenta portal al crear y asociar un recurso de puerta de enlace con la instalación de puerta de enlace. A continuación, seleccione este recurso de puerta de enlace al crear conexión Hola entre el origen de datos lógica hello y aplicaciones locales. [¿Por qué debo usar una cuenta profesional o educativa de Azure AD?](#why-azure-work-school-account)

  > [!TIP]
  > Si se suscribió a una oferta de Office 365 y no proporcionó su correo electrónico profesional real, la dirección de inicio de sesión podría tener un aspecto similar al siguiente: jeff@contoso.onmicrosoft.com. 

* Si tiene una puerta de enlace existente que configura con un instalador que es anterior a la versión 14.16.6317.4, no se puede cambiar la ubicación de la puerta de enlace Installer más reciente de ejecución Hola. Sin embargo, puede usar hello más reciente instalador tooset una nueva puerta de enlace con la ubicación de Hola que desea en su lugar.
  
  Si tiene un instalador de puerta de enlace que es anterior a la versión 14.16.6317.4, pero no ha instalado la puerta de enlace, puede descargar y utilice el instalador de hello más reciente.

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a>Instalar la puerta de enlace de datos de Hola

1.  [Descargue y ejecute el instalador de puerta de enlace de hello en un equipo local](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).

2. Revise y acepte los términos de Hola de uso y declaración de privacidad.

3. Especifique la ruta de acceso de hello en el equipo local donde desea que la puerta de enlace de tooinstall Hola.

4. Cuando se le solicite, inicie sesión con su cuenta profesional o educativa de Azure, no con una cuenta de Microsoft.

   ![Inicio de sesión con una cuenta profesional o educativa de Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. Registrar la puerta de enlace instalada con hello [servicio de nube de puerta de enlace](#gateway-cloud-service). Elija **Registrar una nueva puerta de enlace en este equipo**.

   servicio de nube de puerta de enlace de Hello cifra y almacena sus credenciales de origen de datos y los detalles de la puerta de enlace. 
   servicio de Hello también enruta las consultas y los resultados entre la aplicación lógica, puerta de enlace de datos de hello en local y el origen de datos de forma local.

6. Especifique un nombre para la instalación de la puerta de enlace. Cree una clave de recuperación y luego confírmela. 

   > [!IMPORTANT] 
   > La clave de recuperación debe contener al menos ocho caracteres. Asegúrese de guardar y mantenga la clave de hello en un lugar seguro. También necesitará esta clave cuando se desea toomigrate, restaurar o tomar a través de una puerta de enlace existente.

   1. Elija la región de toochange Hola predeterminados para el servicio de nube de puerta de enlace de Hola y utilizados por la instalación de puerta de enlace, Service Bus de Azure **cambiar región**.

      ![Cambio de región](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      Hola predeterminado Hola región está asociado con el inquilino de Azure AD.

   2. En el siguiente panel hello, abra hello **Seleccionar región** demasiado elija una región diferente.

      ![Seleccione otra región.](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      Por ejemplo, podría seleccionar Hola misma región que la aplicación lógica o, por lo que puede reducir la latencia del origen de datos de local de hello seleccione región más cercanas tooyour. El recurso de puerta de enlace y la aplicación lógica pueden tener ubicaciones distintas.

      > [!IMPORTANT]
      > No puede cambiar esta región después de la instalación. Esta región también determina y restringe la ubicación de Hola donde puede crear Hola recursos de Azure para la puerta de enlace. Por lo que cuando se crea el recurso de puerta de enlace de Azure, asegúrese de que ubicación del recurso Hola coincide con región Hola que seleccionó durante la instalación de puerta de enlace.
      > 
      > Si desea toouse una región distinta para la puerta de enlace más adelante, debe configurar una puerta de enlace.

   3. Cuando esté listo, elija **Hecho**.

7. Ahora siga estos pasos en hello portal de Azure para que pueda [crear un recurso de Azure para la puerta de enlace](../logic-apps/logic-apps-gateway-connection.md). 

Obtenga más información sobre [cómo funciona la puerta de enlace de datos de hello](#gateway-cloud-service).

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a>Migrar, restaurar o controlar una puerta de enlace existente

tooperform estas tareas, debe tener la clave de recuperación de Hola que se especificó cuando se instaló la puerta de enlace de Hola.

1. En el menú Inicio del equipo, elija **Puerta de enlace de datos locales**.

2. Después de hello instalador se abre, inicie sesión con hello mismo Azure trabajar o cuenta organizativa que antes eran usa puerta de enlace de tooinstall Hola.

3. Elija **Migrar, restaurar o controlar una puerta de enlace existente**.

4. Proporcione la clave de nombre y la recuperación de Hola para puerta de enlace de Hola que desee toomigrate, restaurar o sustituir sobre.

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a>Reinicie la puerta de enlace de Hola

puerta de enlace de Hola se ejecuta como un servicio de Windows. Como cualquier otro servicio de Windows, puede iniciar y detener servicio Hola de varias maneras. Por ejemplo, puede abrir un símbolo del sistema con permisos elevados en el equipo de Hola donde se ejecuta la puerta de enlace de Hola y ejecutar cualquiera de estos comandos:

* servicio de hello toostop, ejecute este comando:
  
    `net stop PBIEgwService`

* servicio de hello toostart, ejecute este comando:
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a>Cuenta de servicio de Windows

puerta de enlace de datos de Hello local se configura toouse `NT SERVICE\PBIEgwService` para Windows hello credenciales de inicio de sesión del servicio. De forma predeterminada, puerta de enlace de hello tiene "Hola iniciar sesión como servicio" directamente para la máquina de Hola donde se instala la puerta de enlace de Hola.

> [!NOTE]
> Hola cuenta de servicio de Windows difiere de cuenta de hello usada para conectarse a orígenes de datos locales de tooon y de hello Azure trabajo o cuenta organizativa utiliza toosign en servicios de toocloud.

## <a name="configure-a-firewall-or-proxy"></a>Configuración de un firewall o proxy

puerta de enlace de Hello crea una conexión de salida demasiado [Service Bus de Azure](https://azure.microsoft.com/services/service-bus/). información de proxy de tooprovide para la puerta de enlace, consulte [configurar el proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).

toocheck si el firewall o proxy, puede bloquear las conexiones, confirmar si su equipo puede conectar realmente toohello hello y internet [Service Bus de Azure](https://azure.microsoft.com/services/service-bus/). Desde un símbolo del sistema de PowerShell, ejecute este comando:

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> Este comando sólo comprueba la conectividad de red y conectividad toohello Service Bus de Azure. Por lo que el comando hello no tiene nada toodo con puerta de enlace de Hola o un servicio de nube de puerta de enlace de Hola que cifra y almacena sus credenciales y detalles de la puerta de enlace. 
>
> Además, este comando solo está disponible en Windows Server 2012 R2 o posterior y Windows 8.1 o posterior. En versiones anteriores del sistema operativo, puede usar Telnet demasiado probar la conectividad. Obtenga más información sobre [Azure Service Bus y soluciones híbridas](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

Los resultados deberían ser ejemplo toothis similar:

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

Si **TcpTestSucceeded** no está establecido demasiado**True**, puede estar bloqueado por un firewall. Si lo desea, toobe completa, sustituir hello **ComputerName** y **puerto** valores con valores de hello aparecen bajo [configurar puertos](#configure-ports) en este tema.

firewall de Hello también podría bloquear las conexiones que Hola que Service Bus de Azure hace toohello centros de datos de Azure. Si se produce esta situación, aprobar (desbloquear) todas Hola direcciones IP para esos centros de datos en su región. Para esas direcciones IP, [lista de direcciones aquí de get hello Azure IP](https://www.microsoft.com/download/details.aspx?id=41653).

## <a name="configure-ports"></a>Configuración de los puertos

puerta de enlace de Hello crea una conexión de salida demasiado[Service Bus de Azure](https://azure.microsoft.com/services/service-bus/) y se comunica en los puertos de salida: TCP 443 (valor predeterminado), 5671, 5672 y 9350 a 9354. puerta de enlace de Hello no requiere puertos de entrada. Obtenga más información sobre [Azure Service Bus y soluciones híbridas](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

| NOMBRES DE DOMINIO | PUERTOS DE SALIDA | DESCRIPCIÓN |
| --- | --- | --- |
| *. analysis.windows.net | 443 | HTTPS | 
| *.login.windows.net | 443 | HTTPS | 
| *.servicebus.windows.net | 5671-5672 | Advanced Message Queuing Protocol (AMQP) | 
| *.servicebus.windows.net | 443, 9350-9354 | Agentes de escucha en Service Bus Relay sobre TCP (requiere 443 para la adquisición del token de Access Control) | 
| *.frontend.clouddatahub.net | 443 | HTTPS | 
| *.core.windows.net | 443 | HTTPS | 
| login.microsoftonline.com | 443 | HTTPS | 
| *.msftncsi.com | 443 | Usar tootest conectividad a internet cuando puerta de enlace de hello es inaccesible por hello servicio Power BI. | 

Si tiene direcciones IP de tooapprove en lugar de dominios de hello, puede descargar y usar hello [lista de intervalos de direcciones IP de centro de datos de Azure de Microsoft](https://www.microsoft.com/download/details.aspx?id=41653). En algunos casos, las conexiones de Bus de servicio de Azure de Hola se realizan con la dirección IP en lugar de nombres de dominio completo.

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a>¿Cómo funciona la puerta de enlace de datos de hello?

puerta de enlace de datos de Hello facilita la comunicación rápida y segura entre la lógica de aplicación, servicio de nube de puerta de enlace de Hola y el origen de datos local. 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

Por lo que cuando el usuario hello en la nube de hello interactúa con un elemento que se ha conectado tooyour local de origen de datos:

1. servicio de nube de puerta de enlace de Hola crea una consulta, junto con las credenciales de hello cifrada para el origen de datos de hello y envía la cola de toohello de consulta de Hola para hello tooprocess de puerta de enlace.

2. servicio de nube de puerta de enlace de Hello analiza la consulta de Hola e inserta Hola solicitud toohello Service Bus de Azure.

3. puerta de enlace de datos de Hello local sondea hello Azure Service Bus para las solicitudes pendientes.

4. puerta de enlace de Hello obtiene Hola consulta, descifra las credenciales de Hola y conecta el origen de datos de toohello con esas credenciales.

5. puerta de enlace de Hello envía Hola consultar toohello origen de datos para su ejecución.

6. resultados de Hola se envían desde el origen de datos de hello, puerta de enlace de toohello atrás y, a continuación, servicio de nube de puerta de enlace de toohello. Hello servicio de nube de puerta de enlace, a continuación, usa los resultados de Hola.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

### <a name="general"></a>General

**Preguntas**: ¿necesito una puerta de enlace para los orígenes de datos en la nube de hello, como SQL Azure? <br/>
**R:** No. Una puerta de enlace conecta a orígenes de datos de tooon locales solo.

**¿Preguntas**: puerta de enlace de hello tiene toobe instalado en hello mismo equipo como origen de datos de hello? <br/>
**R:** No. puerta de enlace de Hello conecta toohello origen de datos usando la información de conexión de Hola que proporcionó. Considere la posibilidad de puerta de enlace de hello como una aplicación de cliente en este sentido. puerta de enlace de Hello solo necesita Hola capacidad tooconnect toohello nombre del servidor que se proporcionó.

<a name="why-azure-work-school-account"></a>

**Preguntas**: ¿por qué debo utiliza un trabajo de Azure o toosign de cuenta en la escuela? <br/>
**Un**: solo puede usar un trabajo de Azure o educativa cuenta cuando se instala la puerta de enlace de datos de hello en local. Su cuenta de inicio de sesión se almacena en un inquilino administrado por Azure Active Directory (Azure AD). Por lo general, nombre principal de la cuenta de Azure AD usuario (UPN) coincide con dirección de correo electrónico de Hola.

**P**: ¿Dónde se almacenan mis credenciales? <br/>
**Un**: credenciales de Hola que especifique para un origen de datos se cifran y almacenan en el servicio de nube de puerta de enlace de Hola. las credenciales de Hola se descifran en la puerta de enlace de datos de hello en local.

**P**: ¿Hay algún requisito con respecto al ancho de banda de red? <br/>
**R**: Se recomienda que la conexión de red tenga buen rendimiento. Cada entorno es diferente y cantidad de Hola de datos que se envían afecta a los resultados de Hola. Usar ExpressRoute puede ayudar a tooguarantee un nivel de rendimiento entre hello centros de datos de Azure y local.
Puede usar Hola herramienta de otro fabricante Azure Speed Test aplicación toohelp medidor su rendimiento.

**Preguntas**: ¿qué es la latencia de Hola para consultas tooa datos de origen en ejecución de puerta de enlace de hello? ¿Cuál es la mejor arquitectura de hello? <br/>
**Un**: latencia de red tooreduce, puerta de enlace de instalación hello como origen de datos de toohello cerrar como sea posible. Si puede instalar la puerta de enlace de hello en el origen de datos real de hello, esta proximidad reduce la latencia de hello introducida. Considere la posibilidad de centros de datos de hello demasiado. Por ejemplo, si el servicio usa el centro de datos de hello oeste de Estados Unidos y tiene SQL Server hospedado en una máquina virtual de Azure, la VM de Azure deben estar en hello West US demasiado. Esta proximidad reduce la latencia y evita los cargos de salida en hello VM de Azure.

**Preguntas**: ¿de qué resultados enviados toohello atrás en la nube? <br/>
**Un**: los resultados se envían a través de hello Azure Service Bus.

**Preguntas**: ¿hay ninguna puerta de enlace de toohello de las conexiones entrantes de nube de hello? <br/>
**R:** No. puerta de enlace de Hello utiliza conexiones salientes tooAzure Bus de servicio.

**P**: ¿Qué sucede si bloqueo las conexiones de salida? ¿Qué necesito tooopen? <br/>
**Un**: ver los puertos de Hola y hosts que Hola usos de la puerta de enlace.

**¿Preguntas**: lo que se denomina el servicio de Windows de hello real?<br/>
**Un**: en servicios, puerta de enlace de Hola se denomina servicio Power BI Enterprise Gateway.

**¿Preguntas**: Hola a servicio de Windows de puerta de enlace que se ejecutan con una cuenta de Azure Active Directory? <br/>
**R:** No. Hola servicio de Windows debe tener una cuenta de Windows válida. De forma predeterminada, el servicio de Hola se ejecuta con hello SID de servicio, NT SERVICE\PBIEgwService.

### <a name="high-availability-and-disaster-recovery"></a>Alta disponibilidad y recuperación ante desastres

**P**: ¿Cuáles son las opciones de recuperación ante desastres disponibles? <br/>
**Un**: puede usar toorestore de clave de recuperación de Hola o mover una puerta de enlace. Cuando se instala la puerta de enlace de hello, especifique la clave de recuperación de Hola.

**Preguntas**: ¿cuál es la ventaja de Hola de clave de recuperación de hello? <br/>
**Un**: clave de recuperación de hello proporciona una manera toomigrate o recuperar la configuración de puerta de enlace después de un desastre.

**Preguntas**: ¿existen planes para habilitar escenarios de alta disponibilidad con puerta de enlace de hello? <br/>
**Un**: estos escenarios se encuentran en la guía básica de hello, pero aún no tenemos una escala de tiempo.

## <a name="troubleshooting"></a>Solución de problemas

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

**Preguntas**: ¿Cómo puedo ver las consultas que se están enviando el origen de datos local de toohello? <br/>
**Un**: para habilitar el seguimiento de la consulta, que incluye las consultas de Hola que se envían. Recuerde consulta toochange remontarse toohello valor original cuando haya finalizado la solución de problemas. Si lo deja activado, crea registros de mayor tamaño.

También puede examinar las herramientas de que dispone su origen de datos para el seguimiento de consultas. Por ejemplo, puede utilizar Eventos extendidos o SQL Profiler en SQL Server y Analysis Services.

**¿Preguntas**: donde se encuentran los registros de puerta de enlace de hello? <br/>
**R**: Consulte la sección Herramientas de este mismo tema.

### <a name="update-toohello-latest-version"></a>Actualizar la versión más reciente de toohello

Muchos problemas pueden surgir cuando la versión de la puerta de enlace de Hola quede anticuado. Como buena práctica general, asegúrese de utilizar la versión más reciente de Hola. Si no ha actualizado la puerta de enlace de Hola durante un mes o más, podría pensar en instalar la versión más reciente de Hola de puerta de enlace de Hola y vea si puede reproducir el problema de Hola.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Error: No se pudo tooadd toogroup de usuario. (Usuarios del registro de rendimiento de-2147463168 PBIEgwService)

Podría obtener este error si intentas puerta de enlace de tooinstall hello en un controlador de dominio que no es compatible. Asegúrese de que implemente la puerta de enlace de hello en un equipo que no es un controlador de dominio.

## <a name="tools"></a>Herramientas

### <a name="collect-logs-from-hello-gateway-configurer"></a>Recopilar registros de configurer de puerta de enlace de Hola

Puede recopilar varios registros para puerta de enlace de Hola. Siempre se inician con registros de Hola!

#### <a name="installer-logs"></a>Registros del instalador

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a>Registros de configuración

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a>Registros del servicio de puerta de enlace empresarial

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a>Registros de eventos

Puede encontrar registros de Data Management Gateway y PowerBIGateway en hello **registros de aplicaciones y servicios**.

### <a name="fiddler-trace"></a>Seguimiento de Fiddler

[Fiddler](http://www.telerik.com/fiddler) es una herramienta gratuita de Telerik que supervisa el tráfico HTTP. Puede ver este tráfico mediante el servicio de Power BI desde el equipo cliente de Hola Hola. Este servicio puede mostrar errores y otra información relacionada.

## <a name="next-steps"></a>Pasos siguientes
    
* [Conectar datos tooon locales desde las aplicaciones lógicas](../logic-apps/logic-apps-gateway-connection.md)
* [Características de Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Conectores para Azure Logic Apps](../connectors/apis-list.md)
