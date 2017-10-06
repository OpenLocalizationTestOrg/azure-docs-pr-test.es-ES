---
title: "tutorial de instancias de contenedor de aaaAzure - implementar aplicación | Documentos de Microsoft"
description: "Tutorial de Azure Container Instances: implementación de aplicación"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a>Implementar un contenedor de instancias de contenedor tooAzure

Se trata de hello última de un tutorial de tres partes. En las secciones anteriores, [una imagen de contenedor se creó](container-instances-tutorial-prepare-app.md) y [inserta tooan del registro de contenedor de Azure](container-instances-tutorial-prepare-acr.md). En esta sección, se finaliza el tutorial de hello mediante la implementación de contenedor de hello tooAzure instancias de contenedor. Los pasos completados incluyen:

> [!div class="checklist"]
> * Definición de un grupo de contenedores mediante una plantilla de Azure Resource Manager
> * Implementar grupo de contenedor de hello mediante Hola CLI de Azure
> * Visualización de los registros de contenedores

## <a name="deploy-hello-container-using-hello-azure-cli"></a>Implementar contenedor de hello mediante Hola CLI de Azure

Hola CLI de Azure permite la implementación de un contenedor de tooAzure instancias de contenedor en un solo comando. Puesto que se hospeda la imagen de contenedor de hello en Hola privada del registro de contenedor de Azure, debe incluir hello las credenciales necesarias tooaccess lo. En caso de ser necesario, puede consultarlas tal como se indica a continuación.

Servidor de inicio de sesión en el registro de contenedor (actualice con su nombre de registro):

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

Contraseña del registro de contenedor:

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

toodeploy la imagen de contenedor del registro de contenedor de hello con un recurso de solicitud de 1 núcleo de CPU y 1GB de memoria, ejecute el siguiente comando de hello:

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

En cuestión de segundos, recibirá una respuesta inicial de Azure Resource Manager. estado de hello tooview de implementación de hello, use:

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

Podemos seguir ejecutando este comando hasta que se cambia el estado de Hola de *pendiente* demasiado*ejecutando*. Después, ya se puede continuar.

## <a name="view-hello-application-and-container-logs"></a>Ver los registros de aplicación y el contenedor de Hola

Cuando se complete correctamente la implementación de hello, abra la dirección IP del explorador toohello que se muestra en la salida de hello de hello siguiente comando:

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Aplicación de Hello world en el Explorador de Hola][aci-app-browser]

También puede ver la salida de registro de hello de contenedor de hello:

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

Salida:

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha completado proceso hello de la implementación de su tooAzure contenedores instancias de contenedor. se completaron Hola pasos:

> [!div class="checklist"]
> * Implementación de contenedor de Hola desde el registro de contenedor de Azure con el Hola Hola CLI de Azure
> * Ver aplicación hello en el Explorador de Hola
> * Visualización de registros de contenedor de Hola

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
