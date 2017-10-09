Cuando ya no necesita un disco de datos es tooa adjunto un equipo virtual (VM), puede separar fácilmente. Cuando se separa un disco de hello VM, disco de hello no es eliminen del almacenamiento. Si desea volver a datos existentes de toouse hello en el disco de hello, puede adjuntarla toohello misma máquina virtual, u otro.  

> [!NOTE]
> Una máquina virtual en Azure utiliza distintos tipos de discos, como un disco del sistema operativo, un disco temporal local y discos de datos opcionales. Para más información, consulte [Acerca de los discos y los discos duros virtuales para Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). No se puede separar un disco del sistema operativo, a menos que también se eliminarán Hola máquina virtual.

## <a name="find-hello-disk"></a>Encuentra el disco de Hola
Para poder separar un disco de una máquina virtual debe toofind out Hola número LUN, que es un identificador de hello disco toobe desconectado. toodo que, siga estos pasos:

1. Abra la CLI de Azure y [conectar tooyour suscripción de Azure](../articles/xplat-cli-connect.md). Procure estar en el modo de administración de servicios de Azure (`azure config mode asm`).
2. Averigüe qué discos están conectado tooyour máquina virtual. Hello en el ejemplo siguiente se enumera los discos de máquina virtual denominada Hola `myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    Hola de salida es similar toohello siguiente ejemplo:

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. Tenga en cuenta Hola LUN o hello **número de unidad lógica** para el disco de Hola que desea toodetach.

## <a name="remove-operating-system-references-toohello-disk"></a>Quitar el disco del sistema operativo referencias toohello
Antes de separar disco Hola de invitado de Linux de hello, debe asegurarse de que todas las particiones de disco de hello no están en uso. Asegúrese de ese sistema operativo de hello no intenta tooremount tras un reinicio. Estos pasos deshacer configuración Hola probablemente creó cuando [adjuntar](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) disco Hola.

1. Hola de uso `lsscsi` identificador de disco de comando toodiscover Hola. `lsscsi` puede instalarse mediante `yum install lsscsi` (en distribuciones basadas en Red Hat) o mediante `apt-get install lsscsi` (en distribuciones basadas en Debian). Puede encontrar el identificador de disco de Hola que está buscando utilizando el número LUN de Hola. último número de Hola de tupla de hello en cada fila es hello LUN. Hola siguiente ejemplo de `lsscsi`, LUN 0 se asigna demasiado  */dev/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. Use `fdisk -l <disk>` particiones de hello toodiscover asociadas Hola disco toobe desconectado. Hello en el ejemplo siguiente se muestra la salida de hello para `/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. Desmonte cada partición de disco de Hola. desmonta de Hello en el ejemplo siguiente se `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. Hola de uso `blkid` comando toodiscovery hello UUID de todas las particiones. Hola de salida es similar toohello siguiente ejemplo:

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. Eliminar las entradas en hello **/etcetera/fstab** archivo asociado a las rutas de acceso de dispositivo de Hola o UUID para todas las particiones de hello disco toobe desconectado.  Las entradas de este ejemplo podrían ser:

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    o
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>Desconectar el disco de Hola
Después de encontrar el número LUN de Hola de disco de Hola y referencias de sistema operativo de hello quitado, está listo toodetach:

1. Desconectar el disco seleccionado de hello de la máquina virtual de hello mediante la ejecución de comando hello `azure vm disk detach
   <virtual-machine-name> <LUN>`. Hello en el ejemplo siguiente se separa LUN `0` de hello máquina virtual denominada `myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. Puede comprobar si el disco de hello obtuvo separado mediante la ejecución de `azure vm disk list` nuevo. Después de las comprobaciones de ejemplo de Hola Hola máquina virtual denominada `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Hola de salida es similar toohello siguiente ejemplo, que se muestra en disco de datos de hello ya no está conectado:

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

disco Hola separada permanece en el almacenamiento pero ya no es máquina virtual de tooa adjunto.

