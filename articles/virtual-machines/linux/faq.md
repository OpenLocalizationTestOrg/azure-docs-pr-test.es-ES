---
title: "aaaFrequently pregunta para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Proporciona respuestas toosome de preguntas frecuentes de hello sobre máquinas virtuales Linux creadas con el modelo del Administrador de recursos de Hola."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a>Preguntas frecuentes sobre las máquinas virtuales de Linux
Este artículo tratan algunas preguntas comunes sobre máquinas virtuales Linux creadas en Azure con el modelo de implementación del Administrador de recursos de Hola. Para la versión de Windows hello de este tema, consulte [preguntas más frecuentes acerca de máquinas virtuales de Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>¿Qué puedo ejecutar en una máquina virtual de Azure?
Todos los suscriptores pueden ejecutar software de servidor en una máquina virtual de Azure. Para más información, consulte [Linux en distribuciones aprobadas por Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>¿Cuánto almacenamiento puedo usar con una máquina virtual?
Cada disco de datos puede ser hasta too1 TB. número de Hola de discos de datos que puede usar depende de tamaño de Hola de máquina virtual de Hola. Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Una cuenta de almacenamiento de Azure proporciona almacenamiento para el disco del sistema operativo de Hola y los discos de datos. Cada disco es un archivo .vhd almacenado como un blob en páginas. Para obtener información detallada sobre los precios, consulte [Detalles de precios de almacenamiento](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>¿Cómo puedo tener acceso a mi máquina virtual?
Establecer un toolog de conexión remota en la máquina virtual de toohello, mediante Shell seguro (SSH). Vea Hola instrucciones sobre cómo tooconnect [desde Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [de Linux y Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). De forma predeterminada, SSH permite un máximo de 10 conexiones simultáneas. Puede aumentar este número editando el archivo de configuración de Hola.

Si tiene problemas, consulte [Solución de problemas de conexiones de Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a>¿Puedo usar datos de toostore de saludo disco temporal (/ dev/sdb1)?
No use datos de toostore de saludo disco temporal (/ dev/sdb1). Solo existe para el almacenamiento temporal. Corre el riesgo de perder datos que no se podrán recuperar.

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>¿Puedo copiar o clonar una máquina virtual de Azure existente?
Sí. Para obtener instrucciones, consulte [cómo toocreate una copia de una máquina virtual de Linux en Hola modelo de implementación del Administrador de recursos](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>¿Por qué no veo las regiones de Canadá central y Canadá oriental por medio de Azure Resource Manager?
Hola dos nuevas áreas de Canadá Central y este de Canadá no se registran automáticamente para la creación de máquinas virtuales para las suscripciones de Azure existentes. Este registro se realiza automáticamente cuando se implementa una máquina virtual a través de Hola tooany portal Azure otra región con el Administrador de recursos de Azure. Después de una máquina virtual está implementada tooany otra región de Azure, nuevas áreas de hello deben estar disponibles para máquinas virtuales posteriores.

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>¿Puedo agregar una VM de NIC toomy después de crearla?
Sí, ahora es posible. Hola VM primera necesidades toobe detenida desasignada. A continuación, puede agregar o quitar una NIC (a menos que sea Hola última NIC en hello VM). 

## <a name="are-there-any-computer-name-requirements"></a>¿Hay algún requisito de nombre de equipo?
Sí. nombre del equipo Hola puede ser un máximo de 64 caracteres de longitud. Consulte el artículo sobre las [convenciones y restricciones de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información sobre la denominación de los recursos.

## <a name="are-there-any-resource-group-name-requirements"></a>¿Existen algunos requisitos para los nombres de grupos de recursos?
Sí. nombre de grupo de recursos de Hello puede tener un máximo de 90 caracteres de longitud. Consulte el artículo sobre las [convenciones y restricciones de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información sobre los grupos de recursos.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>¿Cuáles son los requisitos de nombre de usuario de hello al crear una máquina virtual?
Los nombres de usuario deben tener entre 1 y 64 caracteres.

no se permite Hola siguiendo los nombres de usuario:

<table>
    <tr>
        <td style="text-align:center">administrator </td><td style="text-align:center"> admin </td><td style="text-align:center"> user </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>
    <tr>
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
Las contraseñas deben tener 6 a 72 caracteres de longitud y cumplen 3 fuera Hola según los requisitos de complejidad 4:

* Deben incluir caracteres en minúsculas.
* Deben incluir caracteres en mayúsculas.
* Deben incluir un dígito.
* Deben incluir un carácter especial (REGEX.MATCH [\W_]).

no se permite Hola siguientes contraseñas:

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center">P@$$w0rd</td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center">Pa$$word</td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center">Password!</td>
        <td style="text-align:center">Password1</td>
        <td style="text-align:center">Password22</td>
        <td style="text-align:center">iloveyou!</td>
    </tr>
</table>
