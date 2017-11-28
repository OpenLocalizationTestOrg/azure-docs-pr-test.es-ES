---
title: "Creación de una base de datos Oracle en una VM de Azure | Microsoft Docs"
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
ms.openlocfilehash: 8683b016c4db2c66fb1dd994405b70c3d137a7fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="af03c-103">Creación de una base de datos Oracle en una VM de Azure</span><span class="sxs-lookup"><span data-stu-id="af03c-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="af03c-104">En esta guía se describe el uso de la CLI de Azure para implementar una máquina virtual de Azure a partir de la [imagen de la galería de Marketplace de Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) con el fin de crear una base de datos de Oracle 12c.</span><span class="sxs-lookup"><span data-stu-id="af03c-104">This guide details using the Azure CLI to deploy an Azure virtual machine from the [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order to create an Oracle 12c database.</span></span> <span data-ttu-id="af03c-105">Una vez implementado el servidor, el usuario conectará a través de SSH con el fin de configurar la base de datos Oracle.</span><span class="sxs-lookup"><span data-stu-id="af03c-105">Once the server is deployed, you will connect via SSH in order to configure the Oracle database.</span></span> 

<span data-ttu-id="af03c-106">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="af03c-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="af03c-107">Si decide instalar y usar la CLI localmente, para esta guía de inicio rápido es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="af03c-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="af03c-108">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="af03c-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="af03c-109">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="af03c-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="af03c-110">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="af03c-110">Create a resource group</span></span>

<span data-ttu-id="af03c-111">Cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="af03c-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="af03c-112">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="af03c-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="af03c-113">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *eastus*.</span><span class="sxs-lookup"><span data-stu-id="af03c-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="af03c-114">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="af03c-114">Create virtual machine</span></span>

<span data-ttu-id="af03c-115">Para crear una máquina virtual, use el comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="af03c-115">To create a virtual machine (VM), use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="af03c-116">En el ejemplo siguiente se crea una máquina virtual denominada `myVM`.</span><span class="sxs-lookup"><span data-stu-id="af03c-116">The following example creates a VM named `myVM`.</span></span> <span data-ttu-id="af03c-117">También se crean claves SSH si aún no existen en una ubicación de claves predeterminada.</span><span class="sxs-lookup"><span data-stu-id="af03c-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="af03c-118">Para utilizar un conjunto específico de claves, utilice la opción `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="af03c-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="af03c-119">Después de crear la máquina virtual, la CLI de Azure muestra información similar al ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="af03c-119">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="af03c-120">Tome nota del valor de `publicIpAddress`,</span><span class="sxs-lookup"><span data-stu-id="af03c-120">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="af03c-121">ya que usará esta dirección para tener acceso a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af03c-121">You use this address to access the VM.</span></span>

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

## <a name="connect-to-the-vm"></a><span data-ttu-id="af03c-122">Conexión a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="af03c-122">Connect to the VM</span></span>

<span data-ttu-id="af03c-123">Para crear una sesión de SSH con la máquina virtual, use el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="af03c-123">To create an SSH session with the VM, use the following command.</span></span> <span data-ttu-id="af03c-124">Reemplace la dirección IP por el valor `publicIpAddress` para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af03c-124">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-the-database"></a><span data-ttu-id="af03c-125">Creación de la base de datos</span><span class="sxs-lookup"><span data-stu-id="af03c-125">Create the database</span></span>

<span data-ttu-id="af03c-126">El software de Oracle ya está instalado en la imagen de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="af03c-126">The Oracle software is already installed on the Marketplace image.</span></span> <span data-ttu-id="af03c-127">Cree una base de datos de ejemplo de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="af03c-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="af03c-128">Cambie al superusuario *oracle* e inicialice el agente de escucha para el registro:</span><span class="sxs-lookup"><span data-stu-id="af03c-128">Switch to the *oracle* superuser, then initialize the listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="af03c-129">La salida será similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="af03c-129">The output is similar to the following:</span></span>

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written to /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of the LISTENER
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
    The listener supports no services
    The command completed successfully
    ```

2.  <span data-ttu-id="af03c-130">Cree la base de datos:</span><span class="sxs-lookup"><span data-stu-id="af03c-130">Create the database:</span></span>

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

    <span data-ttu-id="af03c-131">La operación de creación de la base de datos tarda unos minutos.</span><span class="sxs-lookup"><span data-stu-id="af03c-131">It takes a few minutes to create the database.</span></span>

3. <span data-ttu-id="af03c-132">Establecimiento de las variables de Oracle</span><span class="sxs-lookup"><span data-stu-id="af03c-132">Set Oracle variables</span></span>

<span data-ttu-id="af03c-133">Antes de conectarse, debe definir dos variables de entorno: *ORACLE_HOME* y *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="af03c-133">Before you connect, you need to set two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="af03c-134">También puede agregar ORACLE_HOME y ORACLE_SID al archivo .bashrc.</span><span class="sxs-lookup"><span data-stu-id="af03c-134">You also can add ORACLE_HOME and ORACLE_SID variables to the .bashrc file.</span></span> <span data-ttu-id="af03c-135">De este modo, las variables de entorno se guardarían para futuros inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="af03c-135">This would save the environment variables for future sign-ins.</span></span> <span data-ttu-id="af03c-136">Confirme que las instrucciones siguientes se han agregado al archivo `~/.bashrc` mediante el editor que elija.</span><span class="sxs-lookup"><span data-stu-id="af03c-136">Confirm the following statements have been added to the `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="af03c-137">Conectividad con Oracle EM Express</span><span class="sxs-lookup"><span data-stu-id="af03c-137">Oracle EM Express connectivity</span></span>

<span data-ttu-id="af03c-138">Para disponer de una herramienta de administración de GUI con la que pueda explorar la base de datos, configure Oracle EM Express.</span><span class="sxs-lookup"><span data-stu-id="af03c-138">For a GUI management tool that you can use to explore the database, set up Oracle EM Express.</span></span> <span data-ttu-id="af03c-139">Para conectarse a Oracle EM Express, primero debe configurar el puerto en Oracle.</span><span class="sxs-lookup"><span data-stu-id="af03c-139">To connect to Oracle EM Express, you must first set up the port in Oracle.</span></span> 

1. <span data-ttu-id="af03c-140">Conéctese a la base de datos mediante sqlplus:</span><span class="sxs-lookup"><span data-stu-id="af03c-140">Connect to your database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="af03c-141">Una vez conectado, establezca el puerto 5502 para EM Express.</span><span class="sxs-lookup"><span data-stu-id="af03c-141">Once connected, set the port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="af03c-142">Abra el contenedor PDB1 si no está ya abierto, pero antes compruebe el estado:</span><span class="sxs-lookup"><span data-stu-id="af03c-142">Open the container PDB1 if not already opened, but first check the status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="af03c-143">La salida será similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="af03c-143">The output is similar to the following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="af03c-144">Si el valor de OPEN_MODE para `PDB1` no es READ WRITE, ejecute los comandos siguientes para abrir PDB1:</span><span class="sxs-lookup"><span data-stu-id="af03c-144">If the OPEN_MODE for `PDB1` is not READ WRITE, then run the followings commands to open PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="af03c-145">Debe escribir `quit` para finalizar la sesión de sqlplus y `exit` para cerrar la sesión del usuario de Oracle.</span><span class="sxs-lookup"><span data-stu-id="af03c-145">You need to type `quit` to end the sqlplus session and type `exit` to logout of the oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="af03c-146">Automatizar el arranque y el apagado de la base de datos</span><span class="sxs-lookup"><span data-stu-id="af03c-146">Automate database startup and shutdown</span></span>

<span data-ttu-id="af03c-147">De forma predeterminada, la base de datos Oracle no se inicia automáticamente al reiniciar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af03c-147">The Oracle database by default doesn't automatically start when you restart the VM.</span></span> <span data-ttu-id="af03c-148">Para configurar la base de datos Oracle para iniciarse automáticamente, inicie primero una sesión como raíz.</span><span class="sxs-lookup"><span data-stu-id="af03c-148">To set up the Oracle database to start automatically, first sign in as root.</span></span> <span data-ttu-id="af03c-149">Después, cree y actualice algunos archivos del sistema.</span><span class="sxs-lookup"><span data-stu-id="af03c-149">Then, create and update some system files.</span></span>

1. <span data-ttu-id="af03c-150">Inicio de sesión como raíz</span><span class="sxs-lookup"><span data-stu-id="af03c-150">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="af03c-151">Con su editor favorito, edite el archivo `/etc/oratab` y cambie el valor predeterminado `N` a `Y`:</span><span class="sxs-lookup"><span data-stu-id="af03c-151">Using your favorite editor, edit the file `/etc/oratab` and change the default `N` to `Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="af03c-152">Cree un archivo denominado `/etc/init.d/dbora` y pegue el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="af03c-152">Create a file named `/etc/init.d/dbora` and paste the following contents:</span></span>

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME to be equivalent to $ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  <span data-ttu-id="af03c-153">Cambie los permisos de los archivos con *chmod* como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="af03c-153">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="af03c-154">Cree vínculos simbólicos para el inicio y el apagado de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="af03c-154">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="af03c-155">Para probar los cambios, reinicie la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="af03c-155">To test your changes, restart the VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="af03c-156">Abrir puertos para la conectividad</span><span class="sxs-lookup"><span data-stu-id="af03c-156">Open ports for connectivity</span></span>

<span data-ttu-id="af03c-157">La tarea final consiste en configurar algunos puntos de conexión externos.</span><span class="sxs-lookup"><span data-stu-id="af03c-157">The final task is to configure some external endpoints.</span></span> <span data-ttu-id="af03c-158">Para configurar el grupo de seguridad de red de Azure que protege la máquina virtual, cierre primero su sesión de SSH en la máquina virtual (si se le expulsó de SSH al reiniciar en el paso anterior).</span><span class="sxs-lookup"><span data-stu-id="af03c-158">To set up the Azure Network Security Group that protects the VM, first exit your SSH session in the VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="af03c-159">Para abrir el punto de conexión que usa para acceder a la base de datos Oracle de forma remota, cree una regla de grupo de seguridad de red con [az network nsg rule create](/cli/azure/network/nsg/rule#create) de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="af03c-159">To open the endpoint that you use to access the Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="af03c-160">Para abrir el punto de conexión que usa para acceder a Oracle EM Express de forma remota, cree una regla de grupo de seguridad de red con [az network nsg rule create](/cli/azure/network/nsg/rule#create) de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="af03c-160">To open the endpoint that you use to access Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="af03c-161">Si es necesario, obtenga de nuevo la dirección IP pública de la máquina virtual con [az network public-ip show](/cli/azure/network/public-ip#show) de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="af03c-161">If needed, obtain the public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="af03c-162">Conecte EM Express desde el explorador.</span><span class="sxs-lookup"><span data-stu-id="af03c-162">Connect EM Express from your browser.</span></span> <span data-ttu-id="af03c-163">Asegúrese de que el explorador sea compatible con Express EM (es necesario que Flash esté instalado):</span><span class="sxs-lookup"><span data-stu-id="af03c-163">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="af03c-164">Puede iniciar sesión mediante la cuenta **SYS** y activar la casilla **as sysdba**.</span><span class="sxs-lookup"><span data-stu-id="af03c-164">You can log in by using the **SYS** account, and check the **as sysdba** checkbox.</span></span> <span data-ttu-id="af03c-165">Use la contraseña **OraPasswd1** que estableció durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="af03c-165">Use the password **OraPasswd1** that you set during installation.</span></span> 

![Captura de pantalla de la página de inicio de sesión de Oracle OEM Express](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="af03c-167">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="af03c-167">Clean up resources</span></span>

<span data-ttu-id="af03c-168">Cuando haya terminado de explorar la primera base de datos Oracle en Azure y la VM ya no se necesite, puede usar el comando [az group delete](/cli/azure/group#delete) para quitar el grupo de recursos, la VM y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="af03c-168">Once you have finished exploring your first Oracle database on Azure and the VM is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="af03c-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af03c-169">Next steps</span></span>

<span data-ttu-id="af03c-170">Conozca otras [soluciones de Oracle en Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="af03c-170">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="af03c-171">Pruebe el tutorial sobre la [instalación y configuración de Oracle Automated Storage Management](configure-oracle-asm.md).</span><span class="sxs-lookup"><span data-stu-id="af03c-171">Try the [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>