---
title: "clústeres de Hadoop de aaaCreate mediante la API de REST de Azure - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate HDInsight clústeres mediante el envío de plantillas de Azure Resource Manager toohello API de REST de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/10/2017
ms.author: larryfr
ms.openlocfilehash: 87b585e5084eccdc3d7c57483deabb4ad6e32597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a>Crear clústeres de Hadoop con hello API de REST de Azure

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Aprenda cómo toocreate una HDInsight clúster usando una plantilla de Azure Resource Manager y Hola API de REST de Azure.

Hola API de REST de Azure permite operaciones de administración de tooperform en servicios hospedados en hello plataforma Windows Azure, incluida la creación de hello de nuevos recursos como clústeres de HDInsight.

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

> [!NOTE]
> Hola los pasos de este Hola de uso de documento [curl (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate utilidad con hello API de REST de Azure.

## <a name="create-a-template"></a>Creación de una plantilla

Las plantillas de Azure Resource Manager son documentos JSON que describen un **grupo de recursos** y todos los recursos incluidos (por ejemplo, HDInsight). Este enfoque basado en plantilla permite los recursos de hello toodefine que necesite para HDInsight en una plantilla.

Hello JSON documento siguiente es un resultado de hello combinar archivos de plantilla y parámetros de [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), que crea una basada en Linux clúster con un saludo de toosecure contraseña cuenta de usuario SSH.

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "hello type of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used tooremotely access hello cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello storage account toobe created and be used as hello cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "hello number of nodes in hello HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
                               "name": "headnode",
                               "targetInstanceCount": "2",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           },
                           {
                               "name": "workernode",
                               "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

En este ejemplo se usa en los pasos de hello en este documento. Reemplace el ejemplo hello *valores* en hello **parámetros** sección con valores de hello para el clúster.

> [!IMPORTANT]
> plantilla de Hola usa el número predeterminado de Hola de nodos de trabajador (4) para un clúster de HDInsight. Si planea crear más de 32 nodos de trabajo, tiene que seleccionar un tamaño de nodo principal con al menos 8 núcleos y 14 GB de RAM.
>
> Para obtener más información acerca de los tamaños de nodo y los costos asociados, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="log-in-tooyour-azure-subscription"></a>Inicie sesión en tooyour suscripción de Azure

Siga los pasos de hello documentados en [empezar a trabajar con Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) y conectar suscripción tooyour con hello `az login` comando.

## <a name="create-a-service-principal"></a>Creación de una entidad de servicio

> [!NOTE]
> Estos pasos son una versión resumida de hello *crear servicio de entidad de seguridad con contraseña* sección de hello [toocreate de CLI de Azure Use una entidad de servicio tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) documento. Estos pasos crea a una entidad de servicio es toohello tooauthenticate usa API de REST de Azure.

1. Desde una línea de comandos, utilice Hola después a toolist comando las suscripciones de Azure.

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    En la lista de hello, seleccione suscripción de Hola que desee toouse y tenga en cuenta hello **Subscription_ID** y __Tenant_ID__ columnas. Copie estos valores.

2. Usar hello después comando toocreate una aplicación en Azure Active Directory.

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    Reemplace los valores de hello de hello `--display-name`, `--homepage`, y `--identifier-uris` con sus propios valores. Proporcione una contraseña para la nueva entrada de Active Directory Hola.

   > [!NOTE]
   > Hola `--home-page` y `--identifier-uris` valores no es necesario tooreference una página web real hospedada en hello internet. Deben ser URI únicos.

   valor devuelto de este comando Hello es hello __Id. de aplicación__ para aplicación Hola. Guarde esta cadena.

3. Comando de uso Hola siguiente toocreate una entidad de servicio con hello **identificador de la aplicación**.

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     valor devuelto de este comando Hello es hello __Id. de objeto__. Guarde esta cadena.

4. Asignar Hola **propietario** entidad de servicio de rol toohello con hello **Id. de objeto** valor. Hola de uso **Id. de suscripción** obtenido anteriormente.

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a>Obtención de un token de autenticación

Usar hello después comando tooretrieve un token de autenticación:

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

Establecer `$TENANTID`, `$APPID`, y `$PASSWORD` toohello valores obtenido o utilizado anteriormente.

Si esta solicitud se realiza correctamente, recibirá una respuesta 200 serie y cuerpo de respuesta de hello contiene un documento JSON.

Hello documento JSON devuelta por esta solicitud contiene un elemento denominado **access_token**. Hola valo **access_token** es toohello de las solicitudes de tooauthentication usa API de REST.

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Usar hello después toocreate un grupo de recursos.

* Establecer `$SUBSCRIPTIONID` Id. de suscripción de toohello recibió durante la creación de hello entidad de servicio.
* Establecer `$ACCESSTOKEN` token de acceso de toohello recibida en el paso anterior de Hola.
* Reemplace `DATACENTERLOCATION` con el centro de datos de hello desea toocreate Hola grupo de recursos, en. Por ejemplo, "Centro-Sur de EE.UU.".
* Establecer `$RESOURCEGROUPNAME` nombre toohello desea toouse para este grupo:

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

Si esta solicitud se realiza correctamente, recibirá una respuesta 200 serie y cuerpo de respuesta de hello contiene un documento JSON que contiene información sobre el grupo de Hola. Hola `"provisioningState"` elemento contiene un valor de `"Succeeded"`.

## <a name="create-a-deployment"></a>de una implementación

Usar hello después el grupo de recursos de comando toodeploy Hola plantilla toohello.

* Establecer `$DEPLOYMENTNAME` nombre toohello desea toouse para esta implementación.

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> Si ha guardado el archivo de hello plantilla tooa, puede usar Hola siguiente comando en lugar de `-d "{ template and parameters}"`:
>
> `--data-binary "@/path/to/file.json"`

Si esta solicitud se realiza correctamente, recibirá una respuesta 200 serie y cuerpo de respuesta de hello contiene un documento JSON que contiene información sobre la operación de implementación de Hola.

> [!IMPORTANT]
> implementación de Hola se ha enviado, pero no se ha completado. Pueden tardar varios minutos, normalmente unos 15, hello toocomplete de implementación.

## <a name="check-hello-status-of-a-deployment"></a>Comprobar el estado de saludo de una implementación

estado de hello toocheck de implementación Hola Hola de uso siguiente comando:

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

Este comando devuelve un documento JSON que contiene información sobre la operación de implementación de Hola. Hola `"provisioningState"` elemento contiene el estado de Hola de implementación de Hola. Si este elemento contiene un valor de `"Succeeded"`, a continuación, la implementación de Hola se haya completado correctamente.

## <a name="troubleshoot"></a>Solución de problemas

Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha creado correctamente un clúster de HDInsight, usar hello sigue toolearn cómo toowork con el clúster.

### <a name="hadoop-clusters"></a>Clústeres Hadoop

* [Uso de Hive con HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Clústeres HBase

* [Introducción a HBase en HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Desarrollo de aplicaciones de Java para HBase en HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Clústeres Storm

* [Desarrollo de topologías de Java para Storm en HDInsight](hdinsight-storm-develop-java-topology.md)
* [Uso de componentes de Python en Storm en HDInsight](hdinsight-storm-develop-python-topology.md)
* [Implementación y supervisión de topologías con Storm en HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)
