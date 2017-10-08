---
title: "del aaaHow tooremove un usuario acceso a la aplicación tooan | Documentos de Microsoft"
description: "Comprender cómo tooremove un usuario tener acceso a la aplicación de tooan"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 17017bddb73aad5a0ef3a411ac91bf0423f0b600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooremove-a-users-access-tooan-application"></a>¿Cómo tooremove un usuario tener acceso a la aplicación de tooan

En este artículo le ayudarán a toounderstand cómo tooremove un usuario tener acceso a la aplicación tooan.

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Deseo tooremove aplicación de tooan de asignación de un usuario específico o un grupo

tooremove una aplicación tooan de asignación de usuario o grupo, siga los pasos de hello indicados en hello [quitar una asignación de usuario o grupo de una aplicación de empresa en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artículo.

. ## deseo toodisable todas las aplicaciones de tooan de acceso para cada usuario

toodisable todos los inicios de sesión tooan aplicación de usuario, siga los pasos de hello enumerados en hello [deshabilitar inicios de sesión de usuario para una aplicación de empresa en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artículo.

## <a name="i-want-toodelete-an-application-entirely"></a>Deseo toodelete una aplicación completamente

demasiado**eliminar una aplicación**, siga estas instrucciones hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccione la aplicación hello desea toodelete.

7.  Una vez que se carga la aplicación hello, haga clic en **eliminar** icono de la aplicación de hello superior **Introducción** hoja.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Deseo toodisable todas las aplicaciones de tooany de operaciones de consentimiento de usuario futuras

Deshabilitando el consentimiento del usuario para todo el directorio impedir que los usuarios finales consentimiento tooany aplicación. A pesar de ello, los administradores podrán seguir dando el consentimiento en nombre de los usuarios. toolearn más información acerca de la aplicación de consentimiento y por qué puede o no ser conveniente toodo, lea [usuario conocimiento y consentimiento del administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

demasiado**deshabilitar todas las operaciones de consentimiento de usuario futuras en todo el directorio**, siga estas instrucciones hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Configuración de usuario**.

6.  Deshabilitar todas las operaciones de consentimiento de usuario futuras establecer hello **a los usuarios pueden permitir aplicaciones tooaccess sus datos** alternar demasiado**No** y haga clic en hello **guardar** botón.


# <a name="next-steps"></a>Pasos siguientes
[Administrar acceso tooapps](active-directory-managing-access-to-apps.md)
