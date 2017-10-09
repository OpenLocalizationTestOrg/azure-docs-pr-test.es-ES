---
title: "aaaBackup máquinas virtuales de Windows Azure | Documentos de Microsoft"
description: "Para proteger las máquinas virtuales Windows, realice una copia de seguridad de ellas mediante Azure Backup."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a>Copia de seguridad de máquinas virtuales Windows en Azure

Para proteger sus datos realice copias de seguridad a intervalos regulares. Azure Backup crea puntos de recuperación que se almacenan en almacenes de recuperación con redundancia geográfica. Cuando se restaura desde un punto de recuperación, puede restaurar Hola toda máquina virtual o simplemente algunos archivos. Este artículo explica cómo toorestore un único archivo tooa VM ejecuta Windows Server e IIS. Si aún no tiene un toouse de máquina virtual, puede crear uno mediante hello [inicio rápido de Windows](quick-create-portal.md). En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una copia de seguridad de una máquina virtual.
> * Programar una copia de seguridad diaria.
> * Restaurar un archivo desde una copia de seguridad.




## <a name="backup-overview"></a>Introducción a Backup

Cuando Hola servicio copia de seguridad de Azure inicia un trabajo de copia de seguridad, desencadena Hola extensión de reserva tootake una instantánea en un momento. Hola servicio de copia de seguridad de Azure usa hello _VMSnapshot_ extensión. extensión de Hola se instala durante la copia de seguridad primera VM Hola si Hola máquina virtual se está ejecutando. Si hello no se está ejecutando, Hola servicio de copia de seguridad toma una instantánea de hello almacenamiento subyacente (debido a que ninguna aplicación de escritura aparecen al Hola que VM está en estado detenido).

Cuando se toma una instantánea de máquinas virtuales de Windows, servicio de copia de seguridad de Hola coordina con tooget de servicio de instantáneas de volumen (VSS) de hello una instantánea coherente de los discos de la máquina virtual Hola. Una vez Hola servicio de copia de seguridad de Azure toma instantáneas de hello, datos de hello están el almacén de toohello transferidos. toomaximize eficacia, servicio de hello identifica y transfiere únicamente los bloques de datos que han cambiado desde la copia de seguridad anterior de Hola Hola.

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

## <a name="recover-a-file"></a>Recuperación de un archivo

Si eliminar ni hacer cambios tooa archivo accidentalmente, puede usar el archivo de hello toorecover de recuperación de archivos desde el almacén de copia de seguridad. Recuperación de archivos utiliza una secuencia de comandos que se ejecuta en hello VM, punto de recuperación de hello toomount como unidad local. Estas unidades permanecerá montadas durante 12 horas para que pueda copiar archivos de punto de recuperación de Hola y restaurarlas toohello máquina virtual.  

En este ejemplo, mostramos cómo toorecover Hola archivo de imagen que se usa en la página web de hello predeterminada de IIS. 

1. Abra un explorador y conéctese toohello dirección IP de página IIS predeterminada de hello VM tooshow Hola.

    ![Página web predeterminada de IIS](./media/tutorial-backup-vms/iis-working.png)

2. Conectar toohello máquina virtual.
3. En hello VM, abra **Explorador de archivos** navegue too\inetpub\wwwroot y elimine el archivo hello **iisstart.png**.
4. En el equipo local, la actualización Hola explorador toosee que Hola imagen en la página IIS predeterminada Hola ha desaparecido.

    ![Página web predeterminada de IIS](./media/tutorial-backup-vms/iis-broken.png)

5. En el equipo local, abra una nueva pestaña y vaya Hola Hola [portal de Azure](https://portal.azure.com).
6. En el menú de Hola Hola izquierda, seleccione **máquinas virtuales** y seleccione Hola VM formulario Hola lista.
8. En el módulo VM hello, Hola **configuración** sección, haga clic en **copia de seguridad**. Hola **copia de seguridad** abre la hoja. 
9. En menú hello en parte superior de Hola de hoja de hello, seleccione **recuperación de archivos**. Hola **recuperación de archivos** abre la hoja.
10. En **paso 1: seleccione el punto de recuperación**, seleccione un punto de recuperación de Hola de lista desplegable.
11. En **paso 2: Descargar script toobrowse y recuperar archivos**, haga clic en hello **descargar ejecutable** botón. Guardar Hola archivo tooyour **descarga** carpeta.
12. En el equipo local, abra **Explorador de archivos** y navegue tooyour **descarga** Hola de carpeta y copie el archivo de .exe descargado. nombre de archivo de Hello estará prefijado por su nombre de máquina virtual. 
13. En la máquina virtual (a través de Hola conexión RDP) Pegar Hola .exe archivo toohello escritorio de la máquina virtual. 
14. Navegue toohello escritorio de la máquina virtual y haga doble clic en .exe Hola. Esto se inicie un símbolo del sistema y a continuación, monte el punto de recuperación de Hola como un recurso compartido de archivos que puede tener acceso. Cuando finaliza crear recurso compartido de hello, escriba **preguntas** tooclose Hola símbolo del sistema.
15. En la máquina virtual, abra **Explorador de archivos** y navegar por la letra de unidad de toohello que se usó para el recurso compartido de archivos de Hola.
16. Navegar por too\inetpub\wwwroot y copia **iisstart.png** desde archivo hello, compartir y pegarlos en \inetpub\wwwroot. Por ejemplo, copie F:\inetpub\wwwroot\iisstart.png y péguelo en el archivo de hello toorecover c:\inetpub\wwwroot.
17. En el equipo local, abra la pestaña del explorador de Hola que está conectado toohello dirección IP de hello máquina virtual que muestra hello IIS de forma predeterminada la página. Presione CTRL + F5 página del explorador toorefresh Hola. Ahora debería ver ese Hola se ha restaurado la imagen.
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









