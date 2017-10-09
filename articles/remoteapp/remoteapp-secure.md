---
title: aaaSecure aplicaciones y recursos de Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo toolock hacia abajo de aplicaciones y recursos de Azure RemoteApp"
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
ms.openlocfilehash: 26325826e92855a12a0087f19a3e32cbe1116449
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Protección de aplicaciones y recursos en Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

RemoteApp de Azure proporciona a los usuarios acceso administrado toocentrally aplicaciones de Windows, que le permite controlar lo que los usuarios pueden y no se pueden hacer.  Esto es especialmente útil cuando el usuario de hello conectarse desde un dispositivo no administrado (por ejemplo, su Macbook personal) y acceso de los usuarios desean toocontrol Hola o experimentar.

Por ejemplo, si está utilizando Active Directory para la autenticación de usuario y desea tooprevent los usuarios finales de copiar datos en una aplicación, puede configurar una directiva de grupo de escritorio remoto tooblock los usuarios copiar datos.

Otro ejemplo es si desea que el acceso a internet de tooblock para una aplicación determinada en la colección. Puede crear una regla de Firewall de Windows que bloques Hola acceso al crear la imagen de hello para la colección.

## <a name="implementation-options"></a>Opciones de implementación
  Estas son opciones de implementación clave hello, que pueden utilizar por separado o conjuntamente según sea necesario:

1. Si la colección RemoteApp está unido al dominio puede aplicar cualquier [directiva de grupo](https://technet.microsoft.com/library/cc725828.aspx) (con la excepción de Hola Hola inactivo Disconnect tiempo de espera de directivas de y se describe [aquí](../azure-subscription-service-limits.md)).
2. Como una alternativa tooGroup directiva (si la colección no está unido al dominio o no tiene los privilegios adecuados de hello en AD), puede configurar [directivas locales](https://technet.microsoft.com/library/cc775702.aspx) en la imagen de plantilla.  Tenga en cuenta que las directivas de grupo superan a las locales cuando hay un conflicto.
3. Algunas configuraciones de SO/aplicación no son configurables a través de la directiva, pero se pueden establecer mediante la clave del registro con hello [herramienta RegEdit](remoteapp-hybridtrouble.md) al configurar la imagen de plantilla.
4. Puede usar [Firewall de Windows](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) toocontrol tooand de acceso de red de la máquina de Hola donde se ejecuta la aplicación hello. Asegúrese de que no bloquee hello las direcciones URL y los puertos que se definen a continuación.
5. Puede usar [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) toocontrol que los usuarios de aplicaciones y archivos pueden ejecutar. Por ejemplo, los usuarios más experimentados pueden averiguar cómo toorun aplicaciones que no se publicó pero que están disponibles en hello imagen utilizó colección de Hola toocreate: puede bloquearlo de AppLocker.

## <a name="detailed-information"></a>Información detallada
* Hola siguiendo las directivas RDS es probablemente toobe más útil:
  * [Redirección de dispositivos y recursos](https://technet.microsoft.com/library/ee791794.aspx)
  * [Redirección de impresoras](https://technet.microsoft.com/library/ee791784.aspx)
  * [Perfiles](https://technet.microsoft.com/library/ee791865.aspx).
* Tenga en cuenta que configurar redirecciones a través de Hola módulo RemoteApp PowerShell (tal como se muestra [aquí](remoteapp-redirection.md)) se basa en hello máquina tooenforce Hola directiva de cliente por lo que si la seguridad es el objetivo principal de hello debe tener la directiva de hello tooenforce a través de Hola directiva local de imagen de plantilla o a través de la directiva de grupo.
* [Directivas de Windows Server 2012 R2](https://technet.microsoft.com/library/hh831791.aspx).
* [Las directivas de Office 2013](https://technet.microsoft.com/library/cc178969.aspx) (incluidos [cómo toocustomize Hola barra de herramientas de Office](https://technet.microsoft.com/library/cc179143.aspx)).

