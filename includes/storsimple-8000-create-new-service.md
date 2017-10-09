<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a>toocreate un nuevo servicio

1. Utilice la toolog de las credenciales de cuenta de Microsoft en toohello [portal de Azure](https://portal.azure.com/).

2. Hola portal de Azure, haga clic en  **+**  y, a continuación, en el mercado de hello, haga clic en **ver todas**.

    ![Creación de un administrador de dispositivos de StorSimple](./media/storsimple-8000-create-new-service/createssdevman1.png)

    Busque el dispositivo _físico de StorSimple_. Seleccione y haga clic en **Serie física de dispositivos de StorSimple** y, a continuación, haga clic en **Crear**. O bien, en hello portal de Azure, haga clic en  **+**  y, a continuación, en **almacenamiento**, haga clic en **serie de dispositivo físico StorSimple**.

    ![Creación de un administrador de dispositivos de StorSimple](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. Hola **el Administrador de dispositivos de StorSimple** hoja, Hola lo siguiente:
   
   1. Proporcione un valor único en **Nombre de recurso** para el servicio. Este nombre es un nombre descriptivo que se puede usar servicio de hello tooidentify. Hola nombre puede tener entre 2 y 50 caracteres que pueden ser letras, números y guiones. nombre de Hello debe empezar y terminar por una letra o un número.

   2. Elija un **suscripción** desde la lista desplegable de Hola. suscripción de Hello está vinculado tooyour cuenta de facturación. Este campo no está presente si tiene una sola suscripción.

   3. Como **Grupo de recursos**, elija la opción **Usar existente** o **Crear nuevo**. Para más información, consulte [Grupos de recursos en Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).
   
   4. Proporcione una **Ubicación** para el servicio. En general, elija una ubicación más próxima toohello región geográfica donde desea toodeploy el dispositivo. Puede que también desee toofactor Hola siguientes consideraciones: 
      
      * Si tiene cargas de trabajo existentes en Azure que piensa también toodeploy con el dispositivo de StorSimple, debe usar ese centro de datos.
      * El servicio Administrador de dispositivos de StorSimple y Azure Storage pueden estar en dos ubicaciones independientes. En tal caso, es necesario toocreate Hola Administrador de dispositivos de StorSimple y cuenta de almacenamiento de Azure por separado. toocreate una cuenta de almacenamiento de Azure, vaya toohello servicio de almacenamiento de Azure en hello portal de Azure y siga los pasos de hello en [crear una cuenta de almacenamiento de Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Después de crear esta cuenta, agregar, servicio de administrador de dispositivos de StorSimple toohello siguiendo los pasos de hello en [configurar una nueva cuenta de almacenamiento para el servicio de hello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).

   5. Seleccione **crear una nueva cuenta de almacenamiento** tooautomatically crear una cuenta de almacenamiento con el servicio de Hola. Especifique un nombre para esta cuenta de almacenamiento. Si necesitas tener tus datos en una ubicación diferente, desactiva esta casilla.

   6. Comprobar **toodashboard Pin** si desea que un servicio de toothis de vínculo rápido en el panel.
      
   7. Haga clic en **crear** toocreate Hola Administrador de dispositivos de StorSimple.

       ![Creación de un administrador de dispositivos de StorSimple](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
creación de servicios de Hello tarda unos minutos. Una vez se haya creado correctamente el servicio de hello, verá una notificación y abrirá la hoja de hello nuevo servicio.
   
![Creación de un administrador de dispositivos de StorSimple](./media/storsimple-8000-create-new-service/createssdevman5.png)


