---
title: "las imágenes de aaaCreate y carga una VM FreeBSD | Documentos de Microsoft"
description: "Obtenga información acerca de toocreate y cargar un disco duro virtual (VHD) que contiene toocreate de sistema operativo de hello FreeBSD máquinas virtuales de Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a>Crear y cargar un tooAzure FreeBSD VHD
Este artículo muestra cómo toocreate y cargar un disco duro virtual (VHD) que contiene Hola sistema de operativo FreeBSD. Después de cargarlo, puede usarlo como su propia toocreate imagen una máquina virtual (VM) en Azure.

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para obtener información sobre cómo cargar un VHD con el modelo del Administrador de recursos de hello, consulte [aquí](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Requisitos previos
Este artículo se supone que dispone de hello siguientes elementos:

* **Una suscripción de Azure**: si no tiene una cuenta, puede crear una en un par de minutos. Si tiene una suscripción a MSDN, consulte [Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). De lo contrario, obtenga información acerca de cómo demasiado[crear una cuenta de prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).  
* **Herramientas de Azure PowerShell**: módulo de Azure PowerShell Hola debe estar instalado y configurado toouse su suscripción de Azure. módulo de hello toodownload, consulte [descargas de Azure](https://azure.microsoft.com/downloads/). Un tutorial que describe cómo tooinstall y configurar el módulo de hello está disponible aquí. Hola de uso [descargas de Azure](https://azure.microsoft.com/downloads/) Hola de cmdlet tooupload disco duro virtual.
* **Sistema de operativo FreeBSD instalado en un archivo .vhd**--un sistema de operativo FreeBSD compatible debe ser tooa disco duro instalado. Varias herramientas existen archivos .vhd de toocreate. Por ejemplo, puede usar una solución de virtualización como archivo .vhd de Hyper-V toocreate Hola e instalar sistema operativo de Hola. Para obtener instrucciones sobre cómo tooinstall y usar Hyper-V, vea [instalar Hyper-V y crear una máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> no se admite el formato VHDX más reciente de Hello en Azure. Puede convertir el formato de tooVHD de disco de hello mediante el Administrador de Hyper-V u Hola cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx). Además, hay un [tutorial de MSDN acerca de cómo toouse FreeBSD con Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).
>
>

Esta tarea incluye Hola siguiendo cinco pasos:

## <a name="step-1-prepare-hello-image-for-upload"></a>Paso 1: Preparar la imagen de hello para la carga
En máquina virtual de Hola donde instaló el sistema operativo de hello FreeBSD, complete Hola procedimientos siguientes:

1. Habilite DHCP.

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. Habilite SSH.

    Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema. De forma predeterminada, se habilita después de la instalación desde el disco FreeBSD. 
3. Configure la consola de serie.

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. Instale sudo.

    cuenta de Hello raíz está deshabilitada en Azure. Esto significa que necesita tooutilize sudo desde un comandos toorun de usuario sin privilegios con privilegios elevados.

        # pkg install sudo
   
5. Requisitos previos del agente de Azure.

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. Instale el agente de Azure.

    Hello versión más reciente de hello agente de Azure siempre se encuentra en [github](https://github.com/Azure/WALinuxAgent/releases). Hola versión 2.0.10 + admita oficialmente FreeBSD 10 & 10.1 y esta versión de Hola 2.1.4 + (incluidos 2.2) admite oficialmente 10.2 FreeBSD y versiones posteriores.

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    Para 2.0, usaremos la 2.0.16 como ejemplo:

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    Para 2.1, utilizaremos la 2.1.4 como ejemplo:

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > Después de instalar al agente de Azure, es un tooverify buena idea que se está ejecutando:
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. Desaprovisionar sistema Hola.

    Desaprovisionamiento Hola tooclean del sistema y asegúrese de que adecuado para reaprovisionamiento. Hello siguiente comando también elimina última cuenta de usuario aprovisionado Hola y Hola asociado datos:

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    Ahora ya puede apagar la máquina virtual.

## <a name="step-2-create-a-storage-account-in-azure"></a>Paso 2: Creación de una cuenta de almacenamiento en Azure
Se necesita una cuenta de almacenamiento en un archivo .vhd de Azure tooupload por lo que puede ser usado toocreate una máquina virtual. Puede usar hello toocreate portal clásico una cuenta de almacenamiento de Azure.

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. En la barra de comandos de hello, seleccione **nuevo**.
3. Seleccione **Data Services** > **Storage** > **Creación rápida**.

    ![Crear rápidamente una cuenta de almacenamiento](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. Rellene los campos de hello como sigue:

   * Hola **dirección URL** , escriba un toouse de nombre de subdominio en hello URL de la cuenta de almacenamiento. entrada de Hello puede contener entre 3 y 24 números y letras en minúscula. Este nombre se convierte en el nombre de host de hello dentro de dirección URL de hello tooaddress usa almacenamiento de blobs de Azure, almacenamiento en la cola de Azure o recursos de almacenamiento de tabla de Azure para la suscripción de Hola.
   * Hola **ubicación/grupo de afinidad** menú desplegable, elija hello **ubicación o grupo de afinidad** Hola cuenta de almacenamiento. Un grupo de afinidad le permite colocar los servicios en la nube y el almacenamiento en hello mismo centro de datos.
   * Hola **replicación** , a continuación, decidir si toouse **con redundancia geográfica** replicación Hola cuenta de almacenamiento. La replicación geográfica está activada de forma predeterminada. Esta opción replica la tooa secundaria ubicación de datos, en ningún tooyou de costo, para que el almacenamiento se conmuta toothat ubicación si un error grave, se produce en la ubicación principal Hola. ubicación secundaria Hola se asigna automáticamente y no se puede cambiar. Si necesita más control sobre la ubicación de Hola de su almacenamiento en la nube debido a los requisitos de toolegal o directiva organizativa, puede desactivar la replicación geográfica. Sin embargo, tenga presente que si más adelante activar la replicación geográfica, se le cobrará una sola vez tooreplicate de cuota de transferencia de datos la ubicación secundaria de toohello de datos existente. Los servicios de almacenamiento sin replicación geográfica se ofrecen con descuento. Puede encontrar más información sobre la administración de la replicación geográfica de cuentas de almacenamiento aquí: [Replicación de Azure Storage](../../../storage/common/storage-redundancy.md).

     ![Escribir los detalles de la cuenta de almacenamiento](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. Haga clic en **Crear cuenta de almacenamiento**. Hello cuenta aparece ahora en **almacenamiento**.

    ![Cuenta de almacenamiento creada correctamente](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. Después, cree un contenedor para los archivos .vhd que ha cargado. Seleccione el nombre de cuenta de almacenamiento de hello y, a continuación, seleccione **contenedores**.

    ![Detalles de la cuenta de almacenamiento](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. Seleccione **Crear un contenedor**.

    ![Detalles de la cuenta de almacenamiento](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. Hola **nombre** , escriba un nombre para el contenedor. A continuación, en hello **acceso** menú de lista desplegable, seleccione el tipo de directiva de acceso que desee.

    ![Nombre del contenedor](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > De forma predeterminada, el contenedor de hello es privado y sólo pueden obtener acceso el propietario de la cuenta de hello. tooallow acceso de lectura público toohello blobs en el contenedor de hello, pero no las propiedades de contenedor toohello y metadatos, utilice hello **Blob público** opción. acceso de lectura público completo tooallow hello contenedor y blobs, use hello **contenedor público** opción.
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a>Paso 3: Preparar Hola conexión tooAzure
Antes de poder cargar un archivo .vhd, debe tooestablish una conexión segura entre el equipo y su suscripción de Azure. Puede usar el método de hello Azure Active Directory (Azure AD) u Hola certificado método toodo.

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a>Usar tooupload de método hello Azure AD un archivo .vhd
1. Consola de Azure PowerShell Hola abierto.
2. Escriba el siguiente comando de hello:  
    `Add-AzureAccount`

    Este comando abre una ventana de inicio de sesión donde podrá iniciar sesión con su cuenta profesional o educativa.

    ![Ventana de PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. Azure se autentica y guarda la información de credenciales de Hola. A continuación, cierra la ventana hello.

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a>Usar tooupload de método hello certificado un archivo .vhd
1. Consola de Azure PowerShell Hola abierto.
2. Escriba: `Get-AzurePublishSettingsFile`.
3. Una ventana del explorador se abre y se le pide toodownload Hola archivo .publishsettings. Este archivo contiene información y un certificado para su suscripción de Azure.

    ![Página de descarga del explorador](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. Guarde el archivo .publishsettings de Hola.
5. Tipo: `Import-AzurePublishSettingsFile <PathToFile>`, donde `<PathToFile>` es el archivo .publishsettings de hello ruta de acceso completa toohello.

   Para obtener información, consulte [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx)(Introducción a los cmdlets de Azure).

   Para obtener más información sobre la instalación y configuración de PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

## <a name="step-4-upload-hello-vhd-file"></a>Paso 4: Cargar archivo .vhd de hello
Cuando se carga el archivo .vhd de hello, puede colocarlo en cualquier lugar dentro de su almacenamiento de blobs. Estos son algunos de los términos que se utilizará al cargar el archivo hello:

* **BlobStorageURL** es la dirección URL de Hola Hola cuenta de almacenamiento que creó en el paso 2.
* **YourImagesFolder** esté contenedor Hola dentro del almacenamiento de blobs donde desee toostore las imágenes.
* **VHDName** es Hola etiqueta que aparece en el disco de duro virtual de hello Azure tooidentify portal clásico Hola.
* **PathToVHDFile** es la ruta de acceso completa de Hola y el nombre de archivo .vhd de Hola.

Desde la ventana de PowerShell de Azure de hello utilizada en el paso anterior de hello, escriba:

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a>Paso 5: Crear una máquina virtual con archivo .vhd cargado de hello
Después de cargar el archivo .vhd de hello, puede agregarlo como una lista de toohello de imagen de imágenes personalizadas que están asociados a su suscripción y crear una máquina virtual con esta imagen personalizada.

1. Desde la ventana de PowerShell de Azure de hello utilizada en el paso anterior de hello, escriba:

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > Usar Linux como tipo de sistema operativo de Hola. versión actual de PowerShell de Azure de Hello acepta solo "Linux" o "Windows" como un parámetro.
   >
   >
2. Después de completar los pasos anteriores de hello, nueva imagen de hello aparece cuando se elige hello **imágenes** ficha en hello portal de Azure clásico.  

    ![Elija una imagen](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. Crear una máquina virtual desde la Galería de Hola. Esta nueva imagen ahora está disponible en **Mis imágenes**.
4. Seleccione la nueva imagen de Hola. A continuación, vaya a través de hello solicita tooset un nombre de host, contraseña, clave SSH, y así sucesivamente.

    ![Imagen personalizada](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. Después de completar el aprovisionamiento de hello, verá la VM de FreeBSD ejecuta en Azure.

    ![Imagen de FreeBSD en Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
