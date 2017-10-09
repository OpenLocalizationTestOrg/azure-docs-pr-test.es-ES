#### <a name="toocreate-a-new-service"></a>toocreate un nuevo servicio

1.  Con sus credenciales de cuenta de Microsoft, inicie sesión en toohello portal de Azure en esta dirección URL: <https://portal.azure.com/>. Si la implementación de dispositivo de hello en el portal de administración pública, inicie sesión en: <https://portal.azure.us/>

2.  Hola portal de Azure, haga clic en **+ nuevo** &gt; **almacenamiento** &gt; **StorSimple Virtual Series**.

    ![Creación de un servicio](./media/storsimple-virtual-array-create-new-service/createnewservice2.png) 

3.  Hola **el Administrador de dispositivos de StorSimple** hoja que aparece, Hola siguientes:

    1.  Proporcione un valor único en **Nombre de recurso** para el servicio. nombre de recurso de Hello es un nombre descriptivo que se puede usar servicio de hello tooidentify. Hola nombre puede tener entre 2 y 50 caracteres que pueden ser letras, números y guiones. nombre de Hello debe empezar y terminar por una letra o un número.

    2.  Elija un **suscripción** desde la lista desplegable de Hola. suscripción de Hello está vinculado tooyour cuenta de facturación. Este campo no está presente si tiene una sola suscripción.

    3.  Para **Grupo de recursos**, seleccione un grupo de recursos existente o cree uno. Para más información, consulte [Grupos de recursos en Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).

    4.  Proporcione una **Ubicación** para el servicio. Consulte [Regiones de Azure](https://azure.microsoft.com/regions/#services) para más información acerca de qué servicios están disponibles en cada región. En general, elija un **ubicación** más cercano toohello de región geográfica donde desea toodeploy el dispositivo. Puede que también desee toofactor siguiente hello:

        -   Si tiene cargas de trabajo existentes en Azure que piensa también toodeploy con el dispositivo de StorSimple, recomendamos que utilice ese centro de datos.

        -   El Administrador de dispositivos de StorSimple y el almacenamiento de Azure pueden encontrarse en dos ubicaciones independientes. En tal caso, es necesario toocreate Hola Administrador de dispositivos de StorSimple y cuenta de almacenamiento de Azure por separado. toocreate una cuenta de almacenamiento de Azure, vaya toohello servicio de almacenamiento de Azure en hello portal de Azure y siga los pasos de hello en [crear una cuenta de almacenamiento de Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account). Después de crear esta cuenta, agregar, servicio de administrador de dispositivos de StorSimple toohello siguiendo los pasos de hello en [configurar una nueva cuenta de almacenamiento para el servicio de hello](https://azure.microsoft.com/en-us/documentation/articles/storsimple-deployment-walkthrough/#configure-a-new-storage-account-for-the-service).

        -   Si la implementación de dispositivo virtual de Hola Hola Portal de administración pública, Hola servicio Administrador de dispositivos de StorSimple está disponible en las ubicaciones de nosotros Iowa y nos Virginia.

    5.  Seleccione **crear una nueva cuenta de almacenamiento de Azure** tooautomatically crear una cuenta de almacenamiento con el servicio de Hola. Especifique un **nombre de cuenta de almacenamiento**. Si necesitas tener tus datos en una ubicación diferente, desactiva esta casilla.

    6.  Comprobar **toodashboard Pin** si desea que un servicio de toothis de vínculo rápido en el panel.

    7.  Haga clic en **crear** toocreate Hola Administrador de dispositivos de StorSimple.

        ![Creación de un servicio](./media/storsimple-virtual-array-create-new-service/createnewservice4.png)  

Está dirigido toohello **servicio** página de aterrizaje. creación de servicios de Hello tarda unos minutos. Después de servicio Hola se crea correctamente, le notificará como corresponda y estado de hello del servicio de hello cambiará demasiado**Active**.


