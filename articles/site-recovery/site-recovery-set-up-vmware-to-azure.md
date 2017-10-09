---
title: Configurar el entorno de origen hello (VMware tooAzure) | Documentos de Microsoft
description: "Este artículo describe cómo tooset seguridad su toostart del entorno local replicar VMware virtual máquinas tooAzure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>Configurar el entorno de origen hello (tooAzure de VMware)
> [!div class="op_single_selector"]
> * [TooAzure de VMware](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure físico](./site-recovery-set-up-physical-to-azure.md)

Este artículo describe cómo ejecutar los equipos de tooset seguridad su toostart del entorno local replicar virtual de VMware tooAzure.

## <a name="prerequisites"></a>Requisitos previos

artículo de Hola se supone que ya ha creado:
- Un almacén de servicios de recuperación de hello [portal de Azure](http://portal.azure.com "portal de Azure").
- Una cuenta dedicada en el vCenter de VMware que se puede usar para [detección automática](./site-recovery-vmware-to-azure.md).
- Una máquina virtual en el servidor de configuración de tooinstall Hola.

## <a name="configuration-server-minimum-requirements"></a>Requisitos mínimos del servidor de configuración
software de servidor de configuración de Hello debe implementarse en una máquina virtual de VMware alta disponibilidad. Hello en la tabla siguiente enumera Hola mínimos de hardware, software y requisitos de red para un servidor de configuración.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> No se admiten servidores proxy basada en HTTPS al servidor de configuración de Hola.

## <a name="choose-your-protection-goals"></a>Selección de los objetivos de protección

1. Hola portal de Azure, vaya toohello **servicios de recuperación** hoja del almacén y seleccione el almacén.
2. En el menú de recursos de Hola de almacén de hello, que se vaya demasiado**Introducción** > **Site Recovery** > **paso 1: preparar la infraestructura**  >  **Objetivo de protección**.

    ![Elegir objetivos](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. En **objetivo de protección**, seleccione **tooAzure**y elija **Sí, con el hipervisor de VMware vSphere**. y, a continuación, haga clic en **Aceptar**.

    ![Elegir objetivos](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola
Configurar el entorno de origen Hola implica dos actividades principales:

- Instale y registre un servidor de configuración con Site Recovery.
- Descubra las máquinas virtuales de local mediante la conexión de Site Recovery tooyour local vCenter o vSphere EXSi hosts de VMware.

### <a name="step-1-install-and-register-a-configuration-server"></a>Paso 1: Instalar y registrar un servidor de configuración

1. Haga clic en **Paso 1: Preparar la infraestructura** > **Origen**. En **preparar origen**, si no tiene un servidor de configuración, haga clic en **+ servidor de configuración** tooadd uno.

    ![Configurar origen](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. En hello **Agregar servidor** hoja, compruebe que **servidor de configuración** aparece en **tipo de servidor**.
4. Descargue el archivo de instalación de configuración de Site Recovery unificado de Hola.
5. Descargue la clave de registro del almacén de Hola. Se necesita la clave de registro de hello al ejecutar el programa de instalación unificada. clave de Hello es válida durante cinco días después de generarlo.

    ![Configurar origen](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. En el equipo de Hola que utilice como servidor de configuración de hello, ejecute **instalación unificada de Azure Site Recovery** servidor de configuración de tooinstall Hola, servidor de procesos de Hola y Hola maestro servidor de destino.

#### <a name="run-azure-site-recovery-unified-setup"></a>Ejecución de la instalación unificada de Azure Site Recovery

> [!TIP]
> Se produce un error en el registro del servidor de configuración si la hora de hello en el reloj del sistema del equipo difiere de la hora local en más de cinco minutos. Sincronizar el reloj del sistema con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar la instalación de Hola.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> servidor de configuración de Hello puede instalarse a través de la línea de comandos. Para obtener más información, consulte [instalar servidor de configuración de hello mediante herramientas de línea de comandos](http://aka.ms/installconfigsrv).

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>Agregar cuenta de VMware de hello para la detección automática

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>Paso 2: Agregar un vCenter
tooallow Azure Site Recovery toodiscover máquinas virtuales que ejecutan en su entorno local, debe tooconnect el servidor VMware vCenter o hosts de ESXi vSphere con Site Recovery.

Seleccione **+ vCenter** toostart conectar un servidor VMware vCenter o un host de VMware vSphere ESXi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>Problemas comunes
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Pasos siguientes
[Configure el entorno de destino](./site-recovery-prepare-target-vmware-to-azure.md) en Azure.
