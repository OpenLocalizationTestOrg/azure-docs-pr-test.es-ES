---
title: aaaIssuer nombre y clave del emisor en servicios de BizTalk | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooretrieve nombre de emisor y clave del emisor de Bus de servicio o de Control de acceso (ACS) en servicios de BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>Servicios de BizTalk: nombre del emisor y clave del emisor

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Servicios de BizTalk de Azure usa Hola nombre de emisor de Bus de servicio y clave del emisor y Hola nombre del emisor de Control de acceso y clave del emisor. Concretamente:

| Tarea | Nombre de emisor y clave de emisor |
| --- | --- |
| Implementación de la aplicación desde Visual Studio |Nombre y clave de emisor del servicio de control de acceso |
| Hola configurar Portal de servicios de BizTalk de Azure |Nombre y clave de emisor del servicio de control de acceso |
| Crear retransmisiones de LOB con hello servicios del adaptador de BizTalk en Visual Studio |Nombre de emisor y clave de emisor del bus de servicio |

Este tema enumeran Hola pasos tooretrieve Hola nombre del emisor y clave del emisor. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Nombre y clave de emisor del servicio de control de acceso
Hola, nombre del emisor de Control de acceso y la clave de emisor se utilizan siguiendo hello:

* La aplicación de servicio de BizTalk de Azure creada en Visual Studio: toosuccessfully implementar la aplicación de BizTalk Service en Visual Studio tooAzure, escriba Hola nombre del emisor de Control de acceso y la clave de emisor. 
* Hola Portal de servicios de BizTalk de Azure: al crear un BizTalk Service y abra Hola Portal de servicios de BizTalk, el nombre del emisor de Control de acceso y clave del emisor se registra automáticamente para las implementaciones con Hola mismos valores de Control de acceso.

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>Obtener Hola nombre del emisor de Control de acceso y la clave de emisor

ACS toouse para la autenticación y get Hola valores de nombre del emisor y clave del emisor, incluyen hello pasos generales:

1. Instalar hello [cmdlets de Powershell de Azure](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Agregue su cuenta de Azure: `Add-AzureAccount`
3. Devuelva el nombre de su suscripción: `get-azuresubscription`
4. Seleccione su suscripción: `select-azuresubscription <name of your subscription>` 
5. Creación de un espacio de nombres nuevo: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    Ejemplo:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Cuando se crea Hola nuevo espacio de nombres ACS (que puede tardar varios minutos), valores de nombre del emisor y clave del emisor de Hola se muestran en la cadena de conexión de hello: 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize:  
Nombre de emisor = SharedSecretIssuer  
Clave de emisor = SharedSecretKey

Más información sobre la hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Nombre de emisor y clave de emisor del bus de servicio
Los servicios de adaptador de BizTalk usan el nombre y la clave de emisor del bus de servicio. En el proyecto de servicios de BizTalk en Visual Studio, utilice sistema de línea de negocio (LOB) de hello servicios del adaptador BizTalk tooconnect tooan local. tooconnect, crear hello retransmisión de LOB y escriba los detalles del sistema LOB. Al hacerlo, también escriba Hola nombre de emisor de Bus de servicio y la clave de emisor.

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>Hola tooretrieve nombre de emisor de Bus de servicio y la clave de emisor
1. Inicie sesión en toohello [portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. En el panel de navegación izquierdo de hello, seleccione **Bus de servicio**.
3. Seleccione su espacio de nombres. En la barra de tareas de hello, seleccione **información de conexión**. Esto muestra hello **emisor predeterminado** (nombre del emisor) y **clave predeterminada** (clave del emisor). Sus valores se pueden copiar.  

toosummarize:  
Nombre de emisor = Emisor predeterminado  
Clave de emisor = Clave predeterminada

## <a name="next"></a>Pasos siguientes
Otros temas acerca de los servicios de BizTalk de Azure:

* [Hola instalar SDK de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Tutoriales: Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Otras referencias
* [Cómo: usar el servicio de administración de ACS tooConfigure las identidades de servicio](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Servicios de BizTalk: gráfico del estado de aprovisionamiento](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Servicios de BizTalk: pestañas Panel, Monitor y Escala](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Servicios de BizTalk: copias de seguridad y restauración](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Servicios de BizTalk: limitaciones](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

