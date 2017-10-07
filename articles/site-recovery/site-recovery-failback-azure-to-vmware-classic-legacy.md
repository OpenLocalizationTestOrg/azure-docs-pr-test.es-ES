---
title: "aaaFail nuevo máquinas virtuales de VMware de Azure en el portal clásico heredado de Hola | Documentos de Microsoft"
description: "Este artículo describe cómo toofail copia una máquina virtual de VMware que se ha había replicado tooAzure con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a>Frente a errores atrás máquinas virtuales de VMware y servidores físicos desde Azure tooVMware con Azure Site Recovery (heredado)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-failback-azure-to-vmware.md)
> * [Portal de Azure clásico](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portal de Azure clásico (heredado)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Este artículo describe cómo toofail atrás máquinas de virtuales de VMware y servidores físicos de Windows/Linux de sitio de Azure tooyour local una vez que haya replicado desde el entorno local del sitio tooAzure utilizando [Azure Site Recovery?](site-recovery-overview.md).

En este artículo se describe una configuración anterior y no debe usarse para almacenes nuevos.

## <a name="architecture"></a>Arquitectura
Este diagrama representa el escenario de conmutación por error y conmutación por recuperación de Hola. líneas de Hello azul son las conexiones de hello utilizadas durante la conmutación por error. líneas de Hello rojo son conexiones de hello utilizadas durante la conmutación por recuperación. líneas de Hello con flechas sobrepasar Hola internet.

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a>Antes de comenzar
* Debe haber conmutado por recuperación sus máquinas virtuales de VMware o servidores físicos y deben estar ejecutándose en Azure.
* Tenga en cuenta que solo puede fallar atrás máquinas virtuales de VMware y servidores físicos de Windows/Linux desde máquinas virtuales de Azure tooVMware en el sitio primario de hello en local.  Si está fallando volver una máquina física, conmutación por error tooAzure convertirá tooan máquina virtual de Azure y conmutación por recuperación tooVMware lo convertirá tooa VM de VMware.

Esta es la instalación de la conmutación por recuperación:

1. **Configurar componentes de conmutación por recuperación**: necesitará tooset de un servidor de vContinuum de forma local y haga que señale el servidor de configuración de toohello VM en Azure. También deberá configurar un servidor de procesos como un servidor de destino maestro de máquina virtual de Azure toosend datos toohello atrás local. Registrar servidor de procesos de hello con servidor de configuración de Hola que administra Hola conmutación por error. Se instala un servidor maestro de destino local. Si necesita un servidor maestro de destino de Windows, se instala automáticamente al instalar vContinuum. Si necesita Linux necesitará tooset, configúrelo manualmente en un servidor independiente.
2. **Habilitar la protección y la conmutación por recuperación**: después de configurar los componentes de hello, en vContinuum necesitará tooenable protección para conmutado por error máquinas virtuales de Azure. Podrá ejecutar una comprobación de preparación en hello las máquinas virtuales y ejecutar una conmutación por error desde el sitio de Azure tooyour local. Una vez finalizada la conmutación por recuperación se vuelva a proteger equipos locales para que se inicie replicar tooAzure.

## <a name="step-1-install-vcontinuum-on-premises"></a>Paso 1: Instalación local de vContinuum
Podrá necesita tooinstall un servidor vContinuum de forma local y seleccione servidor de configuración de toohello.

1. [Descargue vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).
2. A continuación, descargue hello [vContinuum actualización](http://go.microsoft.com/fwlink/?LinkID=533813) versión.
3. Instale la versión más reciente de Hola de vContinuum. En hello **bienvenida** página haga clic en **siguiente**.
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. En la primera página del Asistente para Hola de hello especificar dirección IP del servidor de hello CX y puerto del servidor CX Hola. Seleccione **Use HTTPS**(Usar HTTPS).

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. Buscar dirección IP de servidor de configuración de hello en hello **panel** ficha Hola del servidor de configuración VM en Azure.
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. Buscar el servidor de configuración de hello HTTPS puerto público en hello **extremos** ficha Hola del servidor de configuración VM en Azure.

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. En hello **detalles de la frase de contraseña de CS** página Especifique la frase de contraseña de Hola que anotó hacia abajo al registrar el servidor de configuración de Hola. Si no recuerdas es registrarse **C:\\archivos de programa (x86)\\InMage sistemas\\privada\\connection.passphrase** en la máquina virtual del servidor de configuración de Hola.

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. Hola **Seleccionar ubicación de destino** página Especifique dónde desea tooinstall hello vContinuum servidor y haga clic en **instalar**.

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. Una vez que se complete la instalación, puede iniciar vContinuum.
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a>Paso 2: Instalación de un servidor de procesos de Azure
Tendrá que tooinstall un servidor de proceso de Azure para que hello las máquinas virtuales en Azure pueden enviar el servidor de destino maestro local de hello datos tooan atrás.

1. En hello **servidores de configuración** página en Azure, seleccione tooadd un nuevo servidor de procesos.

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. Especifique un nombre de servidor de procesos y un nombre y una contraseña tooconnect toohello máquina como administrador. Seleccione toowhich servidor hello configuración que desea que el servidor de procesos de tooregister Hola. Debe ser Hola mismo servidor que está usando tooprotect y conmutar por error las máquinas virtuales.
3. Especificar hello Azure red qué Hola se debe implementar el servidor de procesos. Debe ser Hola misma red que el servidor de configuración de Hola. Especifique una subred con una dirección IP única seleccionada y comience la implementación.

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. Un trabajo es servidor de procesos de hello toodeploy desencadenadas.

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. Una vez implementado el servidor de procesos de hello en Azure puede iniciar sesión en servidor de hello mediante credenciales de Hola que especificó. Registrar el servidor de procesos de Hola Hola igual registrado Hola proceso servidor local.

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> servidores de Hello registrados durante la conmutación por recuperación no serán visibles en Propiedades de la máquina virtual en recuperación del sitio. Solo están visibles en hello **servidores** ficha de hello Configuración servidor toowhich se registran. Puede tardar unos 10 a 15 minutos hasta que Hola proceso servidor aparece en la pestaña de Hola.
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a>Paso 3: Instalación de un servidor de destino maestro local
Dependiendo del sistema operativo de máquinas virtuales de origen, deberá tooinstall un Linux o un servidor de destino maestro de Windows de forma local.

### <a name="deploy-a-windows-master-target-server"></a>Implementación de un servidor de destino maestro con Windows
El programa de instalación de vContinuum incluye un destino maestro con Windows. Cuando se instala vContinuum hello, un servidor principal también se implementa en hello mismo equipo y el servidor de configuración de toohello registrados.

1. implementación de toobegin, crear vacío máquina local en el host ESX hello en el que desea toorecover hello las máquinas virtuales de Azure.
2. Asegúrese de que hay al menos dos discos conectados toohello VM: uno se utiliza para el sistema operativo de Hola y Hola otro se usa para la unidad de retención de Hola.
3. Instalar el sistema operativo de Hola.
4. Instale vContinuum hello en el servidor de Hola. También con esto finaliza la instalación del servidor de destino maestro Hola.

### <a name="deploy-a-linux-master-target-server"></a>Implementación de un servidor de destino maestro con Linux
1. implementación de toobegin, crear vacío máquina local en el host ESX hello en el que desea toorecover hello las máquinas virtuales de Azure.
2. Asegúrese de que hay al menos dos discos conectados toohello VM: uno se utiliza para el sistema operativo de Hola y Hola otro se usa para la unidad de retención de Hola.
3. Instalar el sistema operativo de Linux de Hola. Hola sistema de destino maestro de Linux no debe usar LVM de retención o raíz de espacios de almacenamiento. Un servidor de destino maestro de Linux configura detección de particiones o discos LVM tooavoid de forma predeterminada.
4. Estas son las particiones que puede crear:

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. Realizar Hola por debajo de los pasos posteriores a la instalación antes de comenzar la instalación de destino maestro Hola.

#### <a name="post-os-installation-steps"></a>Pasos posteriores a la instalación del sistema operativo:
tooget Hola identificadores de SCSI para cada disco duro de SCSI en una máquina virtual de Linux, habilitar el parámetro hello "disco. EnableUUID = TRUE "como sigue:

1. Apague la máquina virtual.
2. Haga clic en la entrada de la máquina virtual de hello en el panel izquierdo de hello > **modificar configuración**.
3. Haga clic en hello **opciones** ficha. Seleccione **Opciones avanzadas\>General item (Elemento general)** > **Parámetros de configuración**. Hola **parámetros de configuración** opción sólo está disponible cuando se apague la máquina de Hola.

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. Comprueba si existe alguna fila con **disk.EnableUUID** . Si aún está establecido demasiado**False** establecido demasiado**True** (no entre mayúsculas y minúsculas). Si existe y es establecer tootrue, haga clic en **cancelar** y pruebe el comando de SCSI de hello dentro de hello sistema operativo después de se hayan arrancado. Si no existe, haga clic **Add Row**(Agregar fila).
5. Agregar el disco. EnableUUID Hola **nombre** columna. Establezca su valor en TRUE. No agregue Hola por encima de valores junto con comillas dobles.

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a>Descargar e instalar paquetes adicionales de Hola
Nota: Asegúrese de que sistema hello tiene conectividad a internet antes de descargar e instalar paquetes adicionales de Hola.

\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools

Este comando descarga estos 15 paquetes desde el repositorio de CentOS 6.6 y los instala:

bc-1.06.95-1.el6.x86\_64.rpm

busybox-1.15.1-20.el6.x86\_64.rpm

elfutils-libs-0.158-3.2.el6.x86\_64.rpm

kexec-tools-2.0.0-280.el6.x86\_64.rpm

lsscsi-0.23-2.el6.x86\_64.rpm

lzo-2.03-3.1.el6\_5.1.x86\_64.rpm

perl-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm

perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm

perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm

perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-version-0.77-136.el6\_6.1.x86\_64.rpm

rsync-3.0.6-12.el6.x86\_64.rpm

snappy-1.1.0-1.el6.x86\_64.rpm

wget-1.12-5.el6\_6.1.x86\_64.rpm

Si la máquina de origen Hola usa filesystem Reiser o XFS para dispositivo de arranque o raíz de Hola, a continuación, paquetes siguientes deben ser descargados e instalados en tooprotection anterior de destino maestro de Linux.

\# cd /usr/local

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm

\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm

#### <a name="apply-custom-configuration-changes"></a>Aplicación de cambios en la configuración personalizada
Antes de aplicar estos cambios Asegúrese de que se haya completado la sección anterior de hello, a continuación, siga estos pasos:

1. Copie Hola RHEL 6-64 unificado agente toohello binario creado recientemente el sistema operativo.
2. Ejecute este comando toountar hello binario: **tar - zxvf \<nombre de archivo\>**
3. Ejecutar permisos de toogive este comando: \# **./ApplyCustomChanges.sh chmod 755**
4. Ejecutar script de Hola:  **\# ./ApplyCustomChanges.sh**. Ejecutar script de Hola solo una vez en el servidor de Hola. Reinicie el servidor de hello después de ejecutar script de Hola.

### <a name="install-hello-linux-server"></a>Instalar el servidor Linux de Hola
1. [Descargar](http://go.microsoft.com/fwlink/?LinkID=529757) archivo de instalación de hello.
2. Copie Hola archivo toohello máquina virtual de destino maestro de Linux con una utilidad de cliente de sftp de su elección. Como alternativa puede iniciar sesión en la máquina de destino maestro de Linux de Hola y usar el paquete de instalación de wget toodownload Hola desde el vínculo proporcionado
3. Inicie sesión en hello Linux destino maestro servidor máquina virtual mediante un ssh cliente de su elección
4. Si está conectado toohello Azure red en el que se implementa el servidor de destino maestro de Linux a través de una conexión VPN, a continuación, utiliza la dirección IP interna para servidor de Hola que encontrará en la máquina virtual **panel** ficha y puerto 22 tooconnect toohello Linux master de destino mediante el Shell de proteger el servidor.
5. Si se está conectando toohello servidor de destino maestro de Linux a través de una conexión a internet pública usar dirección IP virtual pública del servidor de destino maestro de Linux hello (desde máquinas virtuales de hello **panel** ficha) y Hola extremo público crear para ssh toologin toohello Linux servder.
6. Extraiga los archivos de hello del archivo de instalador de servidor de destino maestro tar de hello comprimido con gzip Linux ejecutando: *"tar – xvzf Microsoft ASR\_UA\_8.2.0.0\_RHEL6-64"* del directorio de Hola que contiene el archivo de instalador de hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. Si se cambia, Hola extraídos instalador archivos tooa otro directorio se extrajeron los contenidos del toohello directorio toowhich Hola Hola tar archivo. En la ruta de acceso al directorio, ejecute "sudo ./install.sh"

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. Cuando se selecciona solicitada toochoose un rol principal **2 (destino maestro)**. Deje Hola otras opciones de instalación interactiva en sus valores predeterminados.
9. Espere a que instalación hello y toocontinue tooappear de interfaz de configuración de Host. Hola utilidad de configuración del Host de destino maestro de Linux de hello Server es una utilidad de línea de comandos. No cambiar el tamaño de hello ssh ventana de la utilidad de cliente. Use Hola flecha claves tooselect Hola **Global** opción y presione ENTRAR en el teclado.

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. En el campo de hello **IP** escriba la dirección IP interna de Hola Hola del servidor de configuración (puede encontrarla en hello **panel** ficha de la máquina virtual del servidor de configuración de hello) y presione ENTRAR. En el campo **Puerto**, escriba **22** y presione Entrar.
11. En **Usar HTTPS** deje la opción **Sí** y presione Entrar.
12. Escriba la frase de contraseña que se generó en el servidor de configuración de Hola Hola. Si usa a un cliente PUTTY desde una máquina virtual de Windows máquina toossh toohello Linux puede usar contenido de hello MAYÚS+INS toopaste de Portapapeles Hola. Copiar Portapapeles local Hola frase de contraseña toohello mediante Ctrl-C y usar MAYÚS+INS toopaste lo. Presione Entrar.
13. Use Hola flecha derecha toonavigate clave tooquit y presione ENTRAR. Espere a que toocomplete de instalación.

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

Si por algún motivo no se pudo tooregister el servidor de configuración Linux toohello de servidor de destino maestro para hacer de nuevo, ejecuta el host de utilidad de configuración de /usr/local/ASR/Vx/bin/hostconfigcli (en primer lugar deberá toothis de permisos de acceso de tooset directorio ejecutando chmod como un superusuario).

#### <a name="validate-master-target-registration"></a>Validación del registro de destino maestro
Puede validar ese Hola servidor de destino maestro se registró correctamente toohello el servidor de configuración en el almacén de Azure Site Recovery > **servidor de configuración** > **detalles del servidor**.

> [!NOTE]
> Después de registrar el servidor de destino maestro de hello, si recibe errores de configuración que Hola máquina virtual puede haber eliminado de Azure o no se han configurado correctamente los puntos de conexión, esto es porque aunque hello se detectó una configuración de destino maestro por hello Azure dndpoints al destino maestro Hola se implementa en Azure, esto no es cierto para un local destino maestro servidor local. Esto no afectará a la conmutación por recuperación y puede ignorar dichos errores.
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a>Paso 4: Proteger el sitio local de hello máquinas virtuales toohello
Necesita al sitio local toohello tooprotect máquinas virtuales antes de realizar conmutación por.

### <a name="before-you-begin"></a>Antes de empezar
Cuando una máquina virtual se conmuta tooAzure, agrega una unidad temporal adicional para el archivo de paginación. La máquina virtual que se ha conmutado por error no suele requerir dicha unidad, ya que es posible que disponga de una unidad dedicada al archivo de paginación. Antes de comenzar inversa protección de máquinas virtuales de hello, debe asegurarse de que esta unidad se queda sin conexión para que no se protegen. Para ello, realice lo siguiente:

1. Abra Administración de equipos y seleccione Administración de almacenamiento, por lo que hace una lista de máquina de hello discos toohello en línea y conectado.
2. Seleccione Hola temporal en el disco adjunto toohello máquina y elija toobring en modo sin conexión.

### <a name="protect-hello-vms"></a>Proteger las máquinas virtuales de Hola
1. Hola portal de Azure, comprobar estados de Hola de hello tooensure de máquina virtual que está conmutación por error.

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. Inicie vContinuum en el equipo

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. Haga clic en **nuevo grupo de protección** y seleccione el tipo de sistema de operación de hello, el
4. En ventana nueva hello que abra Hola seleccione **tipo de SO** > **obtener los detalles de** para hello las máquinas virtuales que desee toofail atrás. En **detalles del servidor principal**, identificar y seleccione Hola máquinas virtuales que desea tooprotect. Máquinas virtuales aparecen en el nombre de host de vCenter Hola que se encontraban en antes de la conmutación por error.
5. Si se selecciona un tooprotect de máquina virtual (y ya haya conmutado tooAzure) una ventana emergente proporciona dos entradas para la máquina virtual de Hola. Esto es porque el servidor de configuración de hello detecta dos instancias de hello máquinas virtuales registradas tooit. Necesita tooremove Hola entrada para hello en servidor local de VM para que pueda proteger Hola máquina virtual correcta. tooidentify hello Azure VM entrada correcta aquí, puede iniciar sesión en hello VM de Azure y vaya tooC:\Program archivos (x86) \Microsoft Azure Site Recovery\Application Data\etc. Hola archivo drscout.conf, identificar Hola identificador de host. En el cuadro de diálogo de hello vContinuum, mantenga hello para el que se ha encontrado una entrada Id. de host de Hola en hello máquina virtual. Elimine las restantes entradas. Hola tooselect corregir VM puede hacer referencia a dirección IP de tooits. Hola IP dirección intervalo local se puede Hola VM local.

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. En servidor de vCenter Hola detener la máquina virtual de Hola. También puede eliminar las máquinas virtuales de hello en local.
7. A continuación, especifique Hola local MT server toowhich desea tooprotect hello las máquinas virtuales. toodo, conectar toohello vCenter server toowhich desea toofail atrás.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. Servidor de destino maestro Hola seleccione según Hola host toowhich desea toorecover Hola máquina virtual.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. Proporciona la opción de replicación de Hola para cada una de las máquinas virtuales Hola. toodo esto necesita tooselect Hola recuperación lado datastore toowhich Hola se recuperarán las máquinas virtuales. tabla de Hello resume opciones diferentes de hello necesita tooprovide para cada máquina virtual.

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | **Opción** | **Valor recomendado de la opción** |
   | --- | --- |
   |  Process server IP address (Dirección IP del servidor de procesos) |Seleccionar servidor de procesos de hello implementado en Azure |
   |  Retention size in MB (Tamaño de retención en MB) | |
   |  Retention value (Valor de retención) |1 |
   |  Days/Hours (Días y horas) |Days (Días) |
   |  Consistency Interval (Intervalo de consistencia) |1 |
   |  Select target Datastore (Seleccionar almacén de datos de destino) |Hola almacén de datos disponible en el sitio de recuperación de Hola. almacén de datos de Hello debe tener suficiente espacio y ser host ESX toohello disponible en el que desea toorestore Hola virtual machine. |
10. Configurar Hola adquirirán propiedades que Hola máquina virtual después de sitio de tooon local de conmutación por error. propiedades de Hola se resumen en hello en la tabla siguiente.

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | **Propiedad** | **Detalles** |
    | --- | --- |
    | Network configuration (Configuración de red) |Para cada adaptador de red detectado, selecciónelo y haga clic en **cambio** dirección IP de conmutación por recuperación tooconfigure hello para la máquina virtual de Hola. |
    | Hardware Configuration (Configuración de hardware) |Especifique Hola CPU y memoria de Hola para hello máquina virtual. Configuración puede ser aplicada tooall hello las máquinas virtuales que está tratando de tooprotect. tooidentify Hola valores correctos hello CPU y memoria, puede hacer referencia toohello tamaño de rol de VM de IAAS y ver Hola número de núcleos y memoria asignada. |
    | Nombre para mostrar |Después de la conmutación por recuperación tooon local, puede cambiar el nombre hello las máquinas virtuales tal y como aparecerán en el inventario de vCenter Hola. Hola predeterminado es nombre de host de equipo de máquina virtual de Hola. nombre de máquina virtual de hello tooidentify, puede hacer referencia toohello lista de máquinas virtuales en el grupo de protección de Hola. |
    | NAT Configuration (Configuración de NAT) |Se describe en detalle a continuación. |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a>Configuración de NAT
1. tooenable protección de máquinas virtuales de hello, dos canales de comunicación necesitan toobe establecido. primer canal de Hello es entre la máquina virtual de Hola y servidor de procesos de Hola. Este canal recopila datos de Hola de hello VM y lo envía el servidor de procesos de toohello que, a continuación, envía Hola servidor de destino maestro toohello de datos. Si el servidor de procesos de Hola y Hola toobe de máquina virtual protegida se encuentran en hello misma red virtual no deberá toouse una configuración de NAT. De lo contrario, especifique la configuración de NAT. Ver la dirección IP pública de Hola Hola del servidor de procesos en Azure.

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. segundo canal de Hello es entre el servidor de procesos de Hola y el servidor de destino maestro Hola. Hola toouse opción NAT o no depende de si está usando una conexión VPN basada o comunicarse a través de Hola internet. No seleccione NAT si utiliza VPN, solo si usa una conexión a Internet.

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. Si aún no lo ha eliminado máquinas de virtuales Hola local tal como se especifica y si el almacén de datos de hello es toostill atrás de errores contiene Hola antiguo VMDK, necesitará tooensure ese Hola de conmutación por recuperación máquina virtual se crea en un nuevo sitio. toodo este Hola seleccione **avanzadas** configuración y especifique una alternativa tooin toorestore de carpeta **configuración de nombre de carpeta**. Deje Hola otras opciones con su configuración predeterminada. Aplicar Hola carpeta nombre configuración tooall Hola servidores.

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. Ejecutar una comprobación de preparación tooensure que hello las máquinas virtuales son toobe listo protegido local tooon back.

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. Espere toocomplete. Si está correctamente en todas las máquinas virtuales puede especificar un nombre para el plan de protección de Hola. A continuación, haga clic en **proteger** toobegin.

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. El progreso se puede supervisar en vContinuum.

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. Después del paso de hello **activar el Plan de protección** finalice, puede supervisar la protección de máquina virtual en el portal de Site Recovery Hola.

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. Puede ver el estado exacto de hello al hacer clic en hello VM y supervisar su progreso.

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a>Preparar el plan de conmutación por recuperación de Hola
Puede preparar un plan de conmutación por recuperación mediante vContinuum para poder aplicación hello sitio local de toohello back-error en cualquier momento. Estos planes de recuperación son muy similares planes de recuperación de toohello en Site Recovery.

1. Inicie vContinuum y seleccione **Manage plans (Administrar planes)** > **Recover** (Recuperar). Puede ver de la lista de todos los planes de Hola que se han usado toofail a máquinas virtuales. Puede usar hello mismo planes toorecover.

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. Seleccione el plan de protección de Hola y todas hello las máquinas virtuales que desee toorecover en ella. Cuando se selecciona cada máquina virtual puede ver más detalles incluidos Hola destino ESX server y el disco de máquina virtual de origen Hola. Haga clic en **siguiente** toobegin Hola Asistente para recuperar y seleccione hello las máquinas virtuales que desee toorecover.

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. Puede recuperar en función de varias opciones, pero le recomendamos que use **etiqueta Latest** y seleccione **aplicar para todas las máquinas virtuales** tooensure que Hola datos más recientes de la máquina virtual de Hola se usará.
4. Ejecute hello **Comprobar preparación.** Comprueba si los parámetros correctos de hello están configurado tooenable de recuperación de máquina virtual. Haga clic en **siguiente** si todas las comprobaciones de hello son correctas. Si no se compruebe el registro de hello y resolver errores de Hola.

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. En **configuración de máquina virtual** Asegúrese de que la configuración de recuperación de Hola se establece correctamente. Puede cambiar la configuración de máquina virtual de hello si necesita.

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. Revise la lista de Hola de máquinas virtuales que se recuperarán y especificar un orden de recuperación. Tenga en cuenta que las máquinas virtuales se muestran utilizando el nombre de host del equipo de Hola. Puede que sea difícil toomap Hola equipo host nombre toohello virtual machine.
   nombres de hello toomap, las máquinas virtuales vaya toohello **panel** en Azure y comprobación de nombre de host de máquina virtual de Hola.

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. Especifique un nombre de plan y seleccione **Recover later**(Recuperar más adelante). Se recomienda toorecover más tarde porque la protección inicial Hola podría no estar completo.
8. Haga clic en **recuperar** toosave Hola plan o un desencadenador Hola recuperación si seleccionó toorecover ahora y no más tarde. Puede comprobar toosee de estado de recuperación de hello si ha guardado el plan de hello del.

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a>Recuperación de máquinas virtuales
Después de crear el plan de hello, puede recuperar las máquinas virtuales Hola. Antes de comprobar que Hola virtual máquinas han completado la sincronización. Si el estado de replicación es correcto, a continuación, se completa la protección de Hola y se ha alcanzado el umbral de RPO de Hola. Puede comprobar el estado en las propiedades de la máquina virtual de Hola.

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

Desactive la opción Hola máquinas virtuales de Azure antes de iniciar la recuperación de Hola. Esto garantiza que no hay ninguna división de cerebro y que los usuarios sólo tendrá acceso a una copia de la aplicación hello.

1. Iniciar Hola guardado plan. En vContinuum seleccione **Monitor** Hola planes. Esto muestra todos los planes de Hola que se han ejecutado.

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. Plan de SELECT hello en **recuperación** y haga clic en **iniciar**. Puede supervisar la recuperación. Después de han sido desactivadas máquinas virtuales en el puede conectarse toothem en vCenter.

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a>Proteger tooAzure nuevo tras la conmutación por recuperación
Una vez completada la conmutación por recuperación que probablemente deseará volver a máquinas virtuales de tooprotect Hola. Para ello, realice lo siguiente:

1. Compruebe que están trabajando Hola máquinas virtuales locales y que las aplicaciones sean accesibles.
2. En el portal de Azure Site Recovery hello, seleccione las máquinas virtuales hello y eliminarlos. Seleccione toodisable Hola protección de máquinas virtuales de Hola. Esto garantiza que no hay más están protegidas hello las máquinas virtuales.
3. En Azure elimine Hola conmutado por error máquinas virtuales de Azure
4. Eliminar Hola de máquina virtual anterior en vSpehere. Se trata de las máquinas virtuales de Hola que habían conmutado por error tooAzure.
5. En el portal de Site Recovery Hola proteger hello las máquinas virtuales que recientemente conmutación por error. Una vez que están protegidos puede agregarlos tooa plan de recuperación.

## <a name="next-steps"></a>Pasos siguientes
* [Obtenga información sobre](site-recovery-vmware-to-azure-classic.md) replicar máquinas virtuales de VMware y tooAzure servidores físicos mediante la implementación de hello mejorado.
