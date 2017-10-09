1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. A partir de la parte superior izquierda de hello, haga clic en **nuevo > proceso > Centro de datos de Windows Server 2016**.

    ![Navegue toohello imágenes de máquina virtual de Azure en el portal de Hola](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. En Windows Server 2016 Datacenter hello, seleccione el modelo de implementación de clásico de Hola. Haga clic en Crear.

    ![Captura de pantalla que muestra las imágenes de máquina virtual de Azure de hello disponibles en el portal de Hola](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a>1. Hoja Básico

hoja de conceptos básicos de Hello solicita la información administrativa para la máquina virtual de Hola.

1. Escriba un **nombre** para la máquina virtual de Hola. En el ejemplo de Hola, _HeroVM_ es Hola nombre de máquina virtual de Hola. nombre de Hello debe ser 1 y 15 caracteres y no puede contener caracteres especiales.

2. Escriba un **nombre de usuario** y una gran **contraseña** que están toocreate usa una cuenta local en hello máquina virtual. Hello cuenta local se usa toosign en tooand administrar Hola máquina virtual. En el ejemplo de Hola, _azureuser_ es el nombre de usuario de Hola.

 Hello contraseña debe tener 8-123 caracteres de longitud y satisfacer tres de hello cuatro requisitos de complejidad: caracteres de una minúscula, una letra mayúscula, un número y un carácter especial. Obtenga más información acerca de los [requisitos de usuario y la contraseña](../articles/virtual-machines/windows/faq.md).

3. Hola **suscripción** es opcional. Una configuración común es "Pago por uso".

4. Seleccione una existente **grupo de recursos** o nombre de tipo hello para uno nuevo. En el ejemplo de Hola, _HeroVMRG_ es nombre Hola Hola del grupo de recursos.

5. Seleccione un centro de datos Azure **ubicación** donde desea Hola VM toorun. En el ejemplo de Hola, **UU** es Hola ubicación.

6. Cuando haya terminado, haga clic en **siguiente** toocontinue toohello siguiente hoja.

    ![Captura de pantalla que muestra la configuración de hello en la hoja de hello conceptos básicos para configurar una máquina virtual de Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a>2. Hoja Tamaño

hoja de tamaño de Hola identifica los detalles de configuración de Hola de hello VM y enumera las distintas opciones que incluyen el sistema operativo, número de procesadores, el tipo de almacenamiento en disco y costos de uso mensual estimado.  

Elija un tamaño de máquina virtual y, a continuación, haga clic en **seleccione** toocontinue. En este ejemplo, _DS1_\__V2 estándar_ es el tamaño de la máquina virtual de Hola.

  ![Captura de pantalla de hoja de tamaño de Hola que muestra hello tamaños de máquina virtual de Azure que se pueden seleccionar](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a>3. Hoja Configuración

hoja de configuración de Hello solicita opciones de almacenamiento y red. Puede aceptar la configuración predeterminada de Hola. Azure crea las entradas correspondientes en caso de ser necesario.

Si seleccionó un tamaño de máquina virtual que lo admita, puede probar Azure Premium Storage, para lo que debe seleccionar Premium (SSD) en Tipo de disco.

Cuando haya terminado de realizar los cambios, haga clic en **Aceptar**.

## <a name="4-summary-blade"></a>4. Hoja Resumen

hoja de resumen de Hola enumera los valores de hello especificados en hojas de hello anterior. Haga clic en **Aceptar** cuando esté listo toomake imagen de Hola.

 ![Informe de resumen de hoja que proporciona los valores especificados de la máquina virtual de Hola](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

Después de crear la máquina virtual de hello, Hola portal mostrará las Hola nueva máquina virtual en **todos los recursos**y muestra un icono de la máquina virtual de hello en el panel de Hola. cuenta de Hello correspondiente en la nube almacenamiento y el servicio también se crean y muestran. Máquina virtual de Hola y servicio de nube se inician automáticamente y su estado aparece como **ejecutando**.

 ![Configurar puntos de conexión de máquina virtual de Hola de hello y agente de máquina virtual](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
