---
title: aaaImplement Oracle Data Guard en VM de Linux de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="04e52-103">Implementación de Oracle Data Guard en máquinas virtuales Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="04e52-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="04e52-104">Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="04e52-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="04e52-105">Esta guía se detalla con hello Azure CLI toodeploy 12C base de datos de imagen de la Galería de hello Marketplace de Oracle.</span><span class="sxs-lookup"><span data-stu-id="04e52-105">This guide details using hello Azure CLI toodeploy an Oracle 12c Database from hello Marketplace gallery image.</span></span> <span data-ttu-id="04e52-106">Una vez que se crea la base de datos de Oracle de hello, este documento muestra cómo paso a paso tooinstall y configurar Data Guard en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="04e52-106">Once hello Oracle database is created, this document shows you step-by-step how tooinstall and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="04e52-107">Antes de empezar, asegúrese de que ese Hola que CLI de Azure se ha instalado.</span><span class="sxs-lookup"><span data-stu-id="04e52-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="04e52-108">Para obtener más información, consulte la [guía de instalación de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="04e52-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="04e52-109">Preparar el entorno de Hola</span><span class="sxs-lookup"><span data-stu-id="04e52-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="04e52-110">Supuestos</span><span class="sxs-lookup"><span data-stu-id="04e52-110">Assumptions</span></span>

<span data-ttu-id="04e52-111">Hola de tooperform instalar Oracle Data Guard, deberá toocreate dos máquinas virtuales de Azure en hello mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="04e52-111">tooperform hello Oracle Data Guard install, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="04e52-112">imagen de Marketplace de Hello usar toocreate hello las máquinas virtuales es "Oracle: Oracle-base de datos-Ee:12.1.0.2:latest".</span><span class="sxs-lookup"><span data-stu-id="04e52-112">hello Marketplace image you use toocreate hello VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="04e52-113">Hello VM principal (myVM1) tiene una instancia de Oracle en ejecución.</span><span class="sxs-lookup"><span data-stu-id="04e52-113">hello primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="04e52-114">Hola que máquina virtual en espera (myVM2) tiene instalado sólo el software de Oracle de Hola.</span><span class="sxs-lookup"><span data-stu-id="04e52-114">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="04e52-115">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="04e52-115">Log in tooAzure</span></span> 

<span data-ttu-id="04e52-116">Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="04e52-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="04e52-117">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="04e52-117">Create a resource group</span></span>

<span data-ttu-id="04e52-118">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="04e52-118">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="04e52-119">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="04e52-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="04e52-120">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westus` ubicación.</span><span class="sxs-lookup"><span data-stu-id="04e52-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="04e52-121">Crear conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="04e52-121">Create availability set</span></span>

<span data-ttu-id="04e52-122">Este paso es opcional, pero recomendable.</span><span class="sxs-lookup"><span data-stu-id="04e52-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="04e52-123">Consulte la [guía de conjuntos de disponibilidad de Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="04e52-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="04e52-124">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="04e52-124">Create virtual machine</span></span>

<span data-ttu-id="04e52-125">Crear una máquina virtual con hello [crear vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="04e52-125">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="04e52-126">Hello en el ejemplo siguiente se crea 2 máquinas virtuales con el nombre `myVM1` y `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="04e52-126">hello following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="04e52-127">También se crean claves SSH si aún no existen en una ubicación de claves predeterminada.</span><span class="sxs-lookup"><span data-stu-id="04e52-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="04e52-128">toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.</span><span class="sxs-lookup"><span data-stu-id="04e52-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="04e52-129">Crear myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="04e52-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="04e52-130">Una vez Hola se ha creado la máquina virtual, Hola CLI de Azure muestra información toohello similar siguiente ejemplo: tomar nota de hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="04e52-130">Once hello VM has been created, hello Azure CLI shows information similar toohello following example: Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="04e52-131">Esta dirección es hello tooaccess usa máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="04e52-131">This address is used tooaccess hello VM.</span></span>

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

<span data-ttu-id="04e52-132">Crear myVM2 (en espera)</span><span class="sxs-lookup"><span data-stu-id="04e52-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="04e52-133">Tome nota de hello `publicIpAddress` así una vez que creó.</span><span class="sxs-lookup"><span data-stu-id="04e52-133">Take note of hello `publicIpAddress` as well once it created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="04e52-134">Hola abierto el puerto TCP para la conectividad</span><span class="sxs-lookup"><span data-stu-id="04e52-134">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="04e52-135">paso de Hello es tooconfigure extremos externos, lo que permite el acceso remoto Hola DB de Oracle, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="04e52-135">hello step is tooconfigure external endpoints, which allows accessing hello Oracle DB remotely, you execute hello following command.</span></span>

<span data-ttu-id="04e52-136">Abrir el puerto para myVM1</span><span class="sxs-lookup"><span data-stu-id="04e52-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="04e52-137">Resultado debería ser similar toohello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="04e52-137">Result should look similar toohello following response:</span></span>

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

<span data-ttu-id="04e52-138">Abrir el puerto para myVM2</span><span class="sxs-lookup"><span data-stu-id="04e52-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a><span data-ttu-id="04e52-139">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="04e52-139">Connect toovirtual machine</span></span>

<span data-ttu-id="04e52-140">Siguiente Hola de uso del comando toocreate una sesión SSH con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="04e52-140">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="04e52-141">Reemplace la dirección IP de hello con hello `publicIpAddress` de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="04e52-141">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="04e52-142">Creación de la base de datos en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="04e52-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="04e52-143">Hola software de Oracle ya está instalado en una imagen de Marketplace hello, para que hello siguiente paso es base de datos de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="04e52-143">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> <span data-ttu-id="04e52-144">primer paso de saludo se está ejecutando como superusuario de hello 'oracle'.</span><span class="sxs-lookup"><span data-stu-id="04e52-144">hello first step is running as hello 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="04e52-145">Crear base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="04e52-145">create hello database:</span></span>

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
<span data-ttu-id="04e52-146">Salidas deben tener un aspecto similar toohello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="04e52-146">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="04e52-147">Establecer variables de hello ORACLE_SID y ORACLE_HOME</span><span class="sxs-lookup"><span data-stu-id="04e52-147">Set hello ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="04e52-148">Si lo desea, puede ORACLE_HOME y ORACLE_SID toohello .bashrc archivo agregado, por lo que esta configuración se guarda para futuras inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="04e52-148">Optionally, You can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="04e52-149">Configuraciones de Data Guard</span><span class="sxs-lookup"><span data-stu-id="04e52-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="04e52-150">Habilitar el modo de archivar registro en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="04e52-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="04e52-151">Habilite el registro forzado y asegúrese de que, al menos, haya un archivo de registro está presente.</span><span class="sxs-lookup"><span data-stu-id="04e52-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="04e52-152">Crear registros de recuperación en espera</span><span class="sxs-lookup"><span data-stu-id="04e52-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="04e52-153">Activar retrospectiva (lo que dificultaba recuperación Hola mucho anteriormente) y establezca STANDBY_FILE_MANAGEMENT tooauto</span><span class="sxs-lookup"><span data-stu-id="04e52-153">Turn on Flashback (which made hello recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT tooauto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="04e52-154">Configuración del servicio en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="04e52-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="04e52-155">Editar o crear el archivo tnsnames.ora de hello, que se encuentra en la carpeta de ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="04e52-155">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="04e52-156">Agregar Hola siguiendo las entradas</span><span class="sxs-lookup"><span data-stu-id="04e52-156">Add hello following entries</span></span>

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

<span data-ttu-id="04e52-157">Editar o crear el archivo listener.ora de hello, que se encuentra en la carpeta de ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="04e52-157">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="04e52-158">Agregar Hola siguiendo las entradas</span><span class="sxs-lookup"><span data-stu-id="04e52-158">Add hello following entries</span></span>

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

<span data-ttu-id="04e52-159">Iniciar el agente de escucha de Hola</span><span class="sxs-lookup"><span data-stu-id="04e52-159">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="04e52-160">Configuración del servicio en myVM2 (en espera)</span><span class="sxs-lookup"><span data-stu-id="04e52-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="04e52-161">Editar o crear el archivo tnsnames.ora de hello, que se encuentra en la carpeta de ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="04e52-161">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="04e52-162">Agregar Hola siguiendo las entradas</span><span class="sxs-lookup"><span data-stu-id="04e52-162">Add hello following entries</span></span>

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

<span data-ttu-id="04e52-163">Editar o crear el archivo listener.ora de hello, que se encuentra en la carpeta de ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="04e52-163">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="04e52-164">Agregar Hola siguiendo las entradas</span><span class="sxs-lookup"><span data-stu-id="04e52-164">Add hello following entries</span></span>

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

<span data-ttu-id="04e52-165">Iniciar el agente de escucha de Hola</span><span class="sxs-lookup"><span data-stu-id="04e52-165">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="04e52-166">Habilitar el agente de Data Guard</span><span class="sxs-lookup"><span data-stu-id="04e52-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a><span data-ttu-id="04e52-167">Restaurar base de datos toomyVM2 (espera)</span><span class="sxs-lookup"><span data-stu-id="04e52-167">Restore database toomyVM2 (Standby)</span></span>

<span data-ttu-id="04e52-168">Crear un archivo de parámetros ' / tmp/initcdb1_stby.ora' con contenido de hello siguiente</span><span class="sxs-lookup"><span data-stu-id="04e52-168">Create a parameter file '/tmp/initcdb1_stby.ora' with hello followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="04e52-169">Crear carpetas</span><span class="sxs-lookup"><span data-stu-id="04e52-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="04e52-170">Crear un archivo de contraseña</span><span class="sxs-lookup"><span data-stu-id="04e52-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="04e52-171">Iniciar la base de datos en myVM2</span><span class="sxs-lookup"><span data-stu-id="04e52-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="04e52-172">Restaurar base de datos con la utilidad RMAN</span><span class="sxs-lookup"><span data-stu-id="04e52-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="04e52-173">Ejecutar Hola siguientes comandos de RMAN</span><span class="sxs-lookup"><span data-stu-id="04e52-173">Execute hello following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="04e52-174">Habilitar el agente de Data Guard</span><span class="sxs-lookup"><span data-stu-id="04e52-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="04e52-175">Configuración del agente de Data Guard en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="04e52-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="04e52-176">Inicie el Administrador de Data Guard Hola e inicie sesión con SYS y la contraseña (lo que no utiliza la autenticación de sistema operativo).</span><span class="sxs-lookup"><span data-stu-id="04e52-176">Start hello Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="04e52-177">Realizar siguiente Hola</span><span class="sxs-lookup"><span data-stu-id="04e52-177">Perform hello followings</span></span>

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

<span data-ttu-id="04e52-178">Revisar la configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="04e52-178">Review hello configuration</span></span>
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

<span data-ttu-id="04e52-179">Esto completa el programa de instalación de Oracle Data Guard de Hola.</span><span class="sxs-lookup"><span data-stu-id="04e52-179">This completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="04e52-180">sección de Hello siguiente muestra cómo tootest Hola conectividad y cambiando</span><span class="sxs-lookup"><span data-stu-id="04e52-180">hello next section shows you how tootest hello connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="04e52-181">Conexión de la base de datos desde el equipo cliente</span><span class="sxs-lookup"><span data-stu-id="04e52-181">Connect database from client machine</span></span>

<span data-ttu-id="04e52-182">Actualizar o crear el archivo tnsnames.ora de hello en el equipo cliente que normalmente se encuentra en ORACLE_HOME\network\admin $.</span><span class="sxs-lookup"><span data-stu-id="04e52-182">Update or create hello tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="04e52-183">Reemplace Hola IP con su `publicIpAddress` para myVM1 y por myVM2</span><span class="sxs-lookup"><span data-stu-id="04e52-183">Replace hello IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="04e52-184">Iniciar sqlplus</span><span class="sxs-lookup"><span data-stu-id="04e52-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="04e52-185">Prueba de la configuración de Data Guard</span><span class="sxs-lookup"><span data-stu-id="04e52-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="04e52-186">Cambio de la base de datos en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="04e52-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="04e52-187">tooswitch de toostandby principal (cdb1 toocdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="04e52-187">tooswitch from primary toostandby (cdb1 toocdb1_stby)</span></span>

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

<span data-ttu-id="04e52-188">Ahora debería base de datos en espera puede tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="04e52-188">You should now be able tooconnect toohello standby database</span></span>

<span data-ttu-id="04e52-189">Iniciar sqlplus</span><span class="sxs-lookup"><span data-stu-id="04e52-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="04e52-190">Regreso a la base de datos en myVM2 (en espera)</span><span class="sxs-lookup"><span data-stu-id="04e52-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="04e52-191">tooswitch, ejecute el siguiente hello en myVM2</span><span class="sxs-lookup"><span data-stu-id="04e52-191">tooswitch back, run hello followings on myVM2</span></span>
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

<span data-ttu-id="04e52-192">Una vez más, ahora debería base de datos principal puede tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="04e52-192">Once again, You should now be able tooconnect toohello primary database</span></span>

<span data-ttu-id="04e52-193">Iniciar sqlplus</span><span class="sxs-lookup"><span data-stu-id="04e52-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="04e52-194">Esto completa la instalación hello y la configuración de protección de datos en Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="04e52-194">This completed hello installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="04e52-195">Eliminación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="04e52-195">Delete virtual machine</span></span>

<span data-ttu-id="04e52-196">Cuando ya no necesite, Hola siguiente comando puede ser usado tooremove Hola grupo de recursos de máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="04e52-196">When no longer needed, hello following command can be used tooremove hello Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="04e52-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04e52-197">Next steps</span></span>

[<span data-ttu-id="04e52-198">Tutorial de creación de máquinas virtuales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="04e52-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="04e52-199">Ejemplos de la CLI de implementación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="04e52-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
