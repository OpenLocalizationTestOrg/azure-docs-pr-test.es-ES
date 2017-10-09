


En este tema se describe cómo:

* Inyectar datos en una máquina virtual (VM) de Azure cuando se está aprovisionando.
* Recuperarlos tanto para Windows como para Linux.
* Usar herramientas especiales disponibles en algunos sistemas toodetect y controlar automáticamente los datos personalizados.

> [!NOTE]
> Este artículo describe cómo personalizados datos pueden insertar mediante el uso de una máquina virtual que se creó con hello API de administración de servicios de Azure. toosee toouse Hola API de administración de recursos de Azure, vea [plantilla de ejemplo de Hola](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>Inyección de datos personalizados en su máquina virtual de Azure
Esta característica se admite actualmente solo en hello [interfaz de línea de comandos de Azure](https://github.com/Azure/azure-xplat-cli). Aquí, se crea un `custom-data.txt` archivo que contiene los datos, a continuación, insertar que en toohello VM durante el aprovisionamiento. Aunque puede utilizar cualquiera de las opciones de Hola para hello `azure vm create` comando siguiente hello muestra un enfoque muy básico:

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>Uso de datos personalizados en la máquina virtual de Hola
* Si la VM de Azure es una máquina virtual basada en Windows, el archivo de datos personalizados de hello se guarda demasiado`%SYSTEMDRIVE%\AzureData\CustomData.bin`. Aunque era tootransfer con codificación base64 de hello ordenador toohello nueva máquina virtual, es automáticamente descodificar y que se puede abrir o utilizar inmediatamente.
  
  > [!NOTE]
  > Si existe el archivo hello, se sobrescribe. seguridad de Hello en el directorio de Hola se establece demasiado**sistema: Control total** y **administradores: Control total**.
  > 
  > 
* Si la VM de Azure es una máquina virtual basadas en Linux, se encuentra el archivo de datos personalizados de hello en uno de los siguientes Hola coloca dependiendo de su distribución. Hola pueden datos con codificación base64, por lo que puede que necesite datos de hello toodecode en primer lugar:
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Cloud-init en Azure
Si la VM de Azure es de una imagen Ubuntu o CoreOS, a continuación, puede usar CustomData toosend una configuración de nube toocloud-init. O bien, si el archivo de datos personalizados es un script, cloud-init puede simplemente ejecutarlo.

### <a name="ubuntu-cloud-images"></a>Ubuntu Cloud Images
En la mayoría de las imágenes de Linux de Azure, debe modificar el "/ etc/waagent.conf" tooconfigure Hola temporal recurso disco y swap el archivo. Para más información, consulte la [Guía de usuario del Agente de Linux de Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Sin embargo, en imágenes de nube de hello Ubuntu, debe usar init de la nube tooconfigure Hola recurso disco (es decir, Hola "efímero") e intercambio de partición. Vea Hola siguiente página de wiki de Ubuntu Hola para obtener más detalles: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>Pasos siguientes: uso de cloud-init
Para obtener más información, vea hello [documentación init en la nube para Ubuntu](https://help.ubuntu.com/community/CloudInit).

<!--Link references-->
[Referencia de la API de REST de administración de servicios: Agregar rol](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Interfaz de línea de comandos de Azure](https://github.com/Azure/azure-xplat-cli)

