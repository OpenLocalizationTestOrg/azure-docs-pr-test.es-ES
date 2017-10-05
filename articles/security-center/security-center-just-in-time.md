---
title: "Acceso a máquina virtual Just-In-Time en Azure Security Center | Microsoft Docs"
description: "En este documento se explica cómo el acceso a máquina virtual Just-In-Time en Azure Security Center ayuda a controlar el acceso a máquinas virtuales de Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: 5bb87488dcfc79ed4baa1dbd81dc4e1174f84e4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="51ba8-103">Administrar el acceso a máquina virtual mediante Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="51ba8-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="51ba8-104">El acceso a máquina virtual Just-In-Time se puede usar para bloquear el tráfico entrante a las máquinas virtuales de Azure. Para ello, se reduce la exposición a ataques al mismo tiempo que se proporciona un acceso sencillo para conectarse a las máquinas virtuales cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="51ba8-104">Just in time virtual machine (VM) access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks while providing easy access to connect to VMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="51ba8-105">La característica Just-In-Time se encuentra en versión preliminar y está disponible en el nivel estándar de Security Center.</span><span class="sxs-lookup"><span data-stu-id="51ba8-105">The just in time feature is in preview and available on the Standard tier of Security Center.</span></span>  <span data-ttu-id="51ba8-106">Para obtener más información sobre los planes de tarifa de Security Center, vea [Precios](security-center-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="51ba8-106">See [Pricing](security-center-pricing.md) to learn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="51ba8-107">Escenario de ataque</span><span class="sxs-lookup"><span data-stu-id="51ba8-107">Attack scenario</span></span>

<span data-ttu-id="51ba8-108">Normalmente, los ataques por fuerza bruta tienen como destino los puertos de administración para obtener acceso a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="51ba8-108">Brute force attacks commonly target management ports as a means to gain access to a VM.</span></span> <span data-ttu-id="51ba8-109">Si un atacante tiene éxito, puede tomar el control de la máquina virtual y establecer un punto de apoyo en su entorno.</span><span class="sxs-lookup"><span data-stu-id="51ba8-109">If successful, an attacker can take control over the VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="51ba8-110">Una manera de reducir el riesgo de sufrir un ataque por fuerza bruta consiste en limitar el tiempo que está abierto un puerto.</span><span class="sxs-lookup"><span data-stu-id="51ba8-110">One way to reduce exposure to a brute force attack is to limit the amount of time that a port is open.</span></span> <span data-ttu-id="51ba8-111">No es necesario que los puertos de administración estén abiertos en todo momento.</span><span class="sxs-lookup"><span data-stu-id="51ba8-111">Management ports do not need to be open at all times.</span></span> <span data-ttu-id="51ba8-112">Solo deben estar abiertos mientras se está conectado a la máquina virtual, por ejemplo, para realizar tareas de administración o mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="51ba8-112">They only need to be open while you are connected to the VM, for example to perform management or maintenance tasks.</span></span> <span data-ttu-id="51ba8-113">Cuando se habilita Just-In-Time, Security Center usa las reglas del [grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md) (NSG), que restringen el acceso a los puertos de administración para que no puedan ser objeto de ataques.</span><span class="sxs-lookup"><span data-stu-id="51ba8-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access to management ports so they cannot be targeted by attackers.</span></span>

![Escenario Just-In-Time][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="51ba8-115">¿Cómo funciona el acceso Just-In-Time?</span><span class="sxs-lookup"><span data-stu-id="51ba8-115">How does just in time access work?</span></span>

<span data-ttu-id="51ba8-116">Cuando se habilita Just-In-Time, Security Center bloquea el tráfico entrante a las máquinas virtuales de Azure mediante la creación de una regla de NSG.</span><span class="sxs-lookup"><span data-stu-id="51ba8-116">When just in time is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="51ba8-117">Se deben seleccionar los puertos de la máquina virtual para la que se bloqueará el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="51ba8-117">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="51ba8-118">Estos puertos están controlados mediante la solución Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="51ba8-118">These ports are controlled by the just in time solution.</span></span>

<span data-ttu-id="51ba8-119">Cuando un usuario solicita acceso a una máquina virtual, Security Center comprueba que el usuario tiene permisos de [control de acceso basado en rol (RBAC)](../active-directory/role-based-access-control-configure.md) que conceden acceso de escritura para el recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="51ba8-119">When a user requests access to a VM, Security Center checks that the user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for the Azure resource.</span></span> <span data-ttu-id="51ba8-120">Si tiene permisos de escritura, se aprueba la solicitud y Security Center configura automáticamente los grupos de seguridad de red (NSG) para permitir el tráfico entrante a los puertos de administración durante el tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="51ba8-120">If they have write permissions, the request is approved and Security Center automatically configures the Network Security Groups (NSGs) to allow inbound traffic to the management ports for the amount of time you specified.</span></span> <span data-ttu-id="51ba8-121">Una vez transcurrido ese tiempo, Security Center restaura los NSG a su estado anterior.</span><span class="sxs-lookup"><span data-stu-id="51ba8-121">After the time has expired, Security Center restores the NSGs to their previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="51ba8-122">En la actualidad, el acceso a máquina virtual Just-In-Time de Security Center solo admite las máquinas virtuales que se han implementado mediante Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51ba8-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="51ba8-123">Para obtener más información sobre los modelos de implementación clásico y de Resource Manager, vea [La implementación de Azure Resource Manager frente a la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="51ba8-123">To learn more about the classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="51ba8-124">Uso del acceso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="51ba8-124">Using just in time access</span></span>

<span data-ttu-id="51ba8-125">En el icono **Acceso a VM Just-In-Time** de la hoja **Security Center** se muestra el número de máquinas virtuales configuradas para el acceso Just-In-Time y el número de solicitudes de acceso aprobadas en la última semana.</span><span class="sxs-lookup"><span data-stu-id="51ba8-125">The **Just in time VM access** tile on the **Security Center** blade shows the number of VMs configured for just in time access and the number of approved access requests made in the last week.</span></span>

<span data-ttu-id="51ba8-126">Seleccione el icono **Acceso a VM Just-In-Time**. Se abrirá la hoja **Acceso a VM Just-In-Time**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-126">Select the **Just in time VM access** tile and the **Just in time VM access** blade opens.</span></span>

![Icono Acceso a VM Just-In-Time][2]

<span data-ttu-id="51ba8-128">La hoja **Acceso a VM Just-In-Time** proporciona información sobre el estado de las máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="51ba8-128">The **Just in time VM access** blade provides information on the state of your VMs:</span></span>

- <span data-ttu-id="51ba8-129">**Configurado**: máquinas virtuales que se han configurado para admitir el acceso a máquina virtual Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="51ba8-129">**Configured** - VMs that have been configured to support just in time VM access.</span></span> <span data-ttu-id="51ba8-130">Los datos que se muestran son de la última semana e incluyen, para cada máquina virtual, el número de solicitudes aprobadas, la fecha y hora del último acceso y el último usuario.</span><span class="sxs-lookup"><span data-stu-id="51ba8-130">The data presented is for the last week and includes for each VM the number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="51ba8-131">**Recomendado**: máquinas virtuales que pueden admitir el acceso a máquina virtual Just-In-Time pero que no se han configurado para ello.</span><span class="sxs-lookup"><span data-stu-id="51ba8-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="51ba8-132">Se recomienda habilitar el control de acceso a máquina virtual Just-In-Time para estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="51ba8-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="51ba8-133">Vea cómo [habilitar el acceso a máquina virtual Just-In-Time](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="51ba8-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="51ba8-134">**Ninguna recomendación**: una máquina virtual podría no recomendarse por diversas razones:</span><span class="sxs-lookup"><span data-stu-id="51ba8-134">**No recommendation** - Reasons that can cause a VM not to be recommended are:</span></span>
  - <span data-ttu-id="51ba8-135">Falta el NSG: la solución Just-In-Time requiere que exista un NSG.</span><span class="sxs-lookup"><span data-stu-id="51ba8-135">Missing NSG - The just in time solution requires an NSG to be in place.</span></span>
  - <span data-ttu-id="51ba8-136">Máquina virtual clásica: en la actualidad, el acceso a máquina virtual Just-In-Time de Security Center solo admite las máquinas virtuales que se han implementado mediante Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51ba8-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="51ba8-137">La solución Just-In-Time no admite las implementaciones clásicas.</span><span class="sxs-lookup"><span data-stu-id="51ba8-137">A classic deployment is not supported by the just in time solution.</span></span>
  - <span data-ttu-id="51ba8-138">Otros: se incluirá una máquina virtual en esta categoría si la solución Just-In-Time está desactivada en la directiva de seguridad de la suscripción o del grupo de recursos, o si la máquina virtual no tiene una IP pública y no existe un NSG.</span><span class="sxs-lookup"><span data-stu-id="51ba8-138">Other - A VM is in this category if the just in time solution is turned off in the security policy of the subscription or the resource group, or that the VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="51ba8-139">Configurar una directiva de acceso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="51ba8-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="51ba8-140">Para seleccionar las máquinas virtuales que quiere habilitar:</span><span class="sxs-lookup"><span data-stu-id="51ba8-140">To select the VMs that you want to enable:</span></span>

1. <span data-ttu-id="51ba8-141">En la hoja **Acceso a VM Just-In-Time**, seleccione la pestaña **Recomendado**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-141">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Habilitar el acceso Just-In-Time][3]

2. <span data-ttu-id="51ba8-143">En **Máquinas virtuales**, seleccione las máquinas virtuales que quiere habilitar.</span><span class="sxs-lookup"><span data-stu-id="51ba8-143">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="51ba8-144">De este modo, se coloca una marca de verificación junto a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="51ba8-144">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="51ba8-145">Seleccione **Habilitar JIT en VM**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="51ba8-146">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="51ba8-147">Puertos predeterminados</span><span class="sxs-lookup"><span data-stu-id="51ba8-147">Default ports</span></span>

<span data-ttu-id="51ba8-148">Puede ver los puertos predeterminados que Security Center recomienda al habilitar Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="51ba8-148">You can see the default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="51ba8-149">En la hoja **Acceso a VM Just-In-Time**, seleccione la pestaña **Recomendado**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-149">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Mostrar los puertos predeterminados][6]

2. <span data-ttu-id="51ba8-151">En **Máquinas virtuales**, seleccione una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="51ba8-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="51ba8-152">De este modo, se coloca una marca de verificación junto a la máquina virtual y se abre la hoja **JIT VM access configuration** (Configuración de acceso a máquina virtual Just-In-Time).</span><span class="sxs-lookup"><span data-stu-id="51ba8-152">This puts a checkmark next to the VM and opens the **JIT VM access configuration** blade.</span></span> <span data-ttu-id="51ba8-153">En esta hoja se muestran los puertos predeterminados.</span><span class="sxs-lookup"><span data-stu-id="51ba8-153">This blade displays the default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="51ba8-154">Agregar puertos</span><span class="sxs-lookup"><span data-stu-id="51ba8-154">Add ports</span></span>

<span data-ttu-id="51ba8-155">Desde la hoja **JIT VM access configuration** (Configuración de acceso a máquina virtual Just-In-Time), también puede agregar y configurar un puerto nuevo en el que habilitar la solución Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="51ba8-155">From the **JIT VM access configuration** blade, you can also add and configure a new port on which you want to enable the just in time solution.</span></span>

1. <span data-ttu-id="51ba8-156">En la hoja **JIT VM access configuration** (Configuración de acceso a máquina virtual Just-In-Time), seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-156">On the **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="51ba8-157">Se abrirá la hoja **Add port configuration** (Agregar configuración de puerto).</span><span class="sxs-lookup"><span data-stu-id="51ba8-157">This opens the **Add port configuration** blade.</span></span>

  ![Configuración de puerto][7]

2. <span data-ttu-id="51ba8-159">En la hoja **Add port configuration** (Agregar configuración de puerto), debe identificar el puerto, el tipo de protocolo, las direcciones IP de origen permitidas y el tiempo de solicitud máximo.</span><span class="sxs-lookup"><span data-stu-id="51ba8-159">On **Add port configuration** blade, you identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="51ba8-160">Las direcciones IP de origen permitidas son los intervalos IP que pueden obtener acceso una vez que se ha aprobado una solicitud.</span><span class="sxs-lookup"><span data-stu-id="51ba8-160">Allowed source IPs are the IP ranges allowed to get access upon an approved request.</span></span>

  <span data-ttu-id="51ba8-161">El tiempo de solicitud máximo es el período de tiempo máximo durante el que puede estar abierto un puerto específico.</span><span class="sxs-lookup"><span data-stu-id="51ba8-161">Maximum request time is the maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="51ba8-162">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-162">Select **OK**.</span></span>

## <a name="requesting-access-to-a-vm"></a><span data-ttu-id="51ba8-163">Solicitar acceso a una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="51ba8-163">Requesting access to a VM</span></span>

<span data-ttu-id="51ba8-164">Para solicitar acceso a una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="51ba8-164">To request access to a VM:</span></span>

1. <span data-ttu-id="51ba8-165">En la hoja **Acceso a VM Just-In-Time**, seleccione la pestaña **Configurado**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-165">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="51ba8-166">En **Máquinas virtuales**, seleccione las máquinas virtuales para las que quiere habilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="51ba8-166">Under **VMs**, select the VMs that you want to enable access.</span></span> <span data-ttu-id="51ba8-167">De este modo, se coloca una marca de verificación junto a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="51ba8-167">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="51ba8-168">Seleccione **Solicitar acceso**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-168">Select **Request access**.</span></span> <span data-ttu-id="51ba8-169">Se abrirá la hoja **Solicitar acceso**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-169">This opens the **Request access** blade.</span></span>

  ![Solicitar acceso a una máquina virtual][4]

4. <span data-ttu-id="51ba8-171">En la hoja **Solicitar acceso**, configure para cada máquina virtual los puertos que deben abrirse, junto con la dirección IP de origen a la que se abre el puerto y el tiempo durante el que permanece abierto.</span><span class="sxs-lookup"><span data-stu-id="51ba8-171">On the **Request access** blade, you configure for each VM the ports to open along with the source IP that the port is opened to and the time window for which the port is opened.</span></span> <span data-ttu-id="51ba8-172">Solo puede solicitar acceso a los puertos que están configurados en la directiva Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="51ba8-172">You can request access only to the ports that are configured in the just in time policy.</span></span> <span data-ttu-id="51ba8-173">Cada puerto tiene un tiempo máximo permitido que se basa en la directiva Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="51ba8-173">Each port has a maximum allowed time derived from the just in time policy.</span></span>
5. <span data-ttu-id="51ba8-174">Seleccione **Open ports** (Abrir puertos).</span><span class="sxs-lookup"><span data-stu-id="51ba8-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="51ba8-175">Editar una directiva de acceso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="51ba8-175">Editing a just in time access policy</span></span>

<span data-ttu-id="51ba8-176">Puede cambiar la directiva Just-In-Time de una máquina virtual. Para ello, agregue y configure un puerto nuevo que se abra para esa máquina virtual, o bien cambie otro parámetro relacionado con un puerto ya protegido.</span><span class="sxs-lookup"><span data-stu-id="51ba8-176">You can change a VM's existing just in time policy by adding and configuring a new port to open for that VM, or by changing any other parameter related to an already protected port.</span></span>

<span data-ttu-id="51ba8-177">Para editar una directiva Just-In-Time de una máquina virtual, use la pestaña **Configurado**:</span><span class="sxs-lookup"><span data-stu-id="51ba8-177">In order to edit an existing just in time policy of a VM, the **Configured** tab is used:</span></span>

1. <span data-ttu-id="51ba8-178">En **Máquinas virtuales**, seleccione una máquina virtual para agregarle un puerto. Para ello, haga clic en los tres puntos situados en la fila de esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="51ba8-178">Under **VMs**, select a VM to add a port to by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="51ba8-179">Se abrirá un menú.</span><span class="sxs-lookup"><span data-stu-id="51ba8-179">This opens a menu.</span></span>
2. <span data-ttu-id="51ba8-180">Seleccione **Editar** en el menú.</span><span class="sxs-lookup"><span data-stu-id="51ba8-180">Select **Edit** in the menu.</span></span> <span data-ttu-id="51ba8-181">Se abrirá la hoja **JIT VM access configuration** (Configuración de acceso a máquina virtual Just-In-Time).</span><span class="sxs-lookup"><span data-stu-id="51ba8-181">This opens the **JIT VM access configuration** blade.</span></span>

  ![Editar directiva][8]

3. <span data-ttu-id="51ba8-183">En la hoja **JIT VM access configuration** (Configuración de acceso a máquina virtual Just-In-Time), puede hacer clic en un puerto ya protegido para modificar la configuración existente, o bien puede seleccionar **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-183">On the **JIT VM access configuration** blade, you can either edit the existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="51ba8-184">Se abrirá la hoja **Add port configuration** (Agregar configuración de puerto).</span><span class="sxs-lookup"><span data-stu-id="51ba8-184">This opens the **Add port configuration** blade.</span></span>

  ![Agregar un puerto][7]

4. <span data-ttu-id="51ba8-186">En la hoja **Add port configuration** (Agregar configuración de puerto), identifique el puerto, el tipo de protocolo, las direcciones IP de origen permitidas y el tiempo de solicitud máximo.</span><span class="sxs-lookup"><span data-stu-id="51ba8-186">On **Add port configuration** blade identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="51ba8-187">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-187">Select **OK**.</span></span>
6. <span data-ttu-id="51ba8-188">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="51ba8-189">Auditar la actividad del acceso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="51ba8-189">Auditing just in time access activity</span></span>

<span data-ttu-id="51ba8-190">Puede usar la búsqueda de registros para obtener información sobre las actividades de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="51ba8-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="51ba8-191">Para ver los registros:</span><span class="sxs-lookup"><span data-stu-id="51ba8-191">To view logs:</span></span>

1. <span data-ttu-id="51ba8-192">En la hoja **Acceso a VM Just-In-Time**, seleccione la pestaña **Configurado**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-192">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="51ba8-193">En **Máquinas virtuales**, seleccione una máquina virtual cuya información quiera ver. Para ello, haga clic en los tres puntos situados en la fila de esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="51ba8-193">Under **VMs**, select a VM to view information about by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="51ba8-194">Se abrirá un menú.</span><span class="sxs-lookup"><span data-stu-id="51ba8-194">This opens a menu.</span></span>
3. <span data-ttu-id="51ba8-195">Seleccione **Registro de actividades** en el menú.</span><span class="sxs-lookup"><span data-stu-id="51ba8-195">Select **Activity Log** in the menu.</span></span> <span data-ttu-id="51ba8-196">Se abrirá la hoja **Registro de actividades**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-196">This opens the **Activity log** blade.</span></span>

![Seleccionar el registro de actividades][9]

<span data-ttu-id="51ba8-198">La hoja **Registro de actividades** proporciona una vista filtrada de las operaciones anteriores para esa máquina virtual, junto con el tiempo, la fecha y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="51ba8-198">The **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Ver el registro de actividades][5]

<span data-ttu-id="51ba8-200">Para descargar la información del registro, seleccione **Haga clic aquí para descargar todos los elementos como archivo .csv**.</span><span class="sxs-lookup"><span data-stu-id="51ba8-200">You can download the log information by selecting **Click here to download all the items as CSV**.</span></span>

<span data-ttu-id="51ba8-201">Modifique los filtros y seleccione **Aplicar** para crear una búsqueda y un registro.</span><span class="sxs-lookup"><span data-stu-id="51ba8-201">Modify the filters and select **Apply** to create a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="51ba8-202">Usar el acceso a máquina virtual Just-In-Time mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ba8-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="51ba8-203">Para usar la solución Just-In-Time a través de PowerShell, asegúrese de que tiene la versión [más reciente](/powershell/azure/install-azurerm-ps) de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51ba8-203">In order to use the just in time solution via PowerShell, make sure you have the [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="51ba8-204">Una vez que lo haya hecho, debe instalar la versión [más reciente](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) de Azure Security Center desde la galería de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51ba8-204">Once you do, you need to install the [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from the PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="51ba8-205">Configurar una directiva Just-In-Time para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="51ba8-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="51ba8-206">Para configurar una directiva Just-In-Time en una máquina virtual específica, debe ejecutar este comando en la sesión de PowerShell: Set-ASCJITAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="51ba8-206">To configure a just in time policy on a specific VM, you need to run this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="51ba8-207">Consulte la documentación del cmdlet para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="51ba8-207">Follow the cmdlet documentation to learn more.</span></span>

### <a name="requesting-access-to-a-vm"></a><span data-ttu-id="51ba8-208">Solicitar acceso a una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="51ba8-208">Requesting access to a VM</span></span>

<span data-ttu-id="51ba8-209">Para obtener acceso a una máquina virtual específica que está protegida con la solución Just-In-Time, debe ejecutar este comando en la sesión de PowerShell: Invoke-ASCJITAccess.</span><span class="sxs-lookup"><span data-stu-id="51ba8-209">To access a specific VM that is protected with the just in time solution, you need to run this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="51ba8-210">Consulte la documentación del cmdlet para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="51ba8-210">Follow the cmdlet documentation to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51ba8-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="51ba8-211">Next steps</span></span>
<span data-ttu-id="51ba8-212">En este artículo, ha aprendido cómo el acceso a máquina virtual Just-In-Time en Security Center ayuda a controlar el acceso a máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="51ba8-212">In this article, you learned how just in time VM access in Security Center helps you control access to your Azure virtual machines.</span></span>

<span data-ttu-id="51ba8-213">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="51ba8-213">To learn more about Security Center, see the following:</span></span>

- <span data-ttu-id="51ba8-214">[Establecimiento de directivas de seguridad](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="51ba8-214">[Setting security policies](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="51ba8-215">[Administración de recomendaciones de seguridad](security-center-recommendations.md): conozca una serie de recomendaciones que le ayudarán a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="51ba8-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="51ba8-216">[Supervisión del estado de seguridad](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="51ba8-216">[Security health monitoring](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
- <span data-ttu-id="51ba8-217">[Administración y respuesta a las alertas de seguridad](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="51ba8-217">[Managing and responding to security alerts](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
- <span data-ttu-id="51ba8-218">[Supervisión de las soluciones de asociados](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="51ba8-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="51ba8-219">[Preguntas más frecuentes sobre Security Center](security-center-faq.md): encuentre las preguntas más frecuentes sobre el uso del servicio.</span><span class="sxs-lookup"><span data-stu-id="51ba8-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
- <span data-ttu-id="51ba8-220">[Blog de seguridad de Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="51ba8-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
