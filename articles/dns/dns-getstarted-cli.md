---
title: aaaGet iniciado en el DNS de Azure mediante Azure CLI 2.0 | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un DNS zona y este registro de DNS de Azure. Esto es una guía paso a paso toocreate y administrar la primera zona DNS y el registro mediante Hola 2.0 de CLI de Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a>Introducción a Azure DNS con la CLI de Azure 2.0

> [!div class="op_single_selector"]
> * [Portal de Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [CLI de Azure 1.0](dns-getstarted-cli-nodejs.md)
> * [CLI de Azure 2.0](dns-getstarted-cli.md)

Este artículo le guiará a través de hello pasos toocreate la primera zona DNS y registro mediante Hola multiplataforma Azure CLI 2.0, que está disponible para Windows, Mac y Linux. También puede realizar estos pasos con el portal de Azure de Hola o Azure PowerShell.

Una zona DNS es toohost usado Hola registros DNS para un dominio en particular. toostart hospedaje de su dominio de DNS de Azure, necesita toocreate una zona DNS para ese nombre de dominio. Cada registro DNS del dominio se crea luego en esta zona DNS. Por último, toopublish su DNS de la zona toohello Internet, necesitará servidores de nombres de hello tooconfigure para dominio de Hola. A continuación, se describen cada uno de estos pasos.

Estas instrucciones se supone que ya haya instalado y firmado en tooAzure 2.0 de CLI. Para obtener ayuda, consulte [cómo toomanage DNS zonas mediante Azure CLI 2.0](dns-operations-dnszones-cli.md).

## <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola

Antes de crear la zona DNS de hello, un grupo de recursos se crea la zona DNS de toocontain Hola. siguiente Hello muestra comandos de Hola.

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>Creación de una zona DNS

Se crea una zona DNS con hello `az network dns zone create` comando. Ayuda de toosee para este comando, escriba `az network dns zone create -h`.

Hello en el ejemplo siguiente se crea una zona DNS denominada *contoso.com* en grupo de recursos de hello *MyResourceGroup*. Utilice toocreate de ejemplo de Hola una zona DNS, sustituyendo los valores de hello para su propio.

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a>Creación de un registro de DNS

toocreate un registro DNS, usar hello `az network dns record-set [record type] add-record` comando. Para obtener ayuda con los registros A, por ejemplo, vea `azure network dns record-set A add-record -h`.

Hello en el ejemplo siguiente se crea un registro con el nombre relativo de Hola "www" Hola "contoso.com", en el grupo de recursos "MyResourceGroup" de la zona DNS. nombre completo de Hola de conjunto de registros de hello es "www.contoso.com". tipo de registro de Hello es "A", con la dirección IP "1.2.3.4" y se utiliza un valor predeterminado TTL de 3600 segundos (1 hora).

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

Para otros tipos de registros, para conjuntos de registros con más de un registro, para los valores TTL alternativos y toomodify los registros existentes, consulte [registros administrar DNS y los conjuntos de registros con hello Azure CLI 2.0](dns-operations-recordsets-cli.md).


## <a name="view-records"></a>Visualización de los registros

registros DNS de hello toolist en su zona, use:

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a>Actualización de los servidores de nombres

Una vez haya satisface que la zona DNS y los registros se han configurado correctamente, necesita tooconfigure su nombre de dominio toouse servidores de nombres DNS de Azure Hola. Esto permite a otros usuarios Hola Internet toofind los registros DNS.

servidores de nombres de Hello para la zona se proporcionan por hello `az network dns zone show` comando. nombres de servidor de nombre de hello toosee, usar JSON de salida, como se muestra en el siguiente ejemplo de Hola.

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Estos servidores de nombres deben configurarse con el registrador de nombres de dominio de hello (que adquirió nombre de dominio de hello). El registrador proporcionará Hola opción tooset los servidores de nombres de hello para el dominio de Hola. Para obtener más información, consulte [delegar su tooAzure de dominio DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Eliminación de todos los recursos
 
toodelete todos los recursos que se crean en este artículo, Hola toman siguiendo el paso:

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de DNS de Azure, consulte [Introducción a DNS de Azure](dns-overview.md).

toolearn más acerca de cómo administrar zonas DNS en DNS de Azure, consulte [zonas DNS de administrar en DNS de Azure mediante Azure CLI 2.0](dns-operations-dnszones-cli.md).

toolearn más información acerca de la administración de registros DNS en DNS de Azure, consulte [registros administrar DNS y un registro se establece en DNS de Azure mediante Azure CLI 2.0](dns-operations-recordsets-cli.md).
