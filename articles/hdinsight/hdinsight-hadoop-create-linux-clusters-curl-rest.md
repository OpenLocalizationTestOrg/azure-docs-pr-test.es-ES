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
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a><span data-ttu-id="f3e40-103">Crear clústeres de Hadoop con hello API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="f3e40-103">Create Hadoop clusters using hello Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="f3e40-104">Aprenda cómo toocreate una HDInsight clúster usando una plantilla de Azure Resource Manager y Hola API de REST de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e40-104">Learn how toocreate an HDInsight cluster using an Azure Resource Manager template and hello Azure REST API.</span></span>

<span data-ttu-id="f3e40-105">Hola API de REST de Azure permite operaciones de administración de tooperform en servicios hospedados en hello plataforma Windows Azure, incluida la creación de hello de nuevos recursos como clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f3e40-105">hello Azure REST API allows you tooperform management operations on services hosted in hello Azure platform, including hello creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3e40-106">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="f3e40-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f3e40-107">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f3e40-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="f3e40-108">Hola los pasos de este Hola de uso de documento [curl (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate utilidad con hello API de REST de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e40-108">hello steps in this document use hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility toocommunicate with hello Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="f3e40-109">Creación de una plantilla</span><span class="sxs-lookup"><span data-stu-id="f3e40-109">Create a template</span></span>

<span data-ttu-id="f3e40-110">Las plantillas de Azure Resource Manager son documentos JSON que describen un **grupo de recursos** y todos los recursos incluidos (por ejemplo, HDInsight). Este enfoque basado en plantilla permite los recursos de hello toodefine que necesite para HDInsight en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="f3e40-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you toodefine hello resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="f3e40-111">Hello JSON documento siguiente es un resultado de hello combinar archivos de plantilla y parámetros de [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), que crea una basada en Linux clúster con un saludo de toosecure contraseña cuenta de usuario SSH.</span><span class="sxs-lookup"><span data-stu-id="f3e40-111">hello following JSON document is a merger of hello template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password toosecure hello SSH user account.</span></span>

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

<span data-ttu-id="f3e40-112">En este ejemplo se usa en los pasos de hello en este documento.</span><span class="sxs-lookup"><span data-stu-id="f3e40-112">This example is used in hello steps in this document.</span></span> <span data-ttu-id="f3e40-113">Reemplace el ejemplo hello *valores* en hello **parámetros** sección con valores de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="f3e40-113">Replace hello example *values* in hello **Parameters** section with hello values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3e40-114">plantilla de Hola usa el número predeterminado de Hola de nodos de trabajador (4) para un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f3e40-114">hello template uses hello default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="f3e40-115">Si planea crear más de 32 nodos de trabajo, tiene que seleccionar un tamaño de nodo principal con al menos 8 núcleos y 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="f3e40-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="f3e40-116">Para obtener más información acerca de los tamaños de nodo y los costos asociados, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f3e40-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="f3e40-117">Inicie sesión en tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="f3e40-117">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="f3e40-118">Siga los pasos de hello documentados en [empezar a trabajar con Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) y conectar suscripción tooyour con hello `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="f3e40-118">Follow hello steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect tooyour subscription using hello `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="f3e40-119">Creación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="f3e40-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="f3e40-120">Estos pasos son una versión resumida de hello *crear servicio de entidad de seguridad con contraseña* sección de hello [toocreate de CLI de Azure Use una entidad de servicio tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) documento.</span><span class="sxs-lookup"><span data-stu-id="f3e40-120">These steps are an abridged version of hello *Create service principal with password* section of hello [Use Azure CLI toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="f3e40-121">Estos pasos crea a una entidad de servicio es toohello tooauthenticate usa API de REST de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e40-121">These steps create a service principal that is used tooauthenticate toohello Azure REST API.</span></span>

1. <span data-ttu-id="f3e40-122">Desde una línea de comandos, utilice Hola después a toolist comando las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e40-122">From a command line, use hello following command toolist your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="f3e40-123">En la lista de hello, seleccione suscripción de Hola que desee toouse y tenga en cuenta hello **Subscription_ID** y __Tenant_ID__ columnas.</span><span class="sxs-lookup"><span data-stu-id="f3e40-123">In hello list, select hello subscription that you want toouse and note hello **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="f3e40-124">Copie estos valores.</span><span class="sxs-lookup"><span data-stu-id="f3e40-124">Save these values.</span></span>

2. <span data-ttu-id="f3e40-125">Usar hello después comando toocreate una aplicación en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f3e40-125">Use hello following command toocreate an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="f3e40-126">Reemplace los valores de hello de hello `--display-name`, `--homepage`, y `--identifier-uris` con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="f3e40-126">Replace hello values for hello `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="f3e40-127">Proporcione una contraseña para la nueva entrada de Active Directory Hola.</span><span class="sxs-lookup"><span data-stu-id="f3e40-127">Provide a password for hello new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f3e40-128">Hola `--home-page` y `--identifier-uris` valores no es necesario tooreference una página web real hospedada en hello internet.</span><span class="sxs-lookup"><span data-stu-id="f3e40-128">hello `--home-page` and `--identifier-uris` values don't need tooreference an actual web page hosted on hello internet.</span></span> <span data-ttu-id="f3e40-129">Deben ser URI únicos.</span><span class="sxs-lookup"><span data-stu-id="f3e40-129">They must be unique URIs.</span></span>

   <span data-ttu-id="f3e40-130">valor devuelto de este comando Hello es hello __Id. de aplicación__ para aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="f3e40-130">hello value returned from this command is hello __App ID__ for hello new application.</span></span> <span data-ttu-id="f3e40-131">Guarde esta cadena.</span><span class="sxs-lookup"><span data-stu-id="f3e40-131">Save this value.</span></span>

3. <span data-ttu-id="f3e40-132">Comando de uso Hola siguiente toocreate una entidad de servicio con hello **identificador de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="f3e40-132">Use hello following command toocreate a service principal using hello **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="f3e40-133">valor devuelto de este comando Hello es hello __Id. de objeto__.</span><span class="sxs-lookup"><span data-stu-id="f3e40-133">hello value returned from this command is hello __Object ID__.</span></span> <span data-ttu-id="f3e40-134">Guarde esta cadena.</span><span class="sxs-lookup"><span data-stu-id="f3e40-134">Save this value.</span></span>

4. <span data-ttu-id="f3e40-135">Asignar Hola **propietario** entidad de servicio de rol toohello con hello **Id. de objeto** valor.</span><span class="sxs-lookup"><span data-stu-id="f3e40-135">Assign hello **Owner** role toohello service principal using hello **Object ID** value.</span></span> <span data-ttu-id="f3e40-136">Hola de uso **Id. de suscripción** obtenido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f3e40-136">Use hello **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="f3e40-137">Obtención de un token de autenticación</span><span class="sxs-lookup"><span data-stu-id="f3e40-137">Get an authentication token</span></span>

<span data-ttu-id="f3e40-138">Usar hello después comando tooretrieve un token de autenticación:</span><span class="sxs-lookup"><span data-stu-id="f3e40-138">Use hello following command tooretrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="f3e40-139">Establecer `$TENANTID`, `$APPID`, y `$PASSWORD` toohello valores obtenido o utilizado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f3e40-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` toohello values obtained or used previously.</span></span>

<span data-ttu-id="f3e40-140">Si esta solicitud se realiza correctamente, recibirá una respuesta 200 serie y cuerpo de respuesta de hello contiene un documento JSON.</span><span class="sxs-lookup"><span data-stu-id="f3e40-140">If this request is successful, you receive a 200 series response and hello response body contains a JSON document.</span></span>

<span data-ttu-id="f3e40-141">Hello documento JSON devuelta por esta solicitud contiene un elemento denominado **access_token**.</span><span class="sxs-lookup"><span data-stu-id="f3e40-141">hello JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="f3e40-142">Hola valo **access_token** es toohello de las solicitudes de tooauthentication usa API de REST.</span><span class="sxs-lookup"><span data-stu-id="f3e40-142">hello value of **access_token** is used tooauthentication requests toohello REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="f3e40-143">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f3e40-143">Create a resource group</span></span>

<span data-ttu-id="f3e40-144">Usar hello después toocreate un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f3e40-144">Use hello following toocreate a resource group.</span></span>

* <span data-ttu-id="f3e40-145">Establecer `$SUBSCRIPTIONID` Id. de suscripción de toohello recibió durante la creación de hello entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="f3e40-145">Set `$SUBSCRIPTIONID` toohello subscription ID received while creating hello service principal.</span></span>
* <span data-ttu-id="f3e40-146">Establecer `$ACCESSTOKEN` token de acceso de toohello recibida en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3e40-146">Set `$ACCESSTOKEN` toohello access token received in hello previous step.</span></span>
* <span data-ttu-id="f3e40-147">Reemplace `DATACENTERLOCATION` con el centro de datos de hello desea toocreate Hola grupo de recursos, en.</span><span class="sxs-lookup"><span data-stu-id="f3e40-147">Replace `DATACENTERLOCATION` with hello data center you wish toocreate hello resource group, and resources, in.</span></span> <span data-ttu-id="f3e40-148">Por ejemplo, "Centro-Sur de EE.UU.".</span><span class="sxs-lookup"><span data-stu-id="f3e40-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="f3e40-149">Establecer `$RESOURCEGROUPNAME` nombre toohello desea toouse para este grupo:</span><span class="sxs-lookup"><span data-stu-id="f3e40-149">Set `$RESOURCEGROUPNAME` toohello name you wish toouse for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="f3e40-150">Si esta solicitud se realiza correctamente, recibirá una respuesta 200 serie y cuerpo de respuesta de hello contiene un documento JSON que contiene información sobre el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3e40-150">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello group.</span></span> <span data-ttu-id="f3e40-151">Hola `"provisioningState"` elemento contiene un valor de `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="f3e40-151">hello `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="f3e40-152">de una implementación</span><span class="sxs-lookup"><span data-stu-id="f3e40-152">Create a deployment</span></span>

<span data-ttu-id="f3e40-153">Usar hello después el grupo de recursos de comando toodeploy Hola plantilla toohello.</span><span class="sxs-lookup"><span data-stu-id="f3e40-153">Use hello following command toodeploy hello template toohello resource group.</span></span>

* <span data-ttu-id="f3e40-154">Establecer `$DEPLOYMENTNAME` nombre toohello desea toouse para esta implementación.</span><span class="sxs-lookup"><span data-stu-id="f3e40-154">Set `$DEPLOYMENTNAME` toohello name you wish toouse for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="f3e40-155">Si ha guardado el archivo de hello plantilla tooa, puede usar Hola siguiente comando en lugar de `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="f3e40-155">If you saved hello template tooa file, you can use hello following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="f3e40-156">Si esta solicitud se realiza correctamente, recibirá una respuesta 200 serie y cuerpo de respuesta de hello contiene un documento JSON que contiene información sobre la operación de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3e40-156">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3e40-157">implementación de Hola se ha enviado, pero no se ha completado.</span><span class="sxs-lookup"><span data-stu-id="f3e40-157">hello deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="f3e40-158">Pueden tardar varios minutos, normalmente unos 15, hello toocomplete de implementación.</span><span class="sxs-lookup"><span data-stu-id="f3e40-158">It can take several minutes, usually around 15, for hello deployment toocomplete.</span></span>

## <a name="check-hello-status-of-a-deployment"></a><span data-ttu-id="f3e40-159">Comprobar el estado de saludo de una implementación</span><span class="sxs-lookup"><span data-stu-id="f3e40-159">Check hello status of a deployment</span></span>

<span data-ttu-id="f3e40-160">estado de hello toocheck de implementación Hola Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f3e40-160">toocheck hello status of hello deployment, use hello following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="f3e40-161">Este comando devuelve un documento JSON que contiene información sobre la operación de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3e40-161">This command returns a JSON document containing information about hello deployment operation.</span></span> <span data-ttu-id="f3e40-162">Hola `"provisioningState"` elemento contiene el estado de Hola de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3e40-162">hello `"provisioningState"` element contains hello status of hello deployment.</span></span> <span data-ttu-id="f3e40-163">Si este elemento contiene un valor de `"Succeeded"`, a continuación, la implementación de Hola se haya completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="f3e40-163">If this element contains a value of `"Succeeded"`, then hello deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="f3e40-164">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="f3e40-164">Troubleshoot</span></span>

<span data-ttu-id="f3e40-165">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="f3e40-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3e40-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3e40-166">Next steps</span></span>

<span data-ttu-id="f3e40-167">Ahora que ha creado correctamente un clúster de HDInsight, usar hello sigue toolearn cómo toowork con el clúster.</span><span class="sxs-lookup"><span data-stu-id="f3e40-167">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="f3e40-168">Clústeres Hadoop</span><span class="sxs-lookup"><span data-stu-id="f3e40-168">Hadoop clusters</span></span>

* [<span data-ttu-id="f3e40-169">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3e40-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f3e40-170">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3e40-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f3e40-171">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3e40-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="f3e40-172">Clústeres HBase</span><span class="sxs-lookup"><span data-stu-id="f3e40-172">HBase clusters</span></span>

* [<span data-ttu-id="f3e40-173">Introducción a HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3e40-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="f3e40-174">Desarrollo de aplicaciones de Java para HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3e40-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="f3e40-175">Clústeres Storm</span><span class="sxs-lookup"><span data-stu-id="f3e40-175">Storm clusters</span></span>

* [<span data-ttu-id="f3e40-176">Desarrollo de topologías de Java para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3e40-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="f3e40-177">Uso de componentes de Python en Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3e40-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="f3e40-178">Implementación y supervisión de topologías con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3e40-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
