<!--author=alkohli last changed: 07/19/2017-->

#### <a name="toocreate-a-volume"></a>toocreate un volumen
1. Desde la lista tabular de Hola de dispositivos de Hola Hola **dispositivos** hoja, seleccione el dispositivo. Haga clic en **+ Agregar volumen**.

    ![Adición de un nuevo volumen](./media/storsimple-8000-create-volume-u2/step5createvol1.png)

2. Hola **agregar un volumen** hoja:
   
   1. Hola **dispositivo seleccione** campo se rellena automáticamente con el dispositivo actual.

   2. Desde la lista desplegable de hello, seleccione el contenedor de volúmenes de hello en las que necesite tooadd un volumen. 

   3.  Escriba un **Nombre** para el volumen. No se puede cambiar el nombre de un volumen una vez que se crea el volumen de Hola.

   4. En la lista desplegable de hello, seleccione hello **tipo** para su volumen. Para cargas de trabajo que requieren garantías locales, latencias bajas y un rendimiento más alto, seleccione un volumen **Localmente anclado** . Para todos los demás datos, seleccione un volumen **En capas** . Si usa este volumen para datos de archivo, seleccione **Usar este volumen para los datos de archivo a los que accede con menos frecuencia**.
      
       Un volumen en capas se aprovisiona de manera fina y se puede crear rápidamente. Seleccionar **usar este volumen de datos acceso menos frecuente archivados** volumen en capas destinado a los datos de archivo cambios tamaño del fragmento de desduplicación de Hola para su volumen too512 KB. Si este campo no está activado, volumen en capas correspondiente de hello usa un tamaño de fragmento de 64 KB. Un tamaño de fragmento de desduplicación permite la transferencia de hello tooexpedite hello de dispositivo de nube de toohello de los datos de archivo grande.
       
       Un volumen anclado localmente se realiza un aprovisionamiento grueso y asegura que los datos principal de hello en volumen de hello permanece dispositivo toohello local y no volcarse toohello en la nube.  Si crea un volumen anclado localmente, comprobación de espacio disponible en los niveles de hello local dispositivo de hello tooprovision volumen de Hola de hello tamaño solicitado. operación Hola de creación de un volumen anclado localmente puede implicar verter los datos existentes de la nube de toohello de dispositivo de Hola y Hola tomadas el volumen de hello toocreate puede ser largo. tiempo total de Hello depende de tamaño de hello del volumen de hello aprovisionado, el ancho de banda de red disponible y datos de hello en el dispositivo.

   5. Especificar hello **capacidad aprovisionada** para su volumen. Tome nota de la capacidad de Hola que está disponible en función de tipo de volumen de hello seleccionado. Hola especifica el tamaño del volumen no debe superar el espacio disponible de Hola.
      
       Puede aprovisionar volúmenes en capas hasta too200 TB en dispositivo 8100 Hola o volúmenes anclados localmente una too8.5 TB. En el dispositivo 8600 mayor de hello, puede aprovisionar volúmenes anclados localmente una too22.5 TB o volúmenes en capas hasta too500 TB. Que haya espacio local en el dispositivo de Hola Hola toohost necesario trabajar el conjunto de volúmenes en capas, creación de volúmenes anclados localmente afecta Hola espacio disponible para aprovisionar volúmenes en capas. Por lo tanto, si crea un volumen anclado localmente, se reduce el espacio disponible para la creación de volúmenes en capas. De forma similar, si se crea un volumen en capas, se reduce el espacio disponible de hello para la creación de volúmenes anclados localmente.
      
       Si se aprovisiona un volumen anclado localmente de 8,5 TB (tamaño máximo permitido) en el dispositivo 8100, es que agote todo Hola local el espacio disponible en los dispositivos de Hola. No se puede crear cualquier volumen en capas desde ese punto en adelante, porque no hay ningún espacio local en espacio de trabajo de hello dispositivo toohost Hola de hello en niveles de volumen. Volúmenes en capas existentes también afectan al espacio Hola disponible. Por ejemplo, si tiene un dispositivo 8100 que ya cuenta con volúmenes en capas de aproximadamente 106 TB, solo 4 TB de espacio estarán disponibles para volúmenes anclados localmente.

    6. Hola **hosts conectados** , a continuación, haga clic en la flecha de Hola. 

        ![Hosts conectados](./media/storsimple-8000-create-volume-u2/step5createvol2.png)

    7. Hola **hosts conectados** hoja, seleccione un ACR existente o agregue un nuevo ACR realizando Hola pasos:

       1. Proporcione un **Nombre** para el ACR.
       2. En **nombre del iniciador iSCSI**, proporcionar Hola iSCSI nombre completo (IQN) de su host de Windows. Si no tienes Hola IQN, vaya demasiado[Get hello IQN de un host de Windows Server](#get-the-iqn-of-a-windows-server-host).

    9. Haga clic en **Crear**. Se crea un volumen con hello especificado valores.

        ![Click Create](./media/storsimple-8000-create-volume-u2/step5createvol3.png)

        > [!NOTE]
        > Tenga en cuenta que el volumen de Hola que ha creado aquí no está protegido. Necesitará toocreate y asociar las directivas de copia de seguridad con copias de seguridad de tootake programada de este volumen. 

