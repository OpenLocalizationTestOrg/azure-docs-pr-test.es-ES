---
title: "aaaSet de ASM de Oracle en una máquina virtual de Linux de Azure | Documentos de Microsoft"
description: "Ponga en funcionamiento rápidamente ASM de Oracle en el entorno de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a>Configuración de ASM de Oracle en una máquina virtual Linux en Azure  

Las máquinas virtuales de Azure proporcionan un entorno informático completamente configurable y flexible. Este tutorial trata la implementación de máquina virtual de Azure básico combinada con la instalación de Hola y configuración de Oracle Automated Storage Management (ASM).  Aprenderá a:

> [!div class="checklist"]
> * Crear y conectar tooan VM de base de datos de Oracle
> * Instalar y configurar Automated Storage Management de Oracle
> * Instalar y configurar la infraestructura Grid de Oracle
> * Inicializar una instalación de ASM de Oracle
> * Crear una base de datos de Oracle administrada por ASM


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-hello-environment"></a>Preparar el entorno de Hola

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

toocreate un grupo de recursos, utilice hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. En este ejemplo, un grupo de recursos denominado *myResourceGroup* en hello *eastus* región.

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a>Creación de una VM

toocreate una máquina virtual basada en imagen de la base de datos de Oracle de Hola y configurar toouse Oracle ASM, usar hello [crear vm az](/cli/azure/vm#create) comando. 

Hello en el ejemplo siguiente se crea una máquina virtual denominada myVM que tiene un tamaño de Standard_DS2_v2 con cuatro discos de datos adjuntos de 50 GB. Si no existe ya en la ubicación de la clave predeterminada Hola, también crea claves SSH.  toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

Después de crear Hola VM, CLI de Azure muestra información toohello similar siguiente ejemplo. Tenga en cuenta el valor de Hola para `publicIpAddress`. Utilice este hello tooaccess de dirección virtual.

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a>Conectar toohello VM

toocreate una sesión SSH con Hola VM y configurar opciones adicionales, use Hola siguiente comando. Reemplace la dirección IP de hello con hello `publicIpAddress` valor para la máquina virtual.

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a>Instalación de ASM de Oracle

tooinstall Oracle ASM, Hola completa pasos. 

Para más información sobre cómo instalar ASM de Oracle, consulte [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html) (Descargas de Oracle ASMLib para Oracle Linux 6).  

1. Necesita toologin como raíz en orden toocontinue con la instalación de ASM:

   ```bash
   sudo su -
   ```
   
2. Ejecute estos comandos adicionales tooinstall componentes de ASM de Oracle:

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. Compruebe que ASM de Oracle esté instalado:

   ```bash
   rpm -qa |grep oracleasm
   ```

    salida de Hello de este comando debería incluir Hola de los componentes siguientes:

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. ASM requiere determinados usuarios y roles en orden toofunction correctamente. Hola, siga los comandos crea grupos y cuentas de usuario son un requisito previo de hello: 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. Compruebe que los usuarios y grupos se han creado correctamente:

   ```bash
   id grid
   ```

    Hello salida de este comando debería incluir siguiente Hola usuarios y grupos:

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. Cree una carpeta para el usuario *cuadrícula* y cambiar el propietario de hello:

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a>Configuración de ASM de Oracle

Para este tutorial, es el usuario predeterminado de hello *cuadrícula* y el grupo predeterminado de hello es *asmadmin*. Asegúrese de que hello *oracle* usuario forma parte del grupo de asmadmin Hola. tooset en la instalación de Oracle ASM completa Hola pasos:

1. Configuración de controlador de biblioteca de Oracle ASM Hola implica definir usuario predeterminado de hello (cuadrícula) y el grupo predeterminado (asmadmin), así como configurar hello toostart de unidad de arranque (elegir y) y tooscan para los discos de arranque (elegir y). Necesita tooanswer Hola mensajes de Hola siguiente comando:

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   salida de Hello de este comando debe ser similar toohello siguiendo, detener con toobe preguntas respondida.

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. Configuración de disco de Hola de vista:
   ```bash
   cat /proc/partitions
   ```

   salida de Hello de este comando debe tener un aspecto similar toohello después de la lista de discos disponibles

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. Dar formato al disco */dev/sdc* ejecutando Hola siguiente comando y responder a Hola mensajes con:
   - *n* para la nueva partición
   - *p* para la partición principal
   - *1* primera partición de tooselect Hola
   - Presione `enter` para el primer cilindro de saludo predeterminado
   - Presione `enter` para último cilindro de saludo predeterminado
   - Presione *w* tabla de particiones de toowrite Hola cambios toohello  

   ```bash
   fdisk /dev/sdc
   ```
   
   Con las respuestas de hello proporcionadas anteriormente, salida de hello para el comando de fdisk Hola debería ser similar Hola siguiente:

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. Hola repetición anterior comando fdisk para `/dev/sdd`, `/dev/sde`, y `/dev/sdf`.

5. Compruebe la configuración de disco de hello:

   ```bash
   cat /proc/partitions
   ```

   salida de Hello de comando hello debería ser similar Hola siguiente:

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. Comprobar estado del servicio de Oracle ASM Hola e iniciar servicio de Oracle ASM de hello:

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   salida de Hello de comando hello debería ser similar Hola siguiente:
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. Cree discos de ASM de Oracle:

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   salida de Hello de comando hello debería ser similar Hola siguiente:

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. Enumere discos de ASM de Oracle:

   ```bash
   service oracleasm listdisks
   ```   

   salida de Hello de comando hello debería incluir desactivar Hola siguientes discos ASM de Oracle:

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. Cambiar las contraseñas de Hola para los usuarios de raíz, oracle y cuadrícula de Hola. **Tome nota de estas nuevas contraseñas** que se utilizan más adelante durante la instalación de Hola.

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. Cambiar los permisos de carpeta de hello:

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a>Descarga y preparación de Oracle Grid Infrastructure

toodownload y preparar el software de infraestructura de red de Oracle hello, Hola completa pasos:

1. Descargar la infraestructura de red de Oracle de hello [página de descarga de Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html). 

   En descargar Hola titulada **Oracle Database 12C Release 1 cuadrícula infraestructura (12.1.0.2.0) para Linux x86-64**, descargue los archivos .zip Hola dos.

2. Después de descargar el equipo cliente tooyour de hello .zip archivos, puede usar el protocolo de copia seguro (SCP) toocopy Hola archivos tooyour VM:

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. SSH nuevamente en la máquina virtual de Oracle en Azure en archivos de .zip de orden toomove hello en hello / opt carpeta. A continuación, cambie el propietario de Hola de archivos de hello:

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. Descomprimir archivos de Hola. (Instalación Hola Linux descomprima herramienta si aún no está instalado).
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. Cambie el permiso:
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. Actualice el espacio de intercambio configurado. Componentes de la cuadrícula de Oracle necesitan al menos 6.8 GB de espacio de intercambio tooinstall cuadrícula. tamaño de archivo de intercambio de Hello predeterminado para las imágenes de Oracle Linux en Azure es solo de 2048MB. Necesita tooincrease `ResourceDisk.SwapSizeMB` en hello `/etc/waagent.conf` archivo y reinicie el servicio de WALinuxAgent de hello en orden para hello actualizar configuración tootake efecto. Dado que es un archivo de solo lectura, necesita acceso de escritura de tooenable de permisos de archivo de toochange.

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   Busque `ResourceDisk.SwapSizeMB` y cambie el valor de hello demasiado**8192**. Necesitará toopress `insert` tooenter modo de inserción, tipo de valor de Hola de **8192** y, a continuación, presione `esc` tooreturn toocommand modo. cambios de hello toowrite y archivo de hello quit, escriba `:wq` y presione `enter`.
   
   > [!NOTE]
   > Se recomienda usar siempre `WALinuxAgent` tooconfigure espacio de intercambio para que siempre se crea en Hola efímero disco local (disco temporal) para mejorar el rendimiento. Para obtener más información sobre, consulte [cómo tooadd un intercambio de archivos de máquinas virtuales de Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a>Preparar el cliente local y la máquina virtual toorun x11
Configuración de Oracle ASM requiere una interfaz gráfica toocomplete Hola instalación y configuración. Estamos usando hello x11 protocolo toofacilitate esta instalación. Si usas un sistema de cliente (Mac o Linux) que ya tiene X11 capacidades habilitada y configurada: puede omitir esta configuración y configurar máquinas de tooWindows exclusivo. 

1. [Descargar PuTTY](http://www.putty.org/) y [descargar Xming](https://xming.en.softonic.com/) tooyour equipo de Windows. Necesitará la instalación de hello toocomplete de ambas de estas aplicaciones con los valores predeterminados de hello antes de continuar.

2. Después de instalar PuTTY, abra un símbolo del sistema, cambie a Hola PuTTY carpeta (por ejemplo, C:\Program Files\PuTTY) y ejecutar `puttygen.exe` en orden toogenerate una clave.

3. En PuTTY Key Generator:
   
   1. Generar una clave seleccionando hello `Generate` botón.
   2. Copie el contenido de Hola de clave de hello (Ctrl + C).
   3. Seleccione hello `Save private key` botón.
   4. Omitir la advertencia Hola sobre la protección de clave de hello con una frase de contraseña y, a continuación, seleccione `OK`.

   ![Captura de pantalla de PuTTY Key Generator](./media/oracle-asm/puttykeygen.png)

4. En la máquina virtual, ejecute estos comandos:

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. Cree un archivo llamado `authorized_keys`. Pegar contenido de Hola de clave de hello en este archivo y, a continuación, guarde el archivo hello.

   > [!NOTE]
   > clave de Hello debe contener la cadena de hello `ssh-rsa`. Además, el contenido de Hola de clave de hello debe ser una sola línea de texto.
   >  

6. En el sistema cliente, inicie PuTTY. Hola **categoría** panel, vaya demasiado**conexión** > **SSH** > **Auth**. Hola **archivo de clave privada para la autenticación** cuadro, busque la clave de toohello que ha generado anteriormente.

   ![Captura de pantalla de opciones de autenticación de SSH de Hola](./media/oracle-asm/setprivatekey.png)

7. Hola **categoría** panel, vaya demasiado**conexión** > **SSH** > **X11**. Seleccione hello **X11 de habilitar el reenvío** casilla de verificación.

   ![Captura de pantalla de hello SSH X11 opciones de reenvío](./media/oracle-asm/enablex11.png)

8. Hola **categoría** panel, vaya demasiado**sesión**. Escriba la máquina virtual de ASM de Oracle `<publicIPaddress>` en el cuadro de diálogo de nombre de host de hello rellene un nuevo `Saved Session` asigne un nombre y, a continuación, haga clic en `Save`.  Una vez guardado, haga clic en `open` tooconnect tooyour Oracle ASM virtual machine.  Hola primera vez que se conecte también le advertirá de sistema remoto hello no se almacena en caché en el registro. Haga clic en `yes` tooadd lo y continuar.

   ![Captura de pantalla de opciones de sesión de PuTTY Hola](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a>Instalación de Oracle Grid Infrastructure

tooinstall infraestructura de red de Oracle, Hola completa pasos:

1. Inicie sesión como **grid**. (Debe ser capaz de toosign en sin que se solicite una contraseña). 

   > [!NOTE]
   > Si está ejecutando Windows, asegúrese de que ha iniciado la Xming antes de comenzar la instalación de Hola.

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   Se abre el instalador de Oracle Grid Infrastructure 12c versión 1. (Puede tardar unos minutos para hello instalador toostart.)

2. En hello **seleccione la opción de instalación** , seleccione **instalar y configurar la infraestructura de red de Oracle para un servidor independiente**.

   ![Captura de pantalla de la página de seleccionar la opción de instalación del instalador de Hola](./media/oracle-asm/install01.png)

3. En hello **seleccionar idiomas de producto** página, asegúrese de **inglés** o se selecciona Hola idioma que desee.  Haga clic en `next`.

4. En hello **crear grupo de discos ASM** página:
   - Escriba un nombre para el grupo de discos de Hola.
   - En **Redundancy** (Redundancia), seleccione **External** (Externa).
   - En **Allocation Unit Size** (Tamaño de la unidad de asignación), seleccione **4**.
   - En **Add Disks** (Agregar discos), seleccione **ORCLASMSP**.
   - Haga clic en `next`.

5. En hello **especificar la contraseña de ASM** página, seleccione hello **Use las mismas contraseñas para estas cuentas** opción y escriba una contraseña.

   ![Captura de pantalla de página de especificar la contraseña de ASM del instalador de Hola](./media/oracle-asm/install04.png)

6. En hello **especificar opciones de administración** página, tienen Hola opción tooconfigure Control de EM en la nube. Se va a omitir esta opción, haga clic `next` toocontinue. 

7. En hello **grupos con privilegios de sistema operativo** , utilice la configuración predeterminada de Hola. Haga clic en `next` toocontinue.

8. En hello **especificar la ubicación de instalación** , utilice la configuración predeterminada de Hola. Haga clic en `next` toocontinue.

9. En hello **crear inventario** página, cambie Hola Directory inventario demasiado`/u01/app/grid/oraInventory`. Haga clic en `next` toocontinue.

   ![Captura de pantalla de la página de inventario de crear del instalador de Hola](./media/oracle-asm/install08.png)

10. En hello **configuración de ejecución de secuencia de comandos de raíz** página, seleccione hello **ejecutar automáticamente los scripts de configuración** casilla de verificación. A continuación, seleccione hello **usar credenciales de usuario de "root"** opción y escriba la contraseña de usuario de hello raíz.

    ![Captura de pantalla de la página de configuración de ejecución de secuencia de comandos del instalador de hello raíz](./media/oracle-asm/install09.png)

11. En hello **realizar comprobaciones de requisitos previos** página, el programa de instalación actual de hello producirá errores. Este es un comportamiento esperado. Seleccione `Fix & Check Again`.

12. Hola **Script de corrección** cuadro de diálogo, haga clic en `OK`.

13. En hello **resumen** página, revise la configuración seleccionada y, a continuación, haga clic en `Install`.

    ![Captura de pantalla de la página de resumen del instalador de Hola](./media/oracle-asm/install12.png)

14. Aparece un cuadro de diálogo de advertencia que le informa de los scripts de configuración necesario toobe que se ejecute como un usuario con privilegios. Haga clic en `Yes` toocontinue.

15. En hello **finalizar** página, haga clic en `Close` instalación de hello toofinish.

## <a name="set-up-your-oracle-asm-installation"></a>Configuración de la instalación de ASM de Oracle

tooset en la instalación de Oracle ASM completa Hola pasos:

1. Asegúrese de que sigue conectado como **grid** desde su sesión de X11. Es posible que tenga toohit `enter` toorevive Hola terminal. A continuación, inicie Hola Oracle Automated Storage Management Asistente para la configuración:

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   Se abre el asistente para la configuración de ASM de Oracle.

2. Hola **configurar ASM: grupos de discos** diálogo cuadro, haga clic en hello `Create` botón y, a continuación, haga clic en `Show Advanced Options`.

3. Hola **crear grupo de discos** cuadro de diálogo:

   - Escriba el nombre de grupo del disco de hello **datos**.
   - En **Select Member Disks** (Seleccionar discos miembro), seleccione **ORCL_DATA** y **ORCL_DATA1**.
   - En **Allocation Unit Size** (Tamaño de la unidad de asignación), seleccione **4**.
   - Haga clic en `ok` grupo de discos toocreate Hola.
   - Haga clic en `ok` ventana de confirmación de tooclose Hola.

   ![Captura de pantalla del cuadro de diálogo Crear grupo de discos de Hola](./media/oracle-asm/asm02.png)

4. Hola **configurar ASM: grupos de discos** diálogo cuadro, haga clic en hello `Create` botón y, a continuación, haga clic en `Show Advanced Options`.

5. Hola **crear grupo de discos** cuadro de diálogo:

   - Escriba el nombre de grupo del disco de hello **FRA**.
   - En **Redundancy** (Redundancia), seleccione **External (none)** (Externa [ninguna]).
   - En **Select Member Disks** (Seleccionar discos miembro), seleccione **ORCL_FRA**.
   - En **Allocation Unit Size** (Tamaño de la unidad de asignación), seleccione **4**.
   - Haga clic en `ok` grupo de discos toocreate Hola.
   - Haga clic en `ok` ventana de confirmación de tooclose Hola.

   ![Captura de pantalla del cuadro de diálogo Crear grupo de discos de Hola](./media/oracle-asm/asm04.png)

6. Seleccione **Exit** tooclose Asistente para la configuración de ASM.

   ![Captura de pantalla de Hola configurar ASM: cuadro de diálogo de grupos de discos con botón Salir](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a>Crear base de datos de Hola

Hola software de base de datos de Oracle ya está instalado en la imagen de hello Azure Marketplace. toocreate una base de datos completa Hola pasos:

1. Cambiar superusuario de Oracle toohello de los usuarios y, a continuación, inicializar el agente de escucha de hello para el registro:

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   Se abre el asistente para la configuración de la base de datos.

2. En hello **operación de base de datos** página, haga clic en `Create Database`.

3. En hello **modo de creación** página:

   - Escriba un nombre para la base de datos de Hola.
   - Para **Storage Type** (Tipo de almacenamiento), asegúrese de que **Automatic Storage Management (ASM)** está seleccionado.
   - Para **ubicación de archivos de base de datos**, usar valor predeterminado de hello ASM sugiere la ubicación.
   - Para **rápida recuperación área**, usar valor predeterminado de hello ASM sugiere la ubicación.
   - Escriba una **contraseña administrativa** y **confirme la contraseña**.
   - Asegúrese de que `create as container database` está seleccionado.
   - Escriba un valor de `pluggable database name`.

4. En hello **resumen** página, revise la configuración seleccionada y, a continuación, haga clic en `Finish` base de datos de toocreate Hola.

   ![Captura de pantalla de la página de resumen de Hola](./media/oracle-asm/createdb03.png)

5. Hola base de datos se ha creado. En hello **finalizar** página, tienen Hola opción toounlock cuentas adicionales toouse esta base de datos y cambiar las contraseñas de Hola. Si lo desea, toodo, seleccione **administración de contraseñas** -en caso contrario, haga clic en `close`.

## <a name="delete-hello-vm"></a>Eliminar Hola VM

Oracle Automated Storage Management se ha configurado correctamente en la imagen de la base de datos de Oracle de Hola de hello Azure Marketplace.  Cuando ya no necesita esta máquina virtual, puede usar Hola después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

[Tutorial: Configuración de Oracle DataGuard](configure-oracle-dataguard.md)

[Tutorial: Configuración de Oracle GoldenGate](Configure-oracle-golden-gate.md)

Revise [Diseño de una base de datos de Oracle](oracle-design.md)
