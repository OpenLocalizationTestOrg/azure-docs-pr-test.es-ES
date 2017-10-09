

Cuando cree una aplicación web para un sitio web de Azure, puede aprovisionar una máquina virtual en Azure. A continuación, puede configurar la máquina virtual de hello con software adicional o usar máquina virtual de Hola para fines de diagnóstico o de depuración.

toocreate una máquina virtual cuando se crea una aplicación web, siga estos pasos:

1. En Visual Studio, haga clic en **archivo** > **New** > **proyecto** > **Web**y, a continuación, elija **Aplicación Web ASP.NET** (en hello **Visual C#** o **Visual Basic** nodos).
2. Hola **nuevo proyecto ASP.NET** cuadro de diálogo, tipo hello seleccione de la aplicación web que desea y, en hello Azure sección del cuadro de diálogo de hello (en la esquina inferior derecha de hello), asegúrese de que ese hello **Host en la nube de hello**casilla está activada (esta casilla de verificación **crear recursos remotos** en algunas instalaciones).
   
    ![][0]
3. En este ejemplo, en la lista desplegable de hello en Microsoft Azure, elija **Máquina Virtual (v1)**y, a continuación, haga clic en hello **Aceptar** botón.
4. Inicie sesión en tooAzure si se le pide. Hola **crear Máquina Virtual** aparece el cuadro de diálogo.
   
    ![][2]
5. Hola **nombre DNS** cuadro, escriba un nombre para la máquina virtual de Hola. nombre DNS de Hello debe ser único en Azure. Si el nombre de Hola que especificó no está disponible, aparece un signo de exclamación rojo.
6. Hola **imagen** lista, elija la imagen de hello desee máquina virtual de toobase hello en. Puede elegir cualquiera de las imágenes de máquina virtual de Azure estándar de Hola o la imagen que ha cargado tooAzure.
7. Deje hello **habilitar IIS y Web Deploy** casilla activada a menos que piense tooinstall un servidor web diferente. No será capaz de toopublish desde Visual Studio si deshabilita Web Deploy. Puede agregar IIS y Web Deploy tooany de imágenes de Windows Server de hello empaquetado, incluidas sus propias imágenes personalizadas.
8. Hola **tamaño** lista, elija el tamaño de Hola de máquina virtual de Hola.
9. Especificar credenciales de inicio de sesión de Hola para esta máquina virtual. Tome nota de ellas, porque los necesitará tooaccess Hola máquina a través de escritorio remoto.
10. Hola **ubicación** lista, elija la máquina virtual de hello región toohost Hola.
11. Haga clic en hello **Aceptar** toostart botón Crear la máquina virtual de Hola. Puede seguir el progreso de Hola de operación de Hola Hola **salida** ventana.
    
    ![][3]
12. Cuando se aprovisiona la máquina virtual de hello, se crean scripts publicados en un **PublishScripts** nodo de la solución. Hola había publicado script se ejecuta y aprovisiona una máquina virtual en Azure. Hola **salida** ventana muestra el estado de saludo. script de Hola realiza Hola después acciones tooset la máquina virtual de hello:
    
    * Crea la máquina virtual de hello si aún no existe.
    * Crea una cuenta de almacenamiento con un nombre que comienza con `devtest`, pero solo si no ya hay una cuenta de almacenamiento de este tipo en la región especificada de Hola.
    * Crea un servicio de nube como un contenedor para la máquina virtual de Hola y crea un rol web para la aplicación web de hello.
    * Configura Web Deploy en la máquina virtual de Hola.
    * Configura IIS y ASP.NET en la máquina virtual de Hola.
    
    ![][4]
13. (Opcional) Puede conectar la nueva máquina virtual de toohello. En **Explorador de servidores**, expanda hello **máquinas virtuales** nodo, elija el nodo de hello para la máquina virtual de Hola que creó y, en el menú contextual, elija **conectar con Escritorio remoto**. O bien, en **Explorer nube** puede elegir **abrir en el Portal** Hola menú contextual y conectar toohello máquina de virtual no existe.
    
    ![][5]

## <a name="next-steps"></a>Pasos siguientes
Si desea toocustomize Hola publicados scripts que ha creado, leer información más detallada en [entornos de prueba y el uso de Scripts de Windows PowerShell tooPublish tooDev](http://msdn.microsoft.com/library/dn642480.aspx).

[0]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_NewProject.PNG
[1]: ./media/dotnet-visual-studio-create-virtual-machine/CreateVM_SignIn.PNG
[2]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_CreateVM.PNG
[3]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_Provisioning.png
[4]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_SolutionExplorer.png
[5]: ./media/virtual-machines-common-classic-web-app-visual-studio/VS_Create_VM_Connect.png
