---
title: problemas de almacenamiento de archivos de Azure aaaTroubleshoot en Linux | Documentos de Microsoft
description: "Solución de problemas de Azure File Storage en Linux"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 3dc537d714244451a5ff8e01f4a27f03873cf2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Solución de problemas de Azure File Storage en Linux

Este artículo enumeran los problemas comunes que están relacionado tooMicrosoft almacenamiento de archivos de Azure cuando conectan desde clientes de Linux. También se proporcionan posibles causas de estos problemas y sus resoluciones.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a>"superada la cuota de disco [permiso denegado]" al intentar tooopen un archivo

En Linux, recibirá un mensaje de error similar al siguiente hello:

**<filename> [permiso denegado] Cuota de disco superada**

### <a name="cause"></a>Causa

Ha alcanzado el límite superior de Hola de identificadores abiertos simultáneas que se permiten en un archivo.

### <a name="solution"></a>Solución

Reduzca el número de Hola de identificadores abiertos simultáneos cerrando algunos controladores y, a continuación, vuelva a intentar la operación de Hola. Para más información, consulte [Lista de comprobación de rendimiento y escalabilidad de Microsoft Azure Storage](storage-performance-checklist.md).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a>Archivo lento copiar tooand de almacenamiento de archivos de Azure en Linux

-   Si no tiene un requisito específico de tamaño de E/S mínima, se recomienda que utilice 1 MB como Hola tamaño de E/S para un rendimiento óptimo.
-   Si conocer Hola tamaño final de un archivo que se está ampliando mediante el uso de escritura, y el software no experimenta problemas de compatibilidad cuando una cola no escrita en el archivo hello contiene ceros, a continuación, establecer tamaño de archivo de Hola de antemano en lugar de realizar cada escritura una extensión escritura.
-   Utilice el método de copia derecho de hello:
    -   Use [AzCopy](storage-use-azcopy.md#file-copy) para todas las transferencias entre dos recursos compartidos de archivos.
    -   Utilice [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre recursos compartidos de archivos y un equipo local.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>"Error de montaje (112): El host está apagado" debido a un tiempo de espera de reconexión

Se produce un error de montaje "112" en el cliente de Linux Hola al cliente hello ha estado inactiva durante mucho tiempo. Después de inactividad prolongados, Hola cliente se desconecta y agota el tiempo de espera de conexión de Hola.  

### <a name="cause"></a>Causa

Hola conexión puede estar inactiva para hello siguientes motivos:

-   Errores de comunicación de red que impiden la volviendo a establecer un servidor de toohello de conexión de TCP, cuando se utiliza la opción de montaje "soft" hello predeterminada
-   Correcciones de reconexión recientes que no están presentes en los kernels anteriores

### <a name="solution"></a>Solución

Este problema de reconexión en el kernel de Linux Hola se ha corregido como parte del programa Hola siguientes cambios:

- [Corrección de volver a conectar toonot aplazar la sesión de smb3 volver a conectarse mucho después de volver a conectar de socket](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7) (Llamar al servicio de eco inmediatamente después de volver a conectar el socket)
-   [CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b) (CIFS: Corregir un posible daño de memoria durante la reconexión)
-   [CIFS: Fix a possible double locking of mutex during reconnect (or kernel v4.9 and later)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183) (CIFS: Corregir un posible bloqueo doble de exclusión mutua durante la reconexión: para el kernel v4.9 y versiones posteriores)

Sin embargo, no se pueden pasar estos cambios todavía tooall Hola las distribuciones de Linux. Esta revisión y otras correcciones de reconexión se realizan en hello después populares kernels de Linux: 4.4.40, 4.8.16 y 4.9.1. Puede obtener esta revisión mediante la actualización tooone de estas versiones de kernel recomendada.

### <a name="workaround"></a>Solución alternativa

Una solución alternativa para este problema es especificar un montaje forzado. Esto fuerza Hola cliente toowait hasta que se establezca una conexión o hasta que se interrumpe explícitamente y puede ser usado tooprevent errores debido a los tiempos de espera de la red. Sin embargo, esta solución alternativa puede provocar esperas indefinidas. Ser conexiones toostop preparada según sea necesario.

Si no se puede actualizar versiones más recientes de kernel de toohello, puede solucionar este problema manteniendo un archivo en el recurso compartido de archivos de Azure de hello escribir tooevery 30 segundos o menos. Debe ser una operación de escritura, como volver a escribir Hola creado o fecha de modificación en el archivo hello. De lo contrario, podría obtener resultados almacenados en caché y la operación puede desencadenar una reconexión Hola.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>"Error de montaje (115): Operación en curso" cuando monta Azure File Storage mediante SMB 3.0

### <a name="cause"></a>Causa

Algunas distribuciones de Linux aún no admiten las características de cifrado de SMB 3.0 y los usuarios pueden recibir un mensaje de error "115" si intentan toomount almacenamiento de archivos de Azure mediante SMB 3.0 debido a una característica que falta.

### <a name="solution"></a>Solución

La característica de cifrado de SMB 3.0 para Linux se introdujo en el kernel 4.11. Esta característica permite el montaje de recursos compartidos de Azure File desde el entorno local o una región distinta de Azure. En tiempo de presentación de la publicación, esta funcionalidad ha sido utilizados tooUbuntu 17.04 y Ubuntu 16,10. Si el cliente SMB de Linux no admite el cifrado, monte el almacenamiento de archivos de Azure mediante SMB 2.1 desde una VM de Linux de Azure que se encuentra en Hola mismo centro de datos como Hola cuenta de almacenamiento de archivos.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Rendimiento lento en un recurso compartido de archivos de Azure montado en una VM de Linux

### <a name="cause"></a>Causa

Una posible causa de un rendimiento lento es que el almacenamiento en caché está deshabilitado.

### <a name="solution"></a>Solución

toocheck si se deshabilita el almacenamiento en caché, busque hello **caché =** entrada. 

**Cache=none** indica que el almacenamiento en caché está deshabilitado.  Recurso compartido de Hola de montar el volumen mediante el comando de montaje predeterminado de Hola o agregando explícitamente hello **caché = strict** opción toohello montaje comando tooensure esos valores predeterminados de almacenamiento en caché o "strict" modo de almacenamiento en caché está habilitado.

En algunos escenarios, Hola **serverino** opción de montaje puede producir hello **ls** stat toorun de comando en cada entrada de directorio. Este comportamiento produce una disminución del rendimiento cuando se muestra un listado de un directorio grande. Puede comprobar las opciones de montaje de hello su **/etcetera/fstab** entrada:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

También puede comprobar si se usan opciones correctas de hello ejecutando hello **sudo montaje | grep cifs** comando y la comprobación de su salida, como la siguiente salida de ejemplo de Hola:

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Si hello **caché = strict** o **serverino** opción es no presente, desmontar y volver a montar el almacenamiento de archivos de Azure ejecutando el comando de montaje de Hola de hello [documentación](storage-how-to-use-files-linux.md). A continuación, volver a comprobar que hello **/etcetera/fstab** entrada tiene opciones correctas de Hola.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a>Se perdieron marcas de tiempo en copiar archivos de Windows tooLinux

En las plataformas de Unix/Linux, Hola **cp -p** comando produce un error si el archivo 1 y 2 pertenecen a distintos usuarios.

### <a name="cause"></a>Causa

Hola marca force **f** en COPYFILE da como resultado en la ejecución de **cp -p -f** en Unix. Este comando también se produce un error de marca de tiempo de hello toopreserve del archivo de Hola que no posee.

### <a name="workaround"></a>Solución alternativa

Usar el usuario de cuenta de almacenamiento de Hola para copiar archivos de hello:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.

Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget resuelva el problema rápidamente.
