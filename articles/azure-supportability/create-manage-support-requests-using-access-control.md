---
title: "toocontrol de Control de acceso basado en roles (RBAC) aaaAzure toocreate de derechos de acceso y administrar solicitudes de soporte técnico | Documentos de Microsoft"
description: "Azure toocontrol de Control de acceso basado en roles (RBAC) toocreate de derechos de acceso y administrar solicitudes de soporte técnico"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a>Azure toocontrol de Control de acceso basado en roles (RBAC) toocreate de derechos de acceso y administrar solicitudes de soporte técnico

El [control de acceso basado en rol (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) permite realizar una administración detallada del acceso en Azure.
Admite la creación de solicitud en el portal de Azure, hello [portal.azure.com](https://portal.azure.com), usa toodefine de modelo RBAC de Azure que puede crear y administrar solicitudes de soporte técnico.
Se concede acceso mediante la asignación de hello adecuado RBAC rol toousers, grupos y las aplicaciones en un ámbito determinado, que puede ser una suscripción, el grupo de recursos o un recurso.

Veamos un ejemplo: como propietario de un grupo de recursos con permisos de lectura en el ámbito de la suscripción de hello, puede administrar todos los recursos de hello en el grupo de recursos de hello, como sitios Web, máquinas virtuales y subredes.
Sin embargo, cuando intente toocreate una solicitud de soporte técnico en un recurso de la máquina virtual de hello, encontrar Hola tras error

![Error de suscripción](./media/create-manage-support-requests-using-access-control/subscription-error.png)

En administración de solicitudes de soporte técnico, necesita permiso de escritura o un rol que tenga Hola acción Microsoft.Support/* en hello suscripción ámbito toobe capaz de toocreate y administrar solicitudes de soporte técnico.

Hola artículo siguiente explica cómo puede utilizar toocreate de Control de acceso basado en roles (RBAC) personalizado de Azure y administrar solicitudes de soporte técnico en hello portal de Azure.

## <a name="getting-started"></a>Introducción

Utilizando el ejemplo de Hola anterior, sería capaz de toocreate una solicitud de soporte técnico para el recurso si se asigna un rol personalizado de RBAC en suscripción Hola por el propietario de la suscripción de Hola.
[Roles personalizados de RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) pueden crearse con hello API de REST, interfaz de línea de comandos (CLI) de Azure y Azure PowerShell.

propiedad de las acciones de Hola de un rol personalizado especifica hello Azure operaciones toowhich Hola función concede acceso.
toocreate un rol personalizado para la administración de la solicitud de soporte técnico, el rol de hello debe tener la acción de hello Microsoft.Support/*

Este es un ejemplo de un rol personalizado puede utilizar toocreate y administrar las solicitudes de soporte.
Nos hemos denominado este rol "Colaborador de solicitud de soporte técnico" y así es cómo nos referimos toohello rol personalizado en este artículo.

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

Siga los pasos de hello descritos en [este vídeo](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn cómo toocreate un rol personalizado para su suscripción.

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a>Crear y administrar solicitudes de soporte técnico en hello portal de Azure

Veamos un ejemplo: es propietario de Hola de suscripción "Visual Studio MSDN suscripción."
Juan es el punto que es un toosome de propietario de recursos de grupos de recursos de hello en esta suscripción y tiene la suscripción de toohello de permiso de lectura.
Desea toogive acceso tooyour del mismo nivel, Joe, toocreate de capacidad de Hola y administrar incidencias de soporte técnico para los recursos de hello en esta suscripción.

1. Hola primer paso es toogo toohello suscripción y en "Configuración" verá una lista de usuarios. Haga clic en el usuario de Hola Juan quién tiene acceso de lectura de hello suscripción y vamos a asignar un nuevo toohim roles personalizados.

    ![Agregar rol](./media/create-manage-support-requests-using-access-control/add-role.png)

2. En la hoja de "Users" Hola, haga clic en "Agregar". Seleccionar roles personalizados de Hola "Colaborador de solicitud de soporte técnico" de lista de Hola de roles

    ![Agregar rol de colaborador de soporte técnico](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. Después de seleccionar el nombre de la función hello, haga clic en "Agregar usuarios" y escriba las credenciales de correo electrónico de Hola Juan. Haga clic en "Seleccionar"

    ![Agregar usuarios](./media/create-manage-support-requests-using-access-control/add-users.png)

4. Haga clic en "Aceptar" tooproceed

    ![Agregar acceso](./media/create-manage-support-requests-using-access-control/add-access.png)

5. Ahora verá el usuario de hello con hello roles personalizados recién agregado "Compatibilidad con solicitudes Colaborador" en la suscripción de Hola que es propietario de Hola

    ![Usuario agregado](./media/create-manage-support-requests-using-access-control/user-added.png)

    Cuando Juan inicia sesión en el portal de hello, ve hello toowhich de suscripción que se agregó.

7. Juan hace clic en "Nueva solicitud de soporte técnico" de la hoja de "Ayuda y soporte técnico" hello y puede crear solicitudes de soporte técnico para "Visual Studio Ultimate con MSDN"

    ![Nueva solicitud de soporte](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. Haga clic en "Todos admiten solicitudes" Juan puede ver lista de Hola de solicitudes de soporte creada para esta suscripción ![caso la vista de detalles](./media/create-manage-support-requests-using-access-control/case-details-view.png)

## <a name="remove-support-request-access-in-hello-azure-portal"></a>Quitar el acceso de solicitud de soporte en hello portal de Azure

Del mismo modo que es posible toogrant acceso tooa usuario toocreate y administrar solicitudes de soporte técnico, es acceso tooremove posibles para el usuario de hello así.
tooremove Hola capacidad toocreate administrar solicitudes de soporte técnico, vaya toohello suscripción, haga clic en "Configuración" y haga clic en usuario hello (en este caso, Juan).
Haga clic en nombre de rol de hello, "Colaborador de solicitud de soporte técnico" y haga clic en "Quitar"

![Quitar el acceso a la solicitud de soporte técnico](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

Cuando Juan inicia sesión en el portal de toohello e intenta toocreate una solicitud de soporte técnico, encuentra Hola tras error

![Error de suscripción-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

Joe no ve ninguna de las solicitudes de soporte técnico al hacer clic en "All support requests" (Todas las solicitudes de soporte técnico)

![vista de detalles del caso-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
