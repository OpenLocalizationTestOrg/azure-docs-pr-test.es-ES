


## <a name="attach-an-empty-disk"></a>Conectar un disco vacío
Conectar un disco vacío es un tooadd de manera sencilla disco de datos, ya que Azure crea el archivo .vhd de hello automáticamente y lo almacena en la cuenta de almacenamiento de Hola.

1. Haga clic en **máquinas virtuales (clásicas)**, y, a continuación, seleccione Hola VM adecuado.

2. En el menú de configuración de hello, haga clic en **discos**.

   ![Conectar un nuevo disco vacío](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. En la barra de comandos de hello, haga clic en **adjuntar nuevas**.  
    Hola **adjuntar nuevo disco** aparece el cuadro de diálogo.

    ![Conexión de un disco nuevo](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    Rellene Hola siguiente información:
    - En **nombre de archivo**, acepte el nombre predeterminado de Hola o escriba otro archivo .vhd de Hola. disco de datos de Hello usa un nombre generado automáticamente, incluso si escribe otro nombre para el archivo .vhd de Hola.
    - Seleccione hello **tipo** Hola disco de datos. Todas las máquinas virtuales admiten discos estándares. Muchas máquinas virtuales también admiten discos premium.
    - Seleccione hello **tamaño (GB)** Hola disco de datos.
    - Para **Almacenamiento en caché de host**, elija Ninguno o Solo lectura.
    - Haga clic en Aceptar toofinish.

4. Después de crear disco de datos de Hola y conectado, se muestra en la sección de discos de Hola de hello máquina virtual.

   ![Disco de datos nuevo y vacío conectado correctamente](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> Después de agregar un disco de datos, es necesario toolog en toohello VM e inicializar disco Hola para que se puede utilizar.

## <a name="how-to-attach-an-existing-disk"></a>Acoplamiento de un disco existente
El acoplamiento de un disco existente requiere que disponga de un .vhd disponible en la cuenta de almacenamiento. Hola de uso [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cuenta de almacenamiento toohello de archivo .vhd de hello tooupload de cmdlet. Una vez que haya creado y cargado el archivo .vhd de hello, puede adjuntarla tooa máquina virtual.

1. Haga clic en **máquinas virtuales (clásicas)**, y, a continuación, seleccione Hola máquina virtual adecuada.

2. En el menú de configuración de hello, haga clic en **discos**.

3. En la barra de comandos de hello, haga clic en **adjuntar existente**.

    ![Acoplar disco de datos](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. Haga clic en **Ubicación**. mostrar las cuentas de almacenamiento disponible de Hola. A continuación, seleccione una cuenta de almacenamiento adecuada de las que aparecen.

    ![Proporcionar la cuenta de almacenamiento de disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. Una **cuenta de almacenamiento** contiene uno o varios contenedores que contienen unidades de disco (discos duros virtuales). Seleccione el contenedor adecuado de Hola de los que aparecen.

    ![Proporcionar el contenedor de máquinas virtuales Windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. Hola **discos duros virtuales** panel muestra las unidades de disco de hello mantenidas en el contenedor de Hola. Haga clic en uno de los discos de hello y, a continuación, haga clic en seleccionar.

    ![Proporcionar la imagen de disco para máquinas virtuales de Windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. Hola **adjuntar el disco existente** panel se mostrará de nuevo con la ubicación de Hola que contiene la cuenta de almacenamiento de hello, contenedor y máquina virtual de disco duro seleccionado (vhd) tooadd toohello.

  Establecer **hospedar el almacenamiento en caché** toonone o lectura únicamente, a continuación, haga clic en Aceptar.

    ![Disco de datos conectado correctamente](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
