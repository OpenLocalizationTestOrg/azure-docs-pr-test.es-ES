---
title: "registros de aaaIntegrate desde el almacén de claves de Azure mediante el uso de los centros de eventos | Documentos de Microsoft"
description: "Tutorial que proporciona los pasos necesarios de hello toomake almacén de claves de registros disponible tooa SIEM mediante la integración de registro de Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="13b0e-103">Tutorial de integración de registros de Azure: Procesamiento de eventos de Azure Key Vault mediante Event Hubs</span><span class="sxs-lookup"><span data-stu-id="13b0e-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="13b0e-104">Puede usar eventos de integración de Azure Log tooretrieve iniciado y que estén en el sistema de administración (SIEM) de eventos e información de seguridad de tooyour disponible.</span><span class="sxs-lookup"><span data-stu-id="13b0e-104">You can use Azure Log Integration tooretrieve logged events and make them available tooyour security information and event management (SIEM) system.</span></span> <span data-ttu-id="13b0e-105">Este tutorial muestra un ejemplo de cómo integración de registro de Azure puede ser usado tooprocess registros adquiridos a través de los centros de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="13b0e-105">This tutorial shows an example of how Azure Log Integration can be used tooprocess logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="13b0e-106">Use este tutorial tooget familiarizará con la integración de registro de Azure y concentradores de eventos trabajo juntos siguiendo Hola ejemplos paso a paso y entender cómo cada paso es compatible con la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="13b0e-106">Use this tutorial tooget acquainted with how Azure Log Integration and Event Hubs work together by following hello example steps and understanding how each step supports hello solution.</span></span> <span data-ttu-id="13b0e-107">A continuación, puede realizarlo que ha aprendido aquí toocreate su propios pasos toosupport requisitos únicos de su empresa.</span><span class="sxs-lookup"><span data-stu-id="13b0e-107">Then you can take what you’ve learned here toocreate your own steps toosupport your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="13b0e-108">pasos de Hola y comandos en este tutorial no son toobe previsto copiado y pegado.</span><span class="sxs-lookup"><span data-stu-id="13b0e-108">hello steps and commands in this tutorial are not intended toobe copied and pasted.</span></span> <span data-ttu-id="13b0e-109">Tan solo son ejemplos.</span><span class="sxs-lookup"><span data-stu-id="13b0e-109">They're examples only.</span></span> <span data-ttu-id="13b0e-110">No use comandos de PowerShell de Hola "tal cual" en el entorno activo.</span><span class="sxs-lookup"><span data-stu-id="13b0e-110">Do not use hello PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="13b0e-111">Deben personalizarse en función del entorno específico.</span><span class="sxs-lookup"><span data-stu-id="13b0e-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="13b0e-112">Este tutorial le guiará por el proceso de Hola de tomar concentrador de eventos de almacén de claves de Azure actividad tooan registrado y ponerlo a disposición como sistema JSON archivos tooyour SIEM.</span><span class="sxs-lookup"><span data-stu-id="13b0e-112">This tutorial walks you through hello process of taking Azure Key Vault activity logged tooan event hub and making it available as JSON files tooyour SIEM system.</span></span> <span data-ttu-id="13b0e-113">A continuación, puede configurar los archivos JSON de SIEM sistema tooprocess Hola.</span><span class="sxs-lookup"><span data-stu-id="13b0e-113">You can then configure your SIEM system tooprocess hello JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="13b0e-114">La mayoría de los pasos de hello en este tutorial implica la configuración de almacenes de claves, las cuentas de almacenamiento y los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="13b0e-114">Most of hello steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="13b0e-115">pasos de integración de Azure registro específicos de Hello son final Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="13b0e-115">hello specific Azure Log Integration steps are at hello end of this tutorial.</span></span> <span data-ttu-id="13b0e-116">No realice estos pasos en un entorno de producción,</span><span class="sxs-lookup"><span data-stu-id="13b0e-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="13b0e-117">ya que se han diseñado exclusivamente para un entorno de laboratorio.</span><span class="sxs-lookup"><span data-stu-id="13b0e-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="13b0e-118">Debe personalizar los pasos de hello antes de usarlos en producción.</span><span class="sxs-lookup"><span data-stu-id="13b0e-118">You must customize hello steps before using them in production.</span></span>

<span data-ttu-id="13b0e-119">Proporciona información a lo largo de la manera de hello le ayuda a que comprender los motivos de hello detrás de cada paso.</span><span class="sxs-lookup"><span data-stu-id="13b0e-119">Information provided along hello way helps you understand hello reasons behind each step.</span></span> <span data-ttu-id="13b0e-120">Artículos de tooother vínculos ofrecen más detalles sobre determinados temas.</span><span class="sxs-lookup"><span data-stu-id="13b0e-120">Links tooother articles give you more detail on certain topics.</span></span>

<span data-ttu-id="13b0e-121">Para obtener más información acerca de los servicios de Hola que se mencione en este tutorial, vea:</span><span class="sxs-lookup"><span data-stu-id="13b0e-121">For more information about hello services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="13b0e-122">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="13b0e-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="13b0e-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="13b0e-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="13b0e-124">Integración de registros de Azure</span><span class="sxs-lookup"><span data-stu-id="13b0e-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="13b0e-125">Configuración inicial</span><span class="sxs-lookup"><span data-stu-id="13b0e-125">Initial setup</span></span>

<span data-ttu-id="13b0e-126">Para poder completar los pasos de hello en este artículo, necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="13b0e-126">Before you can complete hello steps in this article, you need hello following:</span></span>

1. <span data-ttu-id="13b0e-127">Una suscripción de Azure y una cuenta en esa suscripción con derechos de administrador.</span><span class="sxs-lookup"><span data-stu-id="13b0e-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="13b0e-128">Si no tiene una suscripción, puede crear [una cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="13b0e-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="13b0e-129">Un sistema con toohello de acceso a internet que cumpla los requisitos de hello para la instalación de integración de registro de Azure.</span><span class="sxs-lookup"><span data-stu-id="13b0e-129">A system with access toohello internet that meets hello requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="13b0e-130">sistema de Hello puede estar en un servicio de nube u hospedado en local.</span><span class="sxs-lookup"><span data-stu-id="13b0e-130">hello system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="13b0e-131">La [integración de registros de Azure](https://www.microsoft.com/download/details.aspx?id=53324) instalada.</span><span class="sxs-lookup"><span data-stu-id="13b0e-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="13b0e-132">tooinstall:</span><span class="sxs-lookup"><span data-stu-id="13b0e-132">tooinstall it:</span></span>

   <span data-ttu-id="13b0e-133">a.</span><span class="sxs-lookup"><span data-stu-id="13b0e-133">a.</span></span> <span data-ttu-id="13b0e-134">Usar Escritorio remoto tooconnect toohello sistema mencionado en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="13b0e-134">Use Remote Desktop tooconnect toohello system mentioned in step 2.</span></span>   
   <span data-ttu-id="13b0e-135">b.</span><span class="sxs-lookup"><span data-stu-id="13b0e-135">b.</span></span> <span data-ttu-id="13b0e-136">Copie el sistema de toohello de instalador de integración de Azure registro de hello.</span><span class="sxs-lookup"><span data-stu-id="13b0e-136">Copy hello Azure Log Integration installer toohello system.</span></span> <span data-ttu-id="13b0e-137">También puede [descargar archivos de instalación de hello](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="13b0e-137">You can [download hello installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="13b0e-138">c.</span><span class="sxs-lookup"><span data-stu-id="13b0e-138">c.</span></span> <span data-ttu-id="13b0e-139">Inicie al instalador de Hola y acepte los términos de licencia del Software de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="13b0e-139">Start hello installer and accept hello Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="13b0e-140">d.</span><span class="sxs-lookup"><span data-stu-id="13b0e-140">d.</span></span> <span data-ttu-id="13b0e-141">Si va a proporcionar información de telemetría, deje activada la casilla de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="13b0e-141">If you will provide telemetry information, leave hello check box selected.</span></span> <span data-ttu-id="13b0e-142">Si en su lugar enviaría no tooMicrosoft de información de uso, desactive la casilla de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="13b0e-142">If you'd rather not send usage information tooMicrosoft, clear hello check box.</span></span>
   
   <span data-ttu-id="13b0e-143">Para obtener más información acerca de la integración de registro de Azure y cómo tooinstall, consulte [integración de registro de Azure con el registro de diagnósticos de Azure y reenvío de eventos de Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="13b0e-143">For more information about Azure Log Integration and how tooinstall it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="13b0e-144">versión de PowerShell de Hello más reciente.</span><span class="sxs-lookup"><span data-stu-id="13b0e-144">hello latest PowerShell version.</span></span>
 
   <span data-ttu-id="13b0e-145">Si tiene instalado Windows Server 2016, entonces tiene al menos PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="13b0e-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="13b0e-146">Si usa otra versión de Windows Server, es posible que tenga instalada una versión anterior de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13b0e-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="13b0e-147">Puede comprobar la versión de Hola escribiendo ```get-host``` en una ventana de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13b0e-147">You can check hello version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="13b0e-148">Si no tiene PowerShell 5.0 instalado, puede [descargarlo](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="13b0e-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="13b0e-149">Una vez haya al menos PowerShell 5.0, puede continuar la versión más reciente de Hola tooinstall:</span><span class="sxs-lookup"><span data-stu-id="13b0e-149">After you have at least PowerShell 5.0, you can proceed tooinstall hello latest version:</span></span>
   
   <span data-ttu-id="13b0e-150">a.</span><span class="sxs-lookup"><span data-stu-id="13b0e-150">a.</span></span> <span data-ttu-id="13b0e-151">En una ventana de PowerShell, escriba Hola ```Install-Module Azure``` comando.</span><span class="sxs-lookup"><span data-stu-id="13b0e-151">In a PowerShell window, enter hello ```Install-Module Azure``` command.</span></span> <span data-ttu-id="13b0e-152">Complete los pasos de instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="13b0e-152">Complete hello installation steps.</span></span>    
   <span data-ttu-id="13b0e-153">b.</span><span class="sxs-lookup"><span data-stu-id="13b0e-153">b.</span></span> <span data-ttu-id="13b0e-154">Escriba hello ```Install-Module AzureRM``` comando.</span><span class="sxs-lookup"><span data-stu-id="13b0e-154">Enter hello ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="13b0e-155">Complete los pasos de instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="13b0e-155">Complete hello installation steps.</span></span>

   <span data-ttu-id="13b0e-156">Para más información, vea [Instalar Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="13b0e-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="13b0e-157">Crear los elementos de la infraestructura de soporte</span><span class="sxs-lookup"><span data-stu-id="13b0e-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="13b0e-158">Abra una ventana de PowerShell con privilegios elevados y vaya demasiado**C:\Program Files\Microsoft Azure registro integración**.</span><span class="sxs-lookup"><span data-stu-id="13b0e-158">Open an elevated PowerShell window and go too**C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="13b0e-159">Importar hello AzLog cmdlets al ejecutar el script de Hola LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="13b0e-159">Import hello AzLog cmdlets by running hello script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="13b0e-160">Escriba hello `.\LoadAzLogModule.ps1` comando.</span><span class="sxs-lookup"><span data-stu-id="13b0e-160">Enter hello `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="13b0e-161">(Hola aviso ". \" en el comando.) Puede ver algo así:</span><span class="sxs-lookup"><span data-stu-id="13b0e-161">(Notice hello “.\” in that command.) You should see something like this:</span></span></br>

   ![Lista de módulos cargados](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="13b0e-163">Escriba hello `Login-AzureRmAccount` comando.</span><span class="sxs-lookup"><span data-stu-id="13b0e-163">Enter hello `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="13b0e-164">En la ventana de inicio de sesión de hello, escriba la información de credenciales de hello para la suscripción de Hola que va a utilizar para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="13b0e-164">In hello login window, enter hello credential information for hello subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="13b0e-165">Si se trata de hello primera vez que está iniciando una sesión en tooAzure de este equipo, verá un mensaje que permita que los datos de uso de PowerShell de Microsoft toocollect.</span><span class="sxs-lookup"><span data-stu-id="13b0e-165">If this is hello first time that you're logging in tooAzure from this machine, you will see a message about allowing Microsoft toocollect PowerShell usage data.</span></span> <span data-ttu-id="13b0e-166">Se recomienda que habilite esta recopilación de datos ya que será usado tooimprove PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="13b0e-166">We recommend that you enable this data collection because it will be used tooimprove Azure PowerShell.</span></span>

4. <span data-ttu-id="13b0e-167">Tras la autenticación correcta, ha iniciado sesión y ver información de Hola Hola siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="13b0e-167">After successful authentication, you're logged in and you see hello information in hello following screenshot.</span></span> <span data-ttu-id="13b0e-168">Tome nota del nombre de identificador y la suscripción de la suscripción de hello, porque los necesitará más adelante pasos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="13b0e-168">Take note of hello subscription ID and subscription name, because you'll need them toocomplete later steps.</span></span>

   ![Ventana de PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="13b0e-170">Cree variables toostore valores que se usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="13b0e-170">Create variables toostore values that will be used later.</span></span> <span data-ttu-id="13b0e-171">Escriba cada una de hello después de las líneas de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13b0e-171">Enter each of hello following PowerShell lines.</span></span> <span data-ttu-id="13b0e-172">Puede que tenga tooadjust Hola valores toomatch su entorno.</span><span class="sxs-lookup"><span data-stu-id="13b0e-172">You might need tooadjust hello values toomatch your environment.</span></span>
    - <span data-ttu-id="13b0e-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (El nombre de la suscripción puede ser diferente.</span><span class="sxs-lookup"><span data-stu-id="13b0e-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="13b0e-174">Puede ver, como parte del resultado de hello del comando anterior Hola.)</span><span class="sxs-lookup"><span data-stu-id="13b0e-174">You can see it as part of hello output of hello previous command.)</span></span>
    - <span data-ttu-id="13b0e-175">```$location = 'West US'```(Esta variable será la ubicación de Hola de toopass usado donde se deben crear recursos.</span><span class="sxs-lookup"><span data-stu-id="13b0e-175">```$location = 'West US'``` (This variable will be used toopass hello location where resources should be created.</span></span> <span data-ttu-id="13b0e-176">Puede cambiar esta variable toobe cualquier ubicación de su elección.)</span><span class="sxs-lookup"><span data-stu-id="13b0e-176">You can change this variable toobe any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="13b0e-177">``` $name = 'azlogtest' + $random```(nombre de hello puede ser cualquier cosa, pero debe incluir solo letras minúsculas y números).</span><span class="sxs-lookup"><span data-stu-id="13b0e-177">``` $name = 'azlogtest' + $random``` (hello name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="13b0e-178">``` $storageName = $name```(Esta variable se usará para el nombre de cuenta de almacenamiento de Hola.)</span><span class="sxs-lookup"><span data-stu-id="13b0e-178">``` $storageName = $name``` (This variable will be used for hello storage account name.)</span></span>
    - <span data-ttu-id="13b0e-179">```$rgname = $name ```(Esta variable se usará para el nombre de grupo de recursos de Hola.)</span><span class="sxs-lookup"><span data-stu-id="13b0e-179">```$rgname = $name ``` (This variable will be used for hello resource group name.)</span></span>
    - <span data-ttu-id="13b0e-180">``` $eventHubNameSpaceName = $name```(Esto es nombre de Hola de espacio de nombres del concentrador de eventos de hello).</span><span class="sxs-lookup"><span data-stu-id="13b0e-180">``` $eventHubNameSpaceName = $name``` (This is hello name of hello event hub namespace.)</span></span>
6. <span data-ttu-id="13b0e-181">Especifique la suscripción de Hola que se va a trabajar con:</span><span class="sxs-lookup"><span data-stu-id="13b0e-181">Specify hello subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="13b0e-182">Cree un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="13b0e-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="13b0e-183">Si escribe `$rg` en este punto, debería ver la salida de pantalla de toothis similar:</span><span class="sxs-lookup"><span data-stu-id="13b0e-183">If you enter `$rg` at this point, you should see output similar toothis screenshot:</span></span>

   ![Salida después de la creación de un grupo de recursos](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="13b0e-185">Cree una cuenta de almacenamiento que será tookeep usa seguimiento de información de estado:</span><span class="sxs-lookup"><span data-stu-id="13b0e-185">Create a storage account that will be used tookeep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="13b0e-186">Crear espacio de nombres del concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="13b0e-186">Create hello event hub namespace.</span></span> <span data-ttu-id="13b0e-187">Esto es necesario toocreate un concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="13b0e-187">This is required toocreate an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="13b0e-188">Obtener Id. de función hello que se usará con el proveedor de la visión de hello:</span><span class="sxs-lookup"><span data-stu-id="13b0e-188">Get hello rule ID that will be used with hello insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="13b0e-189">Obtenga todas las ubicaciones posibles de Azure y agregue la variable tooa de hello nombres que se puede usar en un paso posterior:</span><span class="sxs-lookup"><span data-stu-id="13b0e-189">Get all possible Azure locations and add hello names tooa variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="13b0e-190">a.</span><span class="sxs-lookup"><span data-stu-id="13b0e-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="13b0e-191">b.</span><span class="sxs-lookup"><span data-stu-id="13b0e-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="13b0e-192">Si escribe `$locations` en este momento, verá los nombres de ubicación de hello sin información adicional de hello devuelto por Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="13b0e-192">If you enter `$locations` at this point, you see hello location names without hello additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="13b0e-193">Cree un perfil de registro de Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="13b0e-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="13b0e-194">Para obtener más información acerca de hello perfil de registros de Azure, consulte [información general de hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="13b0e-194">For more information about hello Azure log profile, see [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="13b0e-195">Podría obtener un mensaje de error cuando intente toocreate un perfil de registro.</span><span class="sxs-lookup"><span data-stu-id="13b0e-195">You might get an error message when you try toocreate a log profile.</span></span> <span data-ttu-id="13b0e-196">A continuación, puede revisar la documentación de Hola para Get-AzureRmLogProfile y Remove-AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="13b0e-196">You can then review hello documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="13b0e-197">Si ejecuta Get-AzureRmLogProfile, verá información sobre el perfil de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="13b0e-197">If you run Get-AzureRmLogProfile, you see information about hello log profile.</span></span> <span data-ttu-id="13b0e-198">Puede eliminar el perfil de registro existente de hello escribiendo hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` comando.</span><span class="sxs-lookup"><span data-stu-id="13b0e-198">You can delete hello existing log profile by entering hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Error de perfil de Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="13b0e-200">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="13b0e-200">Create a key vault</span></span>

1. <span data-ttu-id="13b0e-201">Crear almacén de claves de hello:</span><span class="sxs-lookup"><span data-stu-id="13b0e-201">Create hello key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="13b0e-202">Configurar el registro de almacén de claves de hello:</span><span class="sxs-lookup"><span data-stu-id="13b0e-202">Configure logging for hello key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="13b0e-203">Generar actividad de registro</span><span class="sxs-lookup"><span data-stu-id="13b0e-203">Generate log activity</span></span>

<span data-ttu-id="13b0e-204">Solicitudes necesitan toobe envía tooKey actividad de registro de toogenerate de almacén.</span><span class="sxs-lookup"><span data-stu-id="13b0e-204">Requests need toobe sent tooKey Vault toogenerate log activity.</span></span> <span data-ttu-id="13b0e-205">Acciones como la generación de claves, la lectura o el almacenamiento de secretos de Key Vault, crearán entradas del registro.</span><span class="sxs-lookup"><span data-stu-id="13b0e-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="13b0e-206">Mostrar claves de almacenamiento actual de hello:</span><span class="sxs-lookup"><span data-stu-id="13b0e-206">Display hello current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="13b0e-207">Genere una nueva **key2**:</span><span class="sxs-lookup"><span data-stu-id="13b0e-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="13b0e-208">Mostrar teclas de Hola de nuevo y lo vea **key2** contiene un valor diferente:</span><span class="sxs-lookup"><span data-stu-id="13b0e-208">Display hello keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="13b0e-209">Establecer y leer un secreto toogenerate entradas de registro adicionales:</span><span class="sxs-lookup"><span data-stu-id="13b0e-209">Set and read a secret toogenerate additional log entries:</span></span>
    
   <span data-ttu-id="13b0e-210">a.</span><span class="sxs-lookup"><span data-stu-id="13b0e-210">a.</span></span> <span data-ttu-id="13b0e-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="13b0e-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Secreto devuelto](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="13b0e-213">Configurar la integración de registros de Azure</span><span class="sxs-lookup"><span data-stu-id="13b0e-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="13b0e-214">Ahora que ha configurado el centro de eventos de todos los Hola elementos necesarios toohave registro de almacén de claves tooan, necesita tooconfigure integración de registro de Azure:</span><span class="sxs-lookup"><span data-stu-id="13b0e-214">Now that you have configured all hello required elements toohave Key Vault logging tooan event hub, you need tooconfigure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="13b0e-215">Ejecute hello AzLog comando para cada concentrador de eventos:</span><span class="sxs-lookup"><span data-stu-id="13b0e-215">Run hello AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="13b0e-216">Tras un minuto aproximadamente de dos últimos comandos hello en ejecución, debería ver los archivos JSON que se generan.</span><span class="sxs-lookup"><span data-stu-id="13b0e-216">After a minute or so of running hello last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="13b0e-217">Puede confirmar que mediante la supervisión de directorio de hello **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="13b0e-217">You can confirm that by monitoring hello directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13b0e-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13b0e-218">Next steps</span></span>

- [<span data-ttu-id="13b0e-219">Preguntas más frecuentes sobre la integración de registro de Azure</span><span class="sxs-lookup"><span data-stu-id="13b0e-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="13b0e-220">Introducción a la integración de registros de Azure</span><span class="sxs-lookup"><span data-stu-id="13b0e-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="13b0e-221">Integrar registros de recursos de Azure en sistemas SIEM</span><span class="sxs-lookup"><span data-stu-id="13b0e-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
