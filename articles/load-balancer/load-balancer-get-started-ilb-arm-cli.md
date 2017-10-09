---
title: aaaCreate un interno cargar equilibrador - CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un equilibrador de carga interno mediante el uso de Hola CLI de Azure en el Administrador de recursos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a><span data-ttu-id="459f1-103">Crear un equilibrador de carga interno mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="459f1-103">Create an internal load balancer by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="459f1-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="459f1-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="459f1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="459f1-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="459f1-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="459f1-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="459f1-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="459f1-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="459f1-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="459f1-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="459f1-109">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="459f1-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a><span data-ttu-id="459f1-110">Implementar soluciones de hello mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="459f1-110">Deploy hello solution by using hello Azure CLI</span></span>

<span data-ttu-id="459f1-111">Hola siguientes pasos muestra cómo toocreate una conexión a Internet el equilibrador de carga mediante el Administrador de recursos de Azure con CLI.</span><span class="sxs-lookup"><span data-stu-id="459f1-111">hello following steps show how toocreate an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="459f1-112">Con el Administrador de recursos de Azure, cada recurso se crea y configura de forma individual y, a continuación, reunir toocreate un recurso.</span><span class="sxs-lookup"><span data-stu-id="459f1-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="459f1-113">Necesita toocreate y configurar Hola después objetos toodeploy un equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="459f1-113">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="459f1-114">**Configuración de direcciones IP de front-end**: contiene direcciones IP públicas para el tráfico de red entrante</span><span class="sxs-lookup"><span data-stu-id="459f1-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="459f1-115">**Grupo de direcciones de back-end**: contiene interfaces de red (NIC) que permitan el tráfico de red de tooreceive de máquinas virtuales de Hola Hola equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="459f1-115">**Back-end address pool**: contains network interfaces (NICs) that enable hello virtual machines tooreceive network traffic from hello load balancer</span></span>
* <span data-ttu-id="459f1-116">**Las reglas de equilibrio de carga**: contiene reglas que se asignan a un puerto público en tooport de equilibrador de carga de hello en el grupo de direcciones de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="459f1-116">**Load-balancing rules**: contains rules that map a public port on hello load balancer tooport in hello back-end address pool</span></span>
* <span data-ttu-id="459f1-117">**Reglas NAT de entrada**: contiene reglas que se asignan a un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="459f1-117">**Inbound NAT rules**: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool</span></span>
* <span data-ttu-id="459f1-118">**Sondeos**: contiene los sondeos de mantenimiento que son utilizados toocheck Hola disponibilidad de instancias de máquinas virtuales en el grupo de direcciones de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="459f1-118">**Probes**: contains health probes that are used toocheck hello availability of virtual machines instances in hello back-end address pool</span></span>

<span data-ttu-id="459f1-119">Para más información, consulte [Compatibilidad de Azure Resource Manager con el equilibrador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="459f1-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="459f1-120">Configurar la CLI toouse el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="459f1-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="459f1-121">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="459f1-121">If you have never used Azure CLI, see [Install and configure hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="459f1-122">Siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="459f1-122">Follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="459f1-123">Ejecute hello **modo de configuración de azure** comando modo de administrador de tooswitch tooResource, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="459f1-123">Run hello **azure config mode** command tooswitch tooResource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="459f1-124">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="459f1-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="459f1-125">Creación de un equilibrador de carga interno paso a paso</span><span class="sxs-lookup"><span data-stu-id="459f1-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="459f1-126">Inicie sesión en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="459f1-126">Sign in tooAzure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="459f1-127">Cuando se le solicite, escriba sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="459f1-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="459f1-128">Cambiar el modo de administrador de recursos de hello comando herramientas tooAzure.</span><span class="sxs-lookup"><span data-stu-id="459f1-128">Change hello command tools tooAzure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="459f1-129">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="459f1-129">Create a resource group</span></span>

<span data-ttu-id="459f1-130">Todos los recursos de Azure Resource Manager están asociados a un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="459f1-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="459f1-131">Si todavía no lo ha hecho, cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="459f1-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="459f1-132">Crear un conjunto de equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="459f1-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="459f1-133">Creación de un conjunto de equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="459f1-133">Create an internal load balancer</span></span>

    <span data-ttu-id="459f1-134">Hola siguiendo el escenario, se crea un grupo de recursos denominado nrprg en la región Este de EE..</span><span class="sxs-lookup"><span data-stu-id="459f1-134">In hello following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="459f1-135">Todos los recursos para una equilibradores de carga interno, como redes virtuales y subredes de red virtual, deben estar en Hola el mismo grupo de recursos y de Hola misma región.</span><span class="sxs-lookup"><span data-stu-id="459f1-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in hello same resource group and in hello same region.</span></span>

2. <span data-ttu-id="459f1-136">Crear una dirección IP front-end de equilibrador de carga interno de Hola.</span><span class="sxs-lookup"><span data-stu-id="459f1-136">Create a front-end IP address for hello internal load balancer.</span></span>

    <span data-ttu-id="459f1-137">dirección IP de Hola que utilice debe ser en intervalo de subred de hello de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="459f1-137">hello IP address that you use must be within hello subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="459f1-138">Crear grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="459f1-138">Create hello back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="459f1-139">Después de definir una dirección IP de front-end y un grupo de direcciones de back-end, puede crear reglas de equilibradores de carga, reglas NAT de entrada y sondeos de estado personalizados.</span><span class="sxs-lookup"><span data-stu-id="459f1-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="459f1-140">Crear una regla de equilibrador de carga para el equilibrador de carga interno de Hola.</span><span class="sxs-lookup"><span data-stu-id="459f1-140">Create a load balancer rule for hello internal load balancer.</span></span>

    <span data-ttu-id="459f1-141">Al seguir los pasos anteriores de hello, comando hello crea una regla de equilibrador de carga para tooport escucha 1433 en el grupo de servidores front-end de Hola y envío con equilibrio de carga de red tráfico toohello back-end grupo de direcciones, también utiliza el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="459f1-141">When you follow hello previous steps, hello command creates a load-balancer rule for listening tooport 1433 in hello front-end pool and sending load-balanced network traffic toohello back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="459f1-142">Crear reglas NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="459f1-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="459f1-143">Reglas NAT de entrada son puntos de conexión toocreate usado en un equilibrador de carga que vaya tooa instancia de máquina virtual específica.</span><span class="sxs-lookup"><span data-stu-id="459f1-143">Inbound NAT rules are used toocreate endpoints in a load balancer that go tooa specific virtual machine instance.</span></span> <span data-ttu-id="459f1-144">los pasos anteriores de Hello crean dos reglas NAT para escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="459f1-144">hello previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="459f1-145">Crear sondeos de mantenimiento para el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="459f1-145">Create health probes for hello load balancer.</span></span>

    <span data-ttu-id="459f1-146">Un sondeo de estado comprueba todos los toomake de instancias de máquina virtual que puede enviar tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="459f1-146">A health probe checks all virtual machine instances toomake sure they can send network traffic.</span></span> <span data-ttu-id="459f1-147">instancia de la máquina virtual de Hello con las comprobaciones de sondeo con error se quita del equilibrador de carga de hello hasta que deja de estar en línea y una comprobación de sondeo determina que es correcto.</span><span class="sxs-lookup"><span data-stu-id="459f1-147">hello virtual machine instance with failed probe checks is removed from hello load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="459f1-148">plataforma de Microsoft Azure de Hello usa una dirección IPv4 estática, enrutable públicamente para una amplia variedad de escenarios de administración.</span><span class="sxs-lookup"><span data-stu-id="459f1-148">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="459f1-149">dirección IP de Hello es 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="459f1-149">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="459f1-150">Ningún firewall debe bloquear esta dirección IP, ya que puede causar un comportamiento inesperado.</span><span class="sxs-lookup"><span data-stu-id="459f1-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="459f1-151">Con sentido tooAzure de equilibrio de carga interno, se usa esta dirección IP mediante la supervisión de sondeos de estado de mantenimiento de Hola de toodetermine equilibrador de carga de Hola para máquinas virtuales en un conjunto de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="459f1-151">With respect tooAzure internal load balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="459f1-152">Si un grupo de seguridad de red es toorestrict usado tráfico tooAzure máquinas en un conjunto de carga equilibrada internamente o subred de red virtual tooa aplicado, asegúrese de que una regla de seguridad de red se agrega tráfico tooallow desde 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="459f1-152">If a network security group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa virtual network subnet, ensure that a network security rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="459f1-153">Cree tarjetas NIC</span><span class="sxs-lookup"><span data-stu-id="459f1-153">Create NICs</span></span>

<span data-ttu-id="459f1-154">Necesita toocreate NIC (o modificar los existentes) y asociarlos a tooNAT reglas, reglas de equilibrador de carga y sondeos.</span><span class="sxs-lookup"><span data-stu-id="459f1-154">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="459f1-155">Cree una NIC denominado *nic1 de carga equilibrada puede*y, a continuación, asociar hello *rdp1* NAT hello y regla *beilb* grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="459f1-155">Create an NIC named *lb-nic1-be*, and then associate it with hello *rdp1* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="459f1-156">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="459f1-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="459f1-157">Cree una NIC denominado *nic2 de carga equilibrada puede*y, a continuación, asociar hello *rdp2* NAT hello y regla *beilb* grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="459f1-157">Create an NIC named *lb-nic2-be*, and then associate it with hello *rdp2* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="459f1-158">Crear una máquina virtual denominada *DB1*y, a continuación, asociar Hola NIC denominado *nic1 de carga equilibrada puede*.</span><span class="sxs-lookup"><span data-stu-id="459f1-158">Create a virtual machine named *DB1*, and then associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="459f1-159">Llama a una cuenta de almacenamiento *web1nrp* se crea antes de hello después de la ejecución del comando:</span><span class="sxs-lookup"><span data-stu-id="459f1-159">A storage account called *web1nrp* is created before hello following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="459f1-160">Hola a las máquinas virtuales en un toobe de necesidad de equilibrador de carga en el mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="459f1-160">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="459f1-161">Use `azure availset create` toocreate un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="459f1-161">Use `azure availset create` toocreate an availability set.</span></span>

4. <span data-ttu-id="459f1-162">Crear una máquina virtual (VM) con el nombre *DB2*y, a continuación, asociar Hola NIC denominado *nic2 de carga equilibrada puede*.</span><span class="sxs-lookup"><span data-stu-id="459f1-162">Create a virtual machine (VM) named *DB2*, and then associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="459f1-163">Llama a una cuenta de almacenamiento *web1nrp* se creó antes de ejecutar el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="459f1-163">A storage account called *web1nrp* was created before running hello following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="459f1-164">Eliminar un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="459f1-164">Delete a load balancer</span></span>

<span data-ttu-id="459f1-165">tooremove un equilibrador de carga, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="459f1-165">tooremove a load balancer, use hello following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="459f1-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="459f1-166">Next steps</span></span>

[<span data-ttu-id="459f1-167">Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen</span><span class="sxs-lookup"><span data-stu-id="459f1-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="459f1-168">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="459f1-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

