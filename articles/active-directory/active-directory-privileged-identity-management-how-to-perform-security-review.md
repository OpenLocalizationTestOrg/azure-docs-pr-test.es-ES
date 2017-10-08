---
title: "aaaHow tooperform una revisión de acceso | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooperform un nuevo examen con Hola aplicación de Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a>¿Cómo tooperform un acceso Revise en Azure AD Privileged Identity Management
Active Directory (AD) Privileged Identity Management de Azure simplifica cómo las empresas administran tooresources de acceso con privilegios en Azure AD y otros servicios en línea de Microsoft como Office 365 o Microsoft Intune.  

Si se le asigna el rol administrativo tooan, Administrador de roles con privilegios de su organización puede pedirle que tooregularly confirmar que aún es necesario dicho rol para el trabajo. Puede obtener un correo electrónico que incluye un vínculo, o puede ir recta toohello [portal de Azure](https://portal.azure.com). Siga los pasos de hello en este tooperform artículo revisar automáticamente los roles asignados.

Si es un administrador de roles con privilegios interesado en las revisiones de acceso, obtenga más información en [cómo toostart un acceso revisar](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="add-hello-privileged-identity-management-application"></a>Agregar aplicación de hello Privileged Identity Management
Puede utilizar aplicaciones de administración de identidad con privilegios (PIM) hello Azure AD en hello [portal de Azure](https://portal.azure.com/) tooperform revisarse.  Si no tiene la aplicación de Azure AD Privileged Identity Management de hello en el portal, siga estas tooget pasos que se inició.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Seleccione el nombre de usuario en hello superior derecho de hello portal de Azure y directorio Hola seleccione donde tendrá estar en funcionamiento.
3. Seleccione **más servicios** y usar hello toosearch de cuadro de texto de filtro para **Azure AD Privileged Identity Management**.
4. Comprobar **Pin toodashboard** y, a continuación, haga clic en **crear**. se abrirá Hola aplicación Privileged Identity Management.

## <a name="approve-or-deny-access"></a>Aprobación o denegación de acceso
Al aprobar o denegar el acceso, está indicando solo revisor Hola si seguir utilizando este rol o no. Elija **aprobar** si desea que toostay en función de hello, o **Deny** si no necesita Hola acceso ya. Su estado no cambiará inmediatamente, hasta que el revisor de Hola aplica a los resultados de Hola.
Siga estos pasos toofind y completar la revisión de acceso de hello:

1. En la aplicación de PIM hello, seleccione **revisión privilegios de acceso**. Si tiene cualquier revisiones acceso pendiente, aparecen en hello que acceso de Azure AD revisa hoja.
2. Seleccione revisión Hola desea toocomplete.
3. A menos que cree revisión hello, parece como Hola solo usuario en revisión Hola. Seleccione siguiente tooyour nombre de marca de verificación de Hola.
4. Elija **Aprobar** o **Denegar**. Es posible que tenga una razón para la toma de decisiones en hello tooinclude **proporcionar una razón** cuadro de texto.  
5. Hola cerrar **roles de Azure AD de revisión** hoja.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
