<!--author=alkohli last changed: 08/16/2016-->

#### <a name="toocreate-a-volume"></a>toocreate un volumen
1. En el dispositivo de hello **inicio rápido** página, haga clic en **agregar un volumen** toostart Hola asistente Agregar un volumen.
2. Hola, agregar un asistente de volumen, en **configuración básica**:
   
   1. Escriba un **Nombre** para el volumen.
   2. En la lista desplegable de hello, seleccione hello **tipo de uso** para su volumen. Para cargas de trabajo que requieren garantías locales, latencias bajas y un rendimiento más alto, seleccione un volumen **Localmente anclado** . Para todos los demás datos, seleccione un volumen **En capas** . Si usa este volumen para datos de archivo, seleccione **Usar este volumen para los datos de archivo a los que accede con menos frecuencia**. 
      
       Un volumen anclado localmente se realiza un aprovisionamiento grueso y asegura que los datos principal de hello en volumen de hello permanece dispositivo toohello local y no volcarse toohello en la nube.  Si crea un volumen anclado localmente, comprobación de espacio disponible en los niveles de hello local dispositivo de hello tooprovision volumen de Hola de hello tamaño solicitado. operación Hola de creación de un volumen anclado localmente puede implicar verter los datos existentes de la nube de toohello de dispositivo de Hola y Hola tomadas el volumen de hello toocreate puede ser largo. tiempo total de Hello depende de tamaño de hello del volumen de hello aprovisionado, el ancho de banda de red disponible y datos de hello en el dispositivo. 
      
       Un volumen en capas se aprovisiona de manera fina y se puede crear rápidamente. Seleccionar **usar este volumen de datos acceso menos frecuente archivados** volumen en capas destinado a los datos de archivo cambios tamaño del fragmento de desduplicación de Hola para su volumen too512 KB. Si este campo no está activado, volumen en capas correspondiente de hello usa un tamaño de fragmento de 64 KB. Un tamaño de fragmento de desduplicación permite la transferencia de hello tooexpedite hello de dispositivo de nube de toohello de los datos de archivo grande.
   3. Especificar hello **capacidad aprovisionada** para su volumen. Tome nota de la capacidad de Hola que está disponible en función de tipo de volumen de hello seleccionado. Hola especifica el tamaño del volumen no debe superar el espacio disponible de Hola.
      
       Puede aprovisionar volúmenes en capas hasta too200 TB en dispositivo 8100 Hola o volúmenes anclados localmente una too8.5 TB. En el dispositivo 8600 mayor de hello, puede aprovisionar volúmenes anclados localmente una too22.5 TB o volúmenes en capas hasta too500 TB. Que haya espacio local en el dispositivo de Hola Hola toohost necesario trabajar el conjunto de volúmenes en capas, creación de volúmenes anclados localmente afecta Hola espacio disponible para aprovisionar volúmenes en capas. Por lo tanto, si crea un volumen anclado localmente, se reducirá el espacio disponible para la creación de volúmenes en capas. De forma similar, si se crea un volumen en capas, se reduce el espacio disponible de hello para la creación de volúmenes anclados localmente.
      
       Si se aprovisiona un volumen anclado localmente de 8,5 TB (tamaño máximo permitido) en el dispositivo 8100, es que agote todo Hola local el espacio disponible en los dispositivos de Hola. Es posible no que pueda toocreate cualquier volumen en capas de que el punto en adelante, porque no hay no está ningún espacio local en el espacio de trabajo de hello dispositivo toohost Hola de hello interconectado volumen. Volúmenes en capas existentes también afectan al espacio Hola disponible. Por ejemplo, si tiene un dispositivo 8100 que ya cuenta con volúmenes en capas de aproximadamente 106 TB, solo 4 TB de espacio estarán disponibles para volúmenes anclados localmente.
      
       Hello siguiente imagen muestra hello **configuración básica** cuadro de diálogo para un volumen anclado localmente.
      
        ![Agregar volumen local](./media/storsimple-create-volume-u2/add-local-volume-include.png)
      
       Hello siguiente imagen muestra hello **configuración básica** cuadro de diálogo para un volumen en capas.
      
        ![Agregar volumen local](./media/storsimple-create-volume-u2/add-tiered-volume-include.png)
   
   1. Haga clic en el icono de flecha de Hola ![icono de flecha](./media/storsimple-create-volume-u2/HCS_ArrowIcon-include.png) página siguiente de toogo toohello.
3. Hola **configuración adicional** cuadro de diálogo Agregar un nuevo registro de control de acceso (ACR):
   
   1. Proporcione un **Nombre** para el ACR.
   2. En **nombre del iniciador iSCSI**, proporcionar Hola iSCSI nombre completo (IQN) de su host de Windows. Si no tienes Hola IQN, vaya demasiado[Get hello IQN de un host de Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. En **copia de seguridad predeterminado para este volumen?**, seleccione hello **habilitar** casilla de verificación. copia de seguridad de Hello predeterminado crea una directiva que se ejecute a las 22:30 cada día (hora del dispositivo) y crea una instantánea en la nube de este volumen.
      
      > [!NOTE]
      > Una vez habilitada la copia de seguridad de hello, no se puede revertir. Debe tooedit Hola volumen toomodify esta configuración.
      > 
      > 
      
      ![Agregar volumen](./media/storsimple-create-volume-u2/AddVolumeAdditionalSettings1.png)
4. Haga clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-create-volume-u2/HCS_CheckIcon-include.png). Se crea un volumen con hello especificado valores.

