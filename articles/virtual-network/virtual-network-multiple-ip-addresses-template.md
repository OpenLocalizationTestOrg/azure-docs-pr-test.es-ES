---
title: "aaaMultiple las direcciones IP para máquinas virtuales de Azure - plantilla | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooassign varias direcciones IP de máquina virtual de tooa usando una plantilla de Azure Resource Manager."
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: jdial
ms.openlocfilehash: e7660257b2d5c7da4b8b86771abe51a2c5012fa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-an-azure-resource-manager-template"></a>Asignar varias direcciones IP máquinas toovirtual usando una plantilla de Azure Resource Manager

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Este artículo explica cómo toocreate una máquina virtual (VM) a través de la implementación de Azure Resource Manager Hola modelo utilizando una plantilla de administrador de recursos. Varias direcciones IP públicas y privadas no se puede asignar toohello misma NIC al implementar una máquina virtual a través del modelo de implementación clásica de Hola. más información acerca de los modelos de implementación de Azure, lea hello toolearn [comprender los modelos de implementación](../resource-manager-deployment-model.md) artículo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name="template-description"></a>Descripción de la plantilla

Implementación de una plantilla permite tooquickly y sistemáticamente crear recursos de Azure con los valores de configuración diferente. Hola de lectura [tutorial de la plantilla de administrador de recursos](../azure-resource-manager/resource-manager-template-walkthrough.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo si no está familiarizado con las plantillas de Azure Resource Manager. Hola [implementar una máquina virtual con varias direcciones IP](https://azure.microsoft.com/resources/templates/101-vm-multiple-ipconfig) plantilla se utiliza en este artículo.

<a name="resources"></a>Plantilla de implementación Hola crea Hola recursos siguientes:

|Recurso|Nombre|Descripción|
|---|---|---|
|Interfaz de red|*myNic1*|tres configuraciones de IP Hola que se describe en la sección de escenario de Hola de este artículo se crean y se asignan toothis NIC.|
|Recurso de direcciones IP públicas|Se crean dos: *myPublicIP* y *myPublicIP2*|Estos recursos se asignan direcciones IP públicas estáticas y se asignan toohello *IPConfig-1* y *2 IPConfig* configuraciones IP descritas en hello escenario.|
|máquina virtual|*myVM1*|Una máquina virtual DS3 estándar.|
|Red virtual|*myVNet1*|Una red virtual con una subred con el nombre *mySubnet*.|
|Cuenta de almacenamiento|Implementación de toohello único|Una cuenta de almacenamiento.|

<a name="parameters"></a>Al implementar la plantilla de hello, debe especificar valores para hello parámetros siguientes:

|Nombre|Descripción|
|---|---|
|adminUsername|Nombre de usuario de administrador. nombre de usuario de Hello debe cumplir con [requisitos de nombre de usuario Azure](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json).|
|adminPassword|Contraseña de administrador contraseña Hola debe cumplir con [requisitos de contraseña de Azure](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).|
|dnsLabelPrefix|Nombre DNS para PublicIPAddressName1. nombre DNS de Hello resolverá tooone de direcciones IP públicas Hola asignado toohello máquina virtual. Hello nombre debe ser único dentro de hello Azure región (ubicación) crear Hola VM en.|
|dnsLabelPrefix1|Nombre DNS para PublicIPAddressName2. nombre DNS de Hello resolverá tooone de direcciones IP públicas Hola asignado toohello máquina virtual. Hello nombre debe ser único dentro de hello Azure región (ubicación) crear Hola VM en.|
|OSVersion|versión de Windows o Linux de Hola para hello máquina virtual. sistema operativo de Hello es una imagen totalmente revisada de hello dado la versión de Windows o Linux seleccionado.|
|imagePublisher|publicador de imagen de Windows o Linux de Hola para hello seleccionado máquina virtual.|
|imageOffer|imagen de Windows o Linux de Hola para hello selecciona máquina virtual.|

Cada uno de los recursos de hello implementados por plantilla de Hola se configura con varias configuraciones predeterminadas. Puede ver estos valores a través de cualquiera de los siguientes métodos de hello:

- **Plantilla de vista de hello en GitHub:** si está familiarizado con las plantillas, puede ver configuración de Hola Hola [plantilla](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json).
- **Ver la configuración de hello después de implementar:** si no está familiarizado con las plantillas, puede implementar la plantilla de hello mediante pasos de una de las siguientes secciones de Hola y, a continuación, ver configuración de Hola después de la implementación.

Puede usar Hola portal de Azure, PowerShell o plantilla de hello toodeploy de hello Azure interfaz de línea de comandos (CLI). Todos los métodos generan Hola mismo resultado. plantilla de hello toodeploy, Hola completa los pasos en una de las siguientes secciones de hello:

## <a name="deploy-using-hello-azure-portal"></a>La implementación con hello portal de Azure

plantilla de Hola de toodeploy con hello portal de Azure, Hola completa siguiendo los pasos:

1. Modificar plantilla de hello, si lo desea. plantilla de Hello implementa recursos hello y configuración indicada en hello [recursos](#resources) sección de este artículo. toolearn más acerca de las plantillas y cómo tooauthor usarlas, lea la sección hello [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-network%2ftoc.json)artículo.
2. Implementar la plantilla de hello con uno de los siguientes métodos de hello:
    - **Plantilla de SELECT hello en el portal de Hola:** Hola completa los pasos de hello [implementar los recursos de plantilla personalizada](../azure-resource-manager/resource-group-template-deploy-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#deploy-resources-from-custom-template) artículo. Elegir plantilla preexistente Hola denominado *101-vm-varios-ipconfig*.
    - **Directamente:** haga clic en hello sigue botón tooopen Hola template directamente en el portal de hello:<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-multiple-ipconfig%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

Independientemente del método hello elija, necesitará toosupply valores para hello [parámetros](#parameters) enumeradas anteriormente en este artículo. Después de implementa Hola VM, toohello VM se conectan y agregar pasos Hola privada IP direcciones toohello sistema operativo implementado siguiendo Hola Hola [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo. No agregue el sistema de operativo para toohello el público direcciones IP Hola.

## <a name="deploy-using-powershell"></a>Implementación mediante PowerShell

plantilla de hello toodeploy con PowerShell, Hola completa pasos:

1. Plantilla de hello implementar siguiendo los pasos de Hola Hola [implementar una plantilla con PowerShell](../azure-resource-manager/resource-group-template-deploy-cli.md) artículo. artículo de Hola describen varias opciones para la implementación de una plantilla. Si elige toodeploy con hello `-TemplateUri parameter`, Hola URI para esta plantilla es *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Si elige toodeploy con hello `-TemplateFile` parámetro, copie el contenido de Hola de hello [archivo de plantilla](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) desde GitHub en un nuevo archivo en su equipo. Modificar el contenido de la plantilla de hello, si lo desea. plantilla de Hello implementa recursos hello y configuración indicada en hello [recursos](#resources) sección de este artículo. toolearn más acerca de las plantillas y cómo tooauthor usarlas, lea la sección hello [plantillas del Administrador de recursos de Azure de creación ](../azure-resource-manager/resource-group-authoring-templates.md)artículo.

    Independientemente de que elija toodeploy Hola plantilla con la opción de hello, debe suministrar valores para los valores de parámetro hello enumerados en hello [parámetros](#parameters) sección de este artículo. Si decide que los parámetros de toosupply mediante un archivo de parámetros, copie el contenido de Hola de hello [archivo de parámetros](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) desde GitHub en un nuevo archivo en el equipo. Modificar valores de hello en el archivo hello. Utilizar el archivo de Hola que creó como valor de Hola para hello `-TemplateParameterFile` parámetro.

    valores válidos de toodetermine Hola OSVersion, ImagePublisher y parámetros de imageOffer, Hola completa los pasos de hello [navegue y seleccione artículo de imágenes de máquina virtual de Windows](../virtual-machines/windows/cli-ps-findimage.md) artículo.

    >[!TIP]
    >Si no está seguro de si está disponible un dnslabelprefix, escriba Hola `Test-AzureRmDnsAvailability -DomainNameLabel <name-you-want-to-use> -Location <location>` toofind comando out. Si está disponible, el comando de hello devolverá `True`.

2. Después de implementa Hola VM, toohello VM se conectan y agregar pasos Hola privada IP direcciones toohello sistema operativo implementado siguiendo Hola Hola [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo. No agregue el sistema de operativo para toohello el público direcciones IP Hola.

## <a name="deploy-using-hello-azure-cli"></a>La implementación con hello CLI de Azure

plantilla de hello toodeploy con hello Azure CLI 1.0, Hola completa siguiendo los pasos:

1. Plantilla de hello implementar siguiendo los pasos de Hola Hola [implementar una plantilla con hello Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) artículo. artículo de Hola describen varias opciones para implementar la plantilla de Hola. Si elige toodeploy con hello `--template-uri` (-f), Hola URI para esta plantilla es *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Si elige toodeploy con hello `--template-file` (-f) parámetro, copie el contenido de Hola de hello [archivo de plantilla](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) desde GitHub en un nuevo archivo en su equipo. Modificar el contenido de la plantilla de hello, si lo desea. plantilla de Hello implementa recursos hello y configuración indicada en hello [recursos](#resources) sección de este artículo. toolearn más acerca de las plantillas y cómo tooauthor usarlas, lea la sección hello [plantillas del Administrador de recursos de Azure de creación ](../azure-resource-manager/resource-group-authoring-templates.md)artículo.

    Independientemente de que elija toodeploy Hola plantilla con la opción de hello, debe suministrar valores para los valores de parámetro hello enumerados en hello [parámetros](#parameters) sección de este artículo. Si decide que los parámetros de toosupply mediante un archivo de parámetros, copie el contenido de Hola de hello [archivo de parámetros](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) desde GitHub en un nuevo archivo en el equipo. Modificar valores de hello en el archivo hello. Utilizar el archivo de Hola que creó como valor de Hola para hello `--parameters-file` (-e) parámetro.

    valores válidos de toodetermine Hola OSVersion, ImagePublisher y parámetros de imageOffer, Hola completa los pasos de hello [navegue y seleccione artículo de imágenes de máquina virtual de Windows](../virtual-machines/windows/cli-ps-findimage.md) artículo.

2. Después de implementa Hola VM, toohello VM se conectan y agregar pasos Hola privada IP direcciones toohello sistema operativo implementado siguiendo Hola Hola [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo. No agregue el sistema de operativo para toohello el público direcciones IP Hola.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
