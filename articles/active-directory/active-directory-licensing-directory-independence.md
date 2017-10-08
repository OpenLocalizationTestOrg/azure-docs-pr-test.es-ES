---
title: aaaCharacteristics de Azure Active Directory inquilino intercaction | Documentos de Microsoft
description: "Administre sus inquilinos de Azure Active Directory considerándolos como recursos completamente independientes."
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a>Información de cómo interactúan varios inquilinos de Azure Active Directory

En Azure Active Directory (Azure AD), cada inquilino es un recurso totalmente independiente: Hola a un elemento del mismo nivel que sea lógicamente independiente de otros inquilinos que se administran. No hay ninguna relación de elementos primarios y secundarios entre los inquilinos. Esta independencia entre inquilinos incluye la de los recursos, la independencia administrativa y la de sincronización.

## <a name="resource-independence"></a>Independencia de recursos
* Si crear o eliminar un recurso en un inquilino, no tiene ningún impacto en los recursos en otro inquilino, con la excepción parcial de Hola de usuarios externos. 
* Si usa uno de los nombres de dominio con un inquilino, no se puede usar con ningún otro.

## <a name="administrative-independence"></a>Independencia administrativa
Si un usuario no administrador del inquilino "Contoso" crea un directorio de prueba "Prueba", en ese caso:

* De forma predeterminada, el usuario de Hola que crea a un inquilino se agrega como un usuario externo en ese nuevo inquilino y el rol de administrador global de hello asignado en ese inquilino.
* los administradores de Hola de inquilino "Contoso" no tienen ningún tootenant privilegios administrativos directos 'Test', a menos que un administrador de "Prueba" específicamente les otorgue estos privilegios. Sin embargo, los administradores de "Contoso" pueden controlar acceso tootenant 'Test' Si control de cuenta de usuario de Hola que creó "Prueba".
* Si agrega o quitar un rol de administrador para un usuario en un inquilino, cambio de hello no hace no afectan a roles de administrador de Hola que Hola usuario tiene en otro inquilino.

## <a name="synchronization-independence"></a>Independencia de sincronización
Puede configurar cada Azure AD independientemente inquilino datos tooget sincronizados desde una sola instancia de uno de ellos:

* herramienta de Hello Azure AD Connect, toosynchronize datos con un único bosque de AD.
* Hola a inquilino de Azure Active conector para Forefront Identity Manager, datos toosynchronize con uno o más de forma local bosques o los orígenes de datos de AD no sea de Azure.

## <a name="add-an-azure-ad-tenant"></a>Adición de un inquilino de Azure AD
tooadd un inquilino de Azure AD en hello portal de Azure, el inicio de sesión demasiado[Hola portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global de Azure AD y, a la izquierda de hello, seleccione **nuevo**.

> [!NOTE]
> A diferencia de otros recursos de Azure, los inquilinos no son recursos secundarios de una suscripción a Azure. Si su suscripción de Azure se cancela o expirada, es posible tener acceso los datos de inquilinos mediante Azure PowerShell, Hola API Graph de Azure o centro de administración de hello Office 365. También puede asociar otra suscripción de inquilino de Hola.
>

## <a name="next-steps"></a>Pasos siguientes
Para obtener una amplia visión general de los problemas de licencias de Azure AD y prácticas recomendadas, consulte [¿Qué es la licencia de inquilinos de Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
