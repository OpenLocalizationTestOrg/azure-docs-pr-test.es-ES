#### <a name="to-create-a-new-service"></a>Para crear un nuevo servicio

1.  Con sus credenciales de cuenta de Microsoft, inicie sesión en Azure Portal en esta dirección URL: <https://portal.azure.com/>. Si va a implementar el dispositivo en el Portal de Government, inicie sesión en: <https://portal.azure.us/>.

2.  En Azure Portal, haga clic en **+ Nuevo** &gt; **Almacenamiento** &gt; **Serie virtual de StorSimple**.

    ![Creación de un servicio](./media/storsimple-virtual-array-create-new-service/createnewservice2.png) 

3.  En la hoja **Administrador de dispositivos de StorSimple** que se abre, haga lo siguiente:

    1.  Proporcione un valor único en **Nombre de recurso** para el servicio. El nombre de recurso es un nombre descriptivo que sirve para identificar el servicio. El nombre puede tener entre 2 y 50 caracteres que pueden ser letras, números y guiones. El nombre debe empezar y terminar con una letra o un número.

    2.  Elija una **Suscripción** en la lista desplegable. La suscripción está vinculada a la cuenta de facturación. Este campo no está presente si tiene una sola suscripción.

    3.  Para **Grupo de recursos**, seleccione un grupo de recursos existente o cree uno. Para más información, consulte [Grupos de recursos en Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).

    4.  Proporcione una **Ubicación** para el servicio. Consulte [Regiones de Azure](https://azure.microsoft.com/regions/#services) para más información acerca de qué servicios están disponibles en cada región. En general, elija una **ubicación** más cercana a la región geográfica donde desee implementar el dispositivo. También puedes querer tener en cuenta lo siguiente:

        -   Si tiene cargas de trabajo existentes en Azure que también va a implementar con el dispositivo de StorSimple, se recomienda usar ese centro de datos.

        -   El Administrador de dispositivos de StorSimple y el almacenamiento de Azure pueden encontrarse en dos ubicaciones independientes. En ese caso, se le pedirá que cree la cuenta del Administrador de dispositivos de StorSimple y la de almacenamiento de Azure por separado. Para crear una cuenta de almacenamiento de Azure, vaya al servicio Azure Storage en Azure Portal y siga los pasos indicados en la sección [Crear una cuenta de almacenamiento](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account). Después de crear esta cuenta, agréguela al servicio Administrador de dispositivos de StorSimple mediante los pasos indicados en la sección [Configurar una nueva cuenta de almacenamiento para el servicio](https://azure.microsoft.com/en-us/documentation/articles/storsimple-deployment-walkthrough/#configure-a-new-storage-account-for-the-service).

        -   Si está implementando el dispositivo virtual en el Portal de Government, el servicio Administrador de dispositivos de StorSimple se encuentra disponible en las ubicaciones EE. UU. (Iowa) y EE. UU. (Virginia).

    5.  Seleccione **Crear una nueva cuenta de almacenamiento de Azure** para crear automáticamente una cuenta de almacenamiento con el servicio. Especifique un **nombre de cuenta de almacenamiento**. Si necesitas tener tus datos en una ubicación diferente, desactiva esta casilla.

    6.  Active **Anclar al panel** si desea un vínculo rápido a este servicio en el panel.

    7.  Haga clic en **Crear** para crear el Administrador de dispositivos de StorSimple.

        ![Creación de un servicio](./media/storsimple-virtual-array-create-new-service/createnewservice4.png)  

Se le dirige a la página de destino del **Servicio**. Se tarda unos minutos en crear el servicio. Después de que el servicio se cree correctamente, se le notificará de forma adecuada y el estado del servicio cambiará a **Activo**.


