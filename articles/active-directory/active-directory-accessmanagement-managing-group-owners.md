---
title: "Pasos siguientes para la administración de acceso mediante grupos | Microsoft Docs"
description: Procedimientos avanzados para administrar grupos de seguridad y uso de estos grupos para administrar el acceso a un recurso.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a>Administración de propietarios de un grupo
Una vez que un propietario de recursos haya asignado acceso a un recurso a un grupo de Azure AD, el propietario del grupo será quien administre los miembros del grupo. El propietario del recursos delega de manera eficaz el permiso para asignar usuarios al recurso al propietario del grupo.

> [!IMPORTANT]
> Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo. 

## <a name="assigning-group-ownership"></a>Asignación de la propiedad de un grupo
**Para agregar un propietario a un grupo**

1. En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y luego abra el directorio de su organización.
2. Seleccione la pestaña **Grupos** y abra el grupo al que desea agregar propietarios.
3. Seleccione **Agregar propietarios**.
4. En la página **Agregar propietarios**, seleccione el usuario que desea agregar como propietario del grupo y asegúrese de que este nombre se agrega al panel **Seleccionados**.

**Para quitar un propietario de un grupo**

1. En el [Portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y luego abra el directorio de su organización.
2. Seleccione la pestaña **Grupos** y abra el grupo del que desea quitar un propietario.
3. Seleccione la pestaña **Propietarios** .
4. Seleccione el propietario que desea quitar del grupo y luego seleccione **Quitar**.

## <a name="additional-information"></a>Información adicional
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Administración del acceso a los recursos con grupos de Azure Active Directory](active-directory-manage-groups.md)
* [Cmdlets de Azure Active Directory para configurar las opciones de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [¿Qué es Azure Active Directory?](active-directory-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
