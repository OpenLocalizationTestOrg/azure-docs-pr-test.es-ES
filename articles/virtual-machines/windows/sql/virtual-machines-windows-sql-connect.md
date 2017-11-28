---
title: "aaaConnect tooa Máquina Virtual de SQL Server (Administrador de recursos) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconnect tooSQL Server ejecuta en una máquina Virtual en Azure. En este tema usa el modelo de implementación clásica de Hola. escenarios de Hello varían según la configuración de red de Hola y la ubicación de hello del cliente de Hola."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="e9407-105">Conectar tooa Máquina Virtual de SQL Server en Azure (Administrador de recursos)</span><span class="sxs-lookup"><span data-stu-id="e9407-105">Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9407-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e9407-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="e9407-107">Clásico</span><span class="sxs-lookup"><span data-stu-id="e9407-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e9407-108">Información general</span><span class="sxs-lookup"><span data-stu-id="e9407-108">Overview</span></span>

<span data-ttu-id="e9407-109">Este tema describe cómo tooconnect tooyour SQL Server instancia ejecuta en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9407-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="e9407-110">En él se describen algunos [escenarios de conectividad generales](#connection-scenarios) y se proporcionan los [pasos detallados para configurar la conectividad de SQL Server en una máquina virtual de Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="e9407-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="e9407-111">Para prefiere consultar un tutorial completo sobre aprovisionamiento y conectividad, consulte [Aprovisionamiento de una máquina virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e9407-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="e9407-112">Escenarios de conexión</span><span class="sxs-lookup"><span data-stu-id="e9407-112">Connection scenarios</span></span>

<span data-ttu-id="e9407-113">forma de Hello un cliente conecta tooSQL servidor se ejecuta en una máquina Virtual depende de la ubicación de Hola de cliente de Hola y la configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9407-113">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello networking configuration.</span></span>

<span data-ttu-id="e9407-114">Si se aprovisiona una VM de SQL Server en hello portal de Azure, tiene opción de Hola de especificación de tipo hello de **de conectividad de SQL**.</span><span class="sxs-lookup"><span data-stu-id="e9407-114">If you provision a SQL Server VM in hello Azure portal, you have hello option of specifying hello type of **SQL connectivity**.</span></span>

![Opción de conectividad SQL pública durante el aprovisionamiento](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="e9407-116">Estas son algunas de las opciones de conectividad:</span><span class="sxs-lookup"><span data-stu-id="e9407-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="e9407-117">Opción</span><span class="sxs-lookup"><span data-stu-id="e9407-117">Option</span></span> | <span data-ttu-id="e9407-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="e9407-118">Description</span></span> |
|---|---|
| <span data-ttu-id="e9407-119">**Pública**</span><span class="sxs-lookup"><span data-stu-id="e9407-119">**Public**</span></span> | <span data-ttu-id="e9407-120">Conectar tooSQL Server a través de hello internet</span><span class="sxs-lookup"><span data-stu-id="e9407-120">Connect tooSQL Server over hello internet</span></span> |
| <span data-ttu-id="e9407-121">**Privada**</span><span class="sxs-lookup"><span data-stu-id="e9407-121">**Private**</span></span> | <span data-ttu-id="e9407-122">Conectar tooSQL Server Hola misma red virtual</span><span class="sxs-lookup"><span data-stu-id="e9407-122">Connect tooSQL Server in hello same virtual network</span></span> |
| <span data-ttu-id="e9407-123">**Local**</span><span class="sxs-lookup"><span data-stu-id="e9407-123">**Local**</span></span> | <span data-ttu-id="e9407-124">Conectar tooSQL Server localmente en hello misma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e9407-124">Connect tooSQL Server locally on hello same virtual machine</span></span> | 

<span data-ttu-id="e9407-125">Hello las secciones siguientes explican hello **público** y **privada** opciones con más detalle.</span><span class="sxs-lookup"><span data-stu-id="e9407-125">hello following sections explain hello **Public** and **Private** options in more detail.</span></span>

## <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="e9407-126">Conectar tooSQL Server a través de Internet de Hola</span><span class="sxs-lookup"><span data-stu-id="e9407-126">Connect tooSQL Server over hello Internet</span></span>

<span data-ttu-id="e9407-127">Si desea que tooconnect tooyour el motor de base de datos de SQL Server desde Internet hello, seleccione **público** para hello **de conectividad de SQL** tipo en el portal de Hola durante el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="e9407-127">If you want tooconnect tooyour SQL Server database engine from hello Internet, select **Public** for hello **SQL connectivity** type in hello portal during provisioning.</span></span> <span data-ttu-id="e9407-128">portal de Hola Hola automáticamente lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e9407-128">hello portal automatically does hello following steps:</span></span>

* <span data-ttu-id="e9407-129">Habilita el protocolo TCP/IP de Hola para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e9407-129">Enables hello TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="e9407-130">Configura un hello tooopen de regla de firewall puerto TCP de SQL Server (predeterminado: 1433).</span><span class="sxs-lookup"><span data-stu-id="e9407-130">Configures a firewall rule tooopen hello SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="e9407-131">Habilita la autenticación de SQL Server, que es necesaria para el acceso público.</span><span class="sxs-lookup"><span data-stu-id="e9407-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="e9407-132">Configura el grupo de seguridad de red de hello en hello tráfico TCP de máquina virtual tooall en hello puerto de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e9407-132">Configures hello network security group on hello VM tooall TCP traffic on hello SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9407-133">imágenes de máquina virtual de Hola para hello programador de SQL Server y las ediciones Express no habilitan automáticamente protocolo Hola TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="e9407-133">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="e9407-134">Para las ediciones Developer y Express, debe usar el Administrador de configuración de SQL Server demasiado[habilitar manualmente el protocolo TCP/IP hello](#manualtcp) después de crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e9407-134">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="e9407-135">Cualquier cliente con acceso a internet puede conectarse a instancia de SQL Server toohello especificando la dirección IP pública de Hola de máquina virtual de Hola o cualquier etiqueta DNS que se asigna la dirección IP de toothat.</span><span class="sxs-lookup"><span data-stu-id="e9407-135">Any client with internet access can connect toohello SQL Server instance by specifying either hello public IP address of hello virtual machine or any DNS label assigned toothat IP address.</span></span> <span data-ttu-id="e9407-136">Si hello puerto de SQL Server es 1433, no es necesario toospecify en la cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9407-136">If hello SQL Server port is 1433, you do not need toospecify it in hello connection string.</span></span> <span data-ttu-id="e9407-137">Hola después de la cadena de conexión conecta tooa VM de SQL con una etiqueta DNS de `sqlvmlabel.eastus.cloudapp.azure.com` mediante la autenticación de SQL (también puede usar la dirección IP pública hello).</span><span class="sxs-lookup"><span data-stu-id="e9407-137">hello following connection string connects tooa SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use hello public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="e9407-138">Aunque esto habilita la conectividad de clientes en internet de Hola, esto no implica que cualquier usuario puede conectarse tooyour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e9407-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="e9407-139">Los clientes externos tengan toohello correcta nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="e9407-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="e9407-140">Sin embargo, para mayor seguridad, puede evitar el puerto conocido Hola 1433.</span><span class="sxs-lookup"><span data-stu-id="e9407-140">However, for additional security, you can avoid hello well-known port 1433.</span></span> <span data-ttu-id="e9407-141">Por ejemplo, si ha configurado toolisten de SQL Server en el puerto 1500 y firewall adecuados establecido y reglas del grupo de seguridad de red, podría conectarse mediante la anexión de nombre de servidor de número de puerto de hello toohello.</span><span class="sxs-lookup"><span data-stu-id="e9407-141">For example, if you configured SQL Server toolisten on port 1500 and established proper firewall and network security group rules, you could connect by appending hello port number toohello Server name.</span></span> <span data-ttu-id="e9407-142">Hello en el ejemplo siguiente se modifica Hola anterior mediante la adición de un número de puerto personalizado, **1500**, nombre del servidor toohello:</span><span class="sxs-lookup"><span data-stu-id="e9407-142">hello following example alters hello previous one by adding a custom port number, **1500**, toohello server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="e9407-143">Al consultar SQL Server en una máquina virtual sobre Hola internet, todos los datos de salida de hello Azure datacenter está sujeto toonormal [precios en las transferencias de datos de salida](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="e9407-143">When you query SQL Server in a VM over hello internet, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-toosql-server-within-a-virtual-network"></a><span data-ttu-id="e9407-144">Conectar tooSQL Server dentro de una red virtual</span><span class="sxs-lookup"><span data-stu-id="e9407-144">Connect tooSQL Server within a virtual network</span></span>

<span data-ttu-id="e9407-145">Cuando eliges **privada** para hello **de conectividad de SQL** tipo en el portal de hello, Azure configura la mayoría de los valores de hello idénticos demasiado**público**.</span><span class="sxs-lookup"><span data-stu-id="e9407-145">When you choose **Private** for hello **SQL connectivity** type in hello portal, Azure configures most of hello settings identical too**Public**.</span></span> <span data-ttu-id="e9407-146">Hola una diferencia es que no hay ningún tooallow de regla de grupo de seguridad de red fuera de tráfico en el puerto de SQL Server de hello (predeterminado: 1433).</span><span class="sxs-lookup"><span data-stu-id="e9407-146">hello one difference is that there is no network security group rule tooallow outside traffic on hello SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9407-147">imágenes de máquina virtual de Hola para hello programador de SQL Server y las ediciones Express no habilitan automáticamente protocolo Hola TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="e9407-147">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="e9407-148">Para las ediciones Developer y Express, debe usar el Administrador de configuración de SQL Server demasiado[habilitar manualmente el protocolo TCP/IP hello](#manualtcp) después de crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e9407-148">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="e9407-149">La conectividad privada se suele utilizar utiliza con [Virtual Network](../../../virtual-network/virtual-networks-overview.md), lo que permite varios escenarios.</span><span class="sxs-lookup"><span data-stu-id="e9407-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="e9407-150">Se pueden conectar máquinas virtuales de hello existe misma red virtual, incluso si esas máquinas virtuales en distintos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="e9407-150">You can connect VMs in hello same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="e9407-151">Asimismo, con una [VPN de sitio a sitio](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), puede crear una arquitectura híbrida que conecta las máquinas virtuales con redes y máquinas locales.</span><span class="sxs-lookup"><span data-stu-id="e9407-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="e9407-152">Redes virtuales también permiten toojoin su dominio de tooa de máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9407-152">Virtual networks also enable     you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="e9407-153">Se trata de tooSQL de hello única manera toouse autenticación de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e9407-153">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="e9407-154">Hello otros escenarios de conexión requieren autenticación de SQL con nombres de usuario y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="e9407-154">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="e9407-155">Si damos por hecho que ha configurado DNS en la red virtual, se puede conectar la instancia de SQL Server de tooyour especificando el nombre del equipo de hello VM de SQL Server en la cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9407-155">Assuming that you have configured DNS in your virtual network, you can connect tooyour SQL Server instance by specifying hello SQL Server VM computer name in hello connection string.</span></span> <span data-ttu-id="e9407-156">Hola siguiente ejemplo también se supone que también se ha configurado la autenticación de Windows y se ha concedido a ese usuario de hello instancia de SQL Server toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="e9407-156">hello following example also assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="e9407-157"><a id="change"></a> Cambio de la configuración de conectividad SQL</span><span class="sxs-lookup"><span data-stu-id="e9407-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="e9407-158">Puede cambiar la configuración de conectividad de hello para la máquina virtual de SQL Server en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9407-158">You can change hello connectivity settings for your SQL Server virtual machine in hello Azure portal.</span></span>

1. <span data-ttu-id="e9407-159">Hola portal de Azure, seleccione **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="e9407-159">In hello Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="e9407-160">Seleccione la VM con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e9407-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="e9407-161">En **Configuración**, haga clic en **Configuración de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e9407-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="e9407-162">Hola de cambio **el nivel de conectividad SQL** tooyour requerido configuración.</span><span class="sxs-lookup"><span data-stu-id="e9407-162">Change hello **SQL connectivity level** tooyour required setting.</span></span> <span data-ttu-id="e9407-163">También puede usar este Hola de toochange de área puerto de SQL Server o la configuración de autenticación de SQL Hola.</span><span class="sxs-lookup"><span data-stu-id="e9407-163">You can optionally use this area toochange hello SQL Server port or hello SQL Authentication settings.</span></span>

   ![Cambio de conectividad de SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="e9407-165">Espere unos minutos para hello toocomplete de actualización.</span><span class="sxs-lookup"><span data-stu-id="e9407-165">Wait several minutes for hello update toocomplete.</span></span>

   ![Notificación de actualización de la VM con SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="e9407-167"><a id="manualtcp"></a> Habilitación de TCP/IP para las ediciones Developer y Express</span><span class="sxs-lookup"><span data-stu-id="e9407-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="e9407-168">Al cambiar la configuración de conectividad de SQL Server, Azure no habilita automáticamente protocolo Hola TCP/IP para SQL Server Developer y las ediciones Express.</span><span class="sxs-lookup"><span data-stu-id="e9407-168">When changing SQL Server connectivity settings, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="e9407-169">Hola a continuación se explica cómo toomanually habilitar TCP/IP para que puedan conectarse de forma remota mediante una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="e9407-169">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="e9407-170">En primer lugar, conecte toohello máquina de SQL Server con Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="e9407-170">First, connect toohello SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="e9407-171">A continuación, habilite el protocolo Hola TCP/IP con **Administrador de configuración de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e9407-171">Next, enable hello TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="e9407-172">Conectarse con SSMS</span><span class="sxs-lookup"><span data-stu-id="e9407-172">Connect with SSMS</span></span>

<span data-ttu-id="e9407-173">Hello pasos siguientes muestran cómo toocreate etiqueta de un DNS opcional para la máquina virtual de Azure y, a continuación, conectan con SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="e9407-173">hello following steps show how toocreate an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="e9407-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e9407-174">Next Steps</span></span>

<span data-ttu-id="e9407-175">instrucciones de aprovisionamiento de toosee junto con estos pasos de conectividad, consulte [aprovisionamiento de una máquina Virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e9407-175">toosee provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="e9407-176">Para ver otros temas relacionados con toorunning SQL Server en máquinas virtuales de Azure, consulte [SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9407-176">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
