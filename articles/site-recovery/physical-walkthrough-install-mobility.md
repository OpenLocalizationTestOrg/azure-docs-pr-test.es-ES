---
title: "Instalación de Mobility Service para el servidor físico para la replicación de Azure | Microsoft Docs"
description: "En este artículo se describe cómo instalar el agente de Mobility Service en servidores físicos que se replican en Azure con el servicio Azure Site Recovery."
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
ms.openlocfilehash: d73267d7a64221a3138af19e9a2d5dd15809b927
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="eddc7-103">Paso 9: Instalación del servicio de movilidad</span><span class="sxs-lookup"><span data-stu-id="eddc7-103">Step 9: Install the Mobility service</span></span>


<span data-ttu-id="eddc7-104">En este artículo se describe cómo instalar el componente de Mobility Service cuando se replican servidores físicos de Windows/Linux locales en Azure con el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="eddc7-104">This article describes how to install the Mobility service component when replicating on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="eddc7-105">Mobility Service captura las escrituras de datos en una máquina y las reenvía al servidor de procesos.</span><span class="sxs-lookup"><span data-stu-id="eddc7-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="eddc7-106">Se debe instalar en cada servidor que quiera se replicar en Azure.</span><span class="sxs-lookup"><span data-stu-id="eddc7-106">It should be installed on each server that you want to replicate to Azure.</span></span>

<span data-ttu-id="eddc7-107">Puede realizar la instalación manual de Mobility Service, realizar una instalación de inserción desde el servidor de procesos de Site Recovery cuando la replicación está habilitada o usar una herramienta como System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="eddc7-107">You can install the Mobility service manually, or using a push installation from the Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="eddc7-108">Si usa la instalación de inserción, el servicio se instala en el servidor cuando se habilita la replicación.</span><span class="sxs-lookup"><span data-stu-id="eddc7-108">If you use push installation, the service is installed on the server when you enable replication.</span></span>

<span data-ttu-id="eddc7-109">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="eddc7-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="eddc7-110">Instalación manual</span><span class="sxs-lookup"><span data-stu-id="eddc7-110">Install manually</span></span>

1. <span data-ttu-id="eddc7-111">Compruebe los [requisitos previos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para la instalación manual.</span><span class="sxs-lookup"><span data-stu-id="eddc7-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="eddc7-112">Siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para la instalación manual con el portal.</span><span class="sxs-lookup"><span data-stu-id="eddc7-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="eddc7-113">Si prefiere realizar la instalación desde la línea de comandos, siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="eddc7-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="eddc7-114">Instalación desde el servidor de procesos</span><span class="sxs-lookup"><span data-stu-id="eddc7-114">Install from the process server</span></span>

<span data-ttu-id="eddc7-115">Si quiere insertar la instalación de Mobility Service desde el servidor de procesos al habilitar la replicación de una máquina, necesita una cuenta que el servidor de procesos pueda usar para acceder a la máquina.</span><span class="sxs-lookup"><span data-stu-id="eddc7-115">If you want to push the Mobility service installation from the process server when you enable replication for a machine, you need an account that can be used by the process server to access the machine.</span></span> <span data-ttu-id="eddc7-116">La cuenta solo se utiliza para la instalación de inserción.</span><span class="sxs-lookup"><span data-stu-id="eddc7-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="eddc7-117">Si no ha creado una cuenta, hágalo haciendo uso de estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="eddc7-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="eddc7-118">Puede usar una cuenta local o de dominio.</span><span class="sxs-lookup"><span data-stu-id="eddc7-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="eddc7-119">Para Windows, si no utiliza una cuenta de dominio, debe deshabilitar Access Control de usuario remoto en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="eddc7-119">For Windows, if you're not using a domain account, you need to disable Remote User Access control on the local machine.</span></span> <span data-ttu-id="eddc7-120">Para hacerlo, en el Registro, en **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, agregue la entrada DWORD **LocalAccountTokenFilterPolicy** con un valor de 1.</span><span class="sxs-lookup"><span data-stu-id="eddc7-120">To do this, in the register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add the DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="eddc7-121">Si desea agregar la entrada del Registro de Windows desde una CLI, escriba:</span><span class="sxs-lookup"><span data-stu-id="eddc7-121">If you want to add the registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="eddc7-122">Para Linux, la cuenta debe ser una raíz en el servidor Linux de origen.</span><span class="sxs-lookup"><span data-stu-id="eddc7-122">For Linux, the account should be root on the source Linux server.</span></span>

2. <span data-ttu-id="eddc7-123">Siga luego [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si quiere insertar Mobility Service en máquinas virtuales que ejecutan Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="eddc7-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="eddc7-124">Otros métodos de instalación</span><span class="sxs-lookup"><span data-stu-id="eddc7-124">Other installation methods</span></span>

- <span data-ttu-id="eddc7-125">[Más información sobre la ](site-recovery-install-mobility-service-using-sccm.md)instalación de Mobility Service con Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="eddc7-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing the Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="eddc7-126">[Más información sobre la ](site-recovery-automate-mobility-service-install.md)instalación con DSC de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="eddc7-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="eddc7-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eddc7-127">Next steps</span></span>

<span data-ttu-id="eddc7-128">Vaya a [Paso 10: Habilitación de la replicación](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="eddc7-128">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
