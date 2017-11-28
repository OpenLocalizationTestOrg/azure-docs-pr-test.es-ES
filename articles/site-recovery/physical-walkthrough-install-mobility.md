---
title: "Hola aaaInstall servicio de movilidad de replicación de servidor físico tooAzure | Documentos de Microsoft"
description: "Este artículo describe cómo tooinstall Hola a agente del servicio de movilidad en servidores físicos replicar tooAzure con servicio de Azure Site Recovery Hola."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="fb229-103">Paso 9: Instalar el servicio de movilidad de Hola</span><span class="sxs-lookup"><span data-stu-id="fb229-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="fb229-104">Este artículo describe cómo componente de servicio de movilidad de tooinstall Hola al replicar local tooAzure de servidores físicos de Windows o Linux, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb229-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="fb229-105">Hola servicio de movilidad captura escrituras de datos en un equipo y los reenvía toohello servidor de procesos.</span><span class="sxs-lookup"><span data-stu-id="fb229-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="fb229-106">Debe instalarse en cada servidor que desea tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fb229-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="fb229-107">Se puede instalar manualmente el servicio de movilidad de hello, o mediante una instalación de inserción de hello Site Recovery proceso servidor cuando está habilitada la replicación, o mediante una herramienta como System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="fb229-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="fb229-108">Si utiliza la instalación de inserción, servicio de hello está instalado en el servidor de hello cuando se habilita la replicación.</span><span class="sxs-lookup"><span data-stu-id="fb229-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="fb229-109">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fb229-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="fb229-110">Instalación manual</span><span class="sxs-lookup"><span data-stu-id="fb229-110">Install manually</span></span>

1. <span data-ttu-id="fb229-111">Comprobar hello [requisitos previos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para la instalación manual.</span><span class="sxs-lookup"><span data-stu-id="fb229-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="fb229-112">Siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para la instalación manual mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb229-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="fb229-113">Si prefiere tooinstall desde la línea de comandos de hello, siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="fb229-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="fb229-114">Instalar desde el servidor de procesos de Hola</span><span class="sxs-lookup"><span data-stu-id="fb229-114">Install from hello process server</span></span>

<span data-ttu-id="fb229-115">Si desea toopush Hola instalación del servicio de movilidad Hola del servidor de procesos cuando se habilita la replicación de una máquina, necesita una cuenta que puede usarse para la máquina de hello proceso servidor tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="fb229-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="fb229-116">cuenta de Hello solo se utiliza para la instalación de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb229-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="fb229-117">Si no ha creado una cuenta, hágalo haciendo uso de estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="fb229-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="fb229-118">Puede usar una cuenta local o de dominio.</span><span class="sxs-lookup"><span data-stu-id="fb229-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="fb229-119">Para Windows, si no usa una cuenta de dominio, debe toodisable control de acceso de usuarios remotos en el equipo local de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb229-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="fb229-120">toodo, Hola registrar con **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, agregar una entrada DWORD hello **LocalAccountTokenFilterPolicy**, con un valor de 1.</span><span class="sxs-lookup"><span data-stu-id="fb229-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="fb229-121">Si desea que entrada de registro de hello tooadd de Windows desde una CLI, escriba:</span><span class="sxs-lookup"><span data-stu-id="fb229-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="fb229-122">Para Linux, la cuenta de hello debe ser raíz Hola servidor de origen Linux.</span><span class="sxs-lookup"><span data-stu-id="fb229-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="fb229-123">A continuación, siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si desea que el servicio de movilidad de hello toopush en máquinas virtuales que ejecutan Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="fb229-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="fb229-124">Otros métodos de instalación</span><span class="sxs-lookup"><span data-stu-id="fb229-124">Other installation methods</span></span>

- <span data-ttu-id="fb229-125">[Obtenga información acerca de](site-recovery-install-mobility-service-using-sccm.md) instalar servicio de movilidad de hello mediante Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="fb229-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="fb229-126">[Más información sobre la ](site-recovery-automate-mobility-service-install.md)instalación con DSC de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fb229-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fb229-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb229-127">Next steps</span></span>

<span data-ttu-id="fb229-128">Vaya demasiado[paso 10: habilitar la replicación](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="fb229-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
