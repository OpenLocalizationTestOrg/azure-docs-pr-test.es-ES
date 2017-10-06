---
title: "vista previa de administración de unidades de aaaAdministrative en Azure Active Directory"
description: "Uso de unidades administrativas para una delegación más detallada de permisos en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>Administración de unidades administrativas en Azure AD: versión preliminar pública
Este artículo describen las unidades administrativas: un nuevo contenedor de Azure Active Directory de recursos que puede usar para delegar permisos administrativos en subconjuntos de usuarios y aplicar subconjunto tooa de directivas de usuarios. En Azure Active Directory, unidades administrativas permiten que los administradores de los administradores centrales toodelegate permisos tooregional o tooset directiva en un nivel específico.

Esto es útil en organizaciones con divisiones independientes, por ejemplo, una universidad grande que se compone de varias escuelas autónomas (escuela de negocios, escuela de ingenieros, etc.) que son independientes entre ellas. Estas divisiones tienen sus propios administradores de TI que controlan el acceso, administran usuarios y establecen directivas específicamente para su división. Los administradores centrales desean toobe puede conceder estos permisos de división de los administradores sobre los usuarios de hello en sus divisiones particulares. Más concretamente, con este ejemplo, un administrador central puede, por ejemplo, crear una unidad administrativa para una determinada escuela (escuela de negocios) y rellenarla con solo los usuarios con hello empresariales school. A continuación, un administrador central puede agregar escuela de negocios de hello función de tooa ámbito de personal de TI, en otras palabras, conceder Hola personal de TI de permisos administrativos de escuela de negocios sólo a través de unidad administrativa de escuela de negocios de Hola.

> [!IMPORTANT]
> Puede asignar roles de administrador con rol de unidad administrativa solo si habilita Azure Active Directory Premium. Para obtener más información, consulte [Introducción a Azure AD Premium](active-directory-get-started-premium.md).
>


Desde el punto de vista del administrador central de hello, una unidad administrativa es un objeto de directorio que se pueden crear y rellenar con recursos. **En esta versión preliminar, estos recursos solo pueden ser usuarios.** Una vez creada y rellenada, unidad administrativa Hola puede usarse como un Hola de toorestrict ámbito permiso sólo a través de recursos contenidos en la unidad administrativa Hola.

## <a name="managing-administrative-units"></a>Administración de unidades administrativas
En esta versión preliminar, puede crear y administrar unidades administrativas mediante cmdlets de hello Azure módulo Active Directory para Windows PowerShell. más información acerca de cómo toolearn toodo que vea [trabajar con unidades administrativas](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

Para obtener más información sobre los requisitos de software e instalar módulo hello Azure AD y para obtener información sobre Hola cmdlets de módulo de Azure AD para administrar unidades administrativas, incluida la sintaxis, descripciones de parámetros y ejemplos, vea [activa de Azure Directorio PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).

## <a name="next-steps"></a>Pasos siguientes
[Ediciones de Azure Active Directory](active-directory-editions.md)
