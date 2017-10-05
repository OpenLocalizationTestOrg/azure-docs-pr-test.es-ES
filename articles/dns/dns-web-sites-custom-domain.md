---
title: "Creación de registros DNS personalizados para una aplicación web | Microsoft Docs"
description: "Creación de registros DNS de dominios personalizados para aplicaciones web mediante DNS de Azure."
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
ms.openlocfilehash: b054a41ecd69ee1c802d8403fe4b25128f016e3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="ba576-103">Creación de registros DNS para una aplicación web en un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="ba576-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="ba576-104">Puede utilizar DNS de Azure para hospedar un dominio personalizado para aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="ba576-104">You can use Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="ba576-105">Por ejemplo, va a crear una aplicación web de Azure y desea que los usuarios obtengan acceso a ella con la utilización de contoso.com o www.contoso.com como FQDN.</span><span class="sxs-lookup"><span data-stu-id="ba576-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="ba576-106">Para ello, deberá crear dos registros:</span><span class="sxs-lookup"><span data-stu-id="ba576-106">To do this, you have to create two records:</span></span>

* <span data-ttu-id="ba576-107">Un registro raíz "A" que apunta a contoso.com</span><span class="sxs-lookup"><span data-stu-id="ba576-107">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="ba576-108">Un registro "CNAME" para el nombre www que apunta al registro A</span><span class="sxs-lookup"><span data-stu-id="ba576-108">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="ba576-109">Tenga en cuenta que si crea un registro A para una aplicación web en Azure, este debe actualizarse manualmente si la dirección IP subyacente de la aplicación web cambia.</span><span class="sxs-lookup"><span data-stu-id="ba576-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ba576-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ba576-110">Before you begin</span></span>

<span data-ttu-id="ba576-111">Antes de comenzar, debe crear una zona DNS en DNS de Azure y delegar la zona del registrador a DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba576-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

1. <span data-ttu-id="ba576-112">Para crear una zona DNS, siga los pasos descritos en [Introducción a DNS de Azure](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="ba576-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="ba576-113">Para delegar su DNS a DNS de Azure, siga los pasos descritos en [Delegación de un dominio en DNS de Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="ba576-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="ba576-114">Después de crear una zona y delegarla a DNS de Azure, podrá crear registros para el dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ba576-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="ba576-115">1. Creación de un registro A para un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="ba576-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="ba576-116">Un registro A se usa para asignar un nombre a su dirección IP.</span><span class="sxs-lookup"><span data-stu-id="ba576-116">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="ba576-117">En el ejemplo siguiente, asignaremos @ como un registro A a una dirección IPv4:</span><span class="sxs-lookup"><span data-stu-id="ba576-117">In the following example we will assign @ as an A record to an IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="ba576-118">Paso 1</span><span class="sxs-lookup"><span data-stu-id="ba576-118">Step 1</span></span>

<span data-ttu-id="ba576-119">Cree un registro y asígnelo a una variable $rs</span><span class="sxs-lookup"><span data-stu-id="ba576-119">Create an A record and assign to a variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="ba576-120">Paso 2</span><span class="sxs-lookup"><span data-stu-id="ba576-120">Step 2</span></span>

<span data-ttu-id="ba576-121">Agregue el valor IPv4 al conjunto de registros creado previamente "@" mediante la variable $rs asignada.</span><span class="sxs-lookup"><span data-stu-id="ba576-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span></span> <span data-ttu-id="ba576-122">El valor de IPv4 asignado será la dirección IP de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ba576-122">The IPv4 value assigned will be the IP address for your web app.</span></span>

<span data-ttu-id="ba576-123">Para buscar la dirección IP para una aplicación web, siga los pasos descritos en [Configuración de un nombre de dominio personalizado en Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ba576-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="ba576-124">Paso 3</span><span class="sxs-lookup"><span data-stu-id="ba576-124">Step 3</span></span>

<span data-ttu-id="ba576-125">Confirme los cambios introducidos en el conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="ba576-125">Commit the changes to the record set.</span></span> <span data-ttu-id="ba576-126">Use `Set-AzureRMDnsRecordSet` para cargar los cambios del conjunto de registros en DNS de Azure:</span><span class="sxs-lookup"><span data-stu-id="ba576-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="ba576-127">2. Creación de un registro CNAME para el dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="ba576-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="ba576-128">Si el dominio ya está administrado por DNS de Azure (consulte [Delegación de dominios DNS](dns-domain-delegation.md)), puede utilizar el ejemplo siguiente para crear un registro CNAME para contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="ba576-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="ba576-129">Paso 1</span><span class="sxs-lookup"><span data-stu-id="ba576-129">Step 1</span></span>

<span data-ttu-id="ba576-130">Abra PowerShell y cree un nuevo conjunto de registros CNAME y asígnelo a una variable $rs.</span><span class="sxs-lookup"><span data-stu-id="ba576-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span></span> <span data-ttu-id="ba576-131">Este ejemplo creará un tipo de conjunto de registros CNAME con un "período de vida" de 600 segundos en la zona DNS denominada "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="ba576-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="ba576-132">El ejemplo siguiente es la respuesta.</span><span class="sxs-lookup"><span data-stu-id="ba576-132">The following example is the response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="ba576-133">Paso 2</span><span class="sxs-lookup"><span data-stu-id="ba576-133">Step 2</span></span>

<span data-ttu-id="ba576-134">Una vez creado el conjunto de registros CNAME, deberá crear un valor de alias que apuntará a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ba576-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span></span>

<span data-ttu-id="ba576-135">Mediante la variable asignada previamente "$rs", puede usar el comando de PowerShell siguiente para crear el alias para la aplicación web contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="ba576-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="ba576-136">El ejemplo siguiente es la respuesta.</span><span class="sxs-lookup"><span data-stu-id="ba576-136">The following example is the response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="ba576-137">Paso 3</span><span class="sxs-lookup"><span data-stu-id="ba576-137">Step 3</span></span>

<span data-ttu-id="ba576-138">Confirme los cambios mediante el cmdlet `Set-AzureRMDnsRecordSet` :</span><span class="sxs-lookup"><span data-stu-id="ba576-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="ba576-139">Puede validar que el registro se ha creado correctamente consultando “www.contoso.com” con nslookup, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="ba576-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="ba576-140">Creación de un registro "awverify" para aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="ba576-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="ba576-141">Si decide usar un registro A para la aplicación web, debe seguir un proceso de verificación para asegurarse de que es el titular del dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ba576-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span></span> <span data-ttu-id="ba576-142">Este paso de comprobación se realiza mediante la creación de un registro CNAME especial denominado "awverify".</span><span class="sxs-lookup"><span data-stu-id="ba576-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="ba576-143">Esta sección se aplica solo a los registros A.</span><span class="sxs-lookup"><span data-stu-id="ba576-143">This section applies to A records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="ba576-144">Paso 1</span><span class="sxs-lookup"><span data-stu-id="ba576-144">Step 1</span></span>

<span data-ttu-id="ba576-145">Cree el registro "awverify".</span><span class="sxs-lookup"><span data-stu-id="ba576-145">Create the "awverify" record.</span></span> <span data-ttu-id="ba576-146">En el ejemplo siguiente, el registro "awverify" se creará para contoso.com para verificar la titularidad del dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ba576-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="ba576-147">El ejemplo siguiente es la respuesta.</span><span class="sxs-lookup"><span data-stu-id="ba576-147">The following example is the response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="ba576-148">Paso 2</span><span class="sxs-lookup"><span data-stu-id="ba576-148">Step 2</span></span>

<span data-ttu-id="ba576-149">Una vez creado el conjunto de registros "awverify", asigne el alias del conjunto de registros CNAME.</span><span class="sxs-lookup"><span data-stu-id="ba576-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span></span> <span data-ttu-id="ba576-150">En el ejemplo siguiente, se asignará el alias del conjunto de registros CNAME a awverify.contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="ba576-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="ba576-151">El ejemplo siguiente es la respuesta.</span><span class="sxs-lookup"><span data-stu-id="ba576-151">The following example is the response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="ba576-152">Paso 3</span><span class="sxs-lookup"><span data-stu-id="ba576-152">Step 3</span></span>

<span data-ttu-id="ba576-153">Confirme los cambios mediante el cmdlet `Set-AzureRMDnsRecordSet cmdlet`, como se muestra en el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="ba576-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="ba576-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba576-154">Next steps</span></span>

<span data-ttu-id="ba576-155">Siga los pasos descritos en [Configurar un nombre de dominio personalizado en el Servicio de aplicaciones de Azure](../app-service-web/web-sites-custom-domain-name.md) para configurar la aplicación web para que use un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ba576-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span></span>
