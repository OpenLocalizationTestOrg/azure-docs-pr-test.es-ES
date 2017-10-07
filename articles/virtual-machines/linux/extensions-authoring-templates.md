---
title: plantillas de aaaAuthoring con las extensiones de VM de Linux | Documentos de Microsoft
description: "Obtenga información sobre cómo crear plantillas de Azure Resource Manager con extensiones para máquinas virtuales de Linux."
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual de Linux
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Desde la CLI de Azure, ejecute hello después %1"...cerrando:

      Azure VM extension list

Este comando devuelve el nombre de publicador hello, nombre de la extensión y versión como sigue:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Estas tres propiedades se asignan demasiado "publisher", "type" y "typeHandlerVersion" respectivamente en hello por encima del fragmento de código de plantilla.

> [!NOTE]
> Siempre es toouse recomendada hello más reciente extensión versión tooget Hola actualizado más funcionalidad.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>Esquema de identificación Hola para parámetros de configuración de extensión de Hola
Hola siguiente paso a la creación de una plantilla de la extensión es formato de hello tooidentify para proporcionar parámetros de configuración. Cada extensión es compatible con su propio conjunto de parámetros.

toolook en configuraciones de ejemplo para extensiones de Linux, haga clic en la documentación de Hola para, consulte [Linux eExtensions ejemplos](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Consulte toohello después tooget una plantilla se completará con extensiones de máquina virtual.

[Custom script extension on a Linux VM (Extensión del script personalizado en una máquina virtual de Linux)](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

Después de crear la plantilla de hello, puede implementar mediante Hola CLI de Azure.

