---
title: "Azure Backup: Recuperación de archivos y carpetas desde una copia de seguridad de máquina virtual de Azure | Microsoft Docs"
description: "Recuperación de archivos desde un punto de recuperación de máquina virtual de Azure"
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: "recuperación de elementos; recuperación de archivos desde una copia de seguridad de máquina virtual de Azure; restauración de archivos de máquina virtual de Azure"
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>Recuperación de archivos desde una copia de seguridad de máquina virtual de Azure

Copia de seguridad de Azure proporciona Hola capacidad toorestore [máquinas virtuales de Azure y los discos](./backup-azure-arm-restore-vms.md) desde las copias de seguridad de la máquina virtual de Azure. En este artículo explicaremos cómo recuperar elementos como archivos y carpetas desde una copia de seguridad de máquina virtual de Azure.

> [!Note]
> Esta característica está disponible para máquinas virtuales de Azure que se implementan utilizando el modelo de administrador de recursos de Hola y protegido tooa almacén de servicios de recuperación.
> No se pueden recuperar archivos a partir de una copia de seguridad de máquina virtual cifrada.
>

## <a name="mount-hello-volume-and-copy-files"></a>Montar Hola volumen y copiar archivos

1. Inicio de sesión en hello [portal de Azure](http://portal.Azure.com). Busque almacén de servicios de recuperación relevante de Hola y elemento de copia de seguridad de hello necesario.

2. En la hoja de elemento de la copia de seguridad de hello, haga clic en **recuperación de archivos**

    ![Apertura del elemento de copia de seguridad del almacén de Recovery Services](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    Hola **recuperación de archivos** abre la hoja.

    ![Hoja Recuperación de archivos](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. De hello **Seleccionar punto de recuperación** menú desplegable, el punto de recuperación de hello select que contiene archivos de Hola que desee. De forma predeterminada, ya está seleccionado el punto de recuperación más reciente de Hola.

4. Haga clic en **descargar ejecutable** (para Windows Azure VM) o **descargar Script** (para Linux VM de Azure) software de hello toodownload que podrá usar toocopy archivos de punto de recuperación de Hola.

  archivo ejecutable o script Hello crea una conexión entre el equipo local de Hola y Hola especificado punto de recuperación.

5. Necesita un contraseña toorun Hola descargado script o ejecutable. Puede copiar contraseña Hola Hola portal de usando botón Copiar de hello al lado de la contraseña de hello generado

    ![Contraseña generada](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. En el equipo de Hola donde desea toorecover Hola archivos, ejecute hello ejecutable o script. La ejecución debe realizarla con credenciales de administrador. Si ejecuta el script de Hola en un equipo con acceso restringido, asegúrese de que no hay acceso a:

    - download.Microsoft.com
    - Puntos de conexión de Azure usados para copias de seguridad de máquina virtual de Azure
    - Puerto de salida 3260

   Para Linux, el script de Hola requiere componentes 'open-iscsi' y 'lshw' punto de recuperación de tooconnect toohello. Si los que no existen en la máquina de hello en el que se ejecuta, pide componentes relevantes de permiso tooinstall hello y los instala tras el consentimiento.
   
   Escriba la contraseña de hello copiado desde el portal de hello cuando se le solicite. Una vez que se escribe la contraseña válida Hola scripts Hola conecta toohello punto de recuperación.
      
    ![Hoja Recuperación de archivos](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   Puede ejecutar script de Hola en cualquier equipo que tenga el sistema operativo de hello mismo (o compatibles) como Hola copia de seguridad virtual. Vea hello [tabla de sistema operativo Compatible](backup-azure-restore-files-from-vm.md#compatible-os) para sistemas operativos compatibles. Si Hola protegida virtual de Azure usa máquina en que espacios de almacenamiento de Windows (para las máquinas virtuales de Windows Azure) o Arrays(for Linux VMs) LVM/RAID, que no se puede ejecutar Hola ejecutable o script Hola misma máquina virtual. En su lugar, ejecútelo en otra máquina que tenga un sistema operativo compatible.

### <a name="compatible-os"></a>Sistemas operativos compatibles

#### <a name="for-windows"></a>Para Windows

Hola la siguiente tabla muestra hello compatibilidad entre los sistemas operativos de servidor y el equipo. Al recuperar archivos, no podrá restaurar archivos entre sistemas operativos incompatibles.

|Sistema operativo de servidor | Sistema operativo de cliente compatible  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | Windows 7   |

#### <a name="for-linux"></a>Para Linux

En Linux, requisito fundamental de Hola es ese sistema operativo Hola de máquina de Hola donde se ejecuta el script de Hola debe admitir Hola filesystem de hello archivos presentes en hello seguridad VM de Linux. Al seleccionar una secuencia de comandos de máquina toorun hello, asegúrese de que tiene las versiones compatibles de sistema operativo y Hola Hola como se mencionó en la siguiente tabla se Hola.

|SO Linux | Versiones  |
| --------------- | ---- |
| Ubuntu | 12.04 y posterior |
| CentOS | 6.5 y posterior  |
| RHEL | 6.7 y posterior |
| Debian | 7 y posterior |
| Oracle Linux | 6.4 y posterior |

script de Hola también requiere python y bash tooexecute de componentes y conectarse de forma segura toohello punto de recuperación.

|Componente | Versión  |
| --------------- | ---- |
| Bash | 4 y posterior |
| Python | 2.6.6 y posterior  |


### <a name="identifying-volumes"></a>Identificación de volúmenes

#### <a name="for-windows"></a>Para Windows

Al ejecutar el ejecutable de hello, sistema operativo de hello monta nuevos volúmenes de Hola y asigna letras de unidad. Puede usar el Explorador de Windows o el Explorador de archivos toobrowse esas unidades. Hello letras de unidad asignadas toohello volúmenes pueden no ser Hola se conservan mismas letras hello máquina virtual original, sin embargo, Hola nombre del volumen. Por ejemplo, si hello volumen en la máquina virtual original de hello fue "disco de datos (E:\)", que el volumen puede estar conectado como "disco de datos ('Cualquier letra de unidad disponible':\) en el equipo local de Hola. Buscar en todos los volúmenes que se mencionó en la salida del script de Hola hasta que encuentre la carpeta de archivos.  
       
   ![Hoja Recuperación de archivos](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>Para Linux

En Linux, volúmenes de Hola Hola del punto de recuperación son carpeta montada toohello donde se ejecuta el script de Hola. Hola adjunta discos, volúmenes y montaje correspondiente hello las rutas de acceso se muestran en consecuencia. Estas rutas de acceso de montaje son toousers visible que tengan acceso de nivel de raíz. Buscar en los volúmenes de hello mencionados en la salida del script de Hola.

  ![Hoja de recuperación de archivos de Linux](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a>Cerrar conexión Hola

Después de identificar los archivos de Hola y copiarlos tooa ubicación de almacenamiento local, quite (o desmontar) unidades adicionales de Hola. toounmount Hola unidades, hello **recuperación de archivos** hoja Hola portal de Azure, haga clic en **desmontar discos**.

![Desmontar discos](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

Una vez que los discos de hello están desmontados, recibirá un mensaje que le informará de que se realizó correctamente. Puede tardar unos minutos para hello toorefresh de conexión para que pueda quitar discos de Hola.

En Linux, después de que se rompe el punto de recuperación de hello conexión toohello, Hola SO no quita rutas de acceso de montaje correspondiente Hola automáticamente. Éstos existen como volúmenes "huérfanas" y están visibles, pero producen un error cuando se archivos Hola de acceso/escritura. Se pueden quitar manualmente. script de Hola, cuando se ejecuta, identifica este tipo de los volúmenes existentes de puntos de recuperación anterior y limpia tras el consentimiento.

## <a name="special-configurations"></a>Configuraciones especiales

### <a name="dynamic-disks"></a>Discos dinámicos

Si Hola VM de Azure que se copió tiene volúmenes que abarquen varios discos (volúmenes distribuidos y seccionados) y volúmenes tolerantes a errores (volúmenes reflejados y RAID-5) en discos dinámicos, no se puede ejecutar secuencias de comandos ejecutables hello Hola misma máquina virtual. En su lugar, ejecutar secuencias de comandos ejecutables hello en cualquier otra máquina con un sistema operativo compatible.

### <a name="windows-storage-spaces"></a>Espacios de almacenamiento de Windows

Espacios de almacenamiento de Windows es una tecnología de almacenamiento de Windows que permite el almacenamiento de toovirtualize. Con espacios de almacenamiento de Windows puede agrupar discos estándar del sector en grupos de almacenamiento y, a continuación, crear discos virtuales, denominados espacios de almacenamiento, de espacio disponible de hello en los grupos de almacenamiento.

Si Hola VM de Azure que se copió usa espacios de almacenamiento de Windows, no se puede ejecutar secuencias de comandos ejecutables hello Hola misma máquina virtual. En su lugar, ejecutar secuencias de comandos ejecutables hello en cualquier otra máquina con un sistema operativo compatible.

### <a name="lvmraid-arrays"></a>Matrices LVM/RAID

En Linux, el Administrador de volúmenes lógicos (LVM) o software matrices RAID son volúmenes lógicos toomanage usado por varios discos. Si Hola copia la VM de Linux utiliza LVM o matrices RAID, no se puede ejecutar el script de Hola en hello misma máquina virtual. En su lugar, ejecute el script de Hola en cualquier otra máquina con sistemas operativos compatibles y que admite el sistema de archivos de copia de seguridad de la máquina virtual de hello.

salida del script de Hola muestra hello LVM o discos de matrices RAID y volúmenes de hello con el tipo de partición de hello tal y como se muestra a continuación

   ![Hoja de salida de LVM en Linux](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
Hola después comandos necesita toobe ejecutar Hola usuario toobring estas particiones en línea. 

**Para las particiones de LVM**

```
$ pvs <volume name as shown above in hello script output> 
```
Esta acción muestra nombres de grupo de volúmenes de hello en un volumen físico.

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
Muestra todos los volúmenes lógicos, los nombres y sus rutas de acceso en un grupo de volúmenes.

```
$ mount <LV path> </mountpath>
```
toomount Hola volúmenes lógicos toohello ruta de acceso de su elección.


**Para las matrices RAID**

```
$ mdadm –detail –scan
```
Muestra los detalles sobre todos los discos RAID. disco RAID relevante de Hola se mostrará como`/dev/mdm/<RAID array name in hello backed up VM>`

Use el comando de montaje de hello si disco RAID de hello tiene volúmenes físicos.
```
$ mount [RAID Disk Path] [/mounthpath]
```

Si este disco RAID tiene otro LVM realizada en dicho luego seguir Hola mismo procedimiento descritas anteriormente para las particiones LVM con nombre de volumen de hello es nombre de disco RAID Hola

## <a name="troubleshooting"></a>Solución de problemas

Si tiene problemas durante la recuperación de archivos de máquinas virtuales de hello, compruebe Hola para obtener información adicional en la tabla siguiente.

| Mensaje de error y escenario | Causa probable | Acción recomendada |
| ------------------------ | -------------- | ------------------ |
| Salida de archivo exe: *excepción conectarse toohello destino* |Secuencia de comandos no es tooaccess capaz de punto de recuperación de Hola | Compruebe si máquina Hola cumple los requisitos de acceso de hello mencionados anteriormente|  
|   Salida de archivo exe: *destino Hola ya se haya registrado en a través de una sesión ISCSI.* |   ya se ejecutó el script de Hola en hello mismas unidades hello y máquina se han adjuntado |   ya se han adjuntado volúmenes Hola Hola del punto de recuperación. NO se puede montar con hello mismo letras de unidad Hola VM original. Examine todos los volúmenes disponibles Hola Hola Explorador de archivos para el archivo |
| Salida de archivo exe: *esta secuencia de comandos no es válido porque desmontar discos Hola a través del límite de portal/superado Hola de 12-hr. Descargue una nueva secuencia de comandos desde el portal de Hola.* |    desmontar discos Hola desde portal de Hola o ha superado el límite de 12-hr Hola |  Este archivo ejecutable ahora no es válido y no se puede ejecutar. Si desea tooaccess Hola archivos de esa recuperación punto-in-time, visite el portal de Hola para un nuevo archivo ejecutable|
| En la máquina de Hola donde se ejecuta Hola exe: no se desmontan nuevos volúmenes de hello después de que se hace clic en el botón de desmontaje de Hola |    iniciador ISCSI de Hello en la máquina de hello no responde/actualizar su destino de toohello la conexión y mantener la memoria caché de Hola |    Espere algunos minutos después de que se presiona el botón de hello desmontaje. Si los nuevos volúmenes de hello todavía se desmontan no, vaya a través de todos los volúmenes de Hola. Esta fuerza Hola iniciador toorefresh Hola hello y conexión volumen se desmonta con un mensaje de error que Hola disco no está disponible|
| Salida de archivo exe: secuencia de comandos se ejecuta correctamente pero "Nuevos volúmenes conectados" no se muestran en la salida de script de Hola |   Se trata de un problema transitorio.   | volúmenes de Hello habría ha adjuntado ya. Abra el explorador toobrowse. Si usas Hola mismo equipo para ejecutar secuencias de comandos cada vez, considere la posibilidad de reiniciar el equipo de Hola y se debe mostrar la lista de hello en hello exe posteriores ejecuciones. |
| Específicos de Linux: no se puede tooview Hola deseado volúmenes | Hola SO de la máquina de Hola donde se ejecuta el script de Hola podría no reconocer Hola filesystem subyacente del programa Hola a la copia de seguridad de máquina virtual | Compruebe si el punto de recuperación de hello es coherente o coherentes para el archivo de bloqueo. Si el script en otro equipo cuyo sistema operativo reconoce Hola Hola coherente y ejecución del archivo de copia de sistema de archivos de la máquina virtual |
| Específico de Windows: no se puede tooview Hola deseado volúmenes | se han adjuntado discos Hola pero no se han configurado los volúmenes de Hola | Desde la pantalla de administración de disco de bienvenida, identificar punto de recuperación de hello discos adicionales toohello relacionados. Si cualquiera de estos discos se encuentran sin conexión en estado intente hacerlos en línea con el botón secundario en el disco de Hola y haga clic en 'En línea'|
