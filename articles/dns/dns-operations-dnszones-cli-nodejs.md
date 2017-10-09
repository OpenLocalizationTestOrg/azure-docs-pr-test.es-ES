---
title: aaaManage DNS zonas en DNS de Azure - 1.0 de CLI de Azure | Documentos de Microsoft
description: "Puede administrar zonas DNS con la CLI de Azure 1.0. Este artículo muestra cómo tooupdate, eliminar y crear las zonas DNS en el DNS de Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a>¿Cómo toomanage zonas de DNS de DNS de Azure utilizando Hola 1.0 de CLI de Azure

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [CLI de Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [CLI de Azure 2.0](dns-operations-dnszones-cli.md)

Esta guía le mostrará cómo toomanage su DNS zonas mediante el uso de hello multiplataforma CLI de Azure 1.0, que está disponible para Windows, Mac y Linux. También puede administrar las zonas DNS mediante [Azure PowerShell](dns-operations-dnszones.md) u Hola portal de Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello

Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

* [Azure 1.0 de CLI](dns-operations-dnszones-cli-nodejs.md) -nuestro CLI para modelos de implementación de administración de recursos y clásico Hola.
* [Azure 2.0 CLI](dns-operations-dnszones-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola.

## <a name="introduction"></a>Introducción

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a>Ayuda

Inician todos los comandos de CLI 1.0 relativas tooAzure DNS con `azure network dns`. La Ayuda está disponible para cada comando con hello `--help` opción (forma abreviada `-h`).  Por ejemplo:

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a>Creación de una zona DNS

Se crea una zona DNS con hello `azure network dns zone create` comando. Para obtener ayuda, consulte `azure network dns zone create -h`.

Hello en el ejemplo siguiente se crea una zona DNS denominada *contoso.com* en grupo de recursos de hello denominado *MyResourceGroup*:

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate una zona DNS con etiquetas

Hello en el ejemplo siguiente se muestra cómo toocreate un DNS de la zona con dos [etiquetas de Azure Resource Manager](dns-zones-records.md#tags), *proyecto = demostración* y *env = test*, mediante el uso de hello `--tags` parámetro (forma abreviada `-t`):

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a>Recuperación de una zona DNS

tooretrieve una zona DNS, use `azure network dns zone show`. Para obtener ayuda, consulte `azure network dns zone show -h`.

Hello en el ejemplo siguiente se devuelve la zona DNS hello *contoso.com* y sus datos asociados del grupo de recursos *MyResourceGroup*. 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

Hola siguiente ejemplo es la respuesta de Hola.

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

Tenga en cuenta que `azure network dns zone show` no devuelve los registros DNS. usar los registros DNS toolist, `azure network dns record-set list`.


## <a name="list-dns-zones"></a>Enumeración de zonas DNS

las zonas DNS tooenumerate, utilizar `azure network dns zone list`. Para obtener ayuda, consulte `azure network dns zone list -h`.

Grupo de recursos de hello especificando muestra solo las zonas en el grupo de recursos de hello:

```azurecli
azure network dns zone list MyResourceGroup
```

Si se omite el grupo de recursos de hello enumera todas las zonas de suscripción de hello:

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a>Actualización de una zona DNS

Tooa cambios recursos de zona DNS pueden realizarse con `azure network dns zone set`. Para obtener ayuda, consulte `azure network dns zone set -h`.

Este comando no actualiza cualquiera de los conjuntos de registros de DNS de hello en la zona de hello (vea [cómo los registros DNS tooManage](dns-operations-recordsets-cli-nodejs.md)). Es solo tooupdate usa propiedades del propio recurso de zona Hola. Estas propiedades están limitada actualmente toohello [Azure Resource Manager «etiquetas»](dns-zones-records.md#tags) para recursos de la zona de Hola.

Hello en el ejemplo siguiente se muestra cómo tooupdate Hola etiquetas en una zona DNS. las etiquetas existentes Hola se reemplazan por valor de hello especificado.

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a>Eliminación de una zona DNS

Las zonas DNS se pueden eliminar mediante `azure network dns zone delete`. Para obtener ayuda, consulte `azure network dns zone delete -h`.

> [!NOTE]
> Al eliminar una zona DNS, también eliminan todos los registros DNS en la zona de Hola. Esta operación no se puede deshacer. Si la zona DNS Hola está en uso, se producirá un error en servicios con zona de hello cuando se elimina la zona de Hola.
>
>tooprotect contra la eliminación accidental de zona, consulte [cómo tooprotect DNS zonas y registros](dns-protect-zones-recordsets.md).

Este comando solicita confirmación. Hola opcional `--quiet` cambiar (forma abreviada `-q`) no se muestre este mensaje.

Hello en el ejemplo siguiente se muestra cómo toodelete Hola zona *contoso.com* del grupo de recursos *MyResourceGroup*.

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo demasiado[administrar conjuntos de registros y registros](dns-getstarted-create-recordset-cli-nodejs.md) en la zona DNS.

Obtenga información acerca de cómo demasiado[delegar su tooAzure de dominio DNS](dns-domain-delegation.md).

