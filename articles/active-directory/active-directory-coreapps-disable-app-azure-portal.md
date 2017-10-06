---
title: "aaaDisable inicios de sesión para una aplicación de empresa en Azure Active Directory | Documentos de Microsoft"
description: "¿Cómo toodisable una aplicación empresarial para que ningún usuario puede iniciar sesión en tooit en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Deshabilitación de los inicios de sesión de usuario de una aplicación empresarial en Azure Active Directory
Es fácil toodisable una aplicación empresarial para que ningún usuario puede iniciar sesión en tooit en Azure Active Directory (Azure AD). Debe tener la aplicación empresarial de hello permisos adecuados toomanage hello y debe ser administrador global para el directorio de Hola.

## <a name="how-do-i-disable-user-sign-ins"></a>¿Cómo puedo deshabilitar los inicios de sesión de usuario?
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba **Azure Active Directory** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.
3. En hello **Azure Active Directory** -  ***directoryname*** hoja (es decir, hello Azure AD hoja para el directorio de hello administra), seleccione **lasaplicacionesempresariales**.

    ![Apertura de Enterprise apps (Aplicaciones empresariales)](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. En hello **aplicaciones empresariales** hoja, seleccione **todas las aplicaciones**. Ver una lista de las aplicaciones de hello que puede administrar.
5. En hello **aplicaciones empresariales - todas las aplicaciones** hoja, seleccione una aplicación.
6. En hello ***appname*** hoja (es decir, Hola hoja con nombre Hola de aplicación seleccionada de hello en el título de hello), seleccione **propiedades**.

    ![Selección de Hola a todos los comandos de las aplicaciones](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. En hello ***appname*** - **propiedades** hoja, seleccione **No** para **habilitado para los usuarios de toosign?**.
8. Seleccione hello **guardar** comando.

## <a name="next-steps"></a>Pasos siguientes
* [Ver todos mis grupos](active-directory-groups-view-azure-portal.md)
* [Asignar un usuario o grupo tooan su aplicación empresarial](active-directory-coreapps-assign-user-azure-portal.md)
* [Eliminación de asignaciones de usuario o grupo de una aplicación empresarial](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Cambiar el nombre de Hola o el logotipo de una aplicación de empresa](active-directory-coreapps-change-app-logo-user-azure-portal.md)
