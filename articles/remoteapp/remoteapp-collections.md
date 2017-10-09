---
title: "¿aaaWhat tipo de colección no necesita para Azure RemoteApp? | Microsoft Docs"
description: "Obtenga información acerca de los tipos de Hola de colecciones disponibles con Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>¿Qué tipo de colección necesita para Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

RemoteApp de Azure permite compartir aplicaciones y recursos con usuarios de cualquier dispositivo. Hacer esto mediante la creación de colecciones toohold Hola aplicaciones y los recursos y, a continuación, compartir esas colecciones con los usuarios. Existen 2 opciones de colecciones distintas con diferentes opciones de autenticación y red. ¿Cuál es la que más le conviene?

Pasemos a través de diferentes consideraciones de Hola y las opciones que necesita más toomake tooget Hola fuera de la colección de RemoteApp de Azure. 

## <a name="quick-differences-between-hello-collection-types"></a>Rápido diferencias entre los tipos de colección de Hola
|  | Nube | Híbrida |
| --- | --- | --- |
| Uso de una red virtual existente |Sí |Sí |
| Requiere cuentas conectadas a AD (DirSync) |No |Sí |
| Requiere la unión a un dominio |No |Sí |
| Requiere tooVNET accesible de controlador de dominio |No |Sí |

## <a name="cloud-collections"></a>Colecciones de nube
* Toocreate rápido: colección de hello es aprovisionar rápidamente, lo que significa que las aplicaciones obtener toousers más rápido.
* Ofrecer sus propias aplicaciones o compartir las nuestras. Puede usar una imagen personalizada (generado a partir de una máquina virtual de Azure) o una de las imágenes de hello incluidas con su suscripción.
* No es necesario tooconfigure una conexión entre la colección y el dominio local.
* Pero si lo desea, puede usar su propio acceso tooprovide de red virtual de Azure en su entorno local para datos de uso compartido o toouse distinta de Windows autenticación en recursos, como SQL Server (mediante la autenticación de base de datos).

¿Cómo crear una?

* ¿Solo en la nube? Crear con hello **creación rápida** opción en el portal de Hola.
* ¿Nube + red virtual? Crear mediante hello **crear con red virtual** opción pero no elija toojoin un dominio.

## <a name="hybrid-collections"></a>Colecciones híbridas
* Proporcione la red de tooon local de acceso total + red virtual de Azure.
* Incluye el acceso conjunto de dominio para las aplicaciones y los datos. Las aplicaciones remotas se pueden autenticar con Active Directory local. A continuación, podrán tener acceso a los recursos del dominio.
* Habilitar la supervisión y administración avanzadas con las soluciones de System Center existentes y las directivas de grupo de Windows (mediante una imagen personalizada basada en Windows Server 2012 R2)
* Compatibilidad con [ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect tooyour de su red virtual de Azure red virtual local.

Crear mediante hello **crear con red virtual** opción y elija toojoin un dominio.

## <a name="authentication-options"></a>Opciones de autenticación
RemoteApp de Azure admite tanto cuentas de Microsoft como cuentas de Azure Active Directory; aunque no todas las colecciones admiten todos los métodos. 

| Tipo de cuenta |  | Nube | Nube + red virtual | Híbrida |
| --- | --- | --- | --- | --- |
| Cuenta Microsoft | |Sí |Sí |No |
| Azure Active Directory (Azure AD) | | | | |
| Solo Azure AD |Sí |Sí |No | |
| AD Connect con sincronización de contraseñas |Sí |Sí |Sí | |
| AD Connect sin sincronización de contraseñas |Sí |Sí |No | |
| AD Connect con AD FS |Sí |Sí |Sí | |
| Proveedores de identidades de terceros compatibles con Azure (por ejemplo, Ping) |Sí |Sí |Sí | |
| Multi-Factor Authentication | |Sí |Sí |Sí |

### <a name="cloud-and-cloud--vnet"></a>Nube y nube + red virtual
Con las colecciones en la nube, puede usar las cuentas de Microsoft, cuentas de Azure AD o una combinación de hello dos. Usar cuentas de Hola que funcionan mejor para los usuarios.

No hay ningún requisito específico en cuanto al uso de cuentas Microsoft. 

Si desea que las cuentas de Azure AD toouse, deberá toomake seguro de que el inquilino de Azure AD coincide con hello uno asociado a su suscripción. Cuando crea la suscripción de Azure RemoteApp, inquilino de Azure AD de Hola que estaba usando se asocia automáticamente con su suscripción. Cualquier usuario de Azure AD otorga permiso tooneeds toobe ese mismo inquilino. Si es necesario, puede [cambiar el inquilino de Azure AD hello](remoteapp-changetenant.md) asociados a la suscripción.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Híbrida (o nube + Azure AD + AD)
El uso de Azure AD + Active Directory local es un requisito previo para las colecciones híbridas. Necesita dos directorios de toouse AD Connect toointegrate Hola. Pero tiene algunas opciones cuando se trata de toohow configurar AD Connect. 

Existen 2 escenarios de AD Connect: uso de sincronización de contraseñas o uso de la federación de AD. Extraer del repositorio hello [información de conexión de AD](../active-directory/active-directory-aadconnect.md) toofigure cuáles de estas funciona mejor para usted.

También puede usar Azure AD + AD con una colección de nube. Asegúrese de que siga Hola al mismo conjunto de pasos de configuración.

Extraer del repositorio [Azure AD + requisitos de Active Directory de Azure RemoteApp](remoteapp-ad.md) para hello pasos necesarios tooconfigure Azure AD y Active Directory.

## <a name="go-create-your-collection"></a>¡Ya está preparado para crear su colección!
Bien, creo que nos hemos descubierto ahora, por lo que hay toodo izquierdo de una sola cosa: crear la primera colección de RemoteApp de Azure.

[Crear una colección de nube](remoteapp-create-cloud-deployment.md) o [crear una colección híbrida](remoteapp-create-hybrid-deployment.md): ya está preparado para crear su colección.

