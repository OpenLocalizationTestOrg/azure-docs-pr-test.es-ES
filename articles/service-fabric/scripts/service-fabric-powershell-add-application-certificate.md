---
title: "Ejemplo de script de Azure PowerShell: agregar certificado de aplicación a un clúster | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: agregar un certificado de aplicación a un clúster de Service Fabric."
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
ms.openlocfilehash: 9ccd6bb0458bc03e52103fa70cad26bd6bf98bd5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="add-an-application-certificate-to-a-service-fabric-cluster"></a>Incorporación de un certificado de aplicación a un clúster de Service Fabric

Este script de ejemplo crea un certificado autofirmado en el almacén de claves de Azure especificado y lo instala en todos los nodos del clúster de Service Fabric. El certificado también se descarga en una carpeta local. El nombre del certificado descargado es el mismo que el nombre del certificado del almacén de claves. Personalice los parámetros según sea necesario.

Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [guía de Azure PowerShell](/powershell/azure/overview) y luego ejecute `Login-AzureRmAccount` para crear una conexión con Azure. 

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Incorporación de un certificado de aplicación a un clúster")]

## <a name="script-explanation"></a>Explicación del script

Cada script utiliza los comandos siguientes: cada comando de la tabla crea un vínculo a documentación específica del comando.

| Comando | Notas |
|---|---|
| [Add-AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Agregue un nuevo certificado de aplicación al conjunto de escalado de máquinas virtuales que componen el clúster.  |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).

Puede encontrar ejemplos de Azure PowerShell para Azure Service Fabric en los [ejemplos de PowerShell](../service-fabric-powershell-samples.md).
