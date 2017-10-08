---
title: "aaaHow toostart una revisión de acceso | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate revisar de un acceso de identidades con privilegios con hello aplicación Privileged Identity Management de Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>¿Cómo toostart un acceso Revise en Azure AD Privileged Identity Management
Las asignaciones de roles se convierten en "obsoletas" cuando los usuarios tienen acceso con privilegios que ya no necesitan. En orden tooreduce riesgo de hello asociado con estas asignaciones de funciones obsoletas, los administradores de roles con privilegios con regularidad deben revisar los roles de Hola que se les ha asignado a los usuarios. Este documento describen los pasos de hello para iniciar una revisión de acceso en Azure AD Privileged Identity Management (PIM).

## <a name="start-an-access-review"></a>Inicio de una revisión de acceso
> [!NOTE]
> Si aún no lo ha agregado tooyour panel de hello PIM aplicación Hola portal de Azure, consulte los pasos de hello en [Getting Started with Privileged Identity Management de Azure](active-directory-privileged-identity-management-getting-started.md)
> 
> 

Desde la página principal de hello PIM aplicación, hay tres toostart formas una revisión de acceso:

* **Revisiones de acceso** > **Agregar**
* Botón **Roles** > **Revisar**
* Hola seleccione rol específico toobe revisado de lista de roles de hello > **revisión** botón

Al hacer clic en hello **revisar** button, hello **iniciar una revisión de acceso** aparece hoja. En esta hoja, está continuo tooconfigure Hola revisión con un nombre y límite de tiempo, elija un rol tooreview y decidir quién llevará a cabo revisión Hola.

![Inicio de una revisión de acceso: captura de pantalla][1]

### <a name="configure-hello-review"></a>Configurar la revisión de Hola
toocreate un acceso revisar, deberá tooname y establezca una fecha de inicio y finalización.

![Configuración de una revisión: captura de pantalla][2]

Asegúrese de longitud de Hola de hello revisar tiempo suficiente para que los usuarios toocomplete. Si finaliza antes de la fecha de finalización de hello, siempre puede detener revisión Hola al principio.

### <a name="choose-a-role-tooreview"></a>Elija un rol tooreview
Cada revisión se centra solo en un rol. A menos que iniciara Hola revisión de acceso de una hoja de rol específico, deberá toochoose un rol ahora.

1. Navegue demasiado**revisar la pertenencia a roles**
   
    ![Revisión de pertenencia al rol: captura de pantalla][3]
2. Elegir un rol de la lista de Hola.

### <a name="decide-who-will-perform-hello-review"></a>Decidir quién llevará a cabo revisión Hola
Hay tres opciones para realizar una revisión. Puede asignar Hola revisión toosomeone toocomplete else, puede hacerlo usted mismo, o puede hacer que cada usuario revise su propio acceso.

1. Navegue demasiado**seleccione revisores**
   
    ![Selección de revisores: captura de pantalla][4]
2. Elija una de las opciones de hello:
   
   * **Seleccionar revisor**: utilice esta opción si no sabe quién requiere acceso. Con esta opción, puede asignar el propietario del recurso de hello revisión tooa o grupo administrador toocomplete.
   * **Me**: útil si desea toopreview cómo access revisa el trabajo, o quiere tooreview en nombre de personas que no se pueden.
   * **Revisión los miembros a sí mismos**: Utilice esta opción toohave Hola a los usuarios para revisar sus propias asignaciones de roles.

### <a name="start-hello-review"></a>Revisión de Hola de inicio
Por último, tener Hola opción toorequire que los usuarios proporcionen un motivo si aprueba su acceso. Agregue una descripción de la revisión de hello si lo desea y seleccione **iniciar**.

Asegúrese de que los usuarios saber que hay una revisión de acceso en espera para ellos y mostrarlos en [cómo tooperform un acceso revisar](active-directory-privileged-identity-management-how-to-perform-security-review.md).

## <a name="manage-hello-access-review"></a>Administrar la revisión de acceso de Hola
Puede seguir el progreso de hello revisores Hola complete sus opiniones en hello panel PIM de Azure AD, en hello access revisa la sección. Derechos de acceso no se cambiarán en el directorio de hello hasta que [revisión Hola completa](active-directory-privileged-identity-management-how-to-complete-review.md).

Hasta que se encuentra el período de revisión de hello sobre, recordar a los usuarios toocomplete su revisión o revisión de Hola de detención al principio contra el acceso de Hola revisiones sección.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>Tabla de contenido de PIM
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
