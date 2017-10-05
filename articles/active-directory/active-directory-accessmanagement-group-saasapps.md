---
title: Uso de un grupo para administrar el acceso a aplicaciones SaaS| Microsoft Docs
description: "Cómo usar grupos en Azure Active Directory Premium o Basic para asignar el acceso a aplicaciones SaaS integradas con Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a>Uso de un grupo para administrar el acceso a las aplicaciones SaaS
Con Azure Active Directory (Azure AD) y una licencia de Azure AD Premium o Azure AD Basic, puede usar grupos para asignar el acceso a una aplicación SaaS integrada con Azure AD. Por ejemplo, si desea asignar acceso al departamento de marketing para utilizar cinco aplicaciones SaaS diferentes, puede crear un grupo que contenga a los usuarios del departamento de marketing y, a continuación, asignar ese grupo a las cinco aplicaciones SaaS requeridas por el departamento de marketing. De este modo, ahorrará tiempo administrando la pertenencia a grupos del departamento de marketing en un solo lugar. A continuación, los usuarios se asignan a la aplicación cuando se agregan como miembros del grupo de marketing, y se eliminan sus asignaciones de la aplicación cuando se eliminan del grupo de marketing.

> [!IMPORTANT]
> Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo. 

Esta función se puede utilizar con cientos de aplicaciones que puede agregar desde la Galería de aplicaciones de Azure AD.

**Para asignar acceso para un grupo a una aplicación SaaS**

1. En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory** en la barra de navegación izquierda.
2. Seleccione la pestaña **Directorio** y abra el directorio en el que desea asignar el acceso para un grupo a una aplicación SaaS.
3. Seleccione la pestaña **Aplicaciones** . Seleccione una aplicación que haya agregado desde la Galería de aplicaciones y haga clic en la pestaña **Usuarios y grupos**.
4. En la pestaña **Usuarios y grupos**, en el campo **Empezando por**, escriba el nombre del grupo al que desea asignar acceso y seleccione la marca de verificación en la esquina superior derecha. Solo necesita escribir la primera parte del nombre de un grupo.
5. Seleccione el grupo y luego seleccione el botón **Asignar acceso** . Seleccione **Sí** cuando aparezca el mensaje de confirmación. No se admiten las pertenencias a grupos anidadas para la asignación basada en grupos a aplicaciones en este momento.
6. También puede ver qué usuarios están asignados a la aplicación, directamente o mediante la pertenencia a un grupo. Para ello, cambie la opción **Mostrar lista desplegable de "Grupos"** a **"Todos los usuarios"**. La lista muestra los usuarios en el directorio y si cada uno de ellos está asignado o no a la aplicación. La lista también muestra si los usuarios asignados están asignados a la aplicación directamente (el tipo de asignación aparece como "Directo"), o en virtud de la pertenencia a un grupo (el tipo de asignación aparece como "Heredado").

> [!NOTE]
> Solo después de habilitar Azure AD Premium o Azure AD Basic verá la pestaña Usuarios y grupos.
>
>

### <a name="next-steps"></a>Pasos siguientes
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Administración del acceso a los recursos con grupos de Azure Active Directory](active-directory-manage-groups.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Cmdlets de Azure Active Directory para configurar las opciones de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [¿Qué es Azure Active Directory?](active-directory-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
