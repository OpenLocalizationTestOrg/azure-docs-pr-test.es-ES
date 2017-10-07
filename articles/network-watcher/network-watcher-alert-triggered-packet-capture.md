---
title: "aaaUse automático de toodo de la captura de paquetes de red con funciones de Azure y las alertas de supervisión | Documentos de Microsoft"
description: "Este artículo describe cómo toocreate una alerta activa captura de paquetes con Monitor de red de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="722fb-103">Uso de capturas de paquetes para realizar la supervisión proactiva de la red con alertas y Azure Functions</span><span class="sxs-lookup"><span data-stu-id="722fb-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="722fb-104">Captura de paquetes de Monitor de red crea sesiones de captura tráfico tootrack dentro y fuera de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="722fb-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="722fb-105">Hello archivo de captura puede tener un filtro que se define tootrack Hola solo el tráfico que desea toomonitor.</span><span class="sxs-lookup"><span data-stu-id="722fb-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="722fb-106">Estos datos, a continuación, se almacenan en un blob de almacenamiento o localmente en la máquina de invitado de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="722fb-107">Esta funcionalidad se puede iniciar de forma remota desde otros escenarios de automatización, como Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="722fb-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="722fb-108">Proporciona de captura de paquetes que Hola capturas automático toorun de capacidad, según define anomalías de la red.</span><span class="sxs-lookup"><span data-stu-id="722fb-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="722fb-109">Otros usos son la recopilación de estadísticas de red, la obtención de información sobre las intrusiones de red y la depuración de las comunicaciones cliente-servidor, entre otros.</span><span class="sxs-lookup"><span data-stu-id="722fb-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="722fb-110">Los recursos implementados en Azure se ejecutan las 24 horas, los 7 días de la semana.</span><span class="sxs-lookup"><span data-stu-id="722fb-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="722fb-111">Usted y su personal no se puede supervisar activamente estado Hola de todos los recursos 24/7.</span><span class="sxs-lookup"><span data-stu-id="722fb-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="722fb-112">¿Qué ocurre si un problema se produce a las 2 a. m.?</span><span class="sxs-lookup"><span data-stu-id="722fb-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="722fb-113">Al usar Monitor de red, las alertas y funciones desde dentro de hello ecosistema de Azure, puede responder proactivamente con problemas de toosolve de datos y las herramientas de hello en la red.</span><span class="sxs-lookup"><span data-stu-id="722fb-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![Escenario][scenario]

## <a name="prerequisites"></a><span data-ttu-id="722fb-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="722fb-115">Prerequisites</span></span>

* <span data-ttu-id="722fb-116">versión más reciente de Hola de [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="722fb-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="722fb-117">Una instancia existente de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="722fb-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="722fb-118">[Cree una instancia de Network Watcher](network-watcher-create.md) si aún no tiene una.</span><span class="sxs-lookup"><span data-stu-id="722fb-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="722fb-119">Una máquina virtual existente en hello misma región que el Monitor de red con hello [extensión Windows](../virtual-machines/windows/extensions-nwa.md) o [extensión de máquina virtual Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="722fb-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="722fb-120">Escenario</span><span class="sxs-lookup"><span data-stu-id="722fb-120">Scenario</span></span>

<span data-ttu-id="722fb-121">En este ejemplo, la máquina virtual está enviando los segmentos TCP más de lo habitual y desea toobe una alerta.</span><span class="sxs-lookup"><span data-stu-id="722fb-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="722fb-122">Los segmentos TCP se usan aquí como ejemplo, pero podría usar cualquier condición de alerta.</span><span class="sxs-lookup"><span data-stu-id="722fb-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="722fb-123">Cuando se le indique, desea toounderstand de datos de nivel de paquete tooreceive ¿por qué ha aumentado la comunicación.</span><span class="sxs-lookup"><span data-stu-id="722fb-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="722fb-124">A continuación, puede tomar medidas comunicación tooregular de tooreturn Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="722fb-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="722fb-125">En este escenario se supone que tiene una instancia existente de Network Watcher y un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="722fb-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="722fb-126">Hola lista siguiente es una visión general de flujo de trabajo de Hola que tiene lugar:</span><span class="sxs-lookup"><span data-stu-id="722fb-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="722fb-127">Se desencadena una alerta en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="722fb-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="722fb-128">alerta de Hello llama a la función de Azure a través de un webhook.</span><span class="sxs-lookup"><span data-stu-id="722fb-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="722fb-129">La función de Azure procesa la alerta de Hola e inicia una sesión de captura de paquetes de Monitor de red.</span><span class="sxs-lookup"><span data-stu-id="722fb-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="722fb-130">captura de paquetes de saludo se ejecuta en hello VM y recopila tráfico.</span><span class="sxs-lookup"><span data-stu-id="722fb-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="722fb-131">Hello archivo de captura de paquete se carga tooa cuenta de almacenamiento para su revisión y un diagnóstico más detallado.</span><span class="sxs-lookup"><span data-stu-id="722fb-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="722fb-132">tooautomate este proceso, que creamos y conectar una alerta en nuestro tootrigger de máquina virtual cuando se produce el incidente de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="722fb-133">También creamos un toocall de función en el Monitor de red.</span><span class="sxs-lookup"><span data-stu-id="722fb-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="722fb-134">Este escenario Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="722fb-134">This scenario does hello following:</span></span>

* <span data-ttu-id="722fb-135">Creará una función de Azure que inicie una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="722fb-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="722fb-136">Crea una regla de alerta en una máquina virtual y configura hello toocall de regla de alerta hello Azure función.</span><span class="sxs-lookup"><span data-stu-id="722fb-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="722fb-137">Creación de una función de Azure</span><span class="sxs-lookup"><span data-stu-id="722fb-137">Create an Azure function</span></span>

<span data-ttu-id="722fb-138">primer paso de Hello es toocreate una alerta de hello tooprocess función Azure y crear una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="722fb-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="722fb-139">Hola [portal de Azure](https://portal.azure.com), seleccione **New** > **proceso** > **aplicación de la función**.</span><span class="sxs-lookup"><span data-stu-id="722fb-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Creación de una aplicación de función][1-1]

2. <span data-ttu-id="722fb-141">En hello **aplicación de la función** hoja, escriba Hola después de valores y, a continuación, seleccione **Aceptar** toocreate Hola aplicación:</span><span class="sxs-lookup"><span data-stu-id="722fb-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="722fb-142">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="722fb-142">**Setting**</span></span> | <span data-ttu-id="722fb-143">**Valor**</span><span class="sxs-lookup"><span data-stu-id="722fb-143">**Value**</span></span> | <span data-ttu-id="722fb-144">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="722fb-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="722fb-145">**Nombre de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="722fb-145">**App name**</span></span>|<span data-ttu-id="722fb-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="722fb-146">PacketCaptureExample</span></span>|<span data-ttu-id="722fb-147">nombre de Hola de aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="722fb-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="722fb-148">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="722fb-148">**Subscription**</span></span>|<span data-ttu-id="722fb-149">[La suscripción] Hola suscripción para qué aplicación de función de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="722fb-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="722fb-150">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="722fb-150">**Resource Group**</span></span>|<span data-ttu-id="722fb-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="722fb-151">PacketCaptureRG</span></span>|<span data-ttu-id="722fb-152">Hola recursos grupo toocontain Hola función aplicación.</span><span class="sxs-lookup"><span data-stu-id="722fb-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="722fb-153">**Plan de hospedaje**</span><span class="sxs-lookup"><span data-stu-id="722fb-153">**Hosting Plan**</span></span>|<span data-ttu-id="722fb-154">Plan de consumo</span><span class="sxs-lookup"><span data-stu-id="722fb-154">Consumption Plan</span></span>| <span data-ttu-id="722fb-155">tipo de Hola de plan usa su aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="722fb-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="722fb-156">Las opciones son Consumo o plan de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="722fb-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="722fb-157">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="722fb-157">**Location**</span></span>|<span data-ttu-id="722fb-158">Central EE. UU.:</span><span class="sxs-lookup"><span data-stu-id="722fb-158">Central US</span></span>| <span data-ttu-id="722fb-159">región de Hola de qué aplicación de función de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="722fb-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="722fb-160">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="722fb-160">**Storage Account**</span></span>|<span data-ttu-id="722fb-161">{autogenerated}</span><span class="sxs-lookup"><span data-stu-id="722fb-161">{autogenerated}</span></span>| <span data-ttu-id="722fb-162">cuenta de almacenamiento de Hola que necesita las funciones de Azure para almacenamiento general.</span><span class="sxs-lookup"><span data-stu-id="722fb-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="722fb-163">En hello **PacketCaptureExample función aplicaciones** hoja, seleccione **funciones** > **función personalizada**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="722fb-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="722fb-164">Seleccione **HttpTrigger Powershell**y, a continuación, escriba Hola restante información.</span><span class="sxs-lookup"><span data-stu-id="722fb-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="722fb-165">Por último, toocreate función hello, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="722fb-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="722fb-166">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="722fb-166">**Setting**</span></span> | <span data-ttu-id="722fb-167">**Valor**</span><span class="sxs-lookup"><span data-stu-id="722fb-167">**Value**</span></span> | <span data-ttu-id="722fb-168">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="722fb-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="722fb-169">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="722fb-169">**Scenario**</span></span>|<span data-ttu-id="722fb-170">Experimental</span><span class="sxs-lookup"><span data-stu-id="722fb-170">Experimental</span></span>|<span data-ttu-id="722fb-171">Tipo de escenario</span><span class="sxs-lookup"><span data-stu-id="722fb-171">Type of scenario</span></span>|
    |<span data-ttu-id="722fb-172">**Asigne un nombre a la función**</span><span class="sxs-lookup"><span data-stu-id="722fb-172">**Name your function**</span></span>|<span data-ttu-id="722fb-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="722fb-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="722fb-174">Nombre de función hello</span><span class="sxs-lookup"><span data-stu-id="722fb-174">Name of hello function</span></span>|
    |<span data-ttu-id="722fb-175">**Nivel de autorización**</span><span class="sxs-lookup"><span data-stu-id="722fb-175">**Authorization level**</span></span>|<span data-ttu-id="722fb-176">Función</span><span class="sxs-lookup"><span data-stu-id="722fb-176">Function</span></span>|<span data-ttu-id="722fb-177">Nivel de autorización para la función hello</span><span class="sxs-lookup"><span data-stu-id="722fb-177">Authorization level for hello function</span></span>|

![Ejemplo de funciones][functions1]

> [!NOTE]
> <span data-ttu-id="722fb-179">plantilla de PowerShell de Hello en fase experimental y no tiene compatibilidad completa.</span><span class="sxs-lookup"><span data-stu-id="722fb-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="722fb-180">Las personalizaciones son necesarias para este ejemplo y se explican en pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="722fb-181">Adición de módulos</span><span class="sxs-lookup"><span data-stu-id="722fb-181">Add modules</span></span>

<span data-ttu-id="722fb-182">toouse cmdlets de PowerShell de Monitor de red, cargue la aplicación de hello más reciente PowerShell módulo toohello función.</span><span class="sxs-lookup"><span data-stu-id="722fb-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="722fb-183">En el equipo local con los módulos de PowerShell de Azure más recientes Hola instalado, ejecute hello siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="722fb-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="722fb-184">Esto deja de ejemplo Hola ruta de acceso local de los módulos de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="722fb-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="722fb-185">Estas carpetas se usan en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="722fb-185">These folders are used in a later step.</span></span> <span data-ttu-id="722fb-186">los módulos de Hola que se usan en este escenario son:</span><span class="sxs-lookup"><span data-stu-id="722fb-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="722fb-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="722fb-187">AzureRM.Network</span></span>

    * <span data-ttu-id="722fb-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="722fb-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="722fb-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="722fb-189">AzureRM.Resources</span></span>

    ![Carpetas de PowerShell][functions5]

1. <span data-ttu-id="722fb-191">Seleccione **función de la configuración de la aplicación** > **vaya tooApp Editor servicio**.</span><span class="sxs-lookup"><span data-stu-id="722fb-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![Configuración de Function App][functions2]

1. <span data-ttu-id="722fb-193">Menú contextual hello **AlertPacketCapturePowershell** carpeta y, a continuación, cree una carpeta denominada **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="722fb-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="722fb-194">Cree una subcarpeta para cada módulo que necesite.</span><span class="sxs-lookup"><span data-stu-id="722fb-194">Create a subfolder for each module that you need.</span></span>

    ![Carpeta y subcarpetas][functions3]

    * <span data-ttu-id="722fb-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="722fb-196">AzureRM.Network</span></span>

    * <span data-ttu-id="722fb-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="722fb-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="722fb-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="722fb-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="722fb-199">Menú contextual hello **AzureRM.Network** subcarpeta y, a continuación, seleccione **cargar archivos**.</span><span class="sxs-lookup"><span data-stu-id="722fb-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="722fb-200">Vaya tooyour Azure módulos.</span><span class="sxs-lookup"><span data-stu-id="722fb-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="722fb-201">Hola local **AzureRM.Network** carpeta, seleccione todos los archivos de hello en carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="722fb-202">Después seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="722fb-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="722fb-203">Repita estos pasos para **AzureRM.Profile** y **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="722fb-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Carga de archivos][functions6]

1. <span data-ttu-id="722fb-205">Una vez finalizado, cada carpeta debe tener archivos de módulo de PowerShell de Hola desde el equipo local.</span><span class="sxs-lookup"><span data-stu-id="722fb-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![Archivos de PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="722fb-207">Autenticación</span><span class="sxs-lookup"><span data-stu-id="722fb-207">Authentication</span></span>

<span data-ttu-id="722fb-208">cmdlets de PowerShell de hello toouse, debe autenticarse.</span><span class="sxs-lookup"><span data-stu-id="722fb-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="722fb-209">Configurar la autenticación en la aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="722fb-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="722fb-210">autenticación de tooconfigure, debe configurar las variables de entorno y cargar una aplicación de función de toohello de archivo de clave de cifrado.</span><span class="sxs-lookup"><span data-stu-id="722fb-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="722fb-211">Este escenario proporciona solo un ejemplo de cómo tooimplement la autenticación con las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="722fb-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="722fb-212">Hay otra maneras toodo esto.</span><span class="sxs-lookup"><span data-stu-id="722fb-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="722fb-213">Credenciales cifradas</span><span class="sxs-lookup"><span data-stu-id="722fb-213">Encrypted credentials</span></span>

<span data-ttu-id="722fb-214">Hola siguiente script de PowerShell crea un archivo de claves denominado **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="722fb-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="722fb-215">También proporciona una versión cifrada de la contraseña de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="722fb-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="722fb-216">Esta contraseña es hello misma contraseña que se define para la aplicación de Azure Active Directory de Hola que se usa para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="722fb-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="722fb-217">En el Editor de aplicación de servicio de aplicación de la función de hello hello, cree una carpeta denominada **claves** en **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="722fb-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="722fb-218">A continuación, cargar hello **PassEncryptKey.key** archivo que creó en el ejemplo anterior de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![Clave de funciones][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="722fb-220">Recuperación de valores para variables de entorno</span><span class="sxs-lookup"><span data-stu-id="722fb-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="722fb-221">requisito final de Hello es tooset las variables de entorno de Hola que son valores de hello tooaccess necesarios para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="722fb-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="722fb-222">Hello lista siguiente muestra las variables de entorno de Hola que se crean:</span><span class="sxs-lookup"><span data-stu-id="722fb-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="722fb-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="722fb-223">AzureClientID</span></span>

* <span data-ttu-id="722fb-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="722fb-224">AzureTenant</span></span>

* <span data-ttu-id="722fb-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="722fb-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="722fb-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="722fb-226">AzureClientID</span></span>

<span data-ttu-id="722fb-227">Id. de cliente Hello es hello Id. de aplicación de una aplicación en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="722fb-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="722fb-228">Si aún no tiene un toouse de aplicación, ejecutar Hola después toocreate de ejemplo de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="722fb-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="722fb-229">contraseña de Hola que usar al crear aplicación hello debe ser Hola misma contraseña que creó anteriormente cuando se guarda el archivo de clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="722fb-230">Hola portal de Azure, seleccione **suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="722fb-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="722fb-231">Seleccione toouse de suscripción de hello y, a continuación, seleccione **(de índices IAM) de control de acceso**.</span><span class="sxs-lookup"><span data-stu-id="722fb-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![IAM de Functions][functions9]

1. <span data-ttu-id="722fb-233">Elija toouse de cuenta de hello y, a continuación, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="722fb-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="722fb-234">Copiar Hola identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="722fb-234">Copy hello Application ID.</span></span>

    ![Id. de aplicación de Functions][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="722fb-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="722fb-236">AzureTenant</span></span>

<span data-ttu-id="722fb-237">Obtener Id. de inquilino de hello ejecutando Hola siguiendo el ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="722fb-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="722fb-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="722fb-238">AzureCredPassword</span></span>

<span data-ttu-id="722fb-239">valor de Hola de variable de entorno AzureCredPassword hello es valor de Hola que obtendrá ejecutaran Hola siguiendo el ejemplo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="722fb-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="722fb-240">En este ejemplo se Hola misma que se muestra en hello anterior **credenciales cifradas** sección.</span><span class="sxs-lookup"><span data-stu-id="722fb-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="722fb-241">Hola valor requerido es una salida de hello de hello `$Encryptedpassword` variable.</span><span class="sxs-lookup"><span data-stu-id="722fb-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="722fb-242">Se trata de hello servicio contraseña de la entidad que se ha cifrado mediante script de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a><span data-ttu-id="722fb-243">Almacenar las variables de entorno de Hola</span><span class="sxs-lookup"><span data-stu-id="722fb-243">Store hello environment variables</span></span>

1. <span data-ttu-id="722fb-244">Aplicación de la función de toohello vaya.</span><span class="sxs-lookup"><span data-stu-id="722fb-244">Go toohello function app.</span></span> <span data-ttu-id="722fb-245">A continuación, seleccione **Configuración de Function App** > **Configurar las opciones de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="722fb-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Configuración de aplicaciones][functions11]

1. <span data-ttu-id="722fb-247">Agregar variables de entorno de Hola y configuración de la aplicación toohello de sus valores y, a continuación, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="722fb-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![Configuración de la aplicación][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="722fb-249">Add toohello de PowerShell (función)</span><span class="sxs-lookup"><span data-stu-id="722fb-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="722fb-250">Es ahora toomake tiempo llama al Monitor de red desde dentro de hello Azure función.</span><span class="sxs-lookup"><span data-stu-id="722fb-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="722fb-251">Dependiendo de los requisitos de hello, implementación de Hola de esta función puede variar.</span><span class="sxs-lookup"><span data-stu-id="722fb-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="722fb-252">Sin embargo, el flujo general de Hola de código de hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="722fb-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="722fb-253">Procesar los parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="722fb-253">Process input parameters.</span></span>
2. <span data-ttu-id="722fb-254">Paquete existente de la consulta de captura tooverify límites y resolver conflictos de nombre.</span><span class="sxs-lookup"><span data-stu-id="722fb-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="722fb-255">Crear una captura de paquetes con los parámetros adecuados.</span><span class="sxs-lookup"><span data-stu-id="722fb-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="722fb-256">Sondear la captura de paquetes periódicamente hasta que finalice.</span><span class="sxs-lookup"><span data-stu-id="722fb-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="722fb-257">Notificar a usuario Hola que sesión de captura de paquetes de saludo ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="722fb-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="722fb-258">Hello en el ejemplo siguiente se es código de PowerShell que puede usarse en función de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="722fb-259">Hay valores que necesitan toobe reemplazado para **subscriptionId**, **resourceGroupName**, y **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="722fb-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="722fb-260">Recuperar la dirección URL de hello (función)</span><span class="sxs-lookup"><span data-stu-id="722fb-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="722fb-261">Después de crear la función, configure la dirección URL de Hola de toocall alerta que esté asociada con la función hello.</span><span class="sxs-lookup"><span data-stu-id="722fb-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="722fb-262">tooget este valor, la función de copiar Hola dirección URL desde la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="722fb-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![Buscar la dirección URL de hello (función)][functions13]

2. <span data-ttu-id="722fb-264">Copiar dirección URL de la función de hello para la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="722fb-264">Copy hello function URL for your function app.</span></span>

    ![Copiar dirección URL de hello (función)][2]

<span data-ttu-id="722fb-266">Si necesitas propiedades personalizadas en la carga de Hola de solicitud POST de webhook de hello, consulte demasiado[configurar un webhook en una alerta de métrica Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="722fb-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="722fb-267">Configuración de una alerta en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="722fb-267">Configure an alert on a VM</span></span>

<span data-ttu-id="722fb-268">Las alertas pueden estar configurado toonotify personas cuando una métrica específica supera un umbral que se asigna tooit.</span><span class="sxs-lookup"><span data-stu-id="722fb-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="722fb-269">En este ejemplo, alerta de hello es en hello segmentos TCP que se envían, pero se puede activar la alerta de Hola para muchas otras métricas.</span><span class="sxs-lookup"><span data-stu-id="722fb-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="722fb-270">En este ejemplo, una alerta es toocall configurado una función de webhook toocall Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="722fb-271">Crear regla de alerta de Hola</span><span class="sxs-lookup"><span data-stu-id="722fb-271">Create hello alert rule</span></span>

<span data-ttu-id="722fb-272">Vaya a máquina virtual existente de tooan y, a continuación, agregar una regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="722fb-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="722fb-273">Se puede encontrar documentación más detallada sobre la configuración de alertas en [Creación de alertas en Azure Monitor para servicios de Azure (Azure Portal)](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="722fb-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="722fb-274">Escriba Hola después de valores de hello **regla de alerta** hoja y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="722fb-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="722fb-275">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="722fb-275">**Setting**</span></span> | <span data-ttu-id="722fb-276">**Valor**</span><span class="sxs-lookup"><span data-stu-id="722fb-276">**Value**</span></span> | <span data-ttu-id="722fb-277">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="722fb-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="722fb-278">**Name**</span><span class="sxs-lookup"><span data-stu-id="722fb-278">**Name**</span></span>|<span data-ttu-id="722fb-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="722fb-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="722fb-280">Nombre de regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="722fb-281">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="722fb-281">**Description**</span></span>|<span data-ttu-id="722fb-282">Los segmentos TCP enviados superaron el umbral</span><span class="sxs-lookup"><span data-stu-id="722fb-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="722fb-283">Descripción de Hello para la regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="722fb-284">**Métrica**</span><span class="sxs-lookup"><span data-stu-id="722fb-284">**Metric**</span></span>|<span data-ttu-id="722fb-285">Segmentos TCP enviados</span><span class="sxs-lookup"><span data-stu-id="722fb-285">TCP segments sent</span></span>| <span data-ttu-id="722fb-286">alerta de Hello toouse métrica tootrigger Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="722fb-287">**Condition**</span><span class="sxs-lookup"><span data-stu-id="722fb-287">**Condition**</span></span>|<span data-ttu-id="722fb-288">Mayor que</span><span class="sxs-lookup"><span data-stu-id="722fb-288">Greater than</span></span>| <span data-ttu-id="722fb-289">Hola condición toouse al evaluar la métrica de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="722fb-290">**Umbral**</span><span class="sxs-lookup"><span data-stu-id="722fb-290">**Threshold**</span></span>|<span data-ttu-id="722fb-291">100</span><span class="sxs-lookup"><span data-stu-id="722fb-291">100</span></span>| <span data-ttu-id="722fb-292">valor de Hola de métrica de Hola que desencadena la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="722fb-293">Este valor debe establecerse tooa valor válido para su entorno.</span><span class="sxs-lookup"><span data-stu-id="722fb-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="722fb-294">**Período**</span><span class="sxs-lookup"><span data-stu-id="722fb-294">**Period**</span></span>|<span data-ttu-id="722fb-295">A través de hello últimos cinco minutos</span><span class="sxs-lookup"><span data-stu-id="722fb-295">Over hello last five minutes</span></span>| <span data-ttu-id="722fb-296">Determina el período de hello en qué toolook para el umbral de hello en métrica Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="722fb-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="722fb-297">**Webhook**</span></span>|<span data-ttu-id="722fb-298">[Dirección URL del webhook de la aplicación de función]</span><span class="sxs-lookup"><span data-stu-id="722fb-298">[webhook URL from function app]</span></span>| <span data-ttu-id="722fb-299">URL del webhook Hola de aplicación de función hello que creó en los pasos anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="722fb-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="722fb-300">métrica de segmentos de Hello TCP no está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="722fb-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="722fb-301">Más información acerca de cómo tooenable otras métricas visitando [habilitar la supervisión y diagnóstico](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="722fb-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="722fb-302">Revisar los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="722fb-302">Review hello results</span></span>

<span data-ttu-id="722fb-303">Después de criterios de Hola para desencadenadores de alerta de hello, se crea una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="722fb-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="722fb-304">Vaya tooNetwork monitor y, a continuación, seleccione **captura de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="722fb-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="722fb-305">En esta página, puede seleccionar Hola paquete captura archivo vínculo toodownload Hola captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="722fb-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![Visualización de captura de paquetes][functions14]

<span data-ttu-id="722fb-307">Si el archivo de captura de Hola se almacena localmente, puede recuperarlo mediante la firma en la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="722fb-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="722fb-308">Para obtener instrucciones sobre cómo descargar archivos desde cuentas de Azure Storage, consulte [Introducción a Azure Blob Storage mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="722fb-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="722fb-309">Otra herramienta que puede usar es el [Explorador de almacenamiento](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="722fb-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="722fb-310">Después de que se ha descargado la captura, puede verla con cualquier herramienta que pueda leer un archivo **.cap**.</span><span class="sxs-lookup"><span data-stu-id="722fb-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="722fb-311">Estos son vínculos tootwo de estas herramientas:</span><span class="sxs-lookup"><span data-stu-id="722fb-311">Following are links tootwo of these tools:</span></span>

- <span data-ttu-id="722fb-312">[Analizador de mensajes de Microsoft](https://technet.microsoft.com/library/jj649776.aspx).</span><span class="sxs-lookup"><span data-stu-id="722fb-312">[Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)</span></span>
- [<span data-ttu-id="722fb-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="722fb-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="722fb-314">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="722fb-314">Next steps</span></span>

<span data-ttu-id="722fb-315">Obtenga información acerca de cómo tooview su paquete captura visitando [análisis de captura de paquetes con Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="722fb-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
