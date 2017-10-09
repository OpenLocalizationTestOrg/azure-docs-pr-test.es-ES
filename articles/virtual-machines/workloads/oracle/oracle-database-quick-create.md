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
# <a name="create-an-oracle-database-in-an-azure-vm"></a>Creación de una base de datos Oracle en una VM de Azure

Esta guía se detalla con hello Azure CLI toodeploy una máquina virtual de Azure de hello [imagen de la Galería de Oracle marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) en orden toocreate una base de datos de Oracle 12C. Una vez implementado el servidor de hello, se conectará a través de SSH en la base de datos de Oracle de orden tooconfigure Hola. 

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a>Create virtual machine

toocreate una máquina virtual (VM), usar hello [crear vm az](/cli/azure/vm#create) comando. 

Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM`. También se crean claves SSH si aún no existen en una ubicación de claves predeterminada. toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

Después de crear Hola VM, CLI de Azure muestra información toohello similar siguiente ejemplo. Tenga en cuenta el valor de Hola para `publicIpAddress`. Utilice este hello tooaccess de dirección virtual.

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

## <a name="connect-toohello-vm"></a>Conectar toohello VM

toocreate una sesión SSH con hello de máquina virtual, use Hola siguiente comando. Reemplace la dirección IP de hello con hello `publicIpAddress` valor para la máquina virtual.

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a>Crear base de datos de Hola

Hola software de Oracle ya está instalado en una imagen de Marketplace Hola. Cree una base de datos de ejemplo de la manera siguiente: 

1.  Cambiar toohello *oracle* superusuario y, a continuación, agente de escucha de inicializar hello para el registro:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    salida de Hello es siguiente de toohello similar:

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

2.  Crear base de datos de hello:

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

    Toma el base de datos unos minutos toocreate Hola.

3. Establecimiento de las variables de Oracle

Antes de conectar, necesita tooset dos variables de entorno: *ORACLE_HOME* y *ORACLE_SID*.

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
También puede agregar ORACLE_HOME y ORACLE_SID toohello .bashrc archivo de variables de. Esto ahorraría variables de entorno de Hola para futuros inicios de sesión. Confirme Hola siguiente instrucciones se han agregado toohello `~/.bashrc` archivo mediante el editor de su elección.

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a>Conectividad con Oracle EM Express

Para una herramienta de administración de GUI que puede usar la base de datos de tooexplore hello, configure Oracle EM Express. tooconnect tooOracle EM Express, primero debe establecer el puerto de hello en Oracle. 

1. Conectar la base de datos de tooyour mediante sqlplus:

    ```bash
    sqlplus / as sysdba
    ```

2. Una vez conectado, establezca el puerto de hello 5502 para EM Express

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. Contenedor de hello abierto PDB1 si no ya está abierto, pero primero comprobar el estado de hello:

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    salida de Hello es siguiente de toohello similar:

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. Si Hola OPEN_MODE para `PDB1` no es leer escribir, a continuación, ejecute comandos tooopen PDB1 de hello siguiente:

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

Necesita tootype `quit` tooend Hola sqlplus sesión y el tipo `exit` toologout de usuario de oracle Hola.

## <a name="automate-database-startup-and-shutdown"></a>Automatizar el arranque y el apagado de la base de datos

base de datos de Oracle de Hola de forma predeterminada no se inicia automáticamente cuando se reinicia Hola máquina virtual. tooset una toostart de base de datos de Oracle Hola automáticamente, primero inicie sesión como raíz. Después, cree y actualice algunos archivos del sistema.

1. Inicio de sesión como raíz
    ```bash
    sudo su -
    ```

2.  Con su editor favorito, edite el archivo hello `/etc/oratab` y cambie el valor predeterminado de hello `N` demasiado`Y`:

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  Cree un archivo denominado `/etc/init.d/dbora` y pegar Hola siguiente contenido:

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

4.  Cambie los permisos de los archivos con *chmod* como se indica a continuación:

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  Cree vínculos simbólicos para el inicio y el apagado de la manera siguiente:

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  tootest los cambios, reinicie Hola VM:

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a>Abrir puertos para la conectividad

tarea final de Hello es tooconfigure algunos extremos externos. tooset seguridad Hola grupo de seguridad de red de Azure que protege Hola VM, salir de la sesión de SSH en hello VM (debe haber sido expulsado SSH al reiniciar el sistema en el paso anterior). 

1.  extremo de hello tooopen usar base de datos de Oracle tooaccess Hola de forma remota, cree una regla de grupo de seguridad de red con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) como se indica a continuación: 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  extremo de Hola de tooopen que usar tooaccess Oracle EM Express de forma remota, cree una regla de grupo de seguridad de red con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) como se indica a continuación:

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. Si es necesario, obtenga la dirección IP pública de saludo de la máquina virtual nuevo con [show de public-ip de red az](/cli/azure/network/public-ip#show) como se indica a continuación:

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  Conecte EM Express desde el explorador. Asegúrese de que el explorador sea compatible con Express EM (es necesario que Flash esté instalado): 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

Puede iniciar sesión mediante el uso de hello **SYS** cuenta y comprobar hello **como sysdba** casilla de verificación. Usar la contraseña de hello **OraPasswd1** que establecen durante la instalación. 

![Captura de pantalla de la página de inicio de sesión de Oracle OEM Express Hola](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a>Limpieza de recursos

Una vez que haya terminado de explorar la primera base de datos de Oracle en Azure y hello VM ya no es necesario, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, VM y todos ellos relacionados con recursos.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

Conozca otras [soluciones de Oracle en Azure](oracle-considerations.md). 

Intente hello [instalar y configurar Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.
