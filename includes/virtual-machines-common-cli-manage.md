Hola CLI de Azure 2.0 permite toocreate y administrar los recursos de Azure en Mac OS, Linux y Windows. En este artículo se detallan algunas toocreate comandos más comunes de Hola y administrar máquinas virtuales (VM).

En este artículo requiere hello Azure CLI versión 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooupgrade, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli). También puede usar [Cloud Shell](/azure/cloud-shell/quickstart) desde el explorador.

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Comandos básicos de Azure Resource Manager en la CLI de Azure
Para obtener más ayuda con modificadores de línea de comandos específicos y opciones, puede utilizar opciones y ayuda en línea de comandos de hello escribiendo `az <command> <subcommand> --help`.

### <a name="create-vms"></a>Crear máquinas virtuales
| Tarea | Comandos de la CLI de Azure |
| --- | --- |
| Crear un grupo de recursos | `az group create --name myResourceGroup --location eastus` |
| Creación de una máquina virtual Linux | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| Creación de una máquina virtual Windows | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a>Administración del estado de la máquina virtual
| Tarea | Comandos de la CLI de Azure |
| --- | --- |
| Inicio de una máquina virtual | `az vm start --resource-group myResourceGroup --name myVM` |
| Detención de una máquina virtual | `az vm stop --resource-group myResourceGroup --name myVM` |
| Cancelación de la asignación de una máquina virtual | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| Reinicio de una máquina virtual | `az vm restart --resource-group myResourceGroup --name myVM` |
| Reimplementación de una máquina virtual | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| Eliminación de una máquina virtual | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a>Obtener información de la máquina virtual
| Tarea | Comandos de la CLI de Azure |
| --- | --- |
| Enumeración de máquinas virtuales | `az vm list` |
| Obtención información acerca de una máquina virtual | `az vm show --resource-group myResourceGroup --name myVM` |
| Obtención del uso de los recursos de una máquina virtual | `az vm list-usage --location eastus` |
| Obtención de todos los tamaños disponibles de la máquina virtual | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a>Discos e imágenes
| Tarea | Comandos de la CLI de Azure |
| --- | --- |
| Agregar un tooa de disco de datos VM | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| Eliminación de un disco de datos de una máquina virtual | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| Cambio del tamaño de un disco | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| Instantánea de un disco | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| Crear imagen de una máquina virtual | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| Creación de una máquina virtual desde una imagen | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a>Pasos siguientes
Para obtener más ejemplos de comandos de CLI de hello, vea hello [crear y administrar máquinas virtuales de Linux con hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.

