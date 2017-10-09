---
title: "obtener acceso aaaJust en la máquina virtual de tiempo en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este documento le guía a través de cómo justo a tiempo acceso VM en la Ayuda de Azure Security Center puede controlar acceso a tooyour Azure máquinas virtuales."
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
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="38794-103">Administrar el acceso a máquina virtual mediante Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="38794-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="38794-104">Solo en la máquina virtual (VM) de tiempo acceso puede ser usado toolock hacia abajo el tráfico entrante tooyour máquinas virtuales de Azure, reduce la exposición tooattacks al proporcionar un acceso sencillo tooconnect tooVMs cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="38794-104">Just in time virtual machine (VM) access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks while providing easy access tooconnect tooVMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="38794-105">Hola justo a la característica de tiempo está en la vista previa y disponible en hello nivel estándar del centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="38794-105">hello just in time feature is in preview and available on hello Standard tier of Security Center.</span></span>  <span data-ttu-id="38794-106">Vea [precios](security-center-pricing.md) toolearn más información acerca del centro de seguridad de los niveles de precios.</span><span class="sxs-lookup"><span data-stu-id="38794-106">See [Pricing](security-center-pricing.md) toolearn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="38794-107">Escenario de ataque</span><span class="sxs-lookup"><span data-stu-id="38794-107">Attack scenario</span></span>

<span data-ttu-id="38794-108">Fuerza bruta ataques normalmente los puertos de administración de destino como un tooa de acceso de medios toogain máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="38794-108">Brute force attacks commonly target management ports as a means toogain access tooa VM.</span></span> <span data-ttu-id="38794-109">Si se realiza correctamente, un atacante puede tomar el control sobre Hola VM y establecer un punto de apoyo en su entorno.</span><span class="sxs-lookup"><span data-stu-id="38794-109">If successful, an attacker can take control over hello VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="38794-110">Ataque por fuerza bruta de una manera tooreduce exposición tooa es toolimit Hola cantidad de tiempo que un puerto está abierto.</span><span class="sxs-lookup"><span data-stu-id="38794-110">One way tooreduce exposure tooa brute force attack is toolimit hello amount of time that a port is open.</span></span> <span data-ttu-id="38794-111">Los puertos de administración es no necesidad toobe abrir en todo momento.</span><span class="sxs-lookup"><span data-stu-id="38794-111">Management ports do not need toobe open at all times.</span></span> <span data-ttu-id="38794-112">Solo necesitan toobe abiertos mientras el equipo está conectado toohello VM, por ejemplo tooperform tareas de administración o mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="38794-112">They only need toobe open while you are connected toohello VM, for example tooperform management or maintenance tasks.</span></span> <span data-ttu-id="38794-113">Cuando se habilita justo a tiempo, el centro de seguridad usa [grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md) reglas (NSG), que restringen acceso toomanagement puertos, por lo que no se destinen a los atacantes.</span><span class="sxs-lookup"><span data-stu-id="38794-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access toomanagement ports so they cannot be targeted by attackers.</span></span>

![Escenario Just-In-Time][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="38794-115">¿Cómo funciona el acceso Just-In-Time?</span><span class="sxs-lookup"><span data-stu-id="38794-115">How does just in time access work?</span></span>

<span data-ttu-id="38794-116">Cuando se habilita justo a tiempo, el centro de seguridad para bloquear el tráfico entrante tooyour máquinas virtuales de Azure mediante la creación de una regla de NSG.</span><span class="sxs-lookup"><span data-stu-id="38794-116">When just in time is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="38794-117">Seleccionar puertos hello en hello VM toowhich se bloqueará el tráfico entrante hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="38794-117">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="38794-118">Estos puertos se controlan mediante Hola justo a tiempo la solución.</span><span class="sxs-lookup"><span data-stu-id="38794-118">These ports are controlled by hello just in time solution.</span></span>

<span data-ttu-id="38794-119">Cuando un usuario solicita acceso tooa VM, el centro de seguridad comprueba que el usuario hello tiene [Control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md) permisos que conceden acceso de escritura para hello recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="38794-119">When a user requests access tooa VM, Security Center checks that hello user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for hello Azure resource.</span></span> <span data-ttu-id="38794-120">Si tienen permisos de escritura, se aprueba la solicitud de Hola y el centro de seguridad configura automáticamente los grupos de seguridad de red (NSG) de hello tooallow tráfico toohello administración puertos de entrada para la cantidad de Hola de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="38794-120">If they have write permissions, hello request is approved and Security Center automatically configures hello Network Security Groups (NSGs) tooallow inbound traffic toohello management ports for hello amount of time you specified.</span></span> <span data-ttu-id="38794-121">Una vez transcurrido el tiempo de hello, centro de seguridad restaura el estado anterior de hello NSG tootheir.</span><span class="sxs-lookup"><span data-stu-id="38794-121">After hello time has expired, Security Center restores hello NSGs tootheir previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="38794-122">En la actualidad, el acceso a máquina virtual Just-In-Time de Security Center solo admite las máquinas virtuales que se han implementado mediante Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="38794-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="38794-123">toolearn más sobre Hola clásico y modelos de implementación del Administrador de recursos, consulte [Azure Resource Manager frente a la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="38794-123">toolearn more about hello classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="38794-124">Uso del acceso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="38794-124">Using just in time access</span></span>

<span data-ttu-id="38794-125">Hola **en el acceso en tiempo de máquina virtual** icono hello **centro de seguridad** hoja muestra el número de Hola de máquinas virtuales configuradas para justo a tiempo acceso y Hola el número de solicitudes de acceso autorizado a realizadas en hello última semana.</span><span class="sxs-lookup"><span data-stu-id="38794-125">hello **Just in time VM access** tile on hello **Security Center** blade shows hello number of VMs configured for just in time access and hello number of approved access requests made in hello last week.</span></span>

<span data-ttu-id="38794-126">Seleccione hello **en el acceso en tiempo de máquina virtual** hello y mosaico **en el acceso en tiempo de máquina virtual** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="38794-126">Select hello **Just in time VM access** tile and hello **Just in time VM access** blade opens.</span></span>

![Icono Acceso a VM Just-In-Time][2]

<span data-ttu-id="38794-128">Hola **en el acceso en tiempo de máquina virtual** hoja proporciona información sobre el estado de Hola de las máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="38794-128">hello **Just in time VM access** blade provides information on hello state of your VMs:</span></span>

- <span data-ttu-id="38794-129">**Configurar** -máquinas virtuales que se han configurado toosupport solo en el acceso en tiempo de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="38794-129">**Configured** - VMs that have been configured toosupport just in time VM access.</span></span> <span data-ttu-id="38794-130">datos de Hello presentados es para hello última semana e incluyen para cada número de Hola VM de las solicitudes aprobadas, la fecha del último acceso y la hora y último usuario.</span><span class="sxs-lookup"><span data-stu-id="38794-130">hello data presented is for hello last week and includes for each VM hello number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="38794-131">**Recomendado**: máquinas virtuales que pueden admitir el acceso a máquina virtual Just-In-Time pero que no se han configurado para ello.</span><span class="sxs-lookup"><span data-stu-id="38794-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="38794-132">Se recomienda habilitar el control de acceso a máquina virtual Just-In-Time para estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="38794-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="38794-133">Vea cómo [habilitar el acceso a máquina virtual Just-In-Time](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="38794-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="38794-134">**Sin recomendación** -razones que pueden provocar una máquina virtual no se recomienda toobe son:</span><span class="sxs-lookup"><span data-stu-id="38794-134">**No recommendation** - Reasons that can cause a VM not toobe recommended are:</span></span>
  - <span data-ttu-id="38794-135">Falta el NSG - Hola justo a tiempo la solución requiere un toobe NSG en su lugar.</span><span class="sxs-lookup"><span data-stu-id="38794-135">Missing NSG - hello just in time solution requires an NSG toobe in place.</span></span>
  - <span data-ttu-id="38794-136">Máquina virtual clásica: en la actualidad, el acceso a máquina virtual Just-In-Time de Security Center solo admite las máquinas virtuales que se han implementado mediante Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="38794-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="38794-137">No se admite una implementación clásica Hola justo a tiempo la solución.</span><span class="sxs-lookup"><span data-stu-id="38794-137">A classic deployment is not supported by hello just in time solution.</span></span>
  - <span data-ttu-id="38794-138">Otros: una máquina virtual está en esta categoría si Hola justo a tiempo solución está desactivada en la directiva de seguridad de Hola de suscripción de Hola o grupo de recursos de hello, o que hello VM no tiene una IP pública y no tiene un NSG en su lugar.</span><span class="sxs-lookup"><span data-stu-id="38794-138">Other - A VM is in this category if hello just in time solution is turned off in hello security policy of hello subscription or hello resource group, or that hello VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="38794-139">Configurar una directiva de acceso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="38794-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="38794-140">Hola tooselect máquinas virtuales que desea tooenable:</span><span class="sxs-lookup"><span data-stu-id="38794-140">tooselect hello VMs that you want tooenable:</span></span>

1. <span data-ttu-id="38794-141">En hello **en el acceso en tiempo de máquina virtual** hoja, seleccione hello **recomendado** ficha.</span><span class="sxs-lookup"><span data-stu-id="38794-141">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Habilitar el acceso Just-In-Time][3]

2. <span data-ttu-id="38794-143">En **máquinas virtuales**, seleccione hello las máquinas virtuales que desea tooenable.</span><span class="sxs-lookup"><span data-stu-id="38794-143">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="38794-144">Esto coloca una máquina virtual de tooa siguiente marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="38794-144">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="38794-145">Seleccione **Habilitar JIT en VM**.</span><span class="sxs-lookup"><span data-stu-id="38794-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="38794-146">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="38794-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="38794-147">Puertos predeterminados</span><span class="sxs-lookup"><span data-stu-id="38794-147">Default ports</span></span>

<span data-ttu-id="38794-148">Puede ver los puertos predeterminados de Hola que el centro de seguridad se recomienda habilitar justo a tiempo.</span><span class="sxs-lookup"><span data-stu-id="38794-148">You can see hello default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="38794-149">En hello **en el acceso en tiempo de máquina virtual** hoja, seleccione hello **recomendado** ficha.</span><span class="sxs-lookup"><span data-stu-id="38794-149">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Mostrar los puertos predeterminados][6]

2. <span data-ttu-id="38794-151">En **Máquinas virtuales**, seleccione una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="38794-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="38794-152">Esto coloca una marca de verificación siguiente toohello VM y abre hello **configuración de acceso de VM de JIT** hoja.</span><span class="sxs-lookup"><span data-stu-id="38794-152">This puts a checkmark next toohello VM and opens hello **JIT VM access configuration** blade.</span></span> <span data-ttu-id="38794-153">Esta hoja muestra los puertos predeterminados que Hola.</span><span class="sxs-lookup"><span data-stu-id="38794-153">This blade displays hello default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="38794-154">Agregar puertos</span><span class="sxs-lookup"><span data-stu-id="38794-154">Add ports</span></span>

<span data-ttu-id="38794-155">De hello **configuración de acceso de VM de JIT** hoja, también puede agregar y configurar un puerto nuevo en el que desea tooenable Hola justo a tiempo la solución.</span><span class="sxs-lookup"><span data-stu-id="38794-155">From hello **JIT VM access configuration** blade, you can also add and configure a new port on which you want tooenable hello just in time solution.</span></span>

1. <span data-ttu-id="38794-156">En hello **configuración de acceso de VM de JIT** hoja, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="38794-156">On hello **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="38794-157">Se abrirá hello **Agregar configuración de puerto** hoja.</span><span class="sxs-lookup"><span data-stu-id="38794-157">This opens hello **Add port configuration** blade.</span></span>

  ![Configuración de puerto][7]

2. <span data-ttu-id="38794-159">En **Agregar configuración de puerto** hoja, se identifica el puerto de hello, tipo de protocolo, tiempo de solicitud de direcciones IP de origen y el máximo permitido.</span><span class="sxs-lookup"><span data-stu-id="38794-159">On **Add port configuration** blade, you identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="38794-160">Permiten direcciones IP de origen son Hola IP intervalos permitidos tooget acceso en una solicitud aprobada.</span><span class="sxs-lookup"><span data-stu-id="38794-160">Allowed source IPs are hello IP ranges allowed tooget access upon an approved request.</span></span>

  <span data-ttu-id="38794-161">Tiempo máximo de la solicitud es el período de tiempo máximo de Hola que se puede abrir un puerto específico.</span><span class="sxs-lookup"><span data-stu-id="38794-161">Maximum request time is hello maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="38794-162">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="38794-162">Select **OK**.</span></span>

## <a name="requesting-access-tooa-vm"></a><span data-ttu-id="38794-163">Solicitar acceso tooa VM</span><span class="sxs-lookup"><span data-stu-id="38794-163">Requesting access tooa VM</span></span>

<span data-ttu-id="38794-164">toorequest acceso tooa VM:</span><span class="sxs-lookup"><span data-stu-id="38794-164">toorequest access tooa VM:</span></span>

1. <span data-ttu-id="38794-165">En hello **en el acceso en tiempo de máquina virtual** hoja, seleccione hello **configurado** ficha.</span><span class="sxs-lookup"><span data-stu-id="38794-165">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="38794-166">En **máquinas virtuales**, seleccione hello las máquinas virtuales que desea tooenable access.</span><span class="sxs-lookup"><span data-stu-id="38794-166">Under **VMs**, select hello VMs that you want tooenable access.</span></span> <span data-ttu-id="38794-167">Esto coloca una máquina virtual de tooa siguiente marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="38794-167">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="38794-168">Seleccione **Solicitar acceso**.</span><span class="sxs-lookup"><span data-stu-id="38794-168">Select **Request access**.</span></span> <span data-ttu-id="38794-169">Se abrirá hello **solicitar acceso** hoja.</span><span class="sxs-lookup"><span data-stu-id="38794-169">This opens hello **Request access** blade.</span></span>

  ![Tooa de acceso de solicitud de máquina virtual][4]

4. <span data-ttu-id="38794-171">En hello **solicitar acceso** hoja, configurar para cada tooopen de puertos VM Hola junto con la dirección IP de origen de Hola Hola puerto está abierto tooand Hola período para qué hello puerto esté abierto.</span><span class="sxs-lookup"><span data-stu-id="38794-171">On hello **Request access** blade, you configure for each VM hello ports tooopen along with hello source IP that hello port is opened tooand hello time window for which hello port is opened.</span></span> <span data-ttu-id="38794-172">Puede solicitar puertos toohello solo de acceso que están configurados en hello solo en la directiva de tiempo.</span><span class="sxs-lookup"><span data-stu-id="38794-172">You can request access only toohello ports that are configured in hello just in time policy.</span></span> <span data-ttu-id="38794-173">Cada puerto tiene un tiempo máximo permitido derivan Hola solo en la directiva de tiempo.</span><span class="sxs-lookup"><span data-stu-id="38794-173">Each port has a maximum allowed time derived from hello just in time policy.</span></span>
5. <span data-ttu-id="38794-174">Seleccione **Open ports** (Abrir puertos).</span><span class="sxs-lookup"><span data-stu-id="38794-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="38794-175">Editar una directiva de acceso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="38794-175">Editing a just in time access policy</span></span>

<span data-ttu-id="38794-176">Puede cambiar la máquina virtual existente solo en la directiva de tiempo agregando y configurando un nuevo tooopen de puerto para esa máquina virtual, o al cambiar cualquier otro parámetro tooan relacionado ya protegida puerto.</span><span class="sxs-lookup"><span data-stu-id="38794-176">You can change a VM's existing just in time policy by adding and configuring a new port tooopen for that VM, or by changing any other parameter related tooan already protected port.</span></span>

<span data-ttu-id="38794-177">En Ordenar tooedit existente solo en la directiva de tiempo de una máquina virtual, hello **configurado** ficha se utiliza:</span><span class="sxs-lookup"><span data-stu-id="38794-177">In order tooedit an existing just in time policy of a VM, hello **Configured** tab is used:</span></span>

1. <span data-ttu-id="38794-178">En **máquinas virtuales**, seleccione una máquina virtual tooadd un tooby de puerto al hacer clic en puntos de hello tres dentro de la fila de Hola para esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="38794-178">Under **VMs**, select a VM tooadd a port tooby clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="38794-179">Se abrirá un menú.</span><span class="sxs-lookup"><span data-stu-id="38794-179">This opens a menu.</span></span>
2. <span data-ttu-id="38794-180">Seleccione **editar** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="38794-180">Select **Edit** in hello menu.</span></span> <span data-ttu-id="38794-181">Se abrirá hello **configuración de acceso de VM de JIT** hoja.</span><span class="sxs-lookup"><span data-stu-id="38794-181">This opens hello **JIT VM access configuration** blade.</span></span>

  ![Editar directiva][8]

3. <span data-ttu-id="38794-183">En hello **configuración de acceso de VM de JIT** hoja, puede modificar la configuración existente de Hola de un puerto ya protegido haciendo clic en su puerto, o puede seleccionar **agregar**.</span><span class="sxs-lookup"><span data-stu-id="38794-183">On hello **JIT VM access configuration** blade, you can either edit hello existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="38794-184">Se abrirá hello **Agregar configuración de puerto** hoja.</span><span class="sxs-lookup"><span data-stu-id="38794-184">This opens hello **Add port configuration** blade.</span></span>

  ![Agregar un puerto][7]

4. <span data-ttu-id="38794-186">En **Agregar configuración de puerto** hoja identificar el puerto de hello, tipo de protocolo, direcciones IP de origen permitido y tiempo máximo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="38794-186">On **Add port configuration** blade identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="38794-187">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="38794-187">Select **OK**.</span></span>
6. <span data-ttu-id="38794-188">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="38794-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="38794-189">Auditar la actividad del acceso Just-In-Time</span><span class="sxs-lookup"><span data-stu-id="38794-189">Auditing just in time access activity</span></span>

<span data-ttu-id="38794-190">Puede usar la búsqueda de registros para obtener información sobre las actividades de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="38794-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="38794-191">registros de tooview:</span><span class="sxs-lookup"><span data-stu-id="38794-191">tooview logs:</span></span>

1. <span data-ttu-id="38794-192">En hello **en el acceso en tiempo de máquina virtual** hoja, seleccione hello **configurado** ficha.</span><span class="sxs-lookup"><span data-stu-id="38794-192">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="38794-193">En **máquinas virtuales**, seleccione una información de tooview VM sobre haciendo clic en puntos de hello tres dentro de la fila de Hola para esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="38794-193">Under **VMs**, select a VM tooview information about by clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="38794-194">Se abrirá un menú.</span><span class="sxs-lookup"><span data-stu-id="38794-194">This opens a menu.</span></span>
3. <span data-ttu-id="38794-195">Seleccione **registro de actividad** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="38794-195">Select **Activity Log** in hello menu.</span></span> <span data-ttu-id="38794-196">Se abrirá hello **registro de actividad** hoja.</span><span class="sxs-lookup"><span data-stu-id="38794-196">This opens hello **Activity log** blade.</span></span>

![Seleccionar el registro de actividades][9]

<span data-ttu-id="38794-198">Hola **registro de actividad** hoja proporciona una vista filtrada de las operaciones anteriores para esa máquina virtual junto con el tiempo, la fecha y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="38794-198">hello **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Ver el registro de actividades][5]

<span data-ttu-id="38794-200">Puede descargar información del registro de hello seleccionando **haga clic aquí toodownload todos los elementos de hello como CSV**.</span><span class="sxs-lookup"><span data-stu-id="38794-200">You can download hello log information by selecting **Click here toodownload all hello items as CSV**.</span></span>

<span data-ttu-id="38794-201">Modificar filtros de Hola y seleccione **aplicar** toocreate una búsqueda y un registro.</span><span class="sxs-lookup"><span data-stu-id="38794-201">Modify hello filters and select **Apply** toocreate a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="38794-202">Usar el acceso a máquina virtual Just-In-Time mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="38794-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="38794-203">Hola toouse de orden justo a tiempo la solución a través de PowerShell, asegúrese de que tiene hello [más reciente](/powershell/azure/install-azurerm-ps) versión de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="38794-203">In order toouse hello just in time solution via PowerShell, make sure you have hello [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="38794-204">Una vez que lo hace, deberá hello tooinstall [más reciente](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) centro de seguridad de Azure desde la Galería de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="38794-204">Once you do, you need tooinstall hello [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from hello PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="38794-205">Configurar una directiva Just-In-Time para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="38794-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="38794-206">tooconfigure un solo en la directiva de tiempo en una VM específica, necesite toorun este comando en la sesión de PowerShell: Set-ASCJITAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="38794-206">tooconfigure a just in time policy on a specific VM, you need toorun this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="38794-207">Siga Hola cmdlet documentación toolearn más.</span><span class="sxs-lookup"><span data-stu-id="38794-207">Follow hello cmdlet documentation toolearn more.</span></span>

### <a name="requesting-access-tooa-vm"></a><span data-ttu-id="38794-208">Solicitar acceso tooa VM</span><span class="sxs-lookup"><span data-stu-id="38794-208">Requesting access tooa VM</span></span>

<span data-ttu-id="38794-209">Hola tooaccess una VM específica que está protegido con justo a tiempo la solución, deberá toorun este comando en la sesión de PowerShell: ASCJITAccess invocar.</span><span class="sxs-lookup"><span data-stu-id="38794-209">tooaccess a specific VM that is protected with hello just in time solution, you need toorun this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="38794-210">Siga Hola cmdlet documentación toolearn más.</span><span class="sxs-lookup"><span data-stu-id="38794-210">Follow hello cmdlet documentation toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38794-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="38794-211">Next steps</span></span>
<span data-ttu-id="38794-212">En este artículo, ha aprendido cómo justo a tiempo acceso de VM en el centro de seguridad le ayuda a controlar el acceso tooyour Azure máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="38794-212">In this article, you learned how just in time VM access in Security Center helps you control access tooyour Azure virtual machines.</span></span>

<span data-ttu-id="38794-213">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="38794-213">toolearn more about Security Center, see hello following:</span></span>

- <span data-ttu-id="38794-214">[Configuración de directivas de seguridad](security-center-policies.md) : más información cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="38794-214">[Setting security policies](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="38794-215">[Administración de recomendaciones de seguridad](security-center-recommendations.md): conozca una serie de recomendaciones que le ayudarán a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="38794-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="38794-216">[Supervisión de estado de seguridad](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="38794-216">[Security health monitoring](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
- <span data-ttu-id="38794-217">[Administrar y responder a alertas de toosecurity](security-center-managing-and-responding-alerts.md) : más información cómo toomanage y que responden las alertas de toosecurity.</span><span class="sxs-lookup"><span data-stu-id="38794-217">[Managing and responding toosecurity alerts](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
- <span data-ttu-id="38794-218">[Supervisión de soluciones de socios comerciales](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="38794-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="38794-219">[Preguntas más frecuentes del centro de seguridad](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="38794-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
- <span data-ttu-id="38794-220">[Blog de seguridad de Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="38794-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


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
