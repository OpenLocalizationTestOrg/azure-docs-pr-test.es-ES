
Para más información acerca de los discos, consulte [Acerca de los discos y los discos duros virtuales para Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>Conectar un disco vacío
1. Abra 1.0 de CLI de Azure y [conectar tooyour suscripción de Azure](../articles/xplat-cli-connect.md). Procure estar en el modo de administración de servicios de Azure (`azure config mode asm`).
2. Escriba `azure vm disk attach-new` toocreate y adjuntar un disco nuevo, como se muestra en el siguiente ejemplo de Hola. Reemplace *myVM* con el nombre de la máquina Virtual de Linux de Hola y especifique el tamaño de Hola de disco de hello en GB, que es *100GB* en este ejemplo:

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. Después de que se crea y asocia disco de datos de hello, aparece en la salida de hello de `azure vm disk list <virtual-machine-name>` tal y como se muestra en el siguiente ejemplo de Hola:
   
    ```azurecli
    azure vm disk list TestVM
    ```

    Hola de salida es similar toohello siguiente ejemplo:

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>un disco existente
El acoplamiento de un disco existente requiere que disponga de un .vhd disponible en la cuenta de almacenamiento.

1. Abra 1.0 de CLI de Azure y [conectar tooyour suscripción de Azure](../articles/xplat-cli-connect.md). Procure estar en el modo de administración de servicios de Azure (`azure config mode asm`).
2. Compruebe si Hola VHD desea tooattach ya está cargado tooyour suscripción de Azure:
   
    ```azurecli
    azure vm disk list
    ```

    Hola de salida es similar toohello siguiente ejemplo:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. Si no encuentra el disco de Hola que desee toouse, puede cargar una suscripción de tooyour de disco duro virtual local mediante `azure vm disk create` o `azure vm disk upload`. Un ejemplo de `disk create` sería como en el siguiente ejemplo de Hola:
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    Hola de salida es similar toohello siguiente ejemplo:

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   También puede usar `azure vm disk upload` tooupload una cuenta de almacenamiento específico de tooa de disco duro virtual. Leer más información acerca de hello comandos toomanage los discos de datos de la máquina virtual de Azure [aquí](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

4. Ahora adjuntar Hola había deseado de máquina virtual de tooyour de disco duro virtual:
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   Asegúrese de que tooreplace *myVM* con el nombre de saludo de la máquina virtual, y *myVHD* con el disco duro virtual deseado.

5. Puede comprobar disco hello es toohello adjunta la máquina virtual con `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Hola de salida es similar toohello siguiente ejemplo:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> Después de agregar un disco de datos, podrá necesita toolog en la máquina virtual de toohello e inicializar disco Hola para máquina virtual de hello pueda usar disco hello para el almacenamiento (vea Hola siguiendo los pasos para obtener más información en toodo inicializar disco hello).
> 
> 

