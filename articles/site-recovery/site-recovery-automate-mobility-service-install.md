---
title: "Hola aaaDeploy servicio de movilidad de recuperación de sitio con el DSC de automatización de Azure | Documentos de Microsoft"
description: "Describe cómo implementar toouse DSC de automatización de Azure tooautomatically servicio de movilidad de recuperación del sitio de Azure de Hola y el agente de Azure para VM de VMware y tooAzure de replicación del servidor físico"
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
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="00ab6-103">Implementar el servicio de movilidad Hola con DSC de automatización de Azure para la replicación de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="00ab6-103">Deploy hello Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="00ab6-104">En Operations Management Suite, le proporcionamos una completa solución de copia de seguridad y recuperación ante desastres que puede usar como parte de su plan de continuidad empresarial.</span><span class="sxs-lookup"><span data-stu-id="00ab6-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="00ab6-105">Comenzamos este viaje con Hyper-V usando Réplica de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="00ab6-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="00ab6-106">Pero tenemos toosupport expandido una instalación heterogénea porque los clientes tienen varias plataformas e hipervisores en sus nubes.</span><span class="sxs-lookup"><span data-stu-id="00ab6-106">But we have expanded toosupport a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="00ab6-107">Si se ejecutan cargas de trabajo de VMware o en servidores físicos de hoy en día, un servidor de administración ejecuta todos de hello componentes de Azure Site Recovery en su entorno toohandle Hola comunicación y datos de replicación con Azure, cuando Azure es el destino.</span><span class="sxs-lookup"><span data-stu-id="00ab6-107">If you are running VMware workloads and/or physical servers today, a management server runs all of hello Azure Site Recovery components in your environment toohandle hello communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="00ab6-108">Implementar el servicio de movilidad de recuperación de sitio de hello mediante DSC de automatización</span><span class="sxs-lookup"><span data-stu-id="00ab6-108">Deploy hello Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="00ab6-109">Para comenzar, vamos a realizar un desglose rápido de lo que hace este servidor de administración.</span><span class="sxs-lookup"><span data-stu-id="00ab6-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="00ab6-110">servidor de administración de Hello ejecuta varios roles de servidor.</span><span class="sxs-lookup"><span data-stu-id="00ab6-110">hello management server runs several server roles.</span></span> <span data-ttu-id="00ab6-111">Uno de ellos es el de *configuración*, que coordina la comunicación y administra los procesos de replicación y recuperación de datos.</span><span class="sxs-lookup"><span data-stu-id="00ab6-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="00ab6-112">Además, Hola *proceso* rol actúa como una puerta de enlace de replicación.</span><span class="sxs-lookup"><span data-stu-id="00ab6-112">In addition, hello *process* role acts as a replication gateway.</span></span> <span data-ttu-id="00ab6-113">Esta función recibe datos de replicación de máquinas de origen protegido, optimiza con almacenamiento en caché, la compresión y cifrado y, a continuación, lo envía tooan cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="00ab6-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it tooan Azure storage account.</span></span> <span data-ttu-id="00ab6-114">Una de las funciones hello para el rol de proceso de hello también es toopush instalación de las máquinas de tooprotected de servicio de movilidad de Hola y realizar la detección automática de máquinas virtuales de VMware.</span><span class="sxs-lookup"><span data-stu-id="00ab6-114">One of hello functions for hello process role is also toopush installation of hello Mobility service tooprotected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="00ab6-115">Si se produce una conmutación por recuperación de Azure, Hola *destino maestro* rol controlará los datos de replicación de hello como parte de esta operación.</span><span class="sxs-lookup"><span data-stu-id="00ab6-115">If there's a failback from Azure, hello *master target* role will handle hello replication data as part of this operation.</span></span>

<span data-ttu-id="00ab6-116">Para las máquinas de hello protegido, se basan en Hola *servicio de movilidad*.</span><span class="sxs-lookup"><span data-stu-id="00ab6-116">For hello protected machines, we rely on hello *Mobility service*.</span></span> <span data-ttu-id="00ab6-117">Este componente está implementado tooevery máquina (VM de VMware o servidor físico) que desea tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="00ab6-117">This component is deployed tooevery machine (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="00ab6-118">Captura escrituras de datos en la máquina de Hola y reenvía el servidor de administración de toohello (rol de proceso).</span><span class="sxs-lookup"><span data-stu-id="00ab6-118">It captures data writes on hello machine and forwards them toohello management server (process role).</span></span>

<span data-ttu-id="00ab6-119">Cuando está trabajando con la continuidad del negocio, es importante toounderstand las cargas de trabajo, la infraestructura y los componentes de hello implicados.</span><span class="sxs-lookup"><span data-stu-id="00ab6-119">When you're dealing with business continuity, it's important toounderstand your workloads, your infrastructure, and hello components involved.</span></span> <span data-ttu-id="00ab6-120">A continuación, puede cumplir los requisitos de hello para el objetivo de tiempo de recuperación (RTO) y objetivo de punto de recuperación (RPO).</span><span class="sxs-lookup"><span data-stu-id="00ab6-120">You can then meet hello requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="00ab6-121">En este contexto, servicio de movilidad de hello es tooensuring clave que se protegen las cargas de trabajo tal como se esperaría.</span><span class="sxs-lookup"><span data-stu-id="00ab6-121">In this context, hello Mobility service is key tooensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="00ab6-122">De modo que, ¿cómo puede garantizar, de una forma optimizada, que dispone de una configuración protegida confiable con la ayuda de algunos componentes de Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="00ab6-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="00ab6-123">Este artículo proporciona un ejemplo de cómo puede usar Azure Automation estado configuración deseado (DSC), junto con la recuperación del sitio, tooensure que:</span><span class="sxs-lookup"><span data-stu-id="00ab6-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, tooensure that:</span></span>

* <span data-ttu-id="00ab6-124">servicio de movilidad de Hola y el agente de máquina virtual de Azure son máquinas con Windows toohello implementados que desea tooprotect.</span><span class="sxs-lookup"><span data-stu-id="00ab6-124">hello Mobility service and Azure VM agent are deployed toohello Windows machines that you want tooprotect.</span></span>
* <span data-ttu-id="00ab6-125">servicio de movilidad de Hola y el agente de máquina virtual de Azure siempre se ejecutan cuando Azure es el destino de replicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-125">hello Mobility service and Azure VM agent are always running when Azure is hello replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00ab6-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="00ab6-126">Prerequisites</span></span>
* <span data-ttu-id="00ab6-127">Un programa de instalación de repositorio toostore Hola necesario</span><span class="sxs-lookup"><span data-stu-id="00ab6-127">A repository toostore hello required setup</span></span>
* <span data-ttu-id="00ab6-128">Un tooregister de frase de contraseña de repositorio toostore Hola necesario con el servidor de administración de Hola</span><span class="sxs-lookup"><span data-stu-id="00ab6-128">A repository toostore hello required passphrase tooregister with hello management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="00ab6-129">Se genera una frase de contraseña única para cada servidor de administración.</span><span class="sxs-lookup"><span data-stu-id="00ab6-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="00ab6-130">Si va a toodeploy varios servidores de administración, tiene tooensure ese Hola correcto de frase de contraseña se almacena en el archivo de hello passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="00ab6-130">If you are going toodeploy multiple management servers, you have tooensure that hello correct passphrase is stored in hello passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="00ab6-131">Windows Management Framework (WMF) 5.0 instalado en los equipos de Hola que quiere tooenable de protección (un requisito para DSC de automatización)</span><span class="sxs-lookup"><span data-stu-id="00ab6-131">Windows Management Framework (WMF) 5.0 installed on hello machines that you want tooenable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="00ab6-132">Si desea que las máquinas de DSC para Windows toouse que tienen WMF 4.0 instalado, vea la sección de hello [DSC de uso en entornos desconectados](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="00ab6-132">If you want toouse DSC for Windows machines that have WMF 4.0 installed, see hello section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="00ab6-133">servicio de movilidad de Hello puede instalarse mediante la línea de comandos de Hola y acepta varios argumentos.</span><span class="sxs-lookup"><span data-stu-id="00ab6-133">hello Mobility service can be installed through hello command line and accepts several arguments.</span></span> <span data-ttu-id="00ab6-134">Por eso necesita los archivos binarios de toohave Hola (después de extraer el programa de instalación) y almacenarlas en un lugar donde se pueden recuperar mediante el uso de una configuración DSC.</span><span class="sxs-lookup"><span data-stu-id="00ab6-134">That’s why you need toohave hello binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="00ab6-135">Paso 1: Extracción de los archivos binarios</span><span class="sxs-lookup"><span data-stu-id="00ab6-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="00ab6-136">archivos de hello tooextract que necesite para este programa de instalación, busque toohello después de directorio en el servidor de administración:</span><span class="sxs-lookup"><span data-stu-id="00ab6-136">tooextract hello files that you need for this setup, browse toohello following directory on your management server:</span></span>

    <span data-ttu-id="00ab6-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="00ab6-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="00ab6-138">En esta carpeta, debería ver un archivo MSI denominado:</span><span class="sxs-lookup"><span data-stu-id="00ab6-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="00ab6-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="00ab6-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="00ab6-140">Usar hello después de instalador de hello tooextract de comando:</span><span class="sxs-lookup"><span data-stu-id="00ab6-140">Use hello following command tooextract hello installer:</span></span>

    <span data-ttu-id="00ab6-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="00ab6-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="00ab6-142">Seleccione todos los archivos y enviarlos tooa de carpeta comprimida (zip).</span><span class="sxs-lookup"><span data-stu-id="00ab6-142">Select all files and send them tooa compressed (zipped) folder.</span></span>

<span data-ttu-id="00ab6-143">Ahora dispone de los archivos binarios de Hola que necesita el programa de instalación de tooautomate Hola de hello servicio de movilidad mediante el uso de DSC de automatización.</span><span class="sxs-lookup"><span data-stu-id="00ab6-143">You now have hello binaries that you need tooautomate hello setup of hello Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="00ab6-144">Frase de contraseña</span><span class="sxs-lookup"><span data-stu-id="00ab6-144">Passphrase</span></span>
<span data-ttu-id="00ab6-145">A continuación, deberá toodetermine donde desea tooplace esta carpeta comprimida.</span><span class="sxs-lookup"><span data-stu-id="00ab6-145">Next, you need toodetermine where you want tooplace this zipped folder.</span></span> <span data-ttu-id="00ab6-146">Puede usar una cuenta de almacenamiento de Azure, como se muestra más adelante, toostore Hola frase de contraseña que necesita para el programa de instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-146">You can use an Azure storage account, as shown later, toostore hello passphrase that you need for hello setup.</span></span> <span data-ttu-id="00ab6-147">agente de Hello, a continuación, se registrará con el servidor de administración de hello como parte del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-147">hello agent will then register with hello management server as part of hello process.</span></span>

<span data-ttu-id="00ab6-148">frase de contraseña de Hola que obtuvo al implementar el servidor de administración de Hola se puede guardar archivo de texto tooa como passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="00ab6-148">hello passphrase that you got when you deployed hello management server can be saved tooa text file as passphrase.txt.</span></span>

<span data-ttu-id="00ab6-149">Coloque la carpeta comprimida de Hola y Hola frase de contraseña en un contenedor dedicado Hola cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="00ab6-149">Place both hello zipped folder and hello passphrase in a dedicated container in hello Azure storage account.</span></span>

![Ubicación de la carpeta](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="00ab6-151">Si prefiere tookeep estos archivos en un recurso compartido de la red, puede hacerlo.</span><span class="sxs-lookup"><span data-stu-id="00ab6-151">If you prefer tookeep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="00ab6-152">Solo necesita tooensure que el recurso de hello DSC que se va a usar más adelante tiene acceso y puede obtener el programa de instalación de Hola y la frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="00ab6-152">You just need tooensure that hello DSC resource that you will be using later has access and can get hello setup and passphrase.</span></span>

## <a name="step-2-create-hello-dsc-configuration"></a><span data-ttu-id="00ab6-153">Paso 2: Crear la configuración de hello DSC</span><span class="sxs-lookup"><span data-stu-id="00ab6-153">Step 2: Create hello DSC configuration</span></span>
<span data-ttu-id="00ab6-154">el programa de instalación de Hello depende de WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="00ab6-154">hello setup depends on WMF 5.0.</span></span> <span data-ttu-id="00ab6-155">Para hello máquina toosuccessfully aplicar configuración de Hola a través de DSC de automatización, WMF 5.0 debe toobe presente.</span><span class="sxs-lookup"><span data-stu-id="00ab6-155">For hello machine toosuccessfully apply hello configuration through Automation DSC, WMF 5.0 needs toobe present.</span></span>

<span data-ttu-id="00ab6-156">entorno de Hello usa Hola siguiente configuración de DSC de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="00ab6-156">hello environment uses hello following example DSC configuration:</span></span>

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
<span data-ttu-id="00ab6-157">configuración Hola hará lo siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="00ab6-157">hello configuration will do hello following:</span></span>

* <span data-ttu-id="00ab6-158">variables de Hello indicará configuración Hola donde tooget Hola binarios para el servicio de movilidad de Hola y el agente de máquina virtual de Azure de hello, que tooget Hola frase de contraseña, y donde toostore Hola de salida.</span><span class="sxs-lookup"><span data-stu-id="00ab6-158">hello variables will tell hello configuration where tooget hello binaries for hello Mobility service and hello Azure VM agent, where tooget hello passphrase, and where toostore hello output.</span></span>
* <span data-ttu-id="00ab6-159">Hello configuración importará recursos xPSDesiredStateConfiguration DSC de hello, para que pueda utilizar `xRemoteFile` archivos de hello toodownload del repositorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-159">hello configuration will import hello xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` toodownload hello files from hello repository.</span></span>
* <span data-ttu-id="00ab6-160">configuración de Hello creará un directorio donde desea que los archivos binarios de toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-160">hello configuration will create a directory where you want toostore hello binaries.</span></span>
* <span data-ttu-id="00ab6-161">recurso archive de Hello extraerá archivos Hola desde la carpeta comprimida de Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-161">hello archive resource will extract hello files from hello zipped folder.</span></span>
* <span data-ttu-id="00ab6-162">recursos de instalación de paquete de Hola instalarán el servicio de movilidad de Hola de hello UNIFIEDAGENT. Instalador del archivo EXE con argumentos específicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-162">hello package Install resource will install hello Mobility service from hello UNIFIEDAGENT.EXE installer with hello specific arguments.</span></span> <span data-ttu-id="00ab6-163">(las variables de Hola que construcción argumentos Hola necesitan tooreflect toobe cambiar su entorno).</span><span class="sxs-lookup"><span data-stu-id="00ab6-163">(hello variables that construct hello arguments need toobe changed tooreflect your environment.)</span></span>
* <span data-ttu-id="00ab6-164">paquete de Hello AzureAgent recurso instalará el agente de máquina virtual de Azure hello, que se recomienda en cada máquina virtual que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="00ab6-164">hello package AzureAgent resource will install hello Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="00ab6-165">agente de máquina virtual de Azure de Hello también hace posible tooadd extensiones toohello VM después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="00ab6-165">hello Azure VM agent also makes it possible tooadd extensions toohello VM after failover.</span></span>
* <span data-ttu-id="00ab6-166">Hello servicio o los recursos garantizará que Hola relacionados con servicios de movilidad y hello servicios de Azure se ejecutan siempre.</span><span class="sxs-lookup"><span data-stu-id="00ab6-166">hello service resource or resources will ensure that hello related Mobility services and hello Azure services are always running.</span></span>

<span data-ttu-id="00ab6-167">Guardar configuración de hello como **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="00ab6-167">Save hello configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="00ab6-168">Recuerde tooreplace hello CSIP en el servidor de administración reales de configuración tooreflect hello, para que se conectará correctamente hello agente y usará la frase de contraseña correcta Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-168">Remember tooreplace hello CSIP in your configuration tooreflect hello actual management server, so that hello agent will be connected correctly and will use hello correct passphrase.</span></span>
>
>

## <a name="step-3-upload-tooautomation-dsc"></a><span data-ttu-id="00ab6-169">Paso 3: Cargar tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="00ab6-169">Step 3: Upload tooAutomation DSC</span></span>
<span data-ttu-id="00ab6-170">Como configuración de hello DSC realizados importará un módulo de recursos de DSC necesario (xPSDesiredStateConfiguration), deberá tooimport ese módulo en la automatización de antes de cargar la configuración de hello DSC.</span><span class="sxs-lookup"><span data-stu-id="00ab6-170">Because hello DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need tooimport that module in Automation before you upload hello DSC configuration.</span></span>

<span data-ttu-id="00ab6-171">Inicio de sesión tooyour cuenta de automatización, examinar demasiado**activos** > **módulos**y haga clic en **explorar la galería**.</span><span class="sxs-lookup"><span data-stu-id="00ab6-171">Sign in tooyour Automation account, browse too**Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="00ab6-172">Aquí puede buscar Hola módulo e importarlo tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="00ab6-172">Here you can search for hello module and import it tooyour account.</span></span>

![Importar el módulo](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="00ab6-174">Cuando termine esta operación, ir tooyour máquina donde haya módulos de Azure Resource Manager Hola instalados y continuar tooimport Hola que acaba de crear la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="00ab6-174">When you finish this, go tooyour machine where you have hello Azure Resource Manager modules installed and proceed tooimport hello newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="00ab6-175">Cmdlets de importación</span><span class="sxs-lookup"><span data-stu-id="00ab6-175">Import cmdlets</span></span>
<span data-ttu-id="00ab6-176">En PowerShell, inicie sesión en tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="00ab6-176">In PowerShell, sign in tooyour Azure subscription.</span></span> <span data-ttu-id="00ab6-177">Modificar el entorno de hello cmdlets tooreflect y capturar información de su cuenta de automatización en una variable:</span><span class="sxs-lookup"><span data-stu-id="00ab6-177">Modify hello cmdlets tooreflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="00ab6-178">Cargar configuración de hello tooAutomation DSC mediante Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="00ab6-178">Upload hello configuration tooAutomation DSC by using hello following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a><span data-ttu-id="00ab6-179">Compilar Hola configuración de DSC de automatización</span><span class="sxs-lookup"><span data-stu-id="00ab6-179">Compile hello configuration in Automation DSC</span></span>
<span data-ttu-id="00ab6-180">A continuación, necesita toocompile Hola una configuración de DSC de automatización, para que pueda empezar tooregister nodos tooit.</span><span class="sxs-lookup"><span data-stu-id="00ab6-180">Next, you need toocompile hello configuration in Automation DSC, so that you can start tooregister nodes tooit.</span></span> <span data-ttu-id="00ab6-181">Lograr ejecutando Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="00ab6-181">You achieve that by running hello following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="00ab6-182">Esto puede tardar unos minutos, ya que básicamente está implementando el servicio de extracción de DSC de hello configuración toohello hospedado.</span><span class="sxs-lookup"><span data-stu-id="00ab6-182">This can take a few minutes, because you're basically deploying hello configuration toohello hosted DSC pull service.</span></span>

<span data-ttu-id="00ab6-183">Después de compilar la configuración de hello, puede recuperar información del trabajo de hello mediante PowerShell (Get-AzureRmAutomationDscCompilationJob) o mediante el uso de hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="00ab6-183">After you compile hello configuration, you can retrieve hello job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using hello [Azure portal](https://portal.azure.com/).</span></span>

![Recuperar trabajo](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="00ab6-185">Ahora ha publicado y cargar su tooAutomation de configuración de DSC DSC.</span><span class="sxs-lookup"><span data-stu-id="00ab6-185">You have now successfully published and uploaded your DSC configuration tooAutomation DSC.</span></span>

## <a name="step-4-onboard-machines-tooautomation-dsc"></a><span data-ttu-id="00ab6-186">Paso 4: Incorporar máquinas tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="00ab6-186">Step 4: Onboard machines tooAutomation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="00ab6-187">Uno de los requisitos previos de Hola para completar este escenario es que los equipos de Windows se actualizan con la versión más reciente de Hola de WMF.</span><span class="sxs-lookup"><span data-stu-id="00ab6-187">One of hello prerequisites for completing this scenario is that your Windows machines are updated with hello latest version of WMF.</span></span> <span data-ttu-id="00ab6-188">Puede descargar e instalar la versión correcta de Hola para su plataforma de hello [centro de descarga de](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="00ab6-188">You can download and install hello correct version for your platform from hello [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="00ab6-189">Ahora creará una metaconfig de DSC que se aplicarán tooyour nodos.</span><span class="sxs-lookup"><span data-stu-id="00ab6-189">You will now create a metaconfig for DSC that you will apply tooyour nodes.</span></span> <span data-ttu-id="00ab6-190">toosucceed con esto, debe tooretrieve Hola extremo hello y dirección URL de clave principal para la cuenta de automatización seleccionada en Azure.</span><span class="sxs-lookup"><span data-stu-id="00ab6-190">toosucceed with this, you need tooretrieve hello endpoint URL and hello primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="00ab6-191">Puede encontrar estos valores en **claves** en hello **toda la configuración de** hoja para hello cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="00ab6-191">You can find these values under **Keys** on hello **All settings** blade for hello Automation account.</span></span>

![Valores clave](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="00ab6-193">En este ejemplo, tiene un servidor físico de Windows Server 2012 R2 que desea que tooprotect mediante el uso de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="00ab6-193">In this example, you have a Windows Server 2012 R2 physical server that you want tooprotect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a><span data-ttu-id="00ab6-194">Busque todas las operaciones de cambio de nombre de archivo en el registro de hello pendientes</span><span class="sxs-lookup"><span data-stu-id="00ab6-194">Check for any pending file rename operations in hello registry</span></span>
<span data-ttu-id="00ab6-195">Antes de iniciar tooassociate Hola server con el punto de conexión de hello DSC de automatización, se recomienda que compruebe las todas las operaciones de cambio de nombre de archivo en el registro de hello pendientes.</span><span class="sxs-lookup"><span data-stu-id="00ab6-195">Before you start tooassociate hello server with hello Automation DSC endpoint, we recommend that you check for any pending file rename operations in hello registry.</span></span> <span data-ttu-id="00ab6-196">Puede impedir que el programa de instalación de hello finalizase debido tooa reinicio pendiente.</span><span class="sxs-lookup"><span data-stu-id="00ab6-196">They might prohibit hello setup from finishing due tooa pending reboot.</span></span>

<span data-ttu-id="00ab6-197">Ejecute hello después tooverify de cmdlet que no hay ningún reinicio pendiente en el servidor de hello:</span><span class="sxs-lookup"><span data-stu-id="00ab6-197">Run hello following cmdlet tooverify that there’s no pending reboot on hello server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="00ab6-198">Si esto se muestra vacía, son tooproceed Aceptar.</span><span class="sxs-lookup"><span data-stu-id="00ab6-198">If this shows empty, you are OK tooproceed.</span></span> <span data-ttu-id="00ab6-199">De lo contrario, se debe solucionar este problema, reinicie el equipo servidor de Hola durante una ventana de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="00ab6-199">If not, you should address this by rebooting hello server during a maintenance window.</span></span>

<span data-ttu-id="00ab6-200">configuración de Hola de tooapply en servidor hello, iniciar PowerShell Integrated Scripting Environment (ISE) de Hola y ejecute la siguiente secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-200">tooapply hello configuration on hello server, start hello PowerShell Integrated Scripting Environment (ISE) and run hello following script.</span></span> <span data-ttu-id="00ab6-201">Esto es básicamente una configuración local DSC que se indique a tooregister de motor de administrador de configuración Local de hello con hello servicio DSC de automatización y recuperar la configuración específica de hello (ASRMobilityService.localhost).</span><span class="sxs-lookup"><span data-stu-id="00ab6-201">This is essentially a DSC local configuration that will instruct hello Local Configuration Manager engine tooregister with hello Automation DSC service and retrieve hello specific configuration (ASRMobilityService.localhost).</span></span>

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

<span data-ttu-id="00ab6-202">Esta configuración producirá Hola Administrador de configuración Local tooregister motor propio con DSC de automatización.</span><span class="sxs-lookup"><span data-stu-id="00ab6-202">This configuration will cause hello Local Configuration Manager engine tooregister itself with Automation DSC.</span></span> <span data-ttu-id="00ab6-203">También determinará cómo debe funcionar el motor de hello, lo que debería hacer si no hay un desfase de la configuración (ApplyAndAutoCorrect) y cómo debe continuar con la configuración de hello si es necesario reiniciar.</span><span class="sxs-lookup"><span data-stu-id="00ab6-203">It will also determine how hello engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with hello configuration if a reboot is required.</span></span>

<span data-ttu-id="00ab6-204">Después de ejecutar este script, nodo de hello debe comenzar tooregister con DSC de automatización.</span><span class="sxs-lookup"><span data-stu-id="00ab6-204">After you run this script, hello node should start tooregister with Automation DSC.</span></span>

![Registro del nodo en curso](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="00ab6-206">Si vuelve toohello portal de Azure, puede ver ese nodo recién registrado Hola ahora ha aparecido en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-206">If you go back toohello Azure portal, you can see that hello newly registered node has now appeared in hello portal.</span></span>

![Nodo registrado en el portal de Hola](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="00ab6-208">En el servidor de hello, puede ejecutar Hola después PowerShell tooverify de cmdlet que Hola nodo se ha registrado correctamente:</span><span class="sxs-lookup"><span data-stu-id="00ab6-208">On hello server, you can run hello following PowerShell cmdlet tooverify that hello node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="00ab6-209">Después de configuración de hello toohello extraída y aplicado server, puede comprobarlo ejecutando Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="00ab6-209">After hello configuration has been pulled and applied toohello server, you can verify this by running hello following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="00ab6-210">salida de Hello muestra que ese servidor Hola extrajo correctamente su configuración:</span><span class="sxs-lookup"><span data-stu-id="00ab6-210">hello output shows that hello server has successfully pulled its configuration:</span></span>

![Salida](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="00ab6-212">Además, el programa de instalación del servicio de movilidad de hello tiene su propio registro que se pueden encontrar en *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="00ab6-212">In addition, hello Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="00ab6-213">¡Ya está!</span><span class="sxs-lookup"><span data-stu-id="00ab6-213">That’s it.</span></span> <span data-ttu-id="00ab6-214">Ahora ha implementado y registrado el servicio de movilidad Hola Hola máquina que tooprotect mediante el uso de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="00ab6-214">You have now successfully deployed and registered hello Mobility service on hello machine that you want tooprotect by using Site Recovery.</span></span> <span data-ttu-id="00ab6-215">DSC se asegurará de que siempre están ejecutando los servicios de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="00ab6-215">DSC will make sure that hello required services are always running.</span></span>

![Implementación correcta](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="00ab6-217">Después de que el servidor de administración de hello detecta una implementación correcta hello, puede configurar la protección y habilitar la replicación en la máquina de hello mediante el uso de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="00ab6-217">After hello management server detects hello successful deployment, you can configure protection and enable replication on hello machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="00ab6-218">Uso de DCS en entornos desconectados</span><span class="sxs-lookup"><span data-stu-id="00ab6-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="00ab6-219">Si los equipos no están conectado toohello Internet, puede confiar en DSC toodeploy y configurar el servicio de movilidad de hello en las cargas de trabajo de Hola que desea tooprotect.</span><span class="sxs-lookup"><span data-stu-id="00ab6-219">If your machines aren’t connected toohello Internet, you can still rely on DSC toodeploy and configure hello Mobility service on hello workloads that you want tooprotect.</span></span>

<span data-ttu-id="00ab6-220">Puede crear una instancia de su propio servidor de extracción de DSC en su entorno tooessentially proporcionar Hola mismas capacidades que obtendrá de DSC de automatización.</span><span class="sxs-lookup"><span data-stu-id="00ab6-220">You can instantiate your own DSC pull server in your environment tooessentially provide hello same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="00ab6-221">Es decir, los clientes de hello extraerá configuración hello (después de registrarla) toohello DSC extremo.</span><span class="sxs-lookup"><span data-stu-id="00ab6-221">That is, hello clients will pull hello configuration (after it's registered) toohello DSC endpoint.</span></span> <span data-ttu-id="00ab6-222">Sin embargo, otra opción es toomanually inserción Hola DSC configuración tooyour las máquinas, tanto local como remotamente.</span><span class="sxs-lookup"><span data-stu-id="00ab6-222">However, another option is toomanually push hello DSC configuration tooyour machines, either locally or remotely.</span></span>

<span data-ttu-id="00ab6-223">Tenga en cuenta que en este ejemplo, es un parámetro agregado hello como nombre del equipo.</span><span class="sxs-lookup"><span data-stu-id="00ab6-223">Note that in this example, there's an added parameter for hello computer name.</span></span> <span data-ttu-id="00ab6-224">archivos remotos Hola se encuentran en un recurso compartido remoto debe ser accesible por máquinas de Hola que desea tooprotect.</span><span class="sxs-lookup"><span data-stu-id="00ab6-224">hello remote files are now located on a remote share that should be accessible by hello machines that you want tooprotect.</span></span> <span data-ttu-id="00ab6-225">final de Hello del script de Hola aplica la configuración de hello y, a continuación, inicia el equipo de destino de tooapply Hola DSC configuración toohello.</span><span class="sxs-lookup"><span data-stu-id="00ab6-225">hello end of hello script enacts hello configuration and then starts tooapply hello DSC configuration toohello target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="00ab6-226">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="00ab6-226">Prerequisites</span></span>
<span data-ttu-id="00ab6-227">Asegúrese de que ese módulo de PowerShell de hello xPSDesiredStateConfiguration está instalado.</span><span class="sxs-lookup"><span data-stu-id="00ab6-227">Make sure that hello xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="00ab6-228">Para las máquinas de Windows está instalado WMF 5.0, puede instalar el módulo xPSDesiredStateConfiguration de hello ejecutando Hola siguiente cmdlet de equipos de destino de hello:</span><span class="sxs-lookup"><span data-stu-id="00ab6-228">For Windows machines where WMF 5.0 is installed, you can install hello xPSDesiredStateConfiguration module by running hello following cmdlet on hello target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="00ab6-229">También puede descargar y guardar el módulo de Hola por si tuviera que toodistribute lo tooWindows máquinas que tengan WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="00ab6-229">You can also download and save hello module in case you need toodistribute it tooWindows machines that have WMF 4.0.</span></span> <span data-ttu-id="00ab6-230">Ejecute este cmdlet en una máquina donde esté presente PowerShellGet (WMF 5.0):</span><span class="sxs-lookup"><span data-stu-id="00ab6-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="00ab6-231">También para WMF 4.0, asegúrese de que hello [actualización de Windows 8.1 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) se instala en equipos de Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-231">Also for WMF 4.0, ensure that hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on hello machines.</span></span>

<span data-ttu-id="00ab6-232">Hello configuración siguiente se puede insertar tooWindows máquinas que tengan WMF 5.0 y WMF 4.0:</span><span class="sxs-lookup"><span data-stu-id="00ab6-232">hello following configuration can be pushed tooWindows machines that have WMF 5.0 and WMF 4.0:</span></span>

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

<span data-ttu-id="00ab6-233">Si desea tooinstantiate su propio servidor de extracción de DSC en sus capacidades de hello toomimic de red corporativa que puede obtener de DSC de automatización, vea [configurar un servidor de extracción de DSC web](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="00ab6-233">If you want tooinstantiate your own DSC pull server on your corporate network toomimic hello capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="00ab6-234">Opcional: Implementación de una configuración de DSC mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="00ab6-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="00ab6-235">En este artículo se centra en cómo puede crear su propio tooautomatically de configuración de DSC implementar hello Azure VM Agent--y servicio de movilidad de Hola y asegúrese de que se ejecutan en máquinas de Hola que desea tooprotect.</span><span class="sxs-lookup"><span data-stu-id="00ab6-235">This article has focused on how you can create your own DSC configuration tooautomatically deploy hello Mobility service and hello Azure VM Agent--and ensure that they are running on hello machines that you want tooprotect.</span></span> <span data-ttu-id="00ab6-236">También tenemos una plantilla de administrador de recursos de Azure que implementará esta DSC configuración tooa cuenta nueva o existente automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="00ab6-236">We also have an Azure Resource Manager template that will deploy this DSC configuration tooa new or existing Azure Automation account.</span></span> <span data-ttu-id="00ab6-237">plantilla de Hello usará activos de automatización de toocreate de parámetros de entrada que contienen las variables de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="00ab6-237">hello template will use input parameters toocreate Automation assets that will contain hello variables for your environment.</span></span>

<span data-ttu-id="00ab6-238">Después de implementar la plantilla de hello, simplemente puede consultar toostep 4 en esta guía tooonboard las máquinas.</span><span class="sxs-lookup"><span data-stu-id="00ab6-238">After you deploy hello template, you can simply refer toostep 4 in this guide tooonboard your machines.</span></span>

<span data-ttu-id="00ab6-239">plantilla Hola hará lo siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="00ab6-239">hello template will do hello following:</span></span>

1. <span data-ttu-id="00ab6-240">Usar una cuenta existente de Automatización o crear una nueva</span><span class="sxs-lookup"><span data-stu-id="00ab6-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="00ab6-241">Aceptar los parámetros de entrada de:</span><span class="sxs-lookup"><span data-stu-id="00ab6-241">Take input parameters for:</span></span>
   * <span data-ttu-id="00ab6-242">ASRRemoteFile--ubicación hello en el que haya almacenado el programa de instalación del servicio de movilidad de Hola</span><span class="sxs-lookup"><span data-stu-id="00ab6-242">ASRRemoteFile--hello location where you have stored hello Mobility service setup</span></span>
   * <span data-ttu-id="00ab6-243">ASRPassphrase: ubicación de Hola que haya almacenado el archivo de hello passphrase.txt</span><span class="sxs-lookup"><span data-stu-id="00ab6-243">ASRPassphrase--hello location where you have stored hello passphrase.txt file</span></span>
   * <span data-ttu-id="00ab6-244">ASRCSEndpoint--dirección IP de saludo del servidor de administración</span><span class="sxs-lookup"><span data-stu-id="00ab6-244">ASRCSEndpoint--hello IP address of your management server</span></span>
3. <span data-ttu-id="00ab6-245">Importar el módulo de PowerShell de hello xPSDesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="00ab6-245">Import hello xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="00ab6-246">Crear y compilar la configuración de DSC Hola</span><span class="sxs-lookup"><span data-stu-id="00ab6-246">Create and compile hello DSC configuration</span></span>

<span data-ttu-id="00ab6-247">Hola todos los pasos anteriores se realizará en el orden correcto de hello, para que pueda comenzar la incorporación de las máquinas para la protección.</span><span class="sxs-lookup"><span data-stu-id="00ab6-247">All hello preceding steps will happen in hello right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="00ab6-248">plantilla de Hello, con instrucciones para la implementación, se encuentra en [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="00ab6-248">hello template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="00ab6-249">Implementar la plantilla de hello mediante PowerShell:</span><span class="sxs-lookup"><span data-stu-id="00ab6-249">Deploy hello template by using PowerShell:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="00ab6-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="00ab6-250">Next steps</span></span>
<span data-ttu-id="00ab6-251">Después de implementar los agentes de servicios de movilidad de hello, también puede [habilitar la replicación](site-recovery-vmware-to-azure.md) para las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="00ab6-251">After you deploy hello Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for hello virtual machines.</span></span>
