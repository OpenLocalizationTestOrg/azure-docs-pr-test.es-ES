---
title: "Configurar el entorno de origen hello (tooAzure servidores físicos) | Documentos de Microsoft"
description: "Este artículo se describe cómo tooset seguridad su toostart del entorno local replicar servidores físicos que ejecutan Windows o Linux en Azure."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>Configurar el entorno de origen hello (servidor físico tooAzure)
> [!div class="op_single_selector"]
> * [TooAzure de VMware](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure físico](./site-recovery-set-up-physical-to-azure.md)

Este artículo se describe cómo tooset seguridad su toostart del entorno local replicar servidores físicos que ejecutan Windows o Linux en Azure.

## <a name="prerequisites"></a>Requisitos previos

artículo de Hola se supone que ya tiene:
1. Un almacén de servicios de recuperación de hello [portal de Azure](http://portal.azure.com "portal de Azure").
3. Un equipo físico en el servidor de configuración de tooinstall Hola.

### <a name="configuration-server-minimum-requirements"></a>Requisitos mínimos del servidor de configuración
Hello en la tabla siguiente enumera Hola mínimos de hardware, software y requisitos de red para un servidor de configuración.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> No se admiten servidores proxy basada en HTTPS al servidor de configuración de Hola.

## <a name="choose-your-protection-goals"></a>Selección de los objetivos de protección

1. Hola portal de Azure, vaya toohello **servicios de recuperación** hoja los almacenes de credenciales y seleccione el almacén.
2. Hola **recursos** menú de almacén de hello, haga clic en **Introducción** > **Site Recovery** > **paso 1: preparar Infraestructura** > **objetivo de protección**.

    ![Elegir objetivos](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. En **objetivo de protección**, seleccione **tooAzure** y **no virtualizados/otros**y, a continuación, haga clic en **Aceptar**.

    ![Elegir objetivos](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

1. En **preparar origen**, si no tiene un servidor de configuración, haga clic en **+ servidor de configuración** tooadd uno.

  ![Configurar origen](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. Hola **Agregar servidor** hoja, compruebe que **servidor de configuración** aparece en **tipo de servidor**.
4. Descargue el archivo de instalación de configuración de Site Recovery unificado de Hola.
5. Descargue la clave de registro del almacén de Hola. Se necesita la clave de registro de hello al ejecutar el programa de instalación unificada. clave de Hello es válida durante cinco días después de generarlo.

    ![Configurar origen](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. En el equipo de Hola que utilice como servidor de configuración de hello, ejecute **instalación unificada de Azure Site Recovery** servidor de configuración de tooinstall Hola, servidor de procesos de Hola y Hola maestro servidor de destino.

#### <a name="run-azure-site-recovery-unified-setup"></a>Ejecución de la instalación unificada de Azure Site Recovery

> [!TIP]
> Se produce un error en el registro del servidor de configuración si el tiempo de hello en el reloj del sistema del equipo es más de cinco minutos en hora local. Sincronizar el reloj del sistema con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar la instalación de Hola.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> servidor de configuración de Hello puede instalarse a través de una línea de comandos. Para obtener más información, consulte [Instalación del servidor de configuración con herramientas de línea de comandos](http://aka.ms/installconfigsrv).


## <a name="common-issues"></a>Problemas comunes

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Pasos siguientes

El paso siguiente implica [configurar el entorno de destino](./site-recovery-prepare-target-physical-to-azure.md) en Azure.
