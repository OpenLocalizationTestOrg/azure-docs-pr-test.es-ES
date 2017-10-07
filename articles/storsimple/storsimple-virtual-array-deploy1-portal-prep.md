---
title: aaaPortal prep para StorSimple Virtual Array | Documentos de Microsoft
description: Toodeploy tutorial primera matriz virtual de StorSimple implica preparar Hola portal de Azure
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>Implementar StorSimple Virtual Array: preparar Hola portal de Azure

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>Información general

Se trata de hello primer artículo de hello serie de tutoriales de implementación necesario toocompletely implementar la matriz virtual como un servidor de archivos o un servidor de iSCSI mediante el modelo de administrador de recursos de Hola. Este artículo describe toocreate de preparación necesarios de Hola y configurar el servicio de administrador de dispositivos de StorSimple anteriores tooprovisioning una matriz virtual. En este artículo también incluye vínculos a tooa configuración configuración y lista de comprobación de requisitos previos de implementación.

Necesita privilegios toocomplete Hola el programa de instalación y configuración de proceso del administrador. Se recomienda que revise la lista de comprobación de configuración de implementación de hello antes de empezar. preparación de portal de Hello tarda menos de 10 minutos.

información de Hello publicada en este artículo aplica toohello implementación de StorSimple arreglos de discos virtuales en hello portal de Azure y la nube de Microsoft Azure Government.

### <a name="get-started"></a>Primeros pasos
flujo de trabajo de implementación de Hello consta de preparar portal hello, el aprovisionamiento de una matriz virtual en su entorno virtualizado y completar la instalación de Hola. tooget a trabajar con la implementación de StorSimple Virtual Array Hola como un servidor de archivos o un servidor de iSCSI, debe toohello toorefer tabulados recursos siguientes.

#### <a name="deployment-articles"></a>Artículos de implementación

toodeploy la matriz Virtual de StorSimple, consulte toohello siguientes artículos en hello lo prescrito, secuencia.

| **#** | **En este paso** | **Se hace lo siguiente…** | **Y use estos documentos.** |
| --- | --- | --- | --- |
| 1. |**Configurar Hola portal de Azure** |Crear y configurar el servicio de administrador de dispositivos de StorSimple anteriores tooprovisioning una matriz Virtual de StorSimple. |[Prepare portal Hola](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**Aprovisionar Hola Virtual Array** |Para Hyper-V, aprovisionar y conectar tooa StorSimple Virtual Array en un sistema de host que ejecuta Hyper-V en Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2. <br></br> <br></br> Para VMware, aprovisionar y conectar tooa StorSimple Virtual Array en un sistema host ejecutando VMware ESXi 5.5 y versiones posteriores.<br></br> |[Deploy StorSimple Virtual Array - Provision a Virtual Array in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) (Implementación de StorSimple Virtual Array: aprovisionamiento de una matriz virtual en Hyper-V) <br></br> <br></br> [Deploy StorSimple Virtual Array - Provision a Virtual Array in VMware](storsimple-virtual-array-deploy2-provision-vmware.md) (Implementación de StorSimple Virtual Array: aprovisionamiento de una matriz virtual en VMware) |
| 3. |**Configurar Hola Virtual Array** |Para el servidor de archivos, realizar la instalación inicial, registrar el servidor de archivos de StorSimple y completar el programa de instalación de dispositivo de Hola. A continuación, puede aprovisionar los recursos compartidos de SMB. <br></br> <br></br> Para el servidor de iSCSI, realizar la instalación inicial, registrar el servidor de iSCSI de StorSimple y completar el programa de instalación de dispositivo de Hola. A continuación, puede aprovisionar los volúmenes iSCSI. |[Deploy StorSimple Virtual Array - Set up as file server](storsimple-virtual-array-deploy3-fs-setup.md) (Implementación de StorSimple Virtual Array: configurar como servidor de archivos)<br></br> <br></br>[Implementar una matriz virtual de StorSimple: Configurar el dispositivo virtual como servidor iSCSI (versión preliminar)](storsimple-virtual-array-deploy3-iscsi-setup.md) |

Ahora puede empezar a tooset seguridad Hola portal de Azure.

## <a name="configuration-checklist"></a>Lista de comprobación de la configuración

lista de comprobación de configuración de Hello describe información de hello necesita toocollect antes de configurar el software de hello en la matriz Virtual de StorSimple. Preparar esta información antes de tiempo le ayuda a agilizar Hola proceso de implementación de dispositivo de StorSimple de hello en su entorno. Dependiendo de si la matriz Virtual de StorSimple se implementa como un servidor de archivos o un servidor de iSCSI, se deberán cumplir alguno de hello siguiendo las listas de comprobación.

* Descargar hello [StorSimple Virtual Array archivo Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).
* Descargar hello [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).

## <a name="prerequisites"></a>Requisitos previos

Aquí encontrará los requisitos previos de configuración de Hola de su servicio de administrador de dispositivos de StorSimple, StorSimple Virtual Array y red de centro de datos de Hola.

### <a name="for-hello-storsimple-device-manager-service"></a>Para hello servicio Administrador de dispositivos de StorSimple

Antes de comenzar, asegúrese de que:

* Tiene una cuenta Microsoft con credenciales de acceso.
* Tiene una cuenta de almacenamiento de Microsoft Azure con credenciales de acceso.
* Su suscripción a Microsoft Azure debe estar habilitada para el servicio StorSimple Device Manager.

### <a name="for-hello-storsimple-virtual-array"></a>Para hello StorSimple Virtual Array

Antes de implementar una matriz virtual, asegúrese de que:

* Tiene acceso tooa host sistema que ejecuta Hyper-V en Windows Server 2008 R2 o posterior o VMware (ESXi 5.5 o posterior) que puede ser utilizado tooa Aprovisione un dispositivo.
* sistema de host de Hello es capaz de toodedicate Hola siguientes tooprovision de recursos de la matriz virtual:
  
  * Un mínimo de 4 núcleos.
  * Al menos 8 GB de RAM. Si tiene previsto matriz virtual de hello tooconfigure como servidor de archivos, 8 GB admite 2 millones de archivos. Necesita 16 GB de RAM toosupport 2-4 millones de archivos.
  * Una interfaz de red.
  * Un disco virtual de 500 GB para datos del sistema.

### <a name="for-hello-datacenter-network"></a>Para la red de centro de datos de Hola

Antes de comenzar, asegúrese de que:

* red de Hello en el centro de datos está configurada según los requisitos de red de hello para el dispositivo StorSimple. Para obtener más información, vea hello [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).
* StorSimple Virtual Array tiene un ancho de banda de Internet de 5 Mbps (o más) disponible en todo momento. Este ancho de banda no debe compartirse con otras aplicaciones.

## <a name="step-by-step-preparation"></a>Preparación de paso a paso

Usar el portal de hello siguiendo las instrucciones paso a paso tooprepare para hello servicio Administrador de dispositivos de StorSimple.

## <a name="step-1-create-a-new-service"></a>Paso 1: Crear un nuevo servicio

Una sola instancia del servicio de administrador de dispositivos de StorSimple de hello puede administrar varios arreglos de discos virtuales de StorSimple. Realizar Hola siguiendo los pasos toocreate una instancia de servicio de administrador de dispositivos de StorSimple Hola. Si tienes un toomanage de servicio de administrador de dispositivos de StorSimple existente sus arreglos de discos virtuales, omita este paso y vaya demasiado[paso 2: clave de registro del servicio de Get hello](#step-2-get-the-service-registration-key).

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> Si no ha habilitado la creación automática de Hola de una cuenta de almacenamiento con el servicio, deberá toocreate al menos una cuenta de almacenamiento después de haber creado correctamente un servicio.
> 
> * Si no ha creado una cuenta de almacenamiento automáticamente, vaya demasiado[configurar una nueva cuenta de almacenamiento para el servicio de hello](#optional-step-configure-a-new-storage-account-for-the-service) para obtener instrucciones detalladas.
> * Si ha habilitado la creación automática de Hola de una cuenta de almacenamiento, vaya demasiado[paso 2: clave de registro del servicio de Get hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Paso 2: Obtener la clave de registro del servicio de Hola

Después de hello servicio Administrador de dispositivos de StorSimple está en funcionamiento, deberá clave de registro del servicio de tooget Hola. Esta clave es tooregister usado y conecte el dispositivo StorSimple con el servicio de Hola.

Realizar Hola siguiendo los pasos de hello [portal de Azure](https://portal.azure.com/).

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> clave de registro del servicio Hello es tooregister usado todos los dispositivos de StorSimple el Administrador de dispositivos que necesitan tooregister con el servicio de administrador de dispositivos de StorSimple de Hola.
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>Paso 3: Descargar la imagen de la matriz virtual de Hola

Una vez que la clave de registro del servicio de hello, deberá toodownload Hola matriz virtual correspondiente imagen tooprovision una matriz virtual en el sistema host. imágenes de la matriz virtual de Hello son específicas del sistema operativo y pueden descargarse desde la página de inicio rápido de Hola Hola portal de Azure.

> [!IMPORTANT]
> software de Hola que se ejecuta en hello StorSimple Virtual Array solo puede usarse con hello servicio Administrador de dispositivos de StorSimple.
> 
> 

Realizar Hola siguiendo los pasos de hello [portal de Azure](https://portal.azure.com/).

#### <a name="tooget-hello-virtual-array-image"></a>imagen de la matriz virtual de hello tooget

1. Inicio de sesión en hello [portal de Azure](https://portal.azure.com/). 
2. Hola portal de Azure, haga clic en **examinar > administradores de dispositivos de StorSimple**.
3. Para un servicio StorSimple Device Manager existente. Hola **el Administrador de dispositivos de StorSimple** hoja, haga clic en **inicio rápido**. 
4. Haga clic en hello correspondiente toohello imagen del vínculo que desea toodownload de hello Microsoft Download Center. los archivos de imagen de Hello son aproximadamente 4,8 GB.
   
   * VHDX para Hyper-V en Windows Server 2012 y versiones posteriores
   * VHD para Hyper-V en Windows Server 2008 R2 y versiones posteriores
   * VMDK para VMWare ESXi 5.5 y versiones posteriores
5. Descargue y descomprima Hola archivo tooa unidad local, que realiza una nota de donde está ubicado archivo descomprimida Hola.

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>Paso opcional: configurar una nueva cuenta de almacenamiento para el servicio de Hola

Este paso es opcional y debe realizarse únicamente si no ha habilitado la creación automática de Hola de una cuenta de almacenamiento con su servicio.

Si necesita una cuenta de almacenamiento de Azure en una región distinta de toocreate, consulte [cómo toocreate una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para obtener instrucciones paso a paso.

Realizar Hola siguiendo los pasos de hello [portal de Azure](https://ms.portal.azure.com/) en hello Administrador de dispositivos de StorSimple servicio página tooadd una cuenta de almacenamiento de Microsoft Azure existente.

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd una credencial de cuenta de almacenamiento que tenga Hola misma suscripción de Azure como servicio de administrador de dispositivos de Hola

1. Navegue tooyour servicio de administrador de dispositivos, seleccione y haga doble clic en él. Se abrirá hello **Introducción** hoja.
2. Seleccione **credenciales de la cuenta de almacenamiento** en hello **configuración** sección.
3. Haga clic en **Agregar**.
4. Hola **agregar una cuenta de almacenamiento** hoja, Hola siguientes:
   
    1. En **Suscripción**, seleccione **Actual**.
   
    2. Proporcione el nombre de saludo de la cuenta de almacenamiento de Azure.
   
    3. Seleccione **habilitar** toocreate un canal seguro para la comunicación de red entre la nube de hello y el dispositivo de StorSimple. Seleccione **Deshabilitar** solo si está trabajando en una nube privada.
   
    4. Haga clic en **Agregar**. Se le notifica una vez creada correctamente de la cuenta de almacenamiento de Hola.<br></br>
   
     ![Incorporación de una credencial de cuenta de almacenamiento existente](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a>Paso siguiente

Hola siguiente paso es tooprovision una máquina virtual para la matriz Virtual de StorSimple. Dependiendo del sistema operativo del host, vea Hola detallada instrucciones:

* [Aprovisionamiento de la matriz virtual de StorSimple en Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [Aprovisionamiento de la matriz virtual de StorSimple en VMware](storsimple-virtual-array-deploy2-provision-vmware.md)

