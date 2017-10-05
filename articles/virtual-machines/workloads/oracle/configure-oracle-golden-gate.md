---
title: "Implementación de Oracle Golden Gate en máquinas virtuales Linux de Azure | Microsoft Docs"
description: "Ponga en funcionamiento rápidamente una base de datos de Oracle Golden Gate en el entorno de Azure."
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
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: a05711357d345267647c02e42336fd37c09e1bff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="61a95-103">Implementación de Oracle Golden Gate en máquinas virtuales Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="61a95-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="61a95-104">La CLI de Azure se usa para crear y administrar recursos de Azure desde la línea de comandos o en scripts.</span><span class="sxs-lookup"><span data-stu-id="61a95-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="61a95-105">En esta guía se detalla cómo usar la CLI de Azure para la implementación de la base de datos de Oracle 12c desde la imagen de la galería de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="61a95-105">This guide details how to use the Azure CLI to deploy an Oracle 12c database from the Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="61a95-106">En este documento se muestra paso a paso cómo crear, instalar y configurar Oracle Golden Gate en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="61a95-106">This document shows you step-by-step how to create, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="61a95-107">Antes de empezar, asegúrese de que se ha instalado la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="61a95-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="61a95-108">Para obtener más información, consulte la [guía de instalación de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="61a95-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="61a95-109">Preparación del entorno</span><span class="sxs-lookup"><span data-stu-id="61a95-109">Prepare the environment</span></span>

<span data-ttu-id="61a95-110">Para llevar a cabo la instalación de Oracle Golden Gate, debe crear dos máquinas virtuales de Azure en el mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="61a95-110">To perform the Oracle Golden Gate installation, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="61a95-111">La imagen de Marketplace que se usa para crear las máquinas virtuales es **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="61a95-111">The Marketplace image you use to create the VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="61a95-112">También debe estar familiarizado con vi, el editor de Unix, y tener un conocimiento básico de x11 (Windows X).</span><span class="sxs-lookup"><span data-stu-id="61a95-112">You also need to be familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="61a95-113">Lo siguiente es un resumen de la configuración del entorno:</span><span class="sxs-lookup"><span data-stu-id="61a95-113">The following is a summary of the environment configuration:</span></span>
> 
> |  | <span data-ttu-id="61a95-114">**Sitio principal**</span><span class="sxs-lookup"><span data-stu-id="61a95-114">**Primary site**</span></span> | <span data-ttu-id="61a95-115">**Sitio de réplica**</span><span class="sxs-lookup"><span data-stu-id="61a95-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="61a95-116">**Versión de Oracle**</span><span class="sxs-lookup"><span data-stu-id="61a95-116">**Oracle release**</span></span> |<span data-ttu-id="61a95-117">Oracle 12c Release 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="61a95-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="61a95-118">Oracle 12c Release 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="61a95-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="61a95-119">**Nombre de la máquina**</span><span class="sxs-lookup"><span data-stu-id="61a95-119">**Machine name**</span></span> |<span data-ttu-id="61a95-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="61a95-120">myVM1</span></span> |<span data-ttu-id="61a95-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="61a95-121">myVM2</span></span> |
> | <span data-ttu-id="61a95-122">**Sistema operativos**</span><span class="sxs-lookup"><span data-stu-id="61a95-122">**Operating system**</span></span> |<span data-ttu-id="61a95-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="61a95-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="61a95-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="61a95-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="61a95-125">**SID de Oracle**</span><span class="sxs-lookup"><span data-stu-id="61a95-125">**Oracle SID**</span></span> |<span data-ttu-id="61a95-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="61a95-126">CDB1</span></span> |<span data-ttu-id="61a95-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="61a95-127">CDB1</span></span> |
> | <span data-ttu-id="61a95-128">**Esquema de replicación**</span><span class="sxs-lookup"><span data-stu-id="61a95-128">**Replication schema**</span></span> |<span data-ttu-id="61a95-129">PRUEBA</span><span class="sxs-lookup"><span data-stu-id="61a95-129">TEST</span></span>|<span data-ttu-id="61a95-130">PRUEBA</span><span class="sxs-lookup"><span data-stu-id="61a95-130">TEST</span></span> |
> | <span data-ttu-id="61a95-131">**Propietario/réplica de Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="61a95-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="61a95-132">C##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="61a95-132">C##GGADMIN</span></span> |<span data-ttu-id="61a95-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="61a95-133">REPUSER</span></span> |
> | <span data-ttu-id="61a95-134">**Proceso de Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="61a95-134">**Golden Gate process**</span></span> |<span data-ttu-id="61a95-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="61a95-135">EXTORA</span></span> |<span data-ttu-id="61a95-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="61a95-136">REPORA</span></span>|


### <a name="sign-in-to-azure"></a><span data-ttu-id="61a95-137">Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="61a95-137">Sign in to Azure</span></span> 

<span data-ttu-id="61a95-138">Inicie sesión en su suscripción de Azure con el comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="61a95-138">Sign in to your Azure subscription with the [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="61a95-139">Después, siga las instrucciones que aparecen en pantalla.</span><span class="sxs-lookup"><span data-stu-id="61a95-139">Then follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="61a95-140">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="61a95-140">Create a resource group</span></span>

<span data-ttu-id="61a95-141">Cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="61a95-141">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="61a95-142">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y desde el que se pueden administrar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="61a95-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="61a95-143">En el ejemplo siguiente, se crea un grupo de recursos denominado `myResourceGroup` en la ubicación `westus`.</span><span class="sxs-lookup"><span data-stu-id="61a95-143">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="61a95-144">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="61a95-144">Create an availability set</span></span>

<span data-ttu-id="61a95-145">El paso siguiente es opcional pero recomendable.</span><span class="sxs-lookup"><span data-stu-id="61a95-145">The following step is optional but recommended.</span></span> <span data-ttu-id="61a95-146">Para más información, consulte la [guía de conjuntos de disponibilidad de Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="61a95-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="61a95-147">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="61a95-147">Create a virtual machine</span></span>

<span data-ttu-id="61a95-148">Cree la máquina virtual con el comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="61a95-148">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="61a95-149">En el ejemplo siguiente se crean dos máquinas virtuales, denominadas `myVM1` y `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="61a95-149">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="61a95-150">También se crean claves SSH, si aún no existen en una ubicación de claves predeterminada.</span><span class="sxs-lookup"><span data-stu-id="61a95-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="61a95-151">Para utilizar un conjunto específico de claves, utilice la opción `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="61a95-151">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="61a95-152">Cree myVM1 (principal):</span><span class="sxs-lookup"><span data-stu-id="61a95-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="61a95-153">Después de crear la máquina virtual, la CLI de Azure muestra información similar al ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="61a95-153">After the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="61a95-154">(Anote el valor de `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="61a95-154">(Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="61a95-155">Esta dirección se utiliza para acceder a la máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="61a95-155">This address is used to access the VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="61a95-156">Cree myVM2 (réplica):</span><span class="sxs-lookup"><span data-stu-id="61a95-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="61a95-157">Tome nota de `publicIpAddress` también después de su creación.</span><span class="sxs-lookup"><span data-stu-id="61a95-157">Take note of the `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="61a95-158">Apertura del puerto TCP para la conectividad</span><span class="sxs-lookup"><span data-stu-id="61a95-158">Open the TCP port for connectivity</span></span>

<span data-ttu-id="61a95-159">El siguiente paso consiste en configurar puntos de conexión externos, que le permiten tener acceso remoto a la base de datos de Oracle.</span><span class="sxs-lookup"><span data-stu-id="61a95-159">The next step is to configure external endpoints,  which enable you to access the Oracle database remotely.</span></span> <span data-ttu-id="61a95-160">Para configurar los puntos de conexión externos, ejecute los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="61a95-160">To configure the external endpoints, run the following commands.</span></span>

#### <a name="open-the-port-for-myvm1"></a><span data-ttu-id="61a95-161">Abra el puerto para myVM1:</span><span class="sxs-lookup"><span data-stu-id="61a95-161">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="61a95-162">Los resultados tienen que ser similares a la siguiente respuesta:</span><span class="sxs-lookup"><span data-stu-id="61a95-162">The results should look similar to the following response:</span></span>

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

#### <a name="open-the-port-for-myvm2"></a><span data-ttu-id="61a95-163">Abra el puerto para myVM2:</span><span class="sxs-lookup"><span data-stu-id="61a95-163">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="61a95-164">Conexión a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="61a95-164">Connect to the virtual machine</span></span>

<span data-ttu-id="61a95-165">Ejecute el comando siguiente para crear una sesión SSH con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61a95-165">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="61a95-166">Reemplace la dirección IP por el valor de `publicIpAddress` de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61a95-166">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="61a95-167">Creación de la base de datos en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="61a95-167">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="61a95-168">El software de Oracle ya está instalado en la imagen de Marketplace, por lo que el siguiente paso es instalar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="61a95-168">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="61a95-169">Ejecute el software como el superusuario "oracle":</span><span class="sxs-lookup"><span data-stu-id="61a95-169">Run the software as the 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="61a95-170">Cree la base de datos:</span><span class="sxs-lookup"><span data-stu-id="61a95-170">Create the database:</span></span>

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
<span data-ttu-id="61a95-171">Los resultados tienen que ser similares a la siguiente respuesta:</span><span class="sxs-lookup"><span data-stu-id="61a95-171">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="61a95-172">Establezca las variables ORACLE_SID y ORACLE_HOME.</span><span class="sxs-lookup"><span data-stu-id="61a95-172">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="61a95-173">Opcionalmente, puede agregar ORACLE_HOME y ORACLE_SID al archivo .bashrc, para que esta configuración se guarde para futuros inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="61a95-173">Optionally, you can add ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="61a95-174">Inicio del agente de escucha de Oracle</span><span class="sxs-lookup"><span data-stu-id="61a95-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-the-database-on-myvm2-replicate"></a><span data-ttu-id="61a95-175">Creación de la base de datos en myVM2 (réplica)</span><span class="sxs-lookup"><span data-stu-id="61a95-175">Create the database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="61a95-176">Cree la base de datos:</span><span class="sxs-lookup"><span data-stu-id="61a95-176">Create the database:</span></span>

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
<span data-ttu-id="61a95-177">Establezca las variables ORACLE_SID y ORACLE_HOME.</span><span class="sxs-lookup"><span data-stu-id="61a95-177">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="61a95-178">Opcionalmente, puede agregar ORACLE_HOME y ORACLE_SID al archivo .bashrc, para que esta configuración se guarde para futuros inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="61a95-178">Optionally, you can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="61a95-179">Inicio del agente de escucha de Oracle</span><span class="sxs-lookup"><span data-stu-id="61a95-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="61a95-180">Configuración de Golden Gate</span><span class="sxs-lookup"><span data-stu-id="61a95-180">Configure Golden Gate</span></span> 
<span data-ttu-id="61a95-181">Para configurar Golden Gate, realice los pasos de esta sección.</span><span class="sxs-lookup"><span data-stu-id="61a95-181">To configure Golden Gate, take the steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="61a95-182">Habilitar el modo de archivar registro en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="61a95-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="61a95-183">Habilite el registro forzado y asegúrese de que, al menos, haya un archivo de registro está presente.</span><span class="sxs-lookup"><span data-stu-id="61a95-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="61a95-184">Descargar el software de Golden Gate</span><span class="sxs-lookup"><span data-stu-id="61a95-184">Download Golden Gate software</span></span>
<span data-ttu-id="61a95-185">Para descargar y preparar el software Oracle Golden Gate, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="61a95-185">To download and prepare the Oracle Golden Gate software, complete the following steps:</span></span>

1. <span data-ttu-id="61a95-186">Descargue el archivo **fbo_ggs_Linux_x64_shiphome.zip** desde la [página de descarga de Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="61a95-186">Download the **fbo_ggs_Linux_x64_shiphome.zip** file from the [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="61a95-187">En el título de descarga **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, debe haber un conjunto de archivos .zip para descargar.</span><span class="sxs-lookup"><span data-stu-id="61a95-187">Under the download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files to download.</span></span>

2. <span data-ttu-id="61a95-188">Después de descargar los archivos .zip en el equipo cliente, use el protocolo de copia segura (SCP) para copiar los archivos a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61a95-188">After you download the .zip files to your client computer, use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="61a95-189">Mueva los archivos .zip a la carpeta **/opt**.</span><span class="sxs-lookup"><span data-stu-id="61a95-189">Move the .zip files to the **/opt** folder.</span></span> <span data-ttu-id="61a95-190">A continuación, cambie el propietario de los archivos de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="61a95-190">Then change the owner of the files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="61a95-191">Descomprima los archivos (instale la utilidad de descompresión de Linux si aún no está instalada):</span><span class="sxs-lookup"><span data-stu-id="61a95-191">Unzip the files (install the Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="61a95-192">Cambie el permiso:</span><span class="sxs-lookup"><span data-stu-id="61a95-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-the-client-and-vm-to-run-x11-for-windows-clients-only"></a><span data-ttu-id="61a95-193">Preparación del cliente y la máquina virtual para ejecutar x11 (solo para clientes Windows)</span><span class="sxs-lookup"><span data-stu-id="61a95-193">Prepare the client and VM to run x11 (for Windows clients only)</span></span>
<span data-ttu-id="61a95-194">Se trata de un paso opcional.</span><span class="sxs-lookup"><span data-stu-id="61a95-194">This is an optional step.</span></span> <span data-ttu-id="61a95-195">Puede omitir este paso si está utilizando un cliente Linux o ya ha configurado x11.</span><span class="sxs-lookup"><span data-stu-id="61a95-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="61a95-196">Descargue PuTTY y Xming en el equipo Windows:</span><span class="sxs-lookup"><span data-stu-id="61a95-196">Download PuTTY and Xming to your Windows computer:</span></span>

  * [<span data-ttu-id="61a95-197">Descargar PuTTY</span><span class="sxs-lookup"><span data-stu-id="61a95-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="61a95-198">Descargar Xming</span><span class="sxs-lookup"><span data-stu-id="61a95-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="61a95-199">Después de instalar PuTTY, en la carpeta PuTTY (por ejemplo, C:\Archivos de programa\PuTTY), ejecute puttygen.exe (PuTTY Key Generator).</span><span class="sxs-lookup"><span data-stu-id="61a95-199">After you install PuTTY, in the PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="61a95-200">En PuTTY Key Generator:</span><span class="sxs-lookup"><span data-stu-id="61a95-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="61a95-201">Para generar una clave, seleccione el botón **Generate** (Generar).</span><span class="sxs-lookup"><span data-stu-id="61a95-201">To generate a key, select the **Generate** button.</span></span>
  - <span data-ttu-id="61a95-202">Copie el contenido de la clave (**Ctrl+C**).</span><span class="sxs-lookup"><span data-stu-id="61a95-202">Copy the contents of the key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="61a95-203">Seleccione el botón **Save private key** (Guardar clave privada).</span><span class="sxs-lookup"><span data-stu-id="61a95-203">Select the **Save private key** button.</span></span>
  - <span data-ttu-id="61a95-204">Pase por alto la advertencia que aparece y seleccione **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="61a95-204">Ignore the warning that appears, and then select **OK**.</span></span>

    ![Captura de pantalla de la página de PuTTY Key Generator](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="61a95-206">En la máquina virtual, ejecute estos comandos:</span><span class="sxs-lookup"><span data-stu-id="61a95-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="61a95-207">Cree un archivo denominado **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="61a95-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="61a95-208">Pegue el contenido de la clave en este archivo y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="61a95-208">Paste the contents of the key in this file, and then save the file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="61a95-209">La clave debe contener la cadena `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="61a95-209">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="61a95-210">Además, el contenido de la clave debe ser una sola línea de texto.</span><span class="sxs-lookup"><span data-stu-id="61a95-210">Also, the contents of the key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="61a95-211">Inicie PuTTY.</span><span class="sxs-lookup"><span data-stu-id="61a95-211">Start PuTTY.</span></span> <span data-ttu-id="61a95-212">En el panel **Category** (Categoría), vaya a **Connection** > **SSH** > **Auth** (Conexión > SSH > Autenticación).</span><span class="sxs-lookup"><span data-stu-id="61a95-212">In the **Category** pane, select **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="61a95-213">En el cuadro **Private key file for authentication** (Archivo de clave privada para autenticación), vaya a la clave que generó antes.</span><span class="sxs-lookup"><span data-stu-id="61a95-213">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

  ![Captura de pantalla de la página para establecer la clave privada](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="61a95-215">En el panel **Category** (Categoría), vaya a **Connection** > **SSH** > **X11** (Conexión > SSH > X11).</span><span class="sxs-lookup"><span data-stu-id="61a95-215">In the **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="61a95-216">Después, seleccione el cuadro **Enable X11 forwarding** (Habilitar reenvío a X11).</span><span class="sxs-lookup"><span data-stu-id="61a95-216">Then select the **Enable X11 forwarding** box.</span></span>

  ![Captura de pantalla de la página para habilitar X11](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="61a95-218">En el panel **Category** (Categoría), vaya a **Session** (Sesión).</span><span class="sxs-lookup"><span data-stu-id="61a95-218">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="61a95-219">Escriba la información del host y seleccione **Open** (Abrir).</span><span class="sxs-lookup"><span data-stu-id="61a95-219">Enter the host information, and then select **Open**.</span></span>

  ![Captura de pantalla de la página Session (Sesión)](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="61a95-221">Instalar el software de Golden Gate</span><span class="sxs-lookup"><span data-stu-id="61a95-221">Install Golden Gate software</span></span>

<span data-ttu-id="61a95-222">Para instalar Oracle Golden Gate, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="61a95-222">To install Oracle Golden Gate, complete the following steps:</span></span>

1. <span data-ttu-id="61a95-223">Inicie sesión como oracle.</span><span class="sxs-lookup"><span data-stu-id="61a95-223">Sign in as oracle.</span></span> <span data-ttu-id="61a95-224">(Debe poder iniciar sesión sin que se le solicite una contraseña). Asegúrese de que se esté ejecutando Xming antes de comenzar la instalación.</span><span class="sxs-lookup"><span data-stu-id="61a95-224">(You should be able to sign in without being prompted for a password.) Make sure that Xming is running before you begin the installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="61a95-225">Seleccione 'Oracle GoldenGate para Oracle Database 12c'.</span><span class="sxs-lookup"><span data-stu-id="61a95-225">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="61a95-226">Después, seleccione **Siguiente** para continuar.</span><span class="sxs-lookup"><span data-stu-id="61a95-226">Then select **Next** to continue.</span></span>

  ![Captura de pantalla de la página Select Installation (Seleccionar instalación) en el instalador](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="61a95-228">Cambie la ubicación del software.</span><span class="sxs-lookup"><span data-stu-id="61a95-228">Change the software location.</span></span> <span data-ttu-id="61a95-229">A continuación, active la casilla **Start Manager** (Iniciar administrador) y especifique la ubicación de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="61a95-229">Then select  the **Start Manager** box and enter the database location.</span></span> <span data-ttu-id="61a95-230">Seleccione **Siguiente** para continuar.</span><span class="sxs-lookup"><span data-stu-id="61a95-230">Select **Next** to continue.</span></span>

  ![Captura de pantalla de la página Select Installation (Seleccionar instalación)](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="61a95-232">Cambie el directorio de inventario y, después, seleccione **Siguiente** para continuar.</span><span class="sxs-lookup"><span data-stu-id="61a95-232">Change the inventory directory, and then select **Next** to continue.</span></span>

  ![Captura de pantalla de la página Select Installation (Seleccionar instalación)](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="61a95-234">En la pantalla **Summary** (Resumen), seleccione **Install** (Instalar) para continuar.</span><span class="sxs-lookup"><span data-stu-id="61a95-234">On the **Summary** screen, select **Install** to continue.</span></span>

  ![Captura de pantalla de la página Select Installation (Seleccionar instalación) en el instalador](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="61a95-236">Puede que se le pida que ejecute un script como 'raíz'.</span><span class="sxs-lookup"><span data-stu-id="61a95-236">You might be prompted to run a script as 'root'.</span></span> <span data-ttu-id="61a95-237">Si es así, abra una sesión independiente, envíe un ssh a la máquina virtual, un sudo a la raíz y, después, ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="61a95-237">If so, open a separate session, ssh to the VM, sudo to root, and then run the script.</span></span> <span data-ttu-id="61a95-238">Seleccione **Aceptar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="61a95-238">Select **OK** continue.</span></span>

  ![Captura de pantalla de la página Select Installation (Seleccionar instalación)](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="61a95-240">Cuando haya finalizado la instalación, seleccione **Cerrar** para completar el proceso.</span><span class="sxs-lookup"><span data-stu-id="61a95-240">When the installation has finished, select **Close** to complete the process.</span></span>

  ![Captura de pantalla de la página Select Installation (Seleccionar instalación)](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="61a95-242">Configuración del servicio en myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="61a95-242">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="61a95-243">Cree o actualice el archivo tnsnames.ora:</span><span class="sxs-lookup"><span data-stu-id="61a95-243">Create or update the tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="61a95-244">Cree las cuentas de usuario y de propietario de Golden Gate.</span><span class="sxs-lookup"><span data-stu-id="61a95-244">Create the Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="61a95-245">La cuenta del propietario debe tener el prefijo C##.</span><span class="sxs-lookup"><span data-stu-id="61a95-245">The owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA to C##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="61a95-246">Cree las cuentas de usuario de prueba de Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="61a95-246">Create the Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="61a95-247">Configure el archivo de parámetros de extracción.</span><span class="sxs-lookup"><span data-stu-id="61a95-247">Configure the extract parameter file.</span></span>

 <span data-ttu-id="61a95-248">Inicie la interfaz de la línea de comandos de Golden Gate (ggsci):</span><span class="sxs-lookup"><span data-stu-id="61a95-248">Start the Golden gate command-line interface (ggsci):</span></span>

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. <span data-ttu-id="61a95-249">Agregue lo siguiente al archivo de parámetros de extracción (mediante comandos de vi).</span><span class="sxs-lookup"><span data-stu-id="61a95-249">Add the following to the EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="61a95-250">Presione la tecla Esc, ':wq!'</span><span class="sxs-lookup"><span data-stu-id="61a95-250">Press Esc key, ':wq!'</span></span> <span data-ttu-id="61a95-251">para guardar el archivo.</span><span class="sxs-lookup"><span data-stu-id="61a95-251">to save file.</span></span> 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. <span data-ttu-id="61a95-252">Register extract - extracción integrada:</span><span class="sxs-lookup"><span data-stu-id="61a95-252">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="61a95-253">Configure los puntos de control de extracción e inicie la extracción en tiempo real:</span><span class="sxs-lookup"><span data-stu-id="61a95-253">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request to MANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="61a95-254">En este paso, busque el SCN inicial, que se usará más adelante, en otra sección:</span><span class="sxs-lookup"><span data-stu-id="61a95-254">In this step, you find the starting SCN, which will be used later, in a different section:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="61a95-255">Configuración del servicio en myVM2 (réplica)</span><span class="sxs-lookup"><span data-stu-id="61a95-255">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="61a95-256">Cree o actualice el archivo tnsnames.ora:</span><span class="sxs-lookup"><span data-stu-id="61a95-256">Create or update the tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="61a95-257">Cree una cuenta de replicación:</span><span class="sxs-lookup"><span data-stu-id="61a95-257">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba to repuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="61a95-258">Cree una cuenta de usuario de prueba de Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="61a95-258">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="61a95-259">Archivo de parámetros REPLICAT para replicar los cambios:</span><span class="sxs-lookup"><span data-stu-id="61a95-259">REPLICAT parameter file to replicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="61a95-260">Contenido del archivo de parámetros REPORA:</span><span class="sxs-lookup"><span data-stu-id="61a95-260">Content of REPORA parameter file:</span></span>

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. <span data-ttu-id="61a95-261">Configure un punto de control de replicat:</span><span class="sxs-lookup"><span data-stu-id="61a95-261">Set up a replicat checkpoint:</span></span>

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-the-replication-myvm1-and-myvm2"></a><span data-ttu-id="61a95-262">Configuración de la replicación (myVM1 y myVM2)</span><span class="sxs-lookup"><span data-stu-id="61a95-262">Set up the replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="61a95-263">1. Configure la replicación en myVM2 (réplica).</span><span class="sxs-lookup"><span data-stu-id="61a95-263">1. Set up the replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="61a95-264">Actualice el archivo con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="61a95-264">Update the file with the following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="61a95-265">Después, reinicie el servicio de administrador:</span><span class="sxs-lookup"><span data-stu-id="61a95-265">Then restart the Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-the-replication-on-myvm1-primary"></a><span data-ttu-id="61a95-266">2. Configure la replicación en myVM1 (principal).</span><span class="sxs-lookup"><span data-stu-id="61a95-266">2. Set up the replication on myVM1 (primary)</span></span>

<span data-ttu-id="61a95-267">Inicie la carga inicial y busque errores:</span><span class="sxs-lookup"><span data-stu-id="61a95-267">Start the initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="61a95-268">3. Configure la replicación en myVM2 (réplica).</span><span class="sxs-lookup"><span data-stu-id="61a95-268">3. Set up the replication on myVM2 (replicate)</span></span>

<span data-ttu-id="61a95-269">Cambie el número de SCN con el número que obtuvo antes:</span><span class="sxs-lookup"><span data-stu-id="61a95-269">Change the SCN number with the number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="61a95-270">Ha empezado la replicación y puede probarla mediante la inserción de nuevos registros a las tablas de prueba.</span><span class="sxs-lookup"><span data-stu-id="61a95-270">The replication has begun, and you can test it by inserting new records to TEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="61a95-271">Visualización del estado del trabajo y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="61a95-271">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="61a95-272">Ver informes</span><span class="sxs-lookup"><span data-stu-id="61a95-272">View reports</span></span>
<span data-ttu-id="61a95-273">Para ver los informes en myVM1, ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="61a95-273">To view reports on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="61a95-274">Para ver los informes en myVM2, ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="61a95-274">To view reports on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="61a95-275">Visualización del estado e historial</span><span class="sxs-lookup"><span data-stu-id="61a95-275">View status and history</span></span>
<span data-ttu-id="61a95-276">Para ver el estado e historial en myVM1, ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="61a95-276">To view status and history on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="61a95-277">Para ver el estado e historial en myVM2, ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="61a95-277">To view status and history on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="61a95-278">Este paso completa la instalación y configuración de Golden Gate en Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="61a95-278">This completes the installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="61a95-279">Eliminación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="61a95-279">Delete the virtual machine</span></span>

<span data-ttu-id="61a95-280">Cuando ya no los necesite, se puede usar el comando siguiente para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="61a95-280">When it's no longer needed, the following command can be used to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="61a95-281">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61a95-281">Next steps</span></span>

[<span data-ttu-id="61a95-282">Tutorial de creación de máquinas virtuales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="61a95-282">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="61a95-283">Ejemplos de la CLI de implementación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="61a95-283">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
