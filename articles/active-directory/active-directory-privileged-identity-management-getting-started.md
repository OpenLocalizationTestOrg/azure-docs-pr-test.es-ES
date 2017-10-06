---
title: aaaGet a trabajar con Azure AD Privileged Identity Management | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage había privilegiado identidades con aplicaciones de Azure Active Directory Privileged Identity Management de hello en el portal de Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Comenzar a usar Azure AD Privileged Identity Management
Con Privileged Identity Management de Azure Active Directory (AD), puede administrar, controlar y supervisar el acceso dentro de su organización. Este ámbito incluye tooresources de acceso de Azure AD y otros servicios en línea de Microsoft como Office 365 o Microsoft Intune.

Este artículo explica cómo tooadd Hola tooyour de aplicación de Azure AD PIM Azure panel del portal.

## <a name="add-hello-privileged-identity-management-application"></a>Agregar aplicación de hello Privileged Identity Management
Antes de usar Azure AD Privileged Identity Management, debe tooadd Hola aplicación tooyour Azure panel del portal.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) como administrador global de su directorio.
2. Si su organización tiene más de un directorio, seleccione el nombre de usuario en hello superior derecha del programa Hola a portal de Azure. Seleccione el directorio de hello en el que desea toouse PIM.
3. Seleccione **más servicios** y usar hello toosearch de cuadro de texto de filtro para **Azure AD Privileged Identity Management**.
4. Comprobar **Pin toodashboard** y, a continuación, haga clic en **crear**. Hola aplicación Privileged Identity Management se abre.

Si está hello primera persona toouse AD Privileged Identity Management de Azure en el directorio, se asignan automáticamente hello **Administrador de seguridad** y **Administrador de roles con privilegios de** roles en el directorio de Hola. Solo los administradores de roles con privilegios pueden administrar las asignaciones de roles de los usuarios. Además, puede elegir hello toorun [Asistente para la seguridad.](active-directory-privileged-identity-management-security-wizard.md) le guía a través de la experiencia de detección y asignación inicial Hola.

## <a name="navigate-tooyour-tasks"></a>Navegar por las tareas de tooyour
Una vez que se ha configurado AD Privileged Identity Management de Azure, consulte hoja de navegación de hello cada vez que abra la aplicación hello. Use esta hoja tooaccomplish las tareas de administración de identidad.

![Tareas de nivel superior para PIM (captura de pantalla)](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **Mi Roles** toma tooa lista de roles que se asignan tooyou. Esta sección es donde activará los roles para los que es apto.
* **Aprobar solicitudes (versión preliminar)** muestra una lista de solicitudes de activación pendientes de los usuarios del directorio. [Más información.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **(Vista previa) de solicitudes pendientes** muestra cualquier tooactivate de toohave realizan las solicitudes actuales.
* **Revise el acceso** toma tooany pendientes acceso revisa necesita toocomplete, si se está revisando el acceso para usted mismo u otra persona.
* **Roles de directorio de Azure AD** ubicado en la sección "Administrar" hello es el panel de Hola para asignaciones de roles con privilegios del rol administradores toomanage, cambiar la configuración de activación de rol, revisiones de acceso de inicio y mucho más. Opciones de Hello en este panel se deshabilitan para cualquier persona que no es un administrador de roles con privilegios.

## <a name="next-steps"></a>Pasos siguientes
Hola [Introducción a Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) incluye más detalles sobre cómo administrar el acceso administrativo en su organización.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
