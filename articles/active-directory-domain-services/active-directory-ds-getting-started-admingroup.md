---
title: "Azure Active Directory Domain Services: introducción | Microsoft Docs"
description: Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)
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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)


## <a name="task-3-configure-administrative-group"></a>Tarea 3: Configuración de un grupo administrativo
En esta tarea de configuración, se crea un grupo administrativo en el directorio de Azure AD. Este grupo administrativo especial se llama *Administradores de DC de AAD*. Miembros de este grupo se conceden permisos administrativos en los equipos que están unidos al dominio toohello de dominio administrados. En equipos unidos a un dominio, este grupo se agrega el grupo de administradores de toohello. Además, los miembros de este grupo pueden utilizar Escritorio remoto tooconnect remotamente toodomain-equipos unidos a un.

> [!NOTE]
> No tiene permisos de administrador de dominio o administrador de organización en el dominio administrado Hola que ha creado mediante el uso de servicios de dominio de Active Directory de Azure. En los dominios administrados, estos permisos están reservados por el servicio de hello y no están disponibles toousers dentro de inquilino de Hola. Sin embargo, puede utilizar grupo administrativo especial Hola creado en este tooperform de tareas de configuración algunas operaciones privilegiadas. Estas operaciones incluyen unirse a dominio de equipos toohello, que pertenece el grupo de administración de toohello en equipos unidos a un dominio y la configuración de directiva de grupo.
>

Asistente de Hello crea automáticamente grupo administrativo de hello en su directorio Azure AD. Este grupo se llama "Administradores de DC de AAD". Si tiene un grupo existente con este nombre en el directorio de Azure AD, el Asistente de hello selecciona este grupo. Puede configurar la pertenencia a grupos con hello **grupo de administradores** página del asistente.

1. pertenencia a grupos de tooconfigure, haga clic en **administradores de controlador de dominio de AAD**.

    ![Configuración de la pertenencia a grupos](./media/getting-started/domain-services-blade-admingroup.png)

2. Haga clic en hello **agregar miembros** botón tooadd a los usuarios de su grupo de administradores de toohello de directorio de Azure AD.

3. Cuando haya terminado, haga clic en **Aceptar** toomove en toohello **resumen** página del Asistente para saludo.

4. En hello **resumen** página del Asistente de hello, revisión Hola de configuración de dominio administrados Hola. Puede volver atrás paso tooany de cambios de hello Asistente toomake, si es necesario. Cuando haya terminado, haga clic en **Aceptar** toocreate Hola administrado nuevo dominio.

    ![Resumen](./media/getting-started/domain-services-blade-summary.png)

5. Verá una notificación que muestra el progreso de saludo de la implementación de servicios de dominio de AD de Azure. Haga clic en la notificación de hello toosee detallada progreso para la implementación de Hola.

    ![Notificación: implementación en curso](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>Aprovisionamiento del dominio administrado
proceso de Hola de aprovisionar el dominio administrado puede tardar hasta hora tooan.

1. Mientras que la implementación está en curso, puede buscar "servicios de dominio' en hello **buscar recursos** cuadro de búsqueda. Seleccione **servicios de dominio de AD de Azure** Hola resultados de búsqueda. Hola **servicios de dominio de AD de Azure** hoja muestra hello dominio administrado que se está aprovisionando.

    ![Búsqueda del dominio administrado que se va aprovisionar](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Haga clic en Hola Hola administrado toosee de dominio (por ejemplo, ' contoso100.com') para obtener más detalles sobre el dominio de Hola.

    ![Domain Services: estado de aprovisionamiento](./media/getting-started/domain-services-provisioning-state.png)

3. Hola **Introducción** ficha muestra ese dominio de saludo se está aprovisionando actualmente. No se puede configurar dominio administrado Hola hasta que está aprovisionado por completo. Puede llevar hasta hora tooan para su toobe de dominio administrados aprovisionado por completo.

    ![Servicios de dominio - ficha información general durante Hola estado de aprovisionamiento ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Cuando el dominio administrado Hola está aprovisionado por completo, Hola **información general sobre** ficha muestra el estado del dominio de hello como **ejecutando**.

    ![Domain Services: pestaña Información general después del aprovisionamiento completo](./media/getting-started/domain-services-provisioned.png)

5. En hello **propiedades** ficha, verá dos direcciones IP en el dominio que están disponibles para la red virtual de hello controladores.

    ![Domain Services: pestaña Propiedades después del aprovisionamiento completo](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>Paso siguiente
[Tarea 4: actualizar la configuración de DNS de Hola de hello red virtual de Azure](active-directory-ds-getting-started-dns.md)
