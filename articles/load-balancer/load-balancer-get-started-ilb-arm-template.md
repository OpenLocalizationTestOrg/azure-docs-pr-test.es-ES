---
title: aaaCreate un equilibrador de carga interno - plantilla de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un interno cargar equilibrador utilizando una plantilla en el Administrador de recursos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a>Creación del equilibrador de carga interno con una plantilla

> [!div class="op_single_selector"]
> * [Portal de Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Plantilla](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Implementar la plantilla de hello mediante haga clic en toodeploy

plantilla de ejemplo Hola disponible en el repositorio público de hello usa un archivo de parámetros que contiene el escenario Hola predeterminada valores utilizados toogenerate Hola descrito anteriormente. toodeploy este uso de la plantilla, haga clic en toodeploy, siga [este vínculo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), haga clic en **implementar tooAzure**, reemplazar valores de parámetro predeterminados de hello si es necesario y siga las instrucciones de hello del portal de Hola.

## <a name="deploy-hello-template-by-using-powershell"></a>Implementar la plantilla de hello mediante PowerShell

plantilla de hello toodeploy que ha descargado con PowerShell, siga los pasos de Hola a continuación.

1. Si nunca ha usado PowerShell de Azure, consulte [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) y siga instrucciones de hello todos los toohello de manera Hola finalizar toosign en Azure y seleccione su suscripción.
2. Descargue el disco local de hello parámetros archivo tooyour.
3. Edite el archivo hello y guárdelo.
4. Ejecute hello **New-AzureRmResourceGroupDeployment** toocreate cmdlet un grupo de recursos con Hola plantilla.

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Implementar la plantilla de hello mediante Hola CLI de Azure

plantilla de hello toodeploy mediante el uso de hello CLI de Azure, siga los pasos de Hola a continuación.

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.
2. Ejecute hello **configuración azure modo** modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.

    ```azurecli
    azure config mode arm
    ```

    Este es el resultado de hello esperada en comando hello anterior:

        info:    New mode is arm

3. Abra el archivo de parámetros de hello, seleccione su contenido y guarde el archivo tooa en el equipo. En este ejemplo, hemos guardado archivo de parámetros de hello demasiado*parameters.json*.
4. Ejecute hello **Crear implementación de grupo de azure** archivos de comandos toodeploy Hola nuevo equilibrador de carga interno mediante el uso de la plantilla de Hola y los parámetros que ha descargado y modificado anteriormente. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a>Pasos siguientes

[Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)

