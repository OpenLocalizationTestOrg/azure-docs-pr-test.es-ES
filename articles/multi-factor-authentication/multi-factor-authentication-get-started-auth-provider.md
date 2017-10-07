---
title: "aaaGet inició el proveedor de autenticación multifactor de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un proveedor de autenticación multifactor de Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a>Introducción al Proveedor de Azure Multi-Factor Authentication
La verificación en dos pasos está disponible de forma predeterminada para los administradores globales que tienen usuarios de Azure Active Directory y Office 365. Sin embargo, si desea aprovechar tootake [características avanzadas](multi-factor-authentication-whats-next.md) , a continuación, debe adquirir la versión completa de Hola de Azure la autenticación multifactor (MFA).

Se utiliza un proveedor de autenticación multifactor de Azure tootake aprovechar las características proporcionadas por la versión completa de Hola de MFA de Azure. Es para aquellos usuarios que **no tienen licencias a través de Azure MFA, Azure AD Premium o Enterprise Mobility + Security (EMS)**.  Azure MFA, Azure AD Premium y EMS incluyen hello de versión completa de MFA de Azure de forma predeterminada. Si cuenta con licencias, no necesita un Proveedor de Azure Multi-Factor Authentication.

Un proveedor de autenticación multifactor de Azure es hello toodownload necesario SDK.

> [!IMPORTANT]
> toodownload Hola SDK, deberá toocreate un proveedor de autenticación multifactor de Azure incluso si tienen licencias de Azure MFA, AAD Premium o EMS.  Si crea un proveedor de autenticación multifactor de Azure para este propósito y ya tiene licencias, que seguro toocreate Hola proveedor con hello **por usuario habilitado** modelo. A continuación, vincular directorio Hola de toohello del proveedor que contiene las licencias de MFA de Azure, Azure AD Premium o EMS de Hola. Esta configuración garantiza que solo se le facturará si tiene más usuarios únicos que realizar la comprobación de dos pasos que número Hola de licencias que posee.

## <a name="what-is-an-azure-multi-factor-auth-provider"></a>¿Qué es un Proveedor de Azure Multi-Factor Authentication?

Si no tiene licencias para la autenticación multifactor de Azure, puede crear un verificacion de toorequire de un proveedor de autenticación para los usuarios. Si está desarrollando una aplicación personalizada y desea tooenable MFA de Azure, cree un proveedor de autenticación y [descargar Hola SDK](multi-factor-authentication-sdk.md).

Hay dos tipos de proveedores de autenticación y distinción de hello es alrededor de cómo se aplicarán cargos a su suscripción de Azure. opción de Hola por autenticación calcula número Hola de autenticaciones realizadas en su inquilino en un mes. Esta opción es la más adecuada si tiene un número de usuarios que se autentican solo en algunas ocasiones o si necesita MFA para una aplicación personalizada. opción de Hola por usuario calcula número Hola de personas en el inquilino que realizar la verificación en dos pasos en un mes. Esta opción es mejor si tiene algunos usuarios con licencias pero necesita que tooextend MFA toomore usuarios más allá de los límites de su licencias.

## <a name="create-a-multi-factor-auth-provider"></a>Creación de un proveedor de autenticación multifactor
Usar hello siguiendo los pasos toocreate un proveedor de autenticación multifactor de Azure. Proveedores de autenticación multifactor Azure solo pueden crearse en hello portal de Azure clásico. Si no puede iniciar sesión en toohello portal de Azure clásico, consulte toomake seguro de que el inquilino de Azure AD [asociada a una suscripción de Azure](../active-directory/active-directory-how-subscriptions-associated-directory.md). 

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) como administrador.
2. Hola izquierda, seleccione **Active Directory**.
3. En la página Active Directory hello en la parte superior de hello, seleccione **proveedores de autenticación multifactor**.
   
   ![Creación de un proveedor de MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. En la parte inferior de hello, haga clic en **nuevo**.
   
   ![Creación de un proveedor de MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. En App Services, seleccione **Proveedor de autenticación multifactor**
   
   ![Creación de un proveedor de MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. Seleccione **Creación rápida**.
   
   ![Creación de un proveedor de MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. Rellene Hola después de campos y seleccione **crear**.
   1. **Nombre** : hello nombre del programa Hola a proveedor de autenticación multifactor.
   2. **Modelo de uso**: puede elegir una de las dos opciones a continuación:
      * Por autenticación: modelo de adquisición que se carga por autenticación. Normalmente se usa para escenarios que utilizan Azure Multi-Factor Authentication en una aplicación orientada al consumidor.
      * Por usuario habilitado: modelo de adquisición que se carga por usuario habilitado. Se utiliza normalmente para tooapplications de acceso de empleados, como Office 365. Elija esta opción si tiene algunos usuarios que ya tienen una licencia de Azure MFA.
   3. **Directorio** : hello Azure Active Directory de ese Hola proveedor de autenticación multifactor está asociado a los inquilinos. Tenga en cuenta Hola siguiente:
      * No es necesario un toocreate del directorio de Azure AD un proveedor de autenticación multifactor. Deje este cuadro en blanco si solo va toodownload Hola servidor Azure Multi-factor Authentication o SDK.
      * Hola proveedor de autenticación multifactor debe estar asociado con una ventaja de tootake del directorio de Azure AD de hello características avanzadas.
      * Solo un proveedor de Multi-Factor Authentication puede asociarse con un directorio de Azure AD.  
      ![Creación de un proveedor de MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. Tras hacer clic en crear, Hola se crea el proveedor de autenticación multifactor y debería ver un mensaje que indica: **creado correctamente el proveedor de autenticación multifactor**. Haga clic en **Aceptar**.  
   
   ![Creación de un proveedor de MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a>Administración del proveedor de Multi-Factor Authentication

No se puede cambiar el uso de hello después de crea un proveedor de MFA de modelo (por usuario habilitado o por autenticación). Sin embargo, puede eliminar el proveedor de MFA de hello y, a continuación, crear una con un modelo de uso distintos.

Si hello actual proveedor de autenticación multifactor está asociado a un directorio de Azure AD (también conocido como un inquilino de Azure AD), puede eliminar el proveedor de MFA de Hola y crear uno que esté vinculado toohello AD de Azure mismo inquilino. Como alternativa, si ha adquirido suficiente MFA, Azure AD Premium o Enterprise Mobility + Security (EMS) licencias toocover todos los usuarios que están habilitados para MFA, puede eliminar proveedor de MFA de Hola por completo.

Si el proveedor MFA no está vinculado tooan Azure AD inquilino, o bien vincular a Hola nuevo MFA proveedor tooa Azure AD diferentes inquilino, configuración de usuario y opciones de configuración no se transfieren. Además, Azure MFA servidores existentes necesita toobe vuelve a activar utilizando credenciales de activación que se generan a través de Hola nuevo proveedor de MFA. Reactivar Hola servidores MFA toolink les toohello nuevo proveedor de MFA no afecta a la llamada de teléfono y autenticación de mensajes de texto, pero la aplicación móvil notificaciones dejará de funcionar para todos los usuarios hasta que vuelvan a activar aplicación móvil de Hola.

## <a name="next-steps"></a>Pasos siguientes

[Descargar el SDK de autenticación multifactor Hola](multi-factor-authentication-sdk.md)

[Configuración de Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md)
