---
title: "aaaHow tooinstall un servidor de destino maestro de Linux para conmutación por error desde Azure tooon-local | Documentos de Microsoft"
description: "Antes de volver a proteger una máquina virtual Linux, necesita un servidor de destino maestro Linux. Obtenga información acerca de cómo tooinstall uno."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a>Instalación de un servidor de destino maestro Linux
Después de conmutar las máquinas virtuales, puede producir un error al sitio local toohello Hola atrás máquinas virtuales. toofail nuevo, deberá tooreprotect Hola virtual máquina desde el sitio de Azure toohello local. En este proceso, es necesario un tráfico de hello local tooreceive de servidor de destino maestro. 

Si la máquina virtual protegida es una máquina virtual Windows, necesitará un destino maestro de Windows. Para una máquina virtual Linux, se necesita un destino maestro de Linux. Lectura Hola siguientes pasos le indican toolearn cómo maestro toocreate e instale un Linux de destino.

> [!IMPORTANT]
> A partir de la versión del servidor de destino maestro hello 9.10.0, servidor de destino maestro más reciente de hello puede solo instalarse en un servidor de Ubuntu 16.04. Las nuevas instalaciones no están permitidas en servidores CentOS6.6. Sin embargo, puede seguir tooupgrade los servidores de destino maestra antigua mediante hello 9.10.0 versión.

## <a name="overview"></a>Información general
Este artículo proporciona instrucciones para cómo maestro tooinstall una Linux de destino.

Enviar comentarios o preguntas al final de Hola de este artículo o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Requisitos previos

* host de hello toochoose en qué destino maestro de hello toodeploy, determinar si Hola conmutación por recuperación se va toobe tooan locales existentes máquina virtual o una máquina virtual nueva de tooa. 
    * Para una máquina virtual existente, host de hello del destino maestro Hola debe tener acceso a almacenes de datos toohello de máquina virtual de Hola.
    * Si no existe la máquina virtual de hello en local, máquina virtual de conmutación por recuperación de Hola se crea en Hola mismo host como destino maestro Hola. Puede elegir cualquier host ESXi destino maestro de tooinstall Hola.
* destino maestro Hola debe estar en una red que puede comunicarse con el servidor de procesos de Hola y el servidor de configuración de Hola.
* versión de Hola de destino maestro de Hola debe ser igual tooor anteriores a las versiones de servidor de procesos de Hola y el servidor de configuración de Hola Hola. Por ejemplo, si versión Hola Hola del servidor de configuración se 9.4, versión de Hola de destino maestro Hola pueda 9.4 o 9.3 pero no 9,5.
* destino maestro Hola solo puede tener una máquina virtual VMware y no un servidor físico.

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a>Crear el destino maestro Hola según toohello directrices de ajuste de tamaño

Crear el destino maestro de hello según Hola siguiendo las directrices de ajuste de tamaño:
- **RAM**: 6 GB o más
- **Tamaño de disco de SO**: 100 GB o más (tooinstall CentOS6.6)
- **Tamaño adicional de disco para la unidad de retención**: 1 TB
- **Núcleos de CPU**: 4 núcleos o más

siguiente Hola admite Ubuntu kernels son compatibles.


|Serie de kernel  |Admitir hasta demasiado |
|---------|---------|
|4.4.      |4.4.0-81-generic         |
|4.8      |4.8.0-56-generic         |
|4.10     |4.10.0-24-generic        |


## <a name="deploy-hello-master-target-server"></a>Implementar el servidor de destino maestro Hola

### <a name="install-ubuntu-16042-minimal"></a>Instalación de Ubuntu 16.04.2 mínima

Tomar Hola después de sistema operativo de 64 bits Ubuntu 16.04.2 de hello pasos tooinstall Hola.

**Paso 1:** vaya toohello [vínculo de descarga](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) y elija reflejado más cercano de Hola desde que descargar una imagen de ISO de 64 bits mínima de Ubuntu 16.04.2.

Mantener una imagen de ISO de 64 bits mínima de Ubuntu 16.04.2 en la unidad de DVD de hello e inicie el sistema de Hola.

**Paso 2:** seleccione **English** (Inglés) como idioma preferido y luego **Entrar**.

![Selección de un idioma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**Paso 3:** seleccione **Install Ubuntu Server** (Instalar servidor Ubuntu) y luego **Entrar**.

![Selección de instalación de servidor Ubuntu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**Paso 4:** seleccione **English** (Inglés) como idioma preferido y luego **Entrar**.

![Selección de inglés como idioma preferido](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**Paso 5:** seleccione Hola opción adecuada de hello **zona horaria** lista de opciones y, a continuación, seleccione **ENTRAR**.

![Seleccione la zona horaria correcta de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**Paso 6:** seleccione **No** (hello la opción predeterminada) y, a continuación, seleccione **ENTRAR**.


![Configurar el teclado de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**Paso 7:** seleccione **inglés (Estados Unidos)** como Hola país de origen para el teclado de hello y, a continuación, seleccione **ENTRAR**.

![Seleccionar Estados Unidos como país Hola de origen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**Paso 8:** seleccione **inglés (Estados Unidos)** como distribución del teclado hello y, a continuación, seleccione **ENTRAR**.

![Seleccione el inglés de Estados Unidos como la distribución del teclado Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**Paso 9:** escriba el nombre de host de hello para el servidor en hello **Hostname** cuadro y, a continuación, seleccione **continuar**.

![Escriba el nombre de host de hello para el servidor](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**Paso 10:** toocreate una cuenta de usuario, escriba el nombre de usuario de hello y, a continuación, seleccione **continuar**.

![Crea una cuenta de usuario](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**Paso 11:** escribir contraseña de hello para la nueva cuenta de usuario de hello y, a continuación, seleccione **continuar**.

![Escriba la contraseña de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**Paso 12:** Confirmar contraseña Hola Hola nuevo usuario y, a continuación, seleccione **continuar**.

![Confirmar las contraseñas de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**Paso 13:** seleccione **No** (hello la opción predeterminada) y, a continuación, seleccione **ENTRAR**.

![Configuración de usuarios y contraseñas](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**Paso 14:** si la zona horaria de Hola que se muestra es correcto, seleccione **Sí** (hello la opción predeterminada) y, a continuación, seleccione **ENTRAR**.

tooreconfigure su zona horaria, seleccione **No**.

![Configurar el reloj de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**Paso 15:** en hello opciones del método de creación de particiones, seleccione **interactiva - usar todo el disco**y, a continuación, seleccione **ENTRAR**.

![Seleccione la opción método de creación de particiones de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**Paso 16:** seleccione Hola disco adecuado de hello **Seleccionar disco toopartition** opciones y, a continuación, seleccione **ENTRAR**.


![Seleccione el disco de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**Paso 17:** seleccione **Sí** toowrite Hola toodisk de cambios y, a continuación, seleccione **ENTRAR**.

![Escribir Hola cambios toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**Paso 18:** seleccione la opción predeterminada de hello, seleccione **continuar**y, a continuación, seleccione **ENTRAR**.

![Seleccione la opción predeterminada de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**Paso 19:** seleccione Hola la opción adecuada para administrar las actualizaciones en el sistema y, a continuación, seleccione **ENTRAR**.

![Seleccione cómo se actualiza toomanage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Porque el servidor de destino maestro de Azure Site Recovery Hola requiere una versión muy específica de hello Ubuntu, deberá tooensure ese kernel Hola se deshabilitan las actualizaciones para la máquina virtual de Hola. Si están habilitadas, las actualizaciones normales provocar toomalfunction de servidor de destino maestro Hola. Asegúrese de seleccionar hello **ninguna actualización automática** opción.


**Paso 20:** seleccione las opciones predeterminadas. Si desea que openSSH para la conexión de SSH, seleccione hello **server OpenSSH** opción y, a continuación, seleccione **continuar**.

![Selección de software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**Paso 21:** seleccione **Sí** y luego **Entrar**.

![Cargador de arranque GRUB Hola de instalación](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**Paso 22:** seleccione Hola dispositivo adecuado para la instalación de cargador de arranque de hello (preferiblemente **/dev/sda**) y, a continuación, seleccione **ENTRAR**.

![Selección de un dispositivo para la instalación del cargador de arranque](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**Paso 23:** seleccione **continuar**y, a continuación, seleccione **ENTRAR** instalación de hello toofinish.

![Finalizar la instalación de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

Cuando haya finalizado la instalación de hello, inicie sesión en toohello VM con las nuevas credenciales de usuario Hola. (Consulte demasiado**paso 10** para obtener más información.)

Realice los pasos de Hola que se describen en la siguiente captura de pantalla tooset Hola raíz de hello contraseña de usuario. Luego inicie sesión como usuario raíz.

![Contraseña de usuario de conjunto Hola raíz](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a>Preparar la máquina de hello para la configuración como un servidor de destino maestro
A continuación, prepare máquina de hello para la configuración como un servidor de destino maestro.

Id. de hello tooget para cada disco duro de SCSI en una máquina virtual de Linux, habilitar hello **disco. EnableUUID = TRUE** parámetro.

tooenable este parámetro, Hola toman siguiendo los pasos:

1. Apague la máquina virtual.

2. Haga clic en la entrada de hello para la máquina virtual de hello en el panel izquierdo de Hola y, a continuación, seleccione **modificar configuración**.

3. Seleccione hello **opciones** ficha.

4. En el panel izquierdo de hello, seleccione **avanzadas** > **General**y, a continuación, seleccione hello **parámetros de configuración** botón en la parte inferior derecha de Hola de pantalla de bienvenida.

    ![Pestaña de opciones](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    Hola **parámetros de configuración** opción no está disponible cuando se está ejecutando la máquina de Hola. toomake esta ficha activa, apagar la máquina virtual de Hola.

5. Vea si ya existe una fila con **disk.EnableUUID**.

    - Si el valor de hello existe y está establecido demasiado**False**, cambie el valor de hello demasiado**True**. (los valores de hello no distinguen mayúsculas de minúsculas).

    - Si el valor de hello existe y está establecido demasiado**True**, seleccione **cancelar**.

    - Si no existe el valor de hello, seleccione **Agregar fila**.

    - En la columna de nombre de hello, agregue **disco. EnableUUID**y, a continuación, establezca el valor de hello demasiado**TRUE**.

    ![Comprobación de si el disk.EnableUUID existe](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>Deshabilitación de actualizaciones de kernel

Servidor de destino maestro de Azure Site Recovery requiere una versión muy específica de hello Ubuntu, asegúrese de que las actualizaciones de kernel Hola están deshabilitadas para la máquina virtual de Hola.

Si están habilitadas las actualizaciones de kernel, las actualizaciones normales provocar toomalfunction de servidor de destino maestro Hola.

#### <a name="download-and-install-additional-packages"></a>Descarga e instalación de paquetes adicionales

> [!NOTE]
> Asegúrese de que tiene toodownload de conectividad de Internet e instale paquetes adicionales. Si no tiene conectividad a Internet, necesita toomanually encontrar estos paquetes RPM e instalarlas.

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a>Obtener el instalador de hello para el programa de instalación

Si el destino maestro tiene conectividad a Internet, puede usar Hola después de instalador de pasos toodownload Hola. En caso contrario, puede copiar a instalador Hola Hola servidor de procesos y, a continuación, vuelva a instalarlo.

#### <a name="download-hello-master-target-installation-packages"></a>Descargar los paquetes de instalación de destino maestro Hola

[Descargar los bits de instalación de Linux más recientes de hello destino maestro](https://aka.ms/latestlinuxmobsvc).

toodownload mediante Linux, tipo:

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

Asegúrese de que se descargue y descomprima al instalador de hello en su directorio particular. Si se descomprimen demasiado**/usr/Local**, a continuación, se produce un error en la instalación de Hola.


#### <a name="access-hello-installer-from-hello-process-server"></a>Instalador de Access Hola Hola del servidor de procesos

1. En el servidor de procesos de Hola y vaya demasiado**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.

2. Copie el archivo de instalador necesarios de Hola Hola servidor de procesos y guárdelo como **latestlinuxmobsvc.tar.gz** en su directorio particular.


### <a name="apply-custom-configuration-changes"></a>Aplicación de cambios en la configuración personalizada

cambios de configuración personalizada de tooapply, usar hello pasos:


1. Ejecute hello después binario de comando toountar Hola.
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Captura de pantalla de hello comando toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. Siguiente ejecución Hola comando toogive permiso.
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. Ejecute hello sigue la secuencia de comandos toorun Hola.
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Ejecutar script de Hola solo una vez en el servidor de Hola. Apague el servidor de Hola. A continuación, reinicie servidor hello después de agregar un disco, como se describe en la sección siguiente Hola.

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a>Agregar una máquina virtual del destino maestro de Linux de retención disco toohello

Usar hello siguiendo los pasos toocreate un disco de retención:

1. Adjuntar una nueva máquina de virtual de disco de 1 TB toohello Linux destino maestro y, a continuación, inicie el equipo de Hola.

2. Hola de uso **comando multipath -ll** identificador de comando toolearn Hola múltiples rutas de acceso del disco de retención de Hola.

    ```
    multipath -ll
    ```
    ![Id. de múltiples rutas de Hello del disco de retención de Hola](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. Formatear la unidad de hello y, a continuación, cree un sistema de archivos en la nueva unidad de Hola.

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Crear un sistema de archivos en la unidad de Hola](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. Después de crear el sistema de archivos de hello, montar el disco de retención de Hola.
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Disco de retención de Hola de montaje](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. Crear hello **fstab** unidad de retención de Hola de entrada toomount cada vez que inicia el sistema de Hola.
    ```
    vi /etc/fstab
    ```
    Seleccione **insertar** toobegin Editar archivo hello. Crear una nueva línea y, a continuación, insertar Hola después de texto. Editar Hola disco identificador múltiples rutas de acceso basado en Id. de múltiples rutas de hello resaltado del comando anterior Hola.

    **/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**

    Seleccione **Esc**y, a continuación, escriba **: wq** (escribir y salir) ventana del editor tooclose Hola.

### <a name="install-hello-master-target"></a>Instalar el destino maestro Hola

> [!IMPORTANT]
> versión de Hola Hola maestra del servidor de destino debe ser anterior a las versiones de servidor de procesos de Hola y el servidor de configuración de Hola Hola tooor igual. Si no se cumple esta condición, la reprotección se realiza correctamente, pero se produce un error en la replicación.


> [!NOTE]
> Antes de instalar el servidor de destino maestro de hello, compruebe que hello **/etcetera/hosts** archivo en la máquina virtual de hello contiene entradas que se asignan direcciones IP de toohello de nombre de host local de Hola que están asociadas con todos los adaptadores de red.

1. Copie la frase de contraseña de Hola de **C:\ProgramData\Microsoft Azure sitio Recovery\private\connection.passphrase** en el servidor de configuración de Hola. A continuación, guárdelo como **passphrase.txt** Hola mismo directorio local mediante la ejecución de Hola el siguiente comando:

    ```
    echo <passphrase> >passphrase.txt
    ```
    Ejemplo: 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. Anote la dirección IP del servidor de configuración de Hola. Se necesitará en el paso siguiente de Hola.

3. Ejecute hello siguiente servidor de destino maestro de comando tooinstall hello y registre el servidor de hello con servidor de configuración de Hola.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    Ejemplo: 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    Espere a que finalice el script de Hola. Si el destino maestro Hola registra correctamente, destino maestro Hola aparece en hello **infraestructura del sitio de recuperación** página del portal de Hola.


#### <a name="install-hello-master-target-by-using-interactive-installation"></a>Instalar el destino maestro hello mediante la instalación interactiva

1. Ejecute hello siguiendo el destino maestros del comando tooinstall Hola. Para el rol de agente de hello, elija **destino maestro**.

    ```
    ./install
    ```

2. Elegir ubicación predeterminada de hello para la instalación y, a continuación, seleccione **ENTRAR** toocontinue.

    ![Elección de una ubicación predeterminada para la instalación del destino maestro](./media/site-recovery-how-to-install-linux-master-target/image17.png)

Cuando haya finalizado la instalación de hello, registrar el servidor de configuración de hello mediante el uso de la línea de comandos de Hola.

1. Anote la dirección IP de Hola Hola del servidor de configuración. Se necesitará en el paso siguiente de Hola.

2. Ejecute hello siguiente servidor de destino maestro de comando tooinstall hello y registre el servidor de hello con servidor de configuración de Hola.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    Ejemplo: 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   Espere a que finalice el script de Hola. Si el destino maestro de hello está registrado correctamente, destino maestro Hola aparece en hello **infraestructura del sitio de recuperación** página del portal de Hola.


### <a name="upgrade-hello-master-target"></a>Actualizar el destino maestro Hola

Ejecute al instalador de Hola. Detecta automáticamente que ese agente Hola está instalado en el destino maestro Hola. tooupgrade, seleccione **Y**.  Una vez completado el programa de instalación de hello, comprobar la versión de Hola de destino maestro Hola instalado mediante el siguiente comando de Hola.

    ```
    cat /usr/local/.vx_version
    ```

Puede ver que hello **versión** campo proporciona el número de versión de Hola de destino maestro Hola.

### <a name="install-vmware-tools-on-hello-master-target-server"></a>Instalar las herramientas de VMware en el servidor de destino maestro Hola

Debe tooinstall las herramientas de VMware en el destino maestro de Hola para que puedan detectar Hola almacenes de datos. Si no se instalan herramientas de hello, pantalla de bienvenida reprotección no aparece en los almacenes de datos de Hola. Tras la instalación de las herramientas de VMware hello, deberá toorestart.

## <a name="next-steps"></a>Pasos siguientes
Después de instalación de Hola y el registro de destino maestro hello tiene finsihed, puede ver destino maestro Hola aparecen en hello **destino maestro** sección **infraestructura del sitio de recuperación**, bajo Hola información general del servidor de configuración.

Ahora ya puede continuar con la [reprotección](site-recovery-how-to-reprotect.md), seguido de la conmutación por recuperación.

## <a name="common-issues"></a>Problemas comunes

* Asegúrese de no activar Storage vMotion en ningún componente de administración como, por ejemplo, un destino maestro. Si se mueve destino maestro Hola después un reprotección correcta, no se puede desasociar discos de máquina virtual de hello (VMDK). En este caso se produce un error en la conmutación por recuperación.

* destino maestro Hello no debería tener todas las instantáneas de máquina virtual de Hola. Si hay instantáneas, se produce un error en la conmutación por recuperación.

* Debido a la configuración de la NIC de personalizada de toosome en algunos clientes, está deshabilitada de interfaz de red de Hola durante el inicio y no se puede inicializar el agente de destino maestro Hola. Asegúrese de que ese Hola propiedades siguientes se han definido correctamente. Comprobar /etc/sysconfig/network-scripts/ifcfg del archivo de tarjeta de estas propiedades en hello Ethernet-eth *.
    * BOOTPROTO=dhcp
    * ONBOOT=yes
