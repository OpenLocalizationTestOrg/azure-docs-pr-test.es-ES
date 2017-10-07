---
title: infraestructura de aaaAzure instrucciones - Linux de nomenclatura | Documentos de Microsoft
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para asignar nombres a los servicios de infraestructura de Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a>Directrices de nomenclatura de la infraestructura de Azure para máquinas virtuales Linux 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

En este artículo se centra en describir cómo tooapproach las convenciones de nomenclatura para todos los su toobuild varios recursos de Azure una lógica y fácilmente identificable configuración de recursos en todo el entorno.

## <a name="implementation-guidelines-for-naming-conventions"></a>Directrices de implementación para las convenciones de nomenclatura
Decisiones:

* ¿Cuáles son sus convenciones de nomenclatura para los recursos de Azure?

Tareas:

* Definir Hola pondrá toouse a través de la coherencia de toomaintain de recursos.
* Definir la cuenta de almacenamiento nombres Hola requisito para ellos toobe único global.
* Hola de documento toobe de convención de nomenclatura usa y distribuir tooall partes implicadas tooensure coherencia entre implementaciones.

## <a name="naming-conventions"></a>Convenciones de nomenclatura
Debe existir una buena convención de nomenclatura antes de crear cualquier elemento en Azure. Una convención de nomenclatura garantiza que todos los recursos de hello tienen un nombre de predicción, lo que ayuda a la menor carga administrativa de hello asociada con la administración de esos recursos.

Puede elegir toofollow un conjunto específico de convenciones de nomenclatura definidas para toda la organización o para una cuenta o suscripción de Azure específica. Aunque resulta fácil para los usuarios dentro de las reglas de las organizaciones tooestablish implícita cuando se trabaja con recursos de Azure, necesitará toobe puede tooscale para los equipos que trabajan juntos en Azure.

Debe acordar por adelantado el conjunto de convenciones de nomenclatura. Existen algunas consideraciones sobre las convenciones de nomenclatura que trascienden los conjuntos de reglas.

## <a name="affixes"></a>Afijos
Cuando examine toodefine una convención de nomenclatura, una decisión es si conviene poner hello en:

* principio de Hello del nombre de hello (prefijo)
* final de Hello del nombre de hello (sufijo)

Por ejemplo, presentamos dos nombres posibles para un grupo de recursos con hello `rg` colocará:

* Rg-WebApp (prefijo)
* WebApp-Rg (sufijo)

Pondrá puede hacer referencia a aspectos de toodifferent que se describen los recursos específicos de Hola. Hello tabla siguiente muestran algunos ejemplos que se utilizan normalmente.

| Aspecto | Ejemplos | Notas |
|:--- |:--- |:--- |
| Environment |dev, stg, prod |Según el propósito de Hola y el nombre de cada entorno. |
| Ubicación |usw (Oeste de EE. UU.), use (Este de EE. UU. 2) |Función de la región Hola del centro de datos de Hola o región de Hola de organización de Hola. |
| Componente, servicio o producto de Azure |Rg para grupo de recursos, VNet para red virtual |Dependiendo del producto Hola para qué hello recurso proporciona soporte técnico. |
| Rol |bd, aplicación, web |Dependiendo de la función hello de máquina virtual de Hola. |
| Instance |01, 02, 03, etc. |Para los recursos que pueden tener más de una instancia. Por ejemplo, servidores web de carga equilibrada en un servicio en la nube. |

Al establecer las convenciones de nomenclatura, asegúrese de que especifican claramente que pondrá toouse para cada tipo de recurso y en qué posición (sufijo de vs de prefijo).

## <a name="dates"></a>Fechas
A menudo resulta importante toodetermine fecha de Hola de creación de un recurso de nombre de Hola. Se recomienda el formato de fecha de hello AAAAMMDD. Este formato garantiza que no solo es Hola completa se registra la fecha, pero también que dos recursos cuyos nombres únicamente se diferencian en fecha Hola se ordenan alfabéticamente y cronológicamente.

## <a name="naming-resources"></a>Asignación de nombres a recursos
Definir cada tipo de recurso de convención de nomenclatura de hello, que debe tener reglas que definen cómo tooassign nombres tooeach recursos que se crea. Estas reglas deben aplicar tooall tipos de recursos, por ejemplo:

* Suscripciones
* Cuentas
* Cuentas de almacenamiento
* Redes virtuales
* Subredes
* Conjuntos de disponibilidad
* Grupos de recursos
* Máquinas virtuales
* Extremos
* Grupos de seguridad de red
* Roles

tooensure que Hola nombre proporciona suficientes recursos de información toodetermine toowhich hace referencia, debe usar nombres descriptivos.

## <a name="computer-names"></a>Nombres de equipo
Cuando se crea una máquina virtual (VM), Azure requiere un nombre de VM de los caracteres de too64 que se usa para el nombre del recurso de Hola. Azure usa Hola mismo nombre para el sistema de operativo Hola instalado Hola máquina virtual. Sin embargo, estos nombres pueden no siempre se Hola mismo.

Si se crea una máquina virtual desde un archivo de imagen .vhd que ya contiene un sistema operativo, nombre de la máquina virtual de hello en Azure puede diferir de hello nombre de equipo del sistema operativo de la máquina virtual. Esta situación puede agregar un grado de administración de tooVM de dificultad, que por lo tanto, no se recomienda. Asignar Hola Hola de recursos de máquina virtual de Azure mismo nombre como nombre de equipo de Hola que asigne el sistema de operativo toohello de esa máquina virtual.

Se recomienda ese nombre de máquina virtual de Azure hello es Hola igual que Hola subyacente nombre de equipo del sistema operativo.

## <a name="storage-account-names"></a>Nombres de cuentas de almacenamiento
En esta sección no se aplica demasiado[discos de Azure administrados](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ya que no se cree una cuenta de almacenamiento independiente. En los discos no administrados, las cuentas de almacenamiento tienen reglas especiales que regulan sus nombres. Sólo puede utilizar minúsculas y números. Para obtener más información, consulte [Creación de una cuenta de almacenamiento](../../storage/storage-create-storage-account.md#create-a-storage-account). Además, nombre de cuenta de almacenamiento de hello, con core.windows.net, debe tener un nombre DNS válido globalmente único. Por ejemplo, si se llama a la cuenta de almacenamiento de hello mystorageaccount, hello siguientes nombres DNS resultantes deben ser únicos:

* mystorageaccount.blob.core.windows.net
* mystorageaccount.table.core.windows.net
* mystorageaccount.queue.core.windows.net

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

