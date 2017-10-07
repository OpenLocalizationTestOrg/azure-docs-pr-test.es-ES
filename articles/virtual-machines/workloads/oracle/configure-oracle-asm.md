---
title: "aaaSet de ASM de Oracle en una máquina virtual de Linux de Azure | Documentos de Microsoft"
description: "Ponga en funcionamiento rápidamente ASM de Oracle en el entorno de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="66ae2-103">Configuración de ASM de Oracle en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="66ae2-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="66ae2-104">Las máquinas virtuales de Azure proporcionan un entorno informático completamente configurable y flexible.</span><span class="sxs-lookup"><span data-stu-id="66ae2-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="66ae2-105">Este tutorial trata la implementación de máquina virtual de Azure básico combinada con la instalación de Hola y configuración de Oracle Automated Storage Management (ASM).</span><span class="sxs-lookup"><span data-stu-id="66ae2-105">This tutorial covers basic Azure virtual machine deployment combined with hello installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="66ae2-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="66ae2-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="66ae2-107">Crear y conectar tooan VM de base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="66ae2-107">Create and connect tooan Oracle Database VM</span></span>
> * <span data-ttu-id="66ae2-108">Instalar y configurar Automated Storage Management de Oracle</span><span class="sxs-lookup"><span data-stu-id="66ae2-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="66ae2-109">Instalar y configurar la infraestructura Grid de Oracle</span><span class="sxs-lookup"><span data-stu-id="66ae2-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="66ae2-110">Inicializar una instalación de ASM de Oracle</span><span class="sxs-lookup"><span data-stu-id="66ae2-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="66ae2-111">Crear una base de datos de Oracle administrada por ASM</span><span class="sxs-lookup"><span data-stu-id="66ae2-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="66ae2-112">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="66ae2-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="66ae2-113">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="66ae2-114">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="66ae2-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-hello-environment"></a><span data-ttu-id="66ae2-115">Preparar el entorno de Hola</span><span class="sxs-lookup"><span data-stu-id="66ae2-115">Prepare hello environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="66ae2-116">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="66ae2-116">Create a resource group</span></span>

<span data-ttu-id="66ae2-117">toocreate un grupo de recursos, utilice hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="66ae2-117">toocreate a resource group, use hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="66ae2-118">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="66ae2-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="66ae2-119">En este ejemplo, un grupo de recursos denominado *myResourceGroup* en hello *eastus* región.</span><span class="sxs-lookup"><span data-stu-id="66ae2-119">In this example, a resource group named *myResourceGroup* in hello *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="66ae2-120">Creación de una VM</span><span class="sxs-lookup"><span data-stu-id="66ae2-120">Create a VM</span></span>

<span data-ttu-id="66ae2-121">toocreate una máquina virtual basada en imagen de la base de datos de Oracle de Hola y configurar toouse Oracle ASM, usar hello [crear vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="66ae2-121">toocreate a virtual machine based on hello Oracle Database image and configure it toouse Oracle ASM, use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="66ae2-122">Hello en el ejemplo siguiente se crea una máquina virtual denominada myVM que tiene un tamaño de Standard_DS2_v2 con cuatro discos de datos adjuntos de 50 GB.</span><span class="sxs-lookup"><span data-stu-id="66ae2-122">hello following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="66ae2-123">Si no existe ya en la ubicación de la clave predeterminada Hola, también crea claves SSH.</span><span class="sxs-lookup"><span data-stu-id="66ae2-123">If they do not already exist in hello default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="66ae2-124">toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.</span><span class="sxs-lookup"><span data-stu-id="66ae2-124">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="66ae2-125">Después de crear Hola VM, CLI de Azure muestra información toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="66ae2-125">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="66ae2-126">Tenga en cuenta el valor de Hola para `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-126">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="66ae2-127">Utilice este hello tooaccess de dirección virtual.</span><span class="sxs-lookup"><span data-stu-id="66ae2-127">You use this address tooaccess hello VM.</span></span>

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a><span data-ttu-id="66ae2-128">Conectar toohello VM</span><span class="sxs-lookup"><span data-stu-id="66ae2-128">Connect toohello VM</span></span>

<span data-ttu-id="66ae2-129">toocreate una sesión SSH con Hola VM y configurar opciones adicionales, use Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="66ae2-129">toocreate an SSH session with hello VM and configure additional settings, use hello following command.</span></span> <span data-ttu-id="66ae2-130">Reemplace la dirección IP de hello con hello `publicIpAddress` valor para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="66ae2-130">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="66ae2-131">Instalación de ASM de Oracle</span><span class="sxs-lookup"><span data-stu-id="66ae2-131">Install Oracle ASM</span></span>

<span data-ttu-id="66ae2-132">tooinstall Oracle ASM, Hola completa pasos.</span><span class="sxs-lookup"><span data-stu-id="66ae2-132">tooinstall Oracle ASM, complete hello following steps.</span></span> 

<span data-ttu-id="66ae2-133">Para más información sobre cómo instalar ASM de Oracle, consulte [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html) (Descargas de Oracle ASMLib para Oracle Linux 6).</span><span class="sxs-lookup"><span data-stu-id="66ae2-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="66ae2-134">Necesita toologin como raíz en orden toocontinue con la instalación de ASM:</span><span class="sxs-lookup"><span data-stu-id="66ae2-134">You need toologin as root in order toocontinue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="66ae2-135">Ejecute estos comandos adicionales tooinstall componentes de ASM de Oracle:</span><span class="sxs-lookup"><span data-stu-id="66ae2-135">Run these additional commands tooinstall Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="66ae2-136">Compruebe que ASM de Oracle esté instalado:</span><span class="sxs-lookup"><span data-stu-id="66ae2-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="66ae2-137">salida de Hello de este comando debería incluir Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="66ae2-137">hello output of this command should list hello following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="66ae2-138">ASM requiere determinados usuarios y roles en orden toofunction correctamente.</span><span class="sxs-lookup"><span data-stu-id="66ae2-138">ASM requires specific users and roles in order toofunction correctly.</span></span> <span data-ttu-id="66ae2-139">Hola, siga los comandos crea grupos y cuentas de usuario son un requisito previo de hello:</span><span class="sxs-lookup"><span data-stu-id="66ae2-139">hello following commands create hello pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="66ae2-140">Compruebe que los usuarios y grupos se han creado correctamente:</span><span class="sxs-lookup"><span data-stu-id="66ae2-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="66ae2-141">Hello salida de este comando debería incluir siguiente Hola usuarios y grupos:</span><span class="sxs-lookup"><span data-stu-id="66ae2-141">hello output of this command should list hello following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="66ae2-142">Cree una carpeta para el usuario *cuadrícula* y cambiar el propietario de hello:</span><span class="sxs-lookup"><span data-stu-id="66ae2-142">Create a folder for user *grid* and change hello owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="66ae2-143">Configuración de ASM de Oracle</span><span class="sxs-lookup"><span data-stu-id="66ae2-143">Set up Oracle ASM</span></span>

<span data-ttu-id="66ae2-144">Para este tutorial, es el usuario predeterminado de hello *cuadrícula* y el grupo predeterminado de hello es *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="66ae2-144">For this tutorial, hello default user is *grid* and hello default group is *asmadmin*.</span></span> <span data-ttu-id="66ae2-145">Asegúrese de que hello *oracle* usuario forma parte del grupo de asmadmin Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-145">Ensure that hello *oracle* user is part of hello asmadmin group.</span></span> <span data-ttu-id="66ae2-146">tooset en la instalación de Oracle ASM completa Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="66ae2-146">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="66ae2-147">Configuración de controlador de biblioteca de Oracle ASM Hola implica definir usuario predeterminado de hello (cuadrícula) y el grupo predeterminado (asmadmin), así como configurar hello toostart de unidad de arranque (elegir y) y tooscan para los discos de arranque (elegir y).</span><span class="sxs-lookup"><span data-stu-id="66ae2-147">Setting up hello Oracle ASM library driver involves defining hello default user (grid) and default group (asmadmin) as well as configuring hello drive toostart on boot (choose y) and tooscan for disks on boot (choose y).</span></span> <span data-ttu-id="66ae2-148">Necesita tooanswer Hola mensajes de Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="66ae2-148">You need tooanswer hello prompts from hello following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="66ae2-149">salida de Hello de este comando debe ser similar toohello siguiendo, detener con toobe preguntas respondida.</span><span class="sxs-lookup"><span data-stu-id="66ae2-149">hello output of this command should look similar toohello following, stopping with prompts toobe answered.</span></span>

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="66ae2-150">Configuración de disco de Hola de vista:</span><span class="sxs-lookup"><span data-stu-id="66ae2-150">View hello disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="66ae2-151">salida de Hello de este comando debe tener un aspecto similar toohello después de la lista de discos disponibles</span><span class="sxs-lookup"><span data-stu-id="66ae2-151">hello output of this command should look similar toohello following listing of available disks</span></span>

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. <span data-ttu-id="66ae2-152">Dar formato al disco */dev/sdc* ejecutando Hola siguiente comando y responder a Hola mensajes con:</span><span class="sxs-lookup"><span data-stu-id="66ae2-152">Format disk */dev/sdc* by running hello following command and answering hello prompts with:</span></span>
   - <span data-ttu-id="66ae2-153">*n* para la nueva partición</span><span class="sxs-lookup"><span data-stu-id="66ae2-153">*n* for new partition</span></span>
   - <span data-ttu-id="66ae2-154">*p* para la partición principal</span><span class="sxs-lookup"><span data-stu-id="66ae2-154">*p* for primary partition</span></span>
   - <span data-ttu-id="66ae2-155">*1* primera partición de tooselect Hola</span><span class="sxs-lookup"><span data-stu-id="66ae2-155">*1* tooselect hello first partition</span></span>
   - <span data-ttu-id="66ae2-156">Presione `enter` para el primer cilindro de saludo predeterminado</span><span class="sxs-lookup"><span data-stu-id="66ae2-156">press `enter` for hello default first cylinder</span></span>
   - <span data-ttu-id="66ae2-157">Presione `enter` para último cilindro de saludo predeterminado</span><span class="sxs-lookup"><span data-stu-id="66ae2-157">press `enter` for hello default last cylinder</span></span>
   - <span data-ttu-id="66ae2-158">Presione *w* tabla de particiones de toowrite Hola cambios toohello</span><span class="sxs-lookup"><span data-stu-id="66ae2-158">press *w* toowrite hello changes toohello partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="66ae2-159">Con las respuestas de hello proporcionadas anteriormente, salida de hello para el comando de fdisk Hola debería ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="66ae2-159">Using hello answers provided above, hello output for hello fdisk command should look like hello following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="66ae2-160">Hola repetición anterior comando fdisk para `/dev/sdd`, `/dev/sde`, y `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-160">Repeat hello preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="66ae2-161">Compruebe la configuración de disco de hello:</span><span class="sxs-lookup"><span data-stu-id="66ae2-161">Check hello disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="66ae2-162">salida de Hello de comando hello debería ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="66ae2-162">hello output of hello command should look like hello following:</span></span>

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. <span data-ttu-id="66ae2-163">Comprobar estado del servicio de Oracle ASM Hola e iniciar servicio de Oracle ASM de hello:</span><span class="sxs-lookup"><span data-stu-id="66ae2-163">Check hello Oracle ASM service status and start hello Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="66ae2-164">salida de Hello de comando hello debería ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="66ae2-164">hello output of hello command should look like hello following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="66ae2-165">Cree discos de ASM de Oracle:</span><span class="sxs-lookup"><span data-stu-id="66ae2-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="66ae2-166">salida de Hello de comando hello debería ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="66ae2-166">hello output of hello command should look like hello following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="66ae2-167">Enumere discos de ASM de Oracle:</span><span class="sxs-lookup"><span data-stu-id="66ae2-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="66ae2-168">salida de Hello de comando hello debería incluir desactivar Hola siguientes discos ASM de Oracle:</span><span class="sxs-lookup"><span data-stu-id="66ae2-168">hello output of hello command should list off hello following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="66ae2-169">Cambiar las contraseñas de Hola para los usuarios de raíz, oracle y cuadrícula de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-169">Change hello passwords for hello root, oracle, and grid users.</span></span> <span data-ttu-id="66ae2-170">**Tome nota de estas nuevas contraseñas** que se utilizan más adelante durante la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-170">**Make note of these new passwords** as you are using them later during hello installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="66ae2-171">Cambiar los permisos de carpeta de hello:</span><span class="sxs-lookup"><span data-stu-id="66ae2-171">Change hello folder permission:</span></span>

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="66ae2-172">Descarga y preparación de Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="66ae2-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="66ae2-173">toodownload y preparar el software de infraestructura de red de Oracle hello, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="66ae2-173">toodownload and prepare hello Oracle Grid Infrastructure software, complete hello following steps:</span></span>

1. <span data-ttu-id="66ae2-174">Descargar la infraestructura de red de Oracle de hello [página de descarga de Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="66ae2-174">Download Oracle Grid Infrastructure from hello [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="66ae2-175">En descargar Hola titulada **Oracle Database 12C Release 1 cuadrícula infraestructura (12.1.0.2.0) para Linux x86-64**, descargue los archivos .zip Hola dos.</span><span class="sxs-lookup"><span data-stu-id="66ae2-175">Under hello download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download hello two .zip files.</span></span>

2. <span data-ttu-id="66ae2-176">Después de descargar el equipo cliente tooyour de hello .zip archivos, puede usar el protocolo de copia seguro (SCP) toocopy Hola archivos tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="66ae2-176">After you download hello .zip files tooyour client computer, you can use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="66ae2-177">SSH nuevamente en la máquina virtual de Oracle en Azure en archivos de .zip de orden toomove hello en hello / opt carpeta.</span><span class="sxs-lookup"><span data-stu-id="66ae2-177">SSH back into your Oracle VM in Azure in order toomove hello .zip files into hello /opt folder.</span></span> <span data-ttu-id="66ae2-178">A continuación, cambie el propietario de Hola de archivos de hello:</span><span class="sxs-lookup"><span data-stu-id="66ae2-178">Then, change hello owner of hello files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="66ae2-179">Descomprimir archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-179">Unzip hello files.</span></span> <span data-ttu-id="66ae2-180">(Instalación Hola Linux descomprima herramienta si aún no está instalado).</span><span class="sxs-lookup"><span data-stu-id="66ae2-180">(Install hello Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="66ae2-181">Cambie el permiso:</span><span class="sxs-lookup"><span data-stu-id="66ae2-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="66ae2-182">Actualice el espacio de intercambio configurado.</span><span class="sxs-lookup"><span data-stu-id="66ae2-182">Update configured swap space.</span></span> <span data-ttu-id="66ae2-183">Componentes de la cuadrícula de Oracle necesitan al menos 6.8 GB de espacio de intercambio tooinstall cuadrícula.</span><span class="sxs-lookup"><span data-stu-id="66ae2-183">Oracle Grid components need at least 6.8 GB of swap space tooinstall Grid.</span></span> <span data-ttu-id="66ae2-184">tamaño de archivo de intercambio de Hello predeterminado para las imágenes de Oracle Linux en Azure es solo de 2048MB.</span><span class="sxs-lookup"><span data-stu-id="66ae2-184">hello default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="66ae2-185">Necesita tooincrease `ResourceDisk.SwapSizeMB` en hello `/etc/waagent.conf` archivo y reinicie el servicio de WALinuxAgent de hello en orden para hello actualizar configuración tootake efecto.</span><span class="sxs-lookup"><span data-stu-id="66ae2-185">You need tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` file and restart hello WALinuxAgent service in order for hello updated settings tootake effect.</span></span> <span data-ttu-id="66ae2-186">Dado que es un archivo de solo lectura, necesita acceso de escritura de tooenable de permisos de archivo de toochange.</span><span class="sxs-lookup"><span data-stu-id="66ae2-186">Because it is a read-only file, you need toochange file permissions tooenable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="66ae2-187">Busque `ResourceDisk.SwapSizeMB` y cambie el valor de hello demasiado**8192**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-187">Search for `ResourceDisk.SwapSizeMB` and change hello value too**8192**.</span></span> <span data-ttu-id="66ae2-188">Necesitará toopress `insert` tooenter modo de inserción, tipo de valor de Hola de **8192** y, a continuación, presione `esc` tooreturn toocommand modo.</span><span class="sxs-lookup"><span data-stu-id="66ae2-188">You will need toopress `insert` tooenter insert mode, type in hello value of **8192** and then press `esc` tooreturn toocommand mode.</span></span> <span data-ttu-id="66ae2-189">cambios de hello toowrite y archivo de hello quit, escriba `:wq` y presione `enter`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-189">toowrite hello changes and quit hello file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="66ae2-190">Se recomienda usar siempre `WALinuxAgent` tooconfigure espacio de intercambio para que siempre se crea en Hola efímero disco local (disco temporal) para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="66ae2-190">We highly recommend that you always use `WALinuxAgent` tooconfigure swap space so that it's always created on hello local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="66ae2-191">Para obtener más información sobre, consulte [cómo tooadd un intercambio de archivos de máquinas virtuales de Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="66ae2-191">For more information on, see [How tooadd a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a><span data-ttu-id="66ae2-192">Preparar el cliente local y la máquina virtual toorun x11</span><span class="sxs-lookup"><span data-stu-id="66ae2-192">Prepare your local client and VM toorun x11</span></span>
<span data-ttu-id="66ae2-193">Configuración de Oracle ASM requiere una interfaz gráfica toocomplete Hola instalación y configuración.</span><span class="sxs-lookup"><span data-stu-id="66ae2-193">Configuring Oracle ASM requires a graphical interface toocomplete hello install and configuration.</span></span> <span data-ttu-id="66ae2-194">Estamos usando hello x11 protocolo toofacilitate esta instalación.</span><span class="sxs-lookup"><span data-stu-id="66ae2-194">We are using hello x11 protocol toofacilitate this installation.</span></span> <span data-ttu-id="66ae2-195">Si usas un sistema de cliente (Mac o Linux) que ya tiene X11 capacidades habilitada y configurada: puede omitir esta configuración y configurar máquinas de tooWindows exclusivo.</span><span class="sxs-lookup"><span data-stu-id="66ae2-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive tooWindows machines.</span></span> 

1. <span data-ttu-id="66ae2-196">[Descargar PuTTY](http://www.putty.org/) y [descargar Xming](https://xming.en.softonic.com/) tooyour equipo de Windows.</span><span class="sxs-lookup"><span data-stu-id="66ae2-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) tooyour Windows computer.</span></span> <span data-ttu-id="66ae2-197">Necesitará la instalación de hello toocomplete de ambas de estas aplicaciones con los valores predeterminados de hello antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="66ae2-197">You will need toocomplete hello installation of both of these applications with hello default values before proceeding.</span></span>

2. <span data-ttu-id="66ae2-198">Después de instalar PuTTY, abra un símbolo del sistema, cambie a Hola PuTTY carpeta (por ejemplo, C:\Program Files\PuTTY) y ejecutar `puttygen.exe` en orden toogenerate una clave.</span><span class="sxs-lookup"><span data-stu-id="66ae2-198">After you install PuTTY, open a command prompt, change into hello PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order toogenerate a key.</span></span>

3. <span data-ttu-id="66ae2-199">En PuTTY Key Generator:</span><span class="sxs-lookup"><span data-stu-id="66ae2-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="66ae2-200">Generar una clave seleccionando hello `Generate` botón.</span><span class="sxs-lookup"><span data-stu-id="66ae2-200">Generate a key by selecting hello `Generate` button.</span></span>
   2. <span data-ttu-id="66ae2-201">Copie el contenido de Hola de clave de hello (Ctrl + C).</span><span class="sxs-lookup"><span data-stu-id="66ae2-201">Copy hello contents of hello key (Ctrl+C).</span></span>
   3. <span data-ttu-id="66ae2-202">Seleccione hello `Save private key` botón.</span><span class="sxs-lookup"><span data-stu-id="66ae2-202">Select hello `Save private key` button.</span></span>
   4. <span data-ttu-id="66ae2-203">Omitir la advertencia Hola sobre la protección de clave de hello con una frase de contraseña y, a continuación, seleccione `OK`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-203">Ignore hello warning about securing hello key with a passphrase, and then select `OK`.</span></span>

   ![Captura de pantalla de PuTTY Key Generator](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="66ae2-205">En la máquina virtual, ejecute estos comandos:</span><span class="sxs-lookup"><span data-stu-id="66ae2-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="66ae2-206">Cree un archivo llamado `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="66ae2-207">Pegar contenido de Hola de clave de hello en este archivo y, a continuación, guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="66ae2-207">Paste hello contents of hello key in this file, and then save hello file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="66ae2-208">clave de Hello debe contener la cadena de hello `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-208">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="66ae2-209">Además, el contenido de Hola de clave de hello debe ser una sola línea de texto.</span><span class="sxs-lookup"><span data-stu-id="66ae2-209">Also, hello contents of hello key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="66ae2-210">En el sistema cliente, inicie PuTTY.</span><span class="sxs-lookup"><span data-stu-id="66ae2-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="66ae2-211">Hola **categoría** panel, vaya demasiado**conexión** > **SSH** > **Auth**. Hola **archivo de clave privada para la autenticación** cuadro, busque la clave de toohello que ha generado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="66ae2-211">In hello **Category** pane, go too**Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

   ![Captura de pantalla de opciones de autenticación de SSH de Hola](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="66ae2-213">Hola **categoría** panel, vaya demasiado**conexión** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-213">In hello **Category** pane, go too**Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="66ae2-214">Seleccione hello **X11 de habilitar el reenvío** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="66ae2-214">Select hello **Enable X11 forwarding** check box.</span></span>

   ![Captura de pantalla de hello SSH X11 opciones de reenvío](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="66ae2-216">Hola **categoría** panel, vaya demasiado**sesión**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-216">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="66ae2-217">Escriba la máquina virtual de ASM de Oracle `<publicIPaddress>` en el cuadro de diálogo de nombre de host de hello rellene un nuevo `Saved Session` asigne un nombre y, a continuación, haga clic en `Save`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-217">Enter your Oracle ASM VM `<publicIPaddress>` in hello host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="66ae2-218">Una vez guardado, haga clic en `open` tooconnect tooyour Oracle ASM virtual machine.</span><span class="sxs-lookup"><span data-stu-id="66ae2-218">Once saved, click on `open` tooconnect tooyour Oracle ASM virtual machine.</span></span>  <span data-ttu-id="66ae2-219">Hola primera vez que se conecte también le advertirá de sistema remoto hello no se almacena en caché en el registro.</span><span class="sxs-lookup"><span data-stu-id="66ae2-219">hello first time you connect you are warned  hello remote system is not cached in your registry.</span></span> <span data-ttu-id="66ae2-220">Haga clic en `yes` tooadd lo y continuar.</span><span class="sxs-lookup"><span data-stu-id="66ae2-220">Click on `yes` tooadd it and continue.</span></span>

   ![Captura de pantalla de opciones de sesión de PuTTY Hola](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="66ae2-222">Instalación de Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="66ae2-222">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="66ae2-223">tooinstall infraestructura de red de Oracle, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="66ae2-223">tooinstall Oracle Grid Infrastructure, complete hello following steps:</span></span>

1. <span data-ttu-id="66ae2-224">Inicie sesión como **grid**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-224">Sign in as **grid**.</span></span> <span data-ttu-id="66ae2-225">(Debe ser capaz de toosign en sin que se solicite una contraseña).</span><span class="sxs-lookup"><span data-stu-id="66ae2-225">(You should be able toosign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="66ae2-226">Si está ejecutando Windows, asegúrese de que ha iniciado la Xming antes de comenzar la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-226">If you are running Windows, make sure you have started Xming before you begin hello installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="66ae2-227">Se abre el instalador de Oracle Grid Infrastructure 12c versión 1.</span><span class="sxs-lookup"><span data-stu-id="66ae2-227">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="66ae2-228">(Puede tardar unos minutos para hello instalador toostart.)</span><span class="sxs-lookup"><span data-stu-id="66ae2-228">(It might take a few minutes for hello  installer toostart.)</span></span>

2. <span data-ttu-id="66ae2-229">En hello **seleccione la opción de instalación** , seleccione **instalar y configurar la infraestructura de red de Oracle para un servidor independiente**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-229">On hello **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Captura de pantalla de la página de seleccionar la opción de instalación del instalador de Hola](./media/oracle-asm/install01.png)

3. <span data-ttu-id="66ae2-231">En hello **seleccionar idiomas de producto** página, asegúrese de **inglés** o se selecciona Hola idioma que desee.</span><span class="sxs-lookup"><span data-stu-id="66ae2-231">On hello **Select Product Languages** page, ensure **English** or hello language that you want is selected.</span></span>  <span data-ttu-id="66ae2-232">Haga clic en `next`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-232">Click `next`.</span></span>

4. <span data-ttu-id="66ae2-233">En hello **crear grupo de discos ASM** página:</span><span class="sxs-lookup"><span data-stu-id="66ae2-233">On hello **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="66ae2-234">Escriba un nombre para el grupo de discos de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-234">Enter a name for hello disk group.</span></span>
   - <span data-ttu-id="66ae2-235">En **Redundancy** (Redundancia), seleccione **External** (Externa).</span><span class="sxs-lookup"><span data-stu-id="66ae2-235">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="66ae2-236">En **Allocation Unit Size** (Tamaño de la unidad de asignación), seleccione **4**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-236">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="66ae2-237">En **Add Disks** (Agregar discos), seleccione **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-237">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="66ae2-238">Haga clic en `next`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-238">Click `next`.</span></span>

5. <span data-ttu-id="66ae2-239">En hello **especificar la contraseña de ASM** página, seleccione hello **Use las mismas contraseñas para estas cuentas** opción y escriba una contraseña.</span><span class="sxs-lookup"><span data-stu-id="66ae2-239">On hello **Specify ASM Password** page, select hello **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Captura de pantalla de página de especificar la contraseña de ASM del instalador de Hola](./media/oracle-asm/install04.png)

6. <span data-ttu-id="66ae2-241">En hello **especificar opciones de administración** página, tienen Hola opción tooconfigure Control de EM en la nube.</span><span class="sxs-lookup"><span data-stu-id="66ae2-241">On hello **Specify Management Options** page, you have hello option tooconfigure EM Cloud Control.</span></span> <span data-ttu-id="66ae2-242">Se va a omitir esta opción, haga clic `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="66ae2-242">We are skipping this option - click `next` toocontinue.</span></span> 

7. <span data-ttu-id="66ae2-243">En hello **grupos con privilegios de sistema operativo** , utilice la configuración predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-243">On hello **Privileged Operating System Groups** page, use hello default settings.</span></span> <span data-ttu-id="66ae2-244">Haga clic en `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="66ae2-244">Click `next` toocontinue.</span></span>

8. <span data-ttu-id="66ae2-245">En hello **especificar la ubicación de instalación** , utilice la configuración predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-245">On hello **Specify Installation Location** page, use hello default settings.</span></span> <span data-ttu-id="66ae2-246">Haga clic en `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="66ae2-246">Click `next` toocontinue.</span></span>

9. <span data-ttu-id="66ae2-247">En hello **crear inventario** página, cambie Hola Directory inventario demasiado`/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-247">On hello **Create Inventory** page, change hello Inventory Directory too`/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="66ae2-248">Haga clic en `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="66ae2-248">Click `next` toocontinue.</span></span>

   ![Captura de pantalla de la página de inventario de crear del instalador de Hola](./media/oracle-asm/install08.png)

10. <span data-ttu-id="66ae2-250">En hello **configuración de ejecución de secuencia de comandos de raíz** página, seleccione hello **ejecutar automáticamente los scripts de configuración** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="66ae2-250">On hello **Root script execution configuration** page, select hello **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="66ae2-251">A continuación, seleccione hello **usar credenciales de usuario de "root"** opción y escriba la contraseña de usuario de hello raíz.</span><span class="sxs-lookup"><span data-stu-id="66ae2-251">Then, select hello **Use "root" user credential** option, and enter hello root user password.</span></span>

    ![Captura de pantalla de la página de configuración de ejecución de secuencia de comandos del instalador de hello raíz](./media/oracle-asm/install09.png)

11. <span data-ttu-id="66ae2-253">En hello **realizar comprobaciones de requisitos previos** página, el programa de instalación actual de hello producirá errores.</span><span class="sxs-lookup"><span data-stu-id="66ae2-253">On hello **Perform Prerequisite Checks** page, hello current setup will fail with errors.</span></span> <span data-ttu-id="66ae2-254">Este es un comportamiento esperado.</span><span class="sxs-lookup"><span data-stu-id="66ae2-254">This is an expected behavior.</span></span> <span data-ttu-id="66ae2-255">Seleccione `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-255">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="66ae2-256">Hola **Script de corrección** cuadro de diálogo, haga clic en `OK`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-256">In hello **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="66ae2-257">En hello **resumen** página, revise la configuración seleccionada y, a continuación, haga clic en `Install`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-257">On hello **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Captura de pantalla de la página de resumen del instalador de Hola](./media/oracle-asm/install12.png)

14. <span data-ttu-id="66ae2-259">Aparece un cuadro de diálogo de advertencia que le informa de los scripts de configuración necesario toobe que se ejecute como un usuario con privilegios.</span><span class="sxs-lookup"><span data-stu-id="66ae2-259">A warning dialog box appears informing you configuration scripts need toobe run as a privileged user.</span></span> <span data-ttu-id="66ae2-260">Haga clic en `Yes` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="66ae2-260">Click `Yes` toocontinue.</span></span>

15. <span data-ttu-id="66ae2-261">En hello **finalizar** página, haga clic en `Close` instalación de hello toofinish.</span><span class="sxs-lookup"><span data-stu-id="66ae2-261">On hello **Finish** page, click `Close` toofinish hello installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="66ae2-262">Configuración de la instalación de ASM de Oracle</span><span class="sxs-lookup"><span data-stu-id="66ae2-262">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="66ae2-263">tooset en la instalación de Oracle ASM completa Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="66ae2-263">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="66ae2-264">Asegúrese de que sigue conectado como **grid** desde su sesión de X11.</span><span class="sxs-lookup"><span data-stu-id="66ae2-264">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="66ae2-265">Es posible que tenga toohit `enter` toorevive Hola terminal.</span><span class="sxs-lookup"><span data-stu-id="66ae2-265">You might need toohit `enter` toorevive hello terminal.</span></span> <span data-ttu-id="66ae2-266">A continuación, inicie Hola Oracle Automated Storage Management Asistente para la configuración:</span><span class="sxs-lookup"><span data-stu-id="66ae2-266">Then launch hello Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="66ae2-267">Se abre el asistente para la configuración de ASM de Oracle.</span><span class="sxs-lookup"><span data-stu-id="66ae2-267">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="66ae2-268">Hola **configurar ASM: grupos de discos** diálogo cuadro, haga clic en hello `Create` botón y, a continuación, haga clic en `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-268">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="66ae2-269">Hola **crear grupo de discos** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="66ae2-269">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="66ae2-270">Escriba el nombre de grupo del disco de hello **datos**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-270">Enter hello disk group name **DATA**.</span></span>
   - <span data-ttu-id="66ae2-271">En **Select Member Disks** (Seleccionar discos miembro), seleccione **ORCL_DATA** y **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-271">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="66ae2-272">En **Allocation Unit Size** (Tamaño de la unidad de asignación), seleccione **4**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-272">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="66ae2-273">Haga clic en `ok` grupo de discos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-273">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="66ae2-274">Haga clic en `ok` ventana de confirmación de tooclose Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-274">Click `ok` tooclose hello confirmation window.</span></span>

   ![Captura de pantalla del cuadro de diálogo Crear grupo de discos de Hola](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="66ae2-276">Hola **configurar ASM: grupos de discos** diálogo cuadro, haga clic en hello `Create` botón y, a continuación, haga clic en `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-276">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="66ae2-277">Hola **crear grupo de discos** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="66ae2-277">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="66ae2-278">Escriba el nombre de grupo del disco de hello **FRA**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-278">Enter hello disk group name **FRA**.</span></span>
   - <span data-ttu-id="66ae2-279">En **Redundancy** (Redundancia), seleccione **External (none)** (Externa [ninguna]).</span><span class="sxs-lookup"><span data-stu-id="66ae2-279">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="66ae2-280">En **Select Member Disks** (Seleccionar discos miembro), seleccione **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-280">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="66ae2-281">En **Allocation Unit Size** (Tamaño de la unidad de asignación), seleccione **4**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-281">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="66ae2-282">Haga clic en `ok` grupo de discos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-282">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="66ae2-283">Haga clic en `ok` ventana de confirmación de tooclose Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-283">Click `ok` tooclose hello confirmation window.</span></span>

   ![Captura de pantalla del cuadro de diálogo Crear grupo de discos de Hola](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="66ae2-285">Seleccione **Exit** tooclose Asistente para la configuración de ASM.</span><span class="sxs-lookup"><span data-stu-id="66ae2-285">Select **Exit** tooclose ASM Configuration Assistant.</span></span>

   ![Captura de pantalla de Hola configurar ASM: cuadro de diálogo de grupos de discos con botón Salir](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a><span data-ttu-id="66ae2-287">Crear base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="66ae2-287">Create hello database</span></span>

<span data-ttu-id="66ae2-288">Hola software de base de datos de Oracle ya está instalado en la imagen de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="66ae2-288">hello Oracle database software is already installed on hello Azure Marketplace image.</span></span> <span data-ttu-id="66ae2-289">toocreate una base de datos completa Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="66ae2-289">toocreate a database, complete hello following steps:</span></span>

1. <span data-ttu-id="66ae2-290">Cambiar superusuario de Oracle toohello de los usuarios y, a continuación, inicializar el agente de escucha de hello para el registro:</span><span class="sxs-lookup"><span data-stu-id="66ae2-290">Switch users toohello Oracle superuser, and then initialize hello listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="66ae2-291">Se abre el asistente para la configuración de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="66ae2-291">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="66ae2-292">En hello **operación de base de datos** página, haga clic en `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-292">On hello **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="66ae2-293">En hello **modo de creación** página:</span><span class="sxs-lookup"><span data-stu-id="66ae2-293">On hello **Creation Mode** page:</span></span>

   - <span data-ttu-id="66ae2-294">Escriba un nombre para la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-294">Enter a name for hello database.</span></span>
   - <span data-ttu-id="66ae2-295">Para **Storage Type** (Tipo de almacenamiento), asegúrese de que **Automatic Storage Management (ASM)** está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="66ae2-295">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="66ae2-296">Para **ubicación de archivos de base de datos**, usar valor predeterminado de hello ASM sugiere la ubicación.</span><span class="sxs-lookup"><span data-stu-id="66ae2-296">For **Database Files Location**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="66ae2-297">Para **rápida recuperación área**, usar valor predeterminado de hello ASM sugiere la ubicación.</span><span class="sxs-lookup"><span data-stu-id="66ae2-297">For **Fast Recovery Area**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="66ae2-298">Escriba una **contraseña administrativa** y **confirme la contraseña**.</span><span class="sxs-lookup"><span data-stu-id="66ae2-298">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="66ae2-299">Asegúrese de que `create as container database` está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="66ae2-299">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="66ae2-300">Escriba un valor de `pluggable database name`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-300">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="66ae2-301">En hello **resumen** página, revise la configuración seleccionada y, a continuación, haga clic en `Finish` base de datos de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-301">On hello **Summary** page, review your selected settings, and then click `Finish` toocreate hello database.</span></span>

   ![Captura de pantalla de la página de resumen de Hola](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="66ae2-303">Hola base de datos se ha creado.</span><span class="sxs-lookup"><span data-stu-id="66ae2-303">hello Database has been created.</span></span> <span data-ttu-id="66ae2-304">En hello **finalizar** página, tienen Hola opción toounlock cuentas adicionales toouse esta base de datos y cambiar las contraseñas de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ae2-304">On hello **Finish** page, you have hello option toounlock additional accounts toouse this database and change hello passwords.</span></span> <span data-ttu-id="66ae2-305">Si lo desea, toodo, seleccione **administración de contraseñas** -en caso contrario, haga clic en `close`.</span><span class="sxs-lookup"><span data-stu-id="66ae2-305">If you wish toodo so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="66ae2-306">Eliminar Hola VM</span><span class="sxs-lookup"><span data-stu-id="66ae2-306">Delete hello VM</span></span>

<span data-ttu-id="66ae2-307">Oracle Automated Storage Management se ha configurado correctamente en la imagen de la base de datos de Oracle de Hola de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="66ae2-307">You have successfully configured Oracle Automated Storage Management on hello Oracle DB image from hello Azure Marketplace.</span></span>  <span data-ttu-id="66ae2-308">Cuando ya no necesita esta máquina virtual, puede usar Hola después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos:</span><span class="sxs-lookup"><span data-stu-id="66ae2-308">When you no longer need this VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="66ae2-309">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66ae2-309">Next steps</span></span>

[<span data-ttu-id="66ae2-310">Tutorial: Configuración de Oracle DataGuard</span><span class="sxs-lookup"><span data-stu-id="66ae2-310">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="66ae2-311">Tutorial: Configuración de Oracle GoldenGate</span><span class="sxs-lookup"><span data-stu-id="66ae2-311">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="66ae2-312">Revise [Diseño de una base de datos de Oracle](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="66ae2-312">Review [Architect an Oracle DB](oracle-design.md)</span></span>
