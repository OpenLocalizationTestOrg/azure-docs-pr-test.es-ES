---
title: aaaOpen puertos tooa VM con Hola portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooopen un puerto o cree una máquina virtual de Windows tooyour de punto de conexión con el modelo de implementación de administrador de recursos de Hola Hola Portal de Azure"
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
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="a58a9-103">¿Cómo tooopen puertos tooa virtual machine con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a58a9-103">How tooopen ports tooa virtual machine with hello Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="a58a9-104">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="a58a9-104">Quick commands</span></span>
<span data-ttu-id="a58a9-105">También puede [llevar a cabo estos pasos con Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a58a9-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="a58a9-106">En primer lugar, cree el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="a58a9-106">First, create your Network Security Group.</span></span> <span data-ttu-id="a58a9-107">Seleccione un grupo de recursos en el portal de hello, elija **agregar**, a continuación, busque y seleccione **grupo de seguridad de red**:</span><span class="sxs-lookup"><span data-stu-id="a58a9-107">Select a resource group in hello portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Agregar un grupo de seguridad de red](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="a58a9-109">Escriba el nombre del grupo de seguridad de red, seleccione un grupo de recursos, o créelo, y seleccione una ubicación.</span><span class="sxs-lookup"><span data-stu-id="a58a9-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="a58a9-110">Cuando haya terminado, seleccione **Crear**:</span><span class="sxs-lookup"><span data-stu-id="a58a9-110">Select **Create** when finished:</span></span>

![Creación de un grupo de seguridad de red](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="a58a9-112">Seleccione el nuevo grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="a58a9-112">Select your new Network Security Group.</span></span> <span data-ttu-id="a58a9-113">Seleccione 'Reglas de seguridad de entrada', a continuación, seleccione hello **agregar** botón toocreate una regla:</span><span class="sxs-lookup"><span data-stu-id="a58a9-113">Select 'Inbound security rules', then select hello **Add** button toocreate a rule:</span></span>

![Agregar una regla de entrada](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="a58a9-115">Elija una común **servicio** desde el menú desplegable de hello, como *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="a58a9-115">Choose a common **Service** from hello drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="a58a9-116">También puede seleccionar *personalizado* tooprovide toouse de un puerto específico.</span><span class="sxs-lookup"><span data-stu-id="a58a9-116">You can also select *Custom* tooprovide a specific port toouse.</span></span> <span data-ttu-id="a58a9-117">Si desea cambiar la prioridad de Hola o nombre.</span><span class="sxs-lookup"><span data-stu-id="a58a9-117">If desired, change hello priority or name.</span></span> <span data-ttu-id="a58a9-118">Hello prioridad afecta al orden de hello en el que se aplican las reglas - Hola Hola numérico un valor inferior, hello anteriores Hola regla se aplica.</span><span class="sxs-lookup"><span data-stu-id="a58a9-118">hello priority affects hello order in which rules are applied - hello lower hello numerical value, hello earlier hello rule is applied.</span></span> <span data-ttu-id="a58a9-119">También puede seleccionar **avanzadas** en parte superior de Hola de este tooenter de pantalla de un determinado origen IP bloque o intervalo de puerto, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a58a9-119">You can also select **Advanced** at hello top of this screen tooenter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="a58a9-120">Cuando esté listo, seleccione **Aceptar** regla de Hola toocreate:</span><span class="sxs-lookup"><span data-stu-id="a58a9-120">When you are ready, select **OK** toocreate hello rule:</span></span>

![Crear una regla de entrada](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="a58a9-122">El paso final es tooassociate grupo de seguridad de su red con una subred o una interfaz de red específica.</span><span class="sxs-lookup"><span data-stu-id="a58a9-122">Your final step is tooassociate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="a58a9-123">Vamos a asociar Hola grupo de seguridad de red a una subred.</span><span class="sxs-lookup"><span data-stu-id="a58a9-123">Let's associate hello Network Security Group with a subnet.</span></span> <span data-ttu-id="a58a9-124">Seleccione **Subredes** y elija **Asociar**:</span><span class="sxs-lookup"><span data-stu-id="a58a9-124">Select **Subnets**, then choose **Associate**:</span></span>

![Asociar un grupo de seguridad de red a una subred](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="a58a9-126">Seleccione la red virtual y, a continuación, seleccione subred adecuada de hello:</span><span class="sxs-lookup"><span data-stu-id="a58a9-126">Select your virtual network, and then select hello appropriate subnet:</span></span>

![Asociar un grupo de seguridad de red a una red virtual](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="a58a9-128">Ahora ha creado un grupo de seguridad de red, ha creado una regla de entrada que permite el tráfico en el puerto 80 y lo ha asociado con una subred.</span><span class="sxs-lookup"><span data-stu-id="a58a9-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="a58a9-129">Todas las máquinas virtuales que se conecta toothat subred son accesibles en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="a58a9-129">Any VMs you connect toothat subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="a58a9-130">Más información sobre los grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="a58a9-130">More information on Network Security Groups</span></span>
<span data-ttu-id="a58a9-131">Hola de comandos rápido aquí le permite tooget seguridad y en ejecución con tooyour del flujo de tráfico máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a58a9-131">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="a58a9-132">Grupos de seguridad de red proporcionan muchas características excepcionales y granularidad para controlar acceso a los recursos tooyour.</span><span class="sxs-lookup"><span data-stu-id="a58a9-132">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="a58a9-133">Puede leer más sobre la [creación de un grupo de seguridad de red y las reglas de ACL aquí](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a58a9-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="a58a9-134">Para las aplicaciones web de alta disponibilidad, debe colocar las máquinas virtuales detrás de una instancia de Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="a58a9-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="a58a9-135">equilibrador de carga de Hello distribuye el tráfico tooVMs, con un grupo de seguridad de red que proporciona filtrado de tráfico.</span><span class="sxs-lookup"><span data-stu-id="a58a9-135">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="a58a9-136">Para obtener más información, consulte [cómo equilibrar tooload Linux virtual máquinas en Azure toocreate una aplicación de alta disponibilidad](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="a58a9-136">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a58a9-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a58a9-137">Next steps</span></span>
<span data-ttu-id="a58a9-138">En este ejemplo, ha creado el tráfico de tooallow HTTP de una regla sencilla.</span><span class="sxs-lookup"><span data-stu-id="a58a9-138">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="a58a9-139">Puede encontrar información sobre cómo crear entornos más detallados en hello siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="a58a9-139">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="a58a9-140">Información general sobre Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a58a9-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="a58a9-141">¿Qué es un grupo de seguridad de red?</span><span class="sxs-lookup"><span data-stu-id="a58a9-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)