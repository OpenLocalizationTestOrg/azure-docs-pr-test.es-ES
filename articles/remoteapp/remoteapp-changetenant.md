---
title: inquilino de Azure Active Directory aaaChange hello en Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo inquilino de Azure Active Directory de hello toochange asociada a Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a>Cambiar el inquilino de Azure Active Directory hello en Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

RemoteApp de Azure usa el acceso de usuario de tooallow de Azure Active Directory (Azure AD). inquilino de Hello solo Azure AD que puede usar en Azure RemoteApp es hello asociado Hola suscripción de Azure. Puede ver suscripción Hola asociado en hello **configuración** página del portal de Hola. Mire hello **directorio** columna hello **suscripciones** ficha.

> [!NOTE]
> Para este toosucceed de cambio, quite primero todos los usuarios de inquilino de Azure Active Directory existente de Hola de todas las colecciones de RemoteApp de Azure. toodo, vaya toohello Portal de Azure, vaya toohello **Azure RemoteApp** pestaña y abra cada colección de RemoteApp de Azure. Vaya toohello **usuarios** pestaña y quitar usuarios que pertenecen tooyour inquilino de Azure Active Directory actual. Repita esta acción para todas las colecciones de Azure RemoteApp existentes. Sin tener que realizar esto, no será capaz de toocreate o colecciones de revisión.
> 
> 

Si desea toouse un inquilino diferente, utilice estas asociaciones de hello toochange pasos con su suscripción:

1. En el portal de hello, quite cualquier toowhich de los usuarios de Azure AD haya concedido acceso tooAzure colecciones de RemoteApp. (Vea la nota de hello anteriormente para conocer los pasos sobre cómo toodo esto.)
2. Establecer una cuenta de Microsoft (anteriormente denominada Live ID) como administrador de servicios de Hola. ¿(No sabe si ya están Hola, Administrador de servicio? Puede averiguarlo si hace clic en **Configuración -> Administradores**). Ahora, le mostramos cómo cambiar eso:
   
   1. Haga clic en usuario de hello en la esquina superior derecha de Hola y, a continuación, haga clic en **ver mi factura**.
   2. Haga clic en la suscripción de Hola. A continuación, en la página nueva de hello, desplácese hacia abajo y haga clic en **editar detalles de la suscripción** Hola derecho. (Tipo de hello central inferior derecha, que le ayuda a que le resulte).
   3. Escriba Hola Microsoft cuenta para el usuario de Hola que debe ser administrador del servicio Hola.
3. Ahora, cierre sesión en el portal de hello y, a continuación, iniciar sesión con cuenta de Microsoft que especificó en el paso anterior de Hola Hola.
4. Haga clic en **Nuevo > Servicios de aplicaciones > Active Directory > Directorio > Creación personalizada**.
5. En **Directorio**, elija **Usar directorio existente**. Vamos toohave toosign fuera del portal de hello ahora, por lo que decide **estoy listo toobe cerrar la sesión ahora**.
6. Inicio de sesión de nuevo en hello portal como administrador global del directorio de hello desea tooadd. (Si no fuera todavía administrador global, lo será después de volver a iniciar sesión y luego cerrarla).
7. Se le preguntará cuando inicias sesión si desea toouse su inquilino de AD existente con su suscripción. Haga clic en **Continuar**, y luego haga clic en **Cerrar sesión ahora**.
8. Iniciar sesión en nuevo y volver atrás demasiado**configuración -> suscripciones**. Seleccione la suscripción y haga clic en **Editar directorio**. Seleccione el inquilino de hello Azure AD que desea toouse.

Ahora puede usar Hola nuevo Azure AD inquilino toocontrol acceso toohello acceso de usuario de suscripción y tooconfigure de Azure en Azure RemoteApp.

