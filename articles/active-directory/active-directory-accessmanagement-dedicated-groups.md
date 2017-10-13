---
title: Grupos dedicados en Azure Active Directory | Microsoft Docs
description: "Información general sobre cómo funcionan los grupos específicos en Azure Active Directory y cómo se crean."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;oldportal
ms.openlocfilehash: 992f4563064d7a292cf4fdd90a9a3c84cdec91c0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Grupos dedicados en Azure Active Directory
En Azure Active Directory (Azure AD), la característica de grupos dedicados crea y rellena automáticamente la pertenencia para grupos predefinidos de Azure AD. No es posible agregar ni quitar miembros de grupos dedicados mediante el Portal de Azure clásico, los cmdlets de Windows PowerShell o de manera programática.

> [!NOTE]
> Los grupos dedicados requieren que se asigne una licencia de Azure AD Premium:
>
> * Al administrador que administra la regla en un grupo
> * A todos los usuarios que la regla selecciona para que sean miembros del grupo
>
>

**Para habilitar los grupos dedicados**

1. En [Azure Portal](https://portal.azure.com), seleccione **Active Directory** y luego abra el directorio de su organización.
2. Seleccione la pestaña **Grupos** y abra el grupo que desea editar.
3. Seleccione la pestaña **Configurar** y en **Habilitar grupos dedicados**, seleccione **Sí**.

Una vez que en Habilitar grupos dedicados se selecciona **Sí**, se puede habilitar el directorio para que cree automáticamente el grupo dedicado Todos los usuarios, para lo que en **Habilitar grupo " Todos los usuarios"** es preciso seleccionar **Sí**. También puede editar el nombre de este grupo dedicado; para ello, escríbalo en el campo **Nombre para mostrar del grupo “**Todos los usuarios**”** .

El grupo Todos los usuarios puede usarse para asignar los mismos permisos a todos los usuarios del directorio. Por ejemplo, puede otorgar a todos los usuarios del directorio acceso a una aplicación SaaS si asigna acceso a esta aplicación para el grupo dedicado Todos los usuarios.

El grupo dedicado Todos los usuarios incluye a todos los usuarios del directorio, incluidos los invitados y los usuarios externos. Si necesita un grupo que excluya a los usuarios externos, puede crear un grupo con una regla dinámica basada en atributos, como la siguiente:

                (user.userPrincipalName -notContains "#EXT#@")

Para crear un grupo que excluya a todos los invitados, use una regla como la siguiente:

                (user.userType -ne "Guest")

Para obtener información acerca de cómo crear reglas *avanzadas* (reglas que pueden contener comparaciones múltiples) para la pertenencia a grupos dinámicos, consulte [Uso de atributos para crear reglas avanzadas](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Pasos siguientes
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Administración del acceso a los recursos con grupos de Azure Active Directory](active-directory-manage-groups.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [¿Qué es Azure Active Directory?](active-directory-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
