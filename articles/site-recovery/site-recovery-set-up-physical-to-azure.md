---
title: "Configuración del entorno de origen (servidores físicos a Azure) | Microsoft Docs"
description: "En este artículo se describe cómo configurar el entorno local para comenzar a replicar servidores físicos que ejecutan Windows o Linux en Azure."
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
ms.openlocfilehash: 49b9d2e21dbcb612828a25f21ed4382327d6f64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-the-source-environment-physical-server-to-azure"></a><span data-ttu-id="3fd97-103">Configuración del entorno de origen (servidores físicos a Azure)</span><span class="sxs-lookup"><span data-stu-id="3fd97-103">Set up the source environment (physical server to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3fd97-104">VMware a Azure</span><span class="sxs-lookup"><span data-stu-id="3fd97-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="3fd97-105">Físico a Azure</span><span class="sxs-lookup"><span data-stu-id="3fd97-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="3fd97-106">En este artículo se describe cómo configurar el entorno local para comenzar a replicar servidores físicos que ejecutan Windows o Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="3fd97-106">This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fd97-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3fd97-107">Prerequisites</span></span>

<span data-ttu-id="3fd97-108">En este artículo se supone que ya cuenta con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3fd97-108">The article assumes that you already have:</span></span>
1. <span data-ttu-id="3fd97-109">Un almacén de Recovery Services en [Azure Portal](http://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="3fd97-109">A Recovery Services vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="3fd97-110">Un equipo físico para instalar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="3fd97-110">A physical computer on which to install the configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="3fd97-111">Requisitos mínimos del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="3fd97-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="3fd97-112">En la siguiente tabla se muestran los requisitos mínimos de hardware, software y red para un servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="3fd97-112">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="3fd97-113">El servidor de configuración no admite los servidores proxy basados en HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3fd97-113">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="3fd97-114">Selección de los objetivos de protección</span><span class="sxs-lookup"><span data-stu-id="3fd97-114">Choose your protection goals</span></span>

1. <span data-ttu-id="3fd97-115">En Azure Portal, vaya a la hoja de los almacenes de **Recovery Services** y seleccione su almacén.</span><span class="sxs-lookup"><span data-stu-id="3fd97-115">In the Azure portal, go to the **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="3fd97-116">En el menú de **Recurso** del almacén, haga clic en **Introducción** > **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="3fd97-116">In the **Resource** menu of the vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Elegir objetivos](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="3fd97-118">En **Objetivo de protección**, seleccione **To Azure** (En Azure) y, luego, **No virtualizado/otro**; después haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3fd97-118">In **Protection goal**, select **To Azure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Elegir objetivos](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="3fd97-120">Configuración del entorno de origen</span><span class="sxs-lookup"><span data-stu-id="3fd97-120">Set up the source environment</span></span>

1. <span data-ttu-id="3fd97-121">En **Preparar origen**, si no tiene un servidor de configuración, haga clic en **+Servidor de configuración** para agregar uno.</span><span class="sxs-lookup"><span data-stu-id="3fd97-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

  ![Configurar origen](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="3fd97-123">En la hoja **Agregar servidor**, compruebe que **Servidor de configuración** aparezca en **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="3fd97-123">In the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="3fd97-124">Descargue el archivo de instalación unificada de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3fd97-124">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="3fd97-125">Descargue la clave de registro del almacén.</span><span class="sxs-lookup"><span data-stu-id="3fd97-125">Download the vault registration key.</span></span> <span data-ttu-id="3fd97-126">Necesita la clave de registro cuando ejecuta la instalación unificada.</span><span class="sxs-lookup"><span data-stu-id="3fd97-126">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="3fd97-127">La clave será válida durante cinco días a partir del momento en que se genera.</span><span class="sxs-lookup"><span data-stu-id="3fd97-127">The key is valid for five days after you generate it.</span></span>

    ![Configurar origen](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="3fd97-129">En la máquina que usa como el servidor de configuración, ejecute la **instalación unificada de Azure Site Recovery** para instalar el servidor de configuración, el servidor de procesos y el servidor de destino maestro.</span><span class="sxs-lookup"><span data-stu-id="3fd97-129">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="3fd97-130">Ejecución de la instalación unificada de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="3fd97-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="3fd97-131">El registro del servidor de configuración presenta errores si la hora del reloj del sistema de su equipo tiene más de cinco minutos de diferencia con respecto a la hora local.</span><span class="sxs-lookup"><span data-stu-id="3fd97-131">Configuration server registration fails if the time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="3fd97-132">Sincronice el reloj del sistema con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de comenzar la instalación.</span><span class="sxs-lookup"><span data-stu-id="3fd97-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="3fd97-133">El servidor de configuración se puede instalar a través de una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="3fd97-133">The configuration server can be installed via a command line.</span></span> <span data-ttu-id="3fd97-134">Para obtener más información, consulte [Instalación del servidor de configuración con herramientas de línea de comandos](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="3fd97-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="3fd97-135">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="3fd97-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="3fd97-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3fd97-136">Next steps</span></span>

<span data-ttu-id="3fd97-137">El paso siguiente implica [configurar el entorno de destino](./site-recovery-prepare-target-physical-to-azure.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="3fd97-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
