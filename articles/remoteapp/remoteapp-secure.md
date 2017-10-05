---
title: "Protección de aplicaciones y recursos en Azure RemoteApp | Microsoft Docs"
description: "Obtenga información sobre cómo bloquear las aplicaciones y recursos en Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 1c052906788f0f4fe4ca9fd6d3af63336245174a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Protección de aplicaciones y recursos en Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Azure RemoteApp proporciona a los usuarios acceso a aplicaciones de Windows administradas centralmente, lo cual le permite controlar lo que los usuarios pueden y no pueden hacer.  Esto es especialmente útil cuando el usuario se conecta desde un dispositivo no administrado (por ejemplo, su Macbook personal) y desea controlar el acceso o la experiencia de los usuarios.

Por ejemplo, si está usando Active Directory para la autenticación de usuarios y desea evitar que los usuarios copien datos fuera de una aplicación, puede configurar una directiva de grupo de escritorio remoto para evitar que los usuarios copien datos.

Otro ejemplo es si desea bloquear el acceso a Internet para una aplicación determinada de la colección. Puede crear una regla de Firewall de Windows que bloquea el acceso al crear la imagen de la colección.

## <a name="implementation-options"></a>Opciones de implementación
  A continuación se facilitan las opciones de implementación clave, que se pueden usar por separado o conjuntamente según sea necesario:

1. Si la colección de RemoteApp está unida al dominio, puede aplicar cualquier [Directiva de grupo](https://technet.microsoft.com/library/cc725828.aspx) (a excepción de las directivas de tiempo de espera Inactivo y Desconexión descritas [aquí](../azure-subscription-service-limits.md)).
2. Como alternativa a la directiva de grupo (si la colección no está unida al dominio o no tiene los privilegios adecuados en Active Directory), puede configurar [Directivas locales](https://technet.microsoft.com/library/cc775702.aspx) en su imagen de plantilla.  Tenga en cuenta que las directivas de grupo superan a las locales cuando hay un conflicto.
3. Algunos valores de configuración de SO/aplicación no son configurables a través de la directiva, pero se pueden establecer mediante la clave de registro con la [herramienta RegEdit](remoteapp-hybridtrouble.md) durante la configuración de la imagen de la plantilla.
4. Puede usar el [Firewall de Windows](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) para controlar el acceso de red a y desde el equipo donde se ejecuta la aplicación. Simplemente asegúrese de no bloquear las direcciones URL y los puertos definidos aquí.
5. Puede usar [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) para controlar qué aplicaciones y archivos pueden ejecutar los usuarios. Por ejemplo, los usuarios más experimentados pueden averiguar cómo ejecutar aplicaciones no publicadas por usted pero que están disponibles en la imagen que usó para crear la recopilación (AppLocker puede bloquear esto).

## <a name="detailed-information"></a>Información detallada
* Es probable que las siguientes directivas RDS sean más útiles:
  * [Redirección de dispositivos y recursos](https://technet.microsoft.com/library/ee791794.aspx)
  * [Redirección de impresoras](https://technet.microsoft.com/library/ee791784.aspx)
  * [Perfiles](https://technet.microsoft.com/library/ee791865.aspx).
* Tenga en cuenta que la configuración de las redirecciones a través del módulo de RemoteApp PowerShell (tal como se ve [aquí](remoteapp-redirection.md)) se basa en el equipo cliente para aplicar la directiva, por lo que si la seguridad es el objetivo principal, deberá aplicar la directiva mediante la directiva local de imagen de plantilla o mediante la directiva de grupo.
* [Directivas de Windows Server 2012 R2](https://technet.microsoft.com/library/hh831791.aspx).
* [Directivas de Office 2013](https://technet.microsoft.com/library/cc178969.aspx) (incluido [cómo personalizar la barra de herramientas de Office](https://technet.microsoft.com/library/cc179143.aspx)).

