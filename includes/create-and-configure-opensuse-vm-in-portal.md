1. Inicie sesión en toohello [portal de Azure clásico](http://manage.windowsazure.com).  
2. En la barra de comandos de hello en parte inferior de Hola de ventana hello, haga clic en **nuevo**.
3. En **Proceso**, haga clic en **Máquina virtual** y, después, en **De la galería**.
   
    ![Crear una máquina virtual][Image1]
4. En hello **SUSE** grupo, seleccione una imagen de máquina virtual de OpenSUSE y, a continuación, haga clic en hello flecha toocontinue.
5. En hello primera **configuración de máquina Virtual** página:
   
   * Escriba un **nombre de máquina virtual**, como "testlinuxvm". Hola nombre debe contener entre 3 y 15 caracteres, puede contener solo letras, números y guiones y debe empezar por una letra y terminar por una letra o un número.
   * Comprobar hello **capa** y elegir un **tamaño**. nivel de Hello determina puede elegir entre los tamaños de Hola. Hola tamaño afecta a Hola costo de utilizarlo, así como opciones de configuración como el número de discos de datos se puede adjuntar. Para obtener más información, consulte [Tamaños de máquinas virtuales](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
   * Escriba un **nuevo nombre de usuario**, o acepte el valor predeterminado de hello, **azureuser**. Este nombre se agrega el archivo de lista de toohello Sudoers.
   * Decidir qué tipo de **autenticación** toouse. Para obtener instrucciones generales sobre contraseñas, consulte [Contraseñas seguras](http://msdn.microsoft.com/library/ms161962.aspx).
6. En hello siguiente **configuración de máquina Virtual** página:
   
   * Usar valor predeterminado de hello **crear un nuevo servicio de nube**.
   * Hola **nombre DNS** , escriba un único toouse de nombre DNS como parte de la dirección de hello, como "testlinuxvm".
   * Hola **afinidad región/grupo/red Virtual** , seleccione una región donde se hospedará esta imagen virtual.
   * En **extremos**, mantener el punto de conexión de hello SSH. Puede agregar otros ahora, o agregar, cambiar o eliminarlos una vez creada la máquina virtual de Hola.
     
     > [!NOTE]
     > Si desea que un toouse de máquina virtual una red virtual, se **debe** especificar la red virtual de hello cuando se crea la máquina virtual de Hola. No se puede agregar una red virtual de tooa de máquina virtual después de crear la máquina virtual de Hola. Para más información, consulte [Información general sobre Virtual Network](../articles/virtual-network/virtual-networks-overview.md).
     > 
     > 
7. En hello última **configuración de máquina Virtual** página, mantener la configuración predeterminada de hello y, a continuación, haga clic en hello toofinish de marca de verificación.

portal de Hello indica Hola nueva máquina virtual en **máquinas virtuales**. Mientras se notifica el estado de hello como **(aprovisionamiento)**, máquina virtual de saludo se está configurando. Cuando se notifica el estado de hello como **ejecuta**, puede mover en toohello siguiente paso.

## <a name="connect-toohello-virtual-machine"></a>Conectar toohello Máquina Virtual
Empleará SSH o PuTTY tooconnect toohello máquina virtual, función de sistema operativo de hello en equipo Hola que se conectará desde:

* Desde un equipo que ejecuta Linux, use SSH. En hello símbolo del sistema, escriba:
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    Escriba la contraseña del usuario de Hola.
* Desde un equipo que ejecute Linux, use PuTTY. Si no lo tiene instalado, puede descargarlo en hello [página de descargas de PuTTY][PuTTYDownload].
  
    Guardar **putty.exe** tooa directorio en el equipo. Abra un símbolo del sistema, navegue toothat carpeta y ejecute **putty.exe**.
  
    Escriba el nombre de host de hello, como "testlinuxvm.cloudapp.net" y "22" para hello **puerto**.
  
    ![Pantalla de PuTTY][Image6]  

## <a name="update-hello-virtual-machine-optional"></a>Actualizar Hola Máquina Virtual (opcional)
1. Una vez que esté conectado toohello virtual machine, puede opcionalmente instalar las actualizaciones del sistema y las revisiones. actualización de hello toorun, tipo:
   
    `$ sudo zypper update`
2. Seleccione **Software**, a continuación, **actualización en línea** las actualizaciones disponibles de toolist. Seleccione **Accept** toostart Hola instalación y aplicar todas las revisiones disponibles nueva (excepto Hola los opcionales).
3. Una vez completada la instalación, seleccione **Finalizar**.  El sistema ya está listo toodate.

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
