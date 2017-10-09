En Azure se pueden crear máquinas virtuales desde el Explorador de servidores en Visual Studio.

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>Creación de una máquina virtual de Azure en el Explorador de servidores
Si bien puede crear una máquina virtual en hello [Portal de administración de Azure](http://go.microsoft.com/fwlink/?LinkID=253103), también puede crear una máquina virtual en Azure mediante comandos en el Explorador de servidores. Máquinas virtuales se pueden utilizar, por ejemplo, tooprovide un front end detrás de un extremo público con equilibrio de carga comunes.

### <a name="toocreate-a-new-virtual-machine"></a>toocreate una nueva máquina virtual
1. En el Explorador de servidores, abra hello **Azure** nodo y haga clic en **máquinas virtuales**.
2. En el menú contextual de hello, haga clic en **crear Máquina Virtual**.
   
    Hola **crear una nueva máquina Virtual** aparece el Asistente para.
   
    ![Hola comando Crear Máquina Virtual](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. En hello **elegir una suscripción** , seleccione una suscripción toouse al crear la máquina virtual de hello y, a continuación, haga clic en **siguiente**.
   
    Si no has iniciado sesión en tooAzure, haga clic en **inicio de sesión** toosign en. A continuación, seleccione la suscripción de Azure en el cuadro de lista desplegable de hello si aún no está seleccionada.
4. En hello **seleccionar una imagen de máquina Virtual** , seleccione un tipo de imagen en hello **tipo de imagen** cuadro de lista desplegable y, a continuación, seleccione una imagen de máquina virtual en hello **nombre de la imagen** cuadro de lista. Cuando haya terminado, haga clic en **Siguiente**.
   
    ![Seleccionar una página de imágenes de máquinas virtuales](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    Puede elegir Hola siguientes tipos de imagen.
   
   * **Imágenes públicas** enumera las imágenes de máquinas virtuales de sistemas operativos y software de servidores, como Windows Server y SQL Server.
   * **Imágenes de MSDN** enumera las imágenes de máquina virtual de los suscriptores de tooMSDN disponibles de software, como Visual Studio y Microsoft Dynamics.
   * **Imágenes privadas** enumera imágenes que ha creado de máquinas virtuales especializadas y generalizadas.
     
     toolearn aproximadamente especializadas y generalizadas máquinas virtuales, consulte [imagen de máquina virtual](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/). Vea [cómo tooCapture una tooUse de máquina Virtual de Windows como una plantilla de](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) para obtener información acerca de cómo tooturn una máquina virtual en una plantilla que puede utilizar tooquickly crear nuevas máquinas virtuales preconfiguradas.
     
     Puede hacer clic en una máquina virtual imagen nombre toosee información sobre imágenes de hello en el lado derecho de Hola de hello página.
     
     > [!NOTE]
     > No se puede agregar toohello de imágenes de máquina virtual **imágenes públicas** o **imágenes de MSDN** muestra porque son de solo lectura. Todas las máquinas virtuales que cree se agregan toohello **imágenes privadas** lista.
     > 
     > 
     
     Si es suscriptor de MSDN con una suscripción de nivel de Visual Studio, puede crear una máquina virtual de Azure pregenerada que contenga Visual Studio, así como otras imágenes. Para más información, consulte [Create a Virtual Machine in Visual Studio by Using Images Visual Studio 2013 Gallery image for MSDN subscribers (Creación de una máquina virtual en Visual Studio mediante imágenes de la galería de imágenes de Visual Studio 2013 para suscriptores de MSDN)](http://visualstudio2013msdngalleryimage.azurewebsites.net) y [Suscripciones a MSDN](https://www.visualstudio.com/products/msdn-subscriptions-vs).|
5. En hello **configuración básica de máquina Virtual** página, escriba un nombre de equipo y, a continuación, agregar especificaciones de hello para la máquina virtual de hello, incluido el tamaño de hello y un nombre de usuario y una contraseña. Cuando haya terminado, haga clic en **Siguiente**.
   
    Deberá usar el nuevo nombre de Hola y toolog de contraseña en la máquina de hello mediante Escritorio remoto, por lo que es un toowrite buena idea ellos hacia abajo en caso omitir. Después de crear una máquina virtual de Azure en Visual Studio, puede cambiar su tamaño y otras configuraciones de hello [Portal de administración de Azure](http://go.microsoft.com/fwlink/?LinkID=253103).
   
   > [!NOTE]
   > Si elige tamaños mayores de máquina virtual de hello, se pueden aplicar cargos adicionales. Para obtener más información, consulte [Detalles de precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/) .
   > 
   > 
6. Las máquinas virtuales creadas en Visual Studio requieren un servicio en la nube. En hello **configuración de servicio de nube** página, seleccione un servicio de nube para la máquina virtual de Hola o haga clic en **< crear nuevo... >** en lista de desplegable Hola si aún no tiene una nube de servicio o desea toouse un nuevo uno. También se requiere una cuenta de almacenamiento, por lo que elija una cuenta de almacenamiento (o crear una nueva cuenta de almacenamiento) en hello **cuenta de almacenamiento** cuadro de lista desplegable. Vea [Introducción tooMicrosoft almacenamiento de Azure](../articles/storage/common/storage-introduction.md) para obtener más información.
7. Si desea toospecify una red virtual (que es opcional), selecciónelo en los cuadros de lista de desplegable de red Virtual y subred Hola.
   
    Máquinas virtuales que son miembros de un conjunto de disponibilidad son dominios de error toodifferent implementado. Para obtener más información, consulte [Red virtual de Azure](https://azure.microsoft.com/services/virtual-network/) .
8. Si desea que el conjunto de disponibilidad de máquinas virtuales toobelong tooan (también opcional), seleccione hello **especificar un conjunto de disponibilidad** casilla de verificación y, a continuación, elija un conjunto en el cuadro de lista desplegable de Hola de disponibilidad. Cuando haya terminado, elija hello **siguiente** botón.
   
    Agregar la máquina virtual tooan conjunto de disponibilidad facilita que la aplicación siga estando disponible cuando los errores de red, errores de hardware de disco local y cualquier tiempo de inactividad planeado. Necesita hello toouse [Portal de administración de Azure](http://go.microsoft.com/fwlink/?LinkID=253103) establece toocreate las redes virtuales, subredes y disponibilidad. Vea [administrar Hola disponibilidad de las máquinas virtuales](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/) para obtener más información.
9. En hello **extremos** página, especifique los extremos públicos de Hola que desea toousers disponible de la máquina virtual. Por ejemplo, puede elegir tooenable HTTP (puerto 80) además toohello escritorio remoto y PowerShell puntos de conexión, que están habilitadas de forma predeterminada. tooadd un extremo, elija uno en hello **nombre de puerto** lista desplegable del cuadro de lista y, a continuación, elija hello **agregar** botón. tooremove un extremo, elija Hola rojo **X** siguiente nombre toohello en la lista de puntos de conexión de Hola.
   
    ![página extremos de Hello en el Asistente de máquinas virtuales de Hola.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    los puntos de conexión de Hola que están disponibles dependen de servicio de nube de Hola que seleccionó para la máquina virtual. Para obtener más información, consulte [Extremos de servicio de Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) .
   
   > [!NOTE]
   > Habilitación de extremos públicos hace que los servicios en su toohello disponibles de máquina virtual internet. Ser tooinstall seguro y configurar correctamente los extremos de Hola y servicios en la máquina virtual, como control de acceso (ACL) enumera para extremos de Hola. Vea [cómo tooSet extremos tooa Máquina Virtual](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) para obtener más información.
   > 
   > 
10. Cuando haya terminado la configuración de máquina virtual de hello, elija hello **crear** máquina virtual de botón toocreate Hola.
    
     Hola a medida que Azure crea la máquina virtual de hello, **Azure Activity Log** muestra Hola progreso de la operación de creación de máquina virtual de Hola.
    
     ![Registro de actividad de máquina virtual: en curso.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     información de máquina virtual solo tooview, elija hello **máquinas virtuales** ficha hello **Azure Activity Log**.
    
     ![Registro de actividad de máquina virtual: completado.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     Si finaliza correctamente la operación de hello, nueva máquina virtual de hello aparece bajo hello **máquinas virtuales** nodo en el Explorador de servidores. Puede iniciar sesión en él, haga clic en hello **conectar utilizando Escritorio remoto** acceso directo.
    
     ![Máquina virtual que aparece en el Explorador de servidores.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>Administración de máquinas virtuales
En la página de configuración de máquina virtual de hello, además tooshutting hacia abajo, conectar, actualizar y adición de puntos de control toohello seleccionan máquina virtual, también puede ver o cambiar la configuración de máquina virtual de Hola. Puede:

* Cambiar tamaño de la máquina virtual de Hola.
* Toouse con la máquina virtual de Hola de conjunto de disponibilidad de hello SELECT.
* Agregar, quitar o cambiar la configuración de extremos públicos.
* Agregar, quitar o configurar las extensiones de la máquina virtual.
* Ver información acerca de los discos de hello asociado a la máquina virtual de Hola.

### <a name="view-or-change-virtual-machine-settings"></a>Visualización o cambio de la configuración de la máquina virtual
1. En el Explorador de servidores, elija la máquina virtual de hello **máquinas virtuales de Azure** nodo.
2. En el menú contextual de hello, elija **configurar** página de configuración de máquina virtual de tooview Hola.
   
    ![página de configuración de máquina virtual de Azure Hola](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. Ver información de la máquina virtual de Hola o cambiarlo.

### <a name="save-or-restore-hello-status-of-your-virtual-machine"></a>Guardar o restaurar el estado de saludo de la máquina virtual
Como configurar la máquina virtual e instalar software en él, es un tooregularly conveniente guardar el progreso mediante la creación de puntos de control de máquina virtual. Un punto de comprobación es una imagen del estado actual de hello de la máquina virtual o instantánea. Si algo va mal con la máquina virtual de hello, o si desea tooreconfigure Hola virtual machine, puede ahorrar tiempo mediante la restauración de estado de punto de comprobación anterior tooa en lugar de comenzar desde cero.

### <a name="toocreate-a-virtual-machine-checkpoint"></a>toocreate un punto de control de máquina virtual
1. En el Explorador de servidores, elija la máquina virtual de hello **máquinas virtuales de Azure** nodo.
2. En el menú contextual de hello, elija **configurar** página de configuración de máquina virtual de tooview Hola.
3. En la página de configuración de hello, elija hello **Capturar imagen** botón.
   
    ![Botón de captura de página de configuración de Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    Hola **capturar Máquina Virtual** aparece el cuadro de diálogo.
   
    ![Cuadro de diálogo de máquina virtual de captura de Azure.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. Especifique una etiqueta y una descripción de la imagen. Aparecen una etiqueta y una descripción predeterminadas, pero puede sobrescribirlas si lo desea.
5. Si ya ha ejecutado Sysprep en esta máquina virtual, seleccione hello **he ejecutado Sysprep en la máquina virtual de hello** cuadro.
   
    Sysprep es una herramienta que, entre otras cosas, quita los datos específicos de los sistemas de versión de Hola la máquina virtual de Windows, lo que plantilla que otros usuarios pueden usar. Vea [cómo tooCapture una tooUse de máquina Virtual de Windows como una plantilla de](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) para obtener más información. Respaldar Hola VM antes de ejecutar Sysprep.
6. Cuando haya terminado la configuración de captura de hello, elija hello **capturar** el punto de control de botón toocreate Hola.
   
    Hola a medida que Azure crea el punto de control de hello, **Azure Activity Log** muestra Hola progreso de la operación de Hola.
   
    ![Captura de un punto de control en una máquina virtual](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Cuando se completa la operación de punto de comprobación de hello, lo verá en hello **Azure Activity Log**.
   
    ![Operación de punto de control completada](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="toomanage-virtual-machine-checkpoints"></a>puntos de control de máquina virtual de toomanage
### <a name="toorestore-a-virtual-machine-tooa-previously-saved-state"></a>estado previamente guardado de toorestore tooa de una máquina virtual
* Siga los pasos de hello descritos en [paso a paso: realizar en la nube restaura de Microsoft Azure máquinas virtuales con PowerShell - parte 2](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx).

### <a name="toodelete-a-checkpoint"></a>toodelete un punto de control
1. Vaya toohello [Portal de administración de Azure](http://go.microsoft.com/fwlink/?LinkID=253103).
2. En la página de configuración de máquina virtual de hello, elija hello **imágenes** ficha situada en la parte superior de Hola de página de Hola.
3. Elija el punto de control de Hola que desee toodelete y, a continuación, elija hello **eliminar** situado en la parte inferior de Hola de página de Hola.

## <a name="shut-down-your-virtual-machine"></a>Apague la máquina virtual.
1. En el Explorador de servidores, elija Hola máquina virtual tooshut hacia abajo en hello **máquinas virtuales de Azure** nodo.
2. En el menú contextual de hello, elija hello **apagado** comando o elija **configurar** tooview Hola página de configuración de máquina virtual y, a continuación, elija hello **apagado**botón.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la creación de máquinas virtuales, consulte [crear una máquina Virtual ejecuta Linux](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) y [crear una máquina virtual que ejecuta Windows en el portal de vista previa de hello](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

