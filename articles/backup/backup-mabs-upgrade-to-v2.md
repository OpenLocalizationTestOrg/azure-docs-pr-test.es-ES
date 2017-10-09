---
title: aaaInstall v2 del servidor de copia de seguridad de Azure | Documentos de Microsoft
description: "Azure Backup Server v2 proporciona funciones mejoradas de copia de seguridad para proteger máquinas virtuales, archivos, carpetas, cargas de trabajo, etc. Obtenga información acerca de cómo actualizar o tooinstall tooAzure v2 del servidor de copia de seguridad."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a>Instalar Azure Backup Server v2

Azure Backup Server ayuda a proteger máquinas virtuales (VM), cargas de trabajo, archivos, carpetas, etc. Azure Backup Server v2 se basa en Azure Backup Server v1 y proporciona características nuevas que no están disponibles en la versión v1. Para obtener una comparación de las características de v1 y v2, vea [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md) (Matriz de protección de Azure Backup Server). 

características adicionales de Hello en el servidor de copia de seguridad v2 son una actualización de servidor de copia de seguridad v1. A pesar de ello, no es un requisito previo disponer de Backup Server v1 para instalar Backup Server v2. Si desea tooupgrade desde el servidor de copia de seguridad v1 tooBackup v2 de servidor, instale v2 del servidor de copia de seguridad en servidor de protección del servidor de copia de seguridad de Hola. La configuración existente de Backup Server permanecerá intacta.

Puede instalar Backup Server v2 en Windows Server 2012 R2 o Windows Server 2016. tootake las nuevas características, como moderno copia de seguridad de almacenamiento de System Center 2016 datos Protection Manager, debe instalar el servidor de copia de seguridad v2 en Windows Server 2016. Antes de actualizar tooor install v2 del servidor de copia de seguridad, que conozca hello [requisitos previos de instalación](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).

> [!NOTE]
> Servidor de copia de seguridad de Azure tiene Hola mismo código base como System Center Data Protection Manager. Copia de seguridad v1 de servidor es equivalente tooData Protection Manager 2012 R2 y v2 del servidor de copia de seguridad es equivalente tooData Protection Manager 2016. En ocasiones, este artículo hace referencia a documentación de Data Protection Manager Hola.
>
>

## <a name="upgrade-backup-server-toov2"></a>Actualizar toov2 de copia de seguridad de servidor
tooupgrade desde el servidor de copia de seguridad v1 tooBackup v2 de servidor, asegúrese de que la instalación tiene las actualizaciones de hello necesario:

- [Actualizar agentes de protección de hello](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) en Hola de servidores protegidos.
- Actualizar Windows Server 2012 R2 tooWindows Server 2016.
- Actualice Remote Administrator de Azure Backup Server en todos los servidores de producción.
- Asegúrese de que las copias de seguridad se establecen toocontinue sin necesidad de reiniciar el servidor de producción.


### <a name="upgrade-steps-for-backup-server-v2"></a>Pasos para actualizar a Backup Server v2

1. En el centro de descarga, hello [Descargue el instalador de actualización de hello](https://go.microsoft.com/fwlink/?LinkId=626082).

2. Después de extraer el Asistente para la instalación de hello, asegúrese de que **ejecutar setup.exe** está seleccionada y, a continuación, seleccione **finalizar**.

  ![Instalador: ejecutar el programa de instalación](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. En el Asistente para servidor de copia de seguridad de Microsoft Azure de hello, en **instalar**, seleccione **servidor de copia de seguridad de Microsoft Azure**.

  ![Instalador: seleccionar la instalación](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. En hello **bienvenida** página, revise las advertencias de hello y, a continuación, seleccione **siguiente**.

  ![Instalador: página principal](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. Asistente para la instalación de Hello realiza comprobaciones de requisitos previos toomake seguro que puede actualizar el entorno. En hello **Prerequisite Checks** página, seleccione **comprobar**.

  ![Instalador: página Comprobaciones de requisitos previos](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. El entorno debe pasar comprobaciones de requisitos previos de Hola. Si su entorno no superan las comprobaciones de hello, tenga en cuenta los problemas de Hola y corregirlos. Después, seleccione **Comprobar de nuevo**. Después de pasar comprobaciones de requisitos previos de hello, seleccione **siguiente**.

  ![Instalador: botón Comprobar de nuevo](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. En hello **configuración de SQL** , seleccione la opción relevantes de hello para la instalación de SQL y, a continuación, seleccione **comprobar e instalar**.

  ![Instalador: página Configuración de SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  comprobaciones de Hello pueden tardar unos minutos. Cuando las comprobaciones de Hola se termine, seleccione **siguiente**.

  ![Instalador: botón Comprobar e instalar en Configuración de SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. En hello **configuración de la instalación** página, asegúrese de cualquier ubicación de toohello de cambios que está instalado el servidor de copia de seguridad o toohello ubicación de memoria virtual. Seleccione **Siguiente**.

  ![Instalador: página Configuración de la instalación](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. toofinish Hola Asistente para instalación, seleccione **finalizar**.

  ![Instalador: finalizar](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a>Agregar almacenamiento para Modern Backup Storage

eficiencia del almacenamiento de copia de seguridad tooimprove, servidor de reserva v2 agrega compatibilidad con volúmenes. Al igual que Backup Server v1, Backup Server v2 admite discos.

### <a name="add-volumes-and-disks"></a>Agregar volúmenes y discos
Si ejecuta v2 del servidor de copia de seguridad en Windows Server 2016, puede usar datos de copia de seguridad de volúmenes toostore. Los volúmenes permiten ahorrar almacenamiento y realizar copias de seguridad más rápido. Dado que los volúmenes son tooBackup nuevo servidor, debe agregarlos. 

Cuando se agrega un servidor de tooBackup de volumen, puede permitir el volumen de hello un nombre descriptivo. Haga clic en hello **Nombre_descriptivo** columna del volumen de Hola que desea tooname. Puede cambiar el nombre de hello más adelante, si es necesario. También puede usar PowerShell tooadd o cambiar los nombres descriptivos para los volúmenes.

tooadd un volumen en hello consola de administrador:

1. En la consola de administrador del servidor de copia de seguridad de Azure hello, seleccione **administración** > **almacenamiento en disco** > **agregar**.

    ![Asistente para agregar almacenamiento en disco de hello abierto](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    Se abrirá el Asistente para agregar almacenamiento en disco de Hola.

2. En hello **agregar almacenamiento en disco** página Hola **volúmenes disponibles** cuadro, seleccione un volumen y, a continuación, seleccione **agregar**.
3. Hola **seleccionado volúmenes** cuadro, escriba un nombre descriptivo para el volumen de hello y, a continuación, seleccione **Aceptar**.

      ![Asistente para agregar almacenamiento en disco: agregar volumen](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  Si desea tooadd un disco, disco de hello debe pertenecer tooa grupo de protección que tiene un almacenamiento heredado. Estos discos solo se pueden usar para estos grupos de protección. Si el servidor de copia de seguridad no tiene orígenes que tienen protección heredada, disco de hello no aparece.

  Para obtener más información acerca de cómo agregar discos, consulte [adición de almacenamiento de discos tooincrease heredado](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage). No se puede asignar un nombre descriptivo a un disco.


### <a name="assign-workloads-toovolumes"></a>Asignar toovolumes de cargas de trabajo

En el servidor de copia de seguridad, puede especificar que las cargas de trabajo se asignan toowhich volúmenes. Por ejemplo, puede establecer volúmenes costosos que admiten un gran número de operaciones de entrada/salida por segundo (IOPS) toostore solo las cargas de trabajo que requieren copias de seguridad frecuentes de gran volumen. Un ejemplo es SQL Server con registros de transacciones.

#### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

propiedades de hello tooupdate de un volumen en el bloque de almacenamiento de hello en el servidor de copia de seguridad, use el cmdlet de PowerShell de hello DPMDiskStorage de actualización.

Sintaxis:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

Todos los cambios realizados mediante el uso de PowerShell se reflejan en hello interfaz de usuario.


## <a name="protect-data-sources"></a>Proteger orígenes de datos
toobegin protegen orígenes de datos, cree un grupo de protección. Hola siguiendo los pasos resaltado cambios o adiciones toohello Asistente para nuevo grupo de protección.

toocreate un grupo de protección:

1. En la consola de administrador del servidor de copia de seguridad de hello, seleccione **protección**.

2. En la cinta de opciones de herramienta de hello, seleccione **nuevo**.

    Se abrirá el Asistente para crear nuevo grupo de protección de Hola.

  ![Asistente para crear nuevo grupo de protección](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. En hello **bienvenida** página, seleccione **siguiente**.
4. En hello **Seleccionar tipo de grupo de protección** , seleccione el tipo de saludo de grupo de protección que desee toocreate y, a continuación, seleccione **siguiente**.

  ![Página Seleccionar tipo de grupo de protección](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. En hello **seleccionar miembros del grupo** página Hola **miembros disponibles** panel, los miembros de hello con se muestran los agentes de protección. En este ejemplo, seleccione el volumen D:\ y E:\ y agregarlas toohello **seleccionado miembros** panel. Seleccione **Siguiente**.

  ![Página Seleccionar miembros del grupo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. En hello **Seleccionar método de protección de datos** página, escriba un **el nombre del grupo de protección**, seleccione el método de protección de hello y, a continuación, seleccione **siguiente**. Si desea que la protección a corto plazo, debe seleccionar hello **disco** método de copia de seguridad.

  ![Página Seleccionar método de protección de datos](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. En hello **especificar objetivos a corto plazo** detalles de la página, seleccione Hola para **duración de retención** y **frecuencia de sincronización**. Después, seleccione **Siguiente**. Si lo desea, toochange programación Hola para cuando los puntos de recuperación se realizó, seleccione **modificar**.

  ![Página Especificar objetivos a corto plazo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. En hello **Revisar asignación de almacenamiento de disco** página, revise los detalles acerca de los orígenes de datos de hello seleccionó, su tamaño y los valores de hello espacio toobe aprovisionado y Hola volumen de almacenamiento de destino.

  ![Página Revisar la asignación del almacenamiento en disco](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  Volúmenes de almacenamiento se basan en la asignación del volumen de carga de trabajo de hello (establecido mediante el uso de PowerShell) y Hola almacenamiento disponible. Puede cambiar los volúmenes de almacenamiento de hello seleccionando otros volúmenes en el menú desplegable de Hola. Si cambia el valor de Hola para **almacenamiento de destino**, Hola valor para **almacenamiento en disco disponible** cambia dinámicamente valores tooreflect en **espacio** y **Insuficiente espacio**.

  Si los orígenes de datos de hello aumentan según lo previsto, Hola valor para hello **espacio insuficiente** columna en **almacenamiento en disco disponible** refleja la cantidad de Hola de almacenamiento adicional que se necesita. Use este plan de toohelp valor las necesidades de almacenamiento de copias de seguridad sin problemas. Si Hola valor es cero, significa que no hay ningún problema potencial con el almacenamiento en un futuro previsible Hola. Si el valor de hello es un número distinto de cero, no tiene suficiente espacio de almacenamiento asignado (basado en protección hello y directiva de tamaño de los datos de los miembros protegidos).

  ![Almacenamiento en disco subasignado](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   toofinish crear a un asistente de hello completa, grupo de protección.

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a>Migrar almacenamiento heredado tooModern almacenamiento de copia de seguridad
Después de actualizar tooor install v2 del servidor de copia de seguridad y actualización hello tooWindows de sistema operativo Server 2016, actualice su toouse de grupos de protección moderna almacenamiento de copia de seguridad. De forma predeterminada, los grupos de protección no se cambian. Se siguen toofunction tal y como configuraron inicialmente. 

Actualizar toouse de grupos de protección moderna almacenamiento de copia de seguridad es opcional. grupo de protección de hello tooupdate, detenga la protección de todos los orígenes de datos mediante el uso de hello opción Conservar datos. A continuación, agregue Hola datos orígenes tooa nuevo grupo de protección.

1. En la consola de administrador de hello, seleccione hello **protección** característica. Hola **miembro del grupo de protección** lista, haga clic en miembro de hello y, a continuación, seleccione **detener la protección de miembro**.

  ![Detener protección de miembro](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. Hola **quitar del grupo** cuadro de diálogo, revisión Hola utiliza espacio en disco y espacio libre disponible hello para el grupo de almacenamiento de Hola. predeterminado de Hello es tooleave puntos de recuperación de hello en el disco de Hola y permitirles tooexpire por su directiva de retención asociado. Haga clic en **Aceptar**.

  Si desea que el espacio del disco de hello devuelto utiliza de tooimmediately toohello grupo de almacenamiento libre, seleccione hello **Eliminar réplica en disco** datos de copia de seguridad de casilla de verificación toodelete Hola (y los puntos de recuperación) asociados a ese miembro.

  ![Cuadro de diálogo Quitar del grupo](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. Cree un grupo de protección que use Modern Backup Storage. Incluir orígenes de datos de hello desprotegido.


## <a name="add-disks-tooincrease-legacy-storage"></a>Agregar almacenamiento de discos tooincrease heredado

Si desea toouse almacenamiento heredado con el servidor de copia de seguridad, tendrá que almacenamiento de información de tooadd discos tooincrease heredado. 

almacenamiento en disco tooadd:

1. En la consola de administrador de hello, seleccione **administración** > **almacenamiento en disco** > **agregar**.

    ![Cuadro de diálogo Agregar almacenamiento en disco](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. Hola **agregar almacenamiento en disco** cuadro de diálogo, seleccione **agregar discos**.

5. En la lista de Hola de discos disponibles, seleccione los discos de hello desea tooadd, seleccione **agregar**y, a continuación, seleccione **Aceptar**.

## <a name="update-hello-data-protection-manager-protection-agent"></a>Actualizar el agente de protección de hello Data Protection Manager

Servidor de copia de seguridad utiliza el agente de protección de System Center Data Protection Manager Hola para las actualizaciones. Si va a actualizar a un agente de protección que no sea red toohello conectado, no puede usar hello toocomplete de la consola de administrador de protección de datos de una actualización de agente conectada. Debe actualizar el agente de protección de hello en un entorno de dominio no esté activa. Hasta que Hola cliente equipo red toohello conectado, Hola que consola de administrador de protección de datos muestra esa actualización de agente de protección de hello está pendiente.

Hello siguientes secciones se describen cómo tooupdate los agentes de protección para los equipos cliente que están conectados y los equipos cliente que no están conectados.

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a>Actualizar un agente de protección de un equipo cliente conectado

1. En la consola de administrador del servidor de copia de seguridad de hello, seleccione **administración** > **agentes**.

2. En el panel de información de hello, seleccionar equipos de cliente de hello para el que desea que agente de protección de tooupdate Hola.

  > [!NOTE]
  > Hola **las actualizaciones del agente** columna indica cuando una actualización de agente de protección está disponible para cada equipo protegido. Hola **acciones** panel, hello **actualización** acción sólo está disponible cuando se selecciona un equipo protegido y las actualizaciones están disponibles.
  >
  >

3. tooinstall actualizar agentes de protección en los equipos de hello seleccionado, de hello **acciones** panel, seleccione **actualización**.

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a>Actualizar un agente de protección en un equipo cliente que no está conectado

1. En la consola de administrador del servidor de copia de seguridad de hello, seleccione **administración** > **agentes**.

2. En el panel de información de hello, seleccionar equipos de cliente de hello para el que desea que agente de protección de tooupdate Hola.

  > [!NOTE]
   > Hola **las actualizaciones del agente** columna indica cuando una actualización de agente de protección está disponible para cada equipo protegido. Hola **acciones** panel, hello **actualización** acción no está disponible cuando se selecciona un equipo protegido si existen actualizaciones disponibles.
  >
  >

3. tooinstall actualizar agentes de protección en los equipos de hello seleccionado, seleccionados **actualización**.

4. Para un equipo cliente que no está conectado toohello red, hasta que el equipo de hello red toohello conectado, Hola **estado del agente** columna muestra un estado de **actualizar pendientes**.

  Después de que un equipo cliente está conectado toohello red, Hola **las actualizaciones del agente** columna para el equipo de cliente hello muestra un estado de **actualizar**.
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a>Mover grupos de protección heredados de una versión antigua y la nueva versión de hello de sincronización con Azure

Una vez que se actualizan hello sistema operativo y el servidor de copia de seguridad de Azure, está listo tooprotect nuevos orígenes de datos mediante almacenamiento de copia de seguridad modernos. Los orígenes de datos protegidos sin embargo ya continuará toobe protegida Hola heredado forma que estuviera en el servidor de copia de seguridad de Azure pero todos los nuevo grupo de protección utilizarán moderna almacenamiento de copia de seguridad.

Pasos siguientes son orígenes de datos de toomigrate del modo heredado de almacenamiento de copia de seguridad de tooModern de protección.

• Agregue el bloque de almacenamiento para DPM el nuevo toohello volúmenes hello y asignar etiquetas de origen de datos y nombres descriptivas si lo desea.
• Para cada origen de datos que se encuentra en modo heredado, detenga la protección de orígenes de datos de Hola y "Conservar datos protegidos".  Así permitirá la recuperación de los puntos de recuperación antiguos después de la migración.

• Crear un nuevo grupo de protección y seleccione orígenes de datos de Hola que son toobe almacenada con el nuevo formato.
• DPM realizará una copia de la réplica de almacenamiento de copia de seguridad heredadas de hello en hello volumen de almacenamiento de copia de seguridad moderna localmente.
Nota: Esto se verá como un trabajo de operación posterior a la recuperación • Todos los nuevos puntos de recuperación y sincronización se almacenarán entonces en Modern Backup Storage.
• Puntos de recuperación antiguos se eliminarán cuando expire y finalmente liberar espacio en disco Hola.
• Una vez que todos los volúmenes de hello heredado se eliminan de almacenamiento anterior hello, disco de Hola se puede quitar del sistema de hello y copia de seguridad de Azure.
• Realizar una copia de seguridad de hello Azure DPMDB.

Parte 2:-elementos importantes > Hola nuevo servidor deberá toobe mismo nombre como servidor de copia de seguridad de Azure de hello original. No se puede cambiar el nombre de Hola Hola nueva copia de seguridad del servidor de Azure si desea toouse anterior grupo de almacenamiento y los puntos de recuperación de base de datos DPM tooretain - debe hacer copia de seguridad de base de datos DPM ya que será necesario toobe restaurar

1) Cierre Hola servidor de copia de seguridad de Azure original o dejarlo fuera de conexión de Hola.
2) Restablecimiento de cuentas de máquina de hello en active directory.
3) Instalar Server 2016 en el nombre Hola mismo nombre de equipo como servidor de copia de seguridad de Azure original de Hola y nueva máquina.
4) Unirse a dominio Hola
5) Instale Azure Backup Server V2 (mueva los discos del grupo de DPM Storage desde el servidor antiguo e impórtelos)
6) Restaurar Hola DPMDB tomada del final de la parte 2
7) Adjuntar almacenamiento Hola de hello original copia de seguridad toohello nuevo servidor.
8) De hello SQL Restaurar base de datos DPM
9) Desde la línea de comandos de administración en el nuevo servidor cd tooMicrosoft copia de seguridad de Azure instalar ubicación y la carpeta bin

Ejemplo de ruta de acceso: C:\windows\system32>cd "c:\Archivos de programa\Microsoft Azure Backup\DPM\DPM\bin\
copia de seguridad de tooAzure ejecute DPMSYNC-SYNC

10) Ejecute DPMSYNC-SYNC Nota Si ha agregado el nuevo grupo de almacenamiento de DPM de toohello de discos en lugar de moverse Hola gastadas, a continuación, ejecute DPMSYNC - Reallocatereplica

## <a name="new-powershell-cmdlets-in-v2"></a>Nuevos cmdlets de PowerShell en v2

Cuando se instala Azure Backup Server v2, hay dos nuevos cmdlets disponibles: 
* [Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx)
* [Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooprepare el servidor o empezar a proteger una carga de trabajo:
- [Preparar cargas de trabajo de Backup Server](backup-azure-microsoft-azure-backup.md)
- [Usar tooback del servidor de copia de seguridad de un servidor de VMware](backup-azure-backup-server-vmware.md)
- [Usar tooback del servidor de copia de seguridad de SQL Server](backup-azure-sql-mabs.md)
- [Usar Modern Backup Storage con Backup Server](backup-mabs-add-storage.md)

