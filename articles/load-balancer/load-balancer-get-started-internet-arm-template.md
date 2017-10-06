---
title: "equilibrador de carga de una conexión a Internet de aaaCreate - plantilla de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de en el Administrador de recursos mediante una plantilla de equilibrador de carga de toocreate una conexión a Internet de forma"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a>Creación de un equilibrador de carga orientado a Internet mediante una plantilla

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Plantilla](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación del Administrador de recursos de Hola. También puede [Obtenga información acerca de cómo el equilibrador utilizando el modelo de implementación clásica de la carga de toocreate una conexión a Internet](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Implementar la plantilla de hello mediante haga clic en toodeploy

plantilla de ejemplo Hola disponible en el repositorio público de hello usa un archivo de parámetros que contiene el escenario Hola predeterminada valores utilizados toogenerate Hola descrito anteriormente. toodeploy este uso de la plantilla, haga clic en toodeploy, siga [este vínculo](http://go.microsoft.com/fwlink/?LinkId=544801), haga clic en **implementar tooAzure**, reemplazar valores de parámetro predeterminados de hello si es necesario y siga las instrucciones de hello del portal de Hola.

## <a name="deploy-hello-template-by-using-powershell"></a>Implementar la plantilla de hello mediante PowerShell

plantilla de hello toodeploy que ha descargado con PowerShell, siga los pasos de Hola a continuación.

1. Si nunca ha usado PowerShell de Azure, consulte [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) y siga instrucciones de hello todos los toohello de manera Hola finalizar toosign en Azure y seleccione su suscripción.
2. Ejecute hello **New-AzureRmResourceGroupDeployment** toocreate cmdlet un grupo de recursos con Hola plantilla.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
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

3. Desde el explorador, navegue demasiado[Hola plantilla de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copie el contenido de Hola de archivo json de hello y pegue en un archivo nuevo en el equipo. En este escenario, podría copiar valores de hello a continuación con el nombre de archivo de tooa **c:\lb\azuredeploy.parameters.json**.
4. Ejecute hello **Crear implementación de grupo de azure** cmdlet toodeploy Hola nuevo equilibrador de carga mediante el uso de la plantilla de Hola y los parámetros de archivos que ha descargado y modificado anteriormente. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a>Pasos siguientes

[Introducción a la configuración de un equilibrador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
