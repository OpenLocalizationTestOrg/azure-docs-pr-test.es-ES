---
title: aaaSet de MySQL en una VM de Linux en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall Hola MySQL de la pila en una máquina virtual de Linux (RedHat o Ubuntu familia SO) en Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a><span data-ttu-id="d5e57-103">¿Cómo tooinstall MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="d5e57-103">How tooinstall MySQL on Azure</span></span>
<span data-ttu-id="d5e57-104">En este artículo, aprenderá cómo tooinstall y configurar MySQL en una máquina virtual de Azure ejecutan Linux.</span><span class="sxs-lookup"><span data-stu-id="d5e57-104">In this article, you will learn how tooinstall and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="d5e57-105">Instalación de MySQL en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d5e57-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="d5e57-106">Ya debe tener una máquina virtual de Microsoft Azure ejecutan Linux en orden toocomplete este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d5e57-106">You must already have a Microsoft Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="d5e57-107">Vea la [tutorial de la máquina virtual de Linux de Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate y configurar una VM de Linux con `mysqlnode` como nombre de la máquina virtual de Hola y `azureuser` como usuario antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="d5e57-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate and set up a Linux VM with `mysqlnode` as hello VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="d5e57-108">En este caso, utilice puerto 3306 como Hola puerto de MySQL.</span><span class="sxs-lookup"><span data-stu-id="d5e57-108">In this case, use 3306 port as hello MySQL port.</span></span>  

<span data-ttu-id="d5e57-109">Conectar toohello VM de Linux que creó mediante putty.</span><span class="sxs-lookup"><span data-stu-id="d5e57-109">Connect toohello Linux VM you created via putty.</span></span> <span data-ttu-id="d5e57-110">Si se trata de hello primera vez que use la máquina virtual de Linux de Azure, vea cómo toouse putty conectarse tooa VM de Linux [aquí](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d5e57-110">If this is hello first time you use Azure Linux VM, see how toouse putty connect tooa Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d5e57-111">Usaremos repositorio paquete tooinstall MySQL5.6 como un ejemplo de este artículo.</span><span class="sxs-lookup"><span data-stu-id="d5e57-111">We will use repository package tooinstall MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="d5e57-112">En realidad, MySQL5.6 tiene un mejor rendimiento MySQL5.5.</span><span class="sxs-lookup"><span data-stu-id="d5e57-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="d5e57-113">Puede encontrar más información [aquí](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/):</span><span class="sxs-lookup"><span data-stu-id="d5e57-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-tooinstall-mysql56-on-ubuntu"></a><span data-ttu-id="d5e57-114">Cómo tooinstall MySQL5.6 en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d5e57-114">How tooinstall MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="d5e57-115">Usaremos aquí la máquina virtual de Linux con Ubuntu de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5e57-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="d5e57-116">Paso 1: Instalar un servidor MySQL 5.6 cambiar demasiado`root` usuario:</span><span class="sxs-lookup"><span data-stu-id="d5e57-116">Step 1: Install MySQL Server 5.6   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="d5e57-117">Instalación de mysql-server 5.6:</span><span class="sxs-lookup"><span data-stu-id="d5e57-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="d5e57-118">Durante la instalación, verá un poping de la ventana de cuadro de diálogo seguridad tooask se tooset MySQL raíz contraseña a continuación y se necesita establecer Hola contraseña aquí.</span><span class="sxs-lookup"><span data-stu-id="d5e57-118">During installation, you will see a dialog window poping up tooask you tooset MySQL root password below, and you need set hello password here.</span></span>
  
    ![imagen](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="d5e57-120">Contraseña de entrada hello tooconfirm de nuevo.</span><span class="sxs-lookup"><span data-stu-id="d5e57-120">Input hello password again tooconfirm.</span></span>

    ![imagen](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="d5e57-122">Paso 2: Iniciar sesión en el servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="d5e57-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="d5e57-123">Una vez finalizada la instalación del servidor MySQL, el servicio MySQL se inicia automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d5e57-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="d5e57-124">Puede iniciar sesión en el servidor MySQL con el usuario `root` .</span><span class="sxs-lookup"><span data-stu-id="d5e57-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="d5e57-125">Usar hello por debajo de la contraseña de toologin y entrada de comando.</span><span class="sxs-lookup"><span data-stu-id="d5e57-125">Use hello below command toologin and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="d5e57-126">Paso 3: Administrar Hola ejecutando el servicio MySQL</span><span class="sxs-lookup"><span data-stu-id="d5e57-126">Step 3: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="d5e57-127">(a) Obtener el estado del servicio MySQL</span><span class="sxs-lookup"><span data-stu-id="d5e57-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="d5e57-128">(b) Iniciar el servicio MySQL</span><span class="sxs-lookup"><span data-stu-id="d5e57-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="d5e57-129">(c) Detener el servicio MySQL</span><span class="sxs-lookup"><span data-stu-id="d5e57-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="d5e57-130">(d) reinicie el servicio de MySQL de Hola</span><span class="sxs-lookup"><span data-stu-id="d5e57-130">(d) Restart hello MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="d5e57-131">¿Cómo tooinstall MySQL en la familia de sistemas operativos de Red Hat que CentOS, Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="d5e57-131">How tooinstall MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="d5e57-132">Aquí usaremos la máquina virtual de Linux con CentOS u Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="d5e57-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="d5e57-133">Paso 1: Agregar Hola MySQL Yum repositorio conmutador demasiado`root` usuario:</span><span class="sxs-lookup"><span data-stu-id="d5e57-133">Step 1: Add hello MySQL Yum repository   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="d5e57-134">Descargue e instale el paquete de la versión de Hola MySQL:</span><span class="sxs-lookup"><span data-stu-id="d5e57-134">Download and install hello MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="d5e57-135">Paso 2: Editar por debajo del repositorio de archivos tooenable Hola MySQL para descargar el paquete de MySQL5.6 Hola.</span><span class="sxs-lookup"><span data-stu-id="d5e57-135">Step 2: Edit below file tooenable hello MySQL repository for downloading hello MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="d5e57-136">Actualice cada valor de este toobelow de archivo:</span><span class="sxs-lookup"><span data-stu-id="d5e57-136">Update each value of this file toobelow:</span></span>
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="d5e57-137">Paso 3: Instalación de MySQL desde el repositorio de MySQL Install MySQL:</span><span class="sxs-lookup"><span data-stu-id="d5e57-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="d5e57-138">Se instalará el paquete RPM MySQL y todos los paquetes relacionados.</span><span class="sxs-lookup"><span data-stu-id="d5e57-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="d5e57-139">Paso 4: Administrar Hola ejecutando el servicio MySQL</span><span class="sxs-lookup"><span data-stu-id="d5e57-139">Step 4: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="d5e57-140">(a) comprobar estado de servicio de Hola de servidor de MySQL de hello:</span><span class="sxs-lookup"><span data-stu-id="d5e57-140">(a) Check hello service status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="d5e57-141">(b) Compruebe si está ejecutando el servidor de puerto de MySQL de hello predeterminado:</span><span class="sxs-lookup"><span data-stu-id="d5e57-141">(b) Check whether hello default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="d5e57-142">(c) inicie Hola MySQL server:</span><span class="sxs-lookup"><span data-stu-id="d5e57-142">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="d5e57-143">(d) detener el servidor de MySQL de hello:</span><span class="sxs-lookup"><span data-stu-id="d5e57-143">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="d5e57-144">(e) establecer MySQL toostart cuando el arranque de sistema de hello:</span><span class="sxs-lookup"><span data-stu-id="d5e57-144">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a><span data-ttu-id="d5e57-145">¿Cómo tooinstall MySQL en SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="d5e57-145">How tooinstall MySQL on SUSE Linux</span></span>
<span data-ttu-id="d5e57-146">Aquí usaremos la máquina virtual de Linux con OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="d5e57-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="d5e57-147">Paso 1: Descargar e instalar el servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="d5e57-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="d5e57-148">Cambiar demasiado`root` usuario a través de comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="d5e57-148">Switch too`root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="d5e57-149">Descargar e instalar el paquete MySQL:</span><span class="sxs-lookup"><span data-stu-id="d5e57-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="d5e57-150">Paso 2: Administrar Hola ejecutando el servicio MySQL</span><span class="sxs-lookup"><span data-stu-id="d5e57-150">Step 2: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="d5e57-151">(a) comprobar estado de Hola de servidor de MySQL de hello:</span><span class="sxs-lookup"><span data-stu-id="d5e57-151">(a) Check hello status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="d5e57-152">(b) Compruebe si Hola puerto predeterminado del servidor de MySQL de hello:</span><span class="sxs-lookup"><span data-stu-id="d5e57-152">(b) Check whether hello default port of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="d5e57-153">(c) inicie Hola MySQL server:</span><span class="sxs-lookup"><span data-stu-id="d5e57-153">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="d5e57-154">(d) detener el servidor de MySQL de hello:</span><span class="sxs-lookup"><span data-stu-id="d5e57-154">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="d5e57-155">(e) establecer MySQL toostart cuando el arranque de sistema de hello:</span><span class="sxs-lookup"><span data-stu-id="d5e57-155">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="d5e57-156">siguiente paso</span><span class="sxs-lookup"><span data-stu-id="d5e57-156">Next Step</span></span>
<span data-ttu-id="d5e57-157">Buscar más información de uso y sobre MySQL [aquí](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="d5e57-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

