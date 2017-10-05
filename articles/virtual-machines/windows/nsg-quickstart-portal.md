---
title: Apertura de puertos a una VM mediante Azure Portal | Microsoft Docs
description: "Aprenda a abrir un puerto o crear un punto de conexión a la máquina virtual Windows con el modelo de implementación de Resource Manager en Azure Portal"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 33bc0be0aeae6d0276fd8999b9ac0a010e3067ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-to-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="7a92a-103">Apertura de puertos en una máquina virtual con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7a92a-103">How to open ports to a virtual machine with the Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="7a92a-104">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="7a92a-104">Quick commands</span></span>
<span data-ttu-id="7a92a-105">También puede [llevar a cabo estos pasos con Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7a92a-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="7a92a-106">En primer lugar, cree el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="7a92a-106">First, create your Network Security Group.</span></span> <span data-ttu-id="7a92a-107">Seleccione un grupo de recursos en el portal, elija **Agregar** y busque y seleccione **Grupo de seguridad de red**:</span><span class="sxs-lookup"><span data-stu-id="7a92a-107">Select a resource group in the portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Agregar un grupo de seguridad de red](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="7a92a-109">Escriba el nombre del grupo de seguridad de red, seleccione un grupo de recursos, o créelo, y seleccione una ubicación.</span><span class="sxs-lookup"><span data-stu-id="7a92a-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="7a92a-110">Cuando haya terminado, seleccione **Crear**:</span><span class="sxs-lookup"><span data-stu-id="7a92a-110">Select **Create** when finished:</span></span>

![Creación de un grupo de seguridad de red](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="7a92a-112">Seleccione el nuevo grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="7a92a-112">Select your new Network Security Group.</span></span> <span data-ttu-id="7a92a-113">Seleccione "Reglas de seguridad de entrada" y, después, seleccione el botón **Agregar** para crear una regla:</span><span class="sxs-lookup"><span data-stu-id="7a92a-113">Select 'Inbound security rules', then select the **Add** button to create a rule:</span></span>

![Agregar una regla de entrada](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="7a92a-115">Elija un **servicio** común en el menú desplegable, como *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="7a92a-115">Choose a common **Service** from the drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="7a92a-116">También puede seleccionar *Personalizado* a fin de proporcionar un puerto específico para su uso.</span><span class="sxs-lookup"><span data-stu-id="7a92a-116">You can also select *Custom* to provide a specific port to use.</span></span> <span data-ttu-id="7a92a-117">Si lo desea, cambie la prioridad o el nombre.</span><span class="sxs-lookup"><span data-stu-id="7a92a-117">If desired, change the priority or name.</span></span> <span data-ttu-id="7a92a-118">La prioridad afecta al orden en que se aplican las reglas (cuanto más bajo es el valor numérico, antes se aplica la regla).</span><span class="sxs-lookup"><span data-stu-id="7a92a-118">The priority affects the order in which rules are applied - the lower the numerical value, the earlier the rule is applied.</span></span> <span data-ttu-id="7a92a-119">También puede seleccionar **Avanzado** en la parte superior de esta pantalla para especificar un intervalo de puertos o un bloque de direcciones IP de origen, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7a92a-119">You can also select **Advanced** at the top of this screen to enter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="7a92a-120">Cuando esté listo, seleccione **Aceptar** para crear la regla:</span><span class="sxs-lookup"><span data-stu-id="7a92a-120">When you are ready, select **OK** to create the rule:</span></span>

![Crear una regla de entrada](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="7a92a-122">El paso final es asociar el grupo de seguridad de red a una subred o una interfaz de red específica.</span><span class="sxs-lookup"><span data-stu-id="7a92a-122">Your final step is to associate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="7a92a-123">Vamos a asociar el grupo de seguridad de red con una subred.</span><span class="sxs-lookup"><span data-stu-id="7a92a-123">Let's associate the Network Security Group with a subnet.</span></span> <span data-ttu-id="7a92a-124">Seleccione **Subredes** y elija **Asociar**:</span><span class="sxs-lookup"><span data-stu-id="7a92a-124">Select **Subnets**, then choose **Associate**:</span></span>

![Asociar un grupo de seguridad de red a una subred](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="7a92a-126">Seleccione la red virtual y luego seleccione la subred adecuada:</span><span class="sxs-lookup"><span data-stu-id="7a92a-126">Select your virtual network, and then select the appropriate subnet:</span></span>

![Asociar un grupo de seguridad de red a una red virtual](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="7a92a-128">Ahora ha creado un grupo de seguridad de red, ha creado una regla de entrada que permite el tráfico en el puerto 80 y lo ha asociado con una subred.</span><span class="sxs-lookup"><span data-stu-id="7a92a-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="7a92a-129">A través del puerto 80 se accede a las máquinas virtuales que se conectan a esa subred.</span><span class="sxs-lookup"><span data-stu-id="7a92a-129">Any VMs you connect to that subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="7a92a-130">Más información sobre los grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="7a92a-130">More information on Network Security Groups</span></span>
<span data-ttu-id="7a92a-131">Los comandos rápidos que se describen aquí le permiten ponerse a trabajar con el flujo de tráfico a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7a92a-131">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="7a92a-132">Los grupos de seguridad de red proporcionan muchas características excelentes y un gran nivel de detalle para controlar el acceso a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="7a92a-132">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="7a92a-133">Puede leer más sobre la [creación de un grupo de seguridad de red y las reglas de ACL aquí](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7a92a-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="7a92a-134">Para las aplicaciones web de alta disponibilidad, debe colocar las máquinas virtuales detrás de una instancia de Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="7a92a-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="7a92a-135">El equilibrador de carga distribuye el tráfico a las máquinas virtuales, con un grupo de seguridad de red que proporciona el filtrado del tráfico.</span><span class="sxs-lookup"><span data-stu-id="7a92a-135">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="7a92a-136">Para más información, consulte [Equilibrio de la carga de máquinas virtuales Linux en Azure para crear una aplicación de alta disponibilidad](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="7a92a-136">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a92a-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7a92a-137">Next steps</span></span>
<span data-ttu-id="7a92a-138">En este ejemplo, se ha creado una regla sencilla para permitir tráfico HTTP.</span><span class="sxs-lookup"><span data-stu-id="7a92a-138">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="7a92a-139">Puede encontrar información sobre la creación de entornos más detallados en los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="7a92a-139">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="7a92a-140">Información general sobre Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7a92a-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="7a92a-141">¿Qué es un grupo de seguridad de red?</span><span class="sxs-lookup"><span data-stu-id="7a92a-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)