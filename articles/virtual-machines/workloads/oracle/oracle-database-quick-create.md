---
title: "aaaCreate una base de datos de Oracle en una máquina virtual de Azure | Documentos de Microsoft"
description: "Ponga en funcionamiento rápidamente una base de datos de Oracle Database 12c en el entorno de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="021b1-103">Creación de una base de datos Oracle en una VM de Azure</span><span class="sxs-lookup"><span data-stu-id="021b1-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="021b1-104">Esta guía se detalla con hello Azure CLI toodeploy una máquina virtual de Azure de hello [imagen de la Galería de Oracle marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) en orden toocreate una base de datos de Oracle 12C.</span><span class="sxs-lookup"><span data-stu-id="021b1-104">This guide details using hello Azure CLI toodeploy an Azure virtual machine from hello [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order toocreate an Oracle 12c database.</span></span> <span data-ttu-id="021b1-105">Una vez implementado el servidor de hello, se conectará a través de SSH en la base de datos de Oracle de orden tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="021b1-105">Once hello server is deployed, you will connect via SSH in order tooconfigure hello Oracle database.</span></span> 

<span data-ttu-id="021b1-106">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="021b1-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="021b1-107">Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="021b1-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="021b1-108">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="021b1-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="021b1-109">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="021b1-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="021b1-110">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="021b1-110">Create a resource group</span></span>

<span data-ttu-id="021b1-111">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="021b1-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="021b1-112">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="021b1-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="021b1-113">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.</span><span class="sxs-lookup"><span data-stu-id="021b1-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="021b1-114">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="021b1-114">Create virtual machine</span></span>

<span data-ttu-id="021b1-115">toocreate una máquina virtual (VM), usar hello [crear vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="021b1-115">toocreate a virtual machine (VM), use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="021b1-116">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM`.</span><span class="sxs-lookup"><span data-stu-id="021b1-116">hello following example creates a VM named `myVM`.</span></span> <span data-ttu-id="021b1-117">También se crean claves SSH si aún no existen en una ubicación de claves predeterminada.</span><span class="sxs-lookup"><span data-stu-id="021b1-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="021b1-118">toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.</span><span class="sxs-lookup"><span data-stu-id="021b1-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="021b1-119">Después de crear Hola VM, CLI de Azure muestra información toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="021b1-119">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="021b1-120">Tenga en cuenta el valor de Hola para `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="021b1-120">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="021b1-121">Utilice este hello tooaccess de dirección virtual.</span><span class="sxs-lookup"><span data-stu-id="021b1-121">You use this address tooaccess hello VM.</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a><span data-ttu-id="021b1-122">Conectar toohello VM</span><span class="sxs-lookup"><span data-stu-id="021b1-122">Connect toohello VM</span></span>

<span data-ttu-id="021b1-123">toocreate una sesión SSH con hello de máquina virtual, use Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="021b1-123">toocreate an SSH session with hello VM, use hello following command.</span></span> <span data-ttu-id="021b1-124">Reemplace la dirección IP de hello con hello `publicIpAddress` valor para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="021b1-124">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a><span data-ttu-id="021b1-125">Crear base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="021b1-125">Create hello database</span></span>

<span data-ttu-id="021b1-126">Hola software de Oracle ya está instalado en una imagen de Marketplace Hola.</span><span class="sxs-lookup"><span data-stu-id="021b1-126">hello Oracle software is already installed on hello Marketplace image.</span></span> <span data-ttu-id="021b1-127">Cree una base de datos de ejemplo de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="021b1-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="021b1-128">Cambiar toohello *oracle* superusuario y, a continuación, agente de escucha de inicializar hello para el registro:</span><span class="sxs-lookup"><span data-stu-id="021b1-128">Switch toohello *oracle* superuser, then initialize hello listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="021b1-129">salida de Hello es siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="021b1-129">hello output is similar toohello following:</span></span>

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  <span data-ttu-id="021b1-130">Crear base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="021b1-130">Create hello database:</span></span>

    ```bash
    dbca -silent \
           -createDatabase \
           -templateName General_Purpose.dbc \
           -gdbname cdb1 \
           -sid cdb1 \
           -responseFile NO_VALUE \
           -characterSet AL32UTF8 \
           -sysPassword OraPasswd1 \
           -systemPassword OraPasswd1 \
           -createAsContainerDatabase true \
           -numberOfPDBs 1 \
           -pdbName pdb1 \
           -pdbAdminPassword OraPasswd1 \
           -databaseType MULTIPURPOSE \
           -automaticMemoryManagement false \
           -storageType FS \
           -ignorePreReqs
    ```

    <span data-ttu-id="021b1-131">Toma el base de datos unos minutos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="021b1-131">It takes a few minutes toocreate hello database.</span></span>

3. <span data-ttu-id="021b1-132">Establecimiento de las variables de Oracle</span><span class="sxs-lookup"><span data-stu-id="021b1-132">Set Oracle variables</span></span>

<span data-ttu-id="021b1-133">Antes de conectar, necesita tooset dos variables de entorno: *ORACLE_HOME* y *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="021b1-133">Before you connect, you need tooset two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="021b1-134">También puede agregar ORACLE_HOME y ORACLE_SID toohello .bashrc archivo de variables de.</span><span class="sxs-lookup"><span data-stu-id="021b1-134">You also can add ORACLE_HOME and ORACLE_SID variables toohello .bashrc file.</span></span> <span data-ttu-id="021b1-135">Esto ahorraría variables de entorno de Hola para futuros inicios de sesión. Confirme Hola siguiente instrucciones se han agregado toohello `~/.bashrc` archivo mediante el editor de su elección.</span><span class="sxs-lookup"><span data-stu-id="021b1-135">This would save hello environment variables for future sign-ins. Confirm hello following statements have been added toohello `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="021b1-136">Conectividad con Oracle EM Express</span><span class="sxs-lookup"><span data-stu-id="021b1-136">Oracle EM Express connectivity</span></span>

<span data-ttu-id="021b1-137">Para una herramienta de administración de GUI que puede usar la base de datos de tooexplore hello, configure Oracle EM Express.</span><span class="sxs-lookup"><span data-stu-id="021b1-137">For a GUI management tool that you can use tooexplore hello database, set up Oracle EM Express.</span></span> <span data-ttu-id="021b1-138">tooconnect tooOracle EM Express, primero debe establecer el puerto de hello en Oracle.</span><span class="sxs-lookup"><span data-stu-id="021b1-138">tooconnect tooOracle EM Express, you must first set up hello port in Oracle.</span></span> 

1. <span data-ttu-id="021b1-139">Conectar la base de datos de tooyour mediante sqlplus:</span><span class="sxs-lookup"><span data-stu-id="021b1-139">Connect tooyour database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="021b1-140">Una vez conectado, establezca el puerto de hello 5502 para EM Express</span><span class="sxs-lookup"><span data-stu-id="021b1-140">Once connected, set hello port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="021b1-141">Contenedor de hello abierto PDB1 si no ya está abierto, pero primero comprobar el estado de hello:</span><span class="sxs-lookup"><span data-stu-id="021b1-141">Open hello container PDB1 if not already opened, but first check hello status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="021b1-142">salida de Hello es siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="021b1-142">hello output is similar toohello following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="021b1-143">Si Hola OPEN_MODE para `PDB1` no es leer escribir, a continuación, ejecute comandos tooopen PDB1 de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="021b1-143">If hello OPEN_MODE for `PDB1` is not READ WRITE, then run hello followings commands tooopen PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="021b1-144">Necesita tootype `quit` tooend Hola sqlplus sesión y el tipo `exit` toologout de usuario de oracle Hola.</span><span class="sxs-lookup"><span data-stu-id="021b1-144">You need tootype `quit` tooend hello sqlplus session and type `exit` toologout of hello oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="021b1-145">Automatizar el arranque y el apagado de la base de datos</span><span class="sxs-lookup"><span data-stu-id="021b1-145">Automate database startup and shutdown</span></span>

<span data-ttu-id="021b1-146">base de datos de Oracle de Hola de forma predeterminada no se inicia automáticamente cuando se reinicia Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="021b1-146">hello Oracle database by default doesn't automatically start when you restart hello VM.</span></span> <span data-ttu-id="021b1-147">tooset una toostart de base de datos de Oracle Hola automáticamente, primero inicie sesión como raíz.</span><span class="sxs-lookup"><span data-stu-id="021b1-147">tooset up hello Oracle database toostart automatically, first sign in as root.</span></span> <span data-ttu-id="021b1-148">Después, cree y actualice algunos archivos del sistema.</span><span class="sxs-lookup"><span data-stu-id="021b1-148">Then, create and update some system files.</span></span>

1. <span data-ttu-id="021b1-149">Inicio de sesión como raíz</span><span class="sxs-lookup"><span data-stu-id="021b1-149">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="021b1-150">Con su editor favorito, edite el archivo hello `/etc/oratab` y cambie el valor predeterminado de hello `N` demasiado`Y`:</span><span class="sxs-lookup"><span data-stu-id="021b1-150">Using your favorite editor, edit hello file `/etc/oratab` and change hello default `N` too`Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="021b1-151">Cree un archivo denominado `/etc/init.d/dbora` y pegar Hola siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="021b1-151">Create a file named `/etc/init.d/dbora` and paste hello following contents:</span></span>

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  <span data-ttu-id="021b1-152">Cambie los permisos de los archivos con *chmod* como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="021b1-152">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="021b1-153">Cree vínculos simbólicos para el inicio y el apagado de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="021b1-153">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="021b1-154">tootest los cambios, reinicie Hola VM:</span><span class="sxs-lookup"><span data-stu-id="021b1-154">tootest your changes, restart hello VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="021b1-155">Abrir puertos para la conectividad</span><span class="sxs-lookup"><span data-stu-id="021b1-155">Open ports for connectivity</span></span>

<span data-ttu-id="021b1-156">tarea final de Hello es tooconfigure algunos extremos externos.</span><span class="sxs-lookup"><span data-stu-id="021b1-156">hello final task is tooconfigure some external endpoints.</span></span> <span data-ttu-id="021b1-157">tooset seguridad Hola grupo de seguridad de red de Azure que protege Hola VM, salir de la sesión de SSH en hello VM (debe haber sido expulsado SSH al reiniciar el sistema en el paso anterior).</span><span class="sxs-lookup"><span data-stu-id="021b1-157">tooset up hello Azure Network Security Group that protects hello VM, first exit your SSH session in hello VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="021b1-158">extremo de hello tooopen usar base de datos de Oracle tooaccess Hola de forma remota, cree una regla de grupo de seguridad de red con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="021b1-158">tooopen hello endpoint that you use tooaccess hello Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="021b1-159">extremo de Hola de tooopen que usar tooaccess Oracle EM Express de forma remota, cree una regla de grupo de seguridad de red con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="021b1-159">tooopen hello endpoint that you use tooaccess Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="021b1-160">Si es necesario, obtenga la dirección IP pública de saludo de la máquina virtual nuevo con [show de public-ip de red az](/cli/azure/network/public-ip#show) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="021b1-160">If needed, obtain hello public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="021b1-161">Conecte EM Express desde el explorador.</span><span class="sxs-lookup"><span data-stu-id="021b1-161">Connect EM Express from your browser.</span></span> <span data-ttu-id="021b1-162">Asegúrese de que el explorador sea compatible con Express EM (es necesario que Flash esté instalado):</span><span class="sxs-lookup"><span data-stu-id="021b1-162">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="021b1-163">Puede iniciar sesión mediante el uso de hello **SYS** cuenta y comprobar hello **como sysdba** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="021b1-163">You can log in by using hello **SYS** account, and check hello **as sysdba** checkbox.</span></span> <span data-ttu-id="021b1-164">Usar la contraseña de hello **OraPasswd1** que establecen durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="021b1-164">Use hello password **OraPasswd1** that you set during installation.</span></span> 

![Captura de pantalla de la página de inicio de sesión de Oracle OEM Express Hola](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="021b1-166">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="021b1-166">Clean up resources</span></span>

<span data-ttu-id="021b1-167">Una vez que haya terminado de explorar la primera base de datos de Oracle en Azure y hello VM ya no es necesario, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="021b1-167">Once you have finished exploring your first Oracle database on Azure and hello VM is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="021b1-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="021b1-168">Next steps</span></span>

<span data-ttu-id="021b1-169">Conozca otras [soluciones de Oracle en Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="021b1-169">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="021b1-170">Intente hello [instalar y configurar Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="021b1-170">Try hello [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>
