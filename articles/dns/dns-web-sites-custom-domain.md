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
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="9f6fb-103">Creación de registros DNS para una aplicación web en un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="9f6fb-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="9f6fb-104">Puede utilizar DNS de Azure toohost un dominio personalizado para las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="9f6fb-105">Por ejemplo, va a crear una aplicación web de Azure y desea que su tooaccess a los usuarios que, ya sea mediante contoso.com o www.contoso.com como un FQDN.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="9f6fb-106">toodo, tiene dos registros de toocreate:</span><span class="sxs-lookup"><span data-stu-id="9f6fb-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="9f6fb-107">Un toocontoso.com señalador registro raíz "A"</span><span class="sxs-lookup"><span data-stu-id="9f6fb-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="9f6fb-108">Un "" registro CNAME para el nombre hello World Wide Web que señale toohello un registro</span><span class="sxs-lookup"><span data-stu-id="9f6fb-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="9f6fb-109">Tenga en cuenta que si crea un registro para una aplicación web en Azure, Hola que un registro debe actualizarse manualmente si Hola subyacente dirección IP para el cambio en la aplicación web Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9f6fb-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="9f6fb-110">Before you begin</span></span>

<span data-ttu-id="9f6fb-111">Antes de empezar, primero debe crear una zona DNS de DNS de Azure y delegar la zona de hello en el DNS de registrador tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="9f6fb-112">toocreate una zona DNS, siga los pasos de hello en [crear una zona DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="9f6fb-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="9f6fb-113">toodelegate su tooAzure DNS DNS, siga pasos hello [delegación de dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="9f6fb-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="9f6fb-114">Después de crear una zona y delegar tooAzure DNS, a continuación, puede crear registros para el dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="9f6fb-115">1. Creación de un registro A para un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="9f6fb-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="9f6fb-116">Un registro es toomap usa una dirección IP de tooits de nombre.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="9f6fb-117">En el siguiente ejemplo de Hola asignaremos como un tooan de registro de una dirección IPv4:</span><span class="sxs-lookup"><span data-stu-id="9f6fb-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="9f6fb-118">Paso 1</span><span class="sxs-lookup"><span data-stu-id="9f6fb-118">Step 1</span></span>

<span data-ttu-id="9f6fb-119">Crear un registro y asignar tooa variable $rs</span><span class="sxs-lookup"><span data-stu-id="9f6fb-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="9f6fb-120">Paso 2</span><span class="sxs-lookup"><span data-stu-id="9f6fb-120">Step 2</span></span>

<span data-ttu-id="9f6fb-121">Agregar conjunto de registros de hello IPv4 valor toohello creado anteriormente "@" mediante la variable $rs Hola asignado.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="9f6fb-122">Hola valor IPv4 asignado será la dirección IP de hello para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="9f6fb-123">dirección IP de hello toofind para una aplicación web, siga los pasos de hello en [configurar un nombre de dominio personalizado en el servicio de aplicación de Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="9f6fb-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="9f6fb-124">Paso 3</span><span class="sxs-lookup"><span data-stu-id="9f6fb-124">Step 3</span></span>

<span data-ttu-id="9f6fb-125">Confirmar el conjunto de registros toohello Hola cambios.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="9f6fb-126">Use `Set-AzureRMDnsRecordSet` hello tooupload cambia toohello tooAzure de conjunto de registros DNS:</span><span class="sxs-lookup"><span data-stu-id="9f6fb-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="9f6fb-127">2. Creación de un registro CNAME para el dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="9f6fb-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="9f6fb-128">Si el dominio ya está administrado por DNS de Azure (consulte [delegación de dominio DNS](dns-domain-delegation.md), puede usar Hola después toocreate de ejemplo de Hola un registro CNAME para contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="9f6fb-129">Paso 1</span><span class="sxs-lookup"><span data-stu-id="9f6fb-129">Step 1</span></span>

<span data-ttu-id="9f6fb-130">Abra PowerShell y cree un nuevo conjunto de registros CNAME y asignar tooa variable $rs.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="9f6fb-131">En este ejemplo creará un tipo de conjunto de registros CNAME con un "tiempo toolive" de 600 segundos en la zona DNS denominado "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="9f6fb-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="9f6fb-132">Hola siguiente ejemplo es la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-132">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="9f6fb-133">Paso 2</span><span class="sxs-lookup"><span data-stu-id="9f6fb-133">Step 2</span></span>

<span data-ttu-id="9f6fb-134">Una vez creado el conjunto de registros CNAME de hello, debe toocreate un valor de alias que señalará toohello web app.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="9f6fb-135">En hello previamente asignados variable "$rs" puede utilizar comandos de PowerShell hello debajo de alias de hello toocreate de hello web app contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="9f6fb-136">Hola siguiente ejemplo es la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-136">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="9f6fb-137">Paso 3</span><span class="sxs-lookup"><span data-stu-id="9f6fb-137">Step 3</span></span>

<span data-ttu-id="9f6fb-138">Confirmar cambios de hello mediante hello `Set-AzureRMDnsRecordSet` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9f6fb-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="9f6fb-139">Puede validar el registro de hello se creó correctamente consultando Hola "www.contoso.com" mediante nslookup, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="9f6fb-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="9f6fb-140">Creación de un registro "awverify" para aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="9f6fb-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="9f6fb-141">Si decide toouse un registro de la aplicación web, debe pasar por un tooensure del proceso de comprobación se dominio personalizado propio Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="9f6fb-142">Este paso de comprobación se realiza mediante la creación de un registro CNAME especial denominado "awverify".</span><span class="sxs-lookup"><span data-stu-id="9f6fb-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="9f6fb-143">En esta sección se aplica sólo los registros tooA.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="9f6fb-144">Paso 1</span><span class="sxs-lookup"><span data-stu-id="9f6fb-144">Step 1</span></span>

<span data-ttu-id="9f6fb-145">Crear registro de hello "awverify".</span><span class="sxs-lookup"><span data-stu-id="9f6fb-145">Create hello "awverify" record.</span></span> <span data-ttu-id="9f6fb-146">En el ejemplo de Hola siguiente, crearemos registro de "aweverify" hello para la propiedad del tooverify contoso.com para el dominio personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="9f6fb-147">Hola siguiente ejemplo es la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-147">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="9f6fb-148">Paso 2</span><span class="sxs-lookup"><span data-stu-id="9f6fb-148">Step 2</span></span>

<span data-ttu-id="9f6fb-149">Una vez creado el conjunto de registros "awverify" Hola, asignar registro CNAME Hola establecer el alias.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="9f6fb-150">En el ejemplo de Hola a continuación, asignaremos tooawverify.contoso.azurewebsites.net de alias de conjunto de registros de CNAMe de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="9f6fb-151">Hola siguiente ejemplo es la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-151">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="9f6fb-152">Paso 3</span><span class="sxs-lookup"><span data-stu-id="9f6fb-152">Step 3</span></span>

<span data-ttu-id="9f6fb-153">Confirmar cambios de hello mediante hello `Set-AzureRMDnsRecordSet cmdlet`, tal y como se muestra en el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="9f6fb-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f6fb-154">Next steps</span></span>

<span data-ttu-id="9f6fb-155">Siga los pasos de hello en [configurar un nombre de dominio personalizado para el servicio de aplicaciones](../app-service-web/web-sites-custom-domain-name.md) tooconfigure su toouse de aplicación web un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="9f6fb-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
