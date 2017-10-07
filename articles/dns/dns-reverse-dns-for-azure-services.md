---
title: aaaReverse DNS para servicios de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure invertir las búsquedas DNS para los servicios hospedados en Azure"
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
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>Configuración de DNS inversos para servicios hospedados en Azure

Este artículo explica cómo tooconfigure invertir las búsquedas DNS para los servicios hospedados en Azure.

Los servicios de Azure utilizan direcciones IP asignadas por Azure y propiedad de Microsoft. Estos registros DNS inversos (registros PTR) deben crearse en hello correspondiente propiedad de Microsoft inversas zonas de búsqueda DNS. Este artículo se explica cómo toodo esto.

Este escenario no se debe confundir con capacidad de hello demasiado[hospedan zonas de búsqueda DNS inversas de Hola para los intervalos IP asignadas en DNS de Azure](dns-reverse-dns-hosting.md). En este caso, los intervalos de IP Hola representados por la zona de búsqueda inversa de hello deben asignarse tooyour organización, normalmente por su ISP.

Antes de leer este artículo, debe estar familiarizado con [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md).

Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).
* En el modelo de implementación del Administrador de recursos de hello, recursos de proceso (por ejemplo, las máquinas virtuales, conjuntos de escalas de máquina virtual o clústeres de Service Fabric) se exponen a través de un recurso de PublicIpAddress. Búsquedas inversas de DNS se configuran mediante la propiedad de 'ReverseFqdn' hello de hello PublicIpAddress.
* En el modelo de implementación de hello clásico, los recursos de proceso se exponen mediante servicios en la nube. Búsquedas inversas de DNS se configuran mediante la propiedad de 'ReverseDnsFqdn' hello de hello servicio en la nube.

DNS inversa no se admite actualmente para hello servicio de aplicaciones de Azure.

## <a name="validation-of-reverse-dns-records"></a>Validación de registros de DNS inversos

Otros fabricantes no debe ser capaz de toocreate registros de DNS inverso para sus dominios DNS de tooyour de asignación de servicio de Azure. tooprevent, Azure solo permite la creación de hello de un registro DNS inversa donde nombre de dominio especificado en el registro DNS inverso hello es Hola igual o se resuelve como Hola nombre DNS o dirección IP de un PublicIpAddress o una nube de servicio en hello mismo suscripción de Azure.

Solo se realiza la validación cuando el registro DNS inversa hello es establecer o modificar. No se llevan a cabo revalidaciones periódicas.

Por ejemplo: supongamos que hello PublicIpAddress recurso tiene contosoapp1.northus.cloudapp.azure.com de nombre DNS de hello y una dirección IP 23.96.52.53. Hola ReverseFqdn para hello que publicipaddress puede especificarse como:
* nombre DNS de Hola para hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com
* Hello de nombres DNS a una PublicIpAddress diferentes en hello misma suscripción, como contosoapp2.westus.cloudapp.azure.com
* Un personal de nombres DNS, como app1.contoso.com, siempre y cuando este nombre es *primer* configurado como un CNAME toocontosoapp1.northus.cloudapp.azure.com o tooa PublicIpAddress diferentes en hello misma suscripción.
* Un personal de nombres DNS, como app1.contoso.com, siempre y cuando este nombre es *primer* configurado como una dirección IP de un registro toohello 23.96.52.53 o dirección IP de toohello de una PublicIpAddress diferentes en hello misma suscripción.

Hello mismas restricciones aplican tooreverse DNS para servicios en la nube.


## <a name="reverse-dns-for-publicipaddress-resources"></a>DNS inverso para recursos de PublicIpAddress

Esta sección proporciona instrucciones detalladas sobre cómo tooconfigure inversa DNS para recursos de PublicIpAddress de modelo de implementación del Administrador de recursos de Hola, mediante PowerShell de Azure, Azure CLI 1.0 o 2.0 de CLI de Azure. Configuración de DNS inversa para recursos PublicIpAddress no se admite actualmente a través de hello portal de Azure.

Azure admite un DNS inverso en la actualidad solo para los recursos de PublicIpAddress de IPv4. No es compatible para IPv6.

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>Agregar tooan inversa de DNS existente las publicipaddresses a las

#### <a name="powershell"></a>PowerShell

tooadd inversa DNS tooan existente PublicIpAddress:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd invertir tooan DNS existente PublicIpAddress que aún no tenga un nombre DNS, también debe especificar un nombre DNS:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>CLI de Azure 1.0

tooadd inversa DNS tooan existente PublicIpAddress:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd invertir tooan DNS existente PublicIpAddress que aún no tenga un nombre DNS, también debe especificar un nombre DNS:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>CLI de Azure 2.0

tooadd inversa DNS tooan existente PublicIpAddress:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd invertir tooan DNS existente PublicIpAddress que aún no tenga un nombre DNS, también debe especificar un nombre DNS:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>Creación de una dirección IP pública con un DNS inverso

toocreate un nuevo PublicIpAddress con hello invertir ya ha especificado la propiedad DNS:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>CLI de Azure 1.0

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>CLI de Azure 2.0

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>Visualización de DNS inverso para una PublicIpAddress existente

Hola tooview el valor configurado para una PublicIpAddress existente:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>CLI de Azure 1.0

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>CLI de Azure 2.0

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>Eliminación de DNS inversos de direcciones IP públicas existentes

tooremove una propiedad DNS inversa de una PublicIpAddress existente:

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>CLI de Azure 1.0

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>CLI de Azure 2.0

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>Configuración de DNS inverso para Cloud Services

Esta sección proporciona instrucciones detalladas sobre cómo tooconfigure invertir DNS para servicios en la nube en el modelo de implementación clásico hello, uso de PowerShell de Azure. No se admite la configuración de DNS inverso para servicios en la nube a través de hello portal de Azure, Azure CLI 1.0 o 2.0 de CLI de Azure.

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>Agregar servicios de nube de tooexisting DNS inversa

tooadd un tooan de registro de DNS inversa existente de servicio en la nube:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>Creación de un servicio en la nube con un DNS inverso

toocreate un nuevo servicio de nube con la propiedad Hola DNS inversa ya especificada:

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>Visualización de DNS inverso para los servicios en la nube existentes

Hola tooview invertir la propiedad DNS para un servicio de nube existente:

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>Eliminación de DNS inverso de los servicios en la nube existentes

tooremove una propiedad DNS inversa de un servicio de nube existente:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>P+F

### <a name="how-much-do-reverse-dns-records-cost"></a>¿Cuánto cuestan los registros de DNS inversos?

Son gratuitos.  No existe ningún coste adicional para las consultas o los registros de DNS inversos.

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>¿Hola mi inversa resolver registros DNS de internet?

Sí. Una vez establecida la propiedad DNS inversa hello para el servicio de Azure, Azure administra todas las delegaciones DNS de Hola y zonas DNS necesario tooensure que invertir el registro DNS se resuelve para todos los usuarios de Internet.

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>¿Se crean registros de DNS inverso predeterminados para mis servicios de Azure?

No. El DNS inverso es una característica opcional. No tiene valor predeterminado se crean registros DNS inversos si elige no tooconfigure ellos.

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>¿Qué es el formato de hello para el nombre de dominio completo de hello (FQDN)?

Los FQDN se especifican en orden progresivo y deben terminar con un punto (por ejemplo, "app1.contoso.com.").

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>¿Qué ocurre si la comprobación de validación Hola Hola inversa DNS he especificado se produce un error?

Donde hello comprobación de validación de DNS inversa se produce un error, se produce un error de registro DNS inversa de hello operación tooconfigure Hola. Valor DNS inversa Hola correcto según sea necesario y vuelva a intentarlo.

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>¿Puedo configurar DNS inverso para Azure App Service?

No. DNS inversa no se admite para hello servicio de aplicaciones de Azure.

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>¿Puedo configurar varios registros de DNS inversos para mi servicio de Azure?

No. Azure admite un único registro de DNS inverso por cada servicio en la nube de Azure o PublicIpAddress.

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>¿Puedo configurar DNS inverso para los recursos de PublicIpAddress de IPv6?

No. Azure admite un DNS inverso en la actualidad solo para los recursos de PublicIpAddress de IPv4 y Cloud Services.

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>¿Se pueden enviar mensajes de correo electrónico tooexternal dominios desde Mis servicios de cálculo de Azure?

No. [Servicios de proceso de Azure no admite dominios que envían mensajes de correo electrónico tooexternal](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre los registros de DNS inverso, consulte información sobre la [búsqueda de DNS inverso en Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Obtenga información acerca de cómo demasiado[zona de búsqueda inversa de Hola de host para el intervalo IP asignada por el ISP en DNS de Azure](dns-reverse-dns-for-azure-services.md).

