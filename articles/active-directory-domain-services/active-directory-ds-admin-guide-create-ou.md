---
title: "Active Directory Domain Services: guía de administración | Microsoft Docs"
description: "Creación de una unidad organizativa (OU) en dominios administrados de Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a>Creación de una unidad organizativa en un dominio administrado de Servicios de dominio de Azure AD
Los dominios administrados de Servicios de dominio de Azure AD incluyen dos contenedores integrados denominados "AADDC Computers" y "AADDC Users", respectivamente. Hello 'AADDC equipos' contenedor tiene objetos de equipo para todos los equipos que están unidos a un dominio administrado toohello. contenedor de 'AADDC usuarios' Hello incluye usuarios y grupos en el inquilino de Azure AD de Hola. En ocasiones, es posible que las cuentas de servicio de toocreate necesarios en las cargas de trabajo de hello administrado dominio toodeploy. Para ello, puede crear una unidad organizativa (UO) personalizado en el dominio administrado hello y crear cuentas de servicio dentro de esa unidad organizativa. Este artículo muestra cómo toocreate una unidad organizativa en el dominio administrado.

## <a name="before-you-begin"></a>Antes de empezar
tareas de hello tooperform enumeradas en este artículo, necesita:

1. Una **suscripción de Azure**válida.
2. Un **directorio de Azure AD** : sincronizado con un directorio local o solo en la nube.
3. **Servicios de dominio de Azure AD** debe estar habilitada para directorio de hello Azure AD. Si lo ha hecho, siga todas las tareas de hello descritas en hello [Guía de introducción](active-directory-ds-getting-started.md).
4. Una máquina virtual de Unidos a un dominio desde el que administra los servicios de dominio de hello Azure AD administra el dominio. Si no tiene una máquina virtual de este tipo, siga todas las tareas de hello, que se describen en el artículo de hello titulado [unirse a un dominio administrado de Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. Necesita credenciales de Hola de un **grupo 'Administradores de controlador de dominio de AAD' toohello que pertenecen de cuentas de usuario** en el directorio, toocreate una OU personalizada en el dominio administrado.

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a>Instalación de herramientas de administración de AD en una máquina virtual unida a dominio para la administración remota
Azure dominios administrados de servicios de dominio de Active Directory pueden administrarse de forma remota mediante las conocidas herramientas administrativas de Active Directory como Hola Active Directory centro de administración (ADAC) o AD PowerShell. Los administradores de inquilinos no tiene controladores de privilegios tooconnect toodomain en hello dominio administrado a través de escritorio remoto. tooadminister Hola dominio administrado, instalar la característica de herramientas de administración de hello AD en un dominio administrado toohello combinadas de máquina virtual. Consulte el artículo toohello titulado [administrar un dominio administrado de los servicios de dominio de AD de Azure](active-directory-ds-admin-guide-administer-domain.md) para obtener instrucciones.

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a>Crear a una unidad organizativa en el dominio administrado Hola
Ahora que se instalan herramientas administrativas Hola AD en hello Unidos a un dominio máquina virtual, podemos usar estas herramientas toocreate una unidad organizativa en el dominio de hello administrado. Lleve a cabo Hola pasos:

> [!NOTE]
> Solo los miembros del grupo de 'Administradores de controlador de dominio de AAD' hello ha Hola toocreate de privilegios necesarios en una OU personalizada. Asegúrese de que lleva a cabo Hola siguiendo los pasos como un usuario que pertenece el grupo de toothis.
>
>

1. En la pantalla de inicio de bienvenida, haga clic en **herramientas administrativas**. Debería ver herramientas administrativas Hola AD instaladas en la máquina virtual de Hola.

    ![Herramientas administrativas instaladas en el servidor](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Haga clic en **Centro de administración de Active Directory**.

    ![Centro de administración de Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. dominio de hello tooview, haga clic en el nombre de dominio de hello en el panel izquierdo de hello (por ejemplo, ' contoso100.com').

    ![ADAC: ver dominio](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. En el lado derecho de hello **tareas** panel, haga clic en **New** en el nodo de nombre de dominio de Hola. En este ejemplo, hacemos clic en **New** en el nodo de 'contoso100(local)' hello en el lado derecho de hello **tareas** panel.

    ![ADAC: nueva unidad organizativa](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. Debería ver Hola opción toocreate una unidad organizativa. Haga clic en **unidad organizativa** toolaunch hello **crear unidad organizativa** cuadro de diálogo.
6. Hola **crear unidad organizativa** cuadro de diálogo, especifique un **nombre** para Hola nueva unidad organizativa. Proporcione una descripción breve de hello OU. También es posible establecer hello **administrado por** field para hello OU. toocreate Hola OU personalizada, haga clic en **Aceptar**.

    ![ADAC: cuadro de diálogo de creación de unidad organizativa](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. Hola que acaba de crear unidad organizativa debe aparecer ahora en hello centro de administración de AD (ADAC).

    ![ADAC: unidad organizativa creada](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a>Permisos/seguridad para unidades organizativas recién creadas
De forma predeterminada, usuario de hello (miembro del grupo de hello 'AAD DC administradores') que creó OU personalizada es contar con privilegios administrativos (control total) a través de Hola Hola OU. usuario de Hello, a continuación, puede seguir adelante y conceder a los usuarios de privilegios tooother o un grupo de 'Administradores de controlador de dominio de AAD' toohello según sea necesario. Tal como se muestra en la siguiente captura de pantalla de hello, Hola usuario 'bob@domainservicespreview.onmicrosoft.com' que creado hello 'MyCustomOU' unidades organizativas se le concede control total sobre él.

 ![ADAC: seguridad de nueva unidad organizativa](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a>Notas acerca de cómo administrar unidades organizativas personalizadas
Ahora que ha generado una unidad organizativa personalizada, puede seguir y crear en ella usuarios, grupos, equipos y cuentas de servicio. No se puede mover a los usuarios o grupos de hello 'AADDC usuarios' OU toocustom las unidades organizativas.

> [!WARNING]
> Las cuentas de usuario, los grupos, las cuentas de servicio y los objetos de equipo que se creen en unidades organizativas personalizadas no estarán disponibles en el inquilino de Azure AD. En otras palabras, estos objetos no se muestran utilizando la API de Azure AD Graph Hola u Hola UI de Azure AD. Solo estarán disponibles en el dominio administrado de Azure AD Domain Services.
>
>

## <a name="related-content"></a>Contenido relacionado
* [Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
* [Administración de directiva de grupo en un dominio administrado de Azure AD Domain Services](active-directory-ds-admin-guide-administer-group-policy.md)
* [Centro de administración de Active Directory: introducción](https://technet.microsoft.com/library/dd560651.aspx)
* [Guía paso a paso de las cuentas de servicio](https://technet.microsoft.com/library/dd548356.aspx)
