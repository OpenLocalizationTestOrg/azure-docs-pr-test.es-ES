---
title: aaaPermissions en el centro de seguridad de Azure | Documentos de Microsoft
description: "En este artículo se explica cómo el centro de seguridad de Azure usa toousers de permisos de tooassign de control de acceso basado en roles e identifica Hola permitida acciones para cada rol."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a>Permisos en Azure Security Center

Centro de seguridad de Azure usa [Control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md), lo que proporciona [roles integrados](../active-directory/role-based-access-built-in-roles.md) que se puede asignar toousers, grupos y servicios de Azure.

Centro de seguridad evalúa la configuración de Hola de los problemas de seguridad de recursos tooidentify y vulnerabilidades. En el centro de seguridad, sólo verá información relacionada con recursos tooa cuando se le asigna Hola rol de propietario, Colaborador o lector de hello suscripción o grupo de recursos que pertenece el recurso.

En los roles de toothese adición, hay dos funciones específicas de centro de seguridad:

* **Lector de seguridad**: un usuario que pertenece el rol de toothis tiene ver derechos tooSecurity Center. usuario de Hello puede ver las recomendaciones, alertas, una directiva de seguridad y los Estados de seguridad, pero no puede realizar cambios.
* **Administrador de seguridad**: un usuario que pertenece el rol de toothis tiene Hola mismo derechos como Hola lector de seguridad y puede actualizar también la directiva de seguridad de Hola y descartar las alertas y las recomendaciones.

> [!NOTE]
> roles de seguridad de Hello, lector de seguridad y el Administrador de seguridad, tienen acceso sólo en el centro de seguridad. roles de seguridad de Hello no tiene acceso a las áreas de servicio de tooother de Azure como almacenamiento, Web y móviles o Internet de las cosas.
>
>

## <a name="roles-and-allowed-actions"></a>Roles y acciones permitidas

Hello siguiente tabla muestra los roles y las acciones permitidas en el centro de seguridad. Una X indica que se permite la acción de Hola para ese rol.

| Rol | Editar directivas de seguridad | Aplicar recomendaciones de seguridad en un recurso | Descartar alertas y recomendaciones | Ver alertas y recomendaciones |
|:--- |:---:|:---:|:---:|:---:|
| Propietario de la suscripción | X | X | X | X |
| Colaborador de la suscripción | X | X | X | X |
| Propietario del grupo de recursos | -- | X | -- | X |
| Colaborador del grupo de recursos | -- | X | -- | X |
| Lector | -- | -- | -- | X |
| Administrador de seguridad | X | -- | X | X |
| Lector de seguridad | -- | -- | -- | X |

> [!NOTE]
> Se recomienda que se definan Hola rol menos permisivo necesarios para los usuarios toocomplete sus tareas. Por ejemplo, asigne toousers de rol de lector de Hola que solo necesita tooview información sobre el estado de seguridad de Hola de un recurso pero no realizar acciones como aplicar recomendaciones o editar directivas.
>
>

## <a name="next-steps"></a>Pasos siguientes
Este artículo explica cómo el centro de seguridad utiliza RBAC tooassign permisos toousers e identificado Hola permitida acciones para cada rol. Ahora que está familiarizado con las asignaciones de roles de hello necesarios toomonitor Hola estado de seguridad de su suscripción, editar las directivas de seguridad y aplicar las recomendaciones, obtenga información acerca de cómo:

- [Establecer directivas de seguridad en Security Center](security-center-policies.md)
- [Administrar recomendaciones de seguridad en Security Center](security-center-recommendations.md)
- [Supervisar el estado de seguridad de Hola de los recursos de Azure](security-center-monitoring.md)
- [Administrar y responder a alertas de toosecurity en el centro de seguridad](security-center-managing-and-responding-alerts.md)
- [Supervisar soluciones de seguridad de asociados](security-center-partner-solutions.md)
