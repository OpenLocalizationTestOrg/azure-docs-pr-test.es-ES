---
title: 'Azure Active Directory Domain Services: Unirse a un dominio administrado de RHEL VM tooa | Documentos de Microsoft'
description: "Unir una máquina virtual de Red Hat Enterprise Linux tooAzure AD los servicios de dominio"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a>Unirse a un dominio administrado de Red Hat Enterprise Linux 7 máquina virtual tooa
Este artículo muestra cómo toojoin una tooan de máquina virtual de Red Hat Enterprise Linux (RHEL) 7 Servicios de dominio de Azure AD administra el dominio.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Aprovisionamiento de una máquina virtual de Red Hat Enterprise Linux
Realizar Hola después de la máquina virtual pasos tooprovision un RHEL 7 a través de hello portal de Azure.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

    ![Panel de Portal de Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Haga clic en **New** en hello dejado panel y escriba **Red Hat** en la barra de búsqueda de hello tal y como se muestra en la siguiente captura de pantalla de Hola. Las entradas para Red Hat Enterprise Linux aparezcan en resultados de la búsqueda de Hola. Haga clic en **Red Hat Enterprise Linux 7.2**.

    ![Seleccionar RHEL en resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. resultados de búsqueda de Hello en hello **todo** panel debe enumerar imagen Hola Red Hat Enterprise Linux 7.2. Haga clic en **Red Hat Enterprise Linux 7.2** tooview obtener más información acerca de la imagen de máquina virtual de Hola.

    ![Seleccionar RHEL en resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. Hola **Red Hat Enterprise Linux 7.2** panel, debería ver más información acerca de la imagen de máquina virtual de Hola. Hola **seleccionar un modelo de implementación** lista desplegable, seleccione **clásico**. A continuación, haga clic en hello **crear** botón.

    ![Ver detalles de la imagen](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. Hola **conceptos básicos de** página de hello **crear máquina virtual** asistente, escriba Hola **nombre de Host** para la máquina virtual nueva de Hola. Especificar un nombre de usuario de administrador local en hello **nombre de usuario** campo y un **contraseña**. También puede elegir toouse un usuario de administrador local de Hola de tooauthenticate clave SSH. Seleccionar una **tarifa** para la máquina virtual de Hola.

    ![Crear máquina virtual: página de aspectos básicos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. Hola **tamaño** página de hello **crear máquina virtual** tamaño Hola asistente, seleccione para la máquina virtual de Hola.

    ![Crear máquina virtual: seleccionar tamaño](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. Hola **configuración** página de hello **crear máquina virtual** cuenta de almacenamiento de saludo del asistente, seleccione para la máquina virtual de Hola. Haga clic en **red Virtual** tooselect Hola Hola de toowhich de red virtual se deben implementar la VM de Linux. Hola **red Virtual** hoja, red virtual seleccione hello en el que los servicios de dominio de Azure AD está disponible. En este ejemplo, hemos elegido red virtual de hello 'MyPreviewVNet'.

    ![Crear máquina virtual: seleccionar la red virtual](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. En hello **resumen** página de hello **crear máquina virtual** Hola asistente, revise y haga clic en **Aceptar** botón.

    ![Crear máquina virtual: red virtual seleccionada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. Debe iniciar la implementación de hello nueva máquina virtual basada en imagen de hello RHEL 7.2.

    ![Crear máquina virtual: implementación iniciada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Después de unos minutos, máquina virtual de hello debe ser implementada correctamente y está listo para su uso.

    ![Crear máquina virtual: implementado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a>Conectar la máquina virtual de Linux toohello recién aprovisionado de forma remota
máquina virtual de Hello RHEL 7.2 se haya aprovisionado en Azure. Hola siguiente tarea es tooconnect de forma remota máquinas virtuales de toohello.

**Conectar máquina virtual de toohello RHEL 7.2** siga las instrucciones de hello en el artículo hello [cómo toolog en la máquina virtual de tooa ejecutan Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

resto de Hola de pasos de hello supongamos que se usa Hola PuTTY SSH cliente tooconnect toohello RHEL máquina virtual. Para obtener más información, vea hello [página de descargas de PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Abra Hola PuTTY programa.
2. Escriba hello **nombre de Host** para hello recién creado la máquina virtual RHEL. En este ejemplo, de la máquina virtual tiene el nombre de host de hello 'contoso rhel.cloudapp .net'. Si no está seguro del nombre de host de saludo de la máquina virtual, consulte toohello panel de máquinas virtuales en hello portal de Azure.

    ![Conexión a PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Inicie sesión en la máquina virtual de toohello con credenciales de administrador local de Hola que especificó cuando creó la máquina virtual de Hola. En este ejemplo, se utiliza la cuenta de administrador local de Hola "mahesh".

    ![Inicio de sesión de PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a>Instalar los paquetes necesarios en la máquina virtual de Linux de Hola
Después de la máquina virtual en conexión toohello Hola siguiente tarea es paquetes tooinstall necesarios para unirse a un dominio en la máquina virtual de Hola. Lleve a cabo Hola pasos:

1. **Instalar realmd:** paquete de hello realmd se usa para unirse a un dominio. En el terminal PuTTY, escriba Hola siguiente comando:

    sudo yum install realmd

    ![Instalar realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Después de unos minutos, paquete de hello realmd debe se instala en la máquina virtual de Hola.

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Instalar sssd:** hello realmd paquete dependiente sssd tooperform las operaciones de combinación de dominio. En el terminal PuTTY, escriba Hola siguiente comando:

    sudo yum install sssd

    ![Instalar sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Después de unos minutos, paquete de hello sssd debe se instala en la máquina virtual de Hola.

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Instalar kerberos:** de su terminal PuTTY, escriba Hola siguiente comando:

    sudo yum install krb5-workstation krb5-libs

    ![Instalar kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Después de unos minutos, paquete de hello realmd debe se instala en la máquina virtual de Hola.

    ![Kerberos instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a>Unirse a dominio administrado del toohello de máquina virtual Linux Hola
Ahora que los paquetes de saludo necesario están instalados en la máquina virtual de Linux de hello, Hola siguiente tarea es dominio administrado del toohello toojoin Hola máquina virtual.

1. Detectar el dominio administrado de los servicios de dominio de AAD Hola. En el terminal PuTTY, escriba Hola siguiente comando:

    sudo realm discover CONTOSO100.COM

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Si **territorio detectar** es no se puede toofind el dominio administrado, asegúrese de ese dominio hello es accesible desde la máquina virtual de hello (try ping). Asegúrese también de que la máquina virtual Hola realmente ha sido implementado toohello misma red virtual en qué Hola dominio administrado está disponible.
2. Inicialice kerberos. En el terminal PuTTY, escriba Hola siguiente comando. Asegúrese de especificar un usuario que pertenece el grupo toohello 'AAD DC administradores'. Solo estos usuarios pueden unirse a dominio administrado de equipos toohello.

    kinit bob@CONTOSO100.COM

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Asegurarse de que se especifique el nombre de dominio de hello en letras mayúsculas, kinit else se produce un error.
3. Unirse a dominio de hello máquina toohello. En el terminal PuTTY, escriba Hola siguiente comando. Especificar Hola mismo usuario que especificó en hello anterior paso ('kinit').

    sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'

    ![Unión a dominio kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

Debe obtener un mensaje ("se inscribió correctamente máquina en el dominio Kerberos") cuando la máquina de hello es dominio administrado toohello se unió correctamente.

## <a name="verify-domain-join"></a>Verificación de la unión a un dominio
Para comprobar rápidamente si máquina Hola ha sido el dominio administrado toohello se unió correctamente. Conectar toohello recién Unidos a un dominio RHEL VM con SSH y una cuenta de usuario de dominio y, a continuación, toosee de comprobación si la cuenta de usuario de Hola se resuelve correctamente.

1. En el terminal, PuTTY Hola de tipo siguientes comando tooconnect toohello recién Unidos RHEL virtual máquina mediante SSH a un dominio. Usar una cuenta de dominio que pertenece el dominio administrado toohello (por ejemplo, 'bob@CONTOSO100.COM' en este caso.)

    ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net
2. En el terminal PuTTY, escriba Hola después toosee comando si el directorio particular de Hola se inicializó correctamente.

    pwd
3. En el terminal PuTTY, escriba Hola después toosee comando si se están resolviendo las pertenencias a grupos de hello correctamente.

    id

Este es un ejemplo de los resultados de estos comandos:

![Verificación de la unión a un dominio](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Solución de problemas de unión al dominio
Consulte toohello [unión al dominio de solución de problemas](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artículo.

## <a name="related-content"></a>Contenido relacionado
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Unirse a un dominio administrado de Windows Server máquina virtual tooan servicios de dominio de AD de Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [¿Cómo toolog en la máquina virtual de tooa ejecutan Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Installing Kerberos (Instalación de Kerberos)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 - Windows Integration Guide (Red Hat Enterprise Linux 7: guía de integración de Windows)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
