---
title: "planes de toorecovery de runbooks de automatización de Azure de aaaAdd en el portal clásico de hello | Documentos de Microsoft"
description: "Este artículo describe cómo Azure Site Recovery ahora permite tooextend planes de recuperación mediante tareas de automatización de Azure toocomplete complejas durante la recuperación tooAzure"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a><span data-ttu-id="f5423-103">Agregar planes de toorecovery de runbooks de automatización de Azure en el portal clásico de Hola</span><span class="sxs-lookup"><span data-stu-id="f5423-103">Add Azure automation runbooks toorecovery plans in hello classic portal</span></span>
<span data-ttu-id="f5423-104">Este tutorial describe cómo se integra Azure Site Recovery con automatización de Azure tooprovide extensibilidad toorecovery planes.</span><span class="sxs-lookup"><span data-stu-id="f5423-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation tooprovide extensibility toorecovery plans.</span></span> <span data-ttu-id="f5423-105">Planes de recuperación pueden coordinar la recuperación de las máquinas virtuales protegidos con Azure Site Recovery para la nube de toosecondary de replicación y los escenarios de replicación tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f5423-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication toosecondary cloud and replication tooAzure scenarios.</span></span> <span data-ttu-id="f5423-106">También ayudan a realizar la recuperación de hello **coherentes y precisos**, **repetible**, y **automatizada**.</span><span class="sxs-lookup"><span data-stu-id="f5423-106">They also help in making hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="f5423-107">Si conmuta por error el tooAzure de máquinas virtuales, integración con automatización de Azure extiende los planes de recuperación y proporciona capacidad tooexecute runbooks, por lo que las tareas de automatización eficaz.</span><span class="sxs-lookup"><span data-stu-id="f5423-107">If you are failing over your virtual machines tooAzure, integration with Azure Automation extends the recovery plans and gives you capability tooexecute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="f5423-108">Si aún no ha oído hablar de Azure Automation, suscríbase [aquí](https://azure.microsoft.com/services/automation/) y descargue sus scripts de ejemplo [aquí](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="f5423-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="f5423-109">Obtenga más información sobre [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) y cómo tiene previsto tooorchestrate tooAzure de recuperación mediante la recuperación de [aquí](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="f5423-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how tooorchestrate recovery tooAzure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="f5423-110">En este breve tutorial, veremos cómo se pueden integrar runbooks de Azure Automation en planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="f5423-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="f5423-111">Agregaremos información automatizar tareas sencillas que anteriormente requerían la intervención manual y vea cómo tooconvert un múltiples recuperación paso a paso una acción de recuperación con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="f5423-111">We will automate simple tasks that earlier required manual intervention and see how tooconvert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="f5423-112">También veremos cómo puede solucionar problemas de un script sencillo si algo va mal.</span><span class="sxs-lookup"><span data-stu-id="f5423-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-hello-application-tooazure"></a><span data-ttu-id="f5423-113">Proteger Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="f5423-113">Protect hello application tooAzure</span></span>
<span data-ttu-id="f5423-114">Comenzaremos con una aplicación simple que consta de dos máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f5423-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="f5423-115">En este caso, tenemos una aplicación HRweb de Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="f5423-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="f5423-116">Servidor front-end de HRweb Fabrikam y Fabrikam-Hrweb-back-end están protegidos con dos máquinas virtuales que hello tooAzure con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f5423-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are hello two virtual machines protected tooAzure using Azure Site Recovery.</span></span> <span data-ttu-id="f5423-117">máquinas virtuales tooprotect Hola que con Azure Site Recovery, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="f5423-117">tooprotect hello virtual machines using Azure Site Recovery, follow hello steps below.</span></span>

1. <span data-ttu-id="f5423-118">Habilite la protección para las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f5423-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="f5423-119">Asegúrese de que las máquinas virtuales Hola ha completado la replicación inicial y se replica.</span><span class="sxs-lookup"><span data-stu-id="f5423-119">Ensure that hello virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="f5423-120">Espere a que finalice la replicación inicial de Hola y Hola estado de replicación dice protegidos.</span><span class="sxs-lookup"><span data-stu-id="f5423-120">Wait till hello initial replication completes and hello Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="f5423-121">En este tutorial, se creará un plan de recuperación para hello Fabrikam HRweb aplicación toofailover Hola aplicación tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f5423-121">In this tutorial, we will create a recovery plan for hello Fabrikam HRweb application toofailover hello application tooAzure.</span></span> <span data-ttu-id="f5423-122">A continuación, se integrará con un runbook que va a crear un punto de conexión en hello conmutado por páginas de web tooserve de máquina virtual de Azure en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="f5423-122">Then we will integrate it with a runbook that will create an endpoint on hello failed over Azure virtual machine tooserve web pages at port 80.</span></span>

<span data-ttu-id="f5423-123">En primer lugar, vamos a crear un plan de recuperación para nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5423-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-hello-recovery-plan"></a><span data-ttu-id="f5423-124">Crear plan de recuperación de Hola</span><span class="sxs-lookup"><span data-stu-id="f5423-124">Create hello recovery plan</span></span>
<span data-ttu-id="f5423-125">toorecover Hola aplicación tooAzure, deberá toocreate un plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="f5423-125">toorecover hello application tooAzure, you need toocreate a recovery plan.</span></span>
<span data-ttu-id="f5423-126">Uso de un plan de recuperación, puede especificar el orden de Hola de recuperación de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f5423-126">Using a recovery plan you can specify hello order of recovery of the virtual machines.</span></span> <span data-ttu-id="f5423-127">máquina virtual de Hello colocado en el grupo 1 se recuperar e inicie primero y, a continuación, seguirá la máquina virtual de hello en el grupo 2.</span><span class="sxs-lookup"><span data-stu-id="f5423-127">hello virtual machine placed in group 1 will recover and start first, and then hello virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="f5423-128">Crear un plan de recuperación como el siguiente.</span><span class="sxs-lookup"><span data-stu-id="f5423-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="f5423-129">más información acerca de los planes de recuperación, lea la documentación de tooread [aquí](https://msdn.microsoft.com/library/azure/dn788799.aspx "aquí").</span><span class="sxs-lookup"><span data-stu-id="f5423-129">tooread more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="f5423-130">A continuación, vamos a crear Hola artefactos necesarios en la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5423-130">Next, let's create hello necessary artifacts in Azure Automation.</span></span>

## <a name="create-hello-automation-account-and-its-assets"></a><span data-ttu-id="f5423-131">Crear cuenta de automatización de Hola y de sus activos</span><span class="sxs-lookup"><span data-stu-id="f5423-131">Create hello automation account and its assets</span></span>
<span data-ttu-id="f5423-132">Es necesario un runbooks toocreate de cuenta de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5423-132">You need an Azure Automation account toocreate runbooks.</span></span> <span data-ttu-id="f5423-133">Si no dispone de una cuenta, vaya pestaña de automatización tooAzure denotado por ![](media/site-recovery-runbook-automation/02.png)y crear una nueva cuenta.</span><span class="sxs-lookup"><span data-stu-id="f5423-133">If you do not already have an account, navigate tooAzure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="f5423-134">Conceda a cuenta de hello un tooidentify nombre con.</span><span class="sxs-lookup"><span data-stu-id="f5423-134">Give hello account a name tooidentify with.</span></span>
2. <span data-ttu-id="f5423-135">Especifique una región geográfica donde desea que la cuenta de hello tooplace.</span><span class="sxs-lookup"><span data-stu-id="f5423-135">Specify a geographical region where you want tooplace hello account.</span></span>

<span data-ttu-id="f5423-136">Se recomienda tooplace cuenta de hello en hello misma región que el almacén de hello ASR.</span><span class="sxs-lookup"><span data-stu-id="f5423-136">It is recommended tooplace hello account in hello same region as hello ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="f5423-137">A continuación, cree Hola después activos en hello cuenta.</span><span class="sxs-lookup"><span data-stu-id="f5423-137">Next, create hello following assets in hello Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="f5423-138">Incorporación de un nombre de suscripción como activo</span><span class="sxs-lookup"><span data-stu-id="f5423-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="f5423-139">Agregar una nueva configuración ![](media/site-recovery-runbook-automation/04.png) en Hola activos de automatización de Azure y seleccione demasiado![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="f5423-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select too![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="f5423-140">Seleccione el tipo de variable de hello como **cadena**</span><span class="sxs-lookup"><span data-stu-id="f5423-140">Select hello variable type as **String**</span></span>
3. <span data-ttu-id="f5423-141">Especifique el nombre de la variable como **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="f5423-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="f5423-142">Especifique el nombre real de la suscripción de Azure como valor de la variable Hola.</span><span class="sxs-lookup"><span data-stu-id="f5423-142">Specify your actual Azure Subscription name as hello variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="f5423-143">Puede identificar el nombre hello de su suscripción desde la página de configuración de Hola de su cuenta en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5423-143">You can identify hello name of your subscription from hello settings page of your account on hello Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="f5423-144">Incorporación de una credencial de inicio de sesión de Azure como activo</span><span class="sxs-lookup"><span data-stu-id="f5423-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="f5423-145">Automatización de Azure usa la suscripción de Azure PowerShell tooconnect toothe y funciona en los artefactos de hello no existe.</span><span class="sxs-lookup"><span data-stu-id="f5423-145">Azure Automation uses Azure PowerShell tooconnect toothe subscription and operates on hello artifacts there.</span></span> <span data-ttu-id="f5423-146">Para ello, deberá autenticarse con su cuenta de Microsoft o una cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="f5423-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="f5423-147">Puede almacenar las credenciales de cuenta de hello en un toobe asset utilizado de manera segura por runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="f5423-147">You can store hello account credentials in an asset toobe used securely by hello runbook.</span></span>

1. <span data-ttu-id="f5423-148">Agregar una nueva configuración ![](media/site-recovery-runbook-automation/04.png) en Hola activos de automatización de Azure y seleccione![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="f5423-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="f5423-149">Seleccione el tipo de credencial de hello como **credenciales de Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="f5423-149">Select hello Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="f5423-150">Especificar nombre de hello como **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="f5423-150">Specify hello name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="f5423-151">Especifique Hola username y password toosign en con.</span><span class="sxs-lookup"><span data-stu-id="f5423-151">Specify hello username and password toosign-in with.</span></span>

<span data-ttu-id="f5423-152">Ahora ambas configuraciones están disponibles en los activos.</span><span class="sxs-lookup"><span data-stu-id="f5423-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="f5423-153">Para obtener más información acerca de cómo se proporciona tooconnect tooyour suscripción a través de PowerShell [aquí](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f5423-153">More information about how tooconnect tooyour subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="f5423-154">A continuación, creará un runbook en automatización de Azure que puede agregar un punto de conexión de máquina virtual de front-end Hola después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="f5423-154">Next, you will create a runbook in Azure Automation that can add an endpoint for hello front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="f5423-155">Contexto de automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="f5423-155">Azure automation context</span></span>
<span data-ttu-id="f5423-156">ASR pasa un toohelp de runbook de contexto toohello variable escribir scripts deterministas.</span><span class="sxs-lookup"><span data-stu-id="f5423-156">ASR passes a context variable toohello runbook toohelp you write deterministic scripts.</span></span> <span data-ttu-id="f5423-157">Uno podría argumentar que los nombres de Hola de servicio en la nube de Hola y Hola Máquina Virtual son predecibles, pero no ocurre que no siempre es caso Hola poseer toocertain escenarios como Hola uno donde podría haber cambiado el nombre de hello del nombre de la máquina virtual de hello debido caracteres de toounsupported en Azure.</span><span class="sxs-lookup"><span data-stu-id="f5423-157">One could argue that hello names of hello Cloud Service and hello Virtual Machine are predictable, but happens that it is not always hello case owing toocertain scenarios such as hello one where hello name of hello virtual machine name might have changed due toounsupported characters in Azure.</span></span> <span data-ttu-id="f5423-158">Por lo tanto, esta información se pasa el plan de recuperación de toohello ASR como parte del programa Hola a *contexto*.</span><span class="sxs-lookup"><span data-stu-id="f5423-158">Hence this information is passed toohello ASR recovery plan as part of hello *context*.</span></span>

<span data-ttu-id="f5423-159">A continuación se muestra un ejemplo del aspecto de la variable de contexto de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5423-159">Below is an example of how hello context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="f5423-160">tabla de Hello siguiente contiene el nombre y una descripción para cada variable de contexto de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5423-160">hello table below contains name and description for each variable in hello context.</span></span>

| <span data-ttu-id="f5423-161">**Nombre de la variable**</span><span class="sxs-lookup"><span data-stu-id="f5423-161">**Variable name**</span></span> | <span data-ttu-id="f5423-162">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="f5423-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f5423-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="f5423-163">RecoveryPlanName</span></span> |<span data-ttu-id="f5423-164">Nombre del plan que se va a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="f5423-164">Name of plan being run.</span></span> <span data-ttu-id="f5423-165">Ayuda a realizar acciones en función de nombre usando Hola mismo script</span><span class="sxs-lookup"><span data-stu-id="f5423-165">Helps you take action based on name using hello same script</span></span> |
| <span data-ttu-id="f5423-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="f5423-166">FailoverType</span></span> |<span data-ttu-id="f5423-167">Especifica si se prueba Hola conmutación por error, planeada o no planeada.</span><span class="sxs-lookup"><span data-stu-id="f5423-167">Specifies whether hello failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="f5423-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="f5423-168">FailoverDirection</span></span> |<span data-ttu-id="f5423-169">Especifique si la recuperación es tooprimary o base de datos secundaria</span><span class="sxs-lookup"><span data-stu-id="f5423-169">Specify whether recovery is tooprimary or secondary</span></span> |
| <span data-ttu-id="f5423-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="f5423-170">GroupID</span></span> |<span data-ttu-id="f5423-171">Identifique el número de grupo de hello en el plan de recuperación de hello cuando se ejecuta el plan de Hola</span><span class="sxs-lookup"><span data-stu-id="f5423-171">Identify hello group number within hello recovery plan when hello plan is running</span></span> |
| <span data-ttu-id="f5423-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="f5423-172">VmMap</span></span> |<span data-ttu-id="f5423-173">Matriz de todas las máquinas virtuales de hello en el grupo de Hola</span><span class="sxs-lookup"><span data-stu-id="f5423-173">Array of all hello virtual machines in hello group</span></span> |
| <span data-ttu-id="f5423-174">Clave de VMMap</span><span class="sxs-lookup"><span data-stu-id="f5423-174">VMMap key</span></span> |<span data-ttu-id="f5423-175">Clave única (GUID) para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f5423-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="f5423-176">Ha Hola igual que Hola Id. de máquina virtual de Hola de VMM, si procede.</span><span class="sxs-lookup"><span data-stu-id="f5423-176">It's hello same as hello VMM ID of hello virtual machine where applicable.</span></span> |
| <span data-ttu-id="f5423-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="f5423-177">RoleName</span></span> |<span data-ttu-id="f5423-178">Nombre de máquina virtual de Azure que se va a recuperar de hello</span><span class="sxs-lookup"><span data-stu-id="f5423-178">Name of hello Azure VM that's being recovered</span></span> |
| <span data-ttu-id="f5423-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="f5423-179">CloudServiceName</span></span> |<span data-ttu-id="f5423-180">Nombre de servicio en la nube Azure bajo qué Hola se crea la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f5423-180">Azure Cloud Service name under which hello virtual machine is created.</span></span> |

<span data-ttu-id="f5423-181">Hola de tooidentify VmMap Key en el contexto de hello también puede ir a página de propiedades de máquina virtual de toohello en ASR y mire Hola propiedad VM GUID.</span><span class="sxs-lookup"><span data-stu-id="f5423-181">tooidentify hello VmMap Key in hello context you could also go toohello VM properties page in ASR and look at hello VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="f5423-182">Creación de un runbook de Automatización</span><span class="sxs-lookup"><span data-stu-id="f5423-182">Author an Automation runbook</span></span>
<span data-ttu-id="f5423-183">Ahora cree tooopen puerto 80 de hello runbook en la máquina virtual de front-end Hola.</span><span class="sxs-lookup"><span data-stu-id="f5423-183">Now create hello runbook tooopen port 80 on hello front-end virtual machine.</span></span>

1. <span data-ttu-id="f5423-184">Crear un nuevo runbook en la cuenta de automatización de Azure con el nombre de Hola Hola **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="f5423-184">Create a new runbook in hello Azure Automation account with hello name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="f5423-185">Navegue toohello vista autor de runbook de Hola y entrar en modo de borrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5423-185">Navigate toohello Author view of hello runbook and enter hello draft mode.</span></span>
3. <span data-ttu-id="f5423-186">Especifique primero toouse variable hello como contexto de plan de recuperación de Hola</span><span class="sxs-lookup"><span data-stu-id="f5423-186">First specify hello variable toouse as hello recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="f5423-187">A continuación conectar suscripción toohello con nombre de credencial y la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="f5423-187">Next connect toohello subscription using hello credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="f5423-188">Tenga en cuenta que usar hello Azure activos: **AzureCredential** y **AzureSubscriptionName** aquí.</span><span class="sxs-lookup"><span data-stu-id="f5423-188">Note that you use hello Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="f5423-189">Ahora, especifique los detalles de punto de conexión de Hola y Hola GUID de la máquina virtual de hello para el que desea que el punto de conexión de tooexpose Hola.</span><span class="sxs-lookup"><span data-stu-id="f5423-189">Now specify hello endpoint details and hello GUID of hello virtual machine for which you want tooexpose hello endpoint.</span></span> <span data-ttu-id="f5423-190">En esta máquina virtual front-end de hello mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="f5423-190">In this case hello front-end virtual machine.</span></span>

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="f5423-191">Esto especifica Hola protocolo de extremo de Azure, puerto local en hello VM y su puerto público asignada.</span><span class="sxs-lookup"><span data-stu-id="f5423-191">This specifies hello Azure endpoint protocol, local port on hello VM and its mapped public port.</span></span> <span data-ttu-id="f5423-192">Estas variables son parámetros requieren por hello Azure comandos que agregue tooVMs de puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="f5423-192">These variables are parameters     required by hello Azure commands that add endpoints tooVMs.</span></span> <span data-ttu-id="f5423-193">Hola VMGUID contiene Hola GUID de la máquina virtual de hello en que necesita toooperate.</span><span class="sxs-lookup"><span data-stu-id="f5423-193">hello VMGUID holds hello GUID of hello virtual machine you need toooperate on.</span></span>
6. <span data-ttu-id="f5423-194">script de Hola ahora extraer contexto Hola para hello tiene el GUID de la VM y crear un punto de conexión en la máquina virtual de hello hace referencia a él.</span><span class="sxs-lookup"><span data-stu-id="f5423-194">hello script will now extract hello context for hello given VM GUID and create an endpoint on hello virtual machine referenced by it.</span></span>

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="f5423-195">Una vez completado, publicación de aciertos ![](media/site-recovery-runbook-automation/20.png) tooallow su toobe de secuencia de comandos disponible para su ejecución.</span><span class="sxs-lookup"><span data-stu-id="f5423-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) tooallow your script toobe available for execution.</span></span>

<span data-ttu-id="f5423-196">secuencia de comandos completa Hola se indica a continuación para su referencia</span><span class="sxs-lookup"><span data-stu-id="f5423-196">hello complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a><span data-ttu-id="f5423-197">Agregar plan de recuperación de hello script toohello</span><span class="sxs-lookup"><span data-stu-id="f5423-197">Add hello script toohello recovery plan</span></span>
<span data-ttu-id="f5423-198">Una vez que el script de Hola esté listo, puede agregarlo toohello plan de recuperación que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f5423-198">Once hello script is ready, you can add it toohello recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="f5423-199">En el plan de recuperación de Hola que ha creado, elija tooadd una secuencia de comandos después del grupo 2.</span><span class="sxs-lookup"><span data-stu-id="f5423-199">In hello recovery plan you created, choose tooadd a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="f5423-200">Especifique un nombre de script.</span><span class="sxs-lookup"><span data-stu-id="f5423-200">Specify a script name.</span></span> <span data-ttu-id="f5423-201">Esto es simplemente un nombre descriptivo para esta secuencia de comandos para que se muestra en el plan de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5423-201">This is just a friendly name for this script for showing within hello Recovery plan.</span></span>
3. <span data-ttu-id="f5423-202">En secuencias de comandos de tooAzure de conmutación por error de hello: seleccione el nombre de cuenta de automatización de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5423-202">In hello failover tooAzure script – Select hello Azure Automation Account name.</span></span>
4. <span data-ttu-id="f5423-203">Hola Runbooks de Azure, seleccione runbook Hola que crearon.</span><span class="sxs-lookup"><span data-stu-id="f5423-203">In hello Azure Runbooks, select hello runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="f5423-204">Scripts principales</span><span class="sxs-lookup"><span data-stu-id="f5423-204">Primary side scripts</span></span>
<span data-ttu-id="f5423-205">Cuando se está ejecutando un tooAzure de conmutación por error, también puede elegir tooexecute secuencias de comandos principal.</span><span class="sxs-lookup"><span data-stu-id="f5423-205">When you are executing a failover tooAzure, you can also choose tooexecute primary side scripts.</span></span> <span data-ttu-id="f5423-206">Estas secuencias de comandos se ejecutarán en el servidor VMM de Hola durante la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="f5423-206">These scripts will run on hello VMM server during failover.</span></span>
<span data-ttu-id="f5423-207">Los scripts principales solo están disponibles solo para las fases de preapagado y postapagado.</span><span class="sxs-lookup"><span data-stu-id="f5423-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="f5423-208">Esto es porque esperamos Hola sitio primario toobe normalmente no está disponible cuando se produzca un desastre.</span><span class="sxs-lookup"><span data-stu-id="f5423-208">This is because we expect hello primary site toobe typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="f5423-209">Durante una conmutación por error no planeada, solo si decide no participar en para las operaciones del sitio primario, tratará de scripts del lado principal de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="f5423-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt toorun hello primary side scripts.</span></span> <span data-ttu-id="f5423-210">Si no son accesibles o tiempo de espera, conmutación por error de hello continuará toorecover Hola máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f5423-210">If they are not reachable or timeout, hello failover will continue toorecover hello virtual machines.</span></span>
<span data-ttu-id="f5423-211">Secuencias de comandos principales están sin disponibles para sitios de VMware/físicas/Hyper-v sin tooAzure VMM protegido - mientras se tooAzure de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="f5423-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected tooAzure - while you failover tooAzure.</span></span>
<span data-ttu-id="f5423-212">Sin embargo, cuando se conmutación por recuperación de tooon locales de Azure, secuencias de comandos principal (Runbooks) puede utilizarse para todos los destinos excepto VMware.</span><span class="sxs-lookup"><span data-stu-id="f5423-212">However, when you failback from Azure tooon-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-hello-recovery-plan"></a><span data-ttu-id="f5423-213">Plan de recuperación de Hola de prueba</span><span class="sxs-lookup"><span data-stu-id="f5423-213">Test hello recovery plan</span></span>
<span data-ttu-id="f5423-214">Cuando haya agregado el plan de hello runbook toohello puede iniciar una conmutación por error de prueba y verlo en acción.</span><span class="sxs-lookup"><span data-stu-id="f5423-214">Once you have added hello runbook toohello plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="f5423-215">Siempre es recomendable toorun un tootest de conmutación por error de prueba de su plan de recuperación, hello y aplicación, tooensure que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="f5423-215">It is always recommended toorun a test failover tootest your application and hello recovery plan tooensure that there are no errors.</span></span>

1. <span data-ttu-id="f5423-216">Seleccione el plan de recuperación de hello e iniciar una conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="f5423-216">Select hello recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="f5423-217">Durante la ejecución del plan de hello, puede ver si ha ejecutado runbook Hola o no a través de su estado.</span><span class="sxs-lookup"><span data-stu-id="f5423-217">During hello plan execution, you can see whether hello runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="f5423-218">También puede ver Hola el estado de ejecución de runbook en la página de trabajos de automatización de Azure Hola Hola runbook detallado.</span><span class="sxs-lookup"><span data-stu-id="f5423-218">You can also see hello detailed runbook execution status on hello Azure Automation jobs page for hello runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="f5423-219">Una vez completada la conmutación por error de hello, además de resultado de la ejecución de runbook de hello, puede ver si la ejecución de hello es correcta o no por visitar la página de la máquina virtual de Azure de Hola y examinando los puntos de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5423-219">After hello failover completes, apart from hello runbook execution result, you can see whether hello execution is successful or not by visiting hello Azure virtual machine page and looking at hello endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="f5423-220">Scripts de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f5423-220">Sample scripts</span></span>
<span data-ttu-id="f5423-221">Mientras se pasará a través de automatizar uno normalmente utiliza la tarea de agregar una máquina virtual de Azure de extremo tooan en este tutorial, se podría hacer que un número de otras tareas de automatización eficaz mediante la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5423-221">While we walked through automating one commonly used task of adding an endpoint tooan Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="f5423-222">Microsoft y Hola Comunidad de automatización de Azure proporcionan runbooks de ejemplo que puede ayudarle a empezar a crear sus propias soluciones y runbooks de utilidad, que puede utilizar como bloques de creación para las tareas de automatización más grandes.</span><span class="sxs-lookup"><span data-stu-id="f5423-222">Microsoft and hello Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="f5423-223">Comenzar a usarlos de galería de Hola y generar planes de recuperación de un solo clic eficaz para las aplicaciones con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f5423-223">Start using them from hello gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5423-224">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f5423-224">Additional Resources</span></span>
[<span data-ttu-id="f5423-225">Información general sobre Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="f5423-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Información general sobre Automatización de Azure")

[<span data-ttu-id="f5423-226">Scripts de Automatización de Azure de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f5423-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Scripts de Automatización de Azure de ejemplo")
