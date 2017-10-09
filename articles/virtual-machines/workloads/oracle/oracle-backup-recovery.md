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
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>Copia de seguridad y recuperación de una base de datos de Oracle Database 12c en una máquina virtual Linux de Azure

Puede usar toocreate de CLI de Azure y administrar recursos de Azure en un símbolo del sistema o utilizar secuencias de comandos. En este artículo, utilizamos toodeploy de secuencias de comandos de CLI de Azure una base de datos de Oracle Database 12C desde una imagen de la Galería de Azure Marketplace.

Antes de comenzar, asegúrese de que esté instalada la CLI de Azure. Para obtener más información, vea hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Preparar el entorno de Hola

### <a name="step-1-prerequisites"></a>Paso 1: Requisitos previos

*   proceso de copia de seguridad y recuperación de hello tooperform, primero debe crear una VM de Linux que tiene una instancia instalada de Oracle Database 12C. imagen de Marketplace de Hello usas hello toocreate máquina virtual se denomina *Oracle: Oracle-base de datos-Ee:12.1.0.2:latest*.

    toolearn toocreate una base de datos de Oracle, vea hello [Oracle crear inicio rápido de base de datos](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).


### <a name="step-2-connect-toohello-vm"></a>Paso 2: Conectar toohello VM

*   toocreate una sesión de Shell seguro (SSH) con hello de máquina virtual, use Hola siguiente comando. Reemplace la dirección IP de Hola y combinación de nombre de host de hello con hello `publicIpAddress` valor para la máquina virtual.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a>Paso 3: Preparar la base de datos de Hola

1.  En este paso se presupone que tiene una instancia de Oracle (cdb1) que se ejecuta en una máquina virtual denominada *myVM*.

    Ejecute hello *oracle* raíz de superusuario y, a continuación, el agente de escucha de inicializar hello:

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

2.  (Opcional) Asegúrese de que la base de datos de hello está en modo de registro de archivo:

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
3.  (Opcional) Cree un tabla tootest Hola de confirmación:

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
4.  Comprobar o cambiar el tamaño y la ubicación del archivo de copia de seguridad de hello:

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. Use tooback Oracle Recovery Manager (RMAN) la base de datos de hello:

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>Paso 4: Copias de seguridad coherentes con la aplicación para máquinas virtuales Linux

Las copias de seguridad coherentes con la aplicación es una nueva característica de Azure Backup. Puede crear y seleccionar tooexecute scripts antes y después de la instantánea de la VM de hello (anterior a la instantánea y posterior a la instantánea).

1. Descargar archivo de hello JSON.

    Descargue VMSnapshotScriptPluginConfig.json desde https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig. contenido del archivo Hello tener un aspecto similar siguiente toohello:

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

2. Crear carpeta de /etc/azure de hello en hello VM:

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. Copie el archivo JSON de hello.

    Copie la carpeta de VMSnapshotScriptPluginConfig.json toohello /etc/azure.

4. Editar archivo de hello JSON.

    Editar Hola de hello VMSnapshotScriptPluginConfig.json archivo tooinclude `PreScriptLocation` y `PostScriptlocation` parámetros. Por ejemplo:

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

5. Crear archivos de script anterior a la instantánea y posterior a la instantánea de Hola.

    Este es un ejemplo de scripts anteriores y posteriores a la instantánea para una "copia de seguridad fría" (una copia de seguridad sin conexión, con apagado y reinicio):

    Para /etc/azure/pre_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    Para /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    Este es un ejemplo de scripts anteriores y posteriores a la instantánea para una "copia de seguridad en caliente" (una copia de seguridad con conexión):

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Para /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Para /etc/azure/pre_script.sql, modifique el contenido de Hola de archivo hello según sus requisitos:

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    Para /etc/azure/post_script.sql, modifique el contenido de Hola de archivo hello según sus requisitos:

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. Cambie los permisos de archivo:

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. Probar scripts de Hola.

    secuencias de comandos de tootest hello, en primer lugar, inicie sesión como raíz. Después, asegúrese de que no hay ningún error:

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

Para más información, vea [Copia de seguridad coherente con la aplicación para máquinas virtuales Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a>Paso 5: Usar servicios de recuperación de Azure almacenes de credenciales tooback seguridad Hola VM

1.  En el portal de Azure de Hola, busque **servicios de recuperación de los almacenes de credenciales**.

    ![Página de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_01.png)

2.  En hello **servicios de recuperación de los almacenes de credenciales** hoja, tooadd un nuevo almacén, haga clic en **agregar**.

    ![Página para agregar almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_02.png)

3.  toocontinue, haga clic en **myVault**.

    ![Página de detalles de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_03.png)

4.  En hello **myVault** hoja, haga clic en **copia de seguridad**.

    ![Página de la copia de seguridad de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_04.png)

5.  En hello **objetivo de copia de seguridad** hoja, valores de uso Hola predeterminados de **Azure** y **Máquina Virtual**. Haga clic en **Aceptar**.

    ![Página de detalles de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_05.png)

6.  Para **Directiva de copia de seguridad**, use **DefaultPolicy** (Directiva predeterminada) o haga clic en **Crear nueva directiva**. Haga clic en **Aceptar**.

    ![Página de detalles de la directiva de copia de seguridad de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_06.png)

7.  En hello **seleccionar las máquinas virtuales** hoja, seleccione hello **myVM1** casilla de verificación y, a continuación, haga clic en **Aceptar**. Haga clic en hello **habilitar copia de seguridad** botón.

    ![Página de detalles copia de seguridad de toohello de elementos almacenes de servicios de recuperación](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > Tras hacer clic en **habilitar copia de seguridad**, proceso de copia de seguridad de hello no se inicia hasta que expire hello hora programada. tooset la una copia de seguridad inmediata, completa Hola paso siguiente.

8.  En hello **myVault - elementos de copia de seguridad** hoja, en **recuento de elementos de copia de seguridad**, seleccione el número de elementos de copia de seguridad de Hola.

    ![Página de detalles del almacén myVault de Recovery Services](./media/oracle-backup-recovery/recovery_service_08.png)

9.  En hello **elementos de copia de seguridad (Máquina Virtual de Azure)** hoja, lado derecho de Hola de página de hello, haga clic en puntos suspensivos hello (**...** ) y, a continuación, haga clic en **una copia de seguridad ahora**.

    ![Comando Realizar copia de seguridad ahora de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_09.png)

10. Haga clic en hello **copia de seguridad** botón. Espere a que hello toofinish de proceso de copia de seguridad. A continuación, ir demasiado[paso 6: quitar archivos de base de datos de hello](#step-6-remove-the-database-files).

    Haga clic en estado de hello tooview de trabajo de copia de seguridad de hello, **trabajos**.

    ![Página del trabajo de los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_10.png)

    estado de Hola de trabajo de copia de seguridad de Hola aparece en hello después de la imagen:

    ![Página del trabajo de los almacenes de Recovery Services con el estado](./media/oracle-backup-recovery/recovery_service_11.png)

11. Para una copia de seguridad coherentes con la aplicación, resuelva los errores en el archivo de registro de hello. archivo de registro de Hello se encuentra en /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.

### <a name="step-6-remove-hello-database-files"></a>Paso 6: Quitar archivos de base de datos de Hola 
Más adelante en este artículo, aprenderá cómo tootest Hola proceso de recuperación. Para poder probar el proceso de recuperación de hello, tener archivos de base de datos de tooremove Hola.

1.  Quitar archivos de copia de seguridad y el espacio de tablas de hello:

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  (Opcional) Cierre la instancia de Oracle hello:

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a>Restaure los archivos de hello eliminado de hello que Servicios de recuperación de los almacenes de credenciales
hello toorestore elimina archivos, Hola completa siguiendo los pasos:

1. Hola portal de Azure, busque hello *myVault* elemento de los almacenes de servicios de recuperación de credenciales. En hello **Introducción** hoja, en **elementos de copia de seguridad**, seleccione Hola número de elementos.

    ![Elementos de copia de seguridad del almacén myVault de Recovery Services](./media/oracle-backup-recovery/recovery_service_12.png)

2. En **recuento de elementos de copia de seguridad**, seleccione Hola número de elementos.

    ![Número de elementos de copia de seguridad de máquinas virtuales de Azure en los almacenes de Recovery Services](./media/oracle-backup-recovery/recovery_service_13.png)

3. En hello **myvm1** hoja, haga clic en **recuperación de archivos (vista previa)**.

    ![Captura de pantalla de hello servicios de recuperación de almacenes de credenciales de la página de recuperación de archivos](./media/oracle-backup-recovery/recovery_service_14.png)

4. En hello **recuperación de archivos (vista previa)** panel, haga clic en **descargar Script**. A continuación, guarde el archivo tooa carpeta de descarga (.sh) de hello en el equipo cliente de Hola.

    ![Operaciones de guardado del archivo de script descargado](./media/oracle-backup-recovery/recovery_service_15.png)

5. Copie hello .sh archivo toohello máquina virtual.

    Hola de ejemplo siguiente muestra cómo toouse una toomove de comando de copia de seguridad (scp) Hola archivo toohello máquina virtual. También puede copiar el Portapapeles de hello contenido toohello y, a continuación, pegar Hola contenido en un nuevo archivo que se ha configurado en hello máquina virtual.

    > [!IMPORTANT]
    > En el siguiente ejemplo de Hola, asegúrese de que se actualizan los valores de dirección y la carpeta de la IP de Hola. valores de Hello deben asignar la carpeta toohello donde se guarda el archivo hello.

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. Cambie el archivo de hello, por lo que es propiedad de raíz de Hola.

    En el siguiente ejemplo de Hola, cambiar archivo hello por lo que es propiedad de raíz de Hola. Después, cambie los permisos.

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    Hello en el ejemplo siguiente se muestra lo que verá después de ejecutar Hola anterior secuencia de comandos. Cuando se le pide toocontinue, escriba **Y**.

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

7. Acceso toohello montar volúmenes se ha confirmado.

    tooexit, escriba **preguntas**y, a continuación, busque Hola montada volúmenes. toocreate una lista de hello agrega volúmenes, en un símbolo del sistema, escriba **df -k**.

    ![comando de Hello df -k](./media/oracle-backup-recovery/recovery_service_16.png)

8. Hola de uso después de que falta un script toocopy Hola archivos toohello atrás carpetas:

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
9. En la siguiente secuencia de comandos de hello, usar base de datos RMAN toorecover hello:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. Desmonte el disco de Hola.

    En el portal de Azure, en Hola Hola **recuperación de archivos (vista previa)** hoja, haga clic en **desmontar discos**.

    ![Comando Unmount Disks (Desmontar discos)](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a>Restaurar Hola toda máquina virtual

En lugar de restaurar los archivos eliminado de Hola de almacenes de servicios de recuperación de hello, puede restaurar Hola toda máquina virtual.

### <a name="step-1-delete-myvm"></a>Paso 1: Eliminar myVM

*   Hola portal de Azure, vaya toohello **myVM1** del almacén y, a continuación, seleccione **eliminar**.

    ![Comando Eliminar almacén](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a>Paso 2: Recuperar Hola VM

1.  Vaya demasiado**servicios de recuperación de los almacenes de credenciales**y, a continuación, seleccione **myVault**.

    ![Entrada de myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  En hello **Introducción** hoja, en **elementos de copia de seguridad**, seleccione Hola número de elementos.

    ![Elementos de copias de seguridad de myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  En hello **elementos de copia de seguridad (Máquina Virtual de Azure)** hoja, seleccione **myvm1**.

    ![Página de la máquina virtual de recuperación](./media/oracle-backup-recovery/recover_vm_04.png)

4.  En hello **myvm1** hoja, haga clic en el botón de puntos suspensivos hello (**...** ) y, a continuación, haga clic en **VM restaurar**.

    ![Comando Restaurar máquina virtual](./media/oracle-backup-recovery/recover_vm_05.png)

5.  En hello **Seleccionar punto de restauración** hoja, elemento de select Hola que desee toorestore y, a continuación, haga clic en **Aceptar**.

    ![Punto de restauración de hello SELECT](./media/oracle-backup-recovery/recover_vm_06.png)

    Si ha habilitado la copia de seguridad coherente con la aplicación, aparece una barra vertical de color azul.

6.  En hello **restaurar la configuración** hoja, nombre de la máquina virtual seleccione hello, seleccione el grupo de recursos de hello y, a continuación, haga clic en **Aceptar**.

    ![Valores de configuración de la restauración](./media/oracle-backup-recovery/recover_vm_07.png)

7.  Hola toorestore máquina virtual, haga clic en hello **restaurar** botón.

8.  Haga clic en estado de hello tooview del proceso de restauración de hello, **trabajos**y, a continuación, haga clic en **trabajos de copia de seguridad**.

    ![Comando de estado de los trabajos de copia de seguridad](./media/oracle-backup-recovery/recover_vm_08.png)

    Hello en la ilustración siguiente se muestra hello estado del proceso de restauración de hello:

    ![Estado del proceso de restauración de Hola](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a>Paso 3: Establecer la dirección IP pública Hola
Hola que se restaura la máquina virtual después de haber configurado la dirección IP pública Hola.

1.  En el cuadro de búsqueda de hello, escriba **dirección IP pública**.

    ![Lista de direcciones IP públicas](./media/oracle-backup-recovery/create_ip_00.png)

2.  En hello **direcciones IP públicas** hoja, haga clic en **agregar**. En hello **Crear dirección IP pública** hoja, para **nombre**, seleccione el nombre de IP pública de Hola. En **Grupo de recursos**, seleccione **Usar existente**. A continuación, haga clic en **Crear**.

    ![Creación de la dirección IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  tooassociate Hola la dirección IP pública con interfaz de red de Hola para hello VM, busque y seleccione **myVMip**. Después, haga clic en **Asociar**.

    ![Asociación de la dirección IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  Para **Tipo de recurso**, seleccione **Interfaz de red**. Seleccione Hola interfaz de red utilizado por la instancia de hello myVM y, a continuación, haga clic en **Aceptar**.

    ![Selección del tipo de recurso y los valores de NIC](./media/oracle-backup-recovery/create_ip_03.png)

5.  Busque y abra la instancia de Hola de myVM que se transfieren desde el portal de Hola. Hello dirección IP que está asociado con hello VM aparece en hello myVM **Introducción** hoja.

    ![Valor de la dirección IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a>Paso 4: Conectar toohello VM

*   tooconnect toohello de máquina virtual, use Hola siguiente secuencia de comandos:

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a>Paso 5: Comprobar si la base de datos de hello es accesible
*   tootest accesibilidad, Hola de uso siguiente secuencia de comandos:

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > La base de datos si hello **inicio** comando genera un error, la base de datos de toorecover hello, consulte [paso 6: base de datos de uso RMAN toorecover hello](#step-6-optional-use-rman-to-recover-the-database).

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a>Paso 6: Base de datos (opcional) utilice RMAN toorecover Hola
*   toorecover Hola base de datos, Hola de uso siguiente secuencia de comandos:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

copia de seguridad de Hola y de recuperación de base de datos de hello Oracle Database 12C en una máquina virtual Linux de Azure ya está completado.

## <a name="delete-hello-vm"></a>Eliminar Hola VM

Cuando ya no necesita hello VM, puede usar Hola después el grupo de recursos de comando tooremove hello, Hola VM y todos ellos relacionados con recursos:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

[Tutorial: Creación de máquinas virtuales de alta disponibilidad](../../linux/create-cli-complete.md)

[Ejemplos de la CLI de Azure para implementación de máquinas virtuales](../../linux/cli-samples.md)



