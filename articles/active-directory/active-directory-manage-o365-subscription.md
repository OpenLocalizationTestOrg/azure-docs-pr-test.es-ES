---
title: "directorio de hello aaaManage para la suscripción a Office 365 en Azure | Documentos de Microsoft"
description: "Administrar un directorio de suscripción de Office 365 con Azure Active Directory y Hola portal de Azure clásico"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a>Administrar el directorio de hello para la suscripción a Office 365 en Azure
Este artículo se describe cómo toomanage un directorio que se creó para una suscripción a Office 365, utilizando Hola portal de Azure clásico. Debe ser Hola Administrador de servicios o un CO-Administrador de una toosign de suscripción de Azure en toohello portal de Azure clásico. Si aún no dispone de una suscripción de Azure, desde este vínculo puede registrarse ahora mismo para disfrutar de una [evaluación gratuita durante 30 días](https://azure.microsoft.com/trial/get-started-active-directory/) e implementar su primera solución en la nube en menos de 5 minutos. Toouse seguro Hola trabajo o académica cuenta que usa toosign en tooOffice 365.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.

Después de completar Hola suscripción de Azure, puede iniciar sesión en el portal de Azure clásico toohello y tener acceso a los servicios de Azure. Haga clic en la extensión de Active Directory de hello toomanage Hola el mismo directorio que autentica a los usuarios de Office 365.

Si ya tiene una suscripción de Azure, Hola proceso toomanage un directorio adicional es también muy sencillo. Por ejemplo, suponga que Michael Smith tiene una suscripción a Office 365 para Contoso.com. También tiene una suscripción a Azure, que realizó con su cuenta Microsoft, msmith@hotmail.com. En este caso, administra dos directorios.

| Subscription | Office 365 | Las tablas de Azure |
| --- | --- | --- |
|   Nombre para mostrar |Contoso |Directorio de Azure Active Directory (Azure AD) predeterminado |
|   Nombre de dominio |contoso.com |msmithhotmail.onmicrosoft.com |

Quiere toomanage identidades de usuario de hello en el directorio de Contoso Hola mientras tiene iniciada una sesión en tooAzure utilizando su cuenta de Microsoft, para que poder habilitar características de Azure AD como la autenticación multifactor. Hola después de diagrama puede ayudar en proceso de hello tooillustrate.

![Crear un diagrama de toomanage dos directorios independientes](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

En este caso, los dos directorios de hello son independientes entre sí.

## <a name="toomanage-two-independent-directories"></a>directorios independientes toomanage dos
En el criterio de Michael Smith toomanage dos directorios mientras tiene iniciada una sesión en tooAzure como msmith@hotmail.com, debe completar Hola pasos:

> [!NOTE]
> Estos pasos solo se pueden realizar cuando un usuario ha iniciado sesión con una cuenta Microsoft. Si el usuario de hello ha iniciado sesión con una cuenta profesional o educativa, Hola opción demasiado**usar directorio existente** no está disponible. Una cuenta profesional o educativa puede solo puede autenticarla su directorio particular (es decir, directorio de hello, donde hello cuenta profesional o educativa se almacena y posee ese negocio Hola o centro educativo).
>
>

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) como msmith@hotmail.com.
2. Haga clic en **Nuevo** > **App Services** > **Active Directory** > **Directorio** > **Creación personalizada**.
3. Haga clic en usar existente Hola de directorio y seleccione **estoy listo toobe cerrar la sesión ahora** casilla de verificación.
4. Inicie sesión en toohello portal de Azure clásico como administrador global de Contoso.onmicrosoft.com (por ejemplo, msmith@contoso.com).
5. Cuando se le solicite demasiado**utilizar el directorio de Contoso con Azure Hola?**, haga clic en **continuar**.
6. Haga clic en **Cerrar sesión ahora**.
7. Inicie sesión en toohello portal de Azure clásico como msmith@hotmail.com. directorio de Contoso de Hola y Hola predeterminado aparecen en hello extensión de Active Directory.

Después de completar estos pasos, msmith@hotmail.com es un administrador global en el directorio de Contoso Hola.

## <a name="tooadminister-resources-as-hello-global-admin"></a>tooadminister recursos como Hola administrador global
Ahora imaginemos que Jane Doe necesita administrar sitios Web y recursos de base de datos que están asociados a Hola suscripción de Azure para msmith@hotmail.com. Antes de que puede hacerlo, Michael Smith necesita toocomplete estos pasos adicionales:

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) con cuenta de administrador de servicio de Hola Hola suscripción de Azure (en este ejemplo, msmith@hotmail.com).
2. Transferencia de directorio de Contoso de hello suscripción toohello: haga clic en **configuración** > **suscripciones** > seleccione suscripción hello > **editar directorio** > seleccione **Contoso (Contoso.com)**. Como parte de la transferencia de hello, cualquier trabajo o escuela se quitan las cuentas que son los coadministradores tienen permisos de suscripción de Hola.
3. Agregar Jane Doe como Coadministrador de suscripción de hello: haga clic en **configuración** > **administradores** > seleccione suscripción hello > **agregar** > tipo **JohnDoe@Contoso.com**.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de la relación de hello entre suscripciones y directorios, vea [cómo se asocia a un directorio de una suscripción](active-directory-how-subscriptions-associated-directory.md).
