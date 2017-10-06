---
title: grupos de aaaManaging en Active Directory de Azure | Documentos de Microsoft
description: "¿Cómo toocreate y administrar grupos toomanage Azure usuarios con Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a>Administración de grupos en Azure Active Directory
> [!div class="op_single_selector"]
> * [Portal de Azure](active-directory-groups-create-azure-portal.md)
> * [Portal de Azure clásico](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Una de las características de Hola de administración de usuarios de Azure Active Directory (Azure AD) es grupos de toocreate de capacidad de Hola de usuarios. Use un tareas de administración de grupo tooperform como la asignación de licencias o permisos tooa número de usuarios a la vez. También puede utilizar grupos el permiso de acceso a tooassign

* Recursos como los objetos de directorio de Hola
* Directorio de recursos externos toohello como aplicaciones de SaaS, servicios de Azure, sitios de SharePoint o recursos locales

Además, el propietario de un recurso también puede asignar acceso tooa tooan Azure AD fam. pertenece a otra persona. Esta asignación confiere a sus miembros Hola de ese recurso toohello de acceso de grupo. A continuación, propietario Hola del grupo de hello administra la pertenencia a grupo de Hola. De hecho, Hola recursos propietario delegados toohello propietario de hello grupo Hola permiso tooassign usuarios tootheir recurso.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. Para cómo toomanage los grupos en el centro de administración de hello Azure AD, consulte [crear un grupo y agregar miembros en Azure Active Directory](active-directory-groups-create-azure-portal.md).

## <a name="how-do-i-create-a-group"></a>¿Cómo se crea un grupo?
Dependiendo de los servicios de hello toowhich que ha suscrito su organización, puede crear un grupo mediante uno de los siguientes hello:

* Hola portal de Azure clásico
* portal de la cuenta de Hello Office 365
* portal de cuentas de Windows Intune Hola

Describiremos las tareas realizadas en hello portal de Azure clásico. Para obtener más información acerca del uso de portales de Azure no toomanage su directorio Azure AD, consulte [administrar su directorio Azure AD](active-directory-administer.md).

1. Hola [portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, a continuación, seleccione nombre de hello del directorio de Hola para su organización.
2. Seleccione hello **grupos** ficha.
3. Seleccione **Agregar grupo**.
4. Hola **Agregar grupo** ventana, especifique el nombre de Hola y Hola descripción de un grupo.

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a>Asignación o eliminación de usuarios individuales de un grupo de seguridad
**un grupo de usuarios individuales de tooa tooadd**

1. Hola [portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, a continuación, seleccione nombre de hello del directorio de Hola para su organización.
2. Seleccione hello **grupos** ficha.
3. Abra Hola grupo toowhich desea que los miembros de tooadd. Abra hello **miembros** ficha de hello seleccionado grupo si aún no se muestra.
4. Seleccione **Agregar miembros**.
5. En hello **agregar miembros** página, el nombre de hello select del usuario de Hola o un grupo que desea tooadd sea un miembro de este grupo. Asegúrese de que este nombre se ha agregado toohello **seleccionados** panel.

**tooremove un usuario individual de un grupo**

1. Hola [portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, a continuación, seleccione nombre de hello del directorio de Hola para su organización.
2. Seleccione hello **grupos** ficha.
3. Abrir grupo Hola desde el que desea que los miembros de tooremove.
4. Seleccione hello **miembros** ficha, el nombre de hello seleccione del miembro de Hola que desee tooremove de este grupo y, a continuación, haga clic en **quitar**.
5. Confirmar en el símbolo del sistema de hello tooremove este miembro del grupo de Hola.

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a>¿Cómo puedo administrar pertenencia Hola de un grupo dinámicamente?
En Azure AD, puede configurar fácilmente un toodetermine regla sencilla, los usuarios que son miembros de toobe del grupo de Hola. Una regla sencilla es aquélla que hace solo una comparación única. Por ejemplo, si se asigna a un grupo tooa aplicación SaaS, puede configurar una regla tooadd a los usuarios que tienen un puesto de trabajo de "Representante de ventas". Esta regla, a continuación, concede acceso toothis SaaS aplicación tooall a los usuarios con ese puesto de trabajo en el directorio.

Cuando los atributos de un cambio de usuario, el sistema de hello evalúa todas las reglas de grupo dinámico en un toosee de directorio si cambio de atributo de saludo del usuario de hello desencadenarán ningún grupo agrega o quita. Si un usuario cumple una regla en un grupo, se agregan como un grupo de toothat de miembro. Si ya no se cumplen regla Hola de un grupo que pertenecen, se quitan como un miembro de ese grupo.

> [!NOTE]
> Puede configurar una regla de pertenencia dinámica a grupos de seguridad o en grupos de Office 365. Las pertenencias a grupos anidados no se admiten actualmente para la asignación basada en el grupo tooapplications.
>
> Pertenencia dinámica a grupos requieren un toobe de licencia de Azure AD Premium asignada a
>
> * Administrador de Hola que administra la regla de hello en un grupo
> * Todos los miembros del grupo de Hola
>
>

**tooenable pertenencia dinámica para un grupo**

1. Hola [portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, a continuación, seleccione nombre de hello del directorio de Hola para su organización.
2. Seleccione hello **grupos** ficha y un grupo de hello abierto que desee tooedit.
3. Seleccione hello **configurar** ficha y, a continuación, establezca **habilitar pertenencias dinámicas** demasiado**Sí**.
4. Configurar una sola regla simple para hello grupo toocontrol pertenencia dinámica para las funciones de este grupo. Asegúrese de hello seguro **agregar usuarios donde** opción está seleccionada y, a continuación, seleccione una propiedad de usuario de lista de hello (por ejemplo, departamento, jobTitle, etcetera.)
5. A continuación, seleccione una condición (No es igual a, Es igual a, No empieza por, Empieza por, No contiene, Contiene, No coincide, Coincide).
6. Especifique un valor de comparación para la propiedad de usuario de hello seleccionado.

toolearn acerca de cómo toocreate *avanzadas* (reglas que puede contener varias comparaciones) para la pertenencia dinámica a grupos, consulte [utilizando atributos toocreate reglas avanzadas](active-directory-accessmanagement-groups-with-advanced-rules.md).

## <a name="additional-information"></a>Información adicional
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Administrar acceso tooresources con grupos de Active Directory de Azure](active-directory-manage-groups.md)
* [Cmdlets de Azure Active Directory para configurar las opciones de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [¿Qué es Azure Active Directory?](active-directory-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
