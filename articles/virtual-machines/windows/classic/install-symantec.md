---
title: "Instalación de Symantec Endpoint Protection en una máquina virtual Windows | Microsoft Docs"
description: "Aprenda a instalar y configurar la extensión de seguridad de Symantec Endpoint Protection en una máquina virtual de Azure nueva o existente creada con el modelo de implementación clásica."
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
ms.openlocfilehash: 1603ebc7ee3c29277f30fbb802bdd8205b92d648
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="0d9b9-103">Instalación y configuración de Endpoint Protection en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="0d9b9-103">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="0d9b9-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0d9b9-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0d9b9-105">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0d9b9-106">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="0d9b9-107">En este artículo se muestra cómo instalar y configurar el cliente Symantec Endpoint Protection en una máquina virtual existente con Windows Server.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-107">This article shows you how to install and configure the Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="0d9b9-108">Este es el cliente completo, que incluye servicios como protección contra virus y spyware, firewall y prevención de intrusiones.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="0d9b9-109">El cliente se instala como una extensión de seguridad usando el Agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-109">The client is installed as a security extension by using the VM Agent.</span></span>

<span data-ttu-id="0d9b9-110">Si tiene una suscripción existente de Symantec para una solución local, puede usarla para proteger sus máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it to protect your Azure virtual machines.</span></span> <span data-ttu-id="0d9b9-111">Si todavía no es cliente, puede suscribirse para una prueba.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="0d9b9-112">Para obtener más información sobre esta solución, consulte [Symantec Endpoint Protection en la plataforma de Microsoft Azure][Symantec].</span><span class="sxs-lookup"><span data-stu-id="0d9b9-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="0d9b9-113">Esta página también tiene vínculos a información de licencia e instrucciones para instalar el cliente si ya es un cliente de Symantec.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-113">This page also has links to licensing information and instructions for installing the client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="0d9b9-114">Instalación de Symantec Endpoint Protection en una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="0d9b9-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="0d9b9-115">Antes de comenzar, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0d9b9-115">Before you begin, you need the following:</span></span>

* <span data-ttu-id="0d9b9-116">El módulo Azure PowerShell, versión 0.8.2 o posteriores, en el equipo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-116">The Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="0d9b9-117">Puede comprobar la versión de Azure PowerShell que ha instalado con el comando **Get-Module azure | format-table version** .</span><span class="sxs-lookup"><span data-stu-id="0d9b9-117">You can check the version of Azure PowerShell that you have installed with the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="0d9b9-118">Para obtener instrucciones y un vínculo a la versión más reciente, consulte [Instalación y configuración de Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="0d9b9-118">For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="0d9b9-119">Inicie sesión en la suscripción de Azure mediante `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-119">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="0d9b9-120">El agente de máquina virtual que se ejecuta en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-120">The VM Agent running on the Azure Virtual Machine.</span></span>

<span data-ttu-id="0d9b9-121">En primer lugar, compruebe que el agente de máquina virtual ya está instalado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-121">First, verify that the VM Agent is already installed on the virtual machine.</span></span> <span data-ttu-id="0d9b9-122">Introduzca el nombre de servicio de nube y el nombre de la máquina virtual y, a continuación, ejecute los siguientes comandos en un símbolo de sistema de Azure PowerShell con nivel de administrador.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-122">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="0d9b9-123">Reemplace todo el contenido dentro de las comillas, incluidos los caracteres < y >.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-123">Replace everything within the quotes, including the < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="0d9b9-124">Si no conoce los nombres del servicio en la nube y de la máquina virtual, ejecute **Get-AzureVM** para mostrar los nombres de todas las máquinas virtuales de su suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-124">If you don't know the cloud service and virtual machine names, run **Get-AzureVM** to list the names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="0d9b9-125">Si el comando **write-host** muestra **True**, el agente de la máquina virtual está instalado.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-125">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="0d9b9-126">Si muestra **False**, consulte las instrucciones y un vínculo a la descarga en la publicación del blog de Azure [VM Agent and Extensions - Part 2 (Agente de máquina virtual extensiones: parte 2)][Agent].</span><span class="sxs-lookup"><span data-stu-id="0d9b9-126">If it displays **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="0d9b9-127">Si está instalado el agente de VM, ejecute estos comandos para instalar al agente de Symantec Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-127">If the VM Agent is installed, run these commands to install the Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="0d9b9-128">Para comprobar que la extensión de seguridad de Symantec se ha instalado y está actualizada:</span><span class="sxs-lookup"><span data-stu-id="0d9b9-128">To verify that the Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="0d9b9-129">Iniciar sesión en la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-129">Log on to the virtual machine.</span></span> <span data-ttu-id="0d9b9-130">Para obtener instrucciones, vea [Iniciar sesión en una máquina virtual con Windows Server][Logon].</span><span class="sxs-lookup"><span data-stu-id="0d9b9-130">For instructions, see [How to Log on to a Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="0d9b9-131">Para Windows Server 2008 R2, haga clic en **Inicio > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="0d9b9-132">Para Windows Server 2012 o Windows Server 2012 R2, en la pantalla de inicio, escriba **Symantec** y luego haga clic en **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-132">For Windows Server 2012 or Windows Server 2012 R2, from the start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="0d9b9-133">En la pestaña **Estado** de la ventana **Status-Symantec Endpoint Protection**, aplique actualizaciones o reinicie en caso necesario.</span><span class="sxs-lookup"><span data-stu-id="0d9b9-133">From the **Status** tab of the **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d9b9-134">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0d9b9-134">Additional resources</span></span>
<span data-ttu-id="0d9b9-135">[Inicio de sesión en una máquina virtual con Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="0d9b9-135">[How to Log on to a Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="0d9b9-136">[Características y extensiones de máquina virtual de Azure][Ext]</span><span class="sxs-lookup"><span data-stu-id="0d9b9-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
