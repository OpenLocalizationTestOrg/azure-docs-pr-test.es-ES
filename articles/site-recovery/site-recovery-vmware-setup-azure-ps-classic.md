---
title: " Administración de un servidor de procesos que se ejecuta en Azure (clásico) | Microsoft Docs"
description: "Este artículo se describe cómo tooset la una conmutación por recuperación Server(Classic) del proceso de Azure."
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a>Administración de un servidor de procesos que se ejecuta en Azure (clásico)
> [!div class="op_single_selector"]
> * [Azure clásico](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

Durante la conmutación por recuperación, se recomienda toodeploy servidor de procesos en Azure si no hay una latencia elevada entre Hola red Virtual de Azure y la red local. Este artículo describe cómo instalar, configurar y administrar servidores de procesos de hello ejecuta en Azure.

> [!NOTE]
> Este artículo es toobe si utiliza clásico como modelo de implementación de Hola para las máquinas virtuales de Hola durante la conmutación por error. Si utiliza el Administrador de recursos como Hola pasos de implementación modelo seguimiento hello en [cómo tooset una copia de seguridad y configurar un servidor de procesos de conmutación por recuperación (Administrador de recursos)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a>Requisitos previos

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Implementación de un servidor de procesos en Azure

1. En Azure Marketplace, cree una máquina virtual mediante hello **recuperación de sitio de Microsoft Azure proceso servidor V2** </br>
    ![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)
2. Asegúrese de seleccionar el modelo de implementación de hello como **clásico** </br>
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)
3. En el Asistente para la máquina virtual de creación de hello > configuración básica, asegúrese de seleccionar toowhere de suscripción y la ubicación de hello conmutado hello las máquinas virtuales.</br>
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)
4. Asegúrese de que está conectada a esa máquina virtual de Hola Hola de toowhich de red Virtual de Azure toohello conmutado por máquina virtual está conectado.</br>
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)
5. Cuando se aprovisiona la máquina virtual de servidor de procesos de hello, toolog en es necesario y registrarlo con un servidor de configuración de Hola.

> [!NOTE]
> toobe puede toouse este servidor de procesos de conmutación por recuperación, deberá tooregister con el servidor de configuración de hello en local.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Registrar hello tooa de servidor de proceso (que se ejecuta en Azure) servidor de configuración (ejecutando de forma local)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Actualización de versión de toolatest del servidor de procesos de Hola.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Hola al anular el registro de servidor de proceso (que se ejecuta en Azure) desde un servidor de configuración (ejecutando de forma local)

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
