


## <a name="using-vm-extensions"></a>Uso de extensiones de máquina virtual
Extensiones de VM de Azure implementan comportamientos o características que ya sea ayudan a otros programas a trabajar en máquinas virtuales de Azure (por ejemplo, hello **WebDeployForVSDevTest** extensión permite implementar soluciones tooWeb de Visual Studio en la VM de Azure) o proporcionar Hola capacidad para toointeract con hello VM toosupport algún otro comportamiento (por ejemplo, puede usar las extensiones de acceso de VM de Hola de PowerShell, hello Azure CLI y tooreset de los clientes REST o modificar valores de acceso remoto en la VM de Azure).

> [!IMPORTANT]
> Para obtener una lista completa de las extensiones de características de Hola que admiten, consulte [características y extensiones de VM de Azure](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Dado que cada extensión de VM admite una característica específica, exactamente lo que puede y no puede realizar con una extensión depende Hola extensión. Por lo tanto, antes de modificar la máquina virtual, asegúrese de que ha leído documentación Hola Hola extensión de máquina virtual que desee toouse. Algunas extensiones de máquina virtual no admiten que se quiten; otras tienen propiedades que se pueden establecer y cambian radicalmente el comportamiento de la máquina virtual.
> 
> 

Hola las tareas más comunes son:

1. Buscar extensiones disponibles
2. Actualizar extensiones cargadas
3. Agregar extensiones
4. Quitar extensiones

## <a name="find-available-extensions"></a>Búsqueda de extensiones disponibles
Puede buscar la extensión e información extendida con:

* PowerShell
* Interfaz de la línea de comandos entre plataformas de Azure (CLI de Azure)
* API de REST de administración del servicio

### <a name="azure-powershell"></a>Azure PowerShell
Algunas extensiones tienen cmdlets de PowerShell que están toothem específico, que puede facilitar su configuración desde PowerShell; pero hello siguientes cmdlets funcionan para todas las extensiones de máquina virtual.

Puede usar Hola siguiente cmdlets tooobtain información sobre las extensiones disponibles:

* Para instancias de roles web o roles de trabajo, puede usar hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.
* Para instancias de máquinas virtuales, puede usar hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.
  
   Hola, por ejemplo, el siguiente ejemplo de código muestra cómo toolist la información de hello **IaaSDiagnostics** extensión mediante PowerShell.
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a>Interfaz de la línea de comandos de Azure (CLI de Azure)
Algunas extensiones tienen comandos de CLI de Azure que están toothem específico (Hola extensión de máquina virtual de Docker es un ejemplo), que puede facilitar su configuración; pero los comandos del siguiente Hola todas las extensiones de máquina virtual.

Puede usar hello **lista de extensiones de máquina virtual de azure** comando tooobtain información sobre las extensiones disponibles y usar hello **–-json** opción toodisplay toda la información disponible acerca de una o varias extensiones. Si no usa un nombre de extensión, comando hello devuelve una descripción de JSON de todas las extensiones disponibles.

Por ejemplo, hello el ejemplo de código siguiente muestra cómo toolist Hola información de hello **IaaSDiagnostics** extensión con hello Azure CLI **lista de extensiones de máquina virtual de azure** comando y usos hello **–-json** opción tooreturn obtener información completa.

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a>API de REST de administración de servicios
Puede usar Hola siguiente las API de REST tooobtain información sobre las extensiones disponibles:

* Para instancias de roles web o roles de trabajo, puede usar hello [enumerar extensiones disponibles](https://msdn.microsoft.com/library/dn169559.aspx) operación. versiones de hello toolist de extensiones disponibles, puede usar [enumerar versiones de extensiones](https://msdn.microsoft.com/library/dn495437.aspx).
* Para instancias de máquinas virtuales, puede usar hello [enumerar extensiones de recursos](https://msdn.microsoft.com/library/dn495441.aspx) operación. versiones de hello toolist de extensiones disponibles, puede usar [enumerar versiones de extensión de recursos](https://msdn.microsoft.com/library/dn495440.aspx).

## <a name="add-update-or-disable-extensions"></a>Adición, actualización o deshabilitación de extensiones
Las extensiones se pueden agregar cuando se crea una instancia o se puede agregar tooa ejecuta la instancia. Las extensiones se pueden actualizar, deshabilitar o quitar. Puede realizar estas acciones mediante el uso de cmdlets de PowerShell de Azure o mediante operaciones de API de REST de administración de servicios de Hola. Parámetros necesario tooinstall y configuración algunas extensiones. Se admiten parámetros públicos y privados con las extensiones.

### <a name="azure-powershell"></a>Azure PowerShell
Uso de cmdlets de PowerShell de Azure es extensiones de manera más fáciles tooadd y actualización de Hola. Al usar cmdlets de extensión de hello, la mayor parte de la configuración de Hola de extensión de Hola se realiza automáticamente. En ocasiones, puede que necesite tooprogrammatically agregar una extensión. Cuando necesite toodo esto, debe proporcionar la configuración de Hola de extensión de Hola.

Puede usar Hola después cmdlets tooknow si una extensión requiere una configuración de parámetros públicos o privados:

* Para instancias de roles web o roles de trabajo, puede usar hello **Get-AzureServiceAvailableExtension** cmdlet.
* Para instancias de máquinas virtuales, puede usar hello **Get-AzureVMAvailableExtension** cmdlet.

### <a name="service-management-rest-apis"></a>API de REST de administración de servicios
Al recuperar una lista de extensiones disponibles mediante las API de REST de hello, recibirá información sobre cómo la extensión de hello toobe configurado. información de Hola que se devuelve puede mostrar información sobre parámetros representada por un esquema público y privado. Valores de parámetros públicos se devuelven en las consultas sobre las instancias de Hola. No se devuelven los valores de parámetros privados.

Puede usar Hola siguiendo las API de REST tooknow si una extensión requiere una configuración de parámetros públicos o privados:

* Para instancias de roles web o roles de trabajo, Hola **PublicConfigurationSchema** y **PrivateConfigurationSchema** elementos contienen información de Hola en respuesta Hola Hola [lista Las extensiones disponibles](https://msdn.microsoft.com/library/dn169559.aspx) operación.
* Para instancias de máquinas virtuales, Hola **PublicConfigurationSchema** y **PrivateConfigurationSchema** elementos contienen información de Hola en respuesta Hola Hola [lista Extensiones de recursos](https://msdn.microsoft.com/library/dn495441.aspx) operación.

> [!NOTE]
> Las extensiones también pueden usar configuraciones que se definen con JSON. Cuando se utilizan estos tipos de extensiones, solo Hola **SampleConfig** elemento se utiliza.
> 
> 

