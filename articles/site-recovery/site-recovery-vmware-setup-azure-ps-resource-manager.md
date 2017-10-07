---
title: " Administración de un servidor de procesos que se ejecuta en Azure (Resource Manager) | Microsoft Docs"
description: "Este artículo describe cómo tooset la una conmutación por recuperación proceso server (Administrador de recursos) en Azure."
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a>Administración de un servidor de procesos que se ejecuta en Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [Clásico](./site-recovery-vmware-setup-azure-ps-classic.md)

Durante la conmutación por recuperación, se recomienda toodeploy el servidor de procesos en Azure si no hay una latencia elevada entre Hola red Virtual de Azure y la red local. Este artículo describe cómo instalar, configurar y administrar servidores de procesos de hello ejecuta en Azure.

> [!NOTE]
> Este artículo es toobe si utiliza **el Administrador de recursos** como modelo de implementación de Hola para las máquinas virtuales de Hola durante la conmutación por error. Si ha usado **clásico** como modelo de implementación de hello, siga los pasos de hello en [cómo tooset una copia de seguridad y configurar un servidor de procesos de conmutación por recuperación (clásico)](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a>Requisitos previos

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Implementación de un servidor de procesos en Azure
1. Hola almacén > **infraestructura del sitio de recuperación** (bajo el encabezado de "Manage" hello) > **servidores de configuración** (bajo el encabezado "Para VMware y máquinas físicas"), seleccione el servidor de configuración de Hola.
2. En la página de detalles del servidor de configuración Hola que se abre, haga clic en "+ servidor de procesos"

  ![Adición de una galería del servidor de procesos](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  En hello **Agregar servidor de proceso** seleccione Hola después de los valores de la página

  ![Adición de un elemento de la galería del servidor de procesos](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|**Nombre del campo**|**Valor**|
|-|-|
|Elegir dónde quiere toodeploy el servidor de procesos|Seleccione el valor de hello **implementar un servidor de procesos de conmutación por recuperación de Azure** |
|La suscripción|Seleccione la suscripción de Azure que ha conmutado por error máquinas virtuales de Hola Hola|
|Grupo de recursos|Puede crear un grupo de recursos toodeploy este servidor de procesos o elegir servidor de procesos de hello toodeploy en un grupo de recursos existente|
|Ubicación|Seleccione el centro de datos de Azure de hello en las máquinas virtuales que Hola donde conmutación por error en|
|Red de Azure|Seleccione hello Network(VNet) Virtual de Azure que Hola máquinas virtuales donde conmutación por error en. Si ha conmutado por error máquinas virtuales en varias redes virtuales de Azure, necesita un servidor de proceso implementado por red virtual.|

4. Rellene Hola resto de propiedades de hello en servidor de procesos de Hola

  ![Adición de un resumen del servidor de procesos](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|**Nombre del campo**|**Valor**|
|-|-|
|Nombre del servidor|Nombre para mostrar o nombre de host para la máquina virtual del servidor de procesos|
| User Name|Nombre de usuario que se convierte en un administrador de esa máquina virtual|
|Cuenta de almacenamiento|Nombre de cuenta de almacenamiento donde se coloca del disco virtual de la máquina virtual Hola Hola|
|Subred|Hola subred de máquina virtual de hello red virtual de Azure toowhich Hola está conectada|
| Dirección IP|Dirección IP que desearía Hola proceso servidor tooassume una vez que se inician|
5. Haga clic en hello botón Aceptar toostart implementación de máquina virtual de hello proceso servidor.

> [!NOTE]
> toobe puede toouse este servidor de procesos de conmutación por recuperación, deberá tooregister con el servidor de configuración de hello en local.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Registrar Hola proceso servidor (que se ejecuta en Azure) tooa servidor de configuración (ejecutando de forma local)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Actualizando Hola proceso toolatest versión del servidor.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Al anular el registro de servidor de proceso de hello (que se ejecuta en Azure) desde un servidor de configuración (ejecutando de forma local)

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
