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
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="4ae18-103">Configurar el entorno de origen hello (servidor físico tooAzure)</span><span class="sxs-lookup"><span data-stu-id="4ae18-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ae18-104">TooAzure de VMware</span><span class="sxs-lookup"><span data-stu-id="4ae18-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="4ae18-105">TooAzure físico</span><span class="sxs-lookup"><span data-stu-id="4ae18-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="4ae18-106">Este artículo se describe cómo tooset seguridad su toostart del entorno local replicar servidores físicos que ejecutan Windows o Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae18-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ae18-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4ae18-107">Prerequisites</span></span>

<span data-ttu-id="4ae18-108">artículo de Hola se supone que ya tiene:</span><span class="sxs-lookup"><span data-stu-id="4ae18-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="4ae18-109">Un almacén de servicios de recuperación de hello [portal de Azure](http://portal.azure.com "portal de Azure").</span><span class="sxs-lookup"><span data-stu-id="4ae18-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="4ae18-110">Un equipo físico en el servidor de configuración de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae18-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="4ae18-111">Requisitos mínimos del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="4ae18-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="4ae18-112">Hello en la tabla siguiente enumera Hola mínimos de hardware, software y requisitos de red para un servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="4ae18-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="4ae18-113">No se admiten servidores proxy basada en HTTPS al servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae18-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="4ae18-114">Selección de los objetivos de protección</span><span class="sxs-lookup"><span data-stu-id="4ae18-114">Choose your protection goals</span></span>

1. <span data-ttu-id="4ae18-115">Hola portal de Azure, vaya toohello **servicios de recuperación** hoja los almacenes de credenciales y seleccione el almacén.</span><span class="sxs-lookup"><span data-stu-id="4ae18-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="4ae18-116">Hola **recursos** menú de almacén de hello, haga clic en **Introducción** > **Site Recovery** > **paso 1: preparar Infraestructura** > **objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="4ae18-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Elegir objetivos](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="4ae18-118">En **objetivo de protección**, seleccione **tooAzure** y **no virtualizados/otros**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4ae18-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Elegir objetivos](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="4ae18-120">Configurar el entorno de origen Hola</span><span class="sxs-lookup"><span data-stu-id="4ae18-120">Set up hello source environment</span></span>

1. <span data-ttu-id="4ae18-121">En **preparar origen**, si no tiene un servidor de configuración, haga clic en **+ servidor de configuración** tooadd uno.</span><span class="sxs-lookup"><span data-stu-id="4ae18-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![Configurar origen](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="4ae18-123">Hola **Agregar servidor** hoja, compruebe que **servidor de configuración** aparece en **tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="4ae18-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="4ae18-124">Descargue el archivo de instalación de configuración de Site Recovery unificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae18-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="4ae18-125">Descargue la clave de registro del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae18-125">Download hello vault registration key.</span></span> <span data-ttu-id="4ae18-126">Se necesita la clave de registro de hello al ejecutar el programa de instalación unificada.</span><span class="sxs-lookup"><span data-stu-id="4ae18-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="4ae18-127">clave de Hello es válida durante cinco días después de generarlo.</span><span class="sxs-lookup"><span data-stu-id="4ae18-127">hello key is valid for five days after you generate it.</span></span>

    ![Configurar origen](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="4ae18-129">En el equipo de Hola que utilice como servidor de configuración de hello, ejecute **instalación unificada de Azure Site Recovery** servidor de configuración de tooinstall Hola, servidor de procesos de Hola y Hola maestro servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="4ae18-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="4ae18-130">Ejecución de la instalación unificada de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="4ae18-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="4ae18-131">Se produce un error en el registro del servidor de configuración si el tiempo de hello en el reloj del sistema del equipo es más de cinco minutos en hora local.</span><span class="sxs-lookup"><span data-stu-id="4ae18-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="4ae18-132">Sincronizar el reloj del sistema con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae18-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="4ae18-133">servidor de configuración de Hello puede instalarse a través de una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="4ae18-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="4ae18-134">Para obtener más información, consulte [Instalación del servidor de configuración con herramientas de línea de comandos](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="4ae18-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="4ae18-135">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="4ae18-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="4ae18-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ae18-136">Next steps</span></span>

<span data-ttu-id="4ae18-137">El paso siguiente implica [configurar el entorno de destino](./site-recovery-prepare-target-physical-to-azure.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae18-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
