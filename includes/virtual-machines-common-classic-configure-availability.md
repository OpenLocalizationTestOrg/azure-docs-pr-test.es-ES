


Un conjunto de disponibilidad ayuda a mantener las máquinas virtuales disponibles durante períodos de inactividad, como por ejemplo mientras se realiza mantenimiento. Colocar dos o más máquinas virtuales configuradas de manera similar en un conjunto de disponibilidad crea Hola redundancia necesitado toomaintain disponibilidad de aplicaciones de Hola o servicios que se ejecuta la máquina virtual. Para obtener más información acerca de cómo funciona esto, consulte [administrar Hola disponibilidad de máquinas virtuales][Manage hello availability of virtual machines].

Es una mejor toouse práctica conjuntos de disponibilidad y equilibrio de carga extremos toohelp aseguran de que la aplicación está siempre disponible y se ejecuta eficazmente. Para obtener información detallada acerca de los puntos de conexión de carga equilibrada, consulte [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services] (Equilibrio de carga en los servicios de infraestructura de Azure).

Puede agregar máquinas virtuales clásicas en un conjunto de disponibilidad mediante una de estas dos opciones:

* [Opción 1: Crear una máquina virtual y un conjunto de disponibilidad en hello mismo tiempo][Option 1: Create a virtual machine and an availability set at hello same time]. A continuación, agregue nuevas toohello de máquinas virtuales configurada al crear las máquinas virtuales.
* [Opción 2: Agregar un conjunto de disponibilidad de tooan de máquina virtual existente][Option 2: Add an existing virtual machine tooan availability set].

> [!NOTE]
> En el modelo clásico de hello, máquinas virtuales que desea tooput en Hola mismo conjunto de disponibilidad debe pertenecer toohello mismo servicio en la nube.
> 
> 

## <a id="createset"></a>Opción 1: crear una máquina virtual y un conjunto de disponibilidad en hello mismo tiempo
Puede usar cualquier Hola portal de Azure o Azure PowerShell comandos toodo esto.

Hola toouse portal de Azure:

1. Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **+ nuevo**y, a continuación, haga clic en **Máquina Virtual**.
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. Seleccione la imagen de máquina virtual de Marketplace de hello desea toouse. Puede elegir toocreate una máquina virtual Linux o Windows.
4. Para hello selecciona máquina virtual, compruebe que ese modelo de implementación de Hola se establece demasiado**clásico** y, a continuación, haga clic en **crear**
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. Escriba un nombre de máquina virtual, un nombre de usuario y una contraseña (para máquinas con Windows) o la clave pública SSH (para equipos con Linux). 
6. Elija el tamaño de la máquina virtual de hello y, a continuación, haga clic en **seleccione** toocontinue.
7. Elija **configuración opcional > conjunto de disponibilidad**y seleccione el conjunto de disponibilidad de hello desea tooadd Hola máquina virtual.
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. Revise las opciones de configuración. Cuando haya terminado, haga clic en **Crear**.
9. Mientras Azure crea la máquina virtual, puede seguir el progreso de hello en **máquinas virtuales** en el menú del concentrador de Hola.

toouse Azure PowerShell comandos toocreate una máquina virtual de Azure y Agregar conjunto de disponibilidad nuevo o existente de tooa, consulte [toocreate usar Azure PowerShell y preconfigurar máquinas virtuales basadas en Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>Opción 2: agregar un conjunto de disponibilidad de tooan de máquina virtual existente
Hola portal de Azure, puede agregar existente tooan de máquinas virtuales clásicas existente conjunto de disponibilidad o cree uno nuevo para ellos. (Tenga en cuenta que las máquinas virtuales de hello en Hola mismo conjunto de disponibilidad debe pertenecer toohello mismo servicio en la nube.) pasos de Hello son casi Hola mismo. Con Azure PowerShell, puede agregar conjunto de disponibilidad existente de tooan de máquina virtual de Hola.

1. Si no lo ha hecho ya, inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **máquinas virtuales (clásicas)**.
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. En lista de Hola de máquinas virtuales, seleccione el nombre de Hola de máquina virtual de Hola que desee tooadd toohello establecer.
4. Elija **conjunto de disponibilidad** de la máquina virtual de hello **configuración**.
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. Seleccione conjunto de disponibilidad de hello que desea tooadd Hola máquina virtual. máquina virtual de Hello debe pertenecer toohello mismo servicio en la nube como conjunto de disponibilidad de Hola.
   
    ![Texto alternativo de imagen](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. Haga clic en **Guardar**.

comandos de PowerShell de Azure toouse, abra una sesión de PowerShell de Azure de nivel de administrador y ejecute el siguiente comando de Hola. Para los marcadores de posición de hello (como &lt;VmCloudServiceName&gt;), reemplace todo el contenido de las comillas de hello, incluidos los caracteres de Hola < y >, con hello corregir nombres.

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> máquina virtual de Hello podría tener toofinish toobe reinicia Agregar conjunto de disponibilidad toohello.
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

