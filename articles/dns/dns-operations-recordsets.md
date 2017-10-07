---
title: aaaManage DNS registra en DNS de Azure con PowerShell de Azure | Documentos de Microsoft
description: "Administración de conjuntos de registros y registros DNS en DNS de Azure al hospedar dominios en DNS de Azure. Todos los comandos de PowerShell para operaciones en conjuntos de registros y registros."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a>Administración de conjuntos de registros y registros de DNS en Azure DNS mediante Azure PowerShell

> [!div class="op_single_selector"]
> * [Portal de Azure](dns-operations-recordsets-portal.md)
> * [CLI de Azure 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [CLI de Azure 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Este artículo muestra cómo toomanage DNS los registros de la zona DNS mediante el uso de PowerShell de Azure. También se pueden administrar los registros de DNS mediante el uso de hello multiplataforma [CLI de Azure](dns-operations-recordsets-cli.md) o hello [portal de Azure](dns-operations-recordsets-portal.md).

ejemplos de Hello en este artículo se supone que ya está [instalado PowerShell de Azure, firmado y ha creado una zona DNS](dns-operations-dnszones.md).

## <a name="introduction"></a>Introducción

Antes de crear los registros DNS en DNS de Azure, primero debe toounderstand cómo Azure DNS organiza los registros DNS en conjuntos de registros de DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Para más información sobre los registros DNS en Azure DNS, consulte [DNS zones and records](dns-zones-records.md) (Zonas y registros DNS).


## <a name="create-a-new-dns-record"></a>Creación de un nuevo registro DNS

Si el nuevo registro tiene Hola mismo nombre y tipo como un registro existente, deberá demasiado[Agregar conjunto de registros existente toohello](#add-a-record-to-an-existing-record-set). Si el nuevo registro tiene un tooall de nombre y tipo de diferentes registros existentes, deberá toocreate un nuevo conjunto de registros. 

### <a name="create-a-records-in-a-new-record-set"></a>Creación de registros "D" en un nuevo conjunto de registros

Crear conjuntos de registros mediante hello `New-AzureRmDnsRecordSet` cmdlet. Al crear un conjunto de registros, deberá nombre de conjunto de registros de hello toospecify, zona hello, hora de hello toolive (TTL), tipo de registro de Hola y Hola registros toobe creados.

parámetros de Hola para agregar el conjunto de registros tooa registros varían según tipo de Hola de conjunto de registros de Hola. Por ejemplo, cuando se utiliza un conjunto de registros de tipo 'A', necesitará dirección IP de hello toospecify mediante el parámetro hello `-IPv4Address`. Para otros tipos de registros se usan otros parámetros. Para más información, consulte [Ejemplos de tipos de registros adicionales](#additional-record-type-examples).

Hello en el ejemplo siguiente se crea un conjunto con nombre relativo Hola "www" en la zona DNS de 'contoso.com' hello de registros. nombre completo de Hola de conjunto de registros de hello es 'www.contoso.com'. tipo de registro de Hello es 'A' y Hola TTL es 3600 segundos. conjunto de registros de Hello contiene un único registro con la dirección IP '1.2.3.4'.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

toocreate un conjunto de registros en hello 'vértice' de una zona (en este caso, "contoso.com"), usar el nombre de conjunto de registros de hello ' @' (excepto las comillas):

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

Si necesita toocreate un conjunto de registros que contiene más de un registro, crear una matriz local y agregar registros de Hola y después pasar la matriz de hello demasiado`New-AzureRmDnsRecordSet` como se indica a continuación:

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

[Metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) pueden ser datos específicos de la aplicación de tooassociate usado con cada conjunto de registros, como pares de clave-valor. Hello en el ejemplo siguiente se muestra cómo toocreate un conjunto de registros con dos entradas de metadatos, ' departamento = finance' y ' entorno de producción de ='.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

DNS de Azure también admite los conjuntos de registros 'empty', que pueden actuar como un marcador de posición tooreserve un nombre DNS antes de crear los registros DNS. Conjuntos de registros vacíos son visibles en el plano de control de hello DNS de Azure, pero aparecen en los servidores de nombres DNS de Azure Hola. Hola de ejemplo siguiente crea un conjunto de registros vacío:

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a>Creación de registros de otros tipos

Después de ver en detalle cómo registros toocreate 'A', Hola siguientes ejemplos se muestra cómo toocreate registros de otros registran tipos compatibles con DNS de Azure.

En cada caso, le mostramos cómo toocreate un registro de conjunto que contiene un único registro. Hello ejemplos anteriores para los registros 'A' pueden ser adaptado toocreate conjuntos de registros de otros tipos que contiene varios registros, con metadatos, o conjuntos de registros de toocreate vacía.

No damos un toocreate ejemplo un conjunto de registros SOA, ya que se crea SOA y eliminar con cada zona DNS y no puede crearse o eliminarse por separado. Sin embargo, [Hola SOA se puede modificar, como se muestra en un ejemplo posterior](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record-set-with-a-single-record"></a>Creación de un conjunto de registros AAAA con un único registro

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a>Creación de un conjunto de registros CNAME con un único registro

> [!NOTE]
> los estándares de DNS Hello no permiten registros CNAME en vértice Hola de una zona (`-Name '@'`), ni permiten a los conjuntos de registros que contiene más de un registro.
> 
> Para más información, consulte [Registros CNAME](dns-zones-records.md#cname-records).


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a>Creación de un conjunto de registros MX con un único registro

En este ejemplo, se utiliza el nombre de conjunto de registros de hello ' @' registro toocreate un MX en vértice de la zona de hello (en este caso, "contoso.com").


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a>Creación de un conjunto de registros NS con un único registro

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a>Creación de un conjunto de registros PTR con un único registro

En este caso, ' Mi-arpa-zone.com' representa Hola zona de búsqueda inversa ARPA que representa el intervalo de IP. Cada registro PTR establecida en esta zona corresponde tooan dirección IP dentro de este intervalo IP. Hola último octeto de la dirección IP de hello dentro de este intervalo IP representado por este registro es el nombre de registro de Hello '10'.

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a>Creación de un conjunto de registros SRV con un único registro

Al crear un [conjunto de registros SRV](dns-zones-records.md#srv-records), especifique hello  *\_servicio* y  *\_protocolo* Hola nombre de conjunto de registros. No hay ninguna necesidad de tooinclude ' @' Hola registro establece el nombre al crear un registro SRV en vértice de la zona de Hola.

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a>Crear un conjunto de registros TXT con un único registro

Hello en el ejemplo siguiente se muestra cómo registrar toocreate TXT. Para obtener más información acerca de la longitud de cadena máxima Hola admitida en registros TXT, consulte [registros TXT](dns-zones-records.md#txt-records).

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a>Recuperación de un conjunto de registros

tooretrieve un conjunto de registros existente, utilice `Get-AzureRmDnsRecordSet`. Este cmdlet devuelve un objeto local que representa Hola conjunto de registros de DNS de Azure.

Al igual que con `New-AzureRmDnsRecordSet`, debe ser el nombre de conjunto de registros de hello dado un *relativa* nombre, lo que significa que debe excluir el nombre de la zona de Hola. También necesitará toospecify tipo de registro de hello y zona de Hola que contiene el conjunto de registros de Hola.

Hello en el ejemplo siguiente se muestra cómo tooretrieve un conjunto de registros. En este ejemplo, la zona de Hola se especifica utilizando hello `-ZoneName` y `-ResourceGroupName` parámetros.

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Como alternativa, también puede especificar zona de hello mediante un objeto de zona que se pasan mediante hello `-Zone` parámetro.

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a>Enumeración de conjuntos de registros

También puede usar `Get-AzureRmDnsZone` conjuntos de registros de toolist en una zona, mediante la omisión de hello `-Name` o `-RecordType` parámetros.

Hello en el ejemplo siguiente se devuelve todos los registros se establece en la zona de hello:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Hello en el ejemplo siguiente se muestra cómo todos los conjuntos de un tipo determinado de registros se puede recuperar mediante la especificación de tipo de registro de Hola durante la omisión de registro de hello establece nombre:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

tooretrieve establece todos los registros con un nombre específico, a través de los tipos de registro, deberá tooretrieve todos los conjuntos de registros y, a continuación, resultados del filtro hello:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

En Hola a todos los ejemplos precedentes Hola zona puede especificar mediante el uso de Hola `-ZoneName` y `-ResourceGroupName`parámetros (como se muestra), o mediante la especificación de un objeto de zona:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a>Agregar un registro tooan existente de conjunto de registros

conjunto de tooadd un registro existente de registro tooan, siga Hola siga tres pasos:

1. Obtener el conjunto de registros existente Hola

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Agregar Hola nuevo registro toohello local conjunto de registros. Esta operación se realiza sin conexión.

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Confirmar Hola cambio posterior toohello servicio DNS de Azure. 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

Usar `Set-AzureRmDnsRecordSet` *reemplaza* Hola existente conjunto de registros de DNS de Azure (y todos los registros que lo contiene) con el conjunto de registros de hello especificado. [Comprobaciones de eTag](dns-zones-records.md#etags) sirven cambios simultáneos tooensure no se sobrescriben. Puede usar Hola opcional `-Overwrite` cambiar toosuppress estas comprobaciones.

Esta secuencia de operaciones también puede ser *canaliza*, lo que significa que se pasa el objeto de conjunto de registros de hello mediante canalización hello, en lugar de pasarlo como un parámetro:

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

ejemplos de Hello anteriores muestran cómo establece tooadd un registro existente de 'A' tooan registros de tipo 'A'. Una secuencia de operaciones similar está tooadd usa registros toorecord conjuntos de otros tipos, sustituyendo hello `-Ipv4Address` parámetro de `Add-AzureRmDnsRecordConfig` con otro tipo de registro de tooeach específico de parámetros. Hello parámetros para cada tipo de registro se Hola igual que para hello `New-AzureRmDnsRecordConfig` cmdlet, tal y como se muestra en [ejemplos adicionales de tipo de registro](#additional-record-type-examples) anteriormente.

Los conjuntos de registros de tipo "CNAME" o "SOA" no pueden contener más de un registro. Esta restricción surge de los estándares de DNS Hola. No es una limitación de Azure DNS.

## <a name="remove-a-record-from-an-existing-record-set"></a>Eliminación de un registro de un conjunto de registros existente

Hola proceso tooremove un registro de un conjunto de registros es similar tooadd de proceso de toohello un registro tooan existente grabar conjunto:

1. Obtener el conjunto de registros existente Hola

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Quitar el registro de hello de objeto de conjunto de registros local Hola. Esta operación se realiza sin conexión. registro de Hello que se va a quitar debe ser una coincidencia exacta con un registro existente en todos los parámetros.

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Confirmar Hola cambio posterior toohello servicio DNS de Azure. Hola de uso opcional `-Overwrite` cambiar toosuppress [Etag comprueba](dns-zones-records.md#etags) para cambios simultáneos.

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

Hola anteriormente las último registro de hello del tooremove de secuencia de un conjunto de registros de uso no elimina el conjunto de registros de hello, en su lugar deja un conjunto de registros vacío. tooremove un conjunto de registros por completo, vea [eliminar un conjunto de registros](#delete-a-record-set).

De igual forma tooadding registros tooa conjunto de registros, secuencia de Hola de tooremove operaciones también se puede canalizar un conjunto de registros:

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Se admiten diferentes tipos de registros al pasar parámetros específicos del tipo adecuado de hello demasiado`Remove-AzureRmDnsRecordSet`. Hello parámetros para cada tipo de registro se Hola igual que para hello `New-AzureRmDnsRecordConfig` cmdlet, tal y como se muestra en [ejemplos adicionales de tipo de registro](#additional-record-type-examples) anteriormente.


## <a name="modify-an-existing-record-set"></a>Modificación de un conjunto de registros existente

Hola los pasos para modificar un conjunto de registros existente son similares toohello pasos que seguir al agregar o quitar los registros de un conjunto de registros:

1. Recuperar registro existente de hello establecer mediante `Get-AzureRmDnsRecordSet`.
2. Modifique el objeto de conjunto de registros local Hola por:
    * Agregue o quite registros.
    * Cambiar los parámetros de Hola de registros existentes
    * Cambiar el registro de hello del conjunto de metadatos y la hora toolive (TTL)
3. Confirmar cambios mediante el uso de hello `Set-AzureRmDnsRecordSet` cmdlet. Esto *reemplaza* Hola existente conjunto de registros de DNS de Azure con el conjunto de registros de hello especificado.

Cuando se usa `Set-AzureRmDnsRecordSet`, [Etag comprueba](dns-zones-records.md#etags) sirven cambios simultáneos tooensure no se sobrescriben. Puede usar Hola opcional `-Overwrite` cambiar toosuppress estas comprobaciones.

### <a name="tooupdate-a-record-in-an-existing-record-set"></a>establece tooupdate un registro en un registro existente

En este ejemplo, cambiamos la dirección IP de Hola de un registro "A" existente:

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a>toomodify un registro SOA

No se puede agregar o quitar registros de hello creado automáticamente el registro SOA establecido en vértice de la zona de hello (`-Name "@"`, incluidas las comillas). Sin embargo, puede modificar cualquiera de los parámetros de hello en hello registro SOA (excepto el "Host") y registro de hello establecer TTL.

Hola siguiente ejemplo se muestra cómo hello toochange *correo electrónico* propiedad de hello registro SOA:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>registros de toomodify NS en vértice de la zona de Hola

registro de NS de Hello establecido en vértice de la zona de Hola se crea automáticamente con cada zona DNS. Contiene los nombres de Hola de zona de hello Azure DNS nombre servidores toohello asignado.

Puede agregar nombre adicionales servidores toothis NS conjunto de registros, toosupport alojar conjuntamente dominios con más de un proveedor DNS. También puede modificar Hola TTL y los metadatos para este conjunto de registros. Sin embargo, no se puede quitar o modificar servidores de nombres DNS de Azure previamente rellenados Hola.

Tenga en cuenta que esto se aplica solo toohello NS conjunto de registros en vértice de la zona de Hola. Otros conjuntos de registros NS en su zona (como las zonas secundarias de toodelegate usado) pueden modificarse sin restricción.

Hola de ejemplo siguiente muestra cómo tooadd establece de un registro de NS de toohello de servidor de nombres adicionales en vértice de la zona de hello:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a>metadatos de conjunto de registros de toomodify

[Metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) pueden ser datos específicos de la aplicación de tooassociate usado con cada conjunto de registros, como pares de clave-valor.

Hello en el ejemplo siguiente se muestra cómo establecen toomodify Hola metadatos de un registro existente:

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a>Eliminación de un conjunto de registros

Conjuntos de registros pueden eliminarse mediante el uso de hello `Remove-AzureRmDnsRecordSet` cmdlet. Eliminación de un conjunto de registros, también elimina todas las entradas de conjunto de registros de Hola.

> [!NOTE]
> No se puede eliminar Hola SOA y NS conjuntos de registros en vértice de la zona de hello (`-Name '@'`).  DNS de Azure crea estos operación automáticamente cuando zona Hola se creó y elimina automáticamente cuando se elimina la zona de Hola.

Hello en el ejemplo siguiente se muestra cómo toodelete un conjunto de registros. En este ejemplo, el nombre del conjunto de registros de hello, tipo de conjunto de registros, nombre de la zona y grupo de recursos se cada especifican explícitamente.

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Como alternativa, se puede especificar el conjunto de registros de Hola por nombre y tipo, y Hola especificados mediante un objeto de la zona:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

Como una tercera opción propio conjunto de registros de hello pueden especificarse mediante un objeto de conjunto de registros:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

Cuando se especifica toobe eliminada mediante el uso de un objeto de conjunto de registros de conjunto de registros de hello [Etag comprueba](dns-zones-records.md#etags) sirven cambios simultáneos tooensure no se eliminan. Puede usar Hola opcional `-Overwrite` cambiar toosuppress estas comprobaciones.

También se puede canalizar el objeto de conjunto de registros de Hello en lugar de que se pasa como parámetro:

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a>Mensajes de confirmación

Hola `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, y `Remove-AzureRmDnsRecordSet` todos los cmdlets admiten mensajes de confirmación.

Cada cmdlet pide confirmación si hello `$ConfirmPreference` variable de preferencia de PowerShell tiene un valor de `Medium` o inferior. Desde el valor predeterminado de Hola para `$ConfirmPreference` es `High`, esos mensajes no tienen al usar la configuración de PowerShell de hello predeterminada.

Puede invalidar Hola actual `$ConfirmPreference` configuración mediante hello `-Confirm` parámetro. Si especifica `-Confirm` o `-Confirm:$True` , Hola cmdlet solicita confirmación antes de que se ejecuta. Si especifica `-Confirm:$False` , Hola cmdlet no pide confirmación. 

Para más información sobre `-Confirm` y `$ConfirmPreference`, consulte [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Acerca de las variables de preferencias).

## <a name="next-steps"></a>Pasos siguientes

Más información sobre [zonas y registros en Azure DNS](dns-zones-records.md).
<br>
Obtenga información acerca de cómo demasiado[proteger sus zonas y registros](dns-protect-zones-recordsets.md) cuando se usa DNS de Azure.
<br>
Hola de revisión [documentación de referencia de PowerShell de DNS de Azure](/powershell/module/azurerm.dns).
