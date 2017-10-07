---
title: "aaaHosting invertir zonas de búsqueda DNS en el DNS de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo Hola de toouse DNS de Azure toohost invertir zonas de búsqueda DNS para los intervalos de IP"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a>Alojamiento de zonas de búsqueda inversa DNS en DNS de Azure

Este artículo explica cómo toohost Hola invertir zonas de búsqueda DNS para los intervalos IP asignadas en DNS de Azure. intervalos IP de Hello representados por la zona de búsqueda inversa de hello deben asignarse tooyour organización, normalmente por su ISP.

tooconfigure inversa de DNS para la propiedad de Azure IP dirección asignada tooyour servicio de Azure, consulte [configurar la búsqueda inversa de Hola para direcciones IP que Hola asignan tooyour servicio de Azure](dns-reverse-dns-for-azure-services.md).

Antes de leer este artículo, debe estar familiarizado con [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md).

Este artículo le guiará a través de hello pasos toocreate la primera zona de búsqueda inversa DNS y el registro mediante Hola portal de Azure, PowerShell de Azure, Azure CLI 1.0 o 2.0 de CLI de Azure.

## <a name="create-a-reverse-lookup-dns-zone"></a>Creación de una zona de búsqueda inversa DNS

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com)
1. En el menú del concentrador hello, haga clic en y haga clic en **New** > **red** > y, a continuación, haga clic en **zona DNS** tooopen hello **zona de DNS crear**hoja.

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. En hello **zona DNS crear** hoja, el nombre de la zona DNS. nombre Hola de zona de Hola está diseñada de forma diferente para los prefijos de IPv4 e IPv6. Usar cualquier instrucciones Hola de [IPV4](#ipv4) o [IPv6](#ipv6) tooname su zona. Cuando haya terminado haga clic en **crear** zona de hello toocreate.

### <a name="ipv4"></a>IPv4

nombre de Hola de una zona de búsqueda inversa IPv4 se basa en el intervalo IP de hello representa. Debería ser Hola siguiendo el formato: `<IPv4 network prefix in reverse order>.in-addr.arpa`. Para ver ejemplos, consulte [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md#ipv4).

> [!NOTE]
> Al crear interdominios sin clases zonas de búsqueda inversas de DNS en DNS de Azure, debe usar un guión (`-`) en lugar de una barra diagonal ('/ ') en nombre de la zona de Hola.
>
> Por ejemplo, para hello IP intervalo 192.0.2.128/26, debe utilizar `128-26.2.0.192.in-addr.arpa` como nombre de la zona de hello en lugar de `128/26.2.0.192.in-addr.arpa`.
>
> Esto es porque, aunque ambos son compatibles con los estándares de DNS hello, nombres que contengan diagonal Hola la zona DNS (`/`) caracteres no se admiten en DNS de Azure.

Hello en el ejemplo siguiente se muestra cómo toocreate 'Clase C' invertir la zona DNS con el nombre `2.0.192.in-addr.arpa` en DNS de Azure a través de hello portal de Azure:

 ![Creación de una zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

Hola 'Ubicación del grupo de recursos' define la ubicación de hello para el grupo de recursos de hello y no tiene ningún efecto en la zona DNS de Hola. ubicación de la zona DNS Hola siempre es 'global' y no se muestra.

Hello en los ejemplos siguientes muestran cómo toocomplete esta tarea con hello CLI de Azure y Azure PowerShell:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>CLI de Azure 1.0

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>CLI de Azure 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

Hola nombre de una zona de búsqueda inversa IPv6 debe ser Hola siguiendo el formato: `<IPv6 network prefix in reverse order>.ip6.arpa`.  Para ver ejemplos, consulte [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md#ipv6).


Hello en el ejemplo siguiente se muestra cómo toocreate una zona de búsqueda DNS inversa IPv6 denominado `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` en DNS de Azure a través de hello portal de Azure:

 ![Creación de una zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

Hola 'Ubicación del grupo de recursos' define la ubicación de hello para el grupo de recursos de hello y no tiene ningún efecto en la zona DNS de Hola. ubicación de la zona DNS Hola siempre es 'global' y no se muestra.

Hello en los ejemplos siguientes muestran cómo toocomplete esta tarea con hello CLI de Azure y Azure PowerShell:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a>CLI de Azure 1.0

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a>CLI de Azure 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a>Delegación de una zona de búsqueda inversa DNS

Al haber creado la zona de búsqueda inversa de DNS, debe asegurarse de que esa zona Hola se delega de la zona primaria de Hola. Delegación de DNS permite a Hola resolución proceso toofind Hola nombre servidores de nombres DNS hospeda la zona de búsqueda inversa de DNS. Esto permite que los servidores tooanswer DNS inversas consultas de nombres para las direcciones IP de hello en el intervalo de direcciones.

Para las zonas de búsqueda directa, el proceso de Hola de delegación de una zona DNS se describe en [delegar su tooAzure de dominio DNS](dns-delegate-domain-azure-dns.md). La delegación de zonas de búsqueda inversa funciona Hola igual. Hola única diferencia es que necesita servidores de nombres de hello tooconfigure con hello ISP que proporciona el intervalo de IP, en lugar de su registrador de nombres de dominio.

## <a name="create-a-dns-ptr-record"></a>Creación de un registro PTR DNS

### <a name="ipv4"></a>IPv4

Hello en el ejemplo siguiente se le guía a través del proceso de Hola de creación de un registro PTR en una zona DNS inversa de DNS de Azure. Para otros tipos de registro y toomodify los registros existentes, consulte [registros administrar DNS y los conjuntos de registros mediante el uso de Hola portal de Azure](dns-operations-recordsets-portal.md).

1.  En parte superior de Hola de hello **zona DNS** hoja, seleccione **+ grabar conjunto** tooopen hello **Agregar conjunto de registros** hoja.

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. En hello **Agregar conjunto de registros** hoja. 
1. Seleccione **PTR** de registro de hello "**tipo**" menú.  
1. Hello nombre del conjunto de registros de Hola para un registro PTR debe rest de hello toobe de hello dirección IPv4 en orden inverso. En este ejemplo, hello tres primeros octetos ya se han rellenado como parte del nombre de la zona de hello (.2.0.192). Por lo tanto, solo Hola último octeto se proporciona en el campo de nombre de Hola. Por ejemplo, podría denominar el conjunto de registros "**15**" para un recurso cuya dirección IP es 192.0.2.15.  
1. Hola "**nombre de dominio**", escriba el nombre de dominio completo de hello (FQDN) del recurso de hello con IP Hola.
1. Seleccione **Aceptar** final Hola Hola hoja toocreate Hola de registro de DNS.

 ![Agregar conjunto de registros](./media/dns-reverse-dns-hosting/figure5.png)

Hello éstos son algunos ejemplos sobre cómo toocomplete esta tarea con hello AzureCLI y PowerShell:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a>CLI de Azure 1.0

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a>CLI de Azure 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a>IPv6

Hola siguiente ejemplo explica Hola proceso de creación de nuevo registro de 'PTR'. Para otros tipos de registro y toomodify los registros existentes, consulte [registros administrar DNS y los conjuntos de registros mediante el uso de Hola portal de Azure](dns-operations-recordsets-portal.md).

1. En parte superior de Hola de hello **hoja de zona DNS**, seleccione **+ grabar conjunto** tooopen Hola **Agregar conjunto de registros** hoja.

  ![Hoja de zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. En hello **Agregar conjunto de registros** hoja. 
3. Seleccione **PTR** de registro de hello "**tipo**" menú.  
4. Hello nombre del conjunto de registros de Hola para un registro PTR debe rest de hello toobe de hello dirección IPv6 en orden inverso. No puede contener ninguna compresión de ceros. En este ejemplo, Hola primeros 64 bits de hello IPv6 se rellenan como parte del nombre de la zona de hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa). Por lo tanto, se proporcionan solo Hola últimos 64 bits en el campo de nombre de Hola. Hola últimos 64 bits de la dirección IP de Hola se escriben en orden inverso, con un punto como delimitador de hello entre cada número hexadecimal. Por ejemplo, podría denominar el conjunto de registros "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" para un recurso cuya dirección IP es 2001:0db8:abdc:0000:f524:10bc:1af9:405e.  
5. Hola "**nombre de dominio**", escriba el nombre de dominio completo de hello (FQDN) del recurso de hello con IP Hola.
6. Seleccione **Aceptar** final Hola Hola hoja toocreate Hola de registro de DNS.

![Hoja Agregar conjunto de registros](./media/dns-reverse-dns-hosting/figure7.png)

Hello éstos son algunos ejemplos sobre cómo toocomplete esta tarea con hello AzureCLI y PowerShell:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a>CLI de Azure 1.0

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a>CLI de Azure 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a>Visualización de los registros

registros de hello tooview ha creado, navegue tooyour zona DNS en hello portal de Azure. Hola reducir parte de hello **zona DNS** hoja, puede ver registros de Hola para zona DNS de Hola. Debería ver Hola SOA y NS registros predeterminados, para que se crean en cada zona, además de todos los registros nuevos que haya creado.

### <a name="ipv4"></a>IPv4

Hoja de zona DNS, que muestra los registros PTR de IPv4:

![Hoja de zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

Hello en los ejemplos siguientes muestran cómo tooview Hola PTR registros mediante PowerShell u Hola CLI de Azure:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>CLI de Azure 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>CLI de Azure 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

Hoja de zona DNS, que muestra los registros PTR de IPv6:

![Hoja de zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

siguiente Hola es ejemplos de cómo tooview Hola registros con hello AzureCLI y PowerShell:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>CLI de Azure 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a>CLI de Azure 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a>P+F

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a>¿Puedo hospedar zonas de búsqueda inversa DNS para mis bloques IP asignados por el ISP en DNS de Azure?

Sí. Hospedan zonas de búsqueda inversa (ARPA) Hola para sus propios intervalos de IP en DNS de Azure es totalmente compatible.

Cree la zona de búsqueda inversa de hello en DNS de Azure como se explica en este artículo, a continuación, trabajar con su ISP demasiado[delegado Hola zona](dns-domain-delegation.md).  A continuación, puede administrar los registros PTR Hola para cada búsqueda inversa Hola mismo modo que otros tipos de registros.

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a>¿Cuánto cuesta el hospedaje de mi zona de búsqueda inversa DNS?

Hospedaje de zona de búsqueda DNS inversa hello para el bloque IP asignada por el ISP en DNS de Azure se aplican cargos en [tasas estándar de DNS de Azure](https://azure.microsoft.com/pricing/details/dns/).

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a>Puedo hospedar zonas de búsqueda inversa DNS para direcciones IPv4 e IPv6 en DNS de Azure?

Sí. Este artículo se explica cómo toocreate tanto IPv4 como IPv6 invertir zonas de búsqueda DNS en el DNS de Azure.

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a>¿Puedo importar una zona de búsqueda inversa DNS existente?

Sí. Puede usar zonas DNS existentes de hello Azure CLI tooimport en DNS de Azure. Esto funciona para las zonas de búsqueda directa y las zonas de búsqueda inversa.

Para obtener más información, consulte [importar y exportar un archivo de zona DNS mediante hello Azure CLI](dns-import-export.md).

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre los registros de DNS inverso, consulte información sobre la [búsqueda de DNS inverso en Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Obtenga información acerca de cómo demasiado[administrar registros de DNS inverso para los servicios de Azure](dns-reverse-dns-for-azure-services.md).
