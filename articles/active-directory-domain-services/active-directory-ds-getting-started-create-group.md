---
title: 'Azure Active Directory Domain Services: Crear el grupo de administradores de controlador de dominio de hello Azure AD | Documentos de Microsoft'
description: "Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure clásico"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure clásico
Este artículo describe y le guía a través de las tareas de configuración de Hola que necesita tooenable Azure Active Directory Domain Services (Azure AD DS) para su inquilino de Azure Active Directory (Azure AD).

> [!NOTE]
> [**Pruebe en su lugar hello (versión preliminar) Azure experiencia del nuevo portal**](active-directory-ds-getting-started.md). 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a>Tarea 1: crear el grupo de administradores de controlador de dominio de hello Azure AD
Hola primera tarea es toocreate un grupo administrativo en el inquilino de Azure AD. Este grupo administrativo especial se llama *Administradores de DC de AAD*. Miembros de este grupo se conceden permisos administrativos en los equipos que están en el dominio de servicios de dominio de Active Directory de Azure administrados toohello Unidos a un dominio. En equipos unidos a un dominio, este grupo se agrega el grupo de administradores de toohello. Además, los miembros de este grupo pueden utilizar Escritorio remoto tooconnect remotamente toodomain-equipos unidos a un.  

> [!NOTE]
> No tiene permisos de administrador de dominio o administrador de organización en el dominio administrado Hola que ha creado mediante el uso de servicios de dominio de Active Directory de Azure. En los dominios administrados, estos permisos están reservados por el servicio de hello y no están disponibles toousers dentro de inquilino de Hola. Sin embargo, puede utilizar grupo administrativo especial Hola creado en este tooperform de tareas de configuración algunas operaciones privilegiadas. Estas operaciones incluyen unirse a dominio de equipos toohello, que pertenece el grupo de administración de toohello en equipos unidos a un dominio y la configuración de directiva de grupo.
>

En esta tarea de configuración, cree el grupo administrativo de Hola y agregar uno o más usuarios en el grupo de toohello de directorio. grupo administrativo de hello toocreate para Azure Active Directory Domain Services Hola siguientes:

1. Vaya toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. En el panel izquierdo de hello, seleccione hello **Active Directory** botón.
3. Seleccione el inquilino de Azure AD de hello (directorio) para el que desea que los servicios de dominio de Active Directory de tooenable Azure. Puede crear un único dominio para cada directorio de Azure AD.

    ![Selección de un directorio de Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. En hello **directorio de vista previa** página, haga clic en hello **grupos** ficha.
5. Haga clic en un inquilino de Azure AD tooyour grupo, en panel de tareas de hello en parte inferior de Hola de ventana hello, de tooadd **Agregar grupo**.

    ![botón Agregar grupo de Hola](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. Hola **Agregar grupo** diálogo cuadro, cree un grupo denominado **administradores de controlador de dominio de AAD**y, a continuación, establezca **tipo de grupo** demasiado**seguridad**.

   > [!WARNING]
   > acceso de tooenable dentro de su dominio administrado en servicios de dominio de Active Directory de Azure, cree un grupo con este nombre exacto.
   >
   >

    ![cuadro de diálogo Agregar grupo de Hola](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. Hola **descripción** cuadro, escriba una descripción que permite a otros toounderstand que este grupo concede permisos administrativos en servicios de dominio de Active Directory de Azure.
8. Después de crear el grupo de hello, haga clic en tooview de nombre de grupo de hello sus propiedades.
9. tooadd usuarios como miembros del grupo de hello, en parte inferior de Hola de ventana hello, haga clic en hello **agregar miembros** botón.

    ![Botón Agregar miembros del grupo](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. Hola **agregar miembros** cuadro de diálogo, seleccione Hola quienes deben ser miembros de este grupo y, a continuación, haga clic en el icono de marca de verificación de hello en hello inferior derecho.

    ![Agregar grupo de usuarios tooadministrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>Paso siguiente
Tarea 2: [Creación o selección de una red virtual de Azure](active-directory-ds-getting-started-vnet.md)
