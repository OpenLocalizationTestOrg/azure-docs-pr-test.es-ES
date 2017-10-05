---
title: "Instalación de Mobility Service para VMware en la replicación de Azure | Microsoft Docs"
description: "En este artículo se describe cómo instalar el agente de Mobility Service para VMware en la replicación de Azure con el servicio Azure Site Recovery."
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
ms.openlocfilehash: bc520bd2ea54208889861a7a3b275e3008a05d53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="4cd80-103">Paso 10: Instalación de Mobility Service</span><span class="sxs-lookup"><span data-stu-id="4cd80-103">Step 10: Install the Mobility service</span></span>


<span data-ttu-id="4cd80-104">En este artículo se describe cómo configurar opciones de origen y destino al replicar máquinas virtuales de VMware locales en Azure mediante el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4cd80-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="4cd80-105">Mobility Service captura las escrituras de datos en una máquina y las reenvía al servidor de procesos.</span><span class="sxs-lookup"><span data-stu-id="4cd80-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="4cd80-106">Se debe instalar en cada máquina que quiera se replicar en Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd80-106">It should be installed on each machine that you want to replicate to Azure.</span></span>

<span data-ttu-id="4cd80-107">Puede realizar la instalación manual de Mobility Service con una instalación de inserción desde el servidor de procesos de Site Recovery cuando la replicación está habilitada o usar una herramienta de System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="4cd80-107">You can install the Mobility service manual, using a push installation from the Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="4cd80-108">Si usa la instalación de inserción, el servicio se instala en la VM cuando se habilita la replicación.</span><span class="sxs-lookup"><span data-stu-id="4cd80-108">If you use push installation, the service is installed on the VM when replication is enabled.</span></span>

<span data-ttu-id="4cd80-109">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4cd80-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="4cd80-110">Instalación manual</span><span class="sxs-lookup"><span data-stu-id="4cd80-110">Install manually</span></span>

1. <span data-ttu-id="4cd80-111">Compruebe los [requisitos previos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para la instalación manual.</span><span class="sxs-lookup"><span data-stu-id="4cd80-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="4cd80-112">Siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para la instalación manual con el portal.</span><span class="sxs-lookup"><span data-stu-id="4cd80-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="4cd80-113">Si prefiere realizar la instalación desde la línea de comandos, siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="4cd80-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="4cd80-114">Instalación desde el servidor de procesos</span><span class="sxs-lookup"><span data-stu-id="4cd80-114">Install from the process server</span></span>

<span data-ttu-id="4cd80-115">Si quiere insertar la instalación de Mobility Service desde el servidor de procesos al habilitar la replicación de una máquina virtual, necesita una cuenta que el servidor de procesos pueda usar para acceder a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4cd80-115">If you want to push the Mobility service installation from the process server when you enable replication for a VM, you need an account that can be used by the process server to access the VM.</span></span> <span data-ttu-id="4cd80-116">La cuenta solo se utiliza para la instalación de inserción.</span><span class="sxs-lookup"><span data-stu-id="4cd80-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="4cd80-117">Debe haber [creado una cuenta](vmware-walkthrough-prepare-vmware.md) que pueda usarse para la instalación de inserción.</span><span class="sxs-lookup"><span data-stu-id="4cd80-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="4cd80-118">Especifique después la cuenta que quiere usar al establecer las opciones de configuración del origen durante la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4cd80-118">You then specify the account you want to use when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="4cd80-119">Siga luego [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si quiere insertar Mobility Service en máquinas virtuales que ejecutan Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="4cd80-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="4cd80-120">Otros métodos</span><span class="sxs-lookup"><span data-stu-id="4cd80-120">Other methods</span></span>

<span data-ttu-id="4cd80-121">Obtenga más información sobre la [instalación de Mobility Service con Configuration Manager](site-recovery-install-mobility-service-using-sccm.md) o con [DSC de Azure Automation](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="4cd80-121">Learn more about [installing the Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cd80-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4cd80-122">Next steps</span></span>

<span data-ttu-id="4cd80-123">Ir a [Paso 11: Habilitación de la replicación](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="4cd80-123">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
