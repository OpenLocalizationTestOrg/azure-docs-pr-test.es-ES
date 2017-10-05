---
title: "Creación de clústeres de MySQL con conjuntos con equilibrio de carga | Microsoft Docs"
description: "Configuración de un clúster MySQL Linux de carga equilibrada y alta disponibilidad creado con el modelo de implementación clásica en Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 4eaf86c9ac3e4dc2b51b88383626eda774cab0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-load-balanced-sets-to-clusterize-mysql-on-linux"></a><span data-ttu-id="755c0-103">Uso de conjuntos de carga equilibrada para crear clústeres en MySQL en Linux</span><span class="sxs-lookup"><span data-stu-id="755c0-103">Use load-balanced sets to clusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="755c0-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el modelo clásico.</span><span class="sxs-lookup"><span data-stu-id="755c0-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="755c0-105">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="755c0-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="755c0-106">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="755c0-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="755c0-107">Hay disponible una [plantilla de Resource Manager](https://azure.microsoft.com/documentation/templates/mysql-replication/) si necesita implementar un clúster de MySQL.</span><span class="sxs-lookup"><span data-stu-id="755c0-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need to deploy a MySQL cluster.</span></span>

<span data-ttu-id="755c0-108">Este artículo explora e ilustra los diferentes enfoques disponibles para implementar servicios basados en Linux altamente disponibles en Microsoft Azure, explorando la alta disponibilidad de MySQL Server como base.</span><span class="sxs-lookup"><span data-stu-id="755c0-108">This article explores and illustrates the different approaches available to deploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="755c0-109">En [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)hay un vídeo disponible que ilustra este enfoque.</span><span class="sxs-lookup"><span data-stu-id="755c0-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="755c0-110">Describiremos una solución de alta disponibilidad de MySQL de un solo maestro y dos nodos independientes basada en DRBD, Corosync y Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="755c0-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="755c0-111">Solamente se ejecuta un nodo MySQL en cada momento.</span><span class="sxs-lookup"><span data-stu-id="755c0-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="755c0-112">La lectura y escritura desde el recurso DRBD también se limitan a un solo nodo en cada momento.</span><span class="sxs-lookup"><span data-stu-id="755c0-112">Reading and writing from the DRBD resource is also limited to only one node at a time.</span></span>

<span data-ttu-id="755c0-113">No se necesita una solución VIP como LVS porque usará conjuntos de carga equilibrada de Microsoft Azure para proporcionar tanto funcionalidad round robin como detección, eliminación y recuperación estable de puntos de conexión de VIP.</span><span class="sxs-lookup"><span data-stu-id="755c0-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure to provide round-robin functionality and endpoint detection, removal, and graceful recovery of the VIP.</span></span> <span data-ttu-id="755c0-114">VIP es una dirección IPv4 globalmente enrutable asignada por Microsoft Azure cuando crea el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="755c0-114">The VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create the cloud service.</span></span>

<span data-ttu-id="755c0-115">Hay otras posibles arquitecturas para MySQL, como, por ejemplo, NBD Cluster, Percona, Galera y diversas soluciones middleware que incluyen, al menos, una disponible como máquina virtual en [VM Depot](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="755c0-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="755c0-116">Mientras que estas soluciones pueden replicarse en unidifusión frente a multidifusión o difusión, y no se basan en almacenamiento compartido o interfaces de varias redes, los escenarios deben ser fáciles de implementar en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="755c0-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, the scenarios should be easy to deploy on Microsoft Azure.</span></span>

<span data-ttu-id="755c0-117">Estas arquitecturas de clúster se pueden extender a otros productos como PostgreSQL y OpenLDAP de forma similar.</span><span class="sxs-lookup"><span data-stu-id="755c0-117">These clustering architectures can be extended to other products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="755c0-118">Por ejemplo, este procedimiento de equilibro de carga independiente se probó correctamente con OpenLDAP multimaestro y puede verlo en nuestro blog de Channel 9.</span><span class="sxs-lookup"><span data-stu-id="755c0-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="755c0-119">Prepárese</span><span class="sxs-lookup"><span data-stu-id="755c0-119">Get ready</span></span>
<span data-ttu-id="755c0-120">Necesita los siguientes recursos y capacidades:</span><span class="sxs-lookup"><span data-stu-id="755c0-120">You need the following resources and abilities:</span></span>

  - <span data-ttu-id="755c0-121">Una cuenta de Microsoft Azure con una suscripción válida que permita crear al menos dos VM (en este ejemplo se usó XS)</span><span class="sxs-lookup"><span data-stu-id="755c0-121">A Microsoft Azure account with a valid subscription, able to create at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="755c0-122">Una red y una subred</span><span class="sxs-lookup"><span data-stu-id="755c0-122">A network and a subnet</span></span>
  - <span data-ttu-id="755c0-123">Un grupo de afinidad</span><span class="sxs-lookup"><span data-stu-id="755c0-123">An affinity group</span></span>
  - <span data-ttu-id="755c0-124">Un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="755c0-124">An availability set</span></span>
  - <span data-ttu-id="755c0-125">La capacidad para crear VHD en la misma región que el servicio en la nube y adjuntarlos a las VM de Linux</span><span class="sxs-lookup"><span data-stu-id="755c0-125">The ability to create VHDs in the same region as the cloud service and attach them to the Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="755c0-126">Entorno probado</span><span class="sxs-lookup"><span data-stu-id="755c0-126">Tested environment</span></span>
* <span data-ttu-id="755c0-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="755c0-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="755c0-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="755c0-128">DRBD</span></span>
  * <span data-ttu-id="755c0-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="755c0-129">MySQL Server</span></span>
  * <span data-ttu-id="755c0-130">Corosync y Pacemaker</span><span class="sxs-lookup"><span data-stu-id="755c0-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="755c0-131">Grupo de afinidad</span><span class="sxs-lookup"><span data-stu-id="755c0-131">Affinity group</span></span>
<span data-ttu-id="755c0-132">Cree un grupo de afinidad para la solución. Para ello, inicie sesión en el portal de Azure clásico, seleccione **Configuración** y cree el grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="755c0-132">Create an affinity group for the solution by signing in to the Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="755c0-133">Los recursos asignados creados más tarde se asignarán a este grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="755c0-133">Allocated resources created later will be assigned to this affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="755c0-134">Redes</span><span class="sxs-lookup"><span data-stu-id="755c0-134">Networks</span></span>
<span data-ttu-id="755c0-135">Se crea una nueva red y, a su vez, se crea una subred dentro de la red.</span><span class="sxs-lookup"><span data-stu-id="755c0-135">A new network is created, and a subnet is created inside the network.</span></span> <span data-ttu-id="755c0-136">En este ejemplo se usa una red 10.10.10.0/24 con una sola subred /24 dentro.</span><span class="sxs-lookup"><span data-stu-id="755c0-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="755c0-137">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="755c0-137">Virtual machines</span></span>
<span data-ttu-id="755c0-138">La primera VM Ubuntu 13.10 se crea usando una imagen de la galería de Ubuntu refrendada llamada `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="755c0-138">The first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="755c0-139">En el proceso, se crea un nuevo servicio en la nube llamado hadb.</span><span class="sxs-lookup"><span data-stu-id="755c0-139">A new cloud service is created in the process, called hadb.</span></span> <span data-ttu-id="755c0-140">El nombre refleja la naturaleza compartida y de carga equilibrada que tendrá el servicio cuando agreguemos más recursos.</span><span class="sxs-lookup"><span data-stu-id="755c0-140">This name illustrates the shared, load-balanced nature that the service will have when more resources are added.</span></span> <span data-ttu-id="755c0-141">La creación de `hadb01` no presenta ningún problema y se completa mediante el portal.</span><span class="sxs-lookup"><span data-stu-id="755c0-141">The creation of `hadb01` is uneventful and completed by using the portal.</span></span> <span data-ttu-id="755c0-142">Se crea un punto de conexión para SSH automáticamente y se selecciona la nueva red.</span><span class="sxs-lookup"><span data-stu-id="755c0-142">An endpoint for SSH is automatically created, and the new network is selected.</span></span> <span data-ttu-id="755c0-143">Ahora puede crear un conjunto de disponibilidad para las VM.</span><span class="sxs-lookup"><span data-stu-id="755c0-143">Now you can create an availability set for the VMs.</span></span>

<span data-ttu-id="755c0-144">Tras crear la primera VM (técnicamente, cuando se crea el servicio en la nube), creamos la segunda máquina virtual, `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="755c0-144">After the first VM is created (technically, when the cloud service is created), create the second VM, `hadb02`.</span></span> <span data-ttu-id="755c0-145">Para la segunda VM, usaremos la VM Ubuntu 13.10 desde la galería a través del Portal, pero usaremos un servicio en la nube existente, `hadb.cloudapp.net`, en lugar de crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="755c0-145">For the second VM, use Ubuntu 13.10 VM from the Gallery by using the portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="755c0-146">La red y el conjunto de disponibilidad se deben seleccionar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="755c0-146">The network and availability set should be automatically selected.</span></span> <span data-ttu-id="755c0-147">También se creará un extremo SSH.</span><span class="sxs-lookup"><span data-stu-id="755c0-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="755c0-148">Una vez creadas ambas VM, tomaremos nota del puerto SSH para `hadb01` (TCP 22) y `hadb02` (automáticamente asignado por Azure).</span><span class="sxs-lookup"><span data-stu-id="755c0-148">After both VMs have been created, take note of the SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="755c0-149">Almacenamiento acoplado</span><span class="sxs-lookup"><span data-stu-id="755c0-149">Attached storage</span></span>
<span data-ttu-id="755c0-150">Acoplamos un nuevo disco a ambas VM y creamos discos de 5 GB en el proceso.</span><span class="sxs-lookup"><span data-stu-id="755c0-150">Attach a new disk to both VMs and create 5-GB disks in the process.</span></span> <span data-ttu-id="755c0-151">Los discos se hospedan en el contenedor VHD en uso para nuestros discos del sistema operativo principal.</span><span class="sxs-lookup"><span data-stu-id="755c0-151">The disks are hosted in the VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="755c0-152">Una vez creados y acoplados los discos, no es necesario que reiniciemos Linux, ya que el kernel verá el nuevo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="755c0-152">After disks are created and attached, there is no need to restart Linux because the kernel will see the new device.</span></span> <span data-ttu-id="755c0-153">Este dispositivo suele ser `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="755c0-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="755c0-154">Compruebe el resultado en `dmesg`.</span><span class="sxs-lookup"><span data-stu-id="755c0-154">Check `dmesg` for the output.</span></span>

<span data-ttu-id="755c0-155">En cada VM crearemos una partición mediante `cfdisk` (partición de Linux primaria) y escribiremos la nueva tabla de particiones.</span><span class="sxs-lookup"><span data-stu-id="755c0-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write the new partition table.</span></span> <span data-ttu-id="755c0-156">No cree un sistema de archivos en esta partición.</span><span class="sxs-lookup"><span data-stu-id="755c0-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-the-cluster"></a><span data-ttu-id="755c0-157">Configuración del clúster</span><span class="sxs-lookup"><span data-stu-id="755c0-157">Set up the cluster</span></span>
<span data-ttu-id="755c0-158">Use APT para instalar Corosync, Pacemaker y DRBD en ambas VM de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="755c0-158">Use APT to install Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="755c0-159">Para hacerlo con `apt-get`, ejecute el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="755c0-159">To do so with `apt-get`, run the following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="755c0-160">No instale MySQL en este momento.</span><span class="sxs-lookup"><span data-stu-id="755c0-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="755c0-161">Los scripts de instalación de Debian y Ubuntu inicializarán un directorio de datos de MySQL en `/var/lib/mysql`, pero dado que el directorio se sustituirá por un sistema de archivos DRBD, necesita instalar MySQL más tarde.</span><span class="sxs-lookup"><span data-stu-id="755c0-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because the directory will be superseded by a DRBD file system, you need to install MySQL later.</span></span>

<span data-ttu-id="755c0-162">Compruebe (con `/sbin/ifconfig`) que ambas VM usan las direcciones de la subred 10.10.10.0/24 y que pueden ejecutar el comando ping entre ellas por nombre.</span><span class="sxs-lookup"><span data-stu-id="755c0-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in the 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="755c0-163">También puede usar `ssh-keygen` y `ssh-copy-id` para asegurarse de que ambas VM pueden comunicarse a través de SSH sin necesidad de contraseña.</span><span class="sxs-lookup"><span data-stu-id="755c0-163">You can also use `ssh-keygen` and `ssh-copy-id` to make sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="755c0-164">Configure DRBD</span><span class="sxs-lookup"><span data-stu-id="755c0-164">Set up DRBD</span></span>
<span data-ttu-id="755c0-165">Cree un recurso DRBD que usa la partición `/dev/sdc1` subyacente para generar un recurso `/dev/drbd1` que puede asumir el formato ext3 y usarse tanto en nodos principales como secundarios.</span><span class="sxs-lookup"><span data-stu-id="755c0-165">Create a DRBD resource that uses the underlying `/dev/sdc1` partition to produce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="755c0-166">Abra `/etc/drbd.d/r0.res` y copie la siguiente definición de recurso en ambas VM:</span><span class="sxs-lookup"><span data-stu-id="755c0-166">Open `/etc/drbd.d/r0.res` and copy the following resource definition on both VMs:</span></span>

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. <span data-ttu-id="755c0-167">Inicialice el recurso mediante `drbdadm` en ambas VM:</span><span class="sxs-lookup"><span data-stu-id="755c0-167">Initialize the resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="755c0-168">En la VM principal (`hadb01`), fuerce la propiedad (principal) del recurso DRBD:</span><span class="sxs-lookup"><span data-stu-id="755c0-168">On the primary VM (`hadb01`), force ownership (primary) of the DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="755c0-169">Si examina el contenido de /proc/drbd (`sudo cat /proc/drbd`) en ambas máquinas virtuales, debe ver `Primary/Secondary` en `hadb01` y `Secondary/Primary` en `hadb02`, que concuerda con la solución en este punto.</span><span class="sxs-lookup"><span data-stu-id="755c0-169">If you examine the contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with the solution at this point.</span></span> <span data-ttu-id="755c0-170">El disco de 5 GB se sincronizara través de la red 10.10.10.0/24 sin coste alguno para los clientes.</span><span class="sxs-lookup"><span data-stu-id="755c0-170">The 5-GB disk is synchronized over the 10.10.10.0/24 network at no charge to customers.</span></span>

<span data-ttu-id="755c0-171">Una vez sincronizado el disco, puede crear el sistema de archivos en `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="755c0-171">After the disk is synchronized, you can create the file system on `hadb01`.</span></span> <span data-ttu-id="755c0-172">Para tareas de prueba usamos ext2, pero el siguiente código creará un sistema de archivos ext3:</span><span class="sxs-lookup"><span data-stu-id="755c0-172">For testing purposes, we used ext2, but the following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-the-drbd-resource"></a><span data-ttu-id="755c0-173">Montaje del recurso DRBD</span><span class="sxs-lookup"><span data-stu-id="755c0-173">Mount the DRBD resource</span></span>
<span data-ttu-id="755c0-174">Ahora está preparado para montar los recursos DRBD en `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="755c0-174">You're now ready to mount the DRBD resources on `hadb01`.</span></span> <span data-ttu-id="755c0-175">Debian y productos derivados usan `/var/lib/mysql` como directorio de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="755c0-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="755c0-176">Dado que no ha instalado MySQL, cree el directorio y monte el recurso DRBD.</span><span class="sxs-lookup"><span data-stu-id="755c0-176">Because you haven't installed MySQL, create the directory and mount the DRBD resource.</span></span> <span data-ttu-id="755c0-177">Para llevar a cabo esta opción, ejecute el siguiente código en `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="755c0-177">To perform this option, run the following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="755c0-178">Instalación de MySQL</span><span class="sxs-lookup"><span data-stu-id="755c0-178">Set up MySQL</span></span>
<span data-ttu-id="755c0-179">Ahora estamos preparados para instalar MySQL en `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="755c0-179">Now you're ready to install MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="755c0-180">Para `hadb02`, tiene dos opciones.</span><span class="sxs-lookup"><span data-stu-id="755c0-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="755c0-181">Puede instalar mysql-server, lo que creará /var/lib/mysql, lo rellenará con un nuevo directorio de datos y después quitará el contenido.</span><span class="sxs-lookup"><span data-stu-id="755c0-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove the contents.</span></span> <span data-ttu-id="755c0-182">Para llevar a cabo esta opción, ejecute el siguiente código en `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="755c0-182">To perform this option, run the following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="755c0-183">La segunda opción consiste en un realizar una conmutación por error para `hadb02` y después instalar mysql-server allí.</span><span class="sxs-lookup"><span data-stu-id="755c0-183">The second option is to failover to `hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="755c0-184">Los scripts de instalación tendrán en cuenta la instalación existente y no la tocarán.</span><span class="sxs-lookup"><span data-stu-id="755c0-184">Installation scripts will notice the existing installation and won't touch it.</span></span>

<span data-ttu-id="755c0-185">Ejecute el siguiente fragmento de código en `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="755c0-185">Run the following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="755c0-186">Ejecute el siguiente fragmento de código en `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="755c0-186">Run the following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="755c0-187">Si no pretende conmutar por error DRBD ahora, la primera opción es más sencilla aunque posiblemente menos elegante.</span><span class="sxs-lookup"><span data-stu-id="755c0-187">If you don't plan to failover DRBD now, the first option is easier although arguably less elegant.</span></span> <span data-ttu-id="755c0-188">Después de configurar esto, puede comenzar a trabajar en su base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="755c0-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="755c0-189">Ejecute el código siguiente en `hadb02` (o en cualquiera de los servidores activos, conforme a DRBD):</span><span class="sxs-lookup"><span data-stu-id="755c0-189">Run the following code on `hadb02` (or whichever one of the servers is active, according to DRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* TO root;

> [!WARNING]
> <span data-ttu-id="755c0-190">esta última instrucción deshabilita de forma eficaz la autenticación para el usuario raíz en esta tabla.</span><span class="sxs-lookup"><span data-stu-id="755c0-190">This last statement effectively disables authentication for the root user in this table.</span></span> <span data-ttu-id="755c0-191">Las instrucciones GRANT de producción deben reemplazar esto y solamente se incluye por motivos ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="755c0-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="755c0-192">Si desea realizar consultas desde fuera de las máquinas virtuales, que es la finalidad de esta guía, también necesita habilitar las redes para MySQL.</span><span class="sxs-lookup"><span data-stu-id="755c0-192">If you want to make queries from outside the VMs (which is the purpose of this guide), you also need to enable networking for MySQL.</span></span> <span data-ttu-id="755c0-193">Abra `/etc/mysql/my.cnf` en ambas VM y vaya a `bind-address`.</span><span class="sxs-lookup"><span data-stu-id="755c0-193">On both VMs, open `/etc/mysql/my.cnf` and go to `bind-address`.</span></span> <span data-ttu-id="755c0-194">Cambie la dirección de 127.0.0.1 a 0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="755c0-194">Change the address from 127.0.0.1 to 0.0.0.0.</span></span> <span data-ttu-id="755c0-195">Después de guardar el archivo, emita `sudo service mysql restart` en su principal actual.</span><span class="sxs-lookup"><span data-stu-id="755c0-195">After saving the file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-the-mysql-load-balanced-set"></a><span data-ttu-id="755c0-196">Creación del conjunto de carga equilibrada de MySQL</span><span class="sxs-lookup"><span data-stu-id="755c0-196">Create the MySQL load-balanced set</span></span>
<span data-ttu-id="755c0-197">Vuelva al portal, vaya a `hadb01` y elija **Puntos de conexión**.</span><span class="sxs-lookup"><span data-stu-id="755c0-197">Go back to the portal, go to `hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="755c0-198">Para crear un punto de conexión, elija MySQL (TCP 3306) en la lista desplegable y seleccione **Crear nuevo conjunto de carga equilibrada**.</span><span class="sxs-lookup"><span data-stu-id="755c0-198">To create an endpoint, choose MySQL (TCP 3306) from the drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="755c0-199">Dé un nombre al conjunto de punto de conexión de carga equilibrada `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="755c0-199">Name the load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="755c0-200">Establezca **Tiempo** en 5 segundos como mínimo.</span><span class="sxs-lookup"><span data-stu-id="755c0-200">Set **Time** to 5 seconds, minimum.</span></span>

<span data-ttu-id="755c0-201">Tras crear el punto de conexión, vaya a `hadb02`, elija **Puntos de conexión** y cree un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="755c0-201">After you create the endpoint, go to `hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="755c0-202">Elija `lb-mysql` y seleccione MySQL en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="755c0-202">Choose `lb-mysql`, and then select MySQL from the drop-down list.</span></span> <span data-ttu-id="755c0-203">También puede usar la CLI de Azure para este paso.</span><span class="sxs-lookup"><span data-stu-id="755c0-203">You can also use the Azure CLI for this step.</span></span>

<span data-ttu-id="755c0-204">Ya tiene todo lo que necesita para una operación manual del clúster.</span><span class="sxs-lookup"><span data-stu-id="755c0-204">You now have everything you need for manual operation of the cluster.</span></span>

### <a name="test-the-load-balanced-set"></a><span data-ttu-id="755c0-205">Prueba del conjunto de carga equilibrada</span><span class="sxs-lookup"><span data-stu-id="755c0-205">Test the load-balanced set</span></span>
<span data-ttu-id="755c0-206">Las pruebas se pueden realizar desde un equipo externo usando cualquier cliente MySQL, o bien mediante ciertas aplicaciones, como phpMyAdmin ejecutada como un sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="755c0-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="755c0-207">En este caso, utiliza una herramienta de línea de comandos de MySQL en otro cuadro de Linux:</span><span class="sxs-lookup"><span data-stu-id="755c0-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="755c0-208">Conmutación por error manual</span><span class="sxs-lookup"><span data-stu-id="755c0-208">Manually failing over</span></span>
<span data-ttu-id="755c0-209">Puede simular conmutaciones por error cerrando MySQL, cambiando el rol principal de DRBD e iniciando MySQL de nuevo.</span><span class="sxs-lookup"><span data-stu-id="755c0-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="755c0-210">Para llevar a cabo esta opción, ejecute el siguiente código en hadb01:</span><span class="sxs-lookup"><span data-stu-id="755c0-210">To perform this task, run the following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="755c0-211">Después en hadb02:</span><span class="sxs-lookup"><span data-stu-id="755c0-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="755c0-212">Una vez realizada la conmutación por error manualmente, puede repetir la consulta remota, que debe funcionar perfectamente.</span><span class="sxs-lookup"><span data-stu-id="755c0-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="755c0-213">Configuración de Corosync</span><span class="sxs-lookup"><span data-stu-id="755c0-213">Set up Corosync</span></span>
<span data-ttu-id="755c0-214">Corosync es la infraestructura de clúster subyacente que Pacemaker necesita para trabajar.</span><span class="sxs-lookup"><span data-stu-id="755c0-214">Corosync is the underlying cluster infrastructure required for Pacemaker to work.</span></span> <span data-ttu-id="755c0-215">Para Heartbeat (y otras metodologías como Ultramonkey), Corosync es una división de las funcionalidades CRM, mientras que la funcionalidad de Pacemaker es más similar a Hearbeat.</span><span class="sxs-lookup"><span data-stu-id="755c0-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of the CRM functionalities, while Pacemaker remains more similar to Heartbeat in functionality.</span></span>

<span data-ttu-id="755c0-216">La restricción principal para Corosync en Azure es que Corosync prefiere comunicaciones multidifusión mejor que difusión y difusión mejor que unidifusión, pero las redes de Microsoft Azure solo admiten unidifusión.</span><span class="sxs-lookup"><span data-stu-id="755c0-216">The main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="755c0-217">Por suerte, Corosync tiene un modo de unidifusión activo.</span><span class="sxs-lookup"><span data-stu-id="755c0-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="755c0-218">La única restricción real es que, dado que todos los nodos no se comunican entre sí, necesita definir dichos nodos en los archivos de configuración, incluidas sus direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="755c0-218">The only real constraint is that because all nodes are not communicating among themselves, you need to define the nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="755c0-219">Podemos utilizar los archivos de ejemplo de Corosync para Unidifusión y cambiar la dirección de enlace, las listas de nodos y los directorios de registro (Ubuntu usa `/var/log/corosync`, mientras que los archivos de ejemplo usan `/var/log/cluster`) y habilitar las herramientas de cuórum.</span><span class="sxs-lookup"><span data-stu-id="755c0-219">We can use the Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while the example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="755c0-220">Use la siguiente directiva `transport: udpu` y las direcciones IP definidas manualmente para ambos nodos.</span><span class="sxs-lookup"><span data-stu-id="755c0-220">Use the following `transport: udpu` directive and the manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="755c0-221">Ejecute el siguiente fragmento de código en `/etc/corosync/corosync.conf` en ambos nodos:</span><span class="sxs-lookup"><span data-stu-id="755c0-221">Run the following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

<span data-ttu-id="755c0-222">Copie este archivo de configuración en ambas VM e inicie Corosync en los dos nodos:</span><span class="sxs-lookup"><span data-stu-id="755c0-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="755c0-223">Poco después de iniciar el servicio, el clúster se debe establecer en el anillo actual y se debe constituir el cuórum.</span><span class="sxs-lookup"><span data-stu-id="755c0-223">Shortly after starting the service, the cluster should be established in the current ring, and quorum should be constituted.</span></span> <span data-ttu-id="755c0-224">Podemos comprobar esta funcionalidad revisando registros o ejecutando el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="755c0-224">We can check this functionality by reviewing logs or by running the following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="755c0-225">Verá un resultado similar al de la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="755c0-225">You will see output similar to the following image:</span></span>

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="755c0-227">Configuración de Pacemaker</span><span class="sxs-lookup"><span data-stu-id="755c0-227">Set up Pacemaker</span></span>
<span data-ttu-id="755c0-228">Pacemaker usa el clúster para supervisar recursos, definir el momento en el que los principales dejan de funcionar y cambiar estos recursos a los secundarios.</span><span class="sxs-lookup"><span data-stu-id="755c0-228">Pacemaker uses the cluster to monitor for resources, define when primaries go down, and switch those resources to secondaries.</span></span> <span data-ttu-id="755c0-229">Entre las diferentes posibilidades que existen, los recursos se pueden definir desde un conjunto de scripts disponibles o desde scripts LSB (de tipo init).</span><span class="sxs-lookup"><span data-stu-id="755c0-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="755c0-230">Queremos que Pacemaker "posea" el recurso DRBD, el punto de montaje y el servicio MySQL.</span><span class="sxs-lookup"><span data-stu-id="755c0-230">We want Pacemaker to "own" the DRBD resource, the mount point, and the MySQL service.</span></span> <span data-ttu-id="755c0-231">Si Pacemaker puede activar y desactivar DRBD, montarlo y desmontarlo y después iniciar y detener MySQL en el orden correcto cuando algo vaya mal con la máquina principal, la configuración se habrá completado.</span><span class="sxs-lookup"><span data-stu-id="755c0-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in the right order when something bad happens with the primary, setup is complete.</span></span>

<span data-ttu-id="755c0-232">Cuando instalé por primera vez Pacemaker, la configuración debe ser suficientemente sencilla, algo como lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="755c0-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="755c0-233">Compruebe la configuración ejecutando `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="755c0-233">Check the configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="755c0-234">Después cree un archivo (por ejemplo, `/tmp/cluster.conf`) con los siguiente recursos:</span><span class="sxs-lookup"><span data-stu-id="755c0-234">Then create a file (like `/tmp/cluster.conf`) with the following resources:</span></span>

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. <span data-ttu-id="755c0-235">Cargue el archivo en la configuración.</span><span class="sxs-lookup"><span data-stu-id="755c0-235">Load the file into the configuration.</span></span> <span data-ttu-id="755c0-236">Solo tiene que hacer esto en un nodo.</span><span class="sxs-lookup"><span data-stu-id="755c0-236">You only need to do this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="755c0-237">Asegúrese de que Pacemaker se inicia durante el arranque en ambos nodos:</span><span class="sxs-lookup"><span data-stu-id="755c0-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="755c0-238">Use `sudo crm_mon –L` para comprobar que uno de los nodos se ha convertido en el maestro para el clúster y se ejecuta en todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="755c0-238">By using `sudo crm_mon –L`, verify that one of your nodes has become the master for the cluster and is running all the resources.</span></span> <span data-ttu-id="755c0-239">Puede usar mount y ps para comprobar que los recursos se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="755c0-239">You can use mount and ps to check that the resources are running.</span></span>

<span data-ttu-id="755c0-240">La siguiente captura de pantalla muestra `crm_mon` con un nodo detenido (salga seleccionando Ctrl+C):</span><span class="sxs-lookup"><span data-stu-id="755c0-240">The following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](./media/mysql-cluster/image002.png)

<span data-ttu-id="755c0-242">Esta captura de pantalla muestra ambos nodos, uno maestro y otro subordinado:</span><span class="sxs-lookup"><span data-stu-id="755c0-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="755c0-244">Prueba</span><span class="sxs-lookup"><span data-stu-id="755c0-244">Testing</span></span>
<span data-ttu-id="755c0-245">Ya puede llevar a cabo una simulación de conmutación por error automática.</span><span class="sxs-lookup"><span data-stu-id="755c0-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="755c0-246">Existen dos formas de hacerlo: suave y dura.</span><span class="sxs-lookup"><span data-stu-id="755c0-246">There are two ways to do this: soft and hard.</span></span>

<span data-ttu-id="755c0-247">Para llevar a cabo la simulación suave, usaremos la función de cierre del clúster: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="755c0-247">The soft way uses the cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="755c0-248">Si usa esto en el maestro, el subordinado asume el control.</span><span class="sxs-lookup"><span data-stu-id="755c0-248">If you use this on the master, the slave takes over.</span></span> <span data-ttu-id="755c0-249">No olvide volver a establecer esto en desconectado.</span><span class="sxs-lookup"><span data-stu-id="755c0-249">Remember to set this back to off.</span></span> <span data-ttu-id="755c0-250">Si no lo hace, crm_mon mostrará un nodo en espera.</span><span class="sxs-lookup"><span data-stu-id="755c0-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="755c0-251">La forma dura consiste en cerrar la VM principal (hadb01) mediante el portal o cambiando el nivel de ejecución en la VM (es decir, detener, apagar).</span><span class="sxs-lookup"><span data-stu-id="755c0-251">The hard way is shutting down the primary VM (hadb01) via the portal or by changing the runlevel on the VM (that is, halt, shutdown).</span></span> <span data-ttu-id="755c0-252">Esto ayuda a Corosync y Pacemaker indicando que el maestro deja de funcionar.</span><span class="sxs-lookup"><span data-stu-id="755c0-252">This helps Corosync and Pacemaker by signaling that the master's going down.</span></span> <span data-ttu-id="755c0-253">Puede probar esto (útil para ventanas de mantenimiento), pero también puede forzar el escenario congelando la VM.</span><span class="sxs-lookup"><span data-stu-id="755c0-253">You can test this (useful for maintenance windows), but you can also force the scenario by freezing the VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="755c0-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="755c0-254">STONITH</span></span>
<span data-ttu-id="755c0-255">Debe ser posible emitir un cierre de máquina virtual a través de la CLI de Azure en lugar de un script STONITH que controle un dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="755c0-255">It should be possible to issue a VM shutdown via the Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="755c0-256">Puede usar `/usr/lib/stonith/plugins/external/ssh` como base y habilitar STONITH en la configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="755c0-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in the cluster's configuration.</span></span> <span data-ttu-id="755c0-257">La CLI de Azure se debe instalar globalmente y la configuración y el perfil de publicación se deben cargar para el usuario del clúster.</span><span class="sxs-lookup"><span data-stu-id="755c0-257">Azure CLI should be globally installed, and the publish settings and profile should be loaded for the cluster's user.</span></span>

<span data-ttu-id="755c0-258">Ejemplo de código para el recurso disponible en [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="755c0-258">Sample code for the resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="755c0-259">Cambie la configuración del clúster agregando lo siguiente a `sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="755c0-259">Change the cluster's configuration by adding the following to `sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="755c0-260">El script no realiza comprobaciones ascendentes o descendentes.</span><span class="sxs-lookup"><span data-stu-id="755c0-260">The script doesn't perform up/down checks.</span></span> <span data-ttu-id="755c0-261">El recurso SSH original tenía 15 comprobaciones ping, pero el tiempo de recuperación para una VM de Azure podría ser más variable.</span><span class="sxs-lookup"><span data-stu-id="755c0-261">The original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="755c0-262">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="755c0-262">Limitations</span></span>
<span data-ttu-id="755c0-263">Se aplican las siguientes limitaciones:</span><span class="sxs-lookup"><span data-stu-id="755c0-263">The following limitations apply:</span></span>

* <span data-ttu-id="755c0-264">El script de recursos DRBD linbit que administra DRBD como un recurso en Pacemaker usa `drbdadm down` al cerrar un nodo, aunque dicho nodo esté entrando en modo de espera.</span><span class="sxs-lookup"><span data-stu-id="755c0-264">The linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if the node is just going on standby.</span></span> <span data-ttu-id="755c0-265">No se trata de la situación ideal porque el subordinado no sincronizará el recurso DRBD mientras se escribe en el maestro.</span><span class="sxs-lookup"><span data-stu-id="755c0-265">This is not ideal because the slave will not be synchronizing the DRBD resource while the master gets writes.</span></span> <span data-ttu-id="755c0-266">Si no se produce un error en el maestro, el subordinado podrá asumir el control y el estado del sistema de archivos anterior.</span><span class="sxs-lookup"><span data-stu-id="755c0-266">If the master does not fail graciously, the slave can take over an older file system state.</span></span> <span data-ttu-id="755c0-267">Hay dos formas posibles de resolver este problema:</span><span class="sxs-lookup"><span data-stu-id="755c0-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="755c0-268">Aplicando un comando `drbdadm up r0` en todos los nodos del clúster mediante un guardián local (sin clústeres)</span><span class="sxs-lookup"><span data-stu-id="755c0-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="755c0-269">Editando el script DRBD linbit, asegurándose de que no se llama a `down`, en `/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="755c0-269">Editing the linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="755c0-270">El equilibrador de carga necesita al menos cinco segundos para responder, por lo que las aplicaciones deben ser compatibles con clústeres y ser más tolerantes a errores de tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="755c0-270">The load balancer needs at least five seconds to respond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="755c0-271">También pueden ayudar otras arquitecturas, como las colas de la aplicación y middlewares de consulta.</span><span class="sxs-lookup"><span data-stu-id="755c0-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="755c0-272">El ajuste de MySQL es necesario para garantizar que la escritura se realiza a un ritmo apropiado y las memorias caché se vacían en disco con la máxima frecuencia posible para minimizar la pérdida de memoria.</span><span class="sxs-lookup"><span data-stu-id="755c0-272">MySQL tuning is necessary to ensure that writing is done at a manageable pace and caches are flushed to disk as frequently as possible to minimize memory loss.</span></span>
* <span data-ttu-id="755c0-273">El rendimiento de escritura depende de la interconexión de las VM en la conmutación virtual ya que este es el mecanismo que usa DRBD para replicar el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="755c0-273">Write performance is dependent in VM interconnect in the virtual switch because this is the mechanism used by DRBD to replicate the device.</span></span>
