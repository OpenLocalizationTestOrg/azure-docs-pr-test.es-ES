---
title: aaaClusterize MySQL con conjuntos de carga equilibrada | Documentos de Microsoft
description: "Configurar un equilibrio de carga, la alta disponibilidad Linux MySQL clúster creado con el modelo de implementación clásica de hello en Azure"
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
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a><span data-ttu-id="ad7cd-103">Usar conjuntos de carga equilibrada tooclusterize MySQL en Linux</span><span class="sxs-lookup"><span data-stu-id="ad7cd-103">Use load-balanced sets tooclusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ad7cd-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="ad7cd-105">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="ad7cd-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ad7cd-107">A [plantilla del Administrador de recursos](https://azure.microsoft.com/documentation/templates/mysql-replication/) está disponible si necesita toodeploy un clúster de MySQL.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need toodeploy a MySQL cluster.</span></span>

<span data-ttu-id="ad7cd-108">Este artículo explora y Hola distintos enfoques disponibles toodeploy basados en Linux servicios de alta disponibilidad en Microsoft Azure, exploración de alta disponibilidad del servidor de MySQL como instrucciones detalladas muestra.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-108">This article explores and illustrates hello different approaches available toodeploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="ad7cd-109">En [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)hay un vídeo disponible que ilustra este enfoque.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="ad7cd-110">Describiremos una solución de alta disponibilidad de MySQL de un solo maestro y dos nodos independientes basada en DRBD, Corosync y Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="ad7cd-111">Solamente se ejecuta un nodo MySQL en cada momento.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="ad7cd-112">Lectura y escritura de hello recursos DRBD son también un nodo de tooonly limitado a la vez.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-112">Reading and writing from hello DRBD resource is also limited tooonly one node at a time.</span></span>

<span data-ttu-id="ad7cd-113">No es necesario para una solución VIP como informes LV, dado que va a utilizar conjuntos de carga equilibrada en tooprovide round robin funcionalidad y punto de conexión de detección de Microsoft Azure, eliminación y recuperación correcta de hello VIP.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure tooprovide round-robin functionality and endpoint detection, removal, and graceful recovery of hello VIP.</span></span> <span data-ttu-id="ad7cd-114">Hola VIP es una dirección IPv4 globalmente enrutable asignada por Microsoft Azure al servicio en la nube Hola crearlo.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-114">hello VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create hello cloud service.</span></span>

<span data-ttu-id="ad7cd-115">Hay otras posibles arquitecturas para MySQL, como, por ejemplo, NBD Cluster, Percona, Galera y diversas soluciones middleware que incluyen, al menos, una disponible como máquina virtual en [VM Depot](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="ad7cd-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="ad7cd-116">Siempre que estas soluciones se pueden replicar en unidifusión y multidifusión o difusión y no dependen del almacenamiento compartido o varias interfaces de red, escenarios de hello deben ser fácil toodeploy en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, hello scenarios should be easy toodeploy on Microsoft Azure.</span></span>

<span data-ttu-id="ad7cd-117">Estas arquitecturas de agrupación en clústeres pueden ampliarse tooother productos como PostgreSQL y OpenLDAP de un modo similar.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-117">These clustering architectures can be extended tooother products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="ad7cd-118">Por ejemplo, este procedimiento de equilibro de carga independiente se probó correctamente con OpenLDAP multimaestro y puede verlo en nuestro blog de Channel 9.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="ad7cd-119">Prepárese</span><span class="sxs-lookup"><span data-stu-id="ad7cd-119">Get ready</span></span>
<span data-ttu-id="ad7cd-120">Necesita Hola siguiente recursos y la capacidad de:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-120">You need hello following resources and abilities:</span></span>

  - <span data-ttu-id="ad7cd-121">Una Microsoft Azure cuenta con una suscripción válida, toocreate capaz de al menos dos máquinas virtuales (extra se usó en este ejemplo)</span><span class="sxs-lookup"><span data-stu-id="ad7cd-121">A Microsoft Azure account with a valid subscription, able toocreate at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="ad7cd-122">Una red y una subred</span><span class="sxs-lookup"><span data-stu-id="ad7cd-122">A network and a subnet</span></span>
  - <span data-ttu-id="ad7cd-123">Un grupo de afinidad</span><span class="sxs-lookup"><span data-stu-id="ad7cd-123">An affinity group</span></span>
  - <span data-ttu-id="ad7cd-124">Un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="ad7cd-124">An availability set</span></span>
  - <span data-ttu-id="ad7cd-125">Hola capacidad toocreate discos duros virtuales en Hola misma región que el servicio de nube de Hola y conéctelas toohello máquinas virtuales de Linux</span><span class="sxs-lookup"><span data-stu-id="ad7cd-125">hello ability toocreate VHDs in hello same region as hello cloud service and attach them toohello Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="ad7cd-126">Entorno probado</span><span class="sxs-lookup"><span data-stu-id="ad7cd-126">Tested environment</span></span>
* <span data-ttu-id="ad7cd-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="ad7cd-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="ad7cd-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="ad7cd-128">DRBD</span></span>
  * <span data-ttu-id="ad7cd-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ad7cd-129">MySQL Server</span></span>
  * <span data-ttu-id="ad7cd-130">Corosync y Pacemaker</span><span class="sxs-lookup"><span data-stu-id="ad7cd-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="ad7cd-131">Grupo de afinidad</span><span class="sxs-lookup"><span data-stu-id="ad7cd-131">Affinity group</span></span>
<span data-ttu-id="ad7cd-132">Crear un grupo de afinidad para la solución de hello debe iniciar sesión en el portal de Azure clásico toohello seleccionar **configuración**y la creación de un grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-132">Create an affinity group for hello solution by signing in toohello Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="ad7cd-133">Recursos asignados que se crean con posterioridad se asignarán toothis grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-133">Allocated resources created later will be assigned toothis affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="ad7cd-134">Redes</span><span class="sxs-lookup"><span data-stu-id="ad7cd-134">Networks</span></span>
<span data-ttu-id="ad7cd-135">Se crea una nueva red y se crea una subred dentro de la red de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-135">A new network is created, and a subnet is created inside hello network.</span></span> <span data-ttu-id="ad7cd-136">En este ejemplo se usa una red 10.10.10.0/24 con una sola subred /24 dentro.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="ad7cd-137">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ad7cd-137">Virtual machines</span></span>
<span data-ttu-id="ad7cd-138">Hola primera Ubuntu 13.10 VM se crea mediante una imagen de la Galería de Ubuntu Endorsed y se denomina `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-138">hello first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="ad7cd-139">Se crea un nuevo servicio de nube en proceso de hello, denominado hadb.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-139">A new cloud service is created in hello process, called hadb.</span></span> <span data-ttu-id="ad7cd-140">Este nombre muestra hello compartido, naturaleza con equilibrio de carga que el servicio de hello tendrán cuando se agregan más recursos.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-140">This name illustrates hello shared, load-balanced nature that hello service will have when more resources are added.</span></span> <span data-ttu-id="ad7cd-141">Hola creación de `hadb01` está sin incidentes y se rellena mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-141">hello creation of `hadb01` is uneventful and completed by using hello portal.</span></span> <span data-ttu-id="ad7cd-142">Se crea automáticamente un punto de conexión de SSH, y se selecciona la nueva red de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-142">An endpoint for SSH is automatically created, and hello new network is selected.</span></span> <span data-ttu-id="ad7cd-143">Ahora puede crear un conjunto de disponibilidad para hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-143">Now you can create an availability set for hello VMs.</span></span>

<span data-ttu-id="ad7cd-144">Después de hello primera máquina virtual se crea (técnicamente, cuando se crea el servicio de nube de hello), crear Hola segunda máquina virtual, `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-144">After hello first VM is created (technically, when hello cloud service is created), create hello second VM, `hadb02`.</span></span> <span data-ttu-id="ad7cd-145">Para hello segunda máquina virtual, utilizar Ubuntu 13.10 VM de hello galería mediante el portal de hello, pero usar un servicio de nube existente, `hadb.cloudapp.net`, en lugar de crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-145">For hello second VM, use Ubuntu 13.10 VM from hello Gallery by using hello portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="ad7cd-146">conjunto de red y la disponibilidad de Hello debe seleccionarse automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-146">hello network and availability set should be automatically selected.</span></span> <span data-ttu-id="ad7cd-147">También se creará un extremo SSH.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="ad7cd-148">Después de que se han creado dos máquinas virtuales, tome nota del puerto SSH de Hola para `hadb01` (puerto TCP 22) y `hadb02` (asignado automáticamente por Azure).</span><span class="sxs-lookup"><span data-stu-id="ad7cd-148">After both VMs have been created, take note of hello SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="ad7cd-149">Almacenamiento acoplado</span><span class="sxs-lookup"><span data-stu-id="ad7cd-149">Attached storage</span></span>
<span data-ttu-id="ad7cd-150">Adjuntar un tooboth de disco nuevas máquinas virtuales y crear discos de 5 GB en proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-150">Attach a new disk tooboth VMs and create 5-GB disks in hello process.</span></span> <span data-ttu-id="ad7cd-151">discos de Hola se hospedan en el contenedor VHD de hello en uso para los discos de sistema operativo principal.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-151">hello disks are hosted in hello VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="ad7cd-152">Después de que se crean y se adjuntan discos, no hay ningún toorestart necesidad Linux porque kernel Hola ver Hola nuevo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-152">After disks are created and attached, there is no need toorestart Linux because hello kernel will see hello new device.</span></span> <span data-ttu-id="ad7cd-153">Este dispositivo suele ser `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="ad7cd-154">Comprobar `dmesg` para la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-154">Check `dmesg` for hello output.</span></span>

<span data-ttu-id="ad7cd-155">En cada máquina virtual, cree una partición utilizando `cfdisk` (partición primaria, de Linux) y escribir Hola nueva tabla de partición.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write hello new partition table.</span></span> <span data-ttu-id="ad7cd-156">No cree un sistema de archivos en esta partición.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-hello-cluster"></a><span data-ttu-id="ad7cd-157">Configurar el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="ad7cd-157">Set up hello cluster</span></span>
<span data-ttu-id="ad7cd-158">Utilice APT tooinstall Corosync, marcapasos y DRBD en ambas máquinas virtuales Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-158">Use APT tooinstall Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="ad7cd-159">toodo con `apt-get`, ejecute hello código siguiente:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-159">toodo so with `apt-get`, run hello following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="ad7cd-160">No instale MySQL en este momento.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="ad7cd-161">Debian y Ubuntu scripts de instalación se inicializarán en un directorio de datos de MySQL en `/var/lib/mysql`, pero porque el directorio de hello será reemplazado por un sistema de archivos DRBD, necesita tooinstall MySQL más adelante.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because hello directory will be superseded by a DRBD file system, you need tooinstall MySQL later.</span></span>

<span data-ttu-id="ad7cd-162">Comprobar (mediante el uso de `/sbin/ifconfig`) que ambas máquinas virtuales usan direcciones de subred 10.10.10.0/24 de Hola y que puede hacer ping entre sí por su nombre.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in hello 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="ad7cd-163">También puede usar `ssh-keygen` y `ssh-copy-id` toomake seguro ambas máquinas virtuales pueden comunicarse a través de SSH sin necesidad de una contraseña.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-163">You can also use `ssh-keygen` and `ssh-copy-id` toomake sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="ad7cd-164">Configure DRBD</span><span class="sxs-lookup"><span data-stu-id="ad7cd-164">Set up DRBD</span></span>
<span data-ttu-id="ad7cd-165">Crear un recurso DRBD que usa subyacente hello `/dev/sdc1` partición tooproduce un `/dev/drbd1` recursos que se ha dado formato mediante ext3 y usar en los nodos principales y secundarios.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-165">Create a DRBD resource that uses hello underlying `/dev/sdc1` partition tooproduce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="ad7cd-166">Abra `/etc/drbd.d/r0.res` y Hola copia siguiendo la definición de recursos en ambas máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-166">Open `/etc/drbd.d/r0.res` and copy hello following resource definition on both VMs:</span></span>

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

2. <span data-ttu-id="ad7cd-167">Inicializar recursos hello mediante `drbdadm` en ambas máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-167">Initialize hello resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="ad7cd-168">En Hola VM principal (`hadb01`), forzar (principal) de la propiedad de recurso DRBD de hello:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-168">On hello primary VM (`hadb01`), force ownership (primary) of hello DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="ad7cd-169">Si examina el contenido de Hola de/proc/drbd (`sudo cat /proc/drbd`) en ambas máquinas virtuales, debería ver `Primary/Secondary` en `hadb01` y `Secondary/Primary` en `hadb02`, coherentes con la solución de hello en este momento.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-169">If you examine hello contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with hello solution at this point.</span></span> <span data-ttu-id="ad7cd-170">disco de 5 GB de Hola se sincroniza en la red de 10.10.10.0/24 de hello en ningún toocustomers de forma gratuita.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-170">hello 5-GB disk is synchronized over hello 10.10.10.0/24 network at no charge toocustomers.</span></span>

<span data-ttu-id="ad7cd-171">Después de haber sincronizado disco hello, puede crear sistema de archivos de hello en `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-171">After hello disk is synchronized, you can create hello file system on `hadb01`.</span></span> <span data-ttu-id="ad7cd-172">Para realizar pruebas, hemos usado ext2, pero Hola sigue código creará un sistema de archivos ext3:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-172">For testing purposes, we used ext2, but hello following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a><span data-ttu-id="ad7cd-173">Montar hello DRBD recurso</span><span class="sxs-lookup"><span data-stu-id="ad7cd-173">Mount hello DRBD resource</span></span>
<span data-ttu-id="ad7cd-174">Está ahora listo toomount hello DRBD recursos `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-174">You're now ready toomount hello DRBD resources on `hadb01`.</span></span> <span data-ttu-id="ad7cd-175">Debian y productos derivados usan `/var/lib/mysql` como directorio de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="ad7cd-176">Dado que no tiene instalado MySQL, cree el directorio de Hola y montar hello DRBD recurso.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-176">Because you haven't installed MySQL, create hello directory and mount hello DRBD resource.</span></span> <span data-ttu-id="ad7cd-177">tooperform esta opción, ejecute hello siguiente código de `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-177">tooperform this option, run hello following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="ad7cd-178">Instalación de MySQL</span><span class="sxs-lookup"><span data-stu-id="ad7cd-178">Set up MySQL</span></span>
<span data-ttu-id="ad7cd-179">Ahora está listo tooinstall MySQL en `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-179">Now you're ready tooinstall MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="ad7cd-180">Para `hadb02`, tiene dos opciones.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="ad7cd-181">Puede instalar a mysql server, que se crean /var/lib/mysql, rellenar con un nuevo directorio de datos y, a continuación, quite el contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove hello contents.</span></span> <span data-ttu-id="ad7cd-182">tooperform esta opción, ejecute hello siguiente código de `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-182">tooperform this option, run hello following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="ad7cd-183">segunda opción de Hello es toofailover demasiado`hadb02` y, a continuación, instalar servidor mysql no existe.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-183">hello second option is toofailover too`hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="ad7cd-184">Las secuencias de comandos de instalación dará cuenta de instalación existente de hello y no toque.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-184">Installation scripts will notice hello existing installation and won't touch it.</span></span>

<span data-ttu-id="ad7cd-185">Ejecución hello código en siguiente `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-185">Run hello following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="ad7cd-186">Ejecución hello código en siguiente `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-186">Run hello following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="ad7cd-187">Si no tiene pensado toofailover DRBD ahora, Hola primera opción es más fácil aunque sin duda es menos elegante.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-187">If you don't plan toofailover DRBD now, hello first option is easier although arguably less elegant.</span></span> <span data-ttu-id="ad7cd-188">Después de configurar esto, puede comenzar a trabajar en su base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="ad7cd-189">Ejecución hello código en siguiente `hadb02` (o cualquiera de los servidores de hello está activo, según tooDRBD):</span><span class="sxs-lookup"><span data-stu-id="ad7cd-189">Run hello following code on `hadb02` (or whichever one of hello servers is active, according tooDRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> <span data-ttu-id="ad7cd-190">Esta última instrucción eficazmente deshabilita la autenticación de usuario de la raíz de hello en esta tabla.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-190">This last statement effectively disables authentication for hello root user in this table.</span></span> <span data-ttu-id="ad7cd-191">Las instrucciones GRANT de producción deben reemplazar esto y solamente se incluye por motivos ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="ad7cd-192">Si desea que las consultas de toomake desde máquinas virtuales de hello exterior (que es el propósito de Hola de esta guía), también necesita tooenable redes para MySQL.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-192">If you want toomake queries from outside hello VMs (which is hello purpose of this guide), you also need tooenable networking for MySQL.</span></span> <span data-ttu-id="ad7cd-193">En ambas máquinas virtuales, abra `/etc/mysql/my.cnf` y vaya demasiado`bind-address`.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-193">On both VMs, open `/etc/mysql/my.cnf` and go too`bind-address`.</span></span> <span data-ttu-id="ad7cd-194">Cambiar dirección de hello en 127.0.0.1 too0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-194">Change hello address from 127.0.0.1 too0.0.0.0.</span></span> <span data-ttu-id="ad7cd-195">Después de guardar el archivo hello, emitir una `sudo service mysql restart` en su objeto principal actual.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-195">After saving hello file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-hello-mysql-load-balanced-set"></a><span data-ttu-id="ad7cd-196">Crear conjunto de equilibrio de carga de MySQL de Hola</span><span class="sxs-lookup"><span data-stu-id="ad7cd-196">Create hello MySQL load-balanced set</span></span>
<span data-ttu-id="ad7cd-197">Volver atrás toohello portal, vaya demasiado`hadb01`y elija **extremos**.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-197">Go back toohello portal, go too`hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="ad7cd-198">toocreate un extremo, elija MySQL (TCP 3306) de la lista desplegable de Hola y seleccione **conjunto con equilibrio de carga nueva creación**.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-198">toocreate an endpoint, choose MySQL (TCP 3306) from hello drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="ad7cd-199">Extremo de carga equilibrada de nombre hello `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-199">Name hello load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="ad7cd-200">Establecer **tiempo** too5 segundos, mínimos.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-200">Set **Time** too5 seconds, minimum.</span></span>

<span data-ttu-id="ad7cd-201">Después de crear el punto de conexión de hello, vaya demasiado`hadb02`, elija **extremos**y crear un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-201">After you create hello endpoint, go too`hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="ad7cd-202">Elija `lb-mysql`y, a continuación, seleccione MySQL desde la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-202">Choose `lb-mysql`, and then select MySQL from hello drop-down list.</span></span> <span data-ttu-id="ad7cd-203">También puede utilizar Hola CLI de Azure para este paso.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-203">You can also use hello Azure CLI for this step.</span></span>

<span data-ttu-id="ad7cd-204">Ahora tienes todo lo que necesita para una operación manual del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-204">You now have everything you need for manual operation of hello cluster.</span></span>

### <a name="test-hello-load-balanced-set"></a><span data-ttu-id="ad7cd-205">Probar el conjunto de equilibrio de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="ad7cd-205">Test hello load-balanced set</span></span>
<span data-ttu-id="ad7cd-206">Las pruebas se pueden realizar desde un equipo externo usando cualquier cliente MySQL, o bien mediante ciertas aplicaciones, como phpMyAdmin ejecutada como un sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="ad7cd-207">En este caso, utiliza una herramienta de línea de comandos de MySQL en otro cuadro de Linux:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="ad7cd-208">Conmutación por error manual</span><span class="sxs-lookup"><span data-stu-id="ad7cd-208">Manually failing over</span></span>
<span data-ttu-id="ad7cd-209">Puede simular conmutaciones por error cerrando MySQL, cambiando el rol principal de DRBD e iniciando MySQL de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="ad7cd-210">tooperform esta tarea, ejecute hello siguiente código de hadb01:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-210">tooperform this task, run hello following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="ad7cd-211">Después en hadb02:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="ad7cd-212">Una vez realizada la conmutación por error manualmente, puede repetir la consulta remota, que debe funcionar perfectamente.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="ad7cd-213">Configuración de Corosync</span><span class="sxs-lookup"><span data-stu-id="ad7cd-213">Set up Corosync</span></span>
<span data-ttu-id="ad7cd-214">Corosync es Hola subyacente clúster infraestructura necesaria para marcapasos toowork.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-214">Corosync is hello underlying cluster infrastructure required for Pacemaker toowork.</span></span> <span data-ttu-id="ad7cd-215">Para el latido (y otros métodos como Ultramonkey), Corosync es una división de las funcionalidades CRM de hello, mientras marcapasos permanecen tooHeartbeat más similar en la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of hello CRM functionalities, while Pacemaker remains more similar tooHeartbeat in functionality.</span></span>

<span data-ttu-id="ad7cd-216">restricción principal Hola para Corosync en Azure es que Corosync prefiere multidifusión a través de difusión a las comunicaciones de unidifusión, pero las redes de Microsoft Azure solo admite unidifusión.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-216">hello main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="ad7cd-217">Por suerte, Corosync tiene un modo de unidifusión activo.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="ad7cd-218">Hola única restricción real es que, dado que todos los nodos no se comunican entre sí, es necesario nodos de hello toodefine en los archivos de configuración, incluidas las direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-218">hello only real constraint is that because all nodes are not communicating among themselves, you need toodefine hello nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="ad7cd-219">Podemos usar archivos de ejemplo de Hola Corosync de unidifusión y cambio enlazan la dirección, listas de nodos y directorios de registro (Ubuntu usa `/var/log/corosync` al uso de archivos de ejemplo de Hola a `/var/log/cluster`) y permitir a las herramientas de quórum.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-219">We can use hello Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while hello example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="ad7cd-220">Utilice siguiente hello `transport: udpu` hello y directiva definir manualmente las direcciones IP para ambos nodos.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-220">Use hello following `transport: udpu` directive and hello manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="ad7cd-221">Ejecución hello código en siguiente `/etc/corosync/corosync.conf` para ambos nodos:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-221">Run hello following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

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

<span data-ttu-id="ad7cd-222">Copie este archivo de configuración en ambas VM e inicie Corosync en los dos nodos:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="ad7cd-223">Justo después de iniciar el servicio de hello, clúster Hola se debe establecer en anillo actual de Hola y debe estar constituido quórum.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-223">Shortly after starting hello service, hello cluster should be established in hello current ring, and quorum should be constituted.</span></span> <span data-ttu-id="ad7cd-224">Podemos comprobar esta funcionalidad si examina los registros o ejecutando el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-224">We can check this functionality by reviewing logs or by running hello following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="ad7cd-225">Verá toohello similar de salida después de imagen:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-225">You will see output similar toohello following image:</span></span>

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="ad7cd-227">Configuración de Pacemaker</span><span class="sxs-lookup"><span data-stu-id="ad7cd-227">Set up Pacemaker</span></span>
<span data-ttu-id="ad7cd-228">Usa marcapasos Hola toomonitor de clúster para los recursos, define cuando los elementos dejan de funcionar y cambia esos toosecondaries de recursos.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-228">Pacemaker uses hello cluster toomonitor for resources, define when primaries go down, and switch those resources toosecondaries.</span></span> <span data-ttu-id="ad7cd-229">Entre las diferentes posibilidades que existen, los recursos se pueden definir desde un conjunto de scripts disponibles o desde scripts LSB (de tipo init).</span><span class="sxs-lookup"><span data-stu-id="ad7cd-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="ad7cd-230">Queremos marcapasos demasiado "propio" hello DRBD recurso, punto de montaje de hello y servicio de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-230">We want Pacemaker too"own" hello DRBD resource, hello mount point, and hello MySQL service.</span></span> <span data-ttu-id="ad7cd-231">Si marcapasos pueden activar y desactivar DRBD, montar y desmontar y, a continuación, iniciar y detener MySQL Hola derecha orden cuando algo mal ocurre con hello principal, el programa de instalación está completa.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in hello right order when something bad happens with hello primary, setup is complete.</span></span>

<span data-ttu-id="ad7cd-232">Cuando instalé por primera vez Pacemaker, la configuración debe ser suficientemente sencilla, algo como lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="ad7cd-233">Compruebe la configuración de hello ejecutando `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-233">Check hello configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="ad7cd-234">A continuación, cree un archivo (como `/tmp/cluster.conf`) con hello recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-234">Then create a file (like `/tmp/cluster.conf`) with hello following resources:</span></span>

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

3. <span data-ttu-id="ad7cd-235">Cargar archivo hello en configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-235">Load hello file into hello configuration.</span></span> <span data-ttu-id="ad7cd-236">Solo necesita toodo esto en un nodo.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-236">You only need toodo this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="ad7cd-237">Asegúrese de que Pacemaker se inicia durante el arranque en ambos nodos:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="ad7cd-238">Mediante el uso de `sudo crm_mon –L`, compruebe que uno de los nodos se ha convertido en maestro de hello para el clúster de Hola y todos los recursos de Hola está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-238">By using `sudo crm_mon –L`, verify that one of your nodes has become hello master for hello cluster and is running all hello resources.</span></span> <span data-ttu-id="ad7cd-239">Puede usar toocheck de montaje y ps que ejecutan recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-239">You can use mount and ps toocheck that hello resources are running.</span></span>

<span data-ttu-id="ad7cd-240">Hola siguiente captura de pantalla muestra `crm_mon` con un nodo detenido (salida seleccionando Ctrl + C):</span><span class="sxs-lookup"><span data-stu-id="ad7cd-240">hello following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](./media/mysql-cluster/image002.png)

<span data-ttu-id="ad7cd-242">Esta captura de pantalla muestra ambos nodos, uno maestro y otro subordinado:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="ad7cd-244">Prueba</span><span class="sxs-lookup"><span data-stu-id="ad7cd-244">Testing</span></span>
<span data-ttu-id="ad7cd-245">Ya puede llevar a cabo una simulación de conmutación por error automática.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="ad7cd-246">Hay dos toodo formas esto: flexibles y forzados.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-246">There are two ways toodo this: soft and hard.</span></span>

<span data-ttu-id="ad7cd-247">Hello forma parcial con la función de cierre del clúster de hello: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-247">hello soft way uses hello cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="ad7cd-248">Si usa esto en el patrón de hello, esclavo hello tiene sobre.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-248">If you use this on hello master, hello slave takes over.</span></span> <span data-ttu-id="ad7cd-249">Recuerde tooset esta toooff atrás.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-249">Remember tooset this back toooff.</span></span> <span data-ttu-id="ad7cd-250">Si no lo hace, crm_mon mostrará un nodo en espera.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="ad7cd-251">Hello malas se va a cerrar hacia abajo Hola VM principal (hadb01) mediante el portal de Hola o cambiando Hola runlevel en hello VM (es decir, detener, cierre).</span><span class="sxs-lookup"><span data-stu-id="ad7cd-251">hello hard way is shutting down hello primary VM (hadb01) via hello portal or by changing hello runlevel on hello VM (that is, halt, shutdown).</span></span> <span data-ttu-id="ad7cd-252">Esto ayuda a Corosync y marcapasos mediante señales ir del patrón Hola hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-252">This helps Corosync and Pacemaker by signaling that hello master's going down.</span></span> <span data-ttu-id="ad7cd-253">Puede probarlo (es útil para las ventanas de mantenimiento), pero también puede forzar el escenario de hello inmovilizando Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-253">You can test this (useful for maintenance windows), but you can also force hello scenario by freezing hello VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="ad7cd-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="ad7cd-254">STONITH</span></span>
<span data-ttu-id="ad7cd-255">Debe ser posible tooissue un apagado de máquina virtual a través de hello Azure CLI en lugar de una secuencia de comandos STONITH que controla un dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-255">It should be possible tooissue a VM shutdown via hello Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="ad7cd-256">Puede usar `/usr/lib/stonith/plugins/external/ssh` como base y habilitar STONITH en la configuración del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in hello cluster's configuration.</span></span> <span data-ttu-id="ad7cd-257">Debe instalarse globalmente CLI de Azure y configuración de publicación de Hola y se debe cargar el perfil de usuario del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-257">Azure CLI should be globally installed, and hello publish settings and profile should be loaded for hello cluster's user.</span></span>

<span data-ttu-id="ad7cd-258">Está disponible en el código de ejemplo para el recurso de hello [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="ad7cd-258">Sample code for hello resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="ad7cd-259">Cambiar configuración del clúster de hello agregando Hola después demasiado`sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-259">Change hello cluster's configuration by adding hello following too`sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="ad7cd-260">script de Hola no realiza comprobaciones de arriba/abajo.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-260">hello script doesn't perform up/down checks.</span></span> <span data-ttu-id="ad7cd-261">recurso de Hello original SSH tenía 15 comprobaciones de ping, pero el tiempo de recuperación para una máquina virtual de Azure puede ser más variables.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-261">hello original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="ad7cd-262">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="ad7cd-262">Limitations</span></span>
<span data-ttu-id="ad7cd-263">Hola siguientes limitaciones se aplica:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-263">hello following limitations apply:</span></span>

* <span data-ttu-id="ad7cd-264">Hola de script de recursos DRBD linbit que administra DRBD como un recurso en usos marcapasos `drbdadm down` al apagar un nodo, incluso si solo se va nodo hello en espera.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-264">hello linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if hello node is just going on standby.</span></span> <span data-ttu-id="ad7cd-265">Esto no es lo ideal porque esclavo hello no va a sincronizar recursos DRBD de Hola a pesar de master Hola lo escribe.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-265">This is not ideal because hello slave will not be synchronizing hello DRBD resource while hello master gets writes.</span></span> <span data-ttu-id="ad7cd-266">Si master hello no amablemente, esclavo Hola puede asumir un estado anterior del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-266">If hello master does not fail graciously, hello slave can take over an older file system state.</span></span> <span data-ttu-id="ad7cd-267">Hay dos formas posibles de resolver este problema:</span><span class="sxs-lookup"><span data-stu-id="ad7cd-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="ad7cd-268">Aplicando un comando `drbdadm up r0` en todos los nodos del clúster mediante un guardián local (sin clústeres)</span><span class="sxs-lookup"><span data-stu-id="ad7cd-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="ad7cd-269">Editar el script de Hola linbit DRBD, asegurándose de que `down` en no se llama`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="ad7cd-269">Editing hello linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="ad7cd-270">equilibrador de carga de Hello necesita toorespond de al menos cinco segundos, por lo que las aplicaciones deben ser compatible con clústeres y ser más tolerante a errores de tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-270">hello load balancer needs at least five seconds toorespond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="ad7cd-271">También pueden ayudar otras arquitecturas, como las colas de la aplicación y middlewares de consulta.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="ad7cd-272">MySQL para la optimización es tooensure necesario que realiza la escritura a un ritmo administrable y memorias caché son toodisk vaciado con tanta frecuencia como toominimize posible pérdida de memoria.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-272">MySQL tuning is necessary tooensure that writing is done at a manageable pace and caches are flushed toodisk as frequently as possible toominimize memory loss.</span></span>
* <span data-ttu-id="ad7cd-273">Escribir el rendimiento depende en VM de interconexión de conmutador virtual de hello porque se trata de mecanismo de hello DRBD tooreplicate Hola dispositivo usado.</span><span class="sxs-lookup"><span data-stu-id="ad7cd-273">Write performance is dependent in VM interconnect in hello virtual switch because this is hello mechanism used by DRBD tooreplicate hello device.</span></span>
