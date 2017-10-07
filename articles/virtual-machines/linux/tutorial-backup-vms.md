---
title: "Copia de seguridad de máquinas virtuales Linux en Azure | Microsoft Docs"
description: "Para proteger máquinas virtuales Linux, realice una copia de seguridad mediante Azure Backup."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>Copia de seguridad de máquinas virtuales Linux en Azure

Para proteger sus datos realice copias de seguridad a intervalos regulares. Azure Backup crea puntos de recuperación que se almacenan en almacenes de recuperación con redundancia geográfica. Cuando se restaura desde un punto de recuperación, puede restaurar Hola toda máquina virtual o simplemente algunos archivos. Este artículo explica cómo toorestore un único archivo tooa nginx de ejecución de VM de Linux. Si aún no tiene un toouse de máquina virtual, puede crear uno mediante hello [inicio rápido de Linux](quick-create-cli.md). En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una copia de seguridad de una máquina virtual.
> * Programar una copia de seguridad diaria.
> * Restaurar un archivo desde una copia de seguridad.



## <a name="backup-overview"></a>Introducción a Backup

Cuando Hola servicio copia de seguridad de Azure inicia una copia de seguridad, desencadena Hola extensión de reserva tootake una instantánea en un momento. Hola servicio de copia de seguridad de Azure usa hello _VMSnapshotLinux_ extensión en Linux. extensión de Hola se instala durante la copia de seguridad primera VM Hola si Hola máquina virtual se está ejecutando. Si hello no se está ejecutando, Hola servicio de copia de seguridad toma una instantánea de hello almacenamiento subyacente (debido a que ninguna aplicación de escritura aparecen al Hola que VM está en estado detenido).

De forma predeterminada, copia de seguridad de Azure toma una copia de seguridad coherente sistema para VM de Linux, pero puede ser configurado tootake [aplicación copia de seguridad coherente con marco script previo y posterior a la secuencia de comandos](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). Una vez Hola servicio de copia de seguridad de Azure toma instantáneas de hello, datos de hello están el almacén de toohello transferidos. toomaximize eficacia, servicio de hello identifica y transfiere únicamente los bloques de datos que han cambiado desde la copia de seguridad anterior de Hola Hola.

Una vez completada la transferencia de datos hello, instantánea Hola se quita y se crea un punto de recuperación.


## <a name="create-a-backup"></a>Creación de una copia de seguridad
Crear una sencilla programado diario copia de seguridad tooa almacén de servicios de recuperación. 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de Hola Hola izquierda, seleccione **máquinas virtuales**. 
3. En lista de hello, seleccione tooback de una máquina virtual.
4. En el módulo VM hello, Hola **configuración** sección, haga clic en **copia de seguridad**. Hola **habilitar copia de seguridad** abre la hoja.
5. En **del almacén de servicios de recuperación**, haga clic en **crear nuevo** y proporcione el nombre de hello para el nuevo almacén de Hola. Se crea un nuevo almacén en hello mismo grupo de recursos y la ubicación como máquina virtual de Hola.
6. Haga clic en **Directiva de copia de seguridad**. En este ejemplo, mantenga los valores predeterminados de Hola y haga clic en **Aceptar**.
7. En hello **habilitar copia de seguridad** hoja, haga clic en **habilitar la copia de seguridad**. Esto crea una copia de seguridad diaria según la programación predeterminada de Hola.
10. un punto de recuperación inicial, en hello toocreate **copia de seguridad** hoja haga clic en **una copia de seguridad ahora**.
11. En hello **copia de seguridad ahora** hoja, haga clic en el icono del calendario de hello, usar Hola calendario control tooselect hello último día de este punto de recuperación se conservan y haga clic en **copia de seguridad**.
12. Hola **copia de seguridad** hoja para la máquina virtual, verá Hola número de puntos de recuperación que están completos.

    ![Puntos de recuperación](./media/tutorial-backup-vms/backup-complete.png)

primera copia de seguridad de Hello tarda aproximadamente 20 minutos. Una vez finalizada la copia de seguridad, continúe toohello siguiente parte de este tutorial.

## <a name="restore-a-file"></a>Restauración de un archivo

Si eliminar ni hacer cambios tooa archivo accidentalmente, puede usar el archivo de hello toorecover de recuperación de archivos desde el almacén de copia de seguridad. Recuperación de archivos utiliza una secuencia de comandos que se ejecuta en hello VM, punto de recuperación de hello toomount como unidad local. Estas unidades permanecerá montadas durante 12 horas para que pueda copiar archivos de punto de recuperación de Hola y restaurarlas toohello máquina virtual.  

En este ejemplo, mostramos cómo toorecover Hola predeterminado nginx página web /var/www/html/index.nginx-debian.html. Hola de dirección IP pública de la máquina virtual en este ejemplo es *13.69.75.209*. Puede encontrar la dirección IP de saludo de la vm con:

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. En el equipo local, abra un explorador y escriba en la dirección IP pública de saludo de la página web VM toosee Hola predeterminada nginx.

    ![Página web predeterminada de nginx](./media/tutorial-backup-vms/nginx-working.png)

1. Utilice SSH en la máquina virtual.

    ```bash
    ssh 13.69.75.209
    ```
2. Elimine /var/www/html/index.nginx-debian.html.

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. En el equipo local, actualice el Explorador de hello presionando CTRL + F5 toosee esos valores predeterminados de página nginx ha desaparecido.

    ![Página web predeterminada de nginx](./media/tutorial-backup-vms/nginx-broken.png)
    
1. En el equipo local, inicie sesión toohello [portal de Azure](https://portal.azure.com/).
6. En el menú de Hola Hola izquierda, seleccione **máquinas virtuales**. 
7. En lista de hello, seleccione Hola máquina virtual.
8. En el módulo VM hello, Hola **configuración** sección, haga clic en **copia de seguridad**. Hola **copia de seguridad** abre la hoja. 
9. En menú hello en parte superior de Hola de hoja de hello, seleccione **recuperación de archivos**. Hola **recuperación de archivos** abre la hoja.
10. En **paso 1: seleccione el punto de recuperación**, seleccione un punto de recuperación de Hola de lista desplegable.
11. En **paso 2: Descargar script toobrowse y recuperar archivos**, haga clic en hello **descargar ejecutable** botón. Guarde el equipo local de hello archivo descargado tooyour.
7. Haga clic en **descargar script** archivo de script de Hola de toodownload localmente.
8. Abra un Hola de símbolo del sistema y el tipo de Bash siguientes, reemplazando *Linux_myVM_05-05-2017.sh* con hello corregir la ruta de acceso y nombre de archivo de script de Hola que ha descargado, *azureuser* con nombre de usuario de Hola para hello VM y *13.69.75.209* con la dirección IP pública de hello para la máquina virtual.
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. En el equipo local, abra una toohello de conexión SSH máquina virtual.

    ```bash
    ssh 13.69.75.209
    ```
    
10. En la máquina virtual, agregue ejecutar el archivo de secuencia de comandos de toohello de permisos.

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. En la máquina virtual, ejecute punto de recuperación de hello script toomount Hola como un sistema de archivos.

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. Hola de salida de hello script proporciona que Hola ruta de acceso de punto de montaje de Hola. salida de Hello tiene un aspecto similar toothis:

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. En la máquina virtual, copie hello nginx página web desde el punto de montaje hello toowhere atrás eliminar archivo hello.

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. En el equipo local, abra la pestaña del explorador de Hola que está conectado toohello dirección IP de hello máquina virtual que muestra hello nginx de forma predeterminada la página. Presione CTRL + F5 página del explorador toorefresh Hola. Ahora debería ver ese Hola página predeterminada está funcionando de nuevo.

    ![Página web predeterminada de nginx](./media/tutorial-backup-vms/nginx-working.png)

18. En el equipo local, volver atrás toohello pestaña del explorador para hello portal de Azure y en **paso 3: desmontar discos Hola después de la recuperación** haga clic en hello **desmontar discos** botón. Si olvida este paso toodo, el punto de montaje de hello conexión toohello es cerrar automáticamente después de 12 horas. Después de esas 12 horas, debe toodownload un toocreate de script nuevo un nuevo punto de montaje.


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Crear una copia de seguridad de una máquina virtual.
> * Programar una copia de seguridad diaria.
> * Restaurar un archivo desde una copia de seguridad.

Avanzar toohello toolearn de tutorial siguiente sobre la supervisión de máquinas virtuales.

> [!div class="nextstepaction"]
> [Supervisión de máquinas virtuales](tutorial-monitoring.md)

