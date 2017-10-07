---
title: "aaaRun un MariaDB (MySQL) del clúster en Azure | Documentos de Microsoft"
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
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="5cd5f-103">Clúster MariaDB (MySQL): tutorial de Azure</span><span class="sxs-lookup"><span data-stu-id="5cd5f-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5cd5f-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="5cd5f-105">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-105">This article covers hello classic deployment model.</span></span> <span data-ttu-id="5cd5f-106">Microsoft recomienda que más nuevas implementaciones de usar modelos de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-106">Microsoft recommends that most new deployments use hello Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="5cd5f-107">Clúster de MariaDB Enterprise ahora está disponible en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-107">MariaDB Enterprise cluster is now available in hello Azure Marketplace.</span></span> <span data-ttu-id="5cd5f-108">nueva oferta de Hello implementará automáticamente un clúster de MariaDB Galera en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-108">hello new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="5cd5f-109">Debe usar la nueva oferta de Hola de [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="5cd5f-109">You should use hello new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="5cd5f-110">Este artículo muestra cómo toocreate una con varios maestros [Galera](http://galeracluster.com/products/) clúster de [MariaDBs](https://mariadb.org/en/about/) (un reemplazo e inmediata robusta, escalable y confiable para MySQL) toowork en un entorno de alta disponibilidad en Azure máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-110">This article shows you how toocreate a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) toowork in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="5cd5f-111">Introducción a la arquitectura</span><span class="sxs-lookup"><span data-stu-id="5cd5f-111">Architecture overview</span></span>
<span data-ttu-id="5cd5f-112">Este artículo describe cómo hello toocomplete siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="5cd5f-112">This article describes how toocomplete hello following steps:</span></span>

- <span data-ttu-id="5cd5f-113">Crear un clúster de tres nodos.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="5cd5f-114">Discos de datos de hello independiente del disco de sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-114">Separate hello data disks from hello OS disk.</span></span>
- <span data-ttu-id="5cd5f-115">Crear discos de datos de hello en configuración de RAID-0/particionados tooincrease e/s por segundo.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-115">Create hello data disks in RAID-0/striped setting tooincrease IOPS.</span></span>
- <span data-ttu-id="5cd5f-116">Use de carga del equilibrador de carga de Azure toobalance Hola para hello tres nodos.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-116">Use Azure Load Balancer toobalance hello load for hello three nodes.</span></span>
- <span data-ttu-id="5cd5f-117">toominimize repetitiva de trabajo, crear una imagen de máquina virtual que contiene MariaDB + Galera y utilizarlo toocreate Hola otro máquinas virtuales del clúster.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-117">toominimize repetitive work, create a VM image that contains MariaDB + Galera and use it toocreate hello other cluster VMs.</span></span>

![Arquitectura del sistema](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="5cd5f-119">En este tema usa hello [CLI de Azure](../../../cli-install-nodejs.md) herramientas, por lo que debe toodownload seguro de ellos y conéctelos correspondiente toohello instrucciones de tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-119">This topic uses hello [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure toodownload them and connect them tooyour Azure subscription according toohello instructions.</span></span> <span data-ttu-id="5cd5f-120">Si necesita un comandos de toohello de referencia disponibles en hello CLI de Azure, vea hello [referencia de comandos de CLI de Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="5cd5f-120">If you need a reference toohello commands available in hello Azure CLI, see hello [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="5cd5f-121">También necesitará demasiado[crear una clave SSH para la autenticación] y tome nota de la ubicación del archivo PEM Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-121">You will also need too[create an SSH key for authentication] and make note of hello .pem file location.</span></span>
>
>

## <a name="create-hello-template"></a><span data-ttu-id="5cd5f-122">Crear plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="5cd5f-122">Create hello template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="5cd5f-123">Infraestructura</span><span class="sxs-lookup"><span data-stu-id="5cd5f-123">Infrastructure</span></span>
1. <span data-ttu-id="5cd5f-124">Crear un grupo de afinidad toohold recursos de hello juntos.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-124">Create an affinity group toohold hello resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="5cd5f-125">Cree una red virtual.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="5cd5f-126">Crear un toohost de cuenta de almacenamiento nuestro todos los discos.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-126">Create a storage account toohost all our disks.</span></span> <span data-ttu-id="5cd5f-127">No debería colocar más de 40 discos muy utilizados en hello mismo tooavoid de cuenta de almacenamiento alcanza el límite de la cuenta de almacenamiento de hello 20.000 e/s por segundo.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-127">You shouldn't place more than 40 heavily used disks on hello same storage account tooavoid hitting hello 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="5cd5f-128">En este caso, está por debajo de ese límite, por lo que podrá almacenar todo el contenido en la misma cuenta para simplificar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-128">In this case, you're well below that limit, so you'll store everything on hello same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="5cd5f-129">Buscar el nombre de Hola de imagen de máquina virtual de hello CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-129">Find hello name of hello CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="5cd5f-130">salida de Hello será similar a `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-130">hello output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="5cd5f-131">Use ese nombre en hello siguiendo el paso.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-131">Use that name in hello following step.</span></span>
5. <span data-ttu-id="5cd5f-132">Crear plantilla de VM de Hola y reemplace /path/to/key.pem por ruta de acceso de Hola dónde ha almacenado Hola genera PEM SSH clave.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-132">Create hello VM template and replace /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="5cd5f-133">Adjuntar datos de 500 GB cuatro discos toohello máquina virtual para su uso en la configuración de RAID de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-133">Attach four 500-GB data disks toohello VM for use in hello RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="5cd5f-134">Utilizar SSH toosign en toohello plantilla máquina virtual que creó al mariadbhatemplate.cloudapp.net:22 y conectarse con su clave privada.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-134">Use SSH toosign in toohello template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="5cd5f-135">Software</span><span class="sxs-lookup"><span data-stu-id="5cd5f-135">Software</span></span>
1. <span data-ttu-id="5cd5f-136">Obtener la raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-136">Get hello root.</span></span>

        sudo su

2. <span data-ttu-id="5cd5f-137">Instalar compatibilidad con RAID:</span><span class="sxs-lookup"><span data-stu-id="5cd5f-137">Install RAID support:</span></span>

    <span data-ttu-id="5cd5f-138">a.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-138">a.</span></span> <span data-ttu-id="5cd5f-139">Instale mdadm.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="5cd5f-140">b.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-140">b.</span></span> <span data-ttu-id="5cd5f-141">Crear configuración de RAID0/bandas de hello con un sistema de archivos EXT4.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-141">Create hello RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="5cd5f-142">c.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-142">c.</span></span> <span data-ttu-id="5cd5f-143">Crear el directorio de punto de montaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-143">Create hello mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="5cd5f-144">d.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-144">d.</span></span> <span data-ttu-id="5cd5f-145">Recuperar Hola UUID del dispositivo RAID de hello recién creado.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-145">Retrieve hello UUID of hello newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="5cd5f-146">e.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-146">e.</span></span> <span data-ttu-id="5cd5f-147">Edite /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="5cd5f-148">f.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-148">f.</span></span> <span data-ttu-id="5cd5f-149">Agregar automáticamente de hello dispositivo tooenable montar en el reinicio, reemplazando Hola UUID con valor de hello obtenido de hello anterior **blkid** comando.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-149">Add hello device tooenable auto mounting on reboot, replacing hello UUID with hello value obtained from hello previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="5cd5f-150">g.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-150">g.</span></span> <span data-ttu-id="5cd5f-151">Monte la nueva partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-151">Mount hello new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="5cd5f-152">Instale MariaDB.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-152">Install MariaDB.</span></span>

    <span data-ttu-id="5cd5f-153">a.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-153">a.</span></span> <span data-ttu-id="5cd5f-154">Crear archivo de hello MariaDB.repo.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-154">Create hello MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="5cd5f-155">b.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-155">b.</span></span> <span data-ttu-id="5cd5f-156">Rellenar el archivo de repositorio de hello con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="5cd5f-156">Fill hello repo file with hello following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="5cd5f-157">c.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-157">c.</span></span> <span data-ttu-id="5cd5f-158">tooavoid entra en conflicto, quite postfijo existente y las bibliotecas de mariadb.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-158">tooavoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="5cd5f-159">d.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-159">d.</span></span> <span data-ttu-id="5cd5f-160">Instale MariaDB con Galera.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="5cd5f-161">Mueva el dispositivo de bloque de hello MySQL datos directory toohello RAID.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-161">Move hello MySQL data directory toohello RAID block device.</span></span>

    <span data-ttu-id="5cd5f-162">a.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-162">a.</span></span> <span data-ttu-id="5cd5f-163">Copie el directorio actual de MySQL de hello en su nueva ubicación y quitar el directorio anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-163">Copy hello current MySQL directory into its new location and remove hello old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="5cd5f-164">b.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-164">b.</span></span> <span data-ttu-id="5cd5f-165">Establecer permisos para el nuevo directorio de hello en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-165">Set permissions for hello new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="5cd5f-166">c.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-166">c.</span></span> <span data-ttu-id="5cd5f-167">Crear un vínculo simbólico que apunta Hola antiguo toohello nueva ubicación del directorio en hello partición RAID.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-167">Create a symlink that points hello old directory toohello new location on hello RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="5cd5f-168">Porque [SELinux interfiere con las operaciones del clúster hello](http://galeracluster.com/documentation-webpages/configuration.html#selinux), es necesario toodisable para hello sesión actual.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-168">Because [SELinux interferes with hello cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary toodisable it for hello current session.</span></span> <span data-ttu-id="5cd5f-169">Editar `/etc/selinux/config` toodisable para reinicios posteriores.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-169">Edit `/etc/selinux/config` toodisable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. <span data-ttu-id="5cd5f-170">Valide las ejecuciones de MySQL.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="5cd5f-171">a.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-171">a.</span></span> <span data-ttu-id="5cd5f-172">Inicie MySQL.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="5cd5f-173">b.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-173">b.</span></span> <span data-ttu-id="5cd5f-174">Proteger la instalación de MySQL de hello, establecer contraseña de la raíz de hello, quita el inicio de sesión de los usuarios anónimos toodisable raíz remota y quitar base de datos de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-174">Secure hello MySQL installation, set hello root password, remove anonymous users toodisable remote root login, and remove hello test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="5cd5f-175">c.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-175">c.</span></span> <span data-ttu-id="5cd5f-176">Cree un usuario en la base de datos de Hola para las operaciones del clúster y, opcionalmente, para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-176">Create a user on hello database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="5cd5f-177">d.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-177">d.</span></span> <span data-ttu-id="5cd5f-178">Detenga MySQL.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="5cd5f-179">Cree un marcador de posición de configuración.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="5cd5f-180">a.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-180">a.</span></span> <span data-ttu-id="5cd5f-181">Editar Hola MySQL configuración toocreate un marcador de posición para la configuración de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-181">Edit hello MySQL configuration toocreate a placeholder for hello cluster settings.</span></span> <span data-ttu-id="5cd5f-182">No Reemplace hello  **`<Variables>`**  o quite ahora.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-182">Do not replace hello **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="5cd5f-183">Eso sucederá después de que cree una máquina virtual desde esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="5cd5f-184">b.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-184">b.</span></span> <span data-ttu-id="5cd5f-185">Editar hello  **[galera]**  sección y desactive.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-185">Edit hello **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="5cd5f-186">c.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-186">c.</span></span> <span data-ttu-id="5cd5f-187">Editar hello **[mariadb]** sección.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-187">Edit hello **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. <span data-ttu-id="5cd5f-188">Abra los puertos necesarios en firewall de hello mediante FirewallD en CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-188">Open required ports on hello firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="5cd5f-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="5cd5f-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="5cd5f-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="5cd5f-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="5cd5f-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="5cd5f-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="5cd5f-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="5cd5f-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="5cd5f-193">Volver a cargar Hola firewall:`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="5cd5f-193">Reload hello firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="5cd5f-194">Optimizar el sistema de hello para el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-194">Optimize hello system for performance.</span></span> <span data-ttu-id="5cd5f-195">Para más información, consulte la [estrategia de optimización del rendimiento](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="5cd5f-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="5cd5f-196">a.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-196">a.</span></span> <span data-ttu-id="5cd5f-197">Modifique el archivo de configuración de MySQL de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-197">Edit hello MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="5cd5f-198">b.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-198">b.</span></span> <span data-ttu-id="5cd5f-199">Editar hello **[mariadb]** anexar Hola siguen contenido y la sección:</span><span class="sxs-lookup"><span data-stu-id="5cd5f-199">Edit hello **[mariadb]** section and append hello following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="5cd5f-200">Se recomienda que innodb\_buffer\_pool_size sea el 70 % de la memoria de su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="5cd5f-201">En este ejemplo, se se estableció en 2,45 GB de tamaño mediano Hola VM de Azure con 3,5 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-201">In this example, it has been set at 2.45 GB for hello medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="5cd5f-202">Detener MySQL, deshabilitar el servicio MySQL no se ejecuten en tooavoid inicio interrumpir clúster Hola al agregar un nodo y desaprovisionar máquina Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-202">Stop MySQL, disable MySQL service from running on startup tooavoid disrupting hello cluster when adding a node, and deprovision hello machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="5cd5f-203">Capturar Hola VM a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-203">Capture hello VM through hello portal.</span></span> <span data-ttu-id="5cd5f-204">(Actualmente, [emitir #1268 en herramientas de Azure CLI hello](https://github.com/Azure/azure-xplat-cli/issues/1268) describe los hechos de Hola que imágenes capturadas con herramientas de hello Azure CLI no capturan Hola adjuntada los discos de datos.)</span><span class="sxs-lookup"><span data-stu-id="5cd5f-204">(Currently, [issue #1268 in hello Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes hello fact that images captured by hello Azure CLI tools do not capture hello attached data disks.)</span></span>

    <span data-ttu-id="5cd5f-205">a.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-205">a.</span></span> <span data-ttu-id="5cd5f-206">Apagar la máquina de Hola a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-206">Shut down hello machine through hello portal.</span></span>

    <span data-ttu-id="5cd5f-207">b.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-207">b.</span></span> <span data-ttu-id="5cd5f-208">Haga clic en **capturar** y especifique el nombre de la imagen de hello como **mariadb-galera-image**.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-208">Click **Capture** and specify hello image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="5cd5f-209">Proporcione una descripción y seleccione "He ejecutado waagent".</span><span class="sxs-lookup"><span data-stu-id="5cd5f-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Captura de máquina virtual de Hola](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a><span data-ttu-id="5cd5f-211">Crear clúster Hola</span><span class="sxs-lookup"><span data-stu-id="5cd5f-211">Create hello cluster</span></span>
<span data-ttu-id="5cd5f-212">Cree tres máquinas virtuales con plantilla de hello creado y, a continuación, configurará e iniciará el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-212">Create three VMs with hello template you created, and then configure and start hello cluster.</span></span>

1. <span data-ttu-id="5cd5f-213">Crear Hola primera CentOS 7 VM de hello mariadb-galera-imagen de la imagen que ha creado, a proporcionar Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5cd5f-213">Create hello first CentOS 7 VM from hello mariadb-galera-image image you created, providing hello following information:</span></span>

 - <span data-ttu-id="5cd5f-214">Nombre de la red virtual: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="5cd5f-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="5cd5f-215">Subred: mariadb</span><span class="sxs-lookup"><span data-stu-id="5cd5f-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="5cd5f-216">Tamaño de la máquina: mediana</span><span class="sxs-lookup"><span data-stu-id="5cd5f-216">Machine size: medium</span></span>
 - <span data-ttu-id="5cd5f-217">Nombre de servicio de nube: mariadbha (o cualquier nombre que desee toobe tiene acceso a través de mariadbha.cloudapp.net)</span><span class="sxs-lookup"><span data-stu-id="5cd5f-217">Cloud service name: mariadbha (or whatever name you want toobe accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="5cd5f-218">Nombre de la máquina: mariadb1</span><span class="sxs-lookup"><span data-stu-id="5cd5f-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="5cd5f-219">Nombre del usuario: azureuser</span><span class="sxs-lookup"><span data-stu-id="5cd5f-219">Username: azureuser</span></span>
 - <span data-ttu-id="5cd5f-220">Acceso de SSH: habilitado</span><span class="sxs-lookup"><span data-stu-id="5cd5f-220">SSH access: enabled</span></span>
 - <span data-ttu-id="5cd5f-221">Pasar el archivo de hello SSH certificado PEM y reemplazando /path/to/key.pem por ruta de acceso de Hola dónde ha almacenado Hola generan la clave SSH PEM.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-221">Passing hello SSH certificate .pem file and replacing /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5cd5f-222">siguientes comandos Hello se dividen una en varias líneas por motivos de claridad, pero debe especificar cada uno de ellos como una sola línea.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-222">hello following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
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
2. <span data-ttu-id="5cd5f-223">Cree dos más máquinas virtuales mediante la conexión de servicio en la nube mariadbha toohello.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-223">Create two more virtual machines by connecting them toohello mariadbha cloud service.</span></span> <span data-ttu-id="5cd5f-224">Cambiar el nombre de VM de Hola y Hola puerto tooa único puerto SSH no entra en conflicto con otras máquinas virtuales en Hola mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-224">Change hello VM name and hello SSH port tooa unique port not conflicting with other VMs in hello same cloud service.</span></span>

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
  <span data-ttu-id="5cd5f-225">Para MariaDB3:</span><span class="sxs-lookup"><span data-stu-id="5cd5f-225">For MariaDB3:</span></span>

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
3. <span data-ttu-id="5cd5f-226">Dirección IP tooget Hola interna de cada una de las máquinas virtuales de hello tres, necesitará para el paso siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="5cd5f-226">You will need tooget hello internal IP address of each of hello three VMs for hello next step:</span></span>

    ![Obtención de la dirección IP](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="5cd5f-228">Use toosign SSH en máquinas virtuales de toohello tres y editar el archivo de configuración de hello en cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-228">Use SSH toosign in toohello three VMs and edit hello configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="5cd5f-229">Quite  **`wsrep_cluster_name`**  y  **`wsrep_cluster_address`**  mediante la eliminación de hello  **#**  al principio de Hola de línea de saludo.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing hello **#** at hello beginning of hello line.</span></span>
    <span data-ttu-id="5cd5f-230">Además, reemplace  **`<ServerIP>`**  en  **`wsrep_node_address`**  y  **`<NodeName>`**  en  **`wsrep_node_name`**  con hello IP de la máquina virtual de direcciones y su nombre, respectivamente, y quite el comentario de dichas líneas así.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with hello VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="5cd5f-231">Iniciar el clúster de hello en MariaDB1 y permitir su ejecución en el inicio.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-231">Start hello cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="5cd5f-232">Inicie MySQL en MariaDB2 y MariaDB3 y deje que se ejecute en el inicio.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a><span data-ttu-id="5cd5f-233">Clúster de Hola de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="5cd5f-233">Load balance hello cluster</span></span>
<span data-ttu-id="5cd5f-234">Al crear máquinas virtuales de hello en clúster, se agrega en un conjunto de disponibilidad denominado clusteravset tooensure que se colocan en distintos dominios de error y actualización y que Azure no nunca mantenimiento en todos los equipos a la vez.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-234">When you created hello clustered VMs, you added them into an availability set called clusteravset tooensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="5cd5f-235">Esta configuración cumple los requisitos de hello toobe admite Hola contrato de nivel de servicio de Azure (SLA).</span><span class="sxs-lookup"><span data-stu-id="5cd5f-235">This configuration meets hello requirements toobe supported by hello Azure service level agreement (SLA).</span></span>

<span data-ttu-id="5cd5f-236">Ahora use las solicitudes de toobalance de equilibrador de carga de Azure entre tres nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-236">Now use Azure Load Balancer toobalance requests between hello three nodes.</span></span>

<span data-ttu-id="5cd5f-237">Ejecute hello siga los comandos en su equipo mediante el uso de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-237">Run hello following commands on your machine by using hello Azure CLI.</span></span>

<span data-ttu-id="5cd5f-238">estructura de parámetros de comando de Hello es:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="5cd5f-238">hello command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="5cd5f-239">Hola CLI establece a Hola carga equilibrador sondeo intervalo too15 segundos, lo que pueden resultar un poco demasiado largos.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-239">hello CLI sets hello load balancer probe interval too15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="5cd5f-240">Cambiar en el portal de hello en **extremos** para cualquiera de las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-240">Change it in hello portal under **Endpoints** for any of hello VMs.</span></span>

![Edición del extremo](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="5cd5f-242">Seleccione **Hola Reconfigure Load-Balanced establecer**.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-242">Select **Reconfigure hello Load-Balanced Set**.</span></span>

![Volver a configurar Equilibrio de carga de hello conjunto](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="5cd5f-244">Cambio **intervalo de sondeo** too5 segundos y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-244">Change **Probe Interval** too5 seconds and save your changes.</span></span>

![Cambio del intervalo de sondeo](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a><span data-ttu-id="5cd5f-246">Validar clúster Hola</span><span class="sxs-lookup"><span data-stu-id="5cd5f-246">Validate hello cluster</span></span>
<span data-ttu-id="5cd5f-247">se realiza el trabajo duro Hola.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-247">hello hard work is done.</span></span> <span data-ttu-id="5cd5f-248">clúster de Hello ahora debería estar accesible en `mariadbha.cloudapp.net:3306`, que alcanza el equilibrador de carga de Hola y enrutar las solicitudes entre Hola tres máquinas virtuales de forma perfecta y eficaz.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-248">hello cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits hello load balancer and route requests between hello three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="5cd5f-249">Use los favoritos tooconnect de cliente de MySQL, o conéctese desde uno de hello tooverify de máquinas virtuales que funciona este clúster.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-249">Use your favorite MySQL client tooconnect, or connect from one of hello VMs tooverify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="5cd5f-250">A continuación, cree una base de datos y rellénela con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="5cd5f-251">base de datos de Hello creó devuelve hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="5cd5f-251">hello database you created returns hello following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="5cd5f-252">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5cd5f-252">Next steps</span></span>
<span data-ttu-id="5cd5f-253">En este artículo, creó un clúster MariaDB+Galera de alta disponibilidad de tres nodos en Azure Virtual Machines con CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="5cd5f-254">máquinas virtuales de Hello son carga equilibrada con el equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd5f-254">hello VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="5cd5f-255">Es recomendable toolook en [toocluster de otra manera MySQL en Linux](mysql-cluster.md) y formas demasiado[optimizar y probar el rendimiento de MySQL en máquinas virtuales de Linux de Azure](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="5cd5f-255">You might want toolook at [another way toocluster MySQL on Linux](mysql-cluster.md) and ways too[optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[crear una clave SSH para la autenticación]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
