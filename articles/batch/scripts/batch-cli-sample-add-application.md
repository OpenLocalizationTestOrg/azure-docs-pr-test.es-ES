---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure agregar una aplicación en el lote | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: adición de una aplicación a Batch"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a>Agregar aplicaciones tooAzure por lotes con CLI de Azure

Este script muestra cómo tooset una aplicación para su uso con un grupo de lote de Azure o la tarea. tooset de una aplicación, empaquetar una aplicación ejecutable, junto con las dependencias, en un archivo .zip. En este archivo zip ejecutable de ejemplo Hola archivo se denomina ' Mi-aplicaciones-exe.zip'.

## <a name="prerequisites"></a>Requisitos previos

- Instalación Hola CLI de Azure utilizando instrucciones de hello proporcionadas en hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), si aún no lo ha hecho.
- Cree una cuenta de Batch si aún no tiene una. Vea [crear una cuenta de lote con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para una secuencia de comandos de ejemplo que crea una cuenta.

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a>Aplicación de limpieza

Después de ejecutar Hola por encima de la secuencia de comandos de ejemplo, ejecutar Hola después comandos tooremove la aplicación y todos sus paquetes de aplicación cargada.

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate una aplicación y carga un paquete de aplicación.
Cada comando de la tabla de hello vincula documentación específica del toocommand.

| Comando | Notas |
|---|---|
| [az batch application create](https://docs.microsoft.com/cli/azure/batch/application#create) | Crea una aplicación.  |
| [az batch application set](https://docs.microsoft.com/cli/azure/batch/application#set) | Actualiza las propiedades de una aplicación.  |
| [az batch application package create](https://docs.microsoft.com/cli/azure/batch/application/package#create) | Agrega un toohello de paquete de aplicación especificado aplicación.  |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de lote en hello [documentación de CLI de lote de Azure](../batch-cli-samples.md).
