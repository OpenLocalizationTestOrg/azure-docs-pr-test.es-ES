---
title: "aaaAzure la solución de problemas de cifrado de disco | Documentos de Microsoft"
description: "En este artículo se ofrecen sugerencias para solucionar problemas de Microsoft Azure Disk Encryption para máquinas virtuales IaaS con Windows y Linux."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a>Guía de solución de problemas de Azure Disk Encryption

Esta guía está dirigida a profesionales de tecnologías de información, información los analistas de seguridad y problemas relacionados con los administradores de nube cuyas organizaciones usan el cifrado de disco de Azure y necesitan instrucciones tootroubleshoot cifrado de disco.

## <a name="troubleshooting-linux-os-disk-encryption"></a>Solución de problemas del cifrado de discos con el SO Linux

Cifrado del disco de sistema operativo Linux debe desmontar Hola SO unidad anterior toorunning a través del proceso de cifrado de disco completo Hola.   Si no es posible, un mensaje de error "no se pudo toounmount después..." mensaje de error es probable que toooccur.

Suele ocurrir cuando se intenta el cifrado del disco del sistema operativo en un entorno de máquina virtual de destino que se ha modificado o cambiado desde su imagen de la galería admitida.  Ejemplos de desviaciones de la imagen de hello admitida, lo que puede interferir con la unidad de la extensión de hello capacidad toounmount Hola OS:
- Imágenes personalizadas que ya no coinciden con un sistema de archivos o esquema de partición compatibles.
- Imágenes personalizadas con aplicaciones como antivirus, Docker, SAP, MongoDB o Casandra de Apache que se ejecutan en tooencryption anterior del sistema operativo de Hola.  Estas aplicaciones son difíciles de tooterminate y cuando mantienen unidad de toohello SO de identificadores de archivos abiertos, unidad de hello no se puede desmontar, provocando el error.
- Scripts personalizados que se ejecutan en cierran tiempo paso de cifrado de proximidad toohello puede interferir y hacer que este error. Esto puede ocurrir cuando una plantilla de administrador de recursos define varios tooexecute extensiones al mismo tiempo, o cuando una extensión de la secuencia de comandos personalizada o a otra acción se ejecuta simultáneamente toodisk cifrado.   Serialización y el aislamiento de estos pasos para resolver el problema de Hola.
- Cuando SELinux no se ha cifrado deshabilitado tooenabling anterior, Hola desmonte paso produce un error.  SELinux puede habilitarse de nuevo después de completarse el cifrado.
- Cuando el disco de SO de Hola usa un esquema de LVM (aunque hay compatibilidad limitada de disco de datos LVM, disco del sistema operativo LVM no es)
- Cuando no se cumplen los requisitos mínimos de memoria (se recomiendan 7GB para el cifrado del disco de sistema operativo)
- Cuando las unidades de datos se han montado recursivamente en el directorio /mnt/ o entre sí (por ejemplo, /mnt/datos1, /mnt/datos2, /datos3 + /datos3/datos4, etc.)
- Cuando no se cumplen otros [requisitos previos](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) de Azure Disk Encryption para Linux

## <a name="unable-tooencrypt"></a>No se puede tooencrypt

En algunos casos, cifrado de disco Linux Hola aparece toobe atascada en "Se inició el cifrado de disco de SO" y SSH está deshabilitada. Este proceso puede tardar entre toocomplete 3-16 horas en una imagen de la Galería estándar.  Si se agregan discos de datos de tamaño de múltiples TB, el proceso de hello puede tardar días. Hello secuencia de cifrado del disco de sistema operativo Linux desmonta la unidad de hello SO temporalmente y realiza el cifrado de bloque a bloque de disco del sistema operativo completo hello, antes de volver a montar en su estado cifrado.   A diferencia del cifrado de disco de Azure en Windows, Linux cifrado del disco no permite uso simultáneo de hello VM durante el cifrado de hello en curso.  características de rendimiento de Hola de hello máquina virtual, incluido el tamaño de Hola de disco de Hola y si cuenta de almacenamiento de hello está respaldado por el sistema de almacenamiento (SSD) standard o premium, pueden influir en gran medida Hola tiempo necesario toocomplete cifrado.

toocheck estado, los campos de ProgressMessage Hola devueltos desde hello [AzureRmVmDiskEncryptionStatus Get](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) puede sondearse comando.   Cuando se cifra la unidad de hello SO, Hola VM entra en estado de mantenimiento y SSH también es tooprevent deshabilitado ningún proceso continuo de toohello de interrupción.  EncryptionInProgress se mostrarán para la mayoría de hello del tiempo de Hola durante el cifrado en curso, seguido de más tarde varias horas con un mensaje de confirmación toorestart Hola VM del VMRestartPending.  Por ejemplo:


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

Una vez se le pida tooreboot Hola VM y, después de reiniciar Hola VM y conceder a 2 a 3 minutos para el reinicio de Hola y toobe pasos finales realizada en el destino de hello, mensaje de bienvenida de estado indicará que el cifrado finalmente ha completado.   Cuando este mensaje está disponible, unidad del SO Hola cifrada es esperado toobe listo para su uso y para hello toobe de máquina virtual puede usar de nuevo.

En casos donde no se ha visto esta secuencia, o si otros indicadores de error, mensaje de progreso o información de inicio de informe que no se ha cifrado del sistema operativo en medio de Hola de este proceso (por ejemplo, si ve el error de "error toounmount" hello descrito en esta guía), se recomienda instantánea toohello atrás de toorestore Hola VM o copia de seguridad realizada tooencryption inmediatamente anterior.  Toohello anterior siguiente intento, es toore sugerido: evaluar las características de Hola de hello VM y asegúrese de que se cumplen todos los requisitos previos.

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a>Solución de problemas de Azure Disk Encryption detrás de un firewall
Cuando conectividad está restringida por una capacidad Hola firewall, el requisito de proxy o la configuración de grupo (NSG) de seguridad de red, Hola extensión tooperform necesitan puede interrumpir las tareas.   Esto puede dar lugar a mensajes de estado como "Estado de extensión no está disponible en hello VM" y en los escenarios esperados por error toofinish.  secciones de Hola que van a continuación tiene algunos problemas comunes de firewall que puede investigar.

### <a name="network-security-groups"></a>Grupos de seguridad de red
Aplicada ninguna configuración de grupo de seguridad de red todavía debe permitir la configuración de red de hello documentado de hello extremo toomeet [requisitos previos](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) para el cifrado de disco.

### <a name="azure-keyvault-behind-firewall"></a>Azure Key Vault detrás del firewall
Hola VM debe ser capaz de tooaccess el almacén de claves. Consulte tooguidance en errores de acceso tookey detrás de un firewall que se mantiene por hello [el almacén de claves](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) equipo.

### <a name="linux-package-management-behind-firewall"></a>Administración de paquetes de Linux detrás del firewall
En tiempo de ejecución, cifrado de disco de Azure para Linux se basa en paquete administración tooinstall necesitado componentes de requisitos previos anteriores tooenabling el cifrado del sistema la distribución de destino de hello.  Si la configuración de firewall impiden Hola VM pueda toodownload e instala estos componentes, a continuación, se esperan que produzcan errores posteriores.    pasos de Hello tooconfigure que esto puede variar en función de distribución.  En Red Hat, cuando se requiere un proxy, es vital asegurarse de que el administrador de la suscripción y yum están configurados correctamente.  Consulte [este artículo](https://access.redhat.com/solutions/189533) de soporte técnico de Red Hat sobre este tema.  

## <a name="troubleshooting-windows-server-2016-server-core"></a>Solución de problemas de Windows Server 2016 Server Core

En Server Core de Windows Server 2016, componente de hello bdehdcfg no está disponible de forma predeterminada. y Azure Disk Encryption necesita dicho componente.

tooworkaround este problema, Hola copia siguientes 4 archivos de una carpeta de VM de centro de datos de Windows Server 2016 toohello c:\windows\system32 de imagen de Server Core de hello:

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

A continuación, ejecute el siguiente comando de hello:

```
bdehdcfg.exe -target default
```

Esto creará una partición de sistema de 550MB y, a continuación, tras un reinicio, puede usar Diskpart toocheck Hola volúmenes y continuar.  

Por ejemplo:

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a>Otras referencias
En este documento, ha aprendido más información acerca de algunos problemas comunes en el cifrado de disco de Azure y cómo tootroubleshoot. Para más información acerca de este servicio y su funcionalidad, lea:

- [Aplicación de cifrado de discos en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Cifrado de una máquina virtual de Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Cifrado en reposo de datos de Azure](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
