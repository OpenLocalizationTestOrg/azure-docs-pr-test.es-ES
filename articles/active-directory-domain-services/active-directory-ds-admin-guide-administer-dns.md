---
title: "Azure Active Directory Domain Services: administración de DNS en dominios administrados | Microsoft Docs"
description: "Administración de DNS en dominios administrados de Azure Active Directory Domain Services"
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
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a>Administración de DNS en un dominio administrado con Servicios de dominio de Azure AD
Azure Active Directory Domain Services incluye un servidor DNS (resolución de nombres de dominio) que proporciona una resolución DNS para el dominio administrado Hola. En ocasiones, puede que tenga tooconfigure DNS en el dominio de hello administrado. Puede que tenga toocreate los registros DNS para equipos que no están toohello Unidos a un dominio, configurar direcciones IP virtuales para equilibradores de carga o configurar reenviadores DNS externos. Por este motivo, los usuarios que pertenecen a grupo de 'Administradores de controlador de dominio de AAD' toohello se les conceden privilegios de administración de DNS en el dominio administrado Hola.

## <a name="before-you-begin"></a>Antes de empezar
tareas de hello tooperform enumeradas en este artículo, necesita:

1. Una **suscripción de Azure**válida.
2. Un **directorio de Azure AD** : sincronizado con un directorio local o solo en la nube.
3. **Servicios de dominio de Azure AD** debe estar habilitada para directorio de hello Azure AD. Si lo ha hecho, siga todas las tareas de hello descritas en hello [Guía de introducción](active-directory-ds-getting-started.md).
4. A **Unidos al dominio máquina virtual** desde que se administra Hola dominio administrado de los servicios de dominio de AD de Azure. Si no tiene una máquina virtual de este tipo, siga todas las tareas de hello, que se describen en el artículo de hello titulado [unirse a un dominio administrado de Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. Necesita credenciales de Hola de un **grupo 'Administradores de controlador de dominio de AAD' toohello que pertenecen de cuentas de usuario** en el directorio, tooadminister DNS para el dominio administrado.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a>Tarea 1: aprovisionar un tooremotely unido al dominio virtual machine administrar DNS para el dominio administrado Hola
Azure dominios administrados de servicios de dominio de Active Directory pueden administrarse de forma remota mediante las conocidas herramientas administrativas de Active Directory como Hola Active Directory centro de administración (ADAC) o AD PowerShell. De forma similar, DNS para el dominio administrado Hola pueden administrarse de forma remota con herramientas de administración de servidor DNS de Hola.

Los administradores de su directorio Azure AD no tiene controladores de privilegios tooconnect toodomain en hello dominio administrado a través de escritorio remoto. Los miembros del grupo de 'Administradores de controlador de dominio de AAD' hello pueden administrar DNS dominios administrados de forma remota con las herramientas de servidor DNS desde un equipo cliente de Windows Server que es dominio administrado toohello combinadas. Herramientas de servidor DNS pueden instalarse como parte de la característica opcional de herramientas de administración remota del servidor (RSAT) de hello en Windows Server y equipos cliente Unidos a un dominio toohello administrado.

Hola primera tarea es tooprovision una máquina virtual de Windows Server que es el dominio administrado toohello combinadas. Para obtener instrucciones, consulte el artículo toohello titulado [unirse a un dominio administrado de los servicios de dominio de AD de Azure de Windows Server máquina virtual tooan](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a>Tarea 2: herramientas de instalar un servidor DNS en la máquina virtual de Hola
Realizar Hola siguientes herramientas de administración de DNS de Hola de tooinstall de pasos en la máquina virtual de hello Unidos a un dominio. Para más información sobre cómo [instalar y usar Herramientas de administración remota del servidor](https://technet.microsoft.com/library/hh831501.aspx), consulte TechNet.

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
9. En hello **características** página, haga clic en hello tooexpand **herramientas de administración remota del servidor** nodo y, a continuación, haga clic en hello tooexpand **herramientas de administración de roles** nodo. Seleccione **herramientas del servidor DNS** característica de lista de Hola de herramientas de administración de roles.

    ![Página Características](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. En hello **confirmación** página, haga clic en **instalar** características de las herramientas de servidor DNS de hello tooinstall en la máquina virtual de Hola. Cuando finalice correctamente la instalación de características, haga clic en **cerrar** tooexit hello **agregar Roles y características** asistente.

    ![Página de confirmación](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a>Tarea 3: iniciar Hola DNS administración consola tooadminister DNS
Ahora que Hola herramientas del servidor DNS se instala la característica en hello Unidos a un dominio virtual machine, podemos usar Hola DNS herramientas tooadminister DNS en el dominio de hello administrado.

> [!NOTE]
> Deberá toobe un miembro del grupo de hello 'AAD de DC administradores', tooadminister DNS en el dominio administrado Hola.
>
>

1. En la pantalla de inicio de bienvenida, haga clic en **herramientas administrativas**. Debería ver Hola **DNS** consola instalada en la máquina virtual de Hola.

    ![Herramientas administrativas: consola DNS](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. Haga clic en **DNS** consola de administración DNS toolaunch Hola.
3. Hola **conectar tooDNS Server** cuadro de diálogo, haga clic en la opción de hello titulada **Hola siguientes equipo**y escriba el nombre de dominio DNS de Hola de dominio administrados hello (por ejemplo, ' contoso100.com').

    ![La consola DNS: conectar toodomain](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. Hola consola DNS conecta dominio administrado toohello.

    ![Consola DNS: administración del dominio](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. Ahora puede usar las entradas DNS de hello DNS consola tooadd para los equipos de red virtual de hello en el que se han habilitado los servicios de dominio de AAD.

> [!WARNING]
> Tenga cuidado al administrar DNS para hello administrados mediante herramientas de administración de DNS del dominio. Asegúrese de que **no eliminar ni modificar Hola integrados los registros DNS que se utilizan los servicios de dominio de dominio hello**. Los registros DNS integrados incluyen registros DNS de dominio, registros de servidor de nombres y otros registros usados para la ubicación del controlador de dominio. Si modifica estos registros, se interrumpen los servicios de dominio de red virtual de Hola.
>
>

Vea hello [herramientas DNS artículo en Technet](https://technet.microsoft.com/library/cc753579.aspx) para obtener más información sobre la administración de DNS.

## <a name="related-content"></a>Contenido relacionado
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Unirse a un dominio administrado de Windows Server máquina virtual tooan servicios de dominio de AD de Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administración de un dominio administrado con Servicios de dominio de Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Herramientas de DNS](https://technet.microsoft.com/library/cc753579.aspx)
