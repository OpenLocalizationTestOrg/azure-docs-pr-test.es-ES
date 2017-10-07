---
title: aaaManage DNS zonas en DNS de Azure - 2.0 de CLI de Azure | Documentos de Microsoft
description: "Puede administrar zonas DNS con la CLI de Azure 2.0. Este artículo muestra cómo tooupdate, eliminar y crear las zonas DNS en el DNS de Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>¿Cómo toomanage zonas de DNS de DNS de Azure utilizando Hola 2.0 de CLI de Azure

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [CLI de Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [CLI de Azure 2.0](dns-operations-dnszones-cli.md)


Esta guía le mostrará cómo toomanage su DNS zonas mediante el uso de hello multiplataforma CLI de Azure, que está disponible para Windows, Mac y Linux. También puede administrar las zonas DNS mediante [Azure PowerShell](dns-operations-dnszones.md) u Hola portal de Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello

Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

* [Azure 1.0 de CLI](dns-operations-dnszones-cli-nodejs.md) -nuestro CLI para modelos de implementación de administración de recursos y clásico Hola.
* [Azure 2.0 CLI](dns-operations-dnszones-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola.

## <a name="introduction"></a>Introducción

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Configuración de la CLI de Azure 2.0 para Azure DNS

### <a name="before-you-begin"></a>Antes de empezar

Compruebe que dispone de hello siguientes elementos antes de comenzar la configuración.

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).

* Instale Hola la versión más reciente de hello CLI de Azure 2.0, disponible para Windows, Linux o Mac. Hay disponible más información en [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

### <a name="sign-in-tooyour-azure-account"></a>Inicie sesión en tooyour cuenta de Azure

Abra una ventana de consola y autentíquese con sus credenciales. Para obtener más información, consulte el registro en tooAzure de hello CLI de Azure

```
az login
```

### <a name="select-hello-subscription"></a>Seleccione la suscripción de Hola

Compruebe las suscripciones de hello para la cuenta de hello.

```
az account list
```

Elija qué su toouse de las suscripciones de Azure.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación. Esto se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos. Sin embargo, dado que todos los recursos DNS son globales, no regionales, elección de Hola de ubicación del grupo de recursos tiene ningún impacto en el DNS de Azure.

Puede omitir este paso si utiliza un grupo de recursos existente.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Ayuda

Inician todos los comandos de CLI 2.0 relativas tooAzure DNS con `az network dns`. La Ayuda está disponible para cada comando con hello `--help` opción (forma abreviada `-h`).  Por ejemplo:

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>Creación de una zona DNS

Se crea una zona DNS con hello `az network dns zone create` comando. Para obtener ayuda, consulte `az network dns zone create -h`.

Hello en el ejemplo siguiente se crea una zona DNS denominada *contoso.com* en grupo de recursos de hello denominado *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate una zona DNS con etiquetas

Hello en el ejemplo siguiente se muestra cómo toocreate un DNS de la zona con dos [etiquetas de Azure Resource Manager](dns-zones-records.md#tags), *proyecto = demostración* y *env = test*, mediante el uso de hello `--tags` parámetro (forma abreviada `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Recuperación de una zona DNS

tooretrieve una zona DNS, use `az network dns zone show`. Para obtener ayuda, consulte `az network dns zone show --help`.

Hello en el ejemplo siguiente se devuelve la zona DNS hello *contoso.com* y sus datos asociados del grupo de recursos *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

Hola siguiente ejemplo es la respuesta de Hola.

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Tenga en cuenta que `az network dns zone show` no devuelve los registros DNS. usar los registros DNS toolist, `az network dns record-set list`.


## <a name="list-dns-zones"></a>Enumeración de zonas DNS

las zonas DNS tooenumerate, utilizar `az network dns zone list`. Para obtener ayuda, consulte `az network dns zone list --help`.

Grupo de recursos de hello especificando muestra solo las zonas en el grupo de recursos de hello:

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

Si se omite el grupo de recursos de hello enumera todas las zonas de suscripción de hello:

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Actualización de una zona DNS

Tooa cambios recursos de zona DNS pueden realizarse con `az network dns zone update`. Para obtener ayuda, consulte `az network dns zone update --help`.

Este comando no actualiza cualquiera de los conjuntos de registros de DNS de hello en la zona de hello (vea [cómo los registros DNS tooManage](dns-operations-recordsets-cli.md)). Es solo tooupdate usa propiedades del propio recurso de zona Hola. Estas propiedades están limitada actualmente toohello [Azure Resource Manager «etiquetas»](dns-zones-records.md#tags) para recursos de la zona de Hola.

Hello en el ejemplo siguiente se muestra cómo tooupdate Hola etiquetas en una zona DNS. las etiquetas existentes Hola se reemplazan por valor de hello especificado.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Eliminar una zona DNS

Las zonas DNS se pueden eliminar mediante `az network dns zone delete`. Para obtener ayuda, consulte `az network dns zone delete --help`.

> [!NOTE]
> Al eliminar una zona DNS, también eliminan todos los registros DNS en la zona de Hola. Esta operación no se puede deshacer. Si la zona DNS Hola está en uso, se producirá un error en servicios con zona de hello cuando se elimina la zona de Hola.
>
>tooprotect contra la eliminación accidental de zona, consulte [cómo tooprotect DNS zonas y registros](dns-protect-zones-recordsets.md).

Este comando solicita confirmación. Hola opcional `--yes` modificador suprime esta solicitud.

Hello en el ejemplo siguiente se muestra cómo toodelete Hola zona *contoso.com* del grupo de recursos *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo demasiado[administrar conjuntos de registros y registros](dns-getstarted-create-recordset-cli.md) en la zona DNS.

Obtenga información acerca de cómo demasiado[delegar su tooAzure de dominio DNS](dns-domain-delegation.md).

