---
title: "aaaFAQ sobre máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Proporciona respuestas toosome de preguntas frecuentes de hello sobre máquinas virtuales de Windows creadas con el modelo del Administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Preguntas más frecuentes sobre máquinas virtuales Windows
Este artículo tratan algunas preguntas comunes sobre máquinas virtuales de Windows creadas en Azure con el modelo de implementación del Administrador de recursos de Hola. Para la versión de Linux Hola de este tema, consulte [preguntas más frecuentes acerca de las máquinas virtuales Linux](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>¿Qué puedo ejecutar en una máquina virtual de Azure?
Todos los suscriptores pueden ejecutar software de servidor en una máquina virtual de Azure. Para obtener información sobre la directiva de soporte de Hola para ejecutando software de servidor de Microsoft en Azure, consulte [soporte de software de servidor de Microsoft para máquinas virtuales de Azure](https://support.microsoft.com/kb/2721672)

Ciertas versiones de Windows 7, Windows 8.1 y Windows 10 son tooMSDN disponibles Azure benefit y suscriptores a los suscriptores de MSDN desarrollo y prueba de pago por uso para las tareas de desarrollo y pruebas. Para obtener más información, como instrucciones y limitaciones, consulte [Imágenes de cliente de Windows para los suscriptores de MSDN](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/). 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>¿Cuánto almacenamiento puedo usar con una máquina virtual?
Cada disco de datos puede ser hasta too1 TB. número de Hola de discos de datos que puede usar depende de tamaño de Hola de máquina virtual de Hola. Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Azure discos administrados son Hola disco recomendado y nuevas ofertas de almacenamiento para su uso con máquinas virtuales de Azure para el almacenamiento persistente de datos. Puede usar varios de estos discos con cada máquina virtual. Managed Disks ofrecen dos tipos de opciones de almacenamiento duraderas: discos administrados premium y estándar. Para más información, consulte los [precios de Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks).

Las cuentas de almacenamiento de Azure también pueden proporcionar almacenamiento para el disco del sistema operativo de Hola y los discos de datos. Cada disco es un archivo .vhd almacenado como un blob en páginas. Para obtener información detallada sobre los precios, consulte [Detalles de precios de almacenamiento](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>¿Cómo puedo tener acceso a mi máquina virtual?
Establezca una conexión remota mediante conexión a Escritorio remoto (RDP) para una máquina virtual Windows. Para obtener instrucciones, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Se admite un máximo de dos conexiones simultáneas, a menos que el servidor de hello está configurado como un host de sesión de servicios de escritorio remoto.  

Si tiene problemas con Escritorio remoto, consulte [tooa de conexiones de escritorio remoto solucionar problemas de máquina Virtual de Azure basado en Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Si está familiarizado con Hyper-V, puede que esté buscando un tooVMConnect similar de la herramienta. Azure no ofrece una herramienta similar porque no se admite la máquina virtual de consola acceso tooa.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>¿Puedo usar datos de toostore de saludo (Hola unidad D: de forma predeterminada) del disco temporal?
No use datos de toostore de disco temporal de saludo. Solo proporciona almacenamiento de forma temporal, por lo que se arriesgaría a perder datos que no se pueden recuperar. Puede producirse una pérdida de datos cuando mueve de máquina virtual de hello tooa otro host. Cambiar el tamaño de una máquina virtual, actualizar host hello, o un error de hardware en el host de hello es algunos de los motivos de hello que puede mover una máquina virtual.

Si tiene una aplicación que necesita la letra de unidad D: de toouse hello, puede volver a asignar letras de unidad para que hello disco temporal utiliza un valor distinto de D:. Para obtener instrucciones, consulte [cambiar la letra de unidad Hola de disco temporal de Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>¿Cómo se puede cambiar la letra de unidad de Hola de disco temporal de hello?
Puede cambiar la letra de unidad de hello al mover el archivo de página hello y reasignar letras de unidad, pero necesita toomake seguro que Hola pasos en un orden específico. Para obtener instrucciones, consulte [cambiar la letra de unidad Hola de disco temporal de Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>¿Puedo agregar un conjunto de disponibilidad de tooan VM existente?
No. Si desea que su parte de toobe de máquina virtual de un conjunto de disponibilidad, deberá toocreate Hola VM en el conjunto de Hola. Actualmente no hay un tooadd forma una disponibilidad de tooan VM establecer después de que se ha creado.

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>¿Puedo cargar un tooAzure de máquina virtual?
Sí. Para obtener instrucciones, consulte [migrar máquinas virtuales tooAzure local](on-prem-to-azure.md).

## <a name="can-i-resize-hello-os-disk"></a>¿Puedo cambiar el tamaño de disco del sistema operativo Hola?
Sí. Para obtener instrucciones, consulte [cómo tooexpand Hola unidad de sistema operativo de una máquina Virtual en un grupo de recursos de Azure](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>¿Puedo copiar o clonar una máquina virtual de Azure existente?
Sí. Uso de imágenes administradas, puede crear una imagen de una máquina virtual y, a continuación, usar Hola imagen toobuild varias nuevas máquinas virtuales. Para obtener instrucciones, consulte [Creación de una imagen personalizada de una máquina virtual](tutorial-custom-images.md).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>¿Por qué no veo las regiones de Canadá central y Canadá oriental por medio de Azure Resource Manager?

Hola dos nuevas áreas de Canadá Central y este de Canadá no se registran automáticamente para la creación de máquinas virtuales para las suscripciones de Azure existentes. Este registro se realiza automáticamente cuando se implementa una máquina virtual a través de Hola tooany portal Azure otra región con el Administrador de recursos de Azure. Después de una máquina virtual está implementada tooany otra región de Azure, nuevas áreas de hello deben estar disponibles para máquinas virtuales posteriores.

## <a name="does-azure-support-linux-vms"></a>¿Se admiten máquinas virtuales Linux en Azure?
Sí. tooquickly crear un tootry de VM de Linux out, vea [crear una VM de Linux en Azure con hello Portal](../linux/quick-create-portal.md).

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>¿Puedo agregar una VM de NIC toomy después de crearla?
Sí, ahora es posible. Hola VM primera necesidades toobe detenida desasignada. A continuación, puede agregar o quitar una NIC (a menos que sea Hola última NIC en hello VM). 

## <a name="are-there-any-computer-name-requirements"></a>¿Hay algún requisito de nombre de equipo?
Sí. nombre del equipo Hola puede ser un máximo de 15 caracteres de longitud. Consulte el artículo sobre las [convenciones y restricciones de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para más información sobre la denominación de los recursos.

## <a name="are-there-any-resource-group-name-requirements"></a>¿Existen algunos requisitos para los nombres de grupos de recursos?
Sí. nombre de grupo de recursos de Hello puede tener un máximo de 90 caracteres de longitud. Consulte el artículo sobre las [convenciones y restricciones de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para más información sobre los grupos de recursos.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>¿Cuáles son los requisitos de nombre de usuario de hello al crear una máquina virtual?

Los nombres de usuario pueden tener un máximo de 20 caracteres y no pueden terminar con un punto ("."). 


no se permite Hola siguiendo los nombres de usuario:
<table>
    <tr>
        <td style="text-align:center">administrator </td><td style="text-align:center"> admin </td><td style="text-align:center"> user </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> a</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> aspnet</td>
    </tr>
    <tr>
        <td style="text-align:center">backup </td><td style="text-align:center"> console </td><td style="text-align:center"> david </td><td style="text-align:center"> guest</td>
    </tr>
    <tr>
        <td style="text-align:center">john </td><td style="text-align:center"> owner </td><td style="text-align:center"> root </td><td style="text-align:center"> server</td>
    </tr>
    <tr>
        <td style="text-align:center">sql </td><td style="text-align:center"> support </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">test2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> user4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>

## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>¿Cuáles son los requisitos de contraseña de hello al crear una máquina virtual?
Las contraseñas deben tener 12-123 caracteres de longitud y cumplen 3 fuera Hola según los requisitos de complejidad 4:

* Deben incluir caracteres en minúsculas.
* Deben incluir caracteres en mayúsculas.
* Deben incluir un dígito.
* Deben incluir un carácter especial (REGEX.MATCH [\W_]).

no se permite Hola siguientes contraseñas:

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Pa$$word </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Password! </td>
        <td>Password1 </td>
        <td>Password22 </td>
        <td>iloveyou! </td>
    </tr>
</table>
