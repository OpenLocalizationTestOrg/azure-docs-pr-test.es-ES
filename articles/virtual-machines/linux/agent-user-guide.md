---
title: "Introducción al agente de máquina virtual Linux aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall y configurar el agente de Linux (waagent) toomanage interacción de su máquina virtual con el controlador de tejido de Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>Comprender y usar Hola agente Linux de Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>Introducción
Agente de Linux Hello Microsoft Azure (waagent) administra Linux y FreeBSD aprovisionamiento y la interacción de VM con hello controlador de tejido de Azure. Proporciona Hola después funcionalidad para las implementaciones de Linux y FreeBSD IaaS:

> [!NOTE]
> Vea agente de Linux de Azure de hello [Léame](https://github.com/Azure/WALinuxAgent/blob/master/README.md) para obtener más detalles.
> 
> 

* **Aprovisionamiento de imágenes**
  
  * Creación de una cuenta de usuario
  * Configuración de los tipos de autenticación de SSH
  * Implementación de claves públicas y pares de claves de SSH
  * Nombre de host de Hola de configuración
  * Publicación Hola nombre toohello plataforma del host DNS
  * SSH host huella digital de clave toohello plataforma de informes
  * Administración del disco de recursos
  * Montar el disco del recurso de Hola y formato
  * Configuración del espacio de intercambio
* **Redes**
  
  * Administra las rutas tooimprove compatibilidad con los servidores DHCP de plataforma
  * Garantiza la estabilidad de Hola de nombre de interfaz de red de Hola
* **Kernel**
  
  * Configura NUMA virtual (deshabilitar para el kernel cuya versión es inferior a la versión 2.6.37)
  * Consume entropía de Hyper-V para /dev/random
  * Configura los tiempos de espera de SCSI para dispositivos de la raíz de hello (que pudieron ser remoto)
* **Diagnóstico**
  
  * Puerto serie de toohello de redirección de consola
* **Implementaciones de SCVMM**
  
  * Detecta y ejecuta un agente VMM de Hola para Linux Bootstrap cuando se ejecuta en un entorno de System Center Virtual Machine Manager 2012 R2
* **Extensión de máquina virtual**
  
  * Insertar componente creado por Microsoft y sus socios en la automatización de software y la configuración de tooenable de VM de Linux (IaaS)
  * Implementación de la referencia de la extensión de máquina virtual en [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>Comunicación
Hola el flujo de información desde el agente de hello plataforma toohello se produce a través de dos canales:

* Un DVD conectado de tiempo de arranque para las implementaciones de IaaS. Este DVD incluye un archivo de configuración compatible con OVF que incluye información de aprovisionamiento de todos los que no sea de pares de claves SSH real Hola.
* Un punto de conexión TCP que expone una API de REST usa tooobtain implementación y configuración de la topología.

## <a name="requirements"></a>Requisitos
Hello sistemas siguientes se han probado y se sabe toowork con hello agente Linux de Azure:

> [!NOTE]
> Esta lista puede diferir de la lista oficial de Hola de sistemas compatibles en hello plataforma de Microsoft Azure, como se describe aquí: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3+
* Red Hat Enterprise Linux 6.7+
* Debian 7.0+
* Ubuntu 12.04+
* openSUSE 12.3+
* SLES 11 SP3+
* Oracle Linux 6.4+

Otros sistemas compatibles:

* FreeBSD 10+ (Agente Linux de Azure v2.0.10+)

agente de Linux Hola depende algunos paquetes de sistema en orden toofunction correctamente:

* Python 2.6
* OpenSSL 1.0+
* OpenSSH 5.3+
* Utilidades del sistema de archivos: sfdisk, fdisk, mkfs, parted
* Herramientas de contraseña: chpasswd, sudo
* Herramientas de procesamiento de texto: sed, grep
* Herramientas de red: ip-route
* Compatibilidad de kernel para el montaje de sistemas de archivos UDF.

## <a name="installation"></a>Instalación
Instalación mediante un RPM o un paquete DEB desde el repositorio de paquetes de la distribución es método hello preferido de la instalación y la actualización Hola agente Linux de Azure. Hola todos los [están aprobados proveedores de distribución](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrar paquetes de agente de Linux de Azure de Hola a sus imágenes y repositorios.

Consulte la documentación del toohello Hola [repositorio de agente Linux de Azure en GitHub](https://github.com/Azure/WALinuxAgent) para opciones de instalación avanzada, como la instalación desde ubicaciones de origen o toocustom o prefijos.

## <a name="command-line-options"></a>Opciones de la línea de comandos
### <a name="flags"></a>Marcas
* verbose: Aumenta el nivel de detalle de un comando específico
* force: Omite la confirmación interactiva de algunos comandos

### <a name="commands"></a>Comandos:
* Ayuda: enumera los comandos de hello compatible y marcas.
* Desaprovisionamiento: intento de sistema de hello tooclean y que sea adecuado para volver a aprovisionar. Esta operación elimina siguiente hello:
  
  * Todas las claves de host SSH (si Provisioning.RegenerateSshHostKeyPair es 'y' en el archivo de configuración de hello)
  * Configuración de Nameserver en /etc/resolv.conf
  * Contraseña de la raíz de/etc/shadow (si Provisioning.DeleteRootPassword es 'y' en el archivo de configuración de hello)
  * Concesiones del cliente de DHCP en caché
  * Restablece toolocalhost.localdomain de nombre de host

> [!WARNING]
> Desaprovisionamiento no garantiza que esa imagen Hola haya borrado de toda la información confidencial y adecuado para su redistribución.
> 
> 

* Desaprovisionamiento + user: realiza todo bajo - deprovision (arriba) y también elimina la última cuenta de usuario aprovisionado hello (obtenido de /var/lib/waagent) y los datos asociados. Este parámetro está presente cuando se desaprovisiona una imagen que se estaba aprovisionando anteriormente en Azure de modo que se pueda capturar y volver a usar.
* versión: muestra la versión de Hola de waagent
* serialconsole: configura GRUB toomark ttyS0 (Hola primer puerto serie) como consola de arranque de Hola. Esto garantiza que los registros de arranque de kernel se envía toothe de puerto serie y están disponibles para la depuración.
* demonio: ejecutado waagent como una interacción de toomanage daemon con la plataforma de Hola. Este argumento es toowaagent especificado en la secuencia de comandos de hello waagent init.
* start: Ejecución de waagent como proceso en segundo plano

## <a name="configuration"></a>Configuración
Un archivo de configuración (/ etc/waagent.conf) controles Hola acciones de waagent. Abajo se muestra un archivo de configuración de ejemplo:

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

Hola que distintas opciones de configuración se describen en detalle a continuación. Las opciones de configuración son de tres tipos: Boolean, String o Integer. Opciones de configuración booleano de Hello pueden especificarse como "y" o "n". Hola palabra clave especial "" puede utilizarse para algunas entradas de configuración de tipo de cadena como se detalla a continuación.

**Provisioning.Enabled:**  
Tipo: Boolean  
Predeterminado: y

Esto permite tooenable de usuario de Hola o deshabilitar Hola aprovisionamiento funcionalidad en el agente de Hola. Los valores válidos son "y" o "n". Si se deshabilita el aprovisionamiento, se conservan las claves de host y usuario SSH de imagen de Hola y se omite cualquier configuración especificada en hello API de aprovisionamiento de Azure.

> [!NOTE]
> Hola `Provisioning.Enabled` demasiado "n" en las imágenes de nube de Ubuntu que utilizar init en la nube para el aprovisionamiento de valores predeterminados de parámetros.
> 
> 

**Provisioning.DeleteRootPassword:**  
Tipo: Boolean  
Predeterminado: n

Si se borra el conjunto, la contraseña de la raíz de hello en el archivo de instantáneas de hello/etcetera/durante Hola proceso de aprovisionamiento.

**Provisioning.RegenerateSshHostKeyPair:**  
Tipo: Boolean  
Predeterminado: y

Si se elimina el conjunto de todos los host pares de clave SSH (ecdsa, dsa y rsa) durante el proceso de/etc/ssh/de aprovisionamiento de Hola. Además, se genera un solo par de clave nuevo.

tipo de cifrado de Hola de par de claves nuevo hello es configurable por hello Provisioning.SshHostKeyPairType entrada. Tenga en cuenta que algunas distribuciones volverá a crear pares de claves de SSH para cualquier tipo de cifrado que falta cuando se reinicie el demonio de SSH de hello (por ejemplo, después de reiniciar el equipo).

**Provisioning.SshHostKeyPairType:**  
Tipo: String  
Predeterminado: rsa

Se puede establecer tipo de algoritmo de cifrado tooan que sea compatible con el demonio de SSH de hello en la máquina virtual de Hola. valores de Hello admitida generalmente son "rsa", "dsa" y "ecdsa". Tenga en cuenta que "putty.exe" en Windows no admite "ecdsa". Por lo tanto, si piensa toouse putty.exe Windows tooconnect tooa implementación de Linux, use "rsa" o "dsa".

**Provisioning.MonitorHostName:**  
Tipo: Boolean  
Predeterminado: y

Si establece, waagent supervisará máquina virtual de Linux Hola para cambios de nombre de host (como el devuelto por el comando de "nombre de host" hello) y actualizar automáticamente la configuración de red de hello en hello imagen tooreflect Hola de cambios. En nombre de criterio de hello toopush cambie toohello los servidores DNS, las redes se reiniciará en la máquina virtual de Hola. Esta acción tiene como resultado una breve pérdida de la conectividad con Internet.

**Provisioning.DecodeCustomData**  
Tipo: Boolean  
Predeterminado: n

Si se establece, waagent descodificará CustomData desde Base64.

**Provisioning.ExecuteCustomData**  
Tipo: Boolean  
Predeterminado: n

Si se establece, waagent ejecutará CustomData después del aprovisionamiento.

**Provisioning.PasswordCryptId**  
Tipo: String  
Valor predeterminado: 6

Algoritmo usado por el cifrado al generar el hash de contraseña.   
 1 - MD5  
 2a - Blowfish  
 5 - SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
Tipo: String  
Valor predeterminado: 10

Longitud del valor salt aleatorio usado al generar el hash de contraseña.

**ResourceDisk.Format:**  
Tipo: Boolean  
Predeterminado: y

Si establece, Hola recursos formatea el disco proporcionado por la plataforma de Hola se se y monta waagent si el tipo de sistema de archivos de hello solicitado por el usuario de hello en "ResourceDisk.Filesystem" es un valor distinto de "ntfs". Una sola partición de tipo Linux (83) estará disponible en disco de Hola. Tenga en cuenta que esta partición no se va a formatear si se puede montar correctamente.

**ResourceDisk.Filesystem:**  
Tipo: String  
Predeterminado: ext4

Esto especifica el tipo de sistema de archivos de Hola de disco del recurso de Hola. Los valores admitidos varían según la distribución de Linux. Si la cadena hello es X, a continuación, mkfs. X debe estar presente en la imagen de Linux Hola. Las imágenes de SLES 11 deben usar generalmente "ext3". Las imágenes de FreeBSD deben usar "ufs2".

**ResourceDisk.MountPoint:**  
Tipo: String  
Valor predeterminado: /mnt/resource 

Esto especifica la ruta de acceso de hello en el que está montado el disco del recurso de Hola. Tenga en cuenta ese disco del recurso de hello es un *temporal* en disco y puede ser vaciada cuando Hola VM es deprovisioned.

**ResourceDisk.MountOptions**  
Tipo: String  
Valor predeterminado: None

Especifica opciones de montaje disco toobe pasado toohello mount -o comando. Esta es una lista de valores separados por comas, por ejemplo, 'nodev,nosuid'. Consulte mount(8) para obtener detalles.

**ResourceDisk.EnableSwap:**  
Tipo: Boolean  
Predeterminado: n

Si establece un archivo de intercambio (/ swapfile) se crea en el disco del recurso de Hola y agrega el espacio de intercambio de sistema toohello.

**ResourceDisk.SwapSizeMB:**  
Tipo: Integer  
Valor predeterminado: 0

tamaño de Hola Hola del archivo de intercambio en megabytes.

**Logs.Verbose:**  
Tipo: Boolean  
Predeterminado: n

Si se establece, se aumenta el nivel de detalle del registro. Waagent registra too/var/log/waagent.log y aprovecha la funcionalidad toorotate registros de hello sistema logrotate.

**OS.EnableRDMA**  
Tipo: Boolean  
Predeterminado: n

Si se establece, el agente de Hola se intentarán tooinstall y, a continuación, cargar un controlador de kernel RDMA que coincide con la versión de Hola de firmware Hola Hola subyacente de hardware.

**OS.RootDeviceScsiTimeout:**  
Tipo: Integer  
Valor predeterminado: 300

Esto configura el tiempo de espera de hello SCSI en segundos en unidades de disco y los datos de hello SO. Si no se establece, se usan los valores predeterminados de sistema de Hola.

**OS.OpensslPath:**  
Tipo: String  
Valor predeterminado: None

Esto puede resultar toospecify usa una ruta de acceso alternativa para hello openssl binario toouse para operaciones criptográficas.

**HttpProxy.Host, HttpProxy.Port**  
Tipo: String  
Valor predeterminado: None

Si se establece, agente de hello utilizará este proxy server tooaccess Hola internet. 

## <a name="ubuntu-cloud-images"></a>Ubuntu Cloud Images
Tenga en cuenta que utilizar imágenes de nube Ubuntu [init de la nube](https://launchpad.net/ubuntu/+source/cloud-init) tooperform Hola de muchas tareas de configuración que en caso contrario, podrían ser administradas por agente Linux de Azure.  Tenga en cuenta Hola siguientes diferencias:

* **Provisioning.Enabled** demasiado "n" en las imágenes de nube de Ubuntu que usan tooperform init de la nube tareas de aprovisionamiento de los valores predeterminados.
* Hola parámetros de configuración siguientes no tiene ningún efecto en las imágenes de nube Ubuntu que usar en la nube init toomanage Hola recurso disco y espacio de intercambio:
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* Vea Hola después de punto de montaje de disco de recursos de recursos tooconfigure hello e intercambiar espacio en las imágenes de nube Ubuntu durante el aprovisionamiento:
  
  * [Ubuntu Wiki: Configure Swap Partitions (Configuración de particiones de intercambio)](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Inyección de datos personalizados en una máquina virtual de Azure](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

