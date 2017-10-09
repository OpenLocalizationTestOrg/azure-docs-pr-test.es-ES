Al agregar discos de datos tooa VM de Linux, pueden producirse errores si no existe un disco en LUN 0. Si va a agregar un disco manualmente mediante hello `azure vm disk attach-new` comando y se especifica un LUN (`--lun`) en lugar de permitir Hola Hola LUN adecuado toodetermine de la plataforma Windows Azure, tenga cuidado de que ya existe un disco ni existirá en el LUN 0. 

Considere la posibilidad de hello siguiente ejemplo que muestra un fragmento de código de salida de hello de `lsscsi`:

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

discos de datos de Hello dos existen en LUN 0 y LUN 1 (primera columna de Hola Hola `lsscsi` detalles de salida `[host:channel:target:lun]`). Ambos discos deben ser accessbile desde dentro de hello máquina virtual. Si ha especificado manualmente Hola primer disco toobe agregada a LUN 1 y el segundo disco en LUN 2 de hello, que no vea discos Hola correctamente desde dentro de la máquina virtual.

> [!NOTE]
> Hello Azure `host` valor es 5 en estos ejemplos, pero esto puede variar en función de tipo hello de almacenamiento que seleccione.
> 
> 

Este comportamiento de disco no es un problema de Azure, pero la forma de hello en qué Hola Linux kernel sigue las especificaciones de SCSI de Hola. Cuando el kernel de Linux Hola analiza el bus SCSI de Hola para detectar los dispositivos conectados, un dispositivo debe encontrarse en el LUN 0 en orden para hello sistema toocontinue buscando dispositivos adicionales. De esta forma:

* Revise la salida de hello de `lsscsi` después de agregar un tooverify de disco de datos que tiene un disco en LUN 0.
* Si el disco no aparece correctamente en la máquina virtual, compruebe que existe el disco en LUN 0.

