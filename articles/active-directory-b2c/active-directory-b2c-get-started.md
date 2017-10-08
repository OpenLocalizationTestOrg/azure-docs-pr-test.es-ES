---
title: "Azure Active Directory B2C: creación de un inquilino de Azure Active Directory B2C | Microsoft Docs"
description: Un tema en forma de inquilinos toocreate un B2C de Azure Active Directory
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a>Crear a un inquilino de Azure Active Directory B2C Hola portal de Azure

Editar Sipi.

Este inicio rápido le ayuda a crear un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos. Cuando haya terminado, tendrá un toouse de inquilino B2C para registrar aplicaciones B2C.

## <a name="prerequisites"></a>Requisitos previos

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).

## <a name="create-an-azure-ad-b2c-tenant"></a>Creación de un inquilino de Azure AD B2C

Las características B2C no pueden habilitarse en los inquilinos existentes. Deberá toocreate un inquilino de Azure AD B2C.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

Enhorabuena, ha creado un inquilino de Azure Active Directory B2C. Es un administrador Global del inquilino de Hola. Puede agregar otros administradores globales según sea necesario. tooswitch tooyour nuevo inquilino, haga clic en hello *administrar el nuevo vínculo de inquilino*.

![Vínculo de administración del nuevo inquilino](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> Si tiene previsto toouse un inquilino B2C para una aplicación de producción, lea el artículo de hello en [producción escala frente a los inquilinos de vista previa B2C](active-directory-b2c-reference-tenant-type.md). Se conocen problemas cuando se elimina un B2C existente de inquilinos y vuelva a crearlo con hello mismo nombre de dominio. Deberá toocreate un inquilino B2C con un nombre de dominio diferente.
>
>

## <a name="link-your-tenant-tooyour-subscription"></a>Vincular su suscripción de inquilino tooyour

Necesita toolink su AD B2C de Azure inquilino tooyour suscripción de Azure tooenable toda la funcionalidad de B2C y pagar los cargos por uso. más información, lea toolearn [este artículo](active-directory-b2c-how-to-enable-billing.md). Si no vincula su tooyour de inquilino de Azure AD B2C suscripción de Azure, se bloquea alguna funcionalidad y, verá un mensaje de advertencia ("ninguna suscripción vinculados toothis B2C inquilinos u Hola suscripción necesita su atención.") en la configuración de hello B2C. Es importante que realice este paso antes de enviar las aplicaciones a producción.

## <a name="easy-access-toosettings"></a>Acceso fácil toosettings

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

También puede tener acceso a hoja Hola escribiendo `Azure AD B2C` en **buscar recursos** en parte superior de hello del portal de Hola. En la lista de resultados de hello, seleccione **Azure AD B2C** tooaccess Hola B2C hoja de configuración.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Registro de la aplicación B2C en un inquilino B2C](active-directory-b2c-app-registration.md)
