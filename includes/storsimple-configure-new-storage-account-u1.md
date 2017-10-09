<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a>tooadd una cuenta de almacenamiento de StorSimple 8000 Series Update 1.0
1. En la página de inicio el servicio StorSimple Manager hello, seleccione su servicio y haga doble clic en él. Esto le llevará toohello **inicio rápido** página. Seleccione hello **configurar** página.
2. Haga clic en **Agregar/editar cuenta de almacenamiento**.
3. Hola **Agregar/Editar cuenta de almacenamiento** cuadro de diálogo, haga clic en **agregar nueva**.
4. Hola **proveedor** proveedor de servicios de nube adecuada de campo, seleccione Hola. proveedores de Hola compatibles son Azure, S3 de Amazon, Amazon S3 con registros de recursos, HP y OpenStack. Especificar credenciales de Hola y ubicación de hello asociada con la cuenta de almacenamiento de Hola de sus proveedores de servicios de nube. campos de Hello presentadas las credenciales son diferentes dependiendo de proveedor de servicios de nube de Hola que ha especificado. 
   
   * Si ha seleccionado Azure como su proveedor de servicios de nube, proporcionar hello **nombre** hello principal y **clave de acceso** para su cuenta de almacenamiento de Microsoft Azure. Para una cuenta de Azure, ubicación de Hola se rellenarán automáticamente.
     
        ![Adición de cuenta de Azure Storage](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * Si ha seleccionado Amazon S3 o Amazon S3 con RRS, proporcione un **Nombre de cuenta de almacenamiento** descriptivo, una **Clave de acceso** y una **Clave secreta**. Para S3 de Amazon y Amazon S3 con registros de recursos, se admite Hola ubicaciones siguientes:
     
     * EE.UU. estándar
     * Oeste de EE. UU. (Oregon)
     * Oeste de EE. UU. (Norte de California)
     * UE (Irlanda)
     * Asia Pacífico (Singapur)
     * Asia Pacífico (Sídney)
     * Asia Pacífico (Tokio)
     * Sudamérica (Sao Paulo)
       
       ![Adición de cuenta de almacenamiento de Amazon](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * Si ha seleccionado HP como proveedor de servicios en la nube, proporcione un **nombre de cuenta de almacenamiento** descriptivo, un **identificador de inquilino**, un **nombre de usuario** y una **contraseña**. Para HP, se admite Hola ubicaciones siguientes:
     
     * Este de EE. UU.
     * Oeste de EE. UU.
       
       ![Adición de cuenta de almacenamiento de HP](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * Si ha seleccionado **Openstack** como el proveedor de servicios en la nube, proporcione un **Nombre de host**, una **clave de acceso** y una **clave secreta**.
     
     > [!NOTE]
     > Para todos los proveedores de servicios de nube de hello, excepto de Azure, se permite un nombre descriptivo. Puede usar diferentes nombres descriptivos y crear más de una cuenta de almacenamiento con el mismo conjunto de credenciales de Hola.
     > 
     > 
     
        ![Adición de cuenta de almacenamiento de Openstack](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. Seleccione **habilitar modo SSL** toocreate un canal seguro para la comunicación de red entre su dispositivo y hello en la nube. Desactive hello **habilitar modo SSL** casilla de verificación sólo si está operando en una nube privada.
   
   > [!NOTE]
   > Si usa HP como proveedor, siempre se habilitará SSL.
   > 
   > 
6. Haga clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png). Se le notificará una vez creada correctamente de la cuenta de almacenamiento de Hola.
7. Hola recién creado la cuenta de almacenamiento se mostrará en hello **configurar** página en **cuentas de almacenamiento**. Haga clic en **guardar** toosave Hola nueva cuenta de almacenamiento. Haga clic en **Aceptar** cuando se le pida confirmación.

