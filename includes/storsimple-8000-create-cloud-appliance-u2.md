#### <a name="toocreate-a-cloud-appliance"></a>toocreate un dispositivo de nube

1. Hola portal de Azure, vaya toohello **el Administrador de dispositivos de StorSimple** servicio.
2. Vaya toohello **dispositivos** hoja. En la barra de comandos de hello en la hoja de resumen de servicio de hello, haga clic en **dispositivo de nube crear**.
    ![Creación de dispositivo de nube de StorSimple](./media/storsimple-8000-create-cloud-appliance-u2/sca-create1.png)
3. Hola **crear dispositivo de nube** hoja, especifique Hola detalles siguientes.
   
    ![Creación de dispositivo de nube de StorSimple](./media/storsimple-8000-create-cloud-appliance-u2/sca-create2m.png)
   
   1. **Nombre**: un nombre único para la aplicación de nube.
   2. **Modelo** -elegir modelo hello de dispositivo de hello en la nube. Un dispositivo 8010 ofrece 30 TB de Standard Storage, mientras que 8020 tiene 64 TB de Premium Storage. Especifique 8010 escenarios de recuperación de nivel de elemento toodeploy desde copias de seguridad. Seleccione 8020 toodeploy a alto rendimiento, las cargas de trabajo de baja latencia, o utilice como un dispositivo secundario para la recuperación ante desastres.
   3. **Versión** -Elegir versión de hello de dispositivo de hello en la nube. versión de Hola corresponde toohello versión de imagen de disco virtual de Hola que es usado toocreate Hola nube dispositivo. Versión de Hola de nube de hello especificadas dispositivo determina qué física dispositivo conmutación por error o clonarlo a partir de, es importante que cree una versión adecuada del dispositivo de hello en la nube.
   4. **Red virtual** : especifique una red virtual que desee toouse con este dispositivo en la nube. Si usa el almacenamiento Premium, debe seleccionar una red virtual que es compatible con hello cuenta de almacenamiento Premium. Hola no admitida las redes virtuales están deshabilitadas en la lista desplegable de Hola. Se le avisará si selecciona una red virtual no compatible.
   5. **Subred** -en función de la red virtual de hello seleccionado, lista desplegable de hello muestra subredes Hola asociado. Asignar un dispositivo de nube de tooyour de subred.
   6. **Cuenta de almacenamiento** : seleccione una imagen de hello toohold de cuenta de almacenamiento del dispositivo en la nube de Hola durante el aprovisionamiento. Esta cuenta de almacenamiento debe encontrarse en hello misma región que el dispositivo de hello en la nube y la red virtual. No debe usarse para el almacenamiento de datos Hola físico o dispositivo de hello en la nube. De forma predeterminada, para ello se crea una nueva cuenta de almacenamiento. Sin embargo, si sabe que ya tiene una cuenta de almacenamiento que sea adecuada para este uso, puede seleccionar en lista de Hola. Si crea un dispositivo de nube premium, lista desplegable de hello muestra solo cuentas de almacenamiento Premium.
      
      > [!NOTE]
      > dispositivo de Hello en la nube solo puede trabajar con cuentas de almacenamiento de Azure de Hola.
    
   7. Seleccione tooindicate de casilla de verificación de Hola que entender que los datos de hello almacenados en el dispositivo de hello en la nube se hospedan en un centro de datos de Microsoft.
       * Cuando se utiliza solo un dispositivo físico, la clave de cifrado se mantiene con el dispositivo; por lo tanto, Microsoft no podrá descifrarla.

       * Cuando se usa un dispositivo de nube, las claves de cifrado de Hola y Hola descifrado se almacenan en Microsoft Azure. Para más información, consulte las [consideraciones de seguridad para utilizar una aplicación en la nube](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Haga clic en **crear** dispositivo de tooprovision hello en la nube. dispositivo de Hello puede tardar unos 30 toobe minutos aprovisionado. Se le notificará al dispositivo de hello en la nube se creó correctamente. Vaya tooDevices hoja y actualiza la lista Hola de dispositivos aparato de nube de hello toodisplay. estado de Hello de dispositivo de hello es **listo tooset seguridad**.
      
      ![Dispositivo de StorSimple en la nube listo tooset seguridad](./media/storsimple-8000-create-cloud-appliance-u2/sca-create3.png)

