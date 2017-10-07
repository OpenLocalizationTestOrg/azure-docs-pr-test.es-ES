---
title: aaaGet iniciado en el DNS de Azure mediante PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un DNS zona y este registro de DNS de Azure. Esto es una guía paso a paso toocreate y administrar la primera zona DNS y registre mediante PowerShell."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a>Introducción a DNS de Azure con PowerShell

> [!div class="op_single_selector"]
> * [Portal de Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [CLI de Azure 1.0](dns-getstarted-cli-nodejs.md)
> * [CLI de Azure 2.0](dns-getstarted-cli.md)

Este artículo le guiará a través de hello pasos toocreate la primera zona DNS y el registro mediante Azure PowerShell. También puede realizar estos pasos con el portal de Azure de Hola u Hola CLI de Azure entre plataformas.

Una zona DNS es toohost usado Hola registros DNS para un dominio en particular. toostart hospedaje de su dominio de DNS de Azure, necesita toocreate una zona DNS para ese nombre de dominio. Cada registro DNS del dominio se crea luego en esta zona DNS. Por último, toopublish su DNS de la zona toohello Internet, necesitará servidores de nombres de hello tooconfigure para dominio de Hola. A continuación, se describen cada uno de estos pasos.

Estas instrucciones se supone que ya haya instalado y firmado en tooAzure PowerShell. Para obtener ayuda, consulte [cómo toomanage DNS zonas con PowerShell](dns-operations-dnszones.md).

## <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola

Antes de crear la zona DNS de hello, un grupo de recursos se crea la zona DNS de toocontain Hola. siguiente Hello muestra comandos de Hola.

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a>Creación de una zona DNS

Se crea una zona DNS mediante el uso de hello `New-AzureRmDnsZone` cmdlet. Hello en el ejemplo siguiente se crea una zona DNS denominada *contoso.com* en grupo de recursos de hello denominado *MyResourceGroup*. Utilice toocreate de ejemplo de Hola una zona DNS, sustituyendo los valores de hello para su propio.

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a>Creación de un registro de DNS

Crear conjuntos de registros mediante hello `New-AzureRmDnsRecordSet` cmdlet. Hello en el ejemplo siguiente se crea un registro con el nombre relativo de Hola "www" Hola "contoso.com", en el grupo de recursos "MyResourceGroup" de la zona DNS. nombre completo de Hola de conjunto de registros de hello es "www.contoso.com". tipo de registro de Hello es "A", con la dirección IP "1.2.3.4" y Hola TTL es 3600 segundos.

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

Para otros tipos de registros, para conjuntos de registros con más de un registro y toomodify los registros existentes, consulte [registros administrar DNS y los conjuntos de registros con Azure PowerShell](dns-operations-recordsets.md). 


## <a name="view-records"></a>Visualización de los registros

registros DNS de hello toolist en su zona, use:

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a>Actualización de los servidores de nombres

Una vez haya satisface que la zona DNS y los registros se han configurado correctamente, necesita tooconfigure su nombre de dominio toouse servidores de nombres DNS de Azure Hola. Esto permite a otros usuarios Hola Internet toofind los registros DNS.

servidores de nombres de Hello para la zona se proporcionan por hello `Get-AzureRmDnsZone` cmdlet:

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

Estos servidores de nombres deben configurarse con el registrador de nombres de dominio de hello (que adquirió nombre de dominio de hello). El registrador proporcionará Hola opción tooset los servidores de nombres de hello para el dominio de Hola. Para obtener más información, consulte [delegar su tooAzure de dominio DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Eliminación de todos los recursos

toodelete todos los recursos que se crean en este artículo, Hola toman siguiendo el paso:

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de DNS de Azure, consulte [Introducción a DNS de Azure](dns-overview.md).

toolearn más acerca de cómo administrar zonas DNS en DNS de Azure, consulte [zonas DNS de administrar en DNS de Azure con PowerShell](dns-operations-dnszones.md).

toolearn más información acerca de la administración de registros DNS en DNS de Azure, consulte [registros administrar DNS y un registro se establece en DNS de Azure con PowerShell](dns-operations-recordsets.md).

