<!--author=alkohli last changed:01/14/2016-->


#### <a name="toocreate-a-new-service"></a>toocreate un nuevo servicio
1. Con sus credenciales de cuenta de Microsoft, inicie sesión en toohello portal de Azure clásico en esta dirección URL: [https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. Hola portal de Azure clásico, haga clic en **New** > **Data Services** > **StorSimple Manager** > **rápido Crear**.
3. En el formulario de Hola que se muestra, Hola siguientes:
   
   1. Proporcione un **Nombre** único para el servicio. Se trata de un nombre descriptivo que se puede usar servicio de hello tooidentify. Hola nombre puede tener entre 2 y 50 caracteres que pueden ser letras, números y guiones. nombre de Hello debe empezar y terminar por una letra o un número.
   2. Proporcione una **Ubicación** para el servicio. En general, elija una ubicación más próxima toohello región geográfica donde desea toodeploy el dispositivo. Puede que también desee toofactor siguiente hello: 
      
      * Si tiene cargas de trabajo existentes en Azure que piensa también toodeploy con el dispositivo de StorSimple, debe usar ese centro de datos.
      * El servicio Administrador de StorSimple y el Almacenamiento de Azure pueden estar en dos ubicaciones independientes. En tal caso, es necesario toocreate hello StorSimple Manager y cuenta de almacenamiento de Azure por separado. toocreate una cuenta de almacenamiento de Azure, vaya toohello servicio de almacenamiento de Azure en hello portal de Azure clásico y siga los pasos de hello en [crear una cuenta de almacenamiento de Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Después de crear esta cuenta, agregar, el servicio StorSimple Manager toohello siguiendo los pasos de hello en [configurar una nueva cuenta de almacenamiento para el servicio de hello](../articles/storsimple/storsimple-deployment-walkthrough.md#configure-a-new-storage-account-for-the-service).
   3. Elija un **suscripción** desde la lista desplegable de Hola. suscripción de Hello está vinculado tooyour cuenta de facturación. Este campo no está presente si tiene una sola suscripción.
   4. Seleccione **crear una nueva cuenta de almacenamiento** tooautomatically crear una cuenta de almacenamiento con el servicio de Hola. Esta cuenta de almacenamiento tendrá un nombre especial, como "storsimplebwv8c6dcnf." Si necesitas tener tus datos en una ubicación diferente, desactiva esta casilla. 
   5. Haga clic en **crear Aministrador de StorSimple** toocreate servicio de Hola.
   
   ![Crear Administrador de StorSimple](./media/storsimple-create-new-service/HCS_CreateAService-include.png)
   
   Será dirigido toohello **servicio** página de aterrizaje. creación de servicio de Hello tardará unos minutos. Después de servicio Hola se crea correctamente, le notificará como corresponda y estado de hello del servicio de hello cambiará demasiado**Active**.
   
   ![Creación de servicios](./media/storsimple-create-new-service/HCS_StorSimpleManagerServicePage-include.png)

![Vídeo disponible](./media/storsimple-create-new-service/Video_icon.png)**Vídeo disponible**

toowatch un vídeo que muestra cómo toocreate un nuevo servicio de StorSimple Manager, haga clic en [aquí](https://azure.microsoft.com/documentation/videos/create-a-storsimple-manager-service/).

