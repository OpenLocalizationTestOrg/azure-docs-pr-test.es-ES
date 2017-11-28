---
title: "aaaGet un identificador de máquina virtual de Linux de Azure | Documentos de Microsoft"
description: "Describe cómo tooget y use una única máquina virtual de Azure Linux identificador."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="b4028-103">Acceso y uso del identificador único de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="b4028-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="b4028-104">El identificador único de máquina virtual de Azure es un identificador de 128 bits codificado y almacenado en todas las SMBIOS de la máquina virtual IaaS de Azure; actualmente se puede leer mediante comandos BIOS de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="b4028-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="b4028-105">El identificador único de máquina virtual de Azure es una propiedad de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="b4028-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="b4028-106">El identificador único de máquina virtual de Azure no cambiará durante el cierre de reinicio (tanto si se ha planeado como si no), durante el inicio o la detención de la desasignación, durante la recuperación del servicio o la restauración local.</span><span class="sxs-lookup"><span data-stu-id="b4028-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="b4028-107">Sin embargo, si hello VM es una instantánea y copiado toocreate una nueva instancia, se configura nuevo Id. de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4028-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="b4028-108">Si tiene máquinas virtuales anteriores crearlas y ejecutan porque esta nueva característica se obtuvo implantada (18 de septiembre de 2014), reinicie la máquina virtual tooautomatically obtener un identificador único Azure.</span><span class="sxs-lookup"><span data-stu-id="b4028-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="b4028-109">tooaccess Azure único Id. de máquina virtual desde dentro de hello VM:</span><span class="sxs-lookup"><span data-stu-id="b4028-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="b4028-110">Creación de una VM</span><span class="sxs-lookup"><span data-stu-id="b4028-110">Create a VM</span></span>
<span data-ttu-id="b4028-111">Para más información, consulte [Creación de una máquina virtual](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4028-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="b4028-112">Conectar toohello VM</span><span class="sxs-lookup"><span data-stu-id="b4028-112">Connect toohello VM</span></span>
<span data-ttu-id="b4028-113">Para más información, consulte [SSH desde Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4028-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="b4028-114">Consulta de un identificador único de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b4028-114">Query VM Unique ID</span></span>
<span data-ttu-id="b4028-115">Comando (en el ejemplo se emplea **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="b4028-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="b4028-116">Resultados esperados del ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b4028-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="b4028-117">Pagar tooBig un orden de bits Endian, hello real Id. único de VM en este caso puede ser:</span><span class="sxs-lookup"><span data-stu-id="b4028-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="b4028-118">Id. único de Azure VM puede utilizarse en escenarios diferentes si hello VM se ejecuta en Azure o en local y puede ayudar a los requisitos de seguimiento de licencias, informes o general que puede tener en sus implementaciones de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4028-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="b4028-119">Muchos proveedores independientes de software crear aplicaciones y certificar a ellos en Azure pueden requerir una VM de Azure a lo largo de su ciclo de vida y tootell tooidentify si Hola VM se ejecuta en Azure, local o en otros proveedores de nube.</span><span class="sxs-lookup"><span data-stu-id="b4028-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="b4028-120">Este identificador de plataforma como puede ayudar a detectar si el software de hello tiene una licencia o ayuda toocorrelate cualquier origen de tooits de datos de máquina virtual como tooassist acerca de cómo configurar las métricas de derecho de hello para la plataforma correcta de Hola y tootrack y correlacionar estas métricas entre otros usos.</span><span class="sxs-lookup"><span data-stu-id="b4028-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>

