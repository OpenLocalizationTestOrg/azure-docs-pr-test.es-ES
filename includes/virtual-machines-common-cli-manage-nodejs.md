Para poder usar Hola CLI de Azure con el Administrador de recursos comandos y plantillas toodeploy Azure recursos y cargas de trabajo con grupos de recursos, necesitará una cuenta con Azure. Si no tiene una cuenta, puede obtener [aquí una evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

Si aún no ha instalado hello Azure CLI y suscripción tooyour conectados, consulte [instalación hello Azure CLI](../articles/cli-install-nodejs.md) establecer modo de hello demasiado`arm` con `azure config mode arm`y conecte tooAzure con hello `azure login` comando.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- CLI de Azure 10: la CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](../articles/virtual-machines/linux/cli-manage.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Comandos básicos de Azure Resource Manager en la CLI de Azure
Este artículo explican los comandos básicos que se desea toouse con toomanage de CLI de Azure e interactuar con los recursos (principalmente máquinas virtuales) en su suscripción de Azure.  Para obtener más ayuda con modificadores de línea de comandos específicos y opciones, puede utilizar opciones y ayuda en línea de comandos de hello escribiendo `azure <command> <subcommand> --help` o `azure help <command> <subcommand>`.

> [!NOTE]
> En estos ejemplos no se incluyen las operaciones basadas en plantillas que se recomiendan generalmente para implementaciones de máquina virtual en el Administrador de recursos. Para obtener información, consulte [Hola Utilice CLI de Azure con el Administrador de recursos de Azure](../articles/xplat-cli-azure-resource-manager.md) y [implementar y administrar máquinas virtuales usando plantillas del Administrador de recursos de Azure y hello Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

| Tarea | Resource Manager |
| --- | --- | --- |
| Crear Hola más basic para máquina virtual |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Obtener hello `image-urn` de hello `azure vm image list` comando. En [este artículo](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) encontrará algunos ejemplos.) |
| Creación de una máquina virtual Linux |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| Creación de una máquina virtual Windows |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| Enumeración de máquinas virtuales |`azure  vm list [options]` |
| Obtención información acerca de una máquina virtual |`azure  vm show [options] <resource_group> <name>` |
| Inicio de una máquina virtual |`azure vm start [options] <resource_group> <name>` |
| Detención de una máquina virtual |`azure vm stop [options] <resource_group> <name>` |
| Cancelación de la asignación de una máquina virtual |`azure vm deallocate [options] <resource-group> <name>` |
| Reinicio de una máquina virtual |`azure vm restart [options] <resource_group> <name>` |
| Eliminación de una máquina virtual |`azure vm delete [options] <resource_group> <name>` |
| Captura de una máquina virtual |`azure vm capture [options] <resource_group> <name>` |
| Creación de una máquina virtual a partir de una imagen del usuario |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| Creación de una máquina virtual a partir de un disco especializado |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| Agregar un tooa de disco de datos VM |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| Eliminación de un disco de datos de una máquina virtual |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| Agregar una máquina virtual de extensión genérico tooa |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Agregar acceso de VM extensión tooa VM |`azure vm reset-access [options] <resource-group> <name>` |
| Agregar extensión de Docker tooa VM |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| Eliminación de una extensión de máquina virtual |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Obtención del uso de los recursos de una máquina virtual |`azure vm list-usage [options] <location>` |
| Obtención de todos los tamaños disponibles de la máquina virtual |`azure vm sizes [options]` |

## <a name="next-steps"></a>Pasos siguientes
* Para obtener más ejemplos de comandos CLI de hello más allá de la administración básica de VM, consulte [Using Hola CLI de Azure con el Administrador de recursos de Azure](../articles/virtual-machines/azure-cli-arm-commands.md).
