---
title: "Azure Active Directory Domain Services: administración de directiva de grupo en dominios administrados | Microsoft Docs"
description: "Administración de directiva de grupo en dominios administrados de Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a>Administración de directiva de grupo en un dominio administrado de Azure AD Domain Services
Azure Active Directory Domain Services incluye objetos de directiva de grupo (GPO) integrada para contenedores de hello 'AADDC usuarios' y 'AADDC equipos'. Puede personalizar estos integrados tooconfigure de GPO de directiva de grupo en el dominio administrado Hola. Además, los miembros del grupo de 'Administradores de controlador de dominio de AAD' hello pueden crear sus propias OU personalizado en el dominio administrado Hola. También puede crear GPO personalizados y vincularlas toothese personalizado unidades organizativas. Los usuarios que pertenecen a grupo de 'Administradores de controlador de dominio de AAD' toohello se les conceden privilegios de administración de directiva de grupo en el dominio administrado Hola.

## <a name="before-you-begin"></a>Antes de empezar
tareas de hello tooperform enumeradas en este artículo, necesita:

1. Una **suscripción de Azure**válida.
2. Un **directorio de Azure AD** : sincronizado con un directorio local o solo en la nube.
3. **Servicios de dominio de Azure AD** debe estar habilitada para directorio de hello Azure AD. Si lo ha hecho, siga todas las tareas de hello descritas en hello [Guía de introducción](active-directory-ds-getting-started.md).
4. A **Unidos al dominio máquina virtual** desde que se administra Hola dominio administrado de los servicios de dominio de AD de Azure. Si no tiene una máquina virtual de este tipo, siga todas las tareas de hello, que se describen en el artículo de hello titulado [unirse a un dominio administrado de Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. Necesita credenciales de Hola de un **grupo 'Administradores de controlador de dominio de AAD' toohello que pertenecen de cuentas de usuario** en el directorio, tooadminister directiva de grupo para el dominio administrado.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a>Tarea 1: aprovisionar un tooremotely unido al dominio virtual machine administrar la directiva de grupo para el dominio administrado Hola
Azure dominios administrados de servicios de dominio de Active Directory pueden administrarse de forma remota mediante las conocidas herramientas administrativas de Active Directory como Hola Active Directory centro de administración (ADAC) o AD PowerShell. De forma similar, directiva de grupo de dominio administrados Hola pueden administrarse de forma remota con herramientas de administración de directiva de grupo de Hola.

Los administradores de su directorio Azure AD no tiene controladores de privilegios tooconnect toodomain en hello dominio administrado a través de escritorio remoto. Los miembros del grupo de 'Administradores de controlador de dominio de AAD' hello pueden administrar Directiva de grupo para dominios administrados de forma remota. Puede usar herramientas de directiva de grupo en un dominio administrado de Windows Server o cliente equipo toohello combinadas. Las herramientas de directiva de grupo se pueden instalar como parte de la característica opcional de hello administración de directivas de grupo en equipos cliente y del servidor de Windows Unidos a un dominio administrado toohello.

Hola primera tarea es tooprovision una máquina virtual de Windows Server que es el dominio administrado toohello combinadas. Para obtener instrucciones, consulte el artículo toohello titulado [unirse a un dominio administrado de los servicios de dominio de AD de Azure de Windows Server máquina virtual tooan](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a>Tarea 2: herramientas de directiva de grupo de instalación en la máquina virtual de Hola
Realizar Hola siguientes herramientas de administración de directivas de grupo de pasos tooinstall hello en la máquina virtual de hello Unidos a un dominio.

1. Navegue demasiado**máquinas virtuales** nodo Hola portal de Azure clásico. Seleccione la máquina virtual de Hola que creó en la tarea 1 y haga clic en **conectar** de barra de comandos de hello en parte inferior de Hola de ventana hello.

    ![Conectar máquina virtual de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portal clásico de Hello le pedirá que tooopen o guardar un archivo con la extensión '.rdp', que es usado tooconnect toohello máquina. Cuando haya acabado la descarga, haga clic en archivo hello.
3. En el símbolo del sistema de inicio de sesión hello, use las credenciales de Hola de un usuario que pertenezca el grupo de 'Administradores de controlador de dominio de AAD' toohello. Por ejemplo, usamos 'bob@domainservicespreview.onmicrosoft.com' en nuestro caso.
4. Desde la pantalla de inicio de bienvenida, abra **el administrador del servidor**. Haga clic en **agregar Roles y características** en panel central de Hola de ventana de administrador del servidor de Hola.

    ![Inicio del Administrador del servidor en la máquina virtual](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. En hello **antes de comenzar** página de hello **agregar Roles y características Asistente**, haga clic en **siguiente**.

    ![Página Antes de comenzar](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. En hello **tipo de instalación** página, deje hello **instalación basada en roles o basada en características** opción activada y haga clic en **siguiente**.

    ![Página Tipo de instalación](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. En hello **selección de servidor** página, seleccione la máquina virtual actual de Hola Hola grupo de servidores y haga clic en **siguiente**.

    ![Página Selección de servidor](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. En hello **Roles de servidor** página, haga clic en **siguiente**. Se omite esta página, ya que no nos estamos instalar roles de servidor hello.
9. En hello **características** página, seleccione hello **Group Policy Management** característica.

    ![Página Características](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. En hello **confirmación** página, haga clic en **instalar** característica de administración de directivas de grupo de tooinstall hello en la máquina virtual de Hola. Cuando finalice correctamente la instalación de características, haga clic en **cerrar** tooexit hello **agregar Roles y características** asistente.

    ![Página de confirmación](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a>Tarea 3: iniciar Hola directiva de grupo administración consola tooadminister directiva de grupo
Puede usar consola de administración de directivas de grupo de hello en hello Unidos a un dominio máquina virtual tooadminister directiva de grupo en el dominio administrado Hola.

> [!NOTE]
> Deberá toobe un miembro del grupo de hello 'AAD de DC administradores', tooadminister directiva de grupo en el dominio administrado Hola.
>
>

1. En la pantalla de inicio de bienvenida, haga clic en **herramientas administrativas**. Debería ver Hola **Group Policy Management** consola instalada en la máquina virtual de Hola.

    ![Inicio de la Administración de directivas de grupo](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. Haga clic en **Group Policy Management** consola de administración de directivas de grupo de toolaunch Hola.

    ![Consola de directiva de grupo](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a>Tarea 4: Personalización de objetos de directiva de grupo integrados
Hay dos las objetos de directiva de grupo (GPO) - integrados uno para los contenedores de 'AADDC usuarios' y 'AADDC equipos' hello en el dominio administrado. Puede personalizar estos GPO tooconfigure directiva de grupo Hola administrado dominio.

1. Hola **Group Policy Management** de la consola, haga clic en hello tooexpand **bosque: contoso100.com** y **dominios** directivas de grupo de nodos toosee hello para el dominio administrado.

    ![GPO integrados](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. Puede personalizar estas directivas de grupo de tooconfigure GPO integradas en el dominio administrado. Haga clic en el GPO de Hola y haga clic en **editar...**  toocustomize Hola integrados GPO. herramienta del Editor de configuración de directiva de grupo de Hello permite GPO hello toocustomize.

    ![Editar GPO integrado](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. Ahora puede usar hello **Editor de administración de directivas de grupo** consola tooedit Hola integrados GPO. Por ejemplo, hello siguiente captura de pantalla muestra cómo toocustomize Hola integrado GPO "AADDC equipos".

    ![Personalizar GPO](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a>Tarea 5: Creación de un objeto de directiva de grupo (GPO) personalizado
Puede crear o importar sus propios objetos de directiva de grupo personalizados. También puede vincular personalizada personalizada tooa de GPO de unidad organizativa que ha creado en el dominio administrado. Para más información sobre la creación de unidades organizativas personalizadas, consulte [Creación de una unidad organizativa en un dominio administrado](active-directory-ds-admin-guide-create-ou.md).

> [!NOTE]
> Deberá toobe un miembro del grupo de hello 'AAD de DC administradores', tooadminister directiva de grupo en el dominio administrado Hola.
>
>

1. Hola **Group Policy Management** de la consola, haga clic en tooselect su personalizado unidad organizativa (OU). Haga clic en hello unidad organizativa y haga clic en **crear un GPO en este dominio y vincularlo aquí...** .

    ![Crear un GPO personalizado](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. Especifique un nombre para el nuevo GPO de Hola y haga clic en **Aceptar**.

    ![Especificar un nombre para el GPO](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. Un nuevo GPO se crea y se vincula tooyour personalizado OU. Haga clic en el GPO de Hola y haga clic en **editar...**  en el menú de Hola.

    ![Un GPO recién creado](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. Puede personalizar los GPO de hello recién creada mediante hello **Editor de administración de directivas de grupo**.

    ![Personalizar el nuevo GPO](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


Hay más información sobre el uso de la [Consola de administración de directivas de grupo](https://technet.microsoft.com/library/cc753298.aspx) disponible en Technet.

## <a name="related-content"></a>Contenido relacionado
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Unirse a un dominio administrado de Windows Server máquina virtual tooan servicios de dominio de AD de Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administración de un dominio administrado con Servicios de dominio de Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Consola de administración de directivas de grupo](https://technet.microsoft.com/library/cc753298.aspx)
