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
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a>Implementación de Oracle Data Guard en una máquina virtual Linux en Azure 

CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts. Este artículo describe cómo toouse CLI de Azure toodeploy una base de datos de Oracle 12C base de datos de imagen de hello Azure Marketplace. Este artículo, a continuación, muestra, paso a paso, cómo tooinstall y configurar Data Guard en una máquina virtual (VM) de Azure.

Antes de comenzar, asegúrese de que esté instalada la CLI de Azure. Para obtener más información, vea hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Preparar el entorno de Hola
### <a name="assumptions"></a>Supuestos

tooinstall Oracle Data Guard, deberá toocreate dos máquinas virtuales de Azure en hello mismo conjunto de disponibilidad:

- Hello VM principal (myVM1) tiene una instancia de Oracle en ejecución.
- Hola que máquina virtual en espera (myVM2) tiene instalado sólo el software de Oracle de Hola.

imagen de Marketplace que usar toocreate Hola máquinas virtuales Hello es Oracle: Oracle-base de datos-Ee:12.1.0.2:latest.

### <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure 

Inicie sesión en tooyour suscripción de Azure mediante hello [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos mediante el uso de hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westus` ubicación:

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Crear un conjunto de disponibilidad

La creación de un conjunto de disponibilidad es opcional, pero es recomendable. Para más información, consulte las [directrices de conjuntos de disponibilidad de Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>de una máquina virtual

Crear una máquina virtual mediante hello [crear vm az](/cli/azure/vm#create) comando. 

Hello en el ejemplo siguiente se crea dos máquinas virtuales con el nombre `myVM1` y `myVM2`. También se crean claves SSH si aún no existen en una ubicación de claves predeterminada. toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.

Cree myVM1 (principal):
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

Después de crear Hola VM, CLI de Azure muestra información toohello similar siguiente ejemplo. Tenga en cuenta el valor de Hola de `publicIpAddress`. Utilice este hello tooaccess de dirección virtual.

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

Cree myVM2 (en espera):
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

Tenga en cuenta el valor de Hola de `publicIpAddress` después de crear myVM2.

### <a name="open-hello-tcp-port-for-connectivity"></a>Hola abierto el puerto TCP para la conectividad

Este paso configura extremos externos, lo que permite la base de datos de Oracle de toohello de acceso remoto.

Abrir el puerto de Hola para myVM1:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

resultado de Hello debería ser similar toohello después de respuesta:

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

Abrir el puerto de Hola para myVM2:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Conectar máquina virtual de toohello

Siguiente Hola de uso del comando toocreate una sesión SSH con la máquina virtual de Hola. Reemplace la dirección IP de hello con hello `publicIpAddress` valor para la máquina virtual.

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Crear base de datos de hello en myVM1 (principal)

Hola software de Oracle ya está instalado en una imagen de Marketplace hello, para que hello siguiente paso es base de datos de tooinstall Hola. 

Cambiar toohello superusuario de Oracle:

```bash
$ sudo su - oracle
```

Crear base de datos de hello:

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
Salidas deben tener un aspecto similar toohello después de respuesta:

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

Establecer variables de hello ORACLE_SID y ORACLE_HOME:

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

Si lo desea, puede agregar archivos de /home/oracle/.bashrc toohello ORACLE_HOME y ORACLE_SID, para que esta configuración se guarda para futuras inicios de sesión:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a>Configuración de Data Guard

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>Habilitar el modo de archivar registro en myVM1 (principal)

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
Habilite el registro forzado y asegúrese de que, al menos, haya un archivo de registro está presente:

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

Cree registros de rehacer en espera:

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

Activar retrospectiva (lo que facilita la recuperación mucho) y establezca el modo de espera\_archivo\_tooauto de administración. Salga de SQL * Plus a continuación.

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a>Configuración del servicio en myVM1 (principal)

Editar o crear el archivo tnsnames.ora de hello, que se encuentra en la carpeta de hello $ORACLE_HOME\network\admin.

Agregue Hola siguientes entradas:

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

Editar o crear el archivo listener.ora de hello, que se encuentra en la carpeta de hello $ORACLE_HOME\network\admin.

Agregue Hola siguientes entradas:

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

Habilite el agente de Data Guard:
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
Inicie el agente de escucha de hello:

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a>Configuración del servicio en myVM2 (en espera)

ToomyVM2 SSH:

```bash 
$ ssh azureuser@<publicIpAddress>
```

Inicie sesión como Oracle:

```bash
$ sudo su - oracle
```

Editar o crear el archivo tnsnames.ora de hello, que se encuentra en la carpeta de hello $ORACLE_HOME\network\admin.

Agregue Hola siguientes entradas:

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

Editar o crear el archivo listener.ora de hello, que se encuentra en la carpeta de hello $ORACLE_HOME\network\admin.

Agregue Hola siguientes entradas:

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

Inicie el agente de escucha de hello:

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a>Restaurar hello toomyVM2 de base de datos (en espera)

Crear Hola parámetro archivo /tmp/initcdb1_stby.ora con hello siguiente contenido:
```bash
*.db_name='cdb1'
```

Cree carpetas:

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

Cree un archivo de contraseña:

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
Iniciar la base de datos de hello en myVM2:

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

Restaurar base de datos de hello mediante Hola RMAN herramienta:

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

Ejecute hello siga los comandos en RMAN:
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

Debería aparecer mensajes similares toohello siguiente cuando se completa el comando de Hola. Salga de RMAN.
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

Si lo desea, puede agregar archivos de /home/oracle/.bashrc toohello ORACLE_HOME y ORACLE_SID, para que esta configuración se guarda para futuras inicios de sesión:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

Habilite el agente de Data Guard:
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a>Configuración del agente de Data Guard en myVM1 (principal)

Inicie el administrador de Data Guard e inicie sesión mediante SYS y una contraseña. (No utilice la autenticación de sistema operativo). Realice Hola siguiente:

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

Revisar la configuración de hello:
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

Ha completado el programa de instalación de Oracle Data Guard de Hola. sección de Hello siguiente muestra cómo tootest Hola conectividad y cambiar.

### <a name="connect-hello-database-from-hello-client-machine"></a>Conectar la base de datos de Hola desde el equipo de cliente hello

Actualizar o crear el archivo tnsnames.ora de hello en el equipo cliente. Este archivo suele encontrarse en $ORACLE_HOME\network\admin.

Reemplazar las direcciones IP de hello con su `publicIpAddress` valores para myVM1 y por myVM2:

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

Inicie SQL *Plus:

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a>Configuración de protección de datos de prueba Hola

### <a name="switch-over-hello-database-on-myvm1-primary"></a>Cambiar base de datos de hello en myVM1 (principal)

tooswitch de toostandby principal (cdb1 toocdb1_stby):

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

Ahora puede conectarse toohello base de datos en espera.

Inicie SQL *Plus:

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a>Cambiar base de datos de hello en myVM2 (en espera)

tooswitch sobre, ejecute siguiente de hello en myVM2:
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

Una vez más, ahora debe ser la base de datos principal puede tooconnect toohello.

Inicie SQL *Plus:

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

Ha terminado de hello instalación y configuración de protección de datos en Oracle Linux.


## <a name="delete-hello-virtual-machine"></a>Eliminar la máquina virtual de Hola

Cuando ya no necesita hello VM, puede usar Hola después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

[Tutorial de creación de máquinas virtuales de alta disponibilidad](../../linux/create-cli-complete.md)

[Ejemplos de la CLI de Azure para implementación de máquinas virtuales](../../linux/cli-samples.md)
