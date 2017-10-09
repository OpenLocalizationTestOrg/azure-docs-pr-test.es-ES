

Las extensiones de VM pueden ayudarle a:

* Modificar las características de seguridad e identidad, como el restablecimiento de valores de cuenta y el uso de antimalware
* Iniciar, detener o configurar la supervisión y el diagnóstico
* Restablecer o instalar características de conectividad, como RDP y SSH
* Diagnosticar, supervisar y administrar las máquinas virtuales

Hay muchas otras características. Periódicamente se lanzan nuevas características de extensión de máquina virtual. Este artículo describe hello Azure VM agentes para Windows y Linux, y su compatibilidad con funcionalidad de extensión de máquina virtual. Si desea obtener un listado de las extensiones de máquina virtual por categoría de característica, consulte [Características y extensiones de VM de Azure](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="azure-vm-agents-for-windows-and-linux"></a>Agentes de VM de Azure para Windows y Linux
Hola agente de máquinas virtuales de Azure (agente de VM) es un proceso protegido y ligera que instala, configura y quita las extensiones de VM en las instancias de máquinas virtuales de Azure. Hola agente de máquina virtual actúa como servicio de control local seguro hello para la máquina virtual de Azure. extensiones de Hola que Hola cargas de agente proporcionan tooincrease características específicas su productividad con la instancia de Hola.

Existen dos agentes de Azure Virtual Machines, uno para máquinas virtuales Windows y otro para máquinas virtuales Linux.

Si desea un toouse de la instancia de máquina virtual en una o varias extensiones VM, instancia de hello debe tener un agente de VM instalado. Una imagen de máquina virtual creada mediante Hola portal de Azure y una imagen de hello **Marketplace** instala automáticamente un agente de máquina virtual en el proceso de creación de hello. Si una instancia de la máquina virtual no tiene a un agente de máquina virtual, puede instalar Hola agente de máquina virtual una vez creada la instancia de la máquina virtual de Hola. O bien, puede instalar al agente de hello en una imagen de máquina virtual personalizada que carga posteriormente.

> [!IMPORTANT]
> Estos agentes de máquina virtual son servicios muy ligeros que permiten la administración protegida de las instancias de máquina virtual. Podría haber casos en los que no desea Hola agente de máquina virtual. Si es así, ser VM toocreate seguro de que no tienen Hola agente de VM instalado con hello Azure CLI o PowerShell. Aunque Hola agente de máquina virtual se puede quitar físicamente, el comportamiento de Hola de extensiones de máquina virtual en la instancia de hello es indefinido. Como consecuencia, no se admite la eliminación de agentes de máquina virtual instalados.
>

Hola agente de máquina virtual está habilitada en hello siguientes situaciones:

* Cuando se crea una instancia de una máquina virtual mediante el uso de Hola portal de Azure y selecciona una imagen de hello **Marketplace**,
* Cuando se crea una instancia de una máquina virtual con hello [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx) o hello [New-AzureQuickVM](https://msdn.microsoft.com/library/azure/dn495183.aspx) cmdlet. Puede crear una máquina virtual sin un agente de máquina virtual mediante la adición de hello **– DisableGuestAgent** parámetro toohello [Add-AzureProvisioningConfig](https://msdn.microsoft.com/library/azure/dn495299.aspx) cmdlet,

* Cuando se manualmente descargar e instalar Hola agente de máquina virtual en una instancia existente de la máquina virtual y establecer hello **ProvisionGuestAgent** valor demasiado**true**. Esta técnica se puede usar para agentes Windows y Linux, mediante el uso de un comando de PowerShell o una llamada de REST. (Si no establece hello **ProvisionGuestAgent** valor después de instalar manualmente Hola agente de máquina virtual, adición de Hola de hello agente de máquina virtual no se detecta correctamente.) Hola siguiendo el ejemplo de código muestra cómo toodo esta mediante PowerShell donde hello `$svc` y `$name` ya que se hayan determinado argumentos:

      $vm = Get-AzureVM –ServiceName $svc –Name $name
      $vm.VM.ProvisionGuestAgent = $TRUE
      Update-AzureVM –Name $name –VM $vm.VM –ServiceName $svc

* Cuando se crea una imagen de máquina virtual que incluye a un agente de máquina virtual instalado. Una vez creada la imagen de hello con hello agente de máquina virtual, puede cargar ese tooAzure de imagen. Para una máquina virtual de Windows, descargue hello [archivo .msi del agente de VM de Windows](http://go.microsoft.com/fwlink/?LinkID=394789) e instalar Hola agente de máquina virtual. Para una VM de Linux, instale Hola agente de máquina virtual del repositorio de GitHub de hello ubicado en <https://github.com/Azure/WALinuxAgent>. Para obtener más información sobre cómo tooinstall Hola agente de VM en Linux, vea hello [Guía de usuario de agente de VM de Linux de Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> En PaaS, hello agente de máquina virtual se denomina **WindowsAzureGuestAgent**y siempre está disponible en Web y máquinas virtuales de rol de trabajo. (Para obtener más información, consulte [Azure Role Architecture](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).) Hola agente de máquina virtual para máquinas virtuales de rol ahora puede agregar máquinas virtuales del servicio de nube extensiones toohello Hola igual que lo hace para las máquinas virtuales persistentes. mayor diferencia entre las extensiones de máquina virtual en función de las máquinas virtuales y las máquinas virtuales persistentes de Hello es cuando se agregan las extensiones de VM de Hola. Con máquinas virtuales de rol, las extensiones se agregan primer servicio de nube toohello, a continuación, las implementaciones de toohello dentro de ese servicio en la nube.
>
> Use la [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) toolist cmdlet todas las extensiones VM de rol disponibles.
>
>

## <a name="find-add-update-and-remove-vm-extensions"></a>Buscar, agregar, actualizar y quitar extensiones de VM
Para obtener información sobre estas tareas, consulte [Adición, búsqueda, actualización y eliminación de extensiones de máquina virtual de Azure](../articles/virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
