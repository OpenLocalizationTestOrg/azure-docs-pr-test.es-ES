---
title: "aaaInstall Symantec Endpoint Protection en una máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall y configure la extensión de seguridad de Symantec Endpoint Protection de hello en un nuevo o VM de Azure existente creado con el modelo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="3f675-103">¿Cómo tooinstall y configurar Symantec Endpoint Protection en una VM de Windows</span><span class="sxs-lookup"><span data-stu-id="3f675-103">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="3f675-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3f675-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3f675-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="3f675-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3f675-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f675-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="3f675-107">Este artículo muestra cómo tooinstall y configurar el cliente de Symantec Endpoint Protection de hello en una máquina virtual (VM) existente con Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3f675-107">This article shows you how tooinstall and configure hello Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="3f675-108">Este es el cliente completo, que incluye servicios como protección contra virus y spyware, firewall y prevención de intrusiones.</span><span class="sxs-lookup"><span data-stu-id="3f675-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="3f675-109">cliente de Hola se instala como una extensión de seguridad mediante el uso de hello agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f675-109">hello client is installed as a security extension by using hello VM Agent.</span></span>

<span data-ttu-id="3f675-110">Si tiene una suscripción de Symantec para una solución local, se puede usar tooprotect máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f675-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it tooprotect your Azure virtual machines.</span></span> <span data-ttu-id="3f675-111">Si todavía no es cliente, puede suscribirse para una prueba.</span><span class="sxs-lookup"><span data-stu-id="3f675-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="3f675-112">Para obtener más información sobre esta solución, consulte [Symantec Endpoint Protection en la plataforma de Microsoft Azure][Symantec].</span><span class="sxs-lookup"><span data-stu-id="3f675-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="3f675-113">Esta página también contiene información de toolicensing vínculos e instrucciones para instalar el cliente de hello si ya tiene un cliente de Symantec.</span><span class="sxs-lookup"><span data-stu-id="3f675-113">This page also has links toolicensing information and instructions for installing hello client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="3f675-114">Instalación de Symantec Endpoint Protection en una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="3f675-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="3f675-115">Antes de empezar, necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="3f675-115">Before you begin, you need hello following:</span></span>

* <span data-ttu-id="3f675-116">módulo de PowerShell de Azure de Hello, versión 0.8.2 o posterior, en el equipo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3f675-116">hello Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="3f675-117">Puede comprobar la versión de Hola de PowerShell de Azure que ha instalado con hello **Get-Module azure | versión de formato de tabla** comando.</span><span class="sxs-lookup"><span data-stu-id="3f675-117">You can check hello version of Azure PowerShell that you have installed with hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="3f675-118">Para obtener instrucciones y una versión más reciente de toohello de vínculo, vea [cómo tooInstall y configurar Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="3f675-118">For instructions and a link toohello latest version, see [How tooInstall and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="3f675-119">Inicie sesión con suscripción de Azure de tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="3f675-119">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="3f675-120">Hola Hola de agente de máquina virtual que se ejecuta en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f675-120">hello VM Agent running on hello Azure Virtual Machine.</span></span>

<span data-ttu-id="3f675-121">En primer lugar, compruebe que Hola que ya está instalado el agente de máquina virtual en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f675-121">First, verify that hello VM Agent is already installed on hello virtual machine.</span></span> <span data-ttu-id="3f675-122">Rellene el nombre del servicio de nube de Hola y el nombre de la máquina virtual y, a continuación, ejecute hello siga los comandos en un símbolo de PowerShell de Azure de nivel de administrador.</span><span class="sxs-lookup"><span data-stu-id="3f675-122">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="3f675-123">Reemplace todo el contenido de las comillas de hello, incluidos los caracteres de Hola < y >.</span><span class="sxs-lookup"><span data-stu-id="3f675-123">Replace everything within hello quotes, including hello < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="3f675-124">Si no conoce el servicio de nube de Hola y nombres de máquina virtual, ejecute **Get-AzureVM** nombres de hello toolist para todas las máquinas virtuales en su suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="3f675-124">If you don't know hello cloud service and virtual machine names, run **Get-AzureVM** toolist hello names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="3f675-125">Si hello **escritura host** comando muestra **True**, Hola está instalado el agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f675-125">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="3f675-126">Si muestra **False**, consulte las instrucciones de Hola y un toohello vínculo Descargar en la entrada de blog de Azure de hello [agente de máquina virtual y extensiones: parte 2][Agent].</span><span class="sxs-lookup"><span data-stu-id="3f675-126">If it displays **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="3f675-127">Si está instalado Hola agente de máquina virtual, ejecútelo estos comandos tooinstall Hola Symantec Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="3f675-127">If hello VM Agent is installed, run these commands tooinstall hello Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="3f675-128">tooverify que Hola Symantec extensión de seguridad se ha instalado y está actualizada:</span><span class="sxs-lookup"><span data-stu-id="3f675-128">tooverify that hello Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="3f675-129">Inicie sesión en la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="3f675-129">Log on toohello virtual machine.</span></span> <span data-ttu-id="3f675-130">Para obtener instrucciones, consulte [cómo tooLog en la máquina Virtual que ejecuta Windows Server tooa][Logon].</span><span class="sxs-lookup"><span data-stu-id="3f675-130">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="3f675-131">Para Windows Server 2008 R2, haga clic en **Inicio > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="3f675-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="3f675-132">Para Windows Server 2012 o Windows Server 2012 R2, desde la pantalla de inicio de bienvenida, escriba **Symantec**y, a continuación, haga clic en **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="3f675-132">For Windows Server 2012 or Windows Server 2012 R2, from hello start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="3f675-133">De hello **estado** ficha de hello **estado Symantec Endpoint Protection** ventana, aplicar actualizaciones o reinicie si es necesario.</span><span class="sxs-lookup"><span data-stu-id="3f675-133">From hello **Status** tab of hello **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f675-134">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3f675-134">Additional resources</span></span>
<span data-ttu-id="3f675-135">[¿Cómo tooLog en tooa Máquina Virtual que ejecuta Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="3f675-135">[How tooLog on tooa Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="3f675-136">[Características y extensiones de máquina virtual de Azure][Ext]</span><span class="sxs-lookup"><span data-stu-id="3f675-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
