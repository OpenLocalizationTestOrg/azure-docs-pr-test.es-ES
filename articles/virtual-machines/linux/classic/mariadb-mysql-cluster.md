---
title: "Ejecución de un clúster MariaDB (MySQL) en Azure | Microsoft Docs"
description: "Creación de un clúster MariaDB + Galera MySQL en Azure Virtual Machines"
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: 53e9bf18b26338212411ea7c4f260eb308486738
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="df369-103">Clúster MariaDB (MySQL): tutorial de Azure</span><span class="sxs-lookup"><span data-stu-id="df369-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="df369-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico.</span><span class="sxs-lookup"><span data-stu-id="df369-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="df369-105">Este artículo trata sobre el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="df369-105">This article covers the classic deployment model.</span></span> <span data-ttu-id="df369-106">Microsoft recomienda que las implementaciones más recientes usen el modelo de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="df369-106">Microsoft recommends that most new deployments use the Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="df369-107">El clúster de MariaDB Enterprise está ahora disponible en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="df369-107">MariaDB Enterprise cluster is now available in the Azure Marketplace.</span></span> <span data-ttu-id="df369-108">La nueva oferta implementará automáticamente un clúster MariaDB Galera en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="df369-108">The new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="df369-109">Debe usar la nueva oferta de [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="df369-109">You should use the new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="df369-110">En este artículo se muestra cómo crear un clúster [Galera](http://galeracluster.com/products/) de varios maestros de [MariaDB](https://mariadb.org/en/about/) (una sustitución robusta, escalable y confiable de MySQL) para trabajar en un entorno de alta disponibilidad en Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="df369-110">This article shows you how to create a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) to work in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="df369-111">Introducción a la arquitectura</span><span class="sxs-lookup"><span data-stu-id="df369-111">Architecture overview</span></span>
<span data-ttu-id="df369-112">En este artículo se describe cómo completar los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="df369-112">This article describes how to complete the following steps:</span></span>

- <span data-ttu-id="df369-113">Crear un clúster de tres nodos.</span><span class="sxs-lookup"><span data-stu-id="df369-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="df369-114">Separar los discos de datos del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="df369-114">Separate the data disks from the OS disk.</span></span>
- <span data-ttu-id="df369-115">Crear los discos de datos en la configuración RAID-0/striped para aumentar la tasa de E/S por segundo.</span><span class="sxs-lookup"><span data-stu-id="df369-115">Create the data disks in RAID-0/striped setting to increase IOPS.</span></span>
- <span data-ttu-id="df369-116">Usar Azure Load Balancer para equilibrar la carga de los tres nodos.</span><span class="sxs-lookup"><span data-stu-id="df369-116">Use Azure Load Balancer to balance the load for the three nodes.</span></span>
- <span data-ttu-id="df369-117">Para minimizar el trabajo repetitivo, cree una imagen de máquina virtual que contenga MariaDB+Galera y úsela para crear otras máquinas virtuales de clúster.</span><span class="sxs-lookup"><span data-stu-id="df369-117">To minimize repetitive work, create a VM image that contains MariaDB + Galera and use it to create the other cluster VMs.</span></span>

![Arquitectura del sistema](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="df369-119">En este tema se usan las herramientas de la [CLI de Azure](../../../cli-install-nodejs.md); asegúrese de descargarlas y conectarlas a su suscripción de Azure siguiendo las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="df369-119">This topic uses the [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure to download them and connect them to your Azure subscription according to the instructions.</span></span> <span data-ttu-id="df369-120">Si necesita una referencia a los comandos disponibles en la CLI de Azure, consulte la [referencia de comandos de la CLI de Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="df369-120">If you need a reference to the commands available in the Azure CLI, see the [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="df369-121">También necesitará [crear una clave SSH para la autenticación] y anotar la ubicación del archivo .pem.</span><span class="sxs-lookup"><span data-stu-id="df369-121">You will also need to [create an SSH key for authentication] and make note of the .pem file location.</span></span>
>
>

## <a name="create-the-template"></a><span data-ttu-id="df369-122">Creación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="df369-122">Create the template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="df369-123">Infraestructura</span><span class="sxs-lookup"><span data-stu-id="df369-123">Infrastructure</span></span>
1. <span data-ttu-id="df369-124">Cree un grupo de afinidad para mantener juntos los recursos.</span><span class="sxs-lookup"><span data-stu-id="df369-124">Create an affinity group to hold the resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="df369-125">Cree una red virtual.</span><span class="sxs-lookup"><span data-stu-id="df369-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="df369-126">Cree una cuenta de almacenamiento para hospedar todos nuestros discos.</span><span class="sxs-lookup"><span data-stu-id="df369-126">Create a storage account to host all our disks.</span></span> <span data-ttu-id="df369-127">No debería colocar más de 40 discos de uso intensivo en la misma cuenta de almacenamiento para evitar llegar al límite de la cuenta de almacenamiento de 20,000 E/S por segundo.</span><span class="sxs-lookup"><span data-stu-id="df369-127">You shouldn't place more than 40 heavily used disks on the same storage account to avoid hitting the 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="df369-128">En este caso, está muy por debajo de ese límite, por lo que almacenará todo en la misma cuenta para simplificar.</span><span class="sxs-lookup"><span data-stu-id="df369-128">In this case, you're well below that limit, so you'll store everything on the same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="df369-129">Busque el nombre de la imagen de máquina virtual de CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="df369-129">Find the name of the CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="df369-130">El resultado tendrá un aspecto similar a `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="df369-130">The output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="df369-131">Use ese nombre en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="df369-131">Use that name in the following step.</span></span>
5. <span data-ttu-id="df369-132">Cree la plantilla de máquina virtual y reemplace /path/to/key.pem por la ruta de acceso donde almacenó la clave SSH .pem generada.</span><span class="sxs-lookup"><span data-stu-id="df369-132">Create the VM template and replace /path/to/key.pem with the path where you stored the generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="df369-133">Conecte cuatro discos de datos de 500 GB a la máquina virtual para su uso en la configuración de RAID.</span><span class="sxs-lookup"><span data-stu-id="df369-133">Attach four 500-GB data disks to the VM for use in the RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="df369-134">Use SSH para iniciar sesión en la plantilla de máquina virtual que creó en mariadbhatemplate.cloudapp.net:22 y conéctese con su clave privada.</span><span class="sxs-lookup"><span data-stu-id="df369-134">Use SSH to sign in to the template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="df369-135">Software</span><span class="sxs-lookup"><span data-stu-id="df369-135">Software</span></span>
1. <span data-ttu-id="df369-136">Obtenga la raíz.</span><span class="sxs-lookup"><span data-stu-id="df369-136">Get the root.</span></span>

        sudo su

2. <span data-ttu-id="df369-137">Instalar compatibilidad con RAID:</span><span class="sxs-lookup"><span data-stu-id="df369-137">Install RAID support:</span></span>

    <span data-ttu-id="df369-138">a.</span><span class="sxs-lookup"><span data-stu-id="df369-138">a.</span></span> <span data-ttu-id="df369-139">Instale mdadm.</span><span class="sxs-lookup"><span data-stu-id="df369-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="df369-140">b.</span><span class="sxs-lookup"><span data-stu-id="df369-140">b.</span></span> <span data-ttu-id="df369-141">Cree la configuración RAID0/stripe con un sistema de archivos EXT4.</span><span class="sxs-lookup"><span data-stu-id="df369-141">Create the RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="df369-142">c.</span><span class="sxs-lookup"><span data-stu-id="df369-142">c.</span></span> <span data-ttu-id="df369-143">Cree el directorio de punto de montaje.</span><span class="sxs-lookup"><span data-stu-id="df369-143">Create the mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="df369-144">d.</span><span class="sxs-lookup"><span data-stu-id="df369-144">d.</span></span> <span data-ttu-id="df369-145">Recupere el UUID del dispositivo RAID recién creado.</span><span class="sxs-lookup"><span data-stu-id="df369-145">Retrieve the UUID of the newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="df369-146">e.</span><span class="sxs-lookup"><span data-stu-id="df369-146">e.</span></span> <span data-ttu-id="df369-147">Edite /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="df369-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="df369-148">f.</span><span class="sxs-lookup"><span data-stu-id="df369-148">f.</span></span> <span data-ttu-id="df369-149">Agregue el dispositivo para habilitar el montaje automático en el reinicio. Para ello, reemplace el UUID por el valor obtenido con el comando **blkid** anterior.</span><span class="sxs-lookup"><span data-stu-id="df369-149">Add the device to enable auto mounting on reboot, replacing the UUID with the value obtained from the previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="df369-150">g.</span><span class="sxs-lookup"><span data-stu-id="df369-150">g.</span></span> <span data-ttu-id="df369-151">Monte la partición nueva.</span><span class="sxs-lookup"><span data-stu-id="df369-151">Mount the new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="df369-152">Instale MariaDB.</span><span class="sxs-lookup"><span data-stu-id="df369-152">Install MariaDB.</span></span>

    <span data-ttu-id="df369-153">a.</span><span class="sxs-lookup"><span data-stu-id="df369-153">a.</span></span> <span data-ttu-id="df369-154">Cree el archivo MariaDB.repo.</span><span class="sxs-lookup"><span data-stu-id="df369-154">Create the MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="df369-155">b.</span><span class="sxs-lookup"><span data-stu-id="df369-155">b.</span></span> <span data-ttu-id="df369-156">Rellene el archivo de repositorio con el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="df369-156">Fill the repo file with the following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="df369-157">c.</span><span class="sxs-lookup"><span data-stu-id="df369-157">c.</span></span> <span data-ttu-id="df369-158">Para evitar conflictos, quite el postfijo existente y mariadb-libs.</span><span class="sxs-lookup"><span data-stu-id="df369-158">To avoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="df369-159">d.</span><span class="sxs-lookup"><span data-stu-id="df369-159">d.</span></span> <span data-ttu-id="df369-160">Instale MariaDB con Galera.</span><span class="sxs-lookup"><span data-stu-id="df369-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="df369-161">Mueva el directorio de datos de MySQL al dispositivo de bloques RAID.</span><span class="sxs-lookup"><span data-stu-id="df369-161">Move the MySQL data directory to the RAID block device.</span></span>

    <span data-ttu-id="df369-162">a.</span><span class="sxs-lookup"><span data-stu-id="df369-162">a.</span></span> <span data-ttu-id="df369-163">Copie el directorio actual de MySQL en su nueva ubicación y quite el directorio antiguo.</span><span class="sxs-lookup"><span data-stu-id="df369-163">Copy the current MySQL directory into its new location and remove the old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="df369-164">b.</span><span class="sxs-lookup"><span data-stu-id="df369-164">b.</span></span> <span data-ttu-id="df369-165">Establezca los permisos del nuevo directorio según corresponda.</span><span class="sxs-lookup"><span data-stu-id="df369-165">Set permissions for the new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="df369-166">c.</span><span class="sxs-lookup"><span data-stu-id="df369-166">c.</span></span> <span data-ttu-id="df369-167">Cree un vínculo simbólico que apunte al directorio anterior en la nueva ubicación en la partición RAID.</span><span class="sxs-lookup"><span data-stu-id="df369-167">Create a symlink that points the old directory to the new location on the RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="df369-168">Dado que [SELinux interfiere con las operaciones del clúster](http://galeracluster.com/documentation-webpages/configuration.html#selinux), es necesario deshabilitarlo para la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="df369-168">Because [SELinux interferes with the cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary to disable it for the current session.</span></span> <span data-ttu-id="df369-169">Edite `/etc/selinux/config` para deshabilitar los reinicios posteriores.</span><span class="sxs-lookup"><span data-stu-id="df369-169">Edit `/etc/selinux/config` to disable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` to set `SELINUX=permissive`
6. <span data-ttu-id="df369-170">Valide las ejecuciones de MySQL.</span><span class="sxs-lookup"><span data-stu-id="df369-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="df369-171">a.</span><span class="sxs-lookup"><span data-stu-id="df369-171">a.</span></span> <span data-ttu-id="df369-172">Inicie MySQL.</span><span class="sxs-lookup"><span data-stu-id="df369-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="df369-173">b.</span><span class="sxs-lookup"><span data-stu-id="df369-173">b.</span></span> <span data-ttu-id="df369-174">Proteja la instalación de MySQL, establezca la contraseña raíz, quite los usuarios anónimos para deshabilitar el inicio de sesión raíz remoto y quite la base de datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="df369-174">Secure the MySQL installation, set the root password, remove anonymous users to disable remote root login, and remove the test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="df369-175">c.</span><span class="sxs-lookup"><span data-stu-id="df369-175">c.</span></span> <span data-ttu-id="df369-176">Cree un usuario en la base de datos para las operaciones de clúster y, opcionalmente, para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="df369-176">Create a user on the database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* TO 'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="df369-177">d.</span><span class="sxs-lookup"><span data-stu-id="df369-177">d.</span></span> <span data-ttu-id="df369-178">Detenga MySQL.</span><span class="sxs-lookup"><span data-stu-id="df369-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="df369-179">Cree un marcador de posición de configuración.</span><span class="sxs-lookup"><span data-stu-id="df369-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="df369-180">a.</span><span class="sxs-lookup"><span data-stu-id="df369-180">a.</span></span> <span data-ttu-id="df369-181">Edite la configuración de MySQL para crear un marcador de posición para la configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="df369-181">Edit the MySQL configuration to create a placeholder for the cluster settings.</span></span> <span data-ttu-id="df369-182">En este momento, no reemplace las **`<Variables>`** ni quite la marca de comentario.</span><span class="sxs-lookup"><span data-stu-id="df369-182">Do not replace the **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="df369-183">Eso sucederá después de que cree una máquina virtual desde esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="df369-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="df369-184">b.</span><span class="sxs-lookup"><span data-stu-id="df369-184">b.</span></span> <span data-ttu-id="df369-185">Edite la sección **[galera]** y desactívela.</span><span class="sxs-lookup"><span data-stu-id="df369-185">Edit the **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="df369-186">c.</span><span class="sxs-lookup"><span data-stu-id="df369-186">c.</span></span> <span data-ttu-id="df369-187">Edite la sección **[mariadb]**.</span><span class="sxs-lookup"><span data-stu-id="df369-187">Edit the **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set to 0.0.0.0, the server listens to remote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for the SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set the node name of this server
8. <span data-ttu-id="df369-188">Abra los puertos necesarios en el firewall mediante FirewallD en CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="df369-188">Open required ports on the firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="df369-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="df369-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="df369-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="df369-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="df369-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="df369-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="df369-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="df369-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="df369-193">Vuelva a cargar el firewall: `firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="df369-193">Reload the firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="df369-194">Optimice el sistema para el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="df369-194">Optimize the system for performance.</span></span> <span data-ttu-id="df369-195">Para más información, consulte la [estrategia de optimización del rendimiento](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="df369-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="df369-196">a.</span><span class="sxs-lookup"><span data-stu-id="df369-196">a.</span></span> <span data-ttu-id="df369-197">Edite nuevamente el archivo de configuración de MySQL.</span><span class="sxs-lookup"><span data-stu-id="df369-197">Edit the MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="df369-198">b.</span><span class="sxs-lookup"><span data-stu-id="df369-198">b.</span></span> <span data-ttu-id="df369-199">Edite la sección **[mariadb]** y anexe el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="df369-199">Edit the **[mariadb]** section and append the following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="df369-200">Se recomienda que innodb\_buffer\_pool_size sea el 70 % de la memoria de su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="df369-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="df369-201">En este ejemplo, se estableció en 2.45 GB para la máquina virtual de Azure mediana con 3.5 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="df369-201">In this example, it has been set at 2.45 GB for the medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # The buffer pool contains buffered data and the index. This is usually set to 70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give the server more time to recycle idled connections
           innodb_file_per_table = 1 # Speed up the table space transmission and optimize the debris management performance
           innodb_log_buffer_size = 128M # The log buffer allows transactions to run without having to flush the log to disk before the transactions commit
           innodb_flush_log_at_trx_commit = 2 # The setting of 2 enables the most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="df369-202">Detenga MySQL, deshabilite el servicio MySQL para que no se ejecute al inicio y, de esta forma, evitar toda interrupción del clúster al agregar un nodo y desaprovisionar la máquina.</span><span class="sxs-lookup"><span data-stu-id="df369-202">Stop MySQL, disable MySQL service from running on startup to avoid disrupting the cluster when adding a node, and deprovision the machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="df369-203">Capture la máquina virtual a través del portal.</span><span class="sxs-lookup"><span data-stu-id="df369-203">Capture the VM through the portal.</span></span> <span data-ttu-id="df369-204">(Actualmente, el [problema #1268 en las herramientas de la CLI de Azure](https://github.com/Azure/azure-xplat-cli/issues/1268) describe el hecho de que las imágenes capturadas por las herramientas de la CLI de Azure no capturan los discos de datos adjuntos).</span><span class="sxs-lookup"><span data-stu-id="df369-204">(Currently, [issue #1268 in the Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes the fact that images captured by the Azure CLI tools do not capture the attached data disks.)</span></span>

    <span data-ttu-id="df369-205">a.</span><span class="sxs-lookup"><span data-stu-id="df369-205">a.</span></span> <span data-ttu-id="df369-206">Apague la máquina mediante el portal.</span><span class="sxs-lookup"><span data-stu-id="df369-206">Shut down the machine through the portal.</span></span>

    <span data-ttu-id="df369-207">b.</span><span class="sxs-lookup"><span data-stu-id="df369-207">b.</span></span> <span data-ttu-id="df369-208">Haga clic en **Capturar** y especifique el nombre de la imagen como **mariadb-galera-image**.</span><span class="sxs-lookup"><span data-stu-id="df369-208">Click **Capture** and specify the image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="df369-209">Proporcione una descripción y seleccione "He ejecutado waagent".</span><span class="sxs-lookup"><span data-stu-id="df369-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Captura de la máquina virtual](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-the-cluster"></a><span data-ttu-id="df369-211">Creación de clústeres</span><span class="sxs-lookup"><span data-stu-id="df369-211">Create the cluster</span></span>
<span data-ttu-id="df369-212">Cree tres máquinas virtuales con la plantilla que creó y, luego, configure e inicie el clúster.</span><span class="sxs-lookup"><span data-stu-id="df369-212">Create three VMs with the template you created, and then configure and start the cluster.</span></span>

1. <span data-ttu-id="df369-213">Cree la primera máquina virtual de CentOS 7 desde la imagen mariadb-galera-image que creó y proporcione la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="df369-213">Create the first CentOS 7 VM from the mariadb-galera-image image you created, providing the following information:</span></span>

 - <span data-ttu-id="df369-214">Nombre de la red virtual: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="df369-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="df369-215">Subred: mariadb</span><span class="sxs-lookup"><span data-stu-id="df369-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="df369-216">Tamaño de la máquina: mediana</span><span class="sxs-lookup"><span data-stu-id="df369-216">Machine size: medium</span></span>
 - <span data-ttu-id="df369-217">Nombre del servicio en la nube: mariadbha (o el nombre que desee al que se obtenga acceso desde mariadbha.cloudapp.net)</span><span class="sxs-lookup"><span data-stu-id="df369-217">Cloud service name: mariadbha (or whatever name you want to be accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="df369-218">Nombre de la máquina: mariadb1</span><span class="sxs-lookup"><span data-stu-id="df369-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="df369-219">Nombre del usuario: azureuser</span><span class="sxs-lookup"><span data-stu-id="df369-219">Username: azureuser</span></span>
 - <span data-ttu-id="df369-220">Acceso de SSH: habilitado</span><span class="sxs-lookup"><span data-stu-id="df369-220">SSH access: enabled</span></span>
 - <span data-ttu-id="df369-221">Pase el archivo .pem del certificado SSH y reemplace /path/to/key.pem por la ruta de acceso donde almacenó la clave SSH .pem generada.</span><span class="sxs-lookup"><span data-stu-id="df369-221">Passing the SSH certificate .pem file and replacing /path/to/key.pem with the path where you stored the generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="df369-222">Los comandos siguientes se dividen en varias líneas para mayor claridad, pero debe especificar cada uno de ellos como una sola línea.</span><span class="sxs-lookup"><span data-stu-id="df369-222">The following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. <span data-ttu-id="df369-223">Cree dos máquinas virtuales; para ello, conéctelas al servicio en la nube mariadbha.</span><span class="sxs-lookup"><span data-stu-id="df369-223">Create two more virtual machines by connecting them to the mariadbha cloud service.</span></span> <span data-ttu-id="df369-224">Cambie el nombre de la máquina virtual y el puerto SSH por un puerto único que no tenga conflictos con otras máquinas virtuales en el mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="df369-224">Change the VM name and the SSH port to a unique port not conflicting with other VMs in the same cloud service.</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  <span data-ttu-id="df369-225">Para MariaDB3:</span><span class="sxs-lookup"><span data-stu-id="df369-225">For MariaDB3:</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. <span data-ttu-id="df369-226">Necesitará obtener la dirección IP interna de cada una de las tres máquinas virtuales para el siguiente paso:</span><span class="sxs-lookup"><span data-stu-id="df369-226">You will need to get the internal IP address of each of the three VMs for the next step:</span></span>

    ![Obtención de la dirección IP](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="df369-228">Use SSH para iniciar sesión en las tres máquinas virtuales y edite el archivo de configuración de cada una de ellas.</span><span class="sxs-lookup"><span data-stu-id="df369-228">Use SSH to sign in to the three VMs and edit the configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="df369-229">Quite la marca de comentario **`wsrep_cluster_name`** y **`wsrep_cluster_address`**; para ello, quite el símbolo **#** que se encuentra al comienzo de la línea.</span><span class="sxs-lookup"><span data-stu-id="df369-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing the **#** at the beginning of the line.</span></span>
    <span data-ttu-id="df369-230">Además, reemplace **`<ServerIP>`** en **`wsrep_node_address`** y **`<NodeName>`** en **`wsrep_node_name`** por la dirección IP y el nombre, respectivamente, de las máquinas virtuales, y quite las marcas de comentario de esas líneas también.</span><span class="sxs-lookup"><span data-stu-id="df369-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with the VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="df369-231">Inicie el clúster en MariaDB1 y deje que se ejecute en el inicio.</span><span class="sxs-lookup"><span data-stu-id="df369-231">Start the cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="df369-232">Inicie MySQL en MariaDB2 y MariaDB3 y deje que se ejecute en el inicio.</span><span class="sxs-lookup"><span data-stu-id="df369-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-the-cluster"></a><span data-ttu-id="df369-233">Equilibro de carga del clúster</span><span class="sxs-lookup"><span data-stu-id="df369-233">Load balance the cluster</span></span>
<span data-ttu-id="df369-234">Al crear las máquinas virtuales en clúster, las agregó al conjunto de disponibilidad denominado clusteravset para asegurarse de que se colocaron en diferentes dominios de error y de actualización, y que Azure nunca realizará el mantenimiento en todos los equipos a la vez.</span><span class="sxs-lookup"><span data-stu-id="df369-234">When you created the clustered VMs, you added them into an availability set called clusteravset to ensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="df369-235">Esta configuración cumple los requisitos para ser compatible por el Acuerdo de Nivel de Servicio (SLA) de Azure.</span><span class="sxs-lookup"><span data-stu-id="df369-235">This configuration meets the requirements to be supported by the Azure service level agreement (SLA).</span></span>

<span data-ttu-id="df369-236">Ahora use Azure Load Balancer para equilibrar las solicitudes entre los tres nodos.</span><span class="sxs-lookup"><span data-stu-id="df369-236">Now use Azure Load Balancer to balance requests between the three nodes.</span></span>

<span data-ttu-id="df369-237">Ejecute los comandos siguientes en la máquina con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="df369-237">Run the following commands on your machine by using the Azure CLI.</span></span>

<span data-ttu-id="df369-238">La estructura de los parámetros de comando es: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="df369-238">The command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="df369-239">La CLI establece el intervalo de sondeo del equilibrador de carga en 15 segundos, lo que puede resultar demasiado largo.</span><span class="sxs-lookup"><span data-stu-id="df369-239">The CLI sets the load balancer probe interval to 15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="df369-240">Cámbielo en el portal en **Puntos de conexión** para cualquiera de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="df369-240">Change it in the portal under **Endpoints** for any of the VMs.</span></span>

![Edición del extremo](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="df369-242">Seleccione **Volver a configurar el conjunto de carga equilibrada**.</span><span class="sxs-lookup"><span data-stu-id="df369-242">Select **Reconfigure the Load-Balanced Set**.</span></span>

![Volver a configurar el conjunto de carga equilibrada](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="df369-244">Cambie **Intervalo de sondeo** a 5 segundos y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="df369-244">Change **Probe Interval** to 5 seconds and save your changes.</span></span>

![Cambio del intervalo de sondeo](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-the-cluster"></a><span data-ttu-id="df369-246">Validación del clúster</span><span class="sxs-lookup"><span data-stu-id="df369-246">Validate the cluster</span></span>
<span data-ttu-id="df369-247">El trabajo más duro ya está terminado.</span><span class="sxs-lookup"><span data-stu-id="df369-247">The hard work is done.</span></span> <span data-ttu-id="df369-248">Ahora, el clúster debe ser accesible en `mariadbha.cloudapp.net:3306`, que alcanzará al equilibrador de carga y enrutará las solicitudes entre las tres máquinas virtuales de forma fluida y eficaz.</span><span class="sxs-lookup"><span data-stu-id="df369-248">The cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits the load balancer and route requests between the three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="df369-249">Use el cliente de MySQL de su preferencia para conectarse o conéctese directamente desde una de las máquinas virtuales para comprobar que funciona este clúster.</span><span class="sxs-lookup"><span data-stu-id="df369-249">Use your favorite MySQL client to connect, or connect from one of the VMs to verify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="df369-250">A continuación, cree una base de datos y rellénela con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="df369-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="df369-251">La base de datos que creó devuelve la siguiente tabla:</span><span class="sxs-lookup"><span data-stu-id="df369-251">The database you created returns the following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="df369-252">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df369-252">Next steps</span></span>
<span data-ttu-id="df369-253">En este artículo, creó un clúster MariaDB+Galera de alta disponibilidad de tres nodos en Azure Virtual Machines con CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="df369-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="df369-254">Las máquinas virtuales tienen equilibro de carga con Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="df369-254">The VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="df369-255">Puede que desee echar un vistazo a [otro modo para el clúster MySQL en Linux](mysql-cluster.md) y ver otras formas de [optimizar y probar el rendimiento de MySQL en máquinas virtuales Linux con Azure](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="df369-255">You might want to look at [another way to cluster MySQL on Linux](mysql-cluster.md) and ways to [optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating the template]:#creating-the-template
[Creating the cluster]:#creating-the-cluster
[Load balancing the cluster]:#load-balancing-the-cluster
[Validating the cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
<span data-ttu-id="df369-256">[Galera]:http://galeracluster.com/products/</span><span class="sxs-lookup"><span data-stu-id="df369-256">[Galera]:http://galeracluster.com/products/</span></span>
[MariaDBs]:https://mariadb.org/en/about/
<span data-ttu-id="df369-257">[crear una clave SSH para la autenticación]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/</span><span class="sxs-lookup"><span data-stu-id="df369-257">[create an SSH key for authentication]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/</span></span>
[issue #1268 in the Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
