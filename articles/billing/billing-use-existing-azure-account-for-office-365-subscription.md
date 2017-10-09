---
title: aaaSign hacia arriba para Office 365 con cuenta de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate Office 365 suscripción mediante el uso de una cuenta de Azure"
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: d19e1c1edff0b9658b639e796a72bbf4e87b9c3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a>Suscripción a Office 365 con la cuenta de Azure
Si es suscriptor de Azure, puede usar su toosign cuenta de Azure para disfrutar de una suscripción a Office 365. Si forma parte de una organización que tiene una suscripción de Azure, puede crear una suscripción de Office 365 para los usuarios de su cuenta actual de Azure Active Directory (Azure AD). Regístrese tooOffice 365 con una cuenta que tenga permisos de administrador Global o administrador de facturación de su inquilino de Azure Active Directory. Para más información, consulte [Comprobación de permisos de cuenta en Azure AD](#RoleInAzureAD) y [Asignación de roles de administrador en Azure Active Directory (Azure AD)](../active-directory/active-directory-assign-admin-roles.md).

Si ya tiene una cuenta de Office 365 y una suscripción de Azure, puede [asociar un tooan del inquilino de Office 365 suscripción de Azure](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a>Obtención de una suscripción a Office 365 con la cuenta de Azure

1. Vaya toohello [página del producto de Office 365](https://products.office.com/business)y seleccione un plan.
2. Haga clic en **iniciar sesión en** en la esquina superior derecha de Hola de página Hola.

    ![Captura de pantalla de la página de prueba de Office 365](./media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. Inicie sesión con las credenciales de su cuenta de Azure. Si está creando una suscripción para su organización, use una cuenta de Azure que sea miembro del rol de directorio de hello administrador Global o administrador de facturación de su inquilino de Azure Active Directory.

    ![Captura de pantalla de inicio de sesión en Office 365](./media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. Haga clic en **Probar ahora**.

    ![Captura de pantalla que confirma su pedido para Office 365](./media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. En la página de confirmación de pedido de hello, haga clic en **continuar**.

    ![Captura de pantalla de recibo del pedido Hola Office 365](./media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

Ahora ya está listo. Si ha creado la suscripción de Office 365 Hola para su organización, use Hola siguiendo los pasos toocheck que los usuarios de Azure AD se encuentran ahora en Office 365.

1. Abra el centro de administración de Office 365 Hola.
2. Expanda **USUARIOS** y luego haga clic en **Usuarios activos**.

    ![Captura de pantalla de los usuarios del centro de administración de hello Office 365](./media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

Después de registrarse, Hola suscripción a Office 365 se agrega toohello misma instancia de Azure Active Directory que pertenece la suscripción de Azure. Para más información, consulte [Más información acerca de las suscripciones de Azure y Office 365](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) y [Asociación de las suscripciones de Azure con Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a id="RoleInAzureAD"></a>Comprobación de los permisos de mi cuenta en Azure AD
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Haga clic en **Más servicios** y, a continuación, busque **Active Directory**.

    ![Captura de pantalla de Active Directory en hello portal de Azure](./media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. Haga clic en **Usuarios y grupos** > **Todos los usuarios**.
4. Seleccione el nombre de usuario de Hola. 

    ![Captura de pantalla que muestra los usuarios de Azure Active Directory Hola](./media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. Haga clic en **Rol del directorio**.
  
    ![Captura de pantalla que muestra el rol de Azure directory portal Hola](./media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  rol de Hello **administrador Global** o **administrador limitado** > **Administrador de facturación** es toocreate requiere una suscripción de Office 365 para usuarios en su Azure Active Directory existente.

    ![Captura de pantalla que muestra el rol del directorio de administrador de facturación de Azure Portal](./media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema. 
