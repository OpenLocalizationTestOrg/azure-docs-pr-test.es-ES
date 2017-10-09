#### <a name="toocreate-a-virtual-device"></a>toocreate un dispositivo virtual
1. Hola portal de Azure, vaya toohello **StorSimple Manager** servicio.
2. Vaya toohello **dispositivos** página. Haga clic en **dispositivo virtual crear** final Hola de hello **dispositivos** página.
3. Hola **cuadro de diálogo Crear un dispositivo Virtual**, especifique Hola detalles siguientes.
   
    ![Crear dispositivo virtual de StorSimple](./media/storsimple-create-virtual-device-u2/CreatePremiumsva1.png)
   
   1. **Nombre** : un nombre único para el dispositivo virtual.
   2. **Modelo** -elegir modelo hello de dispositivo virtual Hola. Este campo se muestra solo si se ejecuta Update 2 o posterior. Un modelo de dispositivo 8010 ofrece 30 TB de almacenamiento estándar, mientras que 8020 tiene 64 TB de almacenamiento premium. Especifique 8010
   3. escenarios de recuperación de nivel de elemento toodeploy desde copias de seguridad. Seleccione 8020 toodeploy alto rendimiento, poca las cargas de trabajo de latencia o usar como un dispositivo secundario para la recuperación ante desastres.
   4. **Versión** -Elegir versión de hello de dispositivo virtual Hola. Si se selecciona un modelo de dispositivo 8020, a continuación, campo de versión de hello no se ofrecerá toohello usuario. Esta opción no está presente si Hola físico todos los dispositivos registrados con este servicio están ejecutando Update 1 (o posterior). Este campo se muestra solo si tiene una mezcla de anteriores a la actualización 1 y 1 de las actualizaciones de dispositivos físicos registrados con Hola mismo servicio. Dada Hola versión del dispositivo virtual Hola determinará qué dispositivo físico puede conmutación por error o un clon de, es importante que cree una versión adecuada del dispositivo virtual Hola. Seleccione:
      
      * Versión Update 0.3 si conmuta por error o efectúa una recuperación ante desastres a partir de un dispositivo físico que ejecuta Update 0.3 o una versión anterior. 
      * Versión Update 1 si conmuta por error o efectúa una clonación a partir de un dispositivo físico que ejecuta Update 1 (o una versión posterior). 
   5. **Red virtual** : especifique una red virtual que desee toouse con este dispositivo virtual. Si usa el almacenamiento Premium (Update 2 o posterior), debe seleccionar una red virtual que es compatible con hello cuenta de almacenamiento Premium. Hola no admitida las redes virtuales se atenuará en la lista desplegable de Hola. Se le avisará si selecciona una red virtual no compatible. 
   6. **Cuenta de almacenamiento para crear un dispositivo Virtual** : seleccione una imagen de hello toohold de cuenta de almacenamiento del dispositivo virtual de Hola durante el aprovisionamiento. Esta cuenta de almacenamiento debe encontrarse en hello misma región que el dispositivo virtual de Hola y la red virtual. No debe usarse para el almacenamiento de datos por hello físico o dispositivo virtual Hola. De forma predeterminada, para ello se creará una nueva cuenta de almacenamiento. Sin embargo, si sabe que ya tiene una cuenta de almacenamiento que sea adecuada para este uso, puede seleccionar en lista de Hola. Si crea un dispositivo virtual premium, lista desplegable de Hola solo mostrará las cuentas de almacenamiento Premium. 
      
      > [!NOTE]
      > dispositivo virtual Hola sólo puede trabajar con cuentas de almacenamiento de Azure de Hola. No se admiten otros proveedores de servicios de nube, como Amazon y HP, OpenStack (que son compatibles con el dispositivo físico de hello) para el dispositivo virtual StorSimple Hola.
      > 
      > 
   7. Haga clic en tooindicate de marca de verificación de Hola que entender que datos de hello almacenados en el dispositivo virtual Hola se hospedará en un centro de datos de Microsoft. Cuando se utiliza solo un dispositivo físico, la clave de cifrado se mantiene con el dispositivo; por lo tanto, Microsoft no podrá descifrarla. 
      
       Cuando se usa un dispositivo virtual, las claves de cifrado de Hola y Hola descifrado se almacenan en Microsoft Azure. Para obtener más información, revise las [consideraciones de seguridad para utilizar un dispositivo virtual](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Haga clic en el dispositivo virtual de hello comprobación icono toocreate Hola. dispositivo de Hello puede tardar unos 30 toobe minutos aprovisionado.
      
      ![Fase de creación de dispositivo virtual de StorSimple](./media/storsimple-create-virtual-device-u2/StorSimple_VirtualDeviceCreating1M.png)

