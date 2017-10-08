---
title: recursos de aaaDeploy con API de REST y plantilla | Documentos de Microsoft
description: Use el Administrador de recursos de Azure y API de REST del Administrador de recursos toodeploy un tooAzure de recursos. recursos de Hola se definen en una plantilla de administrador de recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>Implementación de recursos con las plantillas de Resource Manager y la API de REST de Resource Manager
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [CLI de Azure](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [API DE REST](resource-group-template-deploy-rest.md)
> 
> 

Este artículo explica cómo toouse Hola API de REST del Administrador de recursos con el Administrador de recursos plantillas toodeploy su tooAzure de recursos.  

> [!TIP]
> Para obtener ayuda con la depuración de un error durante la implementación, consulte:
> 
> * [Ver las operaciones de implementación](resource-manager-deployment-operations.md) toolearn sobre cómo obtener la información que le ayude a solucionar el error
> * [Solucionar errores comunes al implementar tooAzure de recursos con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md) toolearn cómo tooresolve errores comunes de implementación
> 
> 

La plantilla puede ser un archivo local o en un archivo externo que está disponible a través de un identificador URI. Cuando la plantilla reside en una cuenta de almacenamiento, puede restringir la plantilla de toohello de acceso y proporcionar un token de firma (SAS) de acceso compartido durante la implementación.

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>Implementar con hello API de REST
1. Establezca los [encabezados y parámetros comunes](https://docs.microsoft.com/rest/api/index), incluidos los tokens de autenticación.
2. Si no tiene un grupo de recursos existente, puede crear uno. Proporcionar el Id. de suscripción, el nombre de Hola de nuevo grupo de recursos de Hola y la ubicación que necesite para su solución. Para obtener más información, consulte [Crear un grupo de recursos](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. Validación de la implementación antes de ejecutarlo mediante la ejecución de hello [validar una implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operación. Al probar la implementación de hello, proporcionar parámetros exactamente como lo haría al ejecutar la implementación de hello (que se muestra en el paso siguiente de hello).
4. Cree una implementación. Proporcione el identificador de suscripción, nombre Hola Hola del grupo de recursos, nombre de Hola de implementación de hello y una plantilla de tooyour de vínculo. Para obtener información sobre el archivo de plantilla de hello, consulte [archivo de parámetros](#parameter-file). Para obtener más información acerca de la API de REST de hello toocreate un grupo de recursos, consulte [crear una implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate). Hola aviso **modo** se establece demasiado**Incremental**. establece una implementación completa, toorun **modo** demasiado**completar**. Tenga cuidado al utilizar el modo completo de hello tal y como se puede eliminar accidentalmente los recursos que no están en la plantilla.
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      Si desea el contenido de la respuesta de toolog, contenido de la solicitud o ambos, incluir **debugSetting** en solicitud de saludo.
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      Puede configurar su toouse de cuenta de almacenamiento un token de firma (SAS) de acceso compartido. Para obtener más información, consulte [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature)(Delegación del acceso con una firma de acceso compartido).
5. Obtener estado de Hola de implementación de plantilla de Hola. Para obtener más información, consulte [Obtener información acerca de una implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>Archivo de parámetros

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>Pasos siguientes
* toolearn sobre el control de operaciones asincrónicas de REST, consulte [realizar un seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).
* Para obtener un ejemplo de la implementación de los recursos a través de la biblioteca de cliente de .NET de hello, consulte [implementar usando las bibliotecas de .NET y una plantilla de recursos](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* toodefine parámetros de plantilla, vea [crear plantillas](resource-group-authoring-templates.md#parameters).
* Para obtener instrucciones sobre la implementación de los entornos de toodifferent de solución, vea [entornos de desarrollo y prueba en Microsoft Azure](solution-dev-test-environments.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

