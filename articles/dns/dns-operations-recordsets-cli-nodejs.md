---
title: registros DNS de aaaManage en DNS de Azure mediante Hola 1.0 de CLI de Azure | Documentos de Microsoft
description: "Administración de conjuntos de registros y registros DNS en DNS de Azure al hospedar dominios en DNS de Azure. Todos los comandos de la CLI 1.0 para operaciones en conjuntos de registros y registros."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a>Administrar los registros DNS de DNS de Azure con hello Azure CLI 1.0

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [CLI de Azure 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [CLI de Azure 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Este artículo muestra cómo toomanage registros DNS para la zona DNS mediante el uso de Hola multiplataforma Azure interfaz de línea de comandos (CLI), que está disponible para Windows, Mac y Linux. También puede administrar los registros DNS mediante [Azure PowerShell](dns-operations-recordsets.md) o hello [portal de Azure](dns-operations-recordsets-portal.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello

Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

* [Azure 1.0 de CLI](dns-operations-recordsets-cli-nodejs.md) -nuestro CLI para modelos de implementación de administración de recursos y clásico Hola.
* [Azure 2.0 CLI](dns-operations-recordsets-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola.

ejemplos de Hello en este artículo se supone que ya está [instalado hello Azure CLI 1.0, firmado y ha creado una zona DNS](dns-operations-dnszones-cli-nodejs.md).

## <a name="introduction"></a>Introducción

Antes de crear los registros DNS en DNS de Azure, primero debe toounderstand cómo Azure DNS organiza los registros DNS en conjuntos de registros de DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Para más información sobre los registros DNS en Azure DNS, consulte [DNS zones and records](dns-zones-records.md) (Zonas y registros DNS).

## <a name="create-a-dns-record"></a>Creación de un registro de DNS

toocreate un registro DNS, usar hello `azure network dns record-set add-record` comando. Para obtener ayuda, consulte `azure network dns record-set add-record -h`.

Al crear un registro, necesita el nombre de grupo de recursos de hello toospecify, nombre de la zona, conjunto de registros, nombre, tipo de registro de hello y detalles de Hola de registro de hello va a crear. Hello dado el nombre de conjunto de registros debe ser un *relativa* nombre, lo que significa que debe excluir el nombre de la zona de Hola.

Si aún no existe el conjunto de registros de hello, este comando lo crea automáticamente. Si ya existe un conjunto de registros de hello, este agregue una comando Hola registro que especifique el conjunto de registros existente toohello.

Si se crea un conjunto de registros, se utiliza el valor predeterminado del período de vida (3600). Para obtener instrucciones sobre cómo toouse TTLs diferentes, consulte [crear un conjunto de registros de DNS](#create-a-dns-record-set).

Hello en el ejemplo siguiente se crea un registro denominado *www* en zona de hello *contoso.com* en grupo de recursos de hello *MyResourceGroup*. Hola dirección IP de un registro es de hello *1.2.3.4*.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

toocreate un registro en el vértice de Hola de zona de hello (en este caso, "contoso.com"), use el nombre de registro de hello "@", incluidas las comillas de hello:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>Creación de un conjunto de registros de DNS

Hola por encima de los ejemplos, registro DNS de Hola se cualquier agregado tooan existente de conjunto de registros, o se creó el conjunto de registros de hello *implícitamente*. También puede crear el conjunto de registros de hello *explícitamente* antes de que se agregan registros tooit. DNS de Azure es compatible con conjuntos de registros 'empty', que pueden actuar como un marcador de posición tooreserve un nombre DNS antes de crear los registros DNS. Conjuntos de registros vacíos son visibles en hello Azure DNS control plano, pero no aparecen en los servidores de nombres DNS de Azure Hola.

Conjuntos de registros se crean mediante hello `azure network dns record-set create` comando. Para obtener ayuda, consulte `azure network dns record-set create -h`.

Crear registro de hello establecen explícitamente permite toospecify propiedades de conjunto de registros como hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) y metadatos. [Metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) pueden ser datos específicos de la aplicación de tooassociate usado con cada conjunto de registros, como pares de clave-valor.

Hello en el ejemplo siguiente se crea un registro vacío establece con un TTL de 60 segundos, mediante el uso de hello `--ttl` parámetro (forma abreviada `-l`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

Hello en el ejemplo siguiente se crea un conjunto de registros con dos entradas de metadatos, "departamento = Finanzas" y "entorno = producción", mediante el uso de hello `--metadata` parámetro (forma abreviada `-m`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

Tras haber creado un conjunto de registros vacío, se podrán añadir el registro mediante `azure network dns record-set add-record`, como se describe en [Creación de un registro de DNS](#create-a-dns-record).

## <a name="create-records-of-other-types"></a>Creación de registros de otros tipos

Después de ver en detalle cómo registros toocreate 'A', Hola siguientes ejemplos se muestra cómo se admite toocreate registro de otros tipos de registros DNS de Azure.

parámetros de Hello usar registro de hello toospecify datos varían según el tipo de saludo del registro de hello. Por ejemplo, para un registro de tipo "A", especificar dirección Hola IPv4 con el parámetro hello `-a <IPv4 address>`. Hola parámetros para cada tipo de registro puede aparecer con `azure network dns record-set add-record -h`.

En cada caso, le mostramos cómo toocreate un único registro. registro de Hello es agregado toohello existente de conjunto de registros o un conjunto de registros se crea de forma implícita. Para obtener más información sobre cómo crear conjuntos de registros y definir explícitamente los parámetros de un conjunto de registros, consulte [Creación de un conjunto de registros de DNS](#create-a-dns-record-set).

No damos un toocreate ejemplo un conjunto de registros SOA, ya que se crea SOA y eliminar con cada zona DNS y no puede crearse o eliminarse por separado. Sin embargo, [Hola SOA se puede modificar, como se muestra en un ejemplo posterior](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record"></a>Creación de un registro AAAA

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>Creación de un registro CNAME

> [!NOTE]
> los estándares de DNS Hello no permiten registros CNAME en vértice Hola de una zona (`-Name "@"`), ni permiten a los conjuntos de registros que contiene más de un registro.
> 
> Para más información, consulte [Registros CNAME](dns-zones-records.md#cname-records).

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>Creación de un registro MX

En este ejemplo, se utiliza el nombre de conjunto de registros de Hola "@" hello toocreate registro MX en vértice de la zona de hello (en este caso, "contoso.com").

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>Creación de un registro NS

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>Creación de un registro PTR

En este caso, ' Mi-arpa-zone.com' representa Hola zona ARPA que representa el intervalo de IP. Cada registro PTR establecida en esta zona corresponde tooan dirección IP dentro de este intervalo IP.  Hola último octeto de la dirección IP de hello dentro de este intervalo IP representado por este registro es el nombre de registro de Hello '10'.

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a>Creación de un registro SRV

Al crear un [conjunto de registros SRV](dns-zones-records.md#srv-records), especifique hello  *\_servicio* y  *\_protocolo* Hola nombre de conjunto de registros. No hay ninguna necesidad de tooinclude "@" Hola registro establece el nombre al crear un registro SRV en vértice de la zona de Hola.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a>Creación de un registro TXT

Hello en el ejemplo siguiente se muestra cómo registrar toocreate TXT. Para obtener más información acerca de la longitud de cadena máxima Hola admitida en registros TXT, consulte [registros TXT](dns-zones-records.md#txt-records).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a>Recuperación de un conjunto de registros

tooretrieve un conjunto de registros existente, utilice `azure network dns record-set show`. Para obtener ayuda, consulte `azure network dns record-set show -h`.

Al crear un registro o un conjunto de registros, registro de hello establecer nombre dado debe ser un *relativa* nombre, lo que significa que debe excluir el nombre de la zona de Hola. También necesita toospecify tipo de registro de hello, zona Hola que contiene el registro de hello establecido y Hola grupo de recursos que contiene la zona de Hola.

Hello en el ejemplo siguiente se recupera el registro de hello *www* de un tipo de zona *contoso.com* en grupo de recursos *MyResourceGroup*:

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a>Enumeración de conjuntos de registros

Puede enumerar todos los registros de una zona DNS mediante hello `azure network dns record-set list` comando. Para obtener ayuda, consulte `azure network dns record-set list -h`.

Este ejemplo devuelve todos los registros se establece en la zona de hello *contoso.com*, en el grupo de recursos *MyResourceGroup*independientemente del nombre o tipo de registro:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

Este ejemplo devuelve todos los conjuntos de registros que coinciden con hello tiene el tipo de registro (en este caso, 'A' registros):

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a>Agregar un registro tooan existente de conjunto de registros

Puede usar `azure network dns record-set add-record` ambas toocreate un registro en un nuevo registro configurado o tooadd un registro existente tooan registros.

Para obtener más información, consulte las secciones [Creación de un registro de DNS](#create-a-dns-record) y [Creación de registros de otros tipos](#create-records-of-other-types).

## <a name="remove-a-record-from-an-existing-record-set"></a>Quite un registro de un conjunto de registros existente.

grabar tooremove un DNS de un conjunto de registros existente, use `azure network dns record-set delete-record`. Para obtener ayuda, consulte `azure network dns record-set delete-record -h`.

Este comando elimina un registro de DNS de un conjunto de registros. Si se elimina el último registro de hello en un conjunto de registros, es el propio conjunto de registros de hello **no** eliminado. En su lugar, se conservará un conjunto de registros vacío. registro de hello toodelete establecido en su lugar, consulte [eliminar un conjunto de registros](#delete-a-record-set).

Necesita toospecify hello toobe registro eliminado y la zona de Hola debe eliminarse, con Hola mismos parámetros que al crear un registro mediante `azure network dns record-set add-record`. Estos parámetros se describen en las secciones [Creación de un registro de DNS](#create-a-dns-record) y [Creación de registros de otros tipos](#create-records-of-other-types).

Este comando solicita confirmación. Este mensaje se puede suprimir con hello `--quiet` cambiar (forma abreviada `-q`).

Después de eliminaciones de ejemplo de Hola Hola un registro con valor '1.2.3.4' del registro de hello conjunto con nombre *www* en zona de hello *contoso.com*, en el grupo de recursos de hello *MyResourceGroup*. se suprime la pregunta de confirmación de Hola.

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a>Modificación de un conjunto de registros existente

Cada conjunto de registros contiene un [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadatos](dns-zones-records.md#tags-and-metadata)y los registros de DNS. Hello siguientes secciones se explica cómo toomodify de estas propiedades.

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>toomodify un registro A, AAAA, MX, NS, PTR, SRV o TXT

toomodify un registro existente de tipo A, AAAA, MX, NS, PTR, SRV o TXT, primero debe agregar un nuevo registro y, a continuación, un registro existente de Hola de eliminación. Para obtener instrucciones detalladas sobre cómo toodelete y agregar registros, vea hello las secciones anteriores de este artículo.

Hola de ejemplo siguiente muestra cómo toomodify un registro de 'A', de IP dirección 1.2.3.4 tooIP direccionan 5.6.7.8:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a>toomodify un registro CNAME

usar un registro CNAME, toomodify `azure network dns record-set add-record` tooadd Hola nuevo valor del registro. A diferencia de otros tipos de registros, un conjunto de registros CNAME solo puede contener un único registro. Por lo tanto, es el registro existente de hello *reemplazado* cuando se agrega el nuevo registro de hello y no es necesario toobe eliminar por separado.  También será tooaccept solicitada este reemplazo.

ejemplo Hello modifica conjunto de registros CNAME de hello *www* en zona de hello *contoso.com*, en el grupo de recursos *MyResourceGroup*, toopoint demasiado 'www.fabrikam.net' en lugar de su valor existente:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a>toomodify un registro SOA

Use `azure network dns record-set set-soa-record` toomodify hello SOA para una zona DNS especificada. Para obtener ayuda, consulte `azure network dns record-set set-soa-record -h`.

Hello en el ejemplo siguiente se muestra cómo registrar propiedad tooset Hola "email" Hola SOA de zona de hello *contoso.com* en grupo de recursos de hello *MyResourceGroup*:

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a>registros de toomodify NS en vértice de la zona de Hola

registro de NS de Hello establecido en vértice de la zona de Hola se crea automáticamente con cada zona DNS. Contiene los nombres de Hola de zona de hello Azure DNS nombre servidores toohello asignado.

Puede agregar nombre adicionales servidores toothis NS conjunto de registros, toosupport alojar conjuntamente dominios con más de un proveedor DNS. También puede modificar Hola TTL y los metadatos para este conjunto de registros. Sin embargo, no se puede quitar o modificar servidores de nombres DNS de Azure previamente rellenados Hola.

Tenga en cuenta que esto se aplica solo toohello NS conjunto de registros en vértice de la zona de Hola. Otros conjuntos de registros NS en su zona (como las zonas secundarias de toodelegate usado) pueden modificarse sin restricción.

Hola de ejemplo siguiente muestra cómo tooadd establece de un registro de NS de toohello de servidor de nombres adicionales en vértice de la zona de hello:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a>establece toomodify Hola TTL de un registro existente

establece toomodify Hola TTL de un registro existente, use `azure network dns record-set set`. Para obtener ayuda, consulte `azure network dns record-set set -h`.

Hola de ejemplo siguiente muestra cómo toomodify un conjunto de registros TTL, en este caso a too60 segundos:

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a>toomodify Hola metadatos de un conjunto de registros existente

[Metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) pueden ser datos específicos de la aplicación de tooassociate usado con cada conjunto de registros, como pares de clave-valor. establecen toomodify Hola metadatos de un registro existente, use `azure network dns record-set set`. Para obtener ayuda, consulte `azure network dns record-set set -h`.

Hello en el ejemplo siguiente se muestra cómo toomodify un conjunto de registros con dos entradas de metadatos, "departamento = Finanzas" y "entorno = producción", mediante el uso de hello `--metadata` parámetro (forma abreviada `-m`). Tenga en cuenta que los metadatos existentes *reemplaza* por valores de hello dados.

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a>Eliminación de un conjunto de registros

Conjuntos de registros pueden eliminarse mediante el uso de hello `azure network dns record-set delete` comando. Para obtener ayuda, consulte `azure network dns record-set delete -h`. Eliminación de un conjunto de registros, también elimina todas las entradas de conjunto de registros de Hola.

> [!NOTE]
> No se puede eliminar Hola SOA y NS conjuntos de registros en vértice de la zona de hello (`-Name "@"`).  Se crean automáticamente cuando se creó zona hello y se eliminan automáticamente cuando se elimina la zona de Hola.

Hello en el ejemplo siguiente se elimina conjunto con nombre de registros de hello *www* de un tipo de zona de hello *contoso.com* en grupo de recursos *MyResourceGroup*:

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

Son la operación de eliminación de hello tooconfirm solicitadas. toosuppress este símbolo del sistema, use hello `--quiet` cambiar (forma abreviada `-q`).

## <a name="next-steps"></a>Pasos siguientes

Más información sobre [zonas y registros en Azure DNS](dns-zones-records.md).
<br>
Obtenga información acerca de cómo demasiado[proteger sus zonas y registros](dns-protect-zones-recordsets.md) cuando se usa DNS de Azure.
