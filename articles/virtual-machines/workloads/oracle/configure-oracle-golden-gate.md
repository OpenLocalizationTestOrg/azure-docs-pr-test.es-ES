---
title: "aaaImplement Oracle Golden puerta en una máquina virtual Linux de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a>Implementación de Oracle Golden Gate en máquinas virtuales Linux de Azure 

Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts. Esta guía se detalla cómo toouse hello Azure CLI toodeploy Oracle 12C base de datos de imagen de la Galería de hello Azure Marketplace. 

Este documento explican los pasos cómo toocreate, instalar y configurar la puerta de Golden de Oracle en una máquina virtual de Azure.

Antes de empezar, asegúrese de que ese Hola que CLI de Azure se ha instalado. Para obtener más información, consulte la [guía de instalación de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Preparar el entorno de Hola

instalación de Oracle Golden puerta de tooperform hello, necesita toocreate dos máquinas virtuales de Azure en hello mismo conjunto de disponibilidad. imagen de Marketplace de Hello usar toocreate hello las máquinas virtuales es **Oracle: Oracle-base de datos-Ee:12.1.0.2:latest**.

También necesita toobe familiarizado con Unix editor vi y tener un conocimiento básico de x11 (Windows X).

Hola te mostramos un resumen de configuración del entorno de hello:
> 
> |  | **Sitio principal** | **Sitio de réplica** |
> | --- | --- | --- |
> | **Versión de Oracle** |Oracle 12c Release 2 – (12.1.0.2) |Oracle 12c Release 2 – (12.1.0.2)|
> | **Nombre de la máquina** |myVM1 |myVM2 |
> | **Sistema operativos** |Oracle Linux 6.x |Oracle Linux 6.x |
> | **SID de Oracle** |CDB1 |CDB1 |
> | **Esquema de replicación** |PRUEBA|PRUEBA |
> | **Propietario/réplica de Golden Gate** |C##GGADMIN |REPUSER |
> | **Proceso de Golden Gate** |EXTORA |REPORA|


### <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure 

Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando. A continuación, siga hello en pantalla direcciones.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y desde el que se pueden administrar los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westus` ubicación.

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Crear un conjunto de disponibilidad

Hola siguiendo el paso es opcional pero recomendado. Para más información, consulte la [guía de conjuntos de disponibilidad de Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>de una máquina virtual

Crear una máquina virtual con hello [crear vm az](/cli/azure/vm#create) comando. 

Hello en el ejemplo siguiente se crea dos máquinas virtuales con el nombre `myVM1` y `myVM2`. También se crean claves SSH, si aún no existen en una ubicación de claves predeterminada. toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.

#### <a name="create-myvm1-primary"></a>Cree myVM1 (principal):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Después de Hola que se ha creado la máquina virtual, Hola CLI de Azure muestra información toohello similar siguiente ejemplo. (Tenga en cuenta de hello `publicIpAddress`. Esta dirección es tooaccess usado Hola VM).

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

#### <a name="create-myvm2-replicate"></a>Cree myVM2 (réplica):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Tome nota de hello `publicIpAddress` también después de que se ha creado.

### <a name="open-hello-tcp-port-for-connectivity"></a>Hola abierto el puerto TCP para la conectividad

Hola siguiente paso es tooconfigure extremos externos, lo que permitirá base de datos de Oracle tooaccess Hola remotamente. tooconfigure Hola extremos externos, ejecute hello siga los comandos.

#### <a name="open-hello-port-for-myvm1"></a>Abrir el puerto de Hola para myVM1:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

resultados de Hello deberían ser similar toohello después de respuesta:

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

#### <a name="open-hello-port-for-myvm2"></a>Abrir el puerto de Hola para myVM2:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Conectar máquina virtual de toohello

Siguiente Hola de uso del comando toocreate una sesión SSH con la máquina virtual de Hola. Reemplace la dirección IP de hello con hello `publicIpAddress` de la máquina virtual.

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Crear base de datos de hello en myVM1 (principal)

Hola software de Oracle ya está instalado en una imagen de Marketplace hello, para que hello siguiente paso es base de datos de tooinstall Hola. 

Ejecute software de hello como superusuario de hello 'oracle':

```bash
sudo su - oracle
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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

Establecer variables ORACLE_SID y ORACLE_HOME Hola.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Si lo desea, puede agregar archivos de .bashrc toohello ORACLE_HOME y ORACLE_SID, para que esta configuración se guarda para futuras inicios de sesión:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Inicio del agente de escucha de Oracle
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a>Crear base de datos de hello en myVM2 (replicar)

```bash
sudo su - oracle
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
Establecer variables ORACLE_SID y ORACLE_HOME Hola.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Si lo desea, puede ORACLE_HOME y ORACLE_SID toohello .bashrc archivo agregado, por lo que esta configuración se guarda para futuras inicios de sesión.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Inicio del agente de escucha de Oracle
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a>Configuración de Golden Gate 
tooconfigure Golden puerta, siga los pasos de hello en esta sección.

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
Habilite el registro forzado y asegúrese de que, al menos, haya un archivo de registro está presente.

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a>Descargar el software de Golden Gate
toodownload y preparar el software de Oracle Golden puerta hello, Hola completa pasos:

1. Descargar hello **fbo_ggs_Linux_x64_shiphome.zip** archivo de hello [página de descarga de Oracle Golden puerta](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html). En hello descargar título **12.x.x.x de Oracle GoldenGate para Oracle Linux x86-64**, debe haber un conjunto de toodownload de archivos zip.

2. Después de descargar el equipo cliente tooyour de hello .zip archivos, utilizar protocolo de copia seguro (SCP) toocopy Hola archivos tooyour VM:

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. Mover Hola .zip archivos toohello **/ opt** carpeta. A continuación, cambiar el propietario de Hola de archivos de Hola de como se indica a continuación:

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. Descomprimir archivos de hello (instalación Hola Linux descomprima utilidad si aún no está instalado):

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. Cambie el permiso:

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a>Preparar cliente de Hola y VM toorun x11 (para clientes de Windows)
Se trata de un paso opcional. Puede omitir este paso si está utilizando un cliente Linux o ya ha configurado x11.

1. Descargar PuTTY y Xming tooyour equipo con Windows:

  * [Descargar PuTTY](http://www.putty.org/)
  * [Descargar Xming](https://xming.en.softonic.com/)

2.  Después de instalar PuTTY, en Hola PuTTY carpeta (por ejemplo, C:\Program Files\PuTTY), ejecute puttygen.exe (generador de claves de PuTTY).

3.  En PuTTY Key Generator:

  - una clave, seleccione hello toogenerate **generar** botón.
  - Copie el contenido de Hola de clave de hello (**Ctrl + C**).
  - Seleccione hello **clave privada de guardar** botón.
  - Omitir la advertencia Hola que aparece y, a continuación, seleccione **Aceptar**.

    ![Captura de pantalla de hello PuTTY clave generador (página)](./media/oracle-golden-gate/puttykeygen.png)

4.  En la máquina virtual, ejecute estos comandos:

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. Cree un archivo denominado **authorized_keys**. Pegar contenido de Hola de clave de hello en este archivo y, a continuación, guarde el archivo hello.

  > [!NOTE]
  > clave de Hello debe contener la cadena de hello `ssh-rsa`. Además, el contenido de Hola de clave de hello debe ser una sola línea de texto.
  >  

6. Inicie PuTTY. Hola **categoría** panel, seleccione **conexión** > **SSH** > **Auth**. Hola **archivo de clave privada para la autenticación** cuadro, busque la clave de toohello que ha generado anteriormente.

  ![Captura de pantalla de página de establecer la clave privada de Hola](./media/oracle-golden-gate/setprivatekey.png)

7. Hola **categoría** panel, seleccione **conexión** > **SSH** > **X11**. A continuación, seleccione hello **X11 de habilitar el reenvío** cuadro.

  ![Captura de pantalla de página de habilitar X11 Hola](./media/oracle-golden-gate/enablex11.png)

8. Hola **categoría** panel, vaya demasiado**sesión**. Escriba información de host de hello y, a continuación, seleccione **abiertos**.

  ![Captura de pantalla de página de la sesión de Hola](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a>Instalar el software de Golden Gate

tooinstall Oracle Golden puerta, Hola completa pasos:

1. Inicie sesión como oracle. (Debe ser capaz de toosign en sin que se solicite una contraseña). Asegúrese de que se está ejecutando Xming antes de comenzar la instalación de Hola.
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. Seleccione 'Oracle GoldenGate para Oracle Database 12c'. A continuación, seleccione **siguiente** toocontinue.

  ![Captura de pantalla de la página de instalación seleccione Instalador Hola](./media/oracle-golden-gate/golden_gate_install_01.png)

3. Cambiar la ubicación del software de Hola. A continuación, seleccione hello **iniciar el Administrador de** casilla y especifique la ubicación de la base de datos de Hola. Seleccione **siguiente** toocontinue.

  ![Captura de pantalla de la página de instalación seleccione Hola](./media/oracle-golden-gate/golden_gate_install_02.png)

4. Cambie el directorio de inventario de hello y, a continuación, seleccione **siguiente** toocontinue.

  ![Captura de pantalla de la página de instalación seleccione Hola](./media/oracle-golden-gate/golden_gate_install_03.png)

5. En hello **resumen** pantalla, seleccione **instalar** toocontinue.

  ![Captura de pantalla de la página de instalación seleccione Instalador Hola](./media/oracle-golden-gate/golden_gate_install_04.png)

6. Es posible que una secuencia de comandos de toorun solicitada como 'root'. Si es así, abra una sesión independiente, ssh toohello VM, tooroot sudo y, a continuación, ejecute el script de Hola. Seleccione **Aceptar** para continuar.

  ![Captura de pantalla de la página de instalación seleccione Hola](./media/oracle-golden-gate/golden_gate_install_05.png)

7. Cuando haya finalizado la instalación de hello, seleccione **cerrar** toocomplete proceso de Hola.

  ![Captura de pantalla de la página de instalación seleccione Hola](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a>Configuración del servicio en myVM1 (principal)

1. Crear o actualizar el archivo tnsnames.ora de hello:

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

2. Crear cuentas de usuario y de propietario de Golden puerta de Hola.

  > [!NOTE]
  > cuenta de propietario de Hello debe tener el prefijo C ##.
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. Crear cuenta de usuario de prueba de hello Golden puerta:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. Configurar el archivo de parámetros de extracción de Hola.

 Iniciar la interfaz de línea de comandos Hola puerta dorada (ggsci):

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
5. Agregar Hola siguiendo el archivo de parámetros de extracción toohello (mediante comandos de vi). Presione la tecla Esc, ':wq!' archivo toosave. 

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
6. Register extract - extracción integrada:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. Configure los puntos de control de extracción e inicie la extracción en tiempo real:

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
En este paso, encontrar Hola a partir de SCN, que se usará más adelante, en otra sección:

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

### <a name="set-up-service-on-myvm2-replicate"></a>Configuración del servicio en myVM2 (réplica)


1. Crear o actualizar el archivo tnsnames.ora de hello:

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

2. Cree una cuenta de replicación:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. Cree una cuenta de usuario de prueba de Golden Gate:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. REPLICAT parámetro archivo tooreplicate cambios: 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  Contenido del archivo de parámetros REPORA:

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

5. Configure un punto de control de replicat:

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

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a>Configurar la replicación de hello (myVM1 y myVM2)

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a>1. Configurar la replicación de hello en myVM2 (replicar)

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
Actualizar archivo hello con siguiente hello:

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
A continuación, reinicie el servicio de administrador de hello:

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a>2. Configurar la replicación de hello en myVM1 (principal)

Iniciar la carga inicial de Hola y compruebe si hay errores:

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a>3. Configurar la replicación de hello en myVM2 (replicar)

Cambiar Hola número SCN con hello obtenido antes:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
ha empezado la replicación de Hola y puede probarlo mediante la inserción de nuevas tablas de tooTEST de registros.


### <a name="view-job-status-and-troubleshooting"></a>Visualización del estado del trabajo y solución de problemas

#### <a name="view-reports"></a>Ver informes
tooview informa sobre myVM1, ejecute hello siguientes comandos:

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
tooview informa sobre myVM2, ejecute hello siguientes comandos:

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a>Visualización del estado e historial
estado de tooview y el historial en myVM1, ejecute hello siguientes comandos:

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

estado de tooview y el historial en myVM2, ejecute hello siguientes comandos:

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
Con esto finaliza la instalación de Hola y la configuración de puerta de Golden en Oracle linux.


## <a name="delete-hello-virtual-machine"></a>Eliminar la máquina virtual de Hola

Cuando ya no es necesario, puede ser Hola siguiente comando grupo de recursos de hello tooremove usado, la VM y todos ellos relacionados con recursos.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

[Tutorial de creación de máquinas virtuales de alta disponibilidad](../../linux/create-cli-complete.md)

[Ejemplos de la CLI de implementación de máquinas virtuales](../../linux/cli-samples.md)
