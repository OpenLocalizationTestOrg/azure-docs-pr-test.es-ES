---
title: puerta de enlace de datos de aaaOn-local | Documentos de Microsoft
description: "Una puerta de enlace local es necesario si el servidor de Analysis Services en Azure conectará a orígenes de datos locales de tooon."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a>Conectarse a orígenes de datos locales de tooon con puerta de enlace de datos de Azure en local
puerta de enlace de datos de Hello local actúa como un puente, proporcionando la transferencia segura de datos entre orígenes de datos locales y los servidores de servicios de análisis de Azure en la nube de Hola. En suma tooworking con varios servidores de servicios de análisis de Azure en hello misma región, la versión más reciente de Hola de puerta de enlace de hello también funciona con aplicaciones de Azure lógica, Power BI, las aplicaciones de Power y Microsoft Flow. Puede asociar varios servicios en hello misma región con una sola puerta de enlace. 

 Azure Analysis Services requiere un recurso de puerta de enlace en hello misma región. Por ejemplo, si tiene servidores de Analysis Services de Azure en región de hello UU 2, necesita un recurso de puerta de enlace en la región Este de EE. 2 de Hola. Varios servidores de zona horaria del Pacífico oriental 2 pueden usar hello misma puerta de enlace.

Obtener el programa de instalación con hello de puerta de enlace de hello primera vez es un proceso de cuatro partes:

- **Descargar y ejecutar el programa de instalación**: en este paso se instala un servicio de puerta de enlace en un equipo de la organización.

- **Registrar la puerta de enlace** : en este paso, especifique un nombre y la recuperación de clave para la puerta de enlace y seleccionar una región, registrar la puerta de enlace con hello puerta de enlace de servicio en la nube.

- **Crear un recurso de puerta de enlace en Azure**: en este paso se crea un recurso de puerta de enlace en una suscripción de Azure.

- **Conectar el recurso de puerta de enlace de servidores tooyour** -una vez que tenga un recurso de puerta de enlace en su suscripción, puede empezar a conectar su tooit de servidores.

Una vez que tenga un recurso de puerta de enlace configurado para la suscripción, puede conectar varios servidores y otro tooit de servicios. Solo necesita una puerta de enlace diferentes tooinstall y crear recursos de puerta de enlace adicionales si tiene servidores u otros servicios en una región distinta.

tooget inicia inmediatamente, vea [instalar y configurar la puerta de enlace de datos local](analysis-services-gateway-install.md).

## <a name="how-it-works"></a>Funcionamiento
puerta de enlace de Hello instalar en un equipo de su organización se ejecuta como un servicio de Windows, **puerta de enlace de datos local**. Este servicio está registrado con hello servicio de nube de puerta de enlace a través de Service Bus de Azure. Luego se crea un servicio en la nube de puerta de enlace del recurso de puerta de enlace para la suscripción de Azure. Los servidores son, a continuación, los servicios de análisis Azure conectado tooyour recursos de puerta de enlace. Cuando modelos en su tooyour tooconnect de necesidad de servidor en el servidor local orígenes de datos para las consultas o procesamiento, Hola una consulta y datos flujo recorra Hola puerta de enlace recursos, Bus de servicio de Azure, servicio de puerta de enlace de datos en instalaciones locales y los orígenes de datos. 

![Cómo funciona](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

Flujo de datos y consultas:

1. Se crea una consulta de servicio de nube Hola con credenciales de hello cifrada para origen de datos local de Hola. A continuación, envió cola tooa para tooprocess de puerta de enlace de Hola.
2. servicio de nube de puerta de enlace de Hello analiza Hola consulta e inserta Hola solicitud toohello [Service Bus de Azure](https://azure.microsoft.com/documentation/services/service-bus/).
3. puerta de enlace de datos de Hello local sondea hello Azure Service Bus para las solicitudes pendientes.
4. puerta de enlace de Hello obtiene Hola consulta, descifra las credenciales de Hola y conecta a orígenes de datos toohello con esas credenciales.
5. puerta de enlace de Hello envía Hola consultar toohello origen de datos para su ejecución.
6. Hola resultados se envían de origen de datos de hello, puerta de enlace de toohello atrás y, a continuación, en el servicio de nube de Hola y el servidor.

## <a name="windows-service-account"></a>Cuenta de servicio de Windows
puerta de enlace de datos local Hello es configurado toouse *NT SERVICE\PBIEgwService* de credencial de inicio de sesión de servicio de Windows hello. De manera predeterminada, tiene Hola derecho de inicio de sesión como un servicio; en el contexto de Hola de máquina de Hola que va a instalar la puerta de enlace de hello en. Esta credencial no es Hola mismos orígenes de datos de cuenta usada tooconnect tooon local o su cuenta de Azure.  

Si tiene problemas con el servidor proxy debido tooauthentication, puede que desee toochange usuario de dominio tooa la cuenta de servicio de Windows hello o administrados cuenta de servicio.

## <a name="ports"></a>Puertos
puerta de enlace de Hello crea un Bus de servicio de tooAzure de conexión de salida. Se comunica en los puertos de salida siguientes: TCP 443 (valor predeterminado), 5671, 5672 y del 9350 al 9354.  puerta de enlace de Hello no requiere puertos de entrada.

Se recomienda direcciones IP de Hola de lista blanca de direcciones para la región de datos en el firewall. Puede descargar hello [lista de IP de centro de datos de Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). La lista se actualiza semanalmente.

> [!NOTE]
> Direcciones IP de Hello enumerados en la lista de IP de centro de datos de Azure de Hola están en la notación CIDR. Por ejemplo, 10.0.0.0/24 no significa de 10.0.0.0 a 10.0.0.24. Obtener más información sobre hello [la notación CIDR](http://whatismyipaddress.com/cidr).
>
>

siguiente Hola es nombres de dominio de hello completo utilizados por la puerta de enlace de Hola.

| Nombres de dominio | Puertos de salida | Descripción |
| --- | --- | --- |
| *.powerbi.com |80 |Instalador de hello toodownload utiliza HTTP. |
| *.powerbi.com |443 |HTTPS |
| *. analysis.windows.net |443 |HTTPS |
| *.login.windows.net |443 |HTTPS |
| *.servicebus.windows.net |5671-5672 |Advanced Message Queuing Protocol (AMQP) |
| *.servicebus.windows.net |443, 9350-9354 |Agentes de escucha en Service Bus Relay sobre TCP (requiere 443 para la adquisición del token de Access Control) |
| *.frontend.clouddatahub.net |443 |HTTPS |
| *.core.windows.net |443 |HTTPS |
| login.microsoftonline.com |443 |HTTPS |
| *.msftncsi.com |443 |Usar tootest conectividad a internet si la puerta de enlace de hello es inaccesible por hello servicio Power BI. |
| *.microsoftonline-p.com |443 |Se utiliza para la autenticación dependiendo de la configuración. |

### <a name="force-https"></a>Forzar la comunicación HTTPS con Azure Service Bus
Puede forzar hello toocommunicate de puerta de enlace con el Bus de servicio de Azure mediante HTTPS en lugar de TCP directo; Sin embargo, si lo hace por lo que puede reducir considerablemente rendimiento. Puede modificar hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* archivo cambiando el valor de Hola de `AutoDetect` demasiado`Https`. Este archivo suele encontrarse en *C:\Archivos de programa\Puerta de enlace de datos local*.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <a name="faq"></a>Preguntas más frecuentes

### <a name="general"></a>General

**Preguntas**: ¿necesito una puerta de enlace para los orígenes de datos en la nube de hello, como la base de datos de SQL Azure? <br/>
**R:** No. Una puerta de enlace conecta a orígenes de datos de tooon locales solo.

**¿Preguntas**: puerta de enlace de hello tiene toobe instalado en hello mismo equipo como origen de datos de hello? <br/>
**R:** No. puerta de enlace de Hello conecta toohello origen de datos usando la información de conexión de Hola que proporcionó. Considere la posibilidad de puerta de enlace de hello como una aplicación de cliente en este sentido. Hello puerta de enlace solo necesita Hola capacidad tooconnect toohello nombre del servidor que se proporcionó, normalmente en hello misma red.

<a name="why-azure-work-school-account"></a>

**Preguntas**: ¿por qué necesita toouse un trabajo o escuela cuenta toosign en? <br/>
**Un**: solo puede usar un trabajo de Azure o educativa cuenta cuando se instala la puerta de enlace de datos de hello en local. Su cuenta de inicio de sesión se almacena en un inquilino administrado por Azure Active Directory (Azure AD). Por lo general, nombre principal de la cuenta de Azure AD usuario (UPN) coincide con dirección de correo electrónico de Hola.

**P**: ¿Dónde se almacenan mis credenciales? <br/>
**Un**: credenciales de Hola que especifique para un origen de datos se cifran y almacenan en hello puerta de enlace de servicio en la nube. las credenciales de Hola se descifran en la puerta de enlace de datos de hello en local.

**P**: ¿Hay algún requisito con respecto al ancho de banda de red? <br/>
**R**: Es aconsejable que la conexión de red tenga buen rendimiento. Cada entorno es diferente y cantidad de Hola de datos que se envían afecta a los resultados de Hola. Usar ExpressRoute puede ayudar a tooguarantee un nivel de rendimiento entre hello centros de datos de Azure y local.
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
**Un**: en los servicios, puerta de enlace de Hola se llama servicio de puerta de enlace de datos local.

**¿Preguntas**: Hola a servicio de Windows de puerta de enlace que se ejecutan con una cuenta de Azure Active Directory? <br/>
**R:** No. Hola servicio de Windows debe tener una cuenta de Windows válida. De forma predeterminada, el servicio de Hola se ejecuta con hello SID de servicio, NT SERVICE\PBIEgwService.

### <a name="high-availability"></a>Alta disponibilidad y recuperación ante desastres

**P**: ¿Cuáles son las opciones de recuperación ante desastres disponibles? <br/>
**Un**: puede usar toorestore de clave de recuperación de Hola o mover una puerta de enlace. Cuando se instala la puerta de enlace de hello, especifique la clave de recuperación de Hola.

**Preguntas**: ¿cuál es la ventaja de Hola de clave de recuperación de hello? <br/>
**Un**: clave de recuperación de hello proporciona una manera toomigrate o recuperar la configuración de puerta de enlace después de un desastre.

## <a name="troubleshooting"></a>Solución de problemas

**Preguntas**: ¿Cómo puedo ver las consultas que se están enviando el origen de datos local de toohello? <br/>
**Un**: para habilitar el seguimiento de la consulta, que incluye las consultas de Hola que se envían. Recuerde consulta toochange remontarse toohello valor original cuando haya finalizado la solución de problemas. Si lo deja activado, crea registros de mayor tamaño.

También puede examinar las herramientas de que dispone su origen de datos para el seguimiento de consultas. Por ejemplo, puede utilizar Eventos extendidos o SQL Profiler en SQL Server y Analysis Services.

**¿Preguntas**: donde se encuentran los registros de puerta de enlace de hello? <br/>
**R**: Consulte la sección Registros en este mismo tema.

### <a name="update"></a>Actualizar la versión más reciente de toohello

Muchos problemas pueden surgir cuando la versión de la puerta de enlace de Hola quede anticuado. Como buena práctica general, asegúrese de utilizar la versión más reciente de Hola. Si no ha actualizado la puerta de enlace de Hola durante un mes o más, podría pensar en instalar la versión más reciente de Hola de puerta de enlace de Hola y vea si puede reproducir el problema de Hola.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Error: No se pudo tooadd toogroup de usuario. (Usuarios del registro de rendimiento de-2147463168 PBIEgwService)

Podría obtener este error si intentas puerta de enlace de tooinstall hello en un controlador de dominio que no es compatible. Asegúrese de que implemente la puerta de enlace de hello en un equipo que no es un controlador de dominio.

## <a name="logs"></a>Registros

Los archivos de registro son un recurso importante a la hora de solucionar problemas.

#### <a name="enterprise-gateway-service-logs"></a>Registros del servicio de puerta de enlace empresarial

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a>Registros de configuración

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a>Registros de eventos

Puede encontrar registros de Data Management Gateway y PowerBIGateway en hello **registros de aplicaciones y servicios**.


## <a name="telemetry"></a>Telemetría
La telemetría puede usarse para tareas de supervisión y solución de problemas. De forma predeterminada

**tooturn datos de telemetría**

1.  Compruebe el directorio del cliente de puerta de enlace Hola local datos en el equipo de Hola. Normalmente, es **%systemdrive%\Program Files\On-premises data gateway**. O bien, puede abrir una consola de servicios y compruebe tooexecutable de ruta de acceso de hello: una propiedad del servicio de puerta de enlace de datos de hello local.
2.  En el archivo Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config de hello directorio del cliente. Cambiar hello SendTelemetry configuración tootrue.
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  Guarde los cambios y reinicie el servicio de Windows hello: el servicio de puerta de enlace de datos local.




## <a name="next-steps"></a>Pasos siguientes
* [Administración de Analysis Services](analysis-services-manage.md)
* [Obtención de datos de Azure Analysis Services](analysis-services-connect.md)
