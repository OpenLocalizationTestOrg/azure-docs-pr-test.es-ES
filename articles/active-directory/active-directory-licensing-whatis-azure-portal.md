---
title: "¿aaaWhat es el Administrador de licencias en Azure Active Directory basado en grupos? | Microsoft Docs"
description: "Descripción de las licencias basadas en grupo de Azure Active Directory, cómo funcionan y procedimientos recomendados"
services: active-directory
keywords: Licencias de Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 11647de6b76022cd2393751fcafc67ce671aeba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a>Aspectos básicos de las licencias basadas en grupos en Azure Active Directory

El uso de los servicios de pago en la nube de Microsoft, como Office 365, Enterprise Mobility + Security, Dynamics CRM y otros productos similares, requiere licencias. Estas licencias se asignan a los usuarios tooeach que necesiten acceso a los servicios de toothese. licencias de toomanage, los administradores usar uno de los portales de administración de hello (Office o Azure) y cmdlets de PowerShell. Azure Active Directory (Azure AD) es la infraestructura subyacente de Hola que admite la administración de identidades para todos los servicios de nube de Microsoft. Azure AD almacena información sobre los estados de asignación de licencias para los usuarios.

Hasta ahora, sólo se podrían asignar licencias a nivel de usuario individual de hello, lo que puede dificultar la administración a gran escala. Por ejemplo, tooadd o quitar licencias de usuario basados en cambios en la organización, como los usuarios unirse o salir de Hola organización o un departamento, un administrador a menudo debe escribir un script de PowerShell complejo. Este script realiza llamadas individuales toohello servicio en la nube.

tooaddress los desafíos, ahora, Azure AD incluye basado en el grupo de licencias. Puede asignar a uno o más grupo de tooa de licencias de productos. Azure AD garantiza que licencias de Hola se asignan a tooall miembros del grupo de Hola. Todos los miembros nuevos que se unan a grupo Hola se asignan las licencias adecuadas Hola. Cuando abandonan el grupo de hello, se quitan esas licencias. Esto elimina la necesidad de Hola para automatizar la administración de licencias a través de PowerShell tooreflect cambios de organización de Hola y estructura de departamento a cada usuario.

## <a name="features"></a>Características

Estas son las principales características de Hola de basado en el grupo de licencias:

- Puede asignar las licencias tooany grupo de seguridad de Azure AD. Los grupos de seguridad se pueden sincronizar en el entorno local mediante Azure AD Connect. También puede crear grupos de seguridad directamente en Azure AD (también denominados grupos solo en la nube) o de forma automática a través de la característica de grupo dinámico de hello Azure AD.

- Cuando se asigna una licencia de producto grupo tooa, Administrador de hello puede deshabilitar uno o varios planes de servicio en el producto de Hola. Normalmente, esto se realiza cuando la organización de hello aún no está listo toostart mediante un servicio incluido en un producto. Por ejemplo, Administrador de hello podría asignar departamento tooa de Office 365, pero deshabilitar temporalmente el servicio de Yammer Hola.

- Se admiten todos los Servicios en la nube de Microsoft que requieren licencias a nivel de usuario. Se incluyen todos los productos de Office 365, Enterprise Mobility + Security y Dynamics CRM.

- Basado en el grupo de licencias está actualmente disponible sólo a través de [Hola portal de Azure](https://portal.azure.com). Si se usan principalmente otros portales de administración para el usuario y administración de grupos, como portal de Office 365 hello, puede continuar toodo así. Sino que debe utilizar licencias de Azure toomanage portal hello en el nivel de grupo.

- Azure AD administra automáticamente las modificaciones de licencia resultantes de los cambios de pertenencia a grupos. Habitualmente, las modificaciones de licencia entran en vigor minutos después de un cambio en la pertenencia.

- Un usuario puede ser miembro de varios grupos con directivas de licencia especificadas. Un usuario también puede tener algunas licencias que se asignaron directamente, fuera de cualquier grupo. Hola resultante de estado de usuario es una combinación de todos los productos asignado y las licencias de servicio.

- En algunos casos, licencias no se puede asignar el usuario tooa. Por ejemplo, puede que no haya suficientes licencias disponibles en el inquilino de hello, o servicios en conflicto podrían tener asignados en hello mismo tiempo. Los administradores tienen acceso tooinformation acerca de los usuarios para los que, Azure AD no pudo procesar completamente licencias del grupo. Pueden realizar acciones correctivas según esa información.

- Durante la versión preliminar pública, se requiere una suscripción de pagada o de prueba para las ediciones de Azure AD Basic y Premium en administración de licencias basadas en grupos de toouse de hello inquilino.

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de otros escenarios de administración de licencias a través de basado en el grupo de licencias, vea:

* [Introducción a las licencias de Azure Active Directory](active-directory-licensing-get-started-azure-portal.md)
* [Asignar licencias tooa grupo en Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Identificación y resolución de problemas de licencias de un grupo en Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Cómo toomigrate individuales autoriza el uso de los usuarios según toogroup licencias en Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory group-based licensing additional scenarios](active-directory-licensing-group-advanced.md) (Escenarios adicionales de licencias basadas en grupos de Azure Active Directory)
