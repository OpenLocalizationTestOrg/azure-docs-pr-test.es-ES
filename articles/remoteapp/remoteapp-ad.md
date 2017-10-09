---
title: aaaAzure AD + requisitos de Active Directory de Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset una toowork de Active Directory con Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Requisitos de Azure AD + Active Directory para Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Para la colección de híbrida de RemoteApp de Azure o para una colección en la nube que desea que toofederate mediante AD Connect, necesita toodo Hola siguiente.

### <a name="connect-azure-ad-and-active-directory"></a>Conexión de Azure AD y Active Directory
Si desea tooconnect inquilino de Azure AD y los entornos de Active Directory local, use AD Connect. Éste lo guiará solo [4 clics](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect Hola dos directorios.

Nota: la sincronización de directorios se requiere para las colecciones híbridas.

### <a name="make-sure-your-domaincom-match"></a>Asegúrese de que "@domain.com" coincide.
Antes de comenzar, asegúrese de que ese hello UPN para el sufijo de Hola de coincidencias de bosque local de su dominio de Azure AD. 

Después de configurar el sufijo de dominio UPN de hello en Azure AD, todos los usuarios iniciar sesión en Azure RemoteApp iniciará la sesión como "usuario @<hello suffix you set up>." Asegúrese de que los usuarios también pueden registrar con hello mismo user@suffix en el dominio local de Hola. En ciertos casos, puede configurar el nombre de un dominio en Azure AD al especificar un sufijo de dominio diferente para hello usuario localmente. En este caso, los usuarios no ser capaz de tooconnect tooany Unidos al dominio equipos o los recursos a través de Azure RemoteApp.

Por ejemplo, si configura el sufijo de dominio UPN en AAD como contoso.com, pero algunos usuarios locales y Active Directory son toolog configurado con @contoso.uk, los usuarios no será capaz de toocorrectly registro en hello colección ARA. Los usuarios que debe ser UPN en AAD y AD Hola mismo posibles de toobe de inicio de sesión de hello"

### <a name="create-objects-for-azure-remoteapp"></a>Creación de objetos para Azure RemoteApp
También necesita hello toocreate siguientes objetos de Active Directory local:

* Una cuenta de servicio tooprovide acceso toodomain recursos para los programas de RemoteApp al unirse a dominio RDSH puntos finales toohello local.
* Una unidad organizativa (UO) toocontain RemoteApp máquina los objetos. Uso de hello OU es cuentas de hello tooisolate recomendada (aunque no necesario) y las directivas que se va a utilizar con RemoteApp.

Necesita ambos de estos objetos cuando se crea la colección de RemoteApp, por lo que debe toodo seguro de estos pasos en primer lugar.

