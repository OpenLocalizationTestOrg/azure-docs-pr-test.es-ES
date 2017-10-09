---
title: "base de datos aaaBack seguridad y recuperar una base de datos de Oracle 12C en una máquina virtual de Linux de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooback seguridad y recuperar una base de datos de Oracle 12C base de datos en el entorno de Azure."
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
ms.date: 5/17/2017
ms.author: rclaus
ms.openlocfilehash: 68846f4efce5eabdb71cd71772e003838154e93b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="c91fc-103">Copia de seguridad y recuperación de una base de datos de Oracle Database 12c en una máquina virtual Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="c91fc-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="c91fc-104">Puede usar toocreate de CLI de Azure y administrar recursos de Azure en un símbolo del sistema o utilizar secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="c91fc-104">You can use Azure CLI toocreate and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="c91fc-105">En este artículo, utilizamos toodeploy de secuencias de comandos de CLI de Azure una base de datos de Oracle Database 12C desde una imagen de la Galería de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c91fc-105">In this article, we use Azure CLI scripts toodeploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="c91fc-106">Antes de comenzar, asegúrese de que esté instalada la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c91fc-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="c91fc-107">Para obtener más información, vea hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c91fc-107">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="c91fc-108">Preparar el entorno de Hola</span><span class="sxs-lookup"><span data-stu-id="c91fc-108">Prepare hello environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="c91fc-109">Paso 1: Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c91fc-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="c91fc-110">proceso de copia de seguridad y recuperación de hello tooperform, primero debe crear una VM de Linux que tiene una instancia instalada de Oracle Database 12C.</span><span class="sxs-lookup"><span data-stu-id="c91fc-110">tooperform hello backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="c91fc-111">imagen de Marketplace de Hello usas hello toocreate máquina virtual se denomina *Oracle: Oracle-base de datos-Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="c91fc-111">hello Marketplace image you use toocreate hello VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="c91fc-112">toolearn toocreate una base de datos de Oracle, vea hello [Oracle crear inicio rápido de base de datos](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="c91fc-112">toolearn how toocreate an Oracle database, see hello [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-toohello-vm"></a><span data-ttu-id="c91fc-113">Paso 2: Conectar toohello VM</span><span class="sxs-lookup"><span data-stu-id="c91fc-113">Step 2: Connect toohello VM</span></span>

*   <span data-ttu-id="c91fc-114">toocreate una sesión de Shell seguro (SSH) con hello de máquina virtual, use Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="c91fc-114">toocreate a Secure Shell (SSH) session with hello VM, use hello following command.</span></span> <span data-ttu-id="c91fc-115">Reemplace la dirección IP de Hola y combinación de nombre de host de hello con hello `publicIpAddress` valor para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c91fc-115">Replace hello IP address and hello host name combination with hello `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a><span data-ttu-id="c91fc-116">Paso 3: Preparar la base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="c91fc-116">Step 3: Prepare hello database</span></span>

1.  <span data-ttu-id="c91fc-117">En este paso se presupone que tiene una instancia de Oracle (cdb1) que se ejecuta en una máquina virtual denominada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c91fc-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="c91fc-118">Ejecute hello *oracle* raíz de superusuario y, a continuación, el agente de escucha de inicializar hello:</span><span class="sxs-lookup"><span data-stu-id="c91fc-118">Run hello *oracle* superuser root, and then initialize hello listener:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
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

2.  <span data-ttu-id="c91fc-119">(Opcional) Asegúrese de que la base de datos de hello está en modo de registro de archivo:</span><span class="sxs-lookup"><span data-stu-id="c91fc-119">(Optional) Make sure hello database is in archive log mode:</span></span>

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
    SQL> ALTER SYSTEM SWITCH LOGFILE;
    ```
3.  <span data-ttu-id="c91fc-120">(Opcional) Cree un tabla tootest Hola de confirmación:</span><span class="sxs-lookup"><span data-stu-id="c91fc-120">(Optional) Create a table tootest hello commit:</span></span>

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session tooscott;
    Grant succeeded.
    SQL> grant create table tooscott;
    Grant succeeded.
    SQL> alter user scott quota 100M on users;
    User altered.
    SQL> connect scott/tiger
    SQL> create table scott_table(col1 number, col2 varchar2(50));
    Table created.
    SQL> insert into scott_Table VALUES(1,'Line 1');
    1 row created.
    SQL> commit;
    Commit complete.
    ```
4.  <span data-ttu-id="c91fc-121">Comprobar o cambiar el tamaño y la ubicación del archivo de copia de seguridad de hello:</span><span class="sxs-lookup"><span data-stu-id="c91fc-121">Verify or change hello backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="c91fc-122">Use tooback Oracle Recovery Manager (RMAN) la base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="c91fc-122">Use Oracle Recovery Manager (RMAN) tooback up hello database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="c91fc-123">Paso 4: Copias de seguridad coherentes con la aplicación para máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="c91fc-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="c91fc-124">Las copias de seguridad coherentes con la aplicación es una nueva característica de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="c91fc-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="c91fc-125">Puede crear y seleccionar tooexecute scripts antes y después de la instantánea de la VM de hello (anterior a la instantánea y posterior a la instantánea).</span><span class="sxs-lookup"><span data-stu-id="c91fc-125">You can create and select scripts tooexecute before and after hello VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="c91fc-126">Descargar archivo de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="c91fc-126">Download hello JSON file.</span></span>

    <span data-ttu-id="c91fc-127">Descargue VMSnapshotScriptPluginConfig.json desde https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span><span class="sxs-lookup"><span data-stu-id="c91fc-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="c91fc-128">contenido del archivo Hello tener un aspecto similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="c91fc-128">hello file contents look similar toohello following:</span></span>

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "",
        "postScriptLocation" : "",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

2. <span data-ttu-id="c91fc-129">Crear carpeta de /etc/azure de hello en hello VM:</span><span class="sxs-lookup"><span data-stu-id="c91fc-129">Create hello /etc/azure folder on hello VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="c91fc-130">Copie el archivo JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="c91fc-130">Copy hello JSON file.</span></span>

    <span data-ttu-id="c91fc-131">Copie la carpeta de VMSnapshotScriptPluginConfig.json toohello /etc/azure.</span><span class="sxs-lookup"><span data-stu-id="c91fc-131">Copy VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.</span></span>

4. <span data-ttu-id="c91fc-132">Editar archivo de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="c91fc-132">Edit hello JSON file.</span></span>

    <span data-ttu-id="c91fc-133">Editar Hola de hello VMSnapshotScriptPluginConfig.json archivo tooinclude `PreScriptLocation` y `PostScriptlocation` parámetros.</span><span class="sxs-lookup"><span data-stu-id="c91fc-133">Edit hello VMSnapshotScriptPluginConfig.json file tooinclude hello `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="c91fc-134">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c91fc-134">For example:</span></span>

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "/etc/azure/pre_script.sh",
        "postScriptLocation" : "/etc/azure/post_script.sh",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

5. <span data-ttu-id="c91fc-135">Crear archivos de script anterior a la instantánea y posterior a la instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-135">Create hello pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="c91fc-136">Este es un ejemplo de scripts anteriores y posteriores a la instantánea para una "copia de seguridad fría" (una copia de seguridad sin conexión, con apagado y reinicio):</span><span class="sxs-lookup"><span data-stu-id="c91fc-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="c91fc-137">Para /etc/azure/pre_script.sh:</span><span class="sxs-lookup"><span data-stu-id="c91fc-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="c91fc-138">Para /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="c91fc-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="c91fc-139">Este es un ejemplo de scripts anteriores y posteriores a la instantánea para una "copia de seguridad en caliente" (una copia de seguridad con conexión):</span><span class="sxs-lookup"><span data-stu-id="c91fc-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="c91fc-140">Para /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="c91fc-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="c91fc-141">Para /etc/azure/pre_script.sql, modifique el contenido de Hola de archivo hello según sus requisitos:</span><span class="sxs-lookup"><span data-stu-id="c91fc-141">For /etc/azure/pre_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="c91fc-142">Para /etc/azure/post_script.sql, modifique el contenido de Hola de archivo hello según sus requisitos:</span><span class="sxs-lookup"><span data-stu-id="c91fc-142">For /etc/azure/post_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="c91fc-143">Cambie los permisos de archivo:</span><span class="sxs-lookup"><span data-stu-id="c91fc-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="c91fc-144">Probar scripts de Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-144">Test hello scripts.</span></span>

    <span data-ttu-id="c91fc-145">secuencias de comandos de tootest hello, en primer lugar, inicie sesión como raíz.</span><span class="sxs-lookup"><span data-stu-id="c91fc-145">tootest hello scripts, first, sign in as root.</span></span> <span data-ttu-id="c91fc-146">Después, asegúrese de que no hay ningún error:</span><span class="sxs-lookup"><span data-stu-id="c91fc-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="c91fc-147">Para más información, vea [Copia de seguridad coherente con la aplicación para máquinas virtuales Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span><span class="sxs-lookup"><span data-stu-id="c91fc-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a><span data-ttu-id="c91fc-148">Paso 5: Usar servicios de recuperación de Azure almacenes de credenciales tooback seguridad Hola VM</span><span class="sxs-lookup"><span data-stu-id="c91fc-148">Step 5: Use Azure Recovery Services vaults tooback up hello VM</span></span>

1.  <span data-ttu-id="c91fc-149">En el portal de Azure de Hola, busque **servicios de recuperación de los almacenes de credenciales**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-149">In hello Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Página de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="c91fc-151">En hello **servicios de recuperación de los almacenes de credenciales** hoja, tooadd un nuevo almacén, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-151">On hello **Recovery Services vaults** blade, tooadd a new vault, click **Add**.</span></span>

    ![Página para agregar almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="c91fc-153">toocontinue, haga clic en **myVault**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-153">toocontinue, click **myVault**.</span></span>

    ![Página de detalles de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="c91fc-155">En hello **myVault** hoja, haga clic en **copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-155">On hello **myVault** blade, click **Backup**.</span></span>

    ![Página de la copia de seguridad de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="c91fc-157">En hello **objetivo de copia de seguridad** hoja, valores de uso Hola predeterminados de **Azure** y **Máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-157">On hello **Backup Goal** blade, use hello default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="c91fc-158">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-158">Click **OK**.</span></span>

    ![Página de detalles de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="c91fc-160">Para **Directiva de copia de seguridad**, use **DefaultPolicy** (Directiva predeterminada) o haga clic en **Crear nueva directiva**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="c91fc-161">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-161">Click **OK**.</span></span>

    ![Página de detalles de la directiva de copia de seguridad de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="c91fc-163">En hello **seleccionar las máquinas virtuales** hoja, seleccione hello **myVM1** casilla de verificación y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-163">On hello **Select virtual machines** blade, select hello **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="c91fc-164">Haga clic en hello **habilitar copia de seguridad** botón.</span><span class="sxs-lookup"><span data-stu-id="c91fc-164">Click hello **Enable backup** button.</span></span>

    ![Página de detalles copia de seguridad de toohello de elementos almacenes de servicios de recuperación](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="c91fc-166">Tras hacer clic en **habilitar copia de seguridad**, proceso de copia de seguridad de hello no se inicia hasta que expire hello hora programada.</span><span class="sxs-lookup"><span data-stu-id="c91fc-166">After you click **Enable backup**, hello backup process doesn't start until hello scheduled time expires.</span></span> <span data-ttu-id="c91fc-167">tooset la una copia de seguridad inmediata, completa Hola paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="c91fc-167">tooset up an immediate backup, complete hello next step.</span></span>

8.  <span data-ttu-id="c91fc-168">En hello **myVault - elementos de copia de seguridad** hoja, en **recuento de elementos de copia de seguridad**, seleccione el número de elementos de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-168">On hello **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select hello backup item count.</span></span>

    ![Página de detalles del almacén myVault de Recovery Services](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="c91fc-170">En hello **elementos de copia de seguridad (Máquina Virtual de Azure)** hoja, lado derecho de Hola de página de hello, haga clic en puntos suspensivos hello (**...** ) y, a continuación, haga clic en **una copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-170">On hello **Backup Items (Azure Virtual Machine)** blade, on hello right side of hello page, click hello ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Comando Realizar copia de seguridad ahora de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="c91fc-172">Haga clic en hello **copia de seguridad** botón.</span><span class="sxs-lookup"><span data-stu-id="c91fc-172">Click hello **Backup** button.</span></span> <span data-ttu-id="c91fc-173">Espere a que hello toofinish de proceso de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c91fc-173">Wait for hello backup process toofinish.</span></span> <span data-ttu-id="c91fc-174">A continuación, ir demasiado[paso 6: quitar archivos de base de datos de hello](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="c91fc-174">Then, go too[Step 6: Remove hello database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="c91fc-175">Haga clic en estado de hello tooview de trabajo de copia de seguridad de hello, **trabajos**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-175">tooview hello status of hello backup job, click **Jobs**.</span></span>

    ![Página del trabajo de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="c91fc-177">estado de Hola de trabajo de copia de seguridad de Hola aparece en hello después de la imagen:</span><span class="sxs-lookup"><span data-stu-id="c91fc-177">hello status of hello backup job appears in hello following image:</span></span>

    ![Página del trabajo de los almacenes de Recovery Services con el estado](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="c91fc-179">Para una copia de seguridad coherentes con la aplicación, resuelva los errores en el archivo de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="c91fc-179">For an application-consistent backup, address any errors in hello log file.</span></span> <span data-ttu-id="c91fc-180">archivo de registro de Hello se encuentra en /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span><span class="sxs-lookup"><span data-stu-id="c91fc-180">hello log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-hello-database-files"></a><span data-ttu-id="c91fc-181">Paso 6: Quitar archivos de base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="c91fc-181">Step 6: Remove hello database files</span></span> 
<span data-ttu-id="c91fc-182">Más adelante en este artículo, aprenderá cómo tootest Hola proceso de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c91fc-182">Later in this article, you'll learn how tootest hello recovery process.</span></span> <span data-ttu-id="c91fc-183">Para poder probar el proceso de recuperación de hello, tener archivos de base de datos de tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-183">Before you can test hello recovery process, you have tooremove hello database files.</span></span>

1.  <span data-ttu-id="c91fc-184">Quitar archivos de copia de seguridad y el espacio de tablas de hello:</span><span class="sxs-lookup"><span data-stu-id="c91fc-184">Remove hello tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="c91fc-185">(Opcional) Cierre la instancia de Oracle hello:</span><span class="sxs-lookup"><span data-stu-id="c91fc-185">(Optional) Shut down hello Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a><span data-ttu-id="c91fc-186">Restaure los archivos de hello eliminado de hello que Servicios de recuperación de los almacenes de credenciales</span><span class="sxs-lookup"><span data-stu-id="c91fc-186">Restore hello deleted files from hello Recovery Services vaults</span></span>
<span data-ttu-id="c91fc-187">hello toorestore elimina archivos, Hola completa siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="c91fc-187">toorestore hello deleted files, complete hello following steps:</span></span>

1. <span data-ttu-id="c91fc-188">Hola portal de Azure, busque hello *myVault* elemento de los almacenes de servicios de recuperación de credenciales.</span><span class="sxs-lookup"><span data-stu-id="c91fc-188">In hello Azure portal, search for hello *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="c91fc-189">En hello **Introducción** hoja, en **elementos de copia de seguridad**, seleccione Hola número de elementos.</span><span class="sxs-lookup"><span data-stu-id="c91fc-189">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Elementos de copia de seguridad del almacén myVault de Recovery Services](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="c91fc-191">En **recuento de elementos de copia de seguridad**, seleccione Hola número de elementos.</span><span class="sxs-lookup"><span data-stu-id="c91fc-191">Under **BACKUP ITEM COUNT**, select hello number of items.</span></span>

    ![Número de elementos de copia de seguridad de máquinas virtuales de Azure en los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="c91fc-193">En hello **myvm1** hoja, haga clic en **recuperación de archivos (vista previa)**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-193">On hello **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Captura de pantalla de hello servicios de recuperación de almacenes de credenciales de la página de recuperación de archivos](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="c91fc-195">En hello **recuperación de archivos (vista previa)** panel, haga clic en **descargar Script**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-195">On hello **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="c91fc-196">A continuación, guarde el archivo tooa carpeta de descarga (.sh) de hello en el equipo cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-196">Then, save hello download (.sh) file tooa folder on hello client computer.</span></span>

    ![Operaciones de guardado del archivo de script descargado](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="c91fc-198">Copie hello .sh archivo toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c91fc-198">Copy hello .sh file toohello VM.</span></span>

    <span data-ttu-id="c91fc-199">Hola de ejemplo siguiente muestra cómo toouse una toomove de comando de copia de seguridad (scp) Hola archivo toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c91fc-199">hello following example shows how you toouse a secure copy (scp) command toomove hello file toohello VM.</span></span> <span data-ttu-id="c91fc-200">También puede copiar el Portapapeles de hello contenido toohello y, a continuación, pegar Hola contenido en un nuevo archivo que se ha configurado en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c91fc-200">You also can copy hello contents toohello clipboard, and then paste hello contents in a new file that is set up on hello VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c91fc-201">En el siguiente ejemplo de Hola, asegúrese de que se actualizan los valores de dirección y la carpeta de la IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-201">In hello following example, ensure that you update hello IP address and folder values.</span></span> <span data-ttu-id="c91fc-202">valores de Hello deben asignar la carpeta toohello donde se guarda el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="c91fc-202">hello values must map toohello folder where hello file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="c91fc-203">Cambie el archivo de hello, por lo que es propiedad de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-203">Change hello file, so that it's owned by hello root.</span></span>

    <span data-ttu-id="c91fc-204">En el siguiente ejemplo de Hola, cambiar archivo hello por lo que es propiedad de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-204">In hello following example, change hello file so that it's owned by hello root.</span></span> <span data-ttu-id="c91fc-205">Después, cambie los permisos.</span><span class="sxs-lookup"><span data-stu-id="c91fc-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="c91fc-206">Hello en el ejemplo siguiente se muestra lo que verá después de ejecutar Hola anterior secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="c91fc-206">hello following example shows what you should see after you run hello preceding script.</span></span> <span data-ttu-id="c91fc-207">Cuando se le pide toocontinue, escriba **Y**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-207">When you're prompted toocontinue, enter **Y**.</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    hello script requires 'open-iscsi' and 'lshw' toorun.
    Do you want us tooinstall 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' toocontinue with installation, 'N' tooabort hello operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting toorecovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of hello recovery point toothis machine...

    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

7. <span data-ttu-id="c91fc-208">Acceso toohello montar volúmenes se ha confirmado.</span><span class="sxs-lookup"><span data-stu-id="c91fc-208">Access toohello mounted volumes is confirmed.</span></span>

    <span data-ttu-id="c91fc-209">tooexit, escriba **preguntas**y, a continuación, busque Hola montada volúmenes.</span><span class="sxs-lookup"><span data-stu-id="c91fc-209">tooexit, enter **q**, and then search for hello mounted volumes.</span></span> <span data-ttu-id="c91fc-210">toocreate una lista de hello agrega volúmenes, en un símbolo del sistema, escriba **df -k**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-210">toocreate a list of hello added volumes, at a command prompt, enter **df -k**.</span></span>

    ![comando de Hello df -k](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="c91fc-212">Hola de uso después de que falta un script toocopy Hola archivos toohello atrás carpetas:</span><span class="sxs-lookup"><span data-stu-id="c91fc-212">Use hello following script toocopy hello missing files back toohello folders:</span></span>

    ```bash
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cp *.bkp /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cd /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # chown oracle:oinstall *.bkp
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/oradata/cdb1
    # cp *.dbf /u01/app/oracle/oradata/cdb1
    # cd /u01/app/oracle/oradata/cdb1
    # chown oracle:oinstall *.dbf
    ```
9. <span data-ttu-id="c91fc-213">En la siguiente secuencia de comandos de hello, usar base de datos RMAN toorecover hello:</span><span class="sxs-lookup"><span data-stu-id="c91fc-213">In hello following script, use RMAN toorecover hello database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="c91fc-214">Desmonte el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-214">Unmount hello disk.</span></span>

    <span data-ttu-id="c91fc-215">En el portal de Azure, en Hola Hola **recuperación de archivos (vista previa)** hoja, haga clic en **desmontar discos**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-215">In hello Azure portal, on hello **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Comando Unmount Disks (Desmontar discos)](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a><span data-ttu-id="c91fc-217">Restaurar Hola toda máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c91fc-217">Restore hello entire VM</span></span>

<span data-ttu-id="c91fc-218">En lugar de restaurar los archivos eliminado de Hola de almacenes de servicios de recuperación de hello, puede restaurar Hola toda máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c91fc-218">Instead of restoring hello deleted files from hello Recovery Services vaults, you can restore hello entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="c91fc-219">Paso 1: Eliminar myVM</span><span class="sxs-lookup"><span data-stu-id="c91fc-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="c91fc-220">Hola portal de Azure, vaya toohello **myVM1** del almacén y, a continuación, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-220">In hello Azure portal, go toohello **myVM1** vault, and then select **Delete**.</span></span>

    ![Comando Eliminar almacén](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a><span data-ttu-id="c91fc-222">Paso 2: Recuperar Hola VM</span><span class="sxs-lookup"><span data-stu-id="c91fc-222">Step 2: Recover hello VM</span></span>

1.  <span data-ttu-id="c91fc-223">Vaya demasiado**servicios de recuperación de los almacenes de credenciales**y, a continuación, seleccione **myVault**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-223">Go too**Recovery Services vaults**, and then select **myVault**.</span></span>

    ![Entrada de myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="c91fc-225">En hello **Introducción** hoja, en **elementos de copia de seguridad**, seleccione Hola número de elementos.</span><span class="sxs-lookup"><span data-stu-id="c91fc-225">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Elementos de copias de seguridad de myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="c91fc-227">En hello **elementos de copia de seguridad (Máquina Virtual de Azure)** hoja, seleccione **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-227">On hello **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![Página de la máquina virtual de recuperación](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="c91fc-229">En hello **myvm1** hoja, haga clic en el botón de puntos suspensivos hello (**...** ) y, a continuación, haga clic en **VM restaurar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-229">On hello **myvm1** blade, click hello ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![Comando Restaurar máquina virtual](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="c91fc-231">En hello **Seleccionar punto de restauración** hoja, elemento de select Hola que desee toorestore y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-231">On hello **Select restore point** blade, select hello item that you want toorestore, and then click **OK**.</span></span>

    ![Punto de restauración de hello SELECT](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="c91fc-233">Si ha habilitado la copia de seguridad coherente con la aplicación, aparece una barra vertical de color azul.</span><span class="sxs-lookup"><span data-stu-id="c91fc-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="c91fc-234">En hello **restaurar la configuración** hoja, nombre de la máquina virtual seleccione hello, seleccione el grupo de recursos de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-234">On hello **Restore configuration** blade, select hello virtual machine name, select hello resource group, and then click **OK**.</span></span>

    ![Valores de configuración de la restauración](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="c91fc-236">Hola toorestore máquina virtual, haga clic en hello **restaurar** botón.</span><span class="sxs-lookup"><span data-stu-id="c91fc-236">toorestore hello VM, click hello **Restore** button.</span></span>

8.  <span data-ttu-id="c91fc-237">Haga clic en estado de hello tooview del proceso de restauración de hello, **trabajos**y, a continuación, haga clic en **trabajos de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-237">tooview hello status of hello restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Comando de estado de los trabajos de copia de seguridad](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="c91fc-239">Hello en la ilustración siguiente se muestra hello estado del proceso de restauración de hello:</span><span class="sxs-lookup"><span data-stu-id="c91fc-239">hello following figure shows hello status of hello restore process:</span></span>

    ![Estado del proceso de restauración de Hola](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a><span data-ttu-id="c91fc-241">Paso 3: Establecer la dirección IP pública Hola</span><span class="sxs-lookup"><span data-stu-id="c91fc-241">Step 3: Set hello public IP address</span></span>
<span data-ttu-id="c91fc-242">Hola que se restaura la máquina virtual después de haber configurado la dirección IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-242">After hello VM is restored, set up hello public IP address.</span></span>

1.  <span data-ttu-id="c91fc-243">En el cuadro de búsqueda de hello, escriba **dirección IP pública**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-243">In hello search box, enter **public IP address**.</span></span>

    ![Lista de direcciones IP públicas](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="c91fc-245">En hello **direcciones IP públicas** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-245">On hello **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="c91fc-246">En hello **Crear dirección IP pública** hoja, para **nombre**, seleccione el nombre de IP pública de Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-246">On hello **Create public IP address** blade, for **Name**, select hello public IP name.</span></span> <span data-ttu-id="c91fc-247">En **Grupo de recursos**, seleccione **Usar existente**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="c91fc-248">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-248">Then, click **Create**.</span></span>

    ![Creación de la dirección IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="c91fc-250">tooassociate Hola la dirección IP pública con interfaz de red de Hola para hello VM, busque y seleccione **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-250">tooassociate hello public IP address with hello network interface for hello VM, search for and select **myVMip**.</span></span> <span data-ttu-id="c91fc-251">Después, haga clic en **Asociar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-251">Then, click **Associate**.</span></span>

    ![Asociación de la dirección IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="c91fc-253">Para **Tipo de recurso**, seleccione **Interfaz de red**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="c91fc-254">Seleccione Hola interfaz de red utilizado por la instancia de hello myVM y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c91fc-254">Select hello network interface that is used by hello myVM instance, and then click **OK**.</span></span>

    ![Selección del tipo de recurso y los valores de NIC](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="c91fc-256">Busque y abra la instancia de Hola de myVM que se transfieren desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="c91fc-256">Search for and open hello instance of myVM that is ported from hello portal.</span></span> <span data-ttu-id="c91fc-257">Hello dirección IP que está asociado con hello VM aparece en hello myVM **Introducción** hoja.</span><span class="sxs-lookup"><span data-stu-id="c91fc-257">hello IP address that is associated with hello VM appears on hello myVM **Overview** blade.</span></span>

    ![Valor de la dirección IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a><span data-ttu-id="c91fc-259">Paso 4: Conectar toohello VM</span><span class="sxs-lookup"><span data-stu-id="c91fc-259">Step 4: Connect toohello VM</span></span>

*   <span data-ttu-id="c91fc-260">tooconnect toohello de máquina virtual, use Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="c91fc-260">tooconnect toohello VM, use hello following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a><span data-ttu-id="c91fc-261">Paso 5: Comprobar si la base de datos de hello es accesible</span><span class="sxs-lookup"><span data-stu-id="c91fc-261">Step 5: Test whether hello database is accessible</span></span>
*   <span data-ttu-id="c91fc-262">tootest accesibilidad, Hola de uso siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="c91fc-262">tootest accessibility, use hello following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="c91fc-263">La base de datos si hello **inicio** comando genera un error, la base de datos de toorecover hello, consulte [paso 6: base de datos de uso RMAN toorecover hello](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="c91fc-263">If hello database **startup** command generates an error, toorecover hello database, see [Step 6: Use RMAN toorecover hello database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a><span data-ttu-id="c91fc-264">Paso 6: Base de datos (opcional) utilice RMAN toorecover Hola</span><span class="sxs-lookup"><span data-stu-id="c91fc-264">Step 6: (Optional) Use RMAN toorecover hello database</span></span>
*   <span data-ttu-id="c91fc-265">toorecover Hola base de datos, Hola de uso siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="c91fc-265">toorecover hello database, use hello following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="c91fc-266">copia de seguridad de Hola y de recuperación de base de datos de hello Oracle Database 12C en una máquina virtual Linux de Azure ya está completado.</span><span class="sxs-lookup"><span data-stu-id="c91fc-266">hello backup and recovery of hello Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="c91fc-267">Eliminar Hola VM</span><span class="sxs-lookup"><span data-stu-id="c91fc-267">Delete hello VM</span></span>

<span data-ttu-id="c91fc-268">Cuando ya no necesita hello VM, puede usar Hola después el grupo de recursos de comando tooremove hello, Hola VM y todos ellos relacionados con recursos:</span><span class="sxs-lookup"><span data-stu-id="c91fc-268">When you no longer need hello VM, you can use hello following command tooremove hello resource group, hello VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c91fc-269">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c91fc-269">Next steps</span></span>

[<span data-ttu-id="c91fc-270">Tutorial: Creación de máquinas virtuales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="c91fc-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="c91fc-271">Ejemplos de la CLI de Azure para implementación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c91fc-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)



