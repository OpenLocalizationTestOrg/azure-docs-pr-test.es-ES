---
title: "aaaCreate los registros DNS personalizados para una aplicación web | Documentos de Microsoft"
description: "¿Cómo toocreate DNS de dominio personalizado se registra para la aplicación web usa DNS de Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>Creación de registros DNS para una aplicación web en un dominio personalizado

Puede utilizar DNS de Azure toohost un dominio personalizado para las aplicaciones web. Por ejemplo, va a crear una aplicación web de Azure y desea que su tooaccess a los usuarios que, ya sea mediante contoso.com o www.contoso.com como un FQDN.

toodo, tiene dos registros de toocreate:

* Un toocontoso.com señalador registro raíz "A"
* Un "" registro CNAME para el nombre hello World Wide Web que señale toohello un registro

Tenga en cuenta que si crea un registro para una aplicación web en Azure, Hola que un registro debe actualizarse manualmente si Hola subyacente dirección IP para el cambio en la aplicación web Hola.

## <a name="before-you-begin"></a>Antes de empezar

Antes de empezar, primero debe crear una zona DNS de DNS de Azure y delegar la zona de hello en el DNS de registrador tooAzure.

1. toocreate una zona DNS, siga los pasos de hello en [crear una zona DNS](dns-getstarted-create-dnszone.md).
2. toodelegate su tooAzure DNS DNS, siga pasos hello [delegación de dominio DNS](dns-domain-delegation.md).

Después de crear una zona y delegar tooAzure DNS, a continuación, puede crear registros para el dominio personalizado.

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1. Creación de un registro A para un dominio personalizado

Un registro es toomap usa una dirección IP de tooits de nombre. En el siguiente ejemplo de Hola asignaremos como un tooan de registro de una dirección IPv4:

### <a name="step-1"></a>Paso 1

Crear un registro y asignar tooa variable $rs

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>Paso 2

Agregar conjunto de registros de hello IPv4 valor toohello creado anteriormente "@" mediante la variable $rs Hola asignado. Hola valor IPv4 asignado será la dirección IP de hello para la aplicación web.

dirección IP de hello toofind para una aplicación web, siga los pasos de hello en [configurar un nombre de dominio personalizado en el servicio de aplicación de Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>Paso 3

Confirmar el conjunto de registros toohello Hola cambios. Use `Set-AzureRMDnsRecordSet` hello tooupload cambia toohello tooAzure de conjunto de registros DNS:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2. Creación de un registro CNAME para el dominio personalizado

Si el dominio ya está administrado por DNS de Azure (consulte [delegación de dominio DNS](dns-domain-delegation.md), puede usar Hola después toocreate de ejemplo de Hola un registro CNAME para contoso.azurewebsites.net.

### <a name="step-1"></a>Paso 1

Abra PowerShell y cree un nuevo conjunto de registros CNAME y asignar tooa variable $rs. En este ejemplo creará un tipo de conjunto de registros CNAME con un "tiempo toolive" de 600 segundos en la zona DNS denominado "contoso.com".

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

Hola siguiente ejemplo es la respuesta de Hola.

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Paso 2

Una vez creado el conjunto de registros CNAME de hello, debe toocreate un valor de alias que señalará toohello web app.

En hello previamente asignados variable "$rs" puede utilizar comandos de PowerShell hello debajo de alias de hello toocreate de hello web app contoso.azurewebsites.net.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

Hola siguiente ejemplo es la respuesta de Hola.

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Paso 3

Confirmar cambios de hello mediante hello `Set-AzureRMDnsRecordSet` cmdlet:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

Puede validar el registro de hello se creó correctamente consultando Hola "www.contoso.com" mediante nslookup, tal y como se muestra a continuación:

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a>Creación de un registro "awverify" para aplicaciones web

Si decide toouse un registro de la aplicación web, debe pasar por un tooensure del proceso de comprobación se dominio personalizado propio Hola. Este paso de comprobación se realiza mediante la creación de un registro CNAME especial denominado "awverify". En esta sección se aplica sólo los registros tooA.

### <a name="step-1"></a>Paso 1

Crear registro de hello "awverify". En el ejemplo de Hola siguiente, crearemos registro de "aweverify" hello para la propiedad del tooverify contoso.com para el dominio personalizado de Hola.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

Hola siguiente ejemplo es la respuesta de Hola.

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Paso 2

Una vez creado el conjunto de registros "awverify" Hola, asignar registro CNAME Hola establecer el alias. En el ejemplo de Hola a continuación, asignaremos tooawverify.contoso.azurewebsites.net de alias de conjunto de registros de CNAMe de Hola.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

Hola siguiente ejemplo es la respuesta de Hola.

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Paso 3

Confirmar cambios de hello mediante hello `Set-AzureRMDnsRecordSet cmdlet`, tal y como se muestra en el siguiente comando de Hola.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>Pasos siguientes

Siga los pasos de hello en [configurar un nombre de dominio personalizado para el servicio de aplicaciones](../app-service-web/web-sites-custom-domain-name.md) tooconfigure su toouse de aplicación web un dominio personalizado.
