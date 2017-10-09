Si la máquina virtual (VM) en Azure detecta un error de disco o de arranque, debe tooperform pasos en el disco duro virtual Hola propio para solucionar problemas. Un ejemplo común sería una actualización de la aplicación que ha fallado que impide que Hola VM correctamente. Este artículo se describe cómo toouse tooconnect portal Azure su toofix VM de disco duro virtual tooanother los errores y, a continuación, volver a crear la máquina virtual original.

## <a name="recovery-process-overview"></a>Introducción al proceso de recuperación
proceso de solución de problemas de Hello es como sigue:

1. Eliminar Hola máquina virtual que se produzca problemas, pero conservar los discos duros virtuales Hola.
2. Adjuntar y montar hello tooanother de disco duro virtual para solucionar el problema.
3. Conectar toohello solución de problemas de máquina virtual. Editar los archivos o ejecutar herramientas de errores de toofix en hello: disco duro virtual original.
4. Desmonte y desconecte Hola de disco duro virtual de hello VM de solución de problemas.
5. Crear una máquina virtual mediante hello: disco duro virtual original.

## <a name="delete-hello-original-vm"></a>Eliminar Hola VM original
Los discos duros virtuales y las máquinas virtuales son dos recursos diferentes de Azure. Un disco duro virtual es donde se almacenan el sistema operativo de hello, aplicaciones y configuraciones. Hola VM es solo de metadatos que define el tamaño de Hola o la ubicación y que hace referencia a recursos, como un disco duro virtual o una tarjeta de interfaz de red virtual (NIC). Cada disco duro virtual Obtiene una concesión asignada ese disco una vez conectado tooa máquina virtual. Aunque los discos de datos se pueden conectados y desconectados incluso mientras se está ejecutando Hola VM, no se puede desasociar el disco del sistema operativo Hola a menos que se elimine Hola recurso de máquina virtual. concesión de Hola continúa tooassociate Hola SO disco tooa VM incluso cuando esa máquina virtual está en un estado detenido o desasignado.

Hola primera toorecovering paso la máquina virtual es el recurso de máquina virtual de hello toodelete propio. Eliminando Hola VM deja Hola los discos duros virtuales en su cuenta de almacenamiento. Después de Hola que se elimina la máquina virtual, puede adjuntar Hola disco duro virtual tooanother VM tootroubleshoot y resolver errores de Hola. 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com). 
2. En el menú de hello en el lado izquierdo de hello, haga clic en **máquinas virtuales (clásicas)**.
3. Haga clic en la máquina virtual que tiene el problema de hello, seleccione hello **discos**y, a continuación, identificar nombre Hola de disco duro virtual de Hola. 
4. Seleccione el disco duro virtual de hello SO y comprobar hello **ubicación** cuenta de almacenamiento de hello tooidentify que contiene este disco duro virtual. En el siguiente ejemplo de Hola Hola cadena inmediatamente anterior ". blob.core.windows.net" es el nombre de cuenta de almacenamiento de Hola.

    ```
    https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd
    ```

    ![imagen de Hello acerca de la ubicación de la máquina virtual](./media/virtual-machines-classic-recovery-disks-portal/vm-location.png)

5. Haga clic en hello VM y, a continuación, seleccione **eliminar**. Asegúrese de que no se seleccionen discos Hola al eliminar Hola VM.
6. Cree una nueva máquina virtual de recuperación. Esta máquina virtual debe estar en hello mismo grupo de recursos y región (servicio de nube) como problema Hola VM.
7. Seleccione la máquina virtual de recuperación de hello y, a continuación, seleccione **discos** > **adjuntar existente**.
8. tooselect su disco duro virtual existente, haga clic en **archivo VHD**:

    ![Busque el disco duro virtual existente.](./media/virtual-machines-classic-recovery-disks-portal/select-vhd-location.png)

9. Seleccione la cuenta de almacenamiento de hello > contenedor VHD > Hola disco duro virtual, haga clic en hello **seleccione** botón tooconfirm su elección.

    ![Seleccione el disco duro virtual existente](./media/virtual-machines-classic-recovery-disks-portal/select-vhd.png)

10. Con un VHD ahora seleccionado, seleccione **Aceptar** tooattach Hola disco duro virtual existente.
11. Después de unos segundos, Hola **discos** panel para la máquina virtual se mostrará el disco duro virtual existente conectado como disco de datos:

    ![Disco duro virtual existente conectado como disco de datos](./media/virtual-machines-classic-recovery-disks-portal/attached-disk.png)

## <a name="fix-issues-on-hello-original-virtual-hard-disk"></a>Solucionar problemas en hello: disco duro virtual original
Cuando se montan hello: disco duro virtual existente, ahora puede realizar cualquier tarea de mantenimiento y solución de problemas de pasos según sea necesario. Una vez que se ha solucionado problemas hello, continúe con hello pasos.

## <a name="unmount-and-detach-hello-original-virtual-hard-disk"></a>Desmonte y desconecte hello: disco duro virtual original
Una vez que se resuelven los errores, desmonte y desasociar el disco duro virtual existente del saludo de la máquina virtual para solucionar problemas. No se puede usar el disco duro virtual junto con cualquier otra máquina virtual hasta que se libera la concesión de Hola que asocia toohello de disco duro virtual de hello VM de solución de problemas.  

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com). 
2. En el menú de hello en el lado izquierdo de hello, seleccione **máquinas virtuales (clásicas)**.
3. Busque la máquina virtual de recuperación de Hola. Seleccione los discos, disco de hello del menú contextual y, a continuación, seleccione **separar**.

## <a name="create-a-vm-from-hello-original-hard-disk"></a>Crear una máquina virtual desde el disco duro original de Hola

usar una máquina virtual desde el disco duro virtual original de toocreate [portal de Azure clásico](https://manage.windowsazure.com).

1. Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com).
2. En hello parte inferior del portal de hello, seleccione **New** > **proceso** > **Máquina Virtual** > **de la Galería** .
3. Hola **elegir una imagen** sección, seleccione **Mis discos**, y, a continuación, seleccione Hola disco duro virtual original. Compruebe la información de ubicación de Hola. Se trata de una región Hola donde debe implementarse Hola máquina virtual. Seleccione el botón siguiente Hola.
4. Hola **configuración de máquina Virtual** sección, escriba el nombre de la máquina virtual de Hola y seleccione un tamaño para hello máquina virtual.
