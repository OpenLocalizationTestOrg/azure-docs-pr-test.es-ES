---
title: "plantillas de aaaDeploy con la línea de comandos de hello en la pila de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola tooAzure de plantillas de interfaz de línea de comandos (CLI) de multiplataforma toodeploy pila."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 6fa6b19ac94d3f020008d04ff07f1ce489aa3418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-hello-command-line"></a>Implementación de plantillas en la pila de Azure mediante la línea de comandos de Hola
Utilice Hola línea de comandos toodeploy Azure Resource Manager plantillas toohello Kit de desarrollo de pila de Azure. Plantillas de administrador de recursos de Azure implementación y aprovisionar todos los recursos de Hola para su aplicación en una única operación coordinada.

## <a name="before-you-begin"></a>Antes de empezar
 - [Instalar y conectar](azure-stack-connect-cli.md) tooAzure pila con CLI de Azure
 - Descargar archivos de hello *azuredeploy.json* y *azuredeploy.parameters.json* de hello [crear plantilla de ejemplo de cuenta de almacenamiento](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).
 
## <a name="deploy-template"></a>Implementar plantilla
Desplazarse por las carpetas de toohello que estos archivos se han descargado y ejecute hello después de la plantilla del comando toodeploy hello:

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

Este comando implementa el grupo de recursos de hello plantilla toohello **cliRG** en la ubicación predeterminada de hello Azure pila prueba de concepto.

## <a name="validate-template-deployment"></a>Validar la implementación de la plantilla
comandos de este grupo y almacenamiento cuenta de recursos, Hola de uso después de toosee:

    azure group list

    azure storage account list

## <a name="next-steps"></a>Pasos siguientes
[Administración de permisos de usuario](azure-stack-manage-permissions.md)

