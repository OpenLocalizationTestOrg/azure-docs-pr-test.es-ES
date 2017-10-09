---
title: "nombres de dispositivos de máquina virtual de aaaLinux se cambian en Azure | Documentos de Microsoft"
description: "Explica Hola ¿por qué se cambian los nombres de los dispositivos y proporcionan soluciones para este problema."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Solución de problemas: Se cambian los nombres de dispositivo de máquina virtual de Linux

Hola, se explica por qué se cambian los nombres de los dispositivos después de reiniciar una máquina virtual (VM) de Linux o volver a adjuntar discos Hola. También proporciona soluciones de Hola para este problema.

## <a name="symptom"></a>Síntoma

Puede experimentar Hola los siguientes problemas al ejecutar máquinas virtuales de Linux en Microsoft Azure.

- Hola VM produce un error tooboot después del reinicio.

- Si los discos de datos se separa y volver a adjuntar, los nombres de dispositivos de Hola para discos cambian.

- Se produce un error en una aplicación o un script que hace referencia a un disco con el nombre de dispositivo. Buscar ese Hola se cambia el nombre de dispositivo de disco de Hola.

## <a name="cause"></a>Causa

Rutas de acceso de dispositivo en Linux no se garantiza sean toobe coherente entre los distintos reinicios. Los nombres de dispositivo constan de números principales (letras) y secundarios.  Cuando el controlador de dispositivo de almacenamiento de hello Linux detecta un nuevo dispositivo, asigna tooit de números de dispositivo principal y secundaria de intervalo disponible Hola. Cuando se quita un dispositivo, los números de dispositivo de hello son liberado toobe volver a usar más adelante.

Hello problema se produce porque hello análisis en Linux programada por el subsistema de SCSI de hello de dispositivo realiza de forma asincrónica. nombres de ruta de acceso de dispositivo final Hola pueden variar entre los distintos reinicios. 

## <a name="solution"></a>Solución

tooresolve este problema, utilice nombres persistente. Hay cuatro toopersistent métodos nomenclatura - etiqueta de filesystem, uuid, por Id. y ruta de acceso. Se recomienda etiqueta del sistema de archivos de Hola y métodos UUID para máquinas virtuales de Linux de Azure. 

Cualquier hello también proporciona la mayoría de las distribuciones **nofail** o **nobootwait** fstab opciones. Estas opciones permiten un tooboot sistema aunque hello tiene un error toomount durante el inicio. Consulte la documentación de la distribución de Hola para obtener más información acerca de estos parámetros. Para obtener más información acerca de cómo tooconfigure un toouse de VM de Linux un UUID cuando se agrega un disco de datos, vea [conectar toohello nuevo disco de VM de Linux toomount hello](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

Cuando se instala el agente de Linux de Azure de hello en una máquina virtual, usa Udev reglas tooconstruct un conjunto de vínculos simbólicos en **/dev/disk/azure**. Estas reglas de Udev pueden ser utilizadas por aplicaciones y discos de tooidentify de secuencias de comandos están conectado toohello máquina virtual, su tipo y Hola LUN.

## <a name="more-information"></a>Más información

### <a name="identify-disk-luns"></a>Identificar LUN de disco

Una aplicación puede utilizar LUN toofind todos los discos de hello adjuntada y construir los vínculos simbólicos. agente de Linux de Azure de Hola ahora incluye reglas de udev que configure los vínculos simbólicos de un dispositivo de toohello LUN, como sigue:

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

También se puede recuperar la información de LUN de invitado de Linux de hello con lsscsi o una herramienta similar como se indica a continuación.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Esta información de LUN de invitado puede utilizarse con suscripción de Azure tooidentify Hola ubicación de los metadatos en el almacenamiento de Azure de disco duro virtual que almacena los datos de la partición de Hola Hola. Por ejemplo, use Hola az cli:

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a>Detectar UUID del sistema de archivos mediante blkid

Un script o una aplicación puede leer la salida de hello de blkid o fuentes de información similares y crear vínculos simbólicos en **/dev** para su uso. salida de Hello mostrará Hola UUID de todos los discos conectados toohello hello y VM dispositivo archivo toowhich están asociados:

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

reglas de udev de Hello waagent construcción un conjunto de vínculos simbólicos en **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


aplicación Hello puede utilizar esta información identificar el dispositivo de disco de arranque de Hola y el disco de recursos (efímero) Hola. En Azure, las aplicaciones deben hacer referencia demasiado**/dev/disk/azure/root-part1** o **/dev/disk/azure-resource-part1** toodiscover estas particiones.

Si hay particiones adicionales desde la lista de blkid hello, residen en un disco de datos. Las aplicaciones puedan mantener Hola UUID para estas particiones y usar una ruta de acceso como Hola por debajo del nombre de dispositivo de hello toodiscover en tiempo de ejecución:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>Obtener reglas de almacenamiento de Azure más recientes de Hola

reglas de almacenamiento de Azure más recientes de toohello, ejecute los siguientes comandos:

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Para obtener más información, vea Hola siguientes artículos:

- [Ubuntu: Using UUID](https://help.ubuntu.com/community/UsingUUID) (Ubuntu: Uso de UUID)

- [Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html) (Red Hat: Nomenclatura persistente)

- [Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you) (Linux: ¿Qué pueden hacer los UUID por usted?)

- [UDev: Introducción tooDevice administración en el sistema Linux moderna](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

