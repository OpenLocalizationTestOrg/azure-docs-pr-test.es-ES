---
title: "aaaImplement Oracle Data Guard en una máquina virtual de Linux de Azure | Documentos de Microsoft"
description: "Ponga en funcionamiento rápidamente una instancia de Oracle Data Guard en el entorno de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="b89f7-103">Implementación de Oracle Data Guard en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="b89f7-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="b89f7-104">CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="b89f7-104">Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="b89f7-105">Este artículo describe cómo toouse CLI de Azure toodeploy una base de datos de Oracle 12C base de datos de imagen de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b89f7-105">This article describes how toouse Azure CLI toodeploy an Oracle Database 12c database from hello Azure Marketplace image.</span></span> <span data-ttu-id="b89f7-106">Este artículo, a continuación, muestra, paso a paso, cómo tooinstall y configurar Data Guard en una máquina virtual (VM) de Azure.</span><span class="sxs-lookup"><span data-stu-id="b89f7-106">This article then shows you, step by step, how tooinstall and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="b89f7-107">Antes de comenzar, asegúrese de que esté instalada la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b89f7-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="b89f7-108">Para obtener más información, vea hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b89f7-108">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="b89f7-109">Preparar el entorno de Hola</span><span class="sxs-lookup"><span data-stu-id="b89f7-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="b89f7-110">Supuestos</span><span class="sxs-lookup"><span data-stu-id="b89f7-110">Assumptions</span></span>

<span data-ttu-id="b89f7-111">tooinstall Oracle Data Guard, deberá toocreate dos máquinas virtuales de Azure en hello mismo conjunto de disponibilidad:</span><span class="sxs-lookup"><span data-stu-id="b89f7-111">tooinstall Oracle Data Guard, you need toocreate two Azure VMs on hello same availability set:</span></span>

- <span data-ttu-id="b89f7-112">Hello VM principal (myVM1) tiene una instancia de Oracle en ejecución.</span><span class="sxs-lookup"><span data-stu-id="b89f7-112">hello primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="b89f7-113">Hola que máquina virtual en espera (myVM2) tiene instalado sólo el software de Oracle de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89f7-113">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

<span data-ttu-id="b89f7-114">imagen de Marketplace que usar toocreate Hola máquinas virtuales Hello es Oracle: Oracle-base de datos-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="b89f7-114">hello Marketplace image that you use toocreate hello VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="b89f7-115">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="b89f7-115">Sign in tooAzure</span></span> 

<span data-ttu-id="b89f7-116">Inicie sesión en tooyour suscripción de Azure mediante hello [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="b89f7-116">Sign in tooyour Azure subscription by using hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="b89f7-117">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b89f7-117">Create a resource group</span></span>

<span data-ttu-id="b89f7-118">Crear un grupo de recursos mediante el uso de hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b89f7-118">Create a resource group by using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="b89f7-119">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b89f7-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="b89f7-120">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westus` ubicación:</span><span class="sxs-lookup"><span data-stu-id="b89f7-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="b89f7-121">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="b89f7-121">Create an availability set</span></span>

<span data-ttu-id="b89f7-122">La creación de un conjunto de disponibilidad es opcional, pero es recomendable.</span><span class="sxs-lookup"><span data-stu-id="b89f7-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="b89f7-123">Para más información, consulte las [directrices de conjuntos de disponibilidad de Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="b89f7-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="b89f7-124">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b89f7-124">Create a virtual machine</span></span>

<span data-ttu-id="b89f7-125">Crear una máquina virtual mediante hello [crear vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b89f7-125">Create a VM by using hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="b89f7-126">Hello en el ejemplo siguiente se crea dos máquinas virtuales con el nombre `myVM1` y `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="b89f7-126">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="b89f7-127">También se crean claves SSH si aún no existen en una ubicación de claves predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b89f7-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="b89f7-128">toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.</span><span class="sxs-lookup"><span data-stu-id="b89f7-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="b89f7-129">Cree myVM1 (principal):</span><span class="sxs-lookup"><span data-stu-id="b89f7-129">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="b89f7-130">Después de crear Hola VM, CLI de Azure muestra información toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b89f7-130">After you create hello VM, Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="b89f7-131">Tenga en cuenta el valor de Hola de `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="b89f7-131">Note hello value of `publicIpAddress`.</span></span> <span data-ttu-id="b89f7-132">Utilice este hello tooaccess de dirección virtual.</span><span class="sxs-lookup"><span data-stu-id="b89f7-132">You use this address tooaccess hello VM.</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="b89f7-133">Cree myVM2 (en espera):</span><span class="sxs-lookup"><span data-stu-id="b89f7-133">Create myVM2 (standby):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="b89f7-134">Tenga en cuenta el valor de Hola de `publicIpAddress` después de crear myVM2.</span><span class="sxs-lookup"><span data-stu-id="b89f7-134">Note hello value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="b89f7-135">Hola abierto el puerto TCP para la conectividad</span><span class="sxs-lookup"><span data-stu-id="b89f7-135">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="b89f7-136">Este paso configura extremos externos, lo que permite la base de datos de Oracle de toohello de acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="b89f7-136">This step configures external endpoints, which allow remote access toohello Oracle database.</span></span>

<span data-ttu-id="b89f7-137">Abrir el puerto de Hola para myVM1:</span><span class="sxs-lookup"><span data-stu-id="b89f7-137">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="b89f7-138">resultado de Hello debería ser similar toohello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="b89f7-138">hello result should look similar toohello following response:</span></span>

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

<span data-ttu-id="b89f7-139">Abrir el puerto de Hola para myVM2:</span><span class="sxs-lookup"><span data-stu-id="b89f7-139">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="b89f7-140">Conectar máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="b89f7-140">Connect toohello virtual machine</span></span>

<span data-ttu-id="b89f7-141">Siguiente Hola de uso del comando toocreate una sesión SSH con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89f7-141">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="b89f7-142">Reemplace la dirección IP de hello con hello `publicIpAddress` valor para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b89f7-142">Replace hello IP address with hello `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="b89f7-143">Crear base de datos de hello en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="b89f7-143">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="b89f7-144">Hola software de Oracle ya está instalado en una imagen de Marketplace hello, para que hello siguiente paso es base de datos de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="b89f7-144">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="b89f7-145">Cambiar toohello superusuario de Oracle:</span><span class="sxs-lookup"><span data-stu-id="b89f7-145">Switch toohello Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="b89f7-146">Crear base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="b89f7-146">Create hello database:</span></span>

```bash
$ dbca -silent \
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
<span data-ttu-id="b89f7-147">Salidas deben tener un aspecto similar toohello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="b89f7-147">Outputs should look similar toohello following response:</span></span>

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="b89f7-148">Establecer variables de hello ORACLE_SID y ORACLE_HOME:</span><span class="sxs-lookup"><span data-stu-id="b89f7-148">Set hello ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="b89f7-149">Si lo desea, puede agregar archivos de /home/oracle/.bashrc toohello ORACLE_HOME y ORACLE_SID, para que esta configuración se guarda para futuras inicios de sesión:</span><span class="sxs-lookup"><span data-stu-id="b89f7-149">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="b89f7-150">Configuración de Data Guard</span><span class="sxs-lookup"><span data-stu-id="b89f7-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="b89f7-151">Habilitar el modo de archivar registro en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="b89f7-151">Enable archive log mode on myVM1 (primary)</span></span>

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
<span data-ttu-id="b89f7-152">Habilite el registro forzado y asegúrese de que, al menos, haya un archivo de registro está presente:</span><span class="sxs-lookup"><span data-stu-id="b89f7-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="b89f7-153">Cree registros de rehacer en espera:</span><span class="sxs-lookup"><span data-stu-id="b89f7-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="b89f7-154">Activar retrospectiva (lo que facilita la recuperación mucho) y establezca el modo de espera\_archivo\_tooauto de administración.</span><span class="sxs-lookup"><span data-stu-id="b89f7-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT tooauto.</span></span> <span data-ttu-id="b89f7-155">Salga de SQL * Plus a continuación.</span><span class="sxs-lookup"><span data-stu-id="b89f7-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="b89f7-156">Configuración del servicio en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="b89f7-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="b89f7-157">Editar o crear el archivo tnsnames.ora de hello, que se encuentra en la carpeta de hello $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="b89f7-157">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="b89f7-158">Agregue Hola siguientes entradas:</span><span class="sxs-lookup"><span data-stu-id="b89f7-158">Add hello following entries:</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="b89f7-159">Editar o crear el archivo listener.ora de hello, que se encuentra en la carpeta de hello $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="b89f7-159">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="b89f7-160">Agregue Hola siguientes entradas:</span><span class="sxs-lookup"><span data-stu-id="b89f7-160">Add hello following entries:</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="b89f7-161">Habilite el agente de Data Guard:</span><span class="sxs-lookup"><span data-stu-id="b89f7-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="b89f7-162">Inicie el agente de escucha de hello:</span><span class="sxs-lookup"><span data-stu-id="b89f7-162">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="b89f7-163">Configuración del servicio en myVM2 (en espera)</span><span class="sxs-lookup"><span data-stu-id="b89f7-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="b89f7-164">ToomyVM2 SSH:</span><span class="sxs-lookup"><span data-stu-id="b89f7-164">SSH toomyVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="b89f7-165">Inicie sesión como Oracle:</span><span class="sxs-lookup"><span data-stu-id="b89f7-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="b89f7-166">Editar o crear el archivo tnsnames.ora de hello, que se encuentra en la carpeta de hello $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="b89f7-166">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="b89f7-167">Agregue Hola siguientes entradas:</span><span class="sxs-lookup"><span data-stu-id="b89f7-167">Add hello following entries:</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="b89f7-168">Editar o crear el archivo listener.ora de hello, que se encuentra en la carpeta de hello $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="b89f7-168">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="b89f7-169">Agregue Hola siguientes entradas:</span><span class="sxs-lookup"><span data-stu-id="b89f7-169">Add hello following entries:</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="b89f7-170">Inicie el agente de escucha de hello:</span><span class="sxs-lookup"><span data-stu-id="b89f7-170">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a><span data-ttu-id="b89f7-171">Restaurar hello toomyVM2 de base de datos (en espera)</span><span class="sxs-lookup"><span data-stu-id="b89f7-171">Restore hello database toomyVM2 (standby)</span></span>

<span data-ttu-id="b89f7-172">Crear Hola parámetro archivo /tmp/initcdb1_stby.ora con hello siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="b89f7-172">Create hello parameter file /tmp/initcdb1_stby.ora with hello following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="b89f7-173">Cree carpetas:</span><span class="sxs-lookup"><span data-stu-id="b89f7-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="b89f7-174">Cree un archivo de contraseña:</span><span class="sxs-lookup"><span data-stu-id="b89f7-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="b89f7-175">Iniciar la base de datos de hello en myVM2:</span><span class="sxs-lookup"><span data-stu-id="b89f7-175">Start hello database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="b89f7-176">Restaurar base de datos de hello mediante Hola RMAN herramienta:</span><span class="sxs-lookup"><span data-stu-id="b89f7-176">Restore hello database by using hello RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="b89f7-177">Ejecute hello siga los comandos en RMAN:</span><span class="sxs-lookup"><span data-stu-id="b89f7-177">Run hello following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="b89f7-178">Debería aparecer mensajes similares toohello siguiente cuando se completa el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89f7-178">You should see messages similar toohello following when hello command is completed.</span></span> <span data-ttu-id="b89f7-179">Salga de RMAN.</span><span class="sxs-lookup"><span data-stu-id="b89f7-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="b89f7-180">Si lo desea, puede agregar archivos de /home/oracle/.bashrc toohello ORACLE_HOME y ORACLE_SID, para que esta configuración se guarda para futuras inicios de sesión:</span><span class="sxs-lookup"><span data-stu-id="b89f7-180">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="b89f7-181">Habilite el agente de Data Guard:</span><span class="sxs-lookup"><span data-stu-id="b89f7-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="b89f7-182">Configuración del agente de Data Guard en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="b89f7-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="b89f7-183">Inicie el administrador de Data Guard e inicie sesión mediante SYS y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="b89f7-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="b89f7-184">(No utilice la autenticación de sistema operativo). Realice Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="b89f7-184">(Do not use OS authentication.) Perform hello following:</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="b89f7-185">Revisar la configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="b89f7-185">Review hello configuration:</span></span>
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

<span data-ttu-id="b89f7-186">Ha completado el programa de instalación de Oracle Data Guard de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89f7-186">You've completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="b89f7-187">sección de Hello siguiente muestra cómo tootest Hola conectividad y cambiar.</span><span class="sxs-lookup"><span data-stu-id="b89f7-187">hello next section shows you how tootest hello connectivity and switch over.</span></span>

### <a name="connect-hello-database-from-hello-client-machine"></a><span data-ttu-id="b89f7-188">Conectar la base de datos de Hola desde el equipo de cliente hello</span><span class="sxs-lookup"><span data-stu-id="b89f7-188">Connect hello database from hello client machine</span></span>

<span data-ttu-id="b89f7-189">Actualizar o crear el archivo tnsnames.ora de hello en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="b89f7-189">Update or create hello tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="b89f7-190">Este archivo suele encontrarse en $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="b89f7-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="b89f7-191">Reemplazar las direcciones IP de hello con su `publicIpAddress` valores para myVM1 y por myVM2:</span><span class="sxs-lookup"><span data-stu-id="b89f7-191">Replace hello IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

<span data-ttu-id="b89f7-192">Inicie SQL *Plus:</span><span class="sxs-lookup"><span data-stu-id="b89f7-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a><span data-ttu-id="b89f7-193">Configuración de protección de datos de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="b89f7-193">Test hello Data Guard configuration</span></span>

### <a name="switch-over-hello-database-on-myvm1-primary"></a><span data-ttu-id="b89f7-194">Cambiar base de datos de hello en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="b89f7-194">Switch over hello database on myVM1 (primary)</span></span>

<span data-ttu-id="b89f7-195">tooswitch de toostandby principal (cdb1 toocdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="b89f7-195">tooswitch from primary toostandby (cdb1 toocdb1_stby):</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="b89f7-196">Ahora puede conectarse toohello base de datos en espera.</span><span class="sxs-lookup"><span data-stu-id="b89f7-196">You can now connect toohello standby database.</span></span>

<span data-ttu-id="b89f7-197">Inicie SQL *Plus:</span><span class="sxs-lookup"><span data-stu-id="b89f7-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a><span data-ttu-id="b89f7-198">Cambiar base de datos de hello en myVM2 (en espera)</span><span class="sxs-lookup"><span data-stu-id="b89f7-198">Switch over hello database on myVM2 (standby)</span></span>

<span data-ttu-id="b89f7-199">tooswitch sobre, ejecute siguiente de hello en myVM2:</span><span class="sxs-lookup"><span data-stu-id="b89f7-199">tooswitch over, run hello following on myVM2:</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="b89f7-200">Una vez más, ahora debe ser la base de datos principal puede tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="b89f7-200">Once again, you should now be able tooconnect toohello primary database.</span></span>

<span data-ttu-id="b89f7-201">Inicie SQL *Plus:</span><span class="sxs-lookup"><span data-stu-id="b89f7-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="b89f7-202">Ha terminado de hello instalación y configuración de protección de datos en Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="b89f7-202">You've finished hello installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="b89f7-203">Eliminar la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="b89f7-203">Delete hello virtual machine</span></span>

<span data-ttu-id="b89f7-204">Cuando ya no necesita hello VM, puede usar Hola después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos:</span><span class="sxs-lookup"><span data-stu-id="b89f7-204">When you no longer need hello VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b89f7-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b89f7-205">Next steps</span></span>

[<span data-ttu-id="b89f7-206">Tutorial de creación de máquinas virtuales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="b89f7-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="b89f7-207">Ejemplos de la CLI de Azure para implementación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="b89f7-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
