---
title: "aaaDeploy Deis 3 nodos clúster | Documentos de Microsoft"
description: "Este artículo se describe cómo toocreate un nodo 3 Deis clúster en Azure mediante una plantilla de Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="a9bd6-103">Implementación y configuración de un clúster Deis de 3 nodos en Azure</span><span class="sxs-lookup"><span data-stu-id="a9bd6-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="a9bd6-104">Este artículo le guiará a través de aprovisionamiento de un clúster [Deis](http://deis.io/) en Azure.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="a9bd6-105">Abarca todos los pasos de hello creen Hola certificados necesarios toodeploying y obtener un ejemplo de ajuste de escala **vaya** aplicación en clúster recién suministradas Hola.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-105">It covers all hello steps from creating hello necessary certificates toodeploying and scaling a sample **Go** application on hello newly provisioned cluster.</span></span>

<span data-ttu-id="a9bd6-106">Hello siguiente diagrama muestra hello arquitectura del sistema de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-106">hello following diagram shows hello architecture of hello deployed system.</span></span> <span data-ttu-id="a9bd6-107">Un administrador del sistema administra Hola clúster con Deis herramientas como **deis** y **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-107">A system administrator manages hello cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="a9bd6-108">Las conexiones se establecen a través de un equilibrador de carga de Azure, que reenvía Hola conexiones tooone del miembro de hello nodos en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-108">Connections are established through an Azure load balancer, which forwards hello connections tooone of hello member nodes on hello cluster.</span></span> <span data-ttu-id="a9bd6-109">el acceso de los clientes de Hello implementar aplicaciones a través del equilibrador de carga de hello así.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-109">hello clients access deployed applications through hello load balancer as well.</span></span> <span data-ttu-id="a9bd6-110">En este caso, el equilibrador de carga de hello reenvía Hola tráfico tooa Deis malla de enrutador, que routs más contenedores de Docker de tráfico toocorresponding hospedados en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-110">In this case, hello load balancer forwards hello traffic tooa Deis router mesh, which further routs traffic toocorresponding Docker containers hosted on hello cluster.</span></span>

  ![Diagrama de arquitectura del clúster Desis implementado](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="a9bd6-112">En orden toorun a través de pasos de hello, necesitará:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-112">In order toorun through hello following steps, you'll need:</span></span>

* <span data-ttu-id="a9bd6-113">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-113">An active Azure subscription.</span></span> <span data-ttu-id="a9bd6-114">Si no tiene una, puede obtener una prueba gratuita en [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="a9bd6-115">Un trabajo o grupos de recursos de Azure de escuela id toouse.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-115">A work or school id toouse Azure resource groups.</span></span> <span data-ttu-id="a9bd6-116">Si tiene una cuenta personal y un registro con un Id. de Microsoft, necesita demasiado[crear un identificador de trabajo del que el personal](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-116">If you have a personal account and log in with a Microsoft id, you need too[create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="a9bd6-117">Cualquiera, dependiendo del sistema operativo de cliente: Hola [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello [CLI de Azure para Mac, Linux y Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-117">Either -- depending on your client operating system -- hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="a9bd6-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="a9bd6-119">OpenSSL está certificados necesarios de hello toogenerate usado.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-119">OpenSSL is used toogenerate hello necessary certificates.</span></span>
* <span data-ttu-id="a9bd6-120">Un cliente Git como [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="a9bd6-121">aplicación de ejemplo de Hola tootest, también necesitará un servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-121">tootest hello sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="a9bd6-122">Puede usar los servidores o servicios DNS que admiten los registros de carácter comodín A.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="a9bd6-123">Un equipo toorun Deis herramientas de cliente.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-123">A computer toorun Deis client tools.</span></span> <span data-ttu-id="a9bd6-124">Puede usar un equipo local o en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="a9bd6-125">Puede ejecutar estas herramientas en casi cualquier distribución de Linux, pero las instrucciones siguientes hello usan Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-125">You can run these tools on almost any Linux distribution, but hello following instructions use Ubuntu.</span></span>

## <a name="provision-hello-cluster"></a><span data-ttu-id="a9bd6-126">Clúster de Hola de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="a9bd6-126">Provision hello cluster</span></span>
<span data-ttu-id="a9bd6-127">En esta sección, usará un [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) plantilla del repositorio de código abierto de hello [plantillas de inicio rápido de azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from hello open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="a9bd6-128">En primer lugar, deberá copiar hacia abajo de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-128">First, you'll copy down hello template.</span></span> <span data-ttu-id="a9bd6-129">A continuación, creará un nuevo par de claves SSH para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="a9bd6-130">Y, a continuación, configurará un nuevo identificador para su clúster.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="a9bd6-131">Y por último, usará secuencias de comandos de Shell de Hola o clúster de hello PowerShell script tooprovision Hola.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-131">And finally, you'll use either hello Shell script or hello PowerShell script tooprovision hello cluster.</span></span>

1. <span data-ttu-id="a9bd6-132">Repositorio de Hola de clon: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-132">Clone hello repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="a9bd6-133">Vaya a la carpeta de plantillas de toohello:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-133">Go toohello template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="a9bd6-134">Cree un nuevo par de claves SSH mediante ssh-keygen:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="a9bd6-135">Generar un certificado mediante Hola por encima de la clave privada:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-135">Generate a certificate using hello above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. <span data-ttu-id="a9bd6-136">Vaya demasiado[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate un nuevo token de clúster, que busca un resultado similar:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-136">Go too[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="a9bd6-137">Cada clúster CoreOS debe toohave un token único de este servicio gratuito.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-137">Each CoreOS cluster needs toohave a unique token from this free service.</span></span> <span data-ttu-id="a9bd6-138">Consulte [Documentación de CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="a9bd6-139">Modificar hello **nube config.yaml** tooreplace Hola existente de archivos **detección** token con el nuevo token de hello:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-139">Modify hello **cloud-config.yaml** file tooreplace hello existing  **discovery** token with hello new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="a9bd6-140">Modificar hello **azuredeploy parameters.json** archivo: certificado Hola abierto que creó en el paso 4 en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-140">Modify hello **azuredeploy-parameters.json** file: Open hello certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="a9bd6-141">Copiar todo el texto entre `----BEGIN CERTIFICATE-----` y `-----END CERTIFICATE-----` en hello **sshKeyData** parámetro (deberá tooremove todos los caracteres de nueva línea).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into hello **sshKeyData** parameter (you'll need tooremove all newline characters).</span></span>
8. <span data-ttu-id="a9bd6-142">Modificar hello **newStorageAccountName** parámetro.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-142">Modify hello **newStorageAccountName** parameter.</span></span> <span data-ttu-id="a9bd6-143">Se trata de una cuenta de almacenamiento de Hola para discos de sistema operativo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-143">This is hello storage account for VM OS disks.</span></span> <span data-ttu-id="a9bd6-144">Este nombre de cuenta tiene toobe único global.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-144">This account name has toobe globally unique.</span></span>
9. <span data-ttu-id="a9bd6-145">Modificar hello **publicDomainName** parámetro.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-145">Modify hello **publicDomainName** parameter.</span></span> <span data-ttu-id="a9bd6-146">Esto pasaría a formar parte del nombre DNS de hello asociado con IP pública del equilibrador de carga Hola.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-146">This will become part of hello DNS name associated with hello load balancer public IP.</span></span> <span data-ttu-id="a9bd6-147">Hello FQDN final tendrá formato Hola de *[valor de este parámetro]*. *[Región]* . cloudapp.azure.com. Por ejemplo, si especifica nombre hello como deishbai32 y grupo de recursos de hello es región del oeste de Estados Unidos toohello implementado, Hola final equilibrador de carga FQDN tooyour será deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-147">hello final FQDN will have hello format of *[value of this parameter]*.*[region]*.cloudapp.azure.com. For example, if you specify hello name as deishbai32, and hello resource group is deployed toohello West US region, then hello final FQDN tooyour load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="a9bd6-148">Guarde el archivo de parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-148">Save hello parameter file.</span></span> <span data-ttu-id="a9bd6-149">Y, a continuación, puede aprovisionar clúster Hola con Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-149">And then you can provision hello cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="a9bd6-150">o la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-150">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="a9bd6-151">Cuando se aprovisiona el grupo de recursos de hello, puede ver todos los recursos de hello en el grupo de hello en el portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-151">Once hello resource group is provisioned, you can see all hello resources in hello group on Azure classic portal.</span></span> <span data-ttu-id="a9bd6-152">Como se muestra en la siguiente captura de pantalla, hello de hello grupo de recursos contiene una red virtual con tres máquinas virtuales, que se une toohello mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-152">As shown in hello following screenshot, hello resource group contains a virtual network with three VMs, which are joined toohello same availability set.</span></span> <span data-ttu-id="a9bd6-153">grupo de Hello también contiene un equilibrador de carga, que tiene una dirección IP pública asociada.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-153">hello group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Hola aprovisiona el grupo de recursos en el portal de Azure clásico](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a><span data-ttu-id="a9bd6-155">Instalar el cliente de Hola</span><span class="sxs-lookup"><span data-stu-id="a9bd6-155">Install hello client</span></span>
<span data-ttu-id="a9bd6-156">Necesita **deisctl** toocontrol su Deis clúster.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-156">You need **deisctl** toocontrol your Deis cluster.</span></span> <span data-ttu-id="a9bd6-157">Aunque deisctl se instala automáticamente en todos los nodos de clúster de hello, es un deisctl de toouse buenas prácticas en un equipo administrativo independiente.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-157">Although deisctl is automatically installed in all hello cluster nodes, it's a good practice toouse deisctl on a separate administrative machine.</span></span> <span data-ttu-id="a9bd6-158">Además, dado que todos los nodos se configuran con solo las direcciones IP privadas, deberá toouse SSH túnel a través del equilibrador de carga de hello, que tiene una dirección IP pública, las máquinas de nodo de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-158">Furthermore, because all nodes are configured with only private IP addresses, you'll need toouse SSH tunneling through hello load balancer, which has a public IP, tooconnect toohello node machines.</span></span> <span data-ttu-id="a9bd6-159">Hello siguientes son Hola pasos de configuración de deisctl en una máquina virtual o física Ubuntu independiente.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-159">hello following are hello steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="a9bd6-160">Instalar deisctl:mkdir deis</span><span class="sxs-lookup"><span data-stu-id="a9bd6-160">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="a9bd6-161">Agregue al agente toossh de clave privada:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-161">Add your private key toossh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. <span data-ttu-id="a9bd6-162">Configure deisctl:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-162">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

<span data-ttu-id="a9bd6-163">plantilla de Hello define reglas NAT de entrada que se asignan 2223 tooinstance 1, 2224 tooinstance 2 y 2225 tooinstance 3.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-163">hello template defines inbound NAT rules that map 2223 tooinstance 1, 2224 tooinstance 2, and 2225 tooinstance 3.</span></span> <span data-ttu-id="a9bd6-164">Esto proporciona redundancia para usar la herramienta de deisctl Hola.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-164">This provides redundancy for using hello deisctl tool.</span></span> <span data-ttu-id="a9bd6-165">Puede examinar estas reglas en el Portal de Azure clásico:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-165">You can examine these rules on Azure classic portal:</span></span>

![Reglas NAT en el equilibrador de carga de Hola](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="a9bd6-167">Actualmente plantilla Hola solo admite clústeres de 3 nodos.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-167">Currently hello template only supports 3-node clusters.</span></span> <span data-ttu-id="a9bd6-168">Esto es debido a una limitación en la definición de la regla NAT de la plantilla del Administrador de recursos de Azure, que no admite la sintaxis del bucle.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-168">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-hello-deis-platform"></a><span data-ttu-id="a9bd6-169">Instale e inicie hello Deis plataforma</span><span class="sxs-lookup"><span data-stu-id="a9bd6-169">Install and start hello Deis platform</span></span>
<span data-ttu-id="a9bd6-170">Ahora puede usar deisctl tooinstall e iniciar hello Deis plataforma:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-170">Now you can use deisctl tooinstall and start hello Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="a9bd6-171">Plataforma de saludo inicial tarda un tiempo (hasta 10 minutos).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-171">Starting hello platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="a9bd6-172">Especialmente, al iniciar el servicio del generador de hello puede tardar mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-172">Especially, starting hello builder service can take a long time.</span></span> <span data-ttu-id="a9bd6-173">Y a veces tarda unos toosucceed intentos: operación Hola parezca toohang, pruebe a escribir `ctrl+c` toobreak ejecución de comando de Hola y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-173">And sometimes it takes a few tries toosucceed: If hello operation seems toohang, try typing `ctrl+c` toobreak execution of hello command and retry.</span></span>
> 
> 

<span data-ttu-id="a9bd6-174">Puede usar `deisctl list` tooverify si todos los servicios se están ejecutando:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-174">You can use `deisctl list` tooverify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="a9bd6-175">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="a9bd6-175">Congratulations!</span></span> <span data-ttu-id="a9bd6-176">Ahora ya dispone de un clúster Deis en ejecución en Azure.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-176">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="a9bd6-177">A continuación, vamos a implementar un clúster de Go application toosee hello en acción de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-177">Next, let's deploy a sample Go application toosee hello cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="a9bd6-178">Implementar y escalar una aplicación Hello World</span><span class="sxs-lookup"><span data-stu-id="a9bd6-178">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="a9bd6-179">Hello pasos siguientes muestran cómo toodeploy "Hola mundo" vaya clúster toohello de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-179">hello following steps show how toodeploy a "Hello World" Go application toohello cluster.</span></span> <span data-ttu-id="a9bd6-180">Hola pasos se basan en [Deis documentación](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-180">hello steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="a9bd6-181">Para hello enrutamiento malla toowork correctamente, deberá toohave un registro de un comodín para el dominio que apunta toohello IP pública Hola de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-181">For hello routing mesh toowork properly, you’ll need toohave a wildcard A record for your domain pointing toohello public IP of hello load balancer.</span></span> <span data-ttu-id="a9bd6-182">Hello captura de pantalla siguiente muestra hello un registro de un registro de dominio de ejemplo en GoDaddy:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-182">hello following screenshot shows hello A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Registro de Godaddy A](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="a9bd6-184">Instalar deis:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-184">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="a9bd6-185">Cree una nueva clave SSH y, a continuación, agregue hello tooGitHub de clave pública (por supuesto, también se puede reutilizar las claves existentes).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-185">Create a new SSH key, and then add hello public key tooGitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="a9bd6-186">toocreate un nuevo par de claves de SSH, use:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-186">toocreate a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. <span data-ttu-id="a9bd6-187">Agregar id_rsa.pub u Hola de clave pública de su elección, tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-187">Add id_rsa.pub, or hello public key of your choice, tooGitHub.</span></span> <span data-ttu-id="a9bd6-188">Puede hacerlo mediante el uso de hello agregar SSH clave botón en la pantalla de configuración de claves SSH:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-188">You can do this by using hello Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![Clave de GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="a9bd6-190">Registre un nuevo usuario:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-190">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="a9bd6-191">Agregue la clave SSH hello:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-191">Add hello SSH key:</span></span>
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. <span data-ttu-id="a9bd6-192">Cree una aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-192">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="a9bd6-193">
8.inserción de git Hola desencadenará Docker imágenes toobe compiladas e implementadas, que le llevará unos minutos.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-193">
8. hello git push will trigger Docker images toobe built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="a9bd6-194">Desde mi experiencia, en ocasiones, puede quedar paso 10 (repositorio de Pushing imágenes tooprivate).</span><span class="sxs-lookup"><span data-stu-id="a9bd6-194">From my experience, occasionally, Step 10 (Pushing image tooprivate repository) may hang.</span></span> <span data-ttu-id="a9bd6-195">Cuando esto ocurre, puede detener el proceso de hello, remove Hola aplicación usando ' deis aplicaciones: destruir – a <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind el nombre de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-195">When this happens, you can stop hello process, remove hello application using `deis apps:destroy –a <application name>` tooremove hello application and try again. You can use `deis apps:list` toofind out hello name of your application.</span></span> <span data-ttu-id="a9bd6-196">Si todo funciona, debería ver algo parecido a Hola siguiente al final de Hola de salidas de comandos:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-196">If everything works out, you should see something like hello following at hello end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="a9bd6-197">Compruebe si funciona la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-197">Verify if hello application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="a9bd6-198">Debería ver lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-198">You should see:</span></span>
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. <span data-ttu-id="a9bd6-199">Escala Hola aplicación too3 instancias:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-199">Scale hello application too3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="a9bd6-200">Si lo desea, puede usar deis info tooexamine detalles de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-200">Optionally, you can use deis info tooexamine details of your application.</span></span> <span data-ttu-id="a9bd6-201">Hello resultados siguientes están en la implementación de aplicación:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-201">hello following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="a9bd6-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9bd6-202">Next Steps</span></span>
<span data-ttu-id="a9bd6-203">En este artículo le guía a través de todos los tooprovision de pasos de hello Deis un nuevo clúster en Azure mediante una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-203">This article walked you through all hello steps tooprovision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="a9bd6-204">plantilla de Hello admite la redundancia en herramientas de conexiones, así como para las aplicaciones implementadas de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-204">hello template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="a9bd6-205">plantilla de Hello también evita el uso de direcciones IP públicas en los nodos de miembro, lo que ahorra valiosos recursos de IP pública y proporciona un entorno más seguro a las aplicaciones de toohost.</span><span class="sxs-lookup"><span data-stu-id="a9bd6-205">hello template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment toohost applications.</span></span> <span data-ttu-id="a9bd6-206">toolearn más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="a9bd6-206">toolearn more, see hello following articles:</span></span>

<span data-ttu-id="a9bd6-207">[Información general sobre Azure Resource Manager][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="a9bd6-207">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="a9bd6-208">[¿Cómo toouse Hola CLI de Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="a9bd6-208">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="a9bd6-209">[Uso de Azure PowerShell con Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="a9bd6-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
