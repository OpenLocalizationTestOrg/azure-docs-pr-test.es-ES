---
title: "Ejemplo de Script de PowerShell - aaaAzure Agregar aplicación cert tooa clúster | Documentos de Microsoft"
description: "Script de Azure PowerShell de ejemplo: agregar un clúster de Service Fabric application certificado tooa."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a>Agregar un clúster de Service Fabric application certificado tooa

Este script de ejemplo crea un certificado autofirmado en el almacén de claves Azure especificado hello y lo instala tooall nodos de clúster de Service Fabric Hola. certificado de Hello también descarga tooa de carpeta local. nombre de Hola de hello Descargar certificado es Hola mismo que el nombre del certificado de hello en el almacén de claves de Hola Hola. Personalizar los parámetros de hello según sea necesario.

Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview) y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure. 

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siguientes comandos: cada comando en la tabla de hello vincula documentación específica de toocommand.

| Comando | Notas |
|---|---|
| [Add-AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Agregar que una nueva escala de máquinas virtuales de aplicación certificado toohello conjuntos que componen el clúster de Hola.  |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).

Encontrará más ejemplos de Azure Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).
