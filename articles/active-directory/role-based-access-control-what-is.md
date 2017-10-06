---
title: aaaManage acceso y los permisos con RBAC - RBAC de Azure | Documentos de Microsoft
description: "Introducción a administración de acceso con control de acceso basado en roles de Azure en hello Portal de Azure. Utilizar los permisos de tooassign de asignaciones de rol en el directorio."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 1c133b2b57b49d85f0e12a318c7997478e095fb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-role-based-access-control-in-hello-azure-portal"></a>Empezar a trabajar con Control de acceso basado en roles en hello portal de Azure
Las empresas orientada a servicios de seguridad deben centrarse en conceder a los empleados que necesitan los permisos exactos Hola. Demasiados permisos pueden exponer un tooattackers de cuenta. Si se conceden muy pocos, los empleados no podrán realizar su trabajo de manera eficaz. Gracias al control de acceso basado en roles (RBAC) de Azure, podrá abordar este problema, ya que es posible realizar una administración avanzada del acceso para Azure.

Usar RBAC, puede separar los derechos en el equipo y conceder solo Hola mucha toousers de acceso que necesitan tooperform sus trabajos. En lugar de proporcionar a todos los empleados permisos no restringidos en los recursos o la suscripción de Azure, puede permitir solo determinadas acciones. Por ejemplo, un empleado de uso RBAC toolet administrar máquinas virtuales en una suscripción, mientras que otro puede administrar SQL bases de datos dentro de Hola misma suscripción.

## <a name="basics-of-access-management-in-azure"></a>Aspectos básicos de la administración de acceso en Azure
Cada suscripción de Azure está asociada a un directorio de Azure Active Directory (AD). Los usuarios, grupos y aplicaciones desde ese directorio pueden administrar recursos en hello suscripción de Azure. Asignar estos derechos de acceso mediante Hola portal de Azure, herramientas de línea de comandos de Azure y las API de administración de Azure.

Conceda el acceso mediante la asignación de hello adecuado RBAC rol toousers, grupos y aplicaciones en un ámbito determinado. ámbito de Hola de una asignación de roles puede ser una suscripción, un grupo de recursos o un único recurso. Un rol asignado en un ámbito primario también concede acceso toohello los elementos secundarios incluidos en él. Por ejemplo, un usuario con el grupo de recursos de acceso tooa puede administrar todos los recursos de hello contiene, como sitios Web, máquinas virtuales y subredes.

![Relación entre elementos de Azure Active Directory - diagrama](./media/role-based-access-control-what-is/rbac_aad.png)

rol RBAC Hola que asigne determina qué usuario Hola de recursos, el grupo o la aplicación puede administrar dentro de ese ámbito.

## <a name="built-in-roles"></a>Roles integrados
RBAC de Azure tiene tres funciones básicas que se aplican a tipos de recursos de tooall:

* **Propietario** tiene acceso completo tooall recursos incluidos hello toodelegate derecho acceso tooothers.
* **Colaborador** puede crear y administrar todos los tipos de recursos de Azure, pero no se puede conceder acceso tooothers.
* **lector** solo puede ver los recursos existentes de Azure.

rest Hola de roles RBAC hello en Azure que admita la administración de recursos específicos de Azure. Por ejemplo, hello rol Colaborador de máquina Virtual permite toocreate de usuario de Hola y administrar máquinas virtuales. No ofrece su red virtual de acceso toohello o subred Hola Hola máquina virtual se conecta a. 

[Funciones integradas de RBAC](role-based-access-built-in-roles.md) listas Hola roles disponibles en Azure. Especifica las operaciones de Hola y ámbito que cada rol integrado concede toousers. Si está pensando toodefine sus propios roles para tener un mayor control, vea cómo toobuild [roles personalizados en Azure RBAC](role-based-access-control-custom-roles.md).

## <a name="resource-hierarchy-and-access-inheritance"></a>Jerarquía de recursos de Azure y herencia de acceso
* Cada **suscripción** en Azure pertenece tooonly un directorio. (Pero cada directorio puede tener más de una suscripción).
* Cada **grupo de recursos** pertenece tooonly una suscripción.
* Cada **recursos** pertenece tooonly un grupo de recursos.

El acceso que se concede en el nivel principal se hereda en los ámbitos secundarios. Por ejemplo:

* Asignar a grupo Hola Reader rol tooan Azure AD en el ámbito de la suscripción de Hola. los miembros de Hola de ese grupo pueden ver todos los grupos de recursos y recursos en la suscripción de Hola.
* Asignar la aplicación de tooan de rol de colaborador de hello en el ámbito de grupo de recursos de Hola. Pueden administrar los recursos de todos los tipos de ese grupo de recursos, pero no otros grupos de recursos en la suscripción de Hola.

## <a name="azure-rbac-vs-classic-subscription-administrators"></a>RBAC de Azure frente a administradores de la suscripción clásica
Los administradores de suscripciones clásico y coadministradores tienen acceso total toohello suscripción de Azure. Pueden administrar recursos utilizando hello [portal de Azure](https://portal.azure.com) con las API del Administrador de recursos de Azure, o hello [portal de Azure clásico](https://manage.windowsazure.com) y el modelo de implementación clásico de Azure. En el modelo RBAC hello, los administradores clásicos se asignan rol de propietario de hello en el ámbito de la suscripción de Hola.

Solo Hola portal de Azure y Hola nueva compatibilidad de las API del Administrador de recursos de Azure RBAC de Azure. No pueden usar usuarios y aplicaciones que se asignan roles RBAC portal de administración clásico de Hola y el modelo de implementación clásica Azure Hola.

## <a name="authorization-for-management-vs-data-operations"></a>Autorización para administración frente a operaciones de datos
RBAC de Azure solo admite operaciones de administración de recursos de Azure en Hola Hola portal de Azure y las API del Administrador de recursos de Azure. No todas las operaciones de nivel de datos para recursos de Azure pueden autorizarse. Por ejemplo, puede autorizar a un usuario toomanage cuentas de almacenamiento, pero no toohello blobs o tablas dentro de una cuenta de almacenamiento. De forma similar, una base de datos SQL se puede administrar, pero no Hola tablas dentro de él.

## <a name="next-steps"></a>Pasos siguientes
* Empezar a trabajar con [basada en roles de Control de acceso en el portal de Azure de hello](role-based-access-control-configure.md).
* Vea hello [funciones integradas de RBAC](role-based-access-built-in-roles.md)
* Defina sus propios [Custom Roles in Azure RBAC](role-based-access-control-custom-roles.md)
