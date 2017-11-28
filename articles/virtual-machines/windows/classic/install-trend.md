---
title: "aaaInstall trendmicro Deep Security en una máquina virtual | Documentos de Microsoft"
description: "Este artículo se describe cómo tooinstall y configurar la seguridad de Trend Micro en una máquina virtual creada con el modelo de implementación clásica de hello en Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="8eab1-103">¿Cómo tooinstall y configurar trendmicro Deep Security como un servicio en una VM de Windows</span><span class="sxs-lookup"><span data-stu-id="8eab1-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8eab1-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8eab1-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8eab1-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="8eab1-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8eab1-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8eab1-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="8eab1-107">Este artículo muestra cómo tooinstall y configurar trendmicro Deep Security como un servicio en una existente o nueva máquina virtual (VM) con Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8eab1-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="8eab1-108">Deep Security como servicio proporciona protección antimalware, firewall, sistema de prevención contra intrusiones y supervisión de integridad.</span><span class="sxs-lookup"><span data-stu-id="8eab1-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="8eab1-109">Hola cliente se instala como una extensión de seguridad a través de hello agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8eab1-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="8eab1-110">En una nueva máquina virtual, instale Hola Deep Security Agent, como Hola que Hola portal de Azure crea automáticamente el agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8eab1-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="8eab1-111">Una máquina virtual existente que se creó mediante el portal clásico de hello, hello Azure CLI o PowerShell podría no tener un agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8eab1-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="8eab1-112">Para una máquina virtual existente que no tenga Hola agente de máquina virtual, es necesario toodownload y, a continuación, deberá instalarlo primero.</span><span class="sxs-lookup"><span data-stu-id="8eab1-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="8eab1-113">Este artículo trata ambas situaciones.</span><span class="sxs-lookup"><span data-stu-id="8eab1-113">This article covers both situations.</span></span>

<span data-ttu-id="8eab1-114">Si tiene una suscripción de Trend Micro actual para una solución local, se puede usar toohelp proteger máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="8eab1-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="8eab1-115">Si todavía no es cliente, puede suscribirse para una prueba.</span><span class="sxs-lookup"><span data-stu-id="8eab1-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="8eab1-116">Para obtener más información sobre esta solución, consulte Hola Trend Micro entrada de blog [Microsoft Azure VM Agent extensión para Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="8eab1-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="8eab1-117">Instalar Hola Deep Security Agent en una nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8eab1-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="8eab1-118">Hola [portal de Azure](http://portal.azure.com) le permite instalar la extensión de seguridad de Trend Micro hello cuando se usa una imagen de hello **Marketplace** máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="8eab1-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="8eab1-119">Si va a crear una única máquina virtual, usar el portal de hello es una protección de tooadd de manera sencilla de Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="8eab1-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="8eab1-120">Uso de una entrada de hello **Marketplace** abre un asistente que le ayuda a configura la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8eab1-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="8eab1-121">Usar hello **configuración** hoja, el tercer panel del Asistente para hello, tooinstall Hola extensión de seguridad de Trend Micro de Hola.</span><span class="sxs-lookup"><span data-stu-id="8eab1-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="8eab1-122">Para obtener instrucciones generales, vea [crear una máquina virtual que ejecuta Windows en el portal de Azure hello](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8eab1-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="8eab1-123">Al obtener toohello **configuración** Hola hoja del Asistente para hello, lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8eab1-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="8eab1-124">Haga clic en **extensiones**, a continuación, haga clic en **Agregar extensión** en panel siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="8eab1-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![Empezar a agregar la extensión de Hola][1]

2. <span data-ttu-id="8eab1-126">Seleccione **Deep Security Agent** en hello **nuevo recurso** panel.</span><span class="sxs-lookup"><span data-stu-id="8eab1-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="8eab1-127">En el panel de Deep Security Agent hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="8eab1-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![Identificar agente de Deep Security][2]

3. <span data-ttu-id="8eab1-129">Escriba hello **identificador del inquilino** y **contraseña de activación del inquilino** para extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8eab1-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="8eab1-130">Opcionalmente, puede especificar un **identificador de directiva de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="8eab1-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="8eab1-131">A continuación, haga clic en **Aceptar** cliente de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8eab1-131">Then, click **OK** tooadd hello client.</span></span>

   ![Proporcionar detalles de la extensión][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="8eab1-133">Instalar Hola Deep Security Agent en una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="8eab1-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="8eab1-134">agente de hello tooinstall en una máquina virtual existente, debe Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8eab1-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="8eab1-135">módulo de PowerShell de Azure de Hello, versión 0.8.2 o posterior, instalado en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="8eab1-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="8eab1-136">Puede comprobar la versión de PowerShell de Azure que ha instalado mediante Hola Hola **Get-Module azure | versión de formato de tabla** comando.</span><span class="sxs-lookup"><span data-stu-id="8eab1-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="8eab1-137">Para obtener instrucciones y una versión más reciente de toohello de vínculo, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8eab1-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="8eab1-138">Inicie sesión con suscripción de Azure de tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="8eab1-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="8eab1-139">Agente de VM instalado en la máquina virtual de destino de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="8eab1-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="8eab1-140">En primer lugar, compruebe que Hola que ya está instalado el agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8eab1-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="8eab1-141">Rellene el nombre del servicio de nube de Hola y el nombre de la máquina virtual y, a continuación, ejecute hello siga los comandos en un símbolo de PowerShell de Azure de nivel de administrador.</span><span class="sxs-lookup"><span data-stu-id="8eab1-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="8eab1-142">Reemplace todo el contenido de las comillas de hello, incluidos los caracteres de Hola < y >.</span><span class="sxs-lookup"><span data-stu-id="8eab1-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="8eab1-143">Si no conoce el servicio de nube de Hola y el nombre de la máquina virtual, ejecute **Get-AzureVM** toodisplay que Hola a información para todas las máquinas virtuales en su suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="8eab1-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="8eab1-144">Si hello **escritura host** comando devuelve **True**, Hola está instalado el agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8eab1-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="8eab1-145">Si devuelve **False**, consulte las instrucciones de Hola y un toohello vínculo Descargar en la entrada de blog de Azure de hello [agente de máquina virtual y extensiones: parte 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="8eab1-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="8eab1-146">Si está instalado Hola agente de máquina virtual, ejecute estos comandos.</span><span class="sxs-lookup"><span data-stu-id="8eab1-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="8eab1-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8eab1-147">Next steps</span></span>
<span data-ttu-id="8eab1-148">Se tarda unos minutos para hello agente toostart ejecutando cuando se instala.</span><span class="sxs-lookup"><span data-stu-id="8eab1-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="8eab1-149">Después de eso, necesita tooactivate Deep Security en la máquina virtual de Hola para poder ser administrado por un administrador de seguridad profundo.</span><span class="sxs-lookup"><span data-stu-id="8eab1-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="8eab1-150">Vea Hola siguientes artículos para obtener instrucciones adicionales:</span><span class="sxs-lookup"><span data-stu-id="8eab1-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="8eab1-151">Artículo de Trend sobre esta solución, [Instant-On Cloud Security for Microsoft Azure (Seguridad en la nube instantánea para Microsoft Azure)](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="8eab1-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="8eab1-152">A [script de Windows PowerShell de ejemplo](http://go.microsoft.com/fwlink/?LinkId=404100) máquina virtual de tooconfigure Hola</span><span class="sxs-lookup"><span data-stu-id="8eab1-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="8eab1-153">[Instrucciones](http://go.microsoft.com/fwlink/?LinkId=404099) de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="8eab1-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8eab1-154">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8eab1-154">Additional resources</span></span>
<span data-ttu-id="8eab1-155">[¿Cómo toolog en la máquina virtual de tooa ejecuta Windows Server]</span><span class="sxs-lookup"><span data-stu-id="8eab1-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="8eab1-156">[Características y extensiones de máquina virtual de Azure]</span><span class="sxs-lookup"><span data-stu-id="8eab1-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[¿Cómo toolog en la máquina virtual de tooa ejecuta Windows Server]:connect-logon.md
[Características y extensiones de máquina virtual de Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
