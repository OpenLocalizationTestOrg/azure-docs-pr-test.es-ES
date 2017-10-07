---
title: "Azure Active Directory Domain Services: administración de un dominio administrado | Microsoft Docs"
description: "Administración de dominios administrados con Servicios de dominio de Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a>Administración de un dominio administrado con Servicios de dominio de Azure Active Directory
Este artículo muestra cómo tooadminister los servicios de dominio de Azure Active Directory (AD) administra el dominio.

## <a name="before-you-begin"></a>Antes de empezar
tareas de hello tooperform enumeradas en este artículo, necesita:

1. Una **suscripción de Azure**válida.
2. Un **directorio de Azure AD** : sincronizado con un directorio local o solo en la nube.
3. **Servicios de dominio de Azure AD** debe estar habilitada para directorio de hello Azure AD. Si lo ha hecho, siga todas las tareas de hello descritas en hello [Guía de introducción](active-directory-ds-getting-started.md).
4. A **Unidos al dominio máquina virtual** desde que se administra Hola dominio administrado de los servicios de dominio de AD de Azure. Si no tiene una máquina virtual de este tipo, siga todas las tareas de hello, que se describen en el artículo de hello titulado [unirse a un dominio administrado de Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. Necesita credenciales de Hola de un **grupo 'Administradores de controlador de dominio de AAD' toohello que pertenecen de cuentas de usuario** en el directorio, tooadminister el dominio administrado.

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a>Tareas administrativas que puede realizar en un dominio administrado
Los miembros del grupo de 'Administradores de controlador de dominio de AAD' hello se les conceden privilegios en el dominio administrado Hola que les permitan tooperform tareas como:

* Unirse a dominio administrados de máquinas toohello.
* Configurar GPO integrados de Hola para contenedores de 'AADDC usuarios' y 'AADDC equipos' hello en dominio administrado Hola.
* Administrar DNS en el dominio administrado Hola.
* Crear y administrar a personalizado unidades organizativas (OU) en el dominio administrado Hola.
* Ganancia acceso administrativo toocomputers Unidos a un dominio administrado toohello.

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a>Privilegios de administrador que no tiene en un dominio administrado
dominio de Hello es administrada por Microsoft, incluidas las actividades, como la aplicación de revisiones, supervisión y realizar copias de seguridad. Por lo tanto, dominio Hola está bloqueado y no tiene privilegios tooperform ciertas tareas administrativas en el dominio de Hola. A continuación se proporcionan algunos ejemplos de tareas que no puede realizar.

* No se conceden privilegios de administrador de dominio o administrador de organización para el dominio administrado Hola.
* No se puede extender el esquema Hola de dominio administrados Hola.
* No se puede conectar toodomain controladores para hello dominio administrado mediante Escritorio remoto.
* No se puede agregar el dominio administrado de toohello de controladores de dominio.

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a>Tarea 1: aprovisionar una máquina virtual de Windows Server Unidos a un dominio, tooremotely administrar dominio administrado Hola
Azure dominios administrados de servicios de dominio de Active Directory pueden administrarse con conocidas herramientas administrativas de Active Directory como Hola Active Directory centro de administración (ADAC) o AD PowerShell. Los administradores de inquilinos no tiene controladores de privilegios tooconnect toodomain en hello dominio administrado a través de escritorio remoto. Por lo tanto, los miembros del programa Hola puede administrar el grupo 'Administradores de controlador de dominio de AAD' administran de forma remota con herramientas administrativas de AD desde un equipo cliente de Windows Server que es dominio administrado toohello combinada de dominios. Herramientas administrativas de AD se pueden instalar como parte de la característica opcional de herramientas de administración remota del servidor (RSAT) de hello en equipos cliente y del servidor de Windows Unidos a un dominio toohello administrado.

Hola primer paso es tooset una máquina virtual de Windows Server que es dominio combinados toohello administrado. Para obtener instrucciones, consulte el artículo toohello titulado [unirse a un dominio administrado de los servicios de dominio de AD de Azure de Windows Server máquina virtual tooan](active-directory-ds-admin-guide-join-windows-vm.md).

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a>Administrar Hola de dominio administrados de forma remota desde un equipo cliente (por ejemplo, Windows 10)
Hola instrucciones que aparecen en este artículo utilizan un hello tooadminister de máquina virtual de Windows Server AAD DS administra el dominio. Sin embargo, también puede elegir toouse un toodo de máquina virtual de cliente (por ejemplo, Windows 10) de Windows así.

También puede [instalar herramientas de administración remota del servidor (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) en una máquina virtual de cliente de Windows, siga las instrucciones de hello en TechNet.

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a>Tarea 2: herramientas de administración de la instalación de Active Directory en la máquina virtual de Hola
Realizar Hola siguientes herramientas de administración de Active Directory de pasos tooinstall hello en la máquina virtual de hello Unidos a un dominio. Para más [información sobre la instalación y el uso de Herramientas de administración remota del servidor](https://technet.microsoft.com/library/hh831501.aspx).

1. Navegue demasiado**máquinas virtuales** nodo Hola portal de Azure clásico. Seleccione la máquina virtual de Hola que creó en la tarea 1 y haga clic en **conectar** de barra de comandos de hello en parte inferior de Hola de ventana hello.

    ![Conectar máquina virtual de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portal clásico de Hello le pedirá que tooopen o guardar un archivo con la extensión '.rdp', que es usado tooconnect toohello máquina. Cuando haya acabado la descarga, haga clic en archivo de hello tooopen.
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
9. En hello **características** página, haga clic en hello tooexpand **herramientas de administración remota del servidor** nodo y, a continuación, haga clic en hello tooexpand **herramientas de administración de roles** nodo. Seleccione **AD DS y AD LDS herramientas** característica de lista de Hola de herramientas de administración de roles.

    ![Página Características](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. En hello **confirmación** página, haga clic en **instalar** característica tooinstall Hola AD y herramientas de AD LDS en la máquina virtual de Hola. Cuando finalice correctamente la instalación de características, haga clic en **cerrar** tooexit hello **agregar Roles y características** asistente.

    ![Página de confirmación](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a>Tarea 3: conectar tooand explorar dominio administrado Hola
Ahora que se instalan herramientas administrativas Hola AD en hello Unidos a un dominio máquina virtual, podemos usar estas herramientas tooexplore y administrar el dominio administrado Hola.

> [!NOTE]
> Necesita toobe un miembro del grupo de 'Administradores de controlador de dominio de AAD' hello, hello tooadminister administra el dominio.
>
>

1. En la pantalla de inicio de bienvenida, haga clic en **herramientas administrativas**. Debería ver herramientas administrativas Hola AD instaladas en la máquina virtual de Hola.

    ![Herramientas administrativas instaladas en el servidor](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Haga clic en **Centro de administración de Active Directory**.

    ![Centro de administración de Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. dominio de hello tooexplore, haga clic en el nombre de dominio de hello en el panel izquierdo de hello (por ejemplo, ' contoso100.com'). Observe dos contenedores denominados "AADDC equipos" y "Usuarios de AADDC" respectivamente.

    ![ADAC: ver dominio](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. Haga clic en el contenedor de hello denominado **AADDC usuarios** toosee administran todos los usuarios y grupos que pertenezcan toohello dominio. Debería ver las cuentas de usuario y grupos de su inquilino de Azure AD en este contenedor. Observe que en este ejemplo, una cuenta de usuario para el usuario de hello denominado 'bob' y un grupo llamado 'Administradores de controlador de dominio de AAD' están disponibles en este contenedor.

    ![ADAC: usuarios del dominio](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. Haga clic en el contenedor de hello denominado **AADDC equipos** equipos de hello toosee Unidos a un dominio administrado toothis. Debería ver una entrada para la máquina virtual actual hello, que es toohello Unidos a un dominio. Cuentas de equipo para todos los equipos que están unidos a un toohello dominio administrado se almacenan en este contenedor "AADDC equipos" de servicios de dominio de AD de Azure.

    ![ADAC: equipos unidos al dominio](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a>Contenido relacionado
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Unirse a un dominio administrado de Windows Server máquina virtual tooan servicios de dominio de AD de Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Implementar herramientas de administración remota del servidor](https://technet.microsoft.com/library/hh831501.aspx)
