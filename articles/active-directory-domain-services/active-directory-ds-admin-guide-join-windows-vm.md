---
title: 'Azure Active Directory Domain Services: Unirse a un dominio administrado de VM de Windows Server tooa | Documentos de Microsoft'
description: "Unir una máquina virtual de Windows Server tooAzure AD los servicios de dominio"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>Unirse a un dominio administrado de Windows Server máquina virtual tooa
> [!div class="op_single_selector"]
> * [Portal de Azure clásico - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

Este artículo muestra cómo toojoin un tooan de Windows Server 2012 R2 ejecutando los servicios de dominio de Azure AD de máquina virtual administra el dominio, con hello portal de Azure clásico.

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>Paso 1: Crear la máquina virtual de Windows Server de Hola
Siga las instrucciones de hello descritas en hello [crear una máquina virtual que ejecuta Windows en el portal de Azure clásico hello](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) tutorial. Es importante tooensure que esta máquina virtual recién creada es unido toohello misma red virtual en el que habilita los servicios de dominio de AD de Azure. Hola "Creación rápida" opción no habilita toojoin hello tooa virtual red de máquina virtual. Por lo tanto, debe toouse hello 'De la Galería' opción toocreate Hola virtual machine.

Realizar Hola siguientes pasos toocreate una máquina virtual toohello unido a red virtual de Windows en el que se han habilitado Servicios de dominio de AD de Azure.

1. Hola portal de Azure clásico, en barra de comandos de hello en parte inferior de Hola de ventana hello, haga clic en **nuevo**.
2. En **Compute**, haga clic en **Máquina virtual** y, luego, en **De la galería**.
3. Hola primera pantalla le permite **elegir una imagen** para la máquina virtual desde la lista de Hola de imágenes disponibles. Seleccionar imagen apropiada de Hola.

    ![Seleccionar imagen](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. pantalla de bienvenida segundo le permite elegir un nombre de equipo, el tamaño y el nombre de usuario y la contraseña. Usar capa de Hola y tamaño necesario toorun su aplicación o la carga de trabajo. nombre de usuario de Hola que elija aquí es un usuario de administrador local en el equipo de Hola. No escriba las credenciales de la cuenta de usuario del dominio aquí.

    ![Configurar máquina virtual](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. pantalla de bienvenida tercer le permite configurar los recursos de redes, almacenamiento y disponibilidad. Asegúrese de seleccionar Hola red virtual en el que habilita los servicios de dominio de AD de Azure de hello **afinidad región/grupo/red Virtual** lista desplegable. Especifique un **nombre de DNS del servicio de nube** según corresponda para la máquina virtual de Hola.

    ![Seleccionar una red virtual para una máquina virtual](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Asegúrese de que se une toohello de máquina virtual de hello misma red virtual en el que se han habilitado Servicios de dominio de AD de Azure. Como resultado, máquina virtual de hello puede "ver" dominio de Hola y realizar tareas como unirse a dominio Hola. Si elige máquina virtual de toocreate hello en otra red virtual, conectar esa red virtual de toohello de red virtual en el que se han habilitado Servicios de dominio de AD de Azure.
   >
   >
6. pantalla de bienvenida cuarto permite instalar Hola agente de máquina virtual y configurar algunas de las extensiones disponibles de Hola.

    ![¡Listo!](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Después de crear la máquina virtual de hello, portal clásico de hello muestra hello nueva máquina virtual en hello **máquinas virtuales** nodo. Máquina virtual de Hola y servicio de nube se inician automáticamente y su estado aparece como **ejecutando**.

    ![La máquina virtual está activa y se está ejecutando](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>Paso 2: Conectar la máquina de virtual de Windows Server toohello con cuenta de administrador local de Hola
Ahora, nos conectamos toohello recién creado Windows máquina virtual del servidor toojoin se toohello dominio. Usar credenciales de administrador local de Hola que especificó al crear la máquina virtual de hello, tooconnect tooit.

Realizar Hola siguiendo los pasos tooconnect toohello virtual machine.

1. Navegue demasiado**máquinas virtuales** nodo en el portal clásico de Hola. Seleccione la máquina virtual de Hola que creó en el paso 1 y haga clic en **conectar** de barra de comandos de hello en parte inferior de Hola de ventana hello.

    ![Conectar máquina virtual de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portal clásico de Hello le pedirá que tooopen o guardar un archivo con la extensión '.rdp', que es usado tooconnect toohello máquina. Cuando haya acabado la descarga, haga clic en archivo de hello tooopen.
3. En el símbolo del sistema de inicio de sesión hello, escriba su **credenciales de administrador local**, que especificó al crear la máquina virtual de Hola. Por ejemplo, hemos utilizado localhost\mahesh en este ejemplo.

En este momento, deben registrar en toohello recién creado la máquina virtual de Windows con credenciales de administrador locales. Hola siguiente paso es el dominio de toohello de la máquina virtual de toojoin Hola.

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>Paso 3: Unirse a dominio administrado del toohello AAD DS de máquina virtual de hello Windows Server
Realizar Hola siguiendo los pasos toojoin Hola Windows Server máquina virtual toohello AAD DS dominio administrado.

1. Conecte toohello Windows Server como se muestra en el paso 2. Desde la pantalla de inicio de bienvenida, abra **el administrador del servidor**.
2. Haga clic en **servidor Local** en panel izquierdo de saludo de la ventana del administrador del servidor de Hola.

    ![Inicio del Administrador del servidor en la máquina virtual](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Haga clic en **WORKGROUP** en hello **propiedades** sección. Hola **propiedades del sistema** página de propiedades, haga clic en **cambio** dominio de hello toojoin.

    ![Página Propiedades del sistema](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Especifique el nombre de dominio de Hola de su dominio administrado de los servicios de dominio de AD de Azure en hello **dominio** cuadro de texto y haga clic en **Aceptar**.

    ![Especificar Hola dominio toobe unido](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. Se está tooenter solicitada en su dominio de Hola de toojoin de credenciales. Asegúrese de que **especificar credenciales de Hola para un toohello de usuario que pertenecen los administradores de controlador de dominio de AAD** grupo. Solo los miembros de este grupo tienen privilegios toojoin máquinas toohello administrado dominio.

    ![Especificar las credenciales para unirse al dominio](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. Puede especificar las credenciales de cualquiera de hello siguientes maneras:

   * Formato de UPN: especifique el sufijo UPN de hello para la cuenta de usuario de hello, como está configurado en Azure AD. En este ejemplo, el sufijo UPN de saludo del usuario de hello 'bob' es 'bob@domainservicespreview.onmicrosoft.com'.
   * Formato de SAMAccountName: puede especificar el nombre de la cuenta de hello en formato de SAMAccountName Hola. En este ejemplo, el usuario de hello 'bob' necesitaría tooenter 'CONTOSO100\bob'.

     > [!NOTE]
     > **Se recomienda utilizar las credenciales de hello UPN formato toospecify.** Hola SAMAccountName puede generarse automáticamente si el prefijo del UPN del usuario es demasiado larga (por ejemplo, 'joereallylongnameuser'). Si varios usuarios tengan Hola mismo prefijo UPN (por ejemplo, "bob") en su inquilino de Azure AD, su formato SAMAccountName puede ser generado automáticamente por servicio Hola. En estos casos, formato UPN de hello puede utilizarse de forma confiable toolog toohello dominio.
     >
     >
7. Después de unirse a un dominio es correcta, verá Hola sigue mensaje le dará la bienvenida toohello dominio. Reiniciar la máquina de virtual de Hola para toocomplete de operación de unión de dominio Hola.

    ![Dominio de bienvenida toohello](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Solución de problemas de unión al dominio
### <a name="connectivity-issues"></a>Problemas de conectividad
Si máquina virtual de hello es dominio de hello toofind no se puede, consulte toohello siguiendo los pasos de solución de problemas:

* Asegúrese de que la máquina virtual hello es toohello conectado misma red virtual que ha habilitado en los servicios de dominio. Si no es así, hello y la máquina virtual no se puede tooconnect toohello dominio por lo tanto es dominio de hello toojoin no se puede.
* Si máquina virtual de hello es red virtual tooanother conectado, asegúrese de que esta red virtual está conectado toohello red virtual en el que se han habilitado los servicios de dominio.
* Pruebe a dominio de hello tooping utilizando Hola de nombre de dominio del dominio administrado de hello (por ejemplo, ' ping contoso100.com'). Si no se puede toodo por lo tanto, intente tooping direcciones IP de Hola para dominio hello muestra en la página de Hola donde haya habilitado los servicios de dominio de AD de Azure (por ejemplo, ' ping 10.0.0.4'). Si es la dirección IP de tooping capaz de hello pero no el dominio de hello, DNS puede configurarse incorrectamente. Puede no tienen Hola direcciones IP configuradas del dominio de hello como servidores DNS para la red virtual de Hola.
* Intente vaciar Hola caché de resolución DNS en la máquina virtual de hello ('ipconfig /flushdns').

Si obtiene toohello cuadro de diálogo que pide al dominio de hello toojoin de credenciales, no tiene problemas de conectividad.

### <a name="credentials-related-issues"></a>Problemas relacionados con las credenciales
Consulte toohello siguientes pasos si tiene problemas con las credenciales y están toojoin no se puede Hola dominio.

* Pruebe a usar las credenciales de hello UPN formato toospecify. Hola SAMAccountName para su cuenta puede ser autogenerada si hay varios usuarios con hello UPN mismo prefijo en el inquilino o si el prefijo del UPN es demasiado largo. Por lo tanto, el formato de SAMAccountName de Hola para su cuenta puede ser diferente de lo que espera o usar en el dominio local.
* Ensaye con credenciales de hello toouse de una cuenta de usuario que pertenece toohello 'AAD DC administradores' grupo toojoin máquinas toohello dominio administrado.
* Asegúrese de que tiene [habilitada la sincronización de contraseña](active-directory-ds-getting-started-password-sync.md) con arreglo a los pasos de Hola que se describen en la Guía de introducción de Hola.
* Asegúrese de que usa Hola UPN del usuario de hello como está configurado en Azure AD (por ejemplo, 'bob@domainservicespreview.onmicrosoft.com') toosign en.
* Asegúrese de que han esperado durante el tiempo suficiente para toocomplete de sincronización de contraseña como se especifica en la Guía de introducción de Hola.

## <a name="related-content"></a>Contenido relacionado
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
