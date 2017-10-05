---
title: "Implementación del servicio Site Recovery Mobility con DSC de Azure Automation| Microsoft Docs"
description: "Se describe cómo usar DSC de Azure Automation para implementar automáticamente el servicio Azure Site Recovery Mobility y el agente de Azure para la replicación de servidores físicos y VM de VMware en Azure."
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: bcc5f11afbecac8fe63935f3401dd3e2d767e8aa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-the-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="bb20f-103">Implementación del servicio Mobility con DSC de Azure Automation para la replicación de VM</span><span class="sxs-lookup"><span data-stu-id="bb20f-103">Deploy the Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="bb20f-104">En Operations Management Suite, le proporcionamos una completa solución de copia de seguridad y recuperación ante desastres que puede usar como parte de su plan de continuidad empresarial.</span><span class="sxs-lookup"><span data-stu-id="bb20f-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="bb20f-105">Comenzamos este viaje con Hyper-V usando Réplica de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="bb20f-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="bb20f-106">Pero nos hemos expandido para abarcar la configuración heterogénea dado que los clientes tienen varios hipervisores y plataformas en sus nubes.</span><span class="sxs-lookup"><span data-stu-id="bb20f-106">But we have expanded to support a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="bb20f-107">Si actualmente ejecuta cargas de trabajo de VMware o servidores físicos, un servidor de administración ejecuta todos los componentes de Azure Site Recovery de su entorno para controlar la comunicación y la replicación de datos con Azure, si Azure es su destino.</span><span class="sxs-lookup"><span data-stu-id="bb20f-107">If you are running VMware workloads and/or physical servers today, a management server runs all of the Azure Site Recovery components in your environment to handle the communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-the-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="bb20f-108">Implementación de Mobility Service de Site Recovery mediante DSC de Automatización</span><span class="sxs-lookup"><span data-stu-id="bb20f-108">Deploy the Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="bb20f-109">Para comenzar, vamos a realizar un desglose rápido de lo que hace este servidor de administración.</span><span class="sxs-lookup"><span data-stu-id="bb20f-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="bb20f-110">El servidor de administración ejecuta varios roles de servidor.</span><span class="sxs-lookup"><span data-stu-id="bb20f-110">The management server runs several server roles.</span></span> <span data-ttu-id="bb20f-111">Uno de ellos es el de *configuración*, que coordina la comunicación y administra los procesos de replicación y recuperación de datos.</span><span class="sxs-lookup"><span data-stu-id="bb20f-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="bb20f-112">Además, el rol de *proceso* actúa como puerta de enlace de replicación.</span><span class="sxs-lookup"><span data-stu-id="bb20f-112">In addition, the *process* role acts as a replication gateway.</span></span> <span data-ttu-id="bb20f-113">Este rol recibe datos de replicación provenientes de máquinas de origen protegidas, los optimiza con almacenamiento en caché, compresión y cifrado y los envía a una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb20f-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it to an Azure storage account.</span></span> <span data-ttu-id="bb20f-114">Otra de las funciones del rol de proceso es insertar la instalación de Mobility Service en máquinas protegidas y llevar a cabo la detección automática de máquinas virtuales de VMware.</span><span class="sxs-lookup"><span data-stu-id="bb20f-114">One of the functions for the process role is also to push installation of the Mobility service to protected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="bb20f-115">En el caso de una conmutación por recuperación de Azure, el rol de *destino maestro* será administrará los datos de replicación como parte de esta operación.</span><span class="sxs-lookup"><span data-stu-id="bb20f-115">If there's a failback from Azure, the *master target* role will handle the replication data as part of this operation.</span></span>

<span data-ttu-id="bb20f-116">Para las máquinas protegidas, confiamos en *Mobility Service*.</span><span class="sxs-lookup"><span data-stu-id="bb20f-116">For the protected machines, we rely on the *Mobility service*.</span></span> <span data-ttu-id="bb20f-117">Este componente está implementado en cada máquina (máquina virtual de VMware o servidor físico) que quiere replicar en Azure.</span><span class="sxs-lookup"><span data-stu-id="bb20f-117">This component is deployed to every machine (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="bb20f-118">Lo que hace es capturar las escrituras de datos en la máquina y reenviarlas al servidor de administración (rol de proceso).</span><span class="sxs-lookup"><span data-stu-id="bb20f-118">It captures data writes on the machine and forwards them to the management server (process role).</span></span>

<span data-ttu-id="bb20f-119">Cuando se trabaja hacia la continuidad empresarial, es importante comprender las cargas de trabajo, la infraestructura y los componentes que intervienen.</span><span class="sxs-lookup"><span data-stu-id="bb20f-119">When you're dealing with business continuity, it's important to understand your workloads, your infrastructure, and the components involved.</span></span> <span data-ttu-id="bb20f-120">Así puede cumplir los requisitos de los objetivos de tiempo de recuperación (RTO) y objetivos de punto de recuperación (RPO).</span><span class="sxs-lookup"><span data-stu-id="bb20f-120">You can then meet the requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="bb20f-121">En este contexto, Mobility Service es esencial para garantizar la protección de las cargas de trabajo de la manera prevista.</span><span class="sxs-lookup"><span data-stu-id="bb20f-121">In this context, the Mobility service is key to ensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="bb20f-122">De modo que, ¿cómo puede garantizar, de una forma optimizada, que dispone de una configuración protegida confiable con la ayuda de algunos componentes de Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="bb20f-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="bb20f-123">En este artículo se proporciona un ejemplo de cómo puede usar Configuración de estado deseado (DSC) de Automatización de Azure, en combinación con Site Recovery, para garantizar que:</span><span class="sxs-lookup"><span data-stu-id="bb20f-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, to ensure that:</span></span>

* <span data-ttu-id="bb20f-124">Mobility Service y el agente de máquina virtual de Azure están implementados en las máquinas virtuales que quiere proteger.</span><span class="sxs-lookup"><span data-stu-id="bb20f-124">The Mobility service and Azure VM agent are deployed to the Windows machines that you want to protect.</span></span>
* <span data-ttu-id="bb20f-125">Mobility Service y el agente de máquina virtual de Azure siempre se ejecutan cuando Azure es el destino de la replicación.</span><span class="sxs-lookup"><span data-stu-id="bb20f-125">The Mobility service and Azure VM agent are always running when Azure is the replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb20f-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bb20f-126">Prerequisites</span></span>
* <span data-ttu-id="bb20f-127">Un repositorio para almacenar la instalación necesaria</span><span class="sxs-lookup"><span data-stu-id="bb20f-127">A repository to store the required setup</span></span>
* <span data-ttu-id="bb20f-128">Un repositorio para almacenar la frase de contraseña necesaria para registrarse en el servidor de administración</span><span class="sxs-lookup"><span data-stu-id="bb20f-128">A repository to store the required passphrase to register with the management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="bb20f-129">Se genera una frase de contraseña única para cada servidor de administración.</span><span class="sxs-lookup"><span data-stu-id="bb20f-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="bb20f-130">Si va a implementar varios servidores de administración, tendrá que asegurarse de que se almacene la frase de contraseña correcta en el archivo passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="bb20f-130">If you are going to deploy multiple management servers, you have to ensure that the correct passphrase is stored in the passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="bb20f-131">Windows Management Framework (WMF) 5.0 instalado en las máquinas virtuales en las que quiere habilitar la protección (un requisito para DSC de Automatización de Azure)</span><span class="sxs-lookup"><span data-stu-id="bb20f-131">Windows Management Framework (WMF) 5.0 installed on the machines that you want to enable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="bb20f-132">Si quiere usar DSC para máquinas Windows que tengan instalado WMF 4.0, consulte la sección [Uso de DSC en entornos desconectados](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="bb20f-132">If you want to use DSC for Windows machines that have WMF 4.0 installed, see the section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="bb20f-133">Mobility Service se puede instalar mediante la línea de comandos y acepta varios argumentos.</span><span class="sxs-lookup"><span data-stu-id="bb20f-133">The Mobility service can be installed through the command line and accepts several arguments.</span></span> <span data-ttu-id="bb20f-134">Por ese motivo debe tener los archivos binarios (después de extraerlos de la configuración) y almacenarlos en un lugar donde puede recuperarlos mediante una configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="bb20f-134">That’s why you need to have the binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="bb20f-135">Paso 1: Extracción de los archivos binarios</span><span class="sxs-lookup"><span data-stu-id="bb20f-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="bb20f-136">Para extraer los archivos que necesita para esta configuración, vaya al siguiente directorio en el servidor de administración:</span><span class="sxs-lookup"><span data-stu-id="bb20f-136">To extract the files that you need for this setup, browse to the following directory on your management server:</span></span>

    <span data-ttu-id="bb20f-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="bb20f-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="bb20f-138">En esta carpeta, debería ver un archivo MSI denominado:</span><span class="sxs-lookup"><span data-stu-id="bb20f-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="bb20f-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="bb20f-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="bb20f-140">Use el comando siguiente para extraer el instalador:</span><span class="sxs-lookup"><span data-stu-id="bb20f-140">Use the following command to extract the installer:</span></span>

    <span data-ttu-id="bb20f-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="bb20f-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="bb20f-142">Seleccione todos los archivos y envíelos a una carpeta comprimida (en zip).</span><span class="sxs-lookup"><span data-stu-id="bb20f-142">Select all files and send them to a compressed (zipped) folder.</span></span>

<span data-ttu-id="bb20f-143">Ahora dispone de los archivos binarios que necesita para automatizar la instalación de Mobility Service con DSC de Automatización.</span><span class="sxs-lookup"><span data-stu-id="bb20f-143">You now have the binaries that you need to automate the setup of the Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="bb20f-144">Frase de contraseña</span><span class="sxs-lookup"><span data-stu-id="bb20f-144">Passphrase</span></span>
<span data-ttu-id="bb20f-145">A continuación, debe determinar dónde desea colocar esta carpeta comprimida.</span><span class="sxs-lookup"><span data-stu-id="bb20f-145">Next, you need to determine where you want to place this zipped folder.</span></span> <span data-ttu-id="bb20f-146">Puede utilizar una cuenta de almacenamiento de Azure, tal como se muestra más adelante, para almacenar la frase de contraseña que necesita para la instalación.</span><span class="sxs-lookup"><span data-stu-id="bb20f-146">You can use an Azure storage account, as shown later, to store the passphrase that you need for the setup.</span></span> <span data-ttu-id="bb20f-147">A continuación, el agente se registra con el servidor de administración como parte del proceso.</span><span class="sxs-lookup"><span data-stu-id="bb20f-147">The agent will then register with the management server as part of the process.</span></span>

<span data-ttu-id="bb20f-148">La frase de contraseña que recibió al implementar el servidor de administración se puede guardar en un archivo de texto como passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="bb20f-148">The passphrase that you got when you deployed the management server can be saved to a text file as passphrase.txt.</span></span>

<span data-ttu-id="bb20f-149">Coloque la carpeta comprimida y la frase de contraseña en un contenedor dedicado en la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb20f-149">Place both the zipped folder and the passphrase in a dedicated container in the Azure storage account.</span></span>

![Ubicación de la carpeta](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="bb20f-151">Si prefiere mantener estos archivos en un recurso compartido de la red, puede hacerlo.</span><span class="sxs-lookup"><span data-stu-id="bb20f-151">If you prefer to keep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="bb20f-152">Deberá asegurarse de que el recurso de DSC que se usará más adelante tenga acceso y pueda obtener la instalación y la frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="bb20f-152">You just need to ensure that the DSC resource that you will be using later has access and can get the setup and passphrase.</span></span>

## <a name="step-2-create-the-dsc-configuration"></a><span data-ttu-id="bb20f-153">Paso 2: Creación de la configuración de DSC</span><span class="sxs-lookup"><span data-stu-id="bb20f-153">Step 2: Create the DSC configuration</span></span>
<span data-ttu-id="bb20f-154">La instalación depende de WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="bb20f-154">The setup depends on WMF 5.0.</span></span> <span data-ttu-id="bb20f-155">Para que la máquina aplique correctamente la configuración mediante DSC de automatización, es necesario que WMF 5.0 esté presente.</span><span class="sxs-lookup"><span data-stu-id="bb20f-155">For the machine to successfully apply the configuration through Automation DSC, WMF 5.0 needs to be present.</span></span>

<span data-ttu-id="bb20f-156">En el entorno se usa el siguiente ejemplo de configuración de DSC:</span><span class="sxs-lookup"><span data-stu-id="bb20f-156">The environment uses the following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="bb20f-157">La configuración hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bb20f-157">The configuration will do the following:</span></span>

* <span data-ttu-id="bb20f-158">Las variables indicarán a la configuración dónde obtener los archivos binarios para Mobility Service y el agente de máquina virtual de Azure, dónde obtener la frase de contraseña y dónde almacenar la salida.</span><span class="sxs-lookup"><span data-stu-id="bb20f-158">The variables will tell the configuration where to get the binaries for the Mobility service and the Azure VM agent, where to get the passphrase, and where to store the output.</span></span>
* <span data-ttu-id="bb20f-159">La configuración importará el recurso de DSC xPSDesiredStateConfiguration, por lo que puede usar `xRemoteFile` para descargar los archivos del repositorio.</span><span class="sxs-lookup"><span data-stu-id="bb20f-159">The configuration will import the xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` to download the files from the repository.</span></span>
* <span data-ttu-id="bb20f-160">La configuración creará el directorio donde quiere almacenar los archivos binarios.</span><span class="sxs-lookup"><span data-stu-id="bb20f-160">The configuration will create a directory where you want to store the binaries.</span></span>
* <span data-ttu-id="bb20f-161">El recurso "Archive" extraerá los archivos de la carpeta comprimida.</span><span class="sxs-lookup"><span data-stu-id="bb20f-161">The archive resource will extract the files from the zipped folder.</span></span>
* <span data-ttu-id="bb20f-162">El recurso de instalación del paquete instalará Mobility Service desde el instalador UNIFIEDAGENT.EXE con los argumentos específicos.</span><span class="sxs-lookup"><span data-stu-id="bb20f-162">The package Install resource will install the Mobility service from the UNIFIEDAGENT.EXE installer with the specific arguments.</span></span> <span data-ttu-id="bb20f-163">(Habrá que cambiar las variables que construyen los argumentos para que reflejen el entorno).</span><span class="sxs-lookup"><span data-stu-id="bb20f-163">(The variables that construct the arguments need to be changed to reflect your environment.)</span></span>
* <span data-ttu-id="bb20f-164">El recurso AzureAgent del paquete instalará el agente de máquina virtual de Azure, que se recomienda en cada máquina virtual que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="bb20f-164">The package AzureAgent resource will install the Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="bb20f-165">El agente de máquina virtual de Azure también hace posible agregar extensiones a la máquina virtual tras la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="bb20f-165">The Azure VM agent also makes it possible to add extensions to the VM after failover.</span></span>
* <span data-ttu-id="bb20f-166">El recurso o los recursos de servicios garantizan que los servicios de Mobility Service y los servicios de Azure relacionados están siempre en ejecución.</span><span class="sxs-lookup"><span data-stu-id="bb20f-166">The service resource or resources will ensure that the related Mobility services and the Azure services are always running.</span></span>

<span data-ttu-id="bb20f-167">Guarde la configuración como **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="bb20f-167">Save the configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="bb20f-168">No olvide reemplazar CSIP en la configuración para que refleje el servidor de administración real, de forma que el agente se conecte sin problemas y con la frase de contraseña correcta.</span><span class="sxs-lookup"><span data-stu-id="bb20f-168">Remember to replace the CSIP in your configuration to reflect the actual management server, so that the agent will be connected correctly and will use the correct passphrase.</span></span>
>
>

## <a name="step-3-upload-to-automation-dsc"></a><span data-ttu-id="bb20f-169">Paso 3: Carga en DSC de automatización</span><span class="sxs-lookup"><span data-stu-id="bb20f-169">Step 3: Upload to Automation DSC</span></span>
<span data-ttu-id="bb20f-170">Puesto que la configuración de DSC que ha realizado va a importar un módulo de recursos de DSC necesario (xPSDesiredStateConfiguration), debe importar ese módulo en Automatización antes de cargar la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="bb20f-170">Because the DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need to import that module in Automation before you upload the DSC configuration.</span></span>

<span data-ttu-id="bb20f-171">Inicie sesión en su cuenta de Automation, vaya a **Recursos** > **Módulos** y haga clic en **Examinar la galería**.</span><span class="sxs-lookup"><span data-stu-id="bb20f-171">Sign in to your Automation account, browse to **Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="bb20f-172">Aquí puede buscar el módulo e importarlo en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="bb20f-172">Here you can search for the module and import it to your account.</span></span>

![Importar el módulo](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="bb20f-174">Cuando termine, vaya a la máquina donde tiene instalados los módulos de Azure Resource Manager y continúe para importar la configuración de DSC recién creada.</span><span class="sxs-lookup"><span data-stu-id="bb20f-174">When you finish this, go to your machine where you have the Azure Resource Manager modules installed and proceed to import the newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="bb20f-175">Cmdlets de importación</span><span class="sxs-lookup"><span data-stu-id="bb20f-175">Import cmdlets</span></span>
<span data-ttu-id="bb20f-176">En PowerShell, inicie sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb20f-176">In PowerShell, sign in to your Azure subscription.</span></span> <span data-ttu-id="bb20f-177">Modifique los cmdlets para que reflejen el entorno y capturen la información de la cuenta de Automatización en una variable:</span><span class="sxs-lookup"><span data-stu-id="bb20f-177">Modify the cmdlets to reflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="bb20f-178">Cargue la configuración en DSC de Automatización mediante el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bb20f-178">Upload the configuration to Automation DSC by using the following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-the-configuration-in-automation-dsc"></a><span data-ttu-id="bb20f-179">Compilación de la configuración en DSC de Automatización</span><span class="sxs-lookup"><span data-stu-id="bb20f-179">Compile the configuration in Automation DSC</span></span>
<span data-ttu-id="bb20f-180">A continuación, debe compilar la configuración en DSC de Automatización, para poder comenzar a registrar los nodos en ella.</span><span class="sxs-lookup"><span data-stu-id="bb20f-180">Next, you need to compile the configuration in Automation DSC, so that you can start to register nodes to it.</span></span> <span data-ttu-id="bb20f-181">Para conseguirlo, ejecute el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bb20f-181">You achieve that by running the following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="bb20f-182">Esta operación puede tardar unos minutos, porque básicamente se está implementando la configuración en el servicio de extracción de DSC hospedado.</span><span class="sxs-lookup"><span data-stu-id="bb20f-182">This can take a few minutes, because you're basically deploying the configuration to the hosted DSC pull service.</span></span>

<span data-ttu-id="bb20f-183">Después de compilar la configuración, puede recuperar la información de trabajo mediante PowerShell (Get-AzureRmAutomationDscCompilationJob) o el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bb20f-183">After you compile the configuration, you can retrieve the job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using the [Azure portal](https://portal.azure.com/).</span></span>

![Recuperar trabajo](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="bb20f-185">Ahora ya ha publicado y cargado correctamente la configuración de DSC en DSC de Automatización.</span><span class="sxs-lookup"><span data-stu-id="bb20f-185">You have now successfully published and uploaded your DSC configuration to Automation DSC.</span></span>

## <a name="step-4-onboard-machines-to-automation-dsc"></a><span data-ttu-id="bb20f-186">Paso 4: Incorporación de máquinas a DSC de automatización</span><span class="sxs-lookup"><span data-stu-id="bb20f-186">Step 4: Onboard machines to Automation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="bb20f-187">Uno de los requisitos previos para completar este escenario es que las máquinas Windows estén actualizadas con la versión más reciente de WMF.</span><span class="sxs-lookup"><span data-stu-id="bb20f-187">One of the prerequisites for completing this scenario is that your Windows machines are updated with the latest version of WMF.</span></span> <span data-ttu-id="bb20f-188">Puede descargar e instalar la versión correcta para su plataforma desde el [Centro de descarga](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="bb20f-188">You can download and install the correct version for your platform from the [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="bb20f-189">Ahora creará una metaconfiguración de DSC que se aplicará a los nodos.</span><span class="sxs-lookup"><span data-stu-id="bb20f-189">You will now create a metaconfig for DSC that you will apply to your nodes.</span></span> <span data-ttu-id="bb20f-190">Para hacerlo correctamente, se debe recuperar la dirección URL del punto de conexión y la clave principal para la cuenta de Automatización seleccionada en Azure.</span><span class="sxs-lookup"><span data-stu-id="bb20f-190">To succeed with this, you need to retrieve the endpoint URL and the primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="bb20f-191">Puede encontrar estos valores en **Claves** en la hoja **Toda la configuración** de la cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="bb20f-191">You can find these values under **Keys** on the **All settings** blade for the Automation account.</span></span>

![Valores clave](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="bb20f-193">En este ejemplo, tenemos un servidor físico con Windows Server 2012 R2 que queremos proteger con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bb20f-193">In this example, you have a Windows Server 2012 R2 physical server that you want to protect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-the-registry"></a><span data-ttu-id="bb20f-194">Comprobación de operaciones pendientes de cambio de nombre de archivos en el Registro</span><span class="sxs-lookup"><span data-stu-id="bb20f-194">Check for any pending file rename operations in the registry</span></span>
<span data-ttu-id="bb20f-195">Antes de empezar a asociar el servidor al punto de conexión de DSC de Automatización, recomendamos que compruebe las operaciones pendientes de cambio de nombre de archivos en el Registro.</span><span class="sxs-lookup"><span data-stu-id="bb20f-195">Before you start to associate the server with the Automation DSC endpoint, we recommend that you check for any pending file rename operations in the registry.</span></span> <span data-ttu-id="bb20f-196">Podrían impedir que finalizara la configuración al haber un reinicio pendiente.</span><span class="sxs-lookup"><span data-stu-id="bb20f-196">They might prohibit the setup from finishing due to a pending reboot.</span></span>

<span data-ttu-id="bb20f-197">Ejecute el siguiente cmdlet para comprobar que no haya ningún reinicio pendiente en el servidor:</span><span class="sxs-lookup"><span data-stu-id="bb20f-197">Run the following cmdlet to verify that there’s no pending reboot on the server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="bb20f-198">Si no aparecen resultados, puede continuar.</span><span class="sxs-lookup"><span data-stu-id="bb20f-198">If this shows empty, you are OK to proceed.</span></span> <span data-ttu-id="bb20f-199">Si no es así, debe resolverlo reiniciando el servidor durante una ventana de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="bb20f-199">If not, you should address this by rebooting the server during a maintenance window.</span></span>

<span data-ttu-id="bb20f-200">Para aplicar la configuración en el servidor, inicie el Entorno de scripting integrado (ISE) de PowerShell y ejecute el siguiente script.</span><span class="sxs-lookup"><span data-stu-id="bb20f-200">To apply the configuration on the server, start the PowerShell Integrated Scripting Environment (ISE) and run the following script.</span></span> <span data-ttu-id="bb20f-201">Esta es básicamente una configuración local de DSC que indicará al motor del administrador de configuración local que se registre en el servicio DSC de Automatización y recupere la configuración específica (ASRMobilityService.localhost).</span><span class="sxs-lookup"><span data-stu-id="bb20f-201">This is essentially a DSC local configuration that will instruct the Local Configuration Manager engine to register with the Automation DSC service and retrieve the specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="bb20f-202">Esta configuración hará que el motor del administrador de configuración local se registre en DSC de Automatización.</span><span class="sxs-lookup"><span data-stu-id="bb20f-202">This configuration will cause the Local Configuration Manager engine to register itself with Automation DSC.</span></span> <span data-ttu-id="bb20f-203">También determina cómo debe funcionar el motor, qué debe hacer si se produce un desfase de configuración (ApplyAndAutoCorrect) y cómo se debe continuar con la configuración en caso de que sea necesario un reinicio.</span><span class="sxs-lookup"><span data-stu-id="bb20f-203">It will also determine how the engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with the configuration if a reboot is required.</span></span>

<span data-ttu-id="bb20f-204">Después de ejecutar este script, el nodo debe comenzar a registrarse en DSC de Automatización.</span><span class="sxs-lookup"><span data-stu-id="bb20f-204">After you run this script, the node should start to register with Automation DSC.</span></span>

![Registro del nodo en curso](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="bb20f-206">Si vuelve al Portal de Azure, puede ver que ahora aparece el código recién registrado.</span><span class="sxs-lookup"><span data-stu-id="bb20f-206">If you go back to the Azure portal, you can see that the newly registered node has now appeared in the portal.</span></span>

![Nodo registrado en el portal](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="bb20f-208">En el servidor, puede ejecutar el siguiente cmdlet de PowerShell para comprobar que el nodo se ha registrado correctamente:</span><span class="sxs-lookup"><span data-stu-id="bb20f-208">On the server, you can run the following PowerShell cmdlet to verify that the node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="bb20f-209">Después de que se ha extraído la configuración y se ha aplicado al servidor, puede comprobar esto mediante la ejecución del siguiente script:</span><span class="sxs-lookup"><span data-stu-id="bb20f-209">After the configuration has been pulled and applied to the server, you can verify this by running the following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="bb20f-210">La salida muestra que el servidor ha extraído correctamente su configuración:</span><span class="sxs-lookup"><span data-stu-id="bb20f-210">The output shows that the server has successfully pulled its configuration:</span></span>

![Salida](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="bb20f-212">Además, la configuración de Mobility Service tiene su propio registro, que se encuentra en *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="bb20f-212">In addition, the Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="bb20f-213">¡Ya está!</span><span class="sxs-lookup"><span data-stu-id="bb20f-213">That’s it.</span></span> <span data-ttu-id="bb20f-214">Ahora ha implementado y registrado correctamente Mobility Service en la máquina que quiere proteger con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bb20f-214">You have now successfully deployed and registered the Mobility service on the machine that you want to protect by using Site Recovery.</span></span> <span data-ttu-id="bb20f-215">DSC se asegurará de que los servicios necesarios se estén siempre ejecutando.</span><span class="sxs-lookup"><span data-stu-id="bb20f-215">DSC will make sure that the required services are always running.</span></span>

![Implementación correcta](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="bb20f-217">Después de que el servidor de administración detecta que la implementación es correcta, puede configurar la protección y habilitar la replicación en la máquina mediante Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bb20f-217">After the management server detects the successful deployment, you can configure protection and enable replication on the machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="bb20f-218">Uso de DCS en entornos desconectados</span><span class="sxs-lookup"><span data-stu-id="bb20f-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="bb20f-219">Aunque las máquinas no estén conectadas a Internet, puede usar DSC para implementar y configurar Mobility Service en las cargas de trabajo que quiere proteger.</span><span class="sxs-lookup"><span data-stu-id="bb20f-219">If your machines aren’t connected to the Internet, you can still rely on DSC to deploy and configure the Mobility service on the workloads that you want to protect.</span></span>

<span data-ttu-id="bb20f-220">Puede crear instancias de su propio servidor de extracción de DSC en el entorno para proporcionar básicamente las mismas funcionalidades que obtiene de DSC de Automatización.</span><span class="sxs-lookup"><span data-stu-id="bb20f-220">You can instantiate your own DSC pull server in your environment to essentially provide the same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="bb20f-221">Es decir, los clientes extraerán la configuración (después de registrarla) en el punto de conexión de DSC.</span><span class="sxs-lookup"><span data-stu-id="bb20f-221">That is, the clients will pull the configuration (after it's registered) to the DSC endpoint.</span></span> <span data-ttu-id="bb20f-222">Sin embargo, otra opción es insertar manualmente la configuración de DSC en las máquinas, bien localmente o de forma remota.</span><span class="sxs-lookup"><span data-stu-id="bb20f-222">However, another option is to manually push the DSC configuration to your machines, either locally or remotely.</span></span>

<span data-ttu-id="bb20f-223">Tenga en cuenta que en este ejemplo, se ha agregado un parámetro para el nombre del equipo.</span><span class="sxs-lookup"><span data-stu-id="bb20f-223">Note that in this example, there's an added parameter for the computer name.</span></span> <span data-ttu-id="bb20f-224">Los archivos remotos se encuentran ahora en un recurso compartido remoto al que deben poder acceder las máquinas que quiere proteger.</span><span class="sxs-lookup"><span data-stu-id="bb20f-224">The remote files are now located on a remote share that should be accessible by the machines that you want to protect.</span></span> <span data-ttu-id="bb20f-225">El final del script representa la configuración y luego comienza a aplicar la configuración de DSC al equipo de destino.</span><span class="sxs-lookup"><span data-stu-id="bb20f-225">The end of the script enacts the configuration and then starts to apply the DSC configuration to the target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bb20f-226">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bb20f-226">Prerequisites</span></span>
<span data-ttu-id="bb20f-227">Asegúrese de que está instalado el módulo de PowerShell xPSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="bb20f-227">Make sure that the xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="bb20f-228">Para máquinas Windows con WMF 5.0 instalado, puede instalar el módulo xPSDesiredStateConfiguration ejecutando el siguiente cmdlet en las máquinas de destino:</span><span class="sxs-lookup"><span data-stu-id="bb20f-228">For Windows machines where WMF 5.0 is installed, you can install the xPSDesiredStateConfiguration module by running the following cmdlet on the target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="bb20f-229">También puede descargar y guardar el módulo, en caso de que necesite distribuirlo a máquinas Windows que tienen WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="bb20f-229">You can also download and save the module in case you need to distribute it to Windows machines that have WMF 4.0.</span></span> <span data-ttu-id="bb20f-230">Ejecute este cmdlet en una máquina donde esté presente PowerShellGet (WMF 5.0):</span><span class="sxs-lookup"><span data-stu-id="bb20f-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="bb20f-231">También para WMF 4.0, asegúrese de que la [actualización KB2883200 de Windows 8.1](https://www.microsoft.com/download/details.aspx?id=40749) está instalada en las máquinas.</span><span class="sxs-lookup"><span data-stu-id="bb20f-231">Also for WMF 4.0, ensure that the [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on the machines.</span></span>

<span data-ttu-id="bb20f-232">La siguiente configuración se puede insertar en máquinas Windows que tengan WMF 5.0 y WMF 4.0:</span><span class="sxs-lookup"><span data-stu-id="bb20f-232">The following configuration can be pushed to Windows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="bb20f-233">Si quiere crear una instancia de su propio servidor de inserción de DSC en la red corporativa para imitar las funcionalidades que puede obtener en DSC de Automatización, consulte [Configuración de un servidor de extracción web de DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="bb20f-233">If you want to instantiate your own DSC pull server on your corporate network to mimic the capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="bb20f-234">Opcional: Implementación de una configuración de DSC mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bb20f-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="bb20f-235">Este artículo se ha centrado en cómo puede crear su propia configuración de DSC para implementar automáticamente Mobility Service y el agente de máquina virtual de Azure, y asegurarse de que se ejecutan en las máquinas que quiere proteger.</span><span class="sxs-lookup"><span data-stu-id="bb20f-235">This article has focused on how you can create your own DSC configuration to automatically deploy the Mobility service and the Azure VM Agent--and ensure that they are running on the machines that you want to protect.</span></span> <span data-ttu-id="bb20f-236">También tenemos una plantilla de Azure Resource Manager que implementará esta configuración de DSC en una cuenta de Automatización de Azure nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="bb20f-236">We also have an Azure Resource Manager template that will deploy this DSC configuration to a new or existing Azure Automation account.</span></span> <span data-ttu-id="bb20f-237">La plantilla usará parámetros de entrada para crear recursos de Automatización que contendrán las variables de su entorno.</span><span class="sxs-lookup"><span data-stu-id="bb20f-237">The template will use input parameters to create Automation assets that will contain the variables for your environment.</span></span>

<span data-ttu-id="bb20f-238">Después de implementar la plantilla, puede hacer referencia simplemente al paso 4 de esta guía para incorporar las máquinas.</span><span class="sxs-lookup"><span data-stu-id="bb20f-238">After you deploy the template, you can simply refer to step 4 in this guide to onboard your machines.</span></span>

<span data-ttu-id="bb20f-239">La plantilla hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bb20f-239">The template will do the following:</span></span>

1. <span data-ttu-id="bb20f-240">Usar una cuenta existente de Automatización o crear una nueva</span><span class="sxs-lookup"><span data-stu-id="bb20f-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="bb20f-241">Aceptar los parámetros de entrada de:</span><span class="sxs-lookup"><span data-stu-id="bb20f-241">Take input parameters for:</span></span>
   * <span data-ttu-id="bb20f-242">ASRRemoteFile: la ubicación donde se almacena la configuración de Mobility Service</span><span class="sxs-lookup"><span data-stu-id="bb20f-242">ASRRemoteFile--the location where you have stored the Mobility service setup</span></span>
   * <span data-ttu-id="bb20f-243">ASRPassphrase: la ubicación donde ha almacenado el archivo passphrase.txt</span><span class="sxs-lookup"><span data-stu-id="bb20f-243">ASRPassphrase--the location where you have stored the passphrase.txt file</span></span>
   * <span data-ttu-id="bb20f-244">ASRCSEndpoint: la dirección IP del servidor de administración</span><span class="sxs-lookup"><span data-stu-id="bb20f-244">ASRCSEndpoint--the IP address of your management server</span></span>
3. <span data-ttu-id="bb20f-245">Importar el módulo xPSDesiredStateConfiguration PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb20f-245">Import the xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="bb20f-246">Crear y compilar la configuración de DSC</span><span class="sxs-lookup"><span data-stu-id="bb20f-246">Create and compile the DSC configuration</span></span>

<span data-ttu-id="bb20f-247">Todos los pasos anteriores se realizarán en el orden correcto, para que pueda comenzar a incorporar sus máquinas que reciban protección.</span><span class="sxs-lookup"><span data-stu-id="bb20f-247">All the preceding steps will happen in the right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="bb20f-248">La plantilla, con instrucciones para la implementación, se encuentra en [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="bb20f-248">The template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="bb20f-249">Implemente la plantilla mediante PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bb20f-249">Deploy the template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="bb20f-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb20f-250">Next steps</span></span>
<span data-ttu-id="bb20f-251">Después de implementar los agentes de Mobility Service, puede [habilitar la replicación](site-recovery-vmware-to-azure.md) para las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bb20f-251">After you deploy the Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for the virtual machines.</span></span>
