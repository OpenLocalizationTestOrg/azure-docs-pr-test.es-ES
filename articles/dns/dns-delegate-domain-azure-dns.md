---
title: aaaDelegate su tooAzure de dominio DNS | Documentos de Microsoft
description: "Comprender cómo toochange delegación del dominio y el uso de DNS de Azure nombre servidores tooprovide dominio hospeda."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a>Delegar un tooAzure de dominio DNS

DNS de Azure permite toohost una zona DNS y administrar los registros DNS de Hola para un dominio de Azure. En el orden de las consultas DNS para un tooreach de dominio DNS de Azure, el dominio de hello tiene toobe delegar tooAzure DNS de dominio primario de Hola. Tenga en cuenta el DNS de Azure no es un registrador de dominios de Hola. Este artículo se explica cómo toodelegate su tooAzure de dominio DNS.

En el caso de adquiridas a través de un registrador de dominios, el registrador ofrece Hola opción tooset estos registros NS. No es necesario tooown una toocreate de dominio una zona DNS con ese nombre de dominio en DNS de Azure. Sin embargo, deberá tooown Hola dominio tooset seguridad hello tooAzure de delegación DNS con el registrador de Hola.

Por ejemplo, supongamos que compra dominio hello 'contoso.net' y crea una zona con nombre hello 'contoso.net' en DNS de Azure. Como propietario de hello del dominio de hello, el registrador ofrece que Hola direcciones del servidor de nombre de opción tooconfigure Hola (es decir, registros de hello NS) para su dominio. registrador de Hello almacena estos registros NS en dominio primario de hello, en este caso '.net'. Los clientes alrededor de Hola a todos, a continuación, pueden ser dirigido tooyour dominio en la zona DNS de Azure al tratar de tooresolve registros DNS en 'contoso.net'.

## <a name="create-a-dns-zone"></a>Creación de una zona DNS

1. Inicie sesión en toohello portal de Azure
1. En el menú del concentrador hello, haga clic en y haga clic en **nuevo > redes >** y, a continuación, haga clic en **zona DNS** hoja de zona de DNS crear de tooopen Hola.

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. En hello **zona DNS crear** escriba Hola después valores hoja, haga clic en **crear**:

   | **Configuración** | **Valor** | **Detalles** |
   |---|---|---|
   |**Name**|contoso.net|nombre de Hola de zona DNS de Hola|
   |**Suscripción**|[Su suscripción]|Seleccione una puerta de enlace de suscripción toocreate Hola aplicación en.|
   |**Grupos de recursos**|**Crear nuevo:** contosoRG|Cree un grupo de recursos. nombre de grupo de recursos de Hello debe ser único dentro de la suscripción de Hola que ha seleccionado. más información acerca de los grupos de recursos, leer hello toolearn [el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artículo de información general.|
   |**Ubicación**|Oeste de EE. UU.||

> [!NOTE]
> grupo de recursos de Hello hace referencia la ubicación de toohello Hola del grupo de recursos y no tiene ningún efecto en la zona DNS de Hola. ubicación de la zona DNS Hola siempre es "global" y no se muestra.

## <a name="retrieve-name-servers"></a>Recuperación de los servidores de nombres

Antes de que puede delegar su tooAzure de zona DNS de DNS, primero debe tooknow Hola nombre nombres de los servidores de la zona. El DNS de Azure asigna los servidores de nombres de un grupo cada vez que se crea una zona.

1. Con zona DNS de hello creada, en el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**. Haga clic en hello **contoso.net** zona DNS en hello **todos los recursos** hoja. Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir **contoso.net** Hola filtro por nombre... puerta de enlace de cuadro tooeasily acceso Hola aplicaciones. 

1. Recuperar los servidores de nombres de Hola de hoja de zona DNS de Hola. En este ejemplo, zona hello 'contoso.net' se ha asignado los servidores de nombres ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', y ' ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

DNS de Azure crea automáticamente los registros NS autoritativos en la zona que contiene servidores de nombres asignado de Hola.  nombres de servidor de nombres de hello toosee a través de Azure PowerShell o CLI de Azure, simplemente necesita tooretrieve estos registros.

Hello en los ejemplos siguientes también proporcionan pasos Hola servidores de nombres de hello tooretrieve para una zona de DNS de Azure con PowerShell y la CLI de Azure.

### <a name="powershell"></a>PowerShell

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

Hola siguiente ejemplo es la respuesta de Hola.

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a>CLI de Azure

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

Hola siguiente ejemplo es la respuesta de Hola.

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a>Dominio de Hola de delegado

Ahora que se crea la zona DNS de Hola y tiene servidores de nombres de hello, dominio primario de hello debe toobe actualizado con servidores de nombres DNS de Azure Hola. Cada registrador tiene sus propios registros DNS administración herramientas toochange Hola nombre servidor para un dominio. En la página de administración de DNS del registrador de hello, editar los registros NS hello y reemplace los registros NS Hola por hello las que DNS de Azure creado.

Al delegar un tooAzure de dominio DNS, debe usar nombres de servidor de nombre de hello proporcionados por DNS de Azure. Se recomienda toouse todos los cuatro nombres para los nombres de servidor, independientemente del nombre de Hola de su dominio. Delegación de dominio no requiere toouse de nombre de servidor de nombre de Hola Hola mismo dominio de nivel superior que el dominio.

No se deben usar 'búsqueda de registros' toopoint toohello Azure nombre IP direcciones de servidor DNS, puesto que estas direcciones IP pueden cambiar en el futuro. Las delegaciones que usan nombres de servidor en su propia zona (a veces denominados "servidores DNS personalizados") no se admiten de momento en DNS de Azure.

## <a name="verify-name-resolution-is-working"></a>Comprobación del funcionamiento de la resolución de nombres

Después de completar la delegación hello, puede comprobar que la resolución de nombres funciona con una herramienta como 'nslookup' tooquery Hola registro SOA de la zona (que se crea automáticamente cuando se crea la zona de hello).

No tiene servidores de nombres DNS de Azure de toospecify hello, si se ha configurado la delegación Hola correctamente, Hola DNS resolución proceso normal busca automáticamente los servidores de nombres de Hola.

```
nslookup -type=SOA contoso.com
```

Hola te mostramos una respuesta de ejemplo de Hola anterior comando:

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a>Delegación de subdominios en Azure DNS

Si desea tooset una zona secundaria independiente, puede delegar un subdominio en DNS de Azure. Por ejemplo, después de configurar y delegado 'contoso.net' en el DNS de Azure, suponga que le gustaría tooset una zona secundaria independiente, 'partners.contoso.net'.

1. Crear zona de secundarios de hello 'partners.contoso.net' en el DNS de Azure.
2. Buscar registros NS autoritativos de hello en hello secundarios zona tooobtain Hola servidores de nombres donde se hospeda Hola secundarios zona de DNS de Azure.
3. Delegar la zona secundaria de hello mediante la configuración de los registros NS en zona primaria de Hola que señala la zona secundaria de toohello.

### <a name="create-a-dns-zone"></a>Creación de una zona DNS

1. Inicie sesión en toohello portal de Azure
1. En el menú del concentrador hello, haga clic en y haga clic en **nuevo > redes >** y, a continuación, haga clic en **zona DNS** hoja de zona de DNS crear de tooopen Hola.

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. En hello **zona DNS crear** escriba Hola después valores hoja, haga clic en **crear**:

   | **Configuración** | **Valor** | **Detalles** |
   |---|---|---|
   |**Name**|partners.contoso.net|nombre de Hola de zona DNS de Hola|
   |**Suscripción**|[Su suscripción]|Seleccione una puerta de enlace de suscripción toocreate Hola aplicación en.|
   |**Grupos de recursos**|**Usar existente:** contosoRG|Cree un grupo de recursos. nombre de grupo de recursos de Hello debe ser único dentro de la suscripción de Hola que ha seleccionado. más información acerca de los grupos de recursos, leer hello toolearn [el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artículo de información general.|
   |**Ubicación**|Oeste de EE. UU.||

> [!NOTE]
> grupo de recursos de Hello hace referencia la ubicación de toohello Hola del grupo de recursos y no tiene ningún efecto en la zona DNS de Hola. ubicación de la zona DNS Hola siempre es "global" y no se muestra.

### <a name="retrieve-name-servers"></a>Recuperación de los servidores de nombres

1. Con zona DNS de hello creada, en el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**. Haga clic en hello **partners.contoso.net** zona DNS en hello **todos los recursos** hoja. Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir **partners.contoso.net** Hola filtro por nombre... zona DNS de cuadro tooeasily acceso Hola.

1. Recuperar los servidores de nombres de Hola de hoja de zona DNS de Hola. En este ejemplo, zona hello 'contoso.net' se ha asignado los servidores de nombres ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', y ' ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

DNS de Azure crea automáticamente los registros NS autoritativos en la zona que contiene servidores de nombres asignado de Hola.  nombres de servidor de nombres de hello toosee a través de Azure PowerShell o CLI de Azure, simplemente necesita tooretrieve estos registros.

### <a name="create-name-server-record-in-parent-zone"></a>Creación de un registro de servidor de nombres en la zona primaria

1. Navegue toohello **contoso.net** zona DNS en hello portal de Azure.
1. Haga clic en **+ Conjunto de registros**.
1. En hello **Agregar conjunto de registros** hoja, escriba Hola después de valores, a continuación, haga clic en **Aceptar**:

   | **Configuración** | **Valor** | **Detalles** |
   |---|---|---|
   |**Name**|asociados|nombre de Hola de zona DNS secundarios Hola|
   |**Tipo**|NS|Utilice NS para los registros del servidor de nombres.|
   |**TTL**|1|Tiempo toolive.|
   |**Unidad de TTL**|Horas|establece toohours toolive unidad de tiempo|
   |**SERVIDOR DE NOMBRES**|{servidores de nombres de la zona partners.contoso.net}|Escriba todos los 4 hello de servidores de nombres de zona partners.contoso.net. |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a>Delegación de subdominios en Azure DNS con otras herramientas

Hello en los ejemplos siguientes proporcionan pasos hello toodelegate subdominios en DNS de Azure con PowerShell y la CLI:

#### <a name="powershell"></a>PowerShell

Hola PowerShell ejemplo siguiente muestra cómo funciona. Hola mismos pasos se pueden ejecutar a través del portal de Azure de Hola o a través de Hola CLI de Azure entre plataformas.

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

Use `nslookup` tooverify que todo está configurado correctamente mediante la búsqueda Hola registro SOA de zona secundaria de Hola.

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a>CLI de Azure

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

Recuperar los servidores de nombres de Hola para hello `partners.contoso.net` zona desde la salida de hello.

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Crear conjunto de registros de Hola y los registros NS para cada servidor de nombres.

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a>Eliminación de todos los recursos

toodelete todos los recursos que se crean en este artículo, Hola completa pasos:

1. En el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**. Haga clic en hello **contosorg** grupo de recursos en hello todos los módulos de recursos. Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir **contosorg** en hello **filtrar por nombre...** grupo de recursos de cuadro tooeasily acceso Hola.
1. Hola **contosorg** hoja, haga clic en hello **eliminar** botón.
1. Hello portal requiere tootype Hola nombre del tooconfirm de grupo de recursos de Hola que desea que toodelete lo. Tipo de *contosorg* nombre de grupo de recursos de hello, a continuación, haga clic en **eliminar**. Al eliminar un grupo de recursos eliminan todos los recursos en el grupo de recursos de hello, por lo que siempre puede tooconfirm seguro de contenido de Hola de un grupo de recursos antes de eliminarlo. portal de Hello elimina todos los recursos incluidos en el grupo de recursos de hello, a continuación, elimina el grupo de recursos de hello propio. Este proceso tarda varios minutos.

## <a name="next-steps"></a>Pasos siguientes

[Administración de zonas DNS](dns-operations-dnszones.md)

[Administración de registros DNS](dns-operations-recordsets.md)
