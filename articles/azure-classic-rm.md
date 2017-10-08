---
title: "modos de aaaResource Manager y administración de servicios de implementación (clásica) | Documentos de Microsoft"
description: "Obtenga información acerca de las diferencias de hello entre el Administrador de recursos y los modelos de implementación clásica."
services: virtual-network
documentationcenter: 
author: telmosampaio
manager: carmonm
editor: 
tags: azure-resource-manager,azure-service-management
redirect_url: ./azure-resource-manager/resource-manager-deployment-model
ms.assetid: 18a235d8-38ac-4886-9e56-b3855c73ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: telmos
ms.openlocfilehash: e14f815ba9d79d9dd8f83b45bda78d0eba0bec56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-deployment-models"></a>Modelos de implementación de Azure
Hola plataforma Windows Azure está en transición.  Si es tooAzure nuevo o ha estado utilizando durante años, es importante toounderstand algunos de los cambios clave de hello estamos realizando toohello plataforma durante esta transición.

Todos los recursos de Azure admiten uno o dos de hello después de modelos de implementación:

* **El Administrador de recursos:** se trata de modelo de implementación más reciente de Hola de recursos de Azure. La mayoría de los recursos más recientes ya son compatibles con este modelo de implementación y, a la larga, todos los recursos lo serán.   
* **Clásico:** este modelo es compatible con la mayoría de los recursos de Azure existentes hoy en día. Nuevos recursos agregan tooAzure no será compatible con este modelo.

documentación de Hola para cada servicio que modela los detalles de recursos de Azure puede crearse con.

## <a name="why-does-this-matter"></a>¿Por qué es importante?
Es importante para hello siguientes motivos:

* características de la plataforma Windows Azure de Hola que usa son diferentes entre estos dos modelos.  Por ejemplo, se pueden crear los recursos creados mediante el modelo de implementación del Administrador de recursos de hello (o simplemente el Administrador de recursos) con [plantillas de Azure Resource Manager](azure-resource-manager/resource-group-overview.md#template-deployment), mientras que los recursos creados con el modelo de implementación de hello clásico no pueden.
* Hola características individuales de recursos de Azure o comportamientos pueden ser diferente entre dos modelos de Hola o solo existen en un modelo u Hola otro.  Por ejemplo, equilibrio de carga tráfico entre máquinas virtuales creadas con el modelo de implementación clásica de hello es *implícita* porque las máquinas virtuales son miembros de un servicio de nube de Azure y carga se equilibra automáticamente entre virtual máquinas en un servicio de nube. Las máquinas virtuales creadas mediante el Administrador de recursos no son miembros de un servicio de nube y debe ser un recurso de equilibrador de carga de Azure independiente *explícitamente* creado tráfico de equilibrio de tooload entre varias máquinas virtuales.  
* La forma de crear, configurar y administrar los recursos de Azure es diferente entre estos dos modelos.
* Los recursos creados con un modelo de implementación no necesariamente pueden interoperar con los recursos creados mediante otro modelo de implementación. Por ejemplo, máquinas virtuales de Azure creados mediante un modelo de implementación solo puede estar conectado tooAzure redes virtuales creadas con hello mismo modelo de implementación.    

Cada uno de los modelos de implementación de hello subyacente es una interfaz de programación de aplicaciones (API) para cada recurso.  Hay un [API del Administrador de recursos](https://msdn.microsoft.com/library/azure/dn948464.aspx) para el modelo de implementación del Administrador de recursos de Hola y un [API de administración de servicios](https://msdn.microsoft.com/library/azure/ee460799.aspx) para el modelo de implementación de hello clásico. Los programadores pueden escribir código toointeract con estas API *directamente*.  

Los profesionales de TI sin embargo, normalmente interactúan con estas API *indirectamente* mediante un portal de gráfico en un explorador web, mediante el uso de Azure PowerShell cmdlets en un equipo Windows o mediante el uso de Hola interfaz de línea de comandos (CLI) de Azure en cualquier un Equipo con Windows, OS X o Linux. Las tres de estos métodos indirectos usados por hello profesional de TI interactúan directamente con las API de Hola. Esto significa que cuando nueva funcionalidad se ha introducido toohello Azure plataforma o recursos, está siempre disponible directamente a través de la API de hello en primer lugar, con métodos indirecta Hola obtengan nuevos recursos de soporte técnico para hello y características después de hello API se pone a disposición.  

Hola las siguientes secciones explican cómo Azure recursos se configuran mediante Hola diferentes modelos de implementación a través de métodos de hello tres indirecta.

## <a name="portals"></a>Portales
Azure tiene dos portales:

* **[Azure Portal](https://manage.windowsazure.com):** Si lleva tiempo usando Azure, ya utiliza este portal. Es toocreate usado y configurar los recursos de Azure anteriores que admiten el modelo de implementación clásica de Hola. No se puede usar toocreate o configurar los recursos que solo son compatibles con el Administrador de recursos. 
* **[Portal de vista previa de Azure](https://azure.microsoft.com/overview/preview-portal/):** Si usa un recurso de Azure más reciente, es probable que ya utilice este portal. Puede ser usado toocreate y configurar algunos recursos de Azure. Finalmente deberá ser capaz de toocreate y configure todos los recursos de Azure con él. Para algunos recursos que admiten dos modelos de implementación, este portal puede ser usado toocreate y configurar un recurso con cualquier modelo de implementación. 

Algunas características y recursos solo se crean y configuran en un portal o hello otro. Algunos recursos o características (todavía) no se puede crear o configuran en cualquier portal y solo se pueden configurar con PowerShell, Hola CLI, o ambos. documentación de Hola para cada recurso de Azure detalla qué método se puede crear con. 

## <a name="powershell"></a>PowerShell
Con [PowerShell](/powershell/azureps-cmdlets-docs) puede usar un toocreate de scripts de línea de comandos o el creador y configurar los recursos de Azure desde un equipo de Windows.  Cada uno de los recursos de Azure tiene [cmdlets de Resource Manager](/powershell/azure/overview), [cmdlets de Service Management](/powershell/azure/overview?view=azuresmps-3.7.0) o ambos.  Algunas características y recursos solo pueden crearse o configuran con PowerShell o CLI Hola. Según el recurso de hello, al usar cmdlets de PowerShell del Administrador de recursos puede tiene dos opciones para crear y configurar los recursos de Azure:

* **Solo los cmdlets de PowerShell:** puede crear y configurar cada recurso de Azure individualmente mediante cmdlets de Hola para cada recurso. Puede hacerlo desde una línea de comandos o mediante la inclusión de varios comandos en un script de PowerShell que puede almacenar y modificar para crear versiones.
* **Cmdlets de PowerShell con una plantilla de Azure Resource Manager:** puede usar PowerShell toocreate Azure recursos mediante una plantilla de Azure Resource Manager. Las plantillas se pueden guardar y modificar para crear versiones. Más información, lea hello [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md) artículo. Existen varias [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/) para soluciones comunes que también se pueden descargar y modificar.

## <a name="cli"></a>CLI
Puede crear y configurar los recursos de Azure de equipos de Windows, OS X o Linux con hello CLI.  Hola de lectura [Install hello Azure CLI](cli-install-nodejs.md) Hola de artículo tooinstall CLI en el sistema operativo de elección. Como PowerShell, hay comandos diferentes que se deben usar dependiendo de si va a crear recursos usando [el Administrador de recursos](xplat-cli-azure-resource-manager.md) o hello [clásico (administración de servicios)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) modelos de implementación.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre el [Resource Manager](azure-resource-manager/resource-group-overview.md).
* Comprender cómo demasiado[diseñar plantillas de](best-practices-resource-manager-design-templates.md).

