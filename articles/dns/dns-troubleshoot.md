---
title: "Guía de solución de problemas de DNS aaaAzure | Documentos de Microsoft"
description: "¿Cómo se problemas comunes de tootroubleshoot con DNS de Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="6c048-103">Guía de solución de problemas de Azure DNS</span><span class="sxs-lookup"><span data-stu-id="6c048-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="6c048-104">Esta página proporciona información para solucionar problemas para preguntas que se plantean con frecuencia sobre Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6c048-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="6c048-105">Si estos pasos no resuelven el problema, también puede buscar o publicar su problema en nuestro [foro de soporte técnico de la comunidad en MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="6c048-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="6c048-106">Como alternativa, abra una solicitud de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c048-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="6c048-107">No puedo crear una zona DNS</span><span class="sxs-lookup"><span data-stu-id="6c048-107">I can't create a DNS zone</span></span>

<span data-ttu-id="6c048-108">tooresolve problemas comunes, pruebe uno o varios de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="6c048-108">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="6c048-109">Hola de revisión de auditoría DNS de Azure registra el motivo del error toodetermine Hola.</span><span class="sxs-lookup"><span data-stu-id="6c048-109">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="6c048-110">Cada nombre de zona DNS debe ser único dentro de su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6c048-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="6c048-111">Es decir, dos zonas DNS con hello igual nombre no puede compartir un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6c048-111">That is, two DNS zones with hello same name cannot share a resource group.</span></span> <span data-ttu-id="6c048-112">Intente usar otro nombre de zona u otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6c048-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="6c048-113">Puede ver un error "Se ha alcanzado o superado el número máximo de Hola de zonas en la suscripción {Id. de suscripción}."</span><span class="sxs-lookup"><span data-stu-id="6c048-113">You may see an error "You have reached or exceeded hello maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="6c048-114">Use una suscripción de Azure diferente, elimine algunas zonas o póngase en contacto con soporte técnico de Azure tooraise el límite de suscripción.</span><span class="sxs-lookup"><span data-stu-id="6c048-114">Either use a different Azure subscription, delete some zones, or contact Azure Support tooraise your subscription limit.</span></span>
4.  <span data-ttu-id="6c048-115">Puede ver un error "zona de hello '{nombre de zona}' no está disponible."</span><span class="sxs-lookup"><span data-stu-id="6c048-115">You may see an error "hello zone '{zone name}' is not available."</span></span> <span data-ttu-id="6c048-116">Este error significa que el DNS de Azure estaba servidores de nombres no se puede tooallocate para esta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="6c048-116">This error means that Azure DNS was unable tooallocate name servers for this DNS zone.</span></span> <span data-ttu-id="6c048-117">Pruebe a usar otro nombre de zona.</span><span class="sxs-lookup"><span data-stu-id="6c048-117">Try using a different zone name.</span></span> <span data-ttu-id="6c048-118">O bien, si es propietario de nombre de dominio de hello, póngase en contacto con soporte técnico de Azure, que puede asignar servidores de nombres para usted.</span><span class="sxs-lookup"><span data-stu-id="6c048-118">Alternatively, if you are hello domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="6c048-119">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="6c048-119">**Recommended documents**</span></span>

<span data-ttu-id="6c048-120">[DNS zones and records](dns-zones-records.md)
 (Registros y zonas DNS)</span><span class="sxs-lookup"><span data-stu-id="6c048-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="6c048-121">
[Creación de una zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6c048-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="6c048-122">No puedo crear un registro de DNS</span><span class="sxs-lookup"><span data-stu-id="6c048-122">I can't create a DNS record</span></span>

<span data-ttu-id="6c048-123">tooresolve problemas comunes, pruebe uno o varios de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="6c048-123">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="6c048-124">Hola de revisión de auditoría DNS de Azure registra el motivo del error toodetermine Hola.</span><span class="sxs-lookup"><span data-stu-id="6c048-124">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="6c048-125">¿Existe ya conjunto de registros de hello?</span><span class="sxs-lookup"><span data-stu-id="6c048-125">Does hello record set exist already?</span></span>  <span data-ttu-id="6c048-126">DNS de Azure administra los registros mediante el registro *establece*, que son colección de Hola de registros de hello mismo nombre y Hola mismo tipo.</span><span class="sxs-lookup"><span data-stu-id="6c048-126">Azure DNS manages records using record *sets*, which are hello collection of records of hello same name and hello same type.</span></span> <span data-ttu-id="6c048-127">Si un registro con hello mismo nombre y tipo ya existe, tooadd otro registro de dicho tipo debe modificar el registro existente de Hola establezca.</span><span class="sxs-lookup"><span data-stu-id="6c048-127">If a record with hello same name and type already exists, then tooadd another such record you should edit hello existing record set.</span></span>
3.  <span data-ttu-id="6c048-128">¿Estás tratando de toocreate un registro en el vértice (Hola 'raíz' de la zona de hello) de la zona DNS del Hola?</span><span class="sxs-lookup"><span data-stu-id="6c048-128">Are you trying toocreate a record at hello DNS zone apex (hello ‘root’ of hello zone)?</span></span> <span data-ttu-id="6c048-129">Si es así, Hola convención DNS es toouse Hola ' @' carácter como nombre de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="6c048-129">If so, hello DNS convention is toouse hello ‘@’ character as hello record name.</span></span> <span data-ttu-id="6c048-130">Tenga en cuenta también que los estándares de DNS hello no permiten registros CNAME en vértice de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c048-130">Also note that hello DNS standards do not permit CNAME records at hello zone apex.</span></span>
4.  <span data-ttu-id="6c048-131">¿Tiene un conflicto de CNAME?</span><span class="sxs-lookup"><span data-stu-id="6c048-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="6c048-132">los estándares de DNS Hello no permiten un registro CNAME con el mismo nombre como un registro de cualquier otro tipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c048-132">hello DNS standards do not allow a CNAME record with hello same name as a record of any other type.</span></span> <span data-ttu-id="6c048-133">Si tienes un CNAME existente, crear un registro con hello se produce un error en el mismo nombre de un tipo diferente.</span><span class="sxs-lookup"><span data-stu-id="6c048-133">If you have an existing CNAME, creating a record with hello same name of a different type fails.</span></span>  <span data-ttu-id="6c048-134">Del mismo modo, crear un CNAME se produce un error si el nombre de hello coincide con un registro existente de un tipo diferente.</span><span class="sxs-lookup"><span data-stu-id="6c048-134">Likewise, creating a CNAME fails if hello name matches an existing record of a different type.</span></span> <span data-ttu-id="6c048-135">Quitar conflicto Hola quitando Hola otro registro o elegir un nombre de registro diferente.</span><span class="sxs-lookup"><span data-stu-id="6c048-135">Remove hello conflict by removing hello other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="6c048-136">¿Ha alcanzado Hola Hola número límite de conjuntos de registros que se permiten en una zona DNS? establece el número actual de Hola de registro y hello número máximo de conjuntos de registros aparecen en el portal de Azure, en "Hello"propiedades"para zona de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="6c048-136">Have you reached hello limit on hello number of record sets permitted in a DNS zone? hello current number of record sets and hello maximum number of record sets are shown in hello Azure portal, under hello 'Properties' for hello zone.</span></span> <span data-ttu-id="6c048-137">Si se ha alcanzado este límite, a continuación, eliminar algunos conjuntos de registros o póngase en contacto con soporte técnico de Azure tooraise el límite de conjunto de registros para esta zona, vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="6c048-137">If you have reached this limit, then either delete some record sets or contact Azure Support tooraise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="6c048-138">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="6c048-138">**Recommended documents**</span></span>

<span data-ttu-id="6c048-139">[DNS zones and records](dns-zones-records.md)
 (Registros y zonas DNS)</span><span class="sxs-lookup"><span data-stu-id="6c048-139">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="6c048-140">
[Creación de una zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6c048-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="6c048-141">No puedo resolver mi registro de DNS</span><span class="sxs-lookup"><span data-stu-id="6c048-141">I can't resolve my DNS record</span></span>

<span data-ttu-id="6c048-142">La resolución de nombres de DNS es un proceso de varios pasos que puede generar un error por diversos motivos.</span><span class="sxs-lookup"><span data-stu-id="6c048-142">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="6c048-143">Hello pasos siguientes ayudarle a investigar por qué se producen errores en la resolución de DNS para un registro DNS en una zona alojada en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c048-143">hello following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="6c048-144">Confirme que se hayan configurado correctamente los registros DNS de hello en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c048-144">Confirm that hello DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="6c048-145">Revise los registros DNS de Hola Hola portal de Azure, la comprobación de que el nombre de la zona de Hola, nombre del registro y tipo de registro son correctos.</span><span class="sxs-lookup"><span data-stu-id="6c048-145">Review hello DNS records in hello Azure portal, checking that hello zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="6c048-146">Confirme que los registros DNS de hello resuelven correctamente en servidores de nombres DNS de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="6c048-146">Confirm that hello DNS records resolve correctly on hello Azure DNS name servers.</span></span>
    - <span data-ttu-id="6c048-147">Si realiza las consultas DNS del equipo local, puede ver los resultados almacenados en caché que no reflejan el estado actual de Hola Hola de servidores de nombres.</span><span class="sxs-lookup"><span data-stu-id="6c048-147">If you make DNS queries from your local PC, you may see cached results that don’t reflect hello current state of hello name servers.</span></span>  <span data-ttu-id="6c048-148">Además, las redes corporativas suelen utilizar servidores de proxy DNS, que impiden las consultas DNS dirige toospecific servidores de nombres.</span><span class="sxs-lookup"><span data-stu-id="6c048-148">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed toospecific name servers.</span></span>  <span data-ttu-id="6c048-149">tooavoid estos problemas, utilice un servicio de resolución de nombres basado en web como [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="6c048-149">tooavoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="6c048-150">Ser toospecify seguro de servidores de nombres correcta de hello para la zona DNS, como se muestra en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c048-150">Be sure toospecify hello correct name servers for your DNS zone, as shown in hello Azure portal.</span></span>
    - <span data-ttu-id="6c048-151">Compruebe que el nombre DNS de hello es correcto (tiene toospecify Hola completo nombre, incluido el nombre de la zona de hello) y tipo de registro de hello es correcta</span><span class="sxs-lookup"><span data-stu-id="6c048-151">Check that hello DNS name is correct (you have toospecify hello fully qualified name, including hello zone name) and hello record type is correct</span></span>
3.  <span data-ttu-id="6c048-152">Confirmar ese nombre de dominio DNS de hello ha sido correctamente [delegado servidores de nombres DNS de Azure toohello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="6c048-152">Confirm that hello DNS domain name has been correctly [delegated toohello Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="6c048-153">Hay un [muchos sitios web de terceros que ofrecen la validación de la delegación de DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="6c048-153">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="6c048-154">Esta prueba es un *zona* prueba de delegación, por lo que sólo se deben escribir el nombre de zona del DNS de hello y no Hola registro nombre completo.</span><span class="sxs-lookup"><span data-stu-id="6c048-154">This test is a *zone* delegation test, so you should only enter hello DNS zone name and not hello fully qualified record name.</span></span>
4.  <span data-ttu-id="6c048-155">Completada Hola anterior, el registro DNS debe resolver correctamente.</span><span class="sxs-lookup"><span data-stu-id="6c048-155">Having completed hello above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="6c048-156">tooverify, puede volver a usar [digwebinterface](http://digwebinterface.com), pero esta vez con la configuración de servidor de nombre de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6c048-156">tooverify, you can again use [digwebinterface](http://digwebinterface.com), this time using hello default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="6c048-157">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="6c048-157">**Recommended documents**</span></span>

[<span data-ttu-id="6c048-158">Delegar un tooAzure de dominio DNS</span><span class="sxs-lookup"><span data-stu-id="6c048-158">Delegate a domain tooAzure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="6c048-159">¿Cómo puedo especificar Hola "service" y "protocol" para un registro SRV?</span><span class="sxs-lookup"><span data-stu-id="6c048-159">How do I specify hello ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="6c048-160">DNS de Azure administra los registros DNS como conjuntos de registros: Hola colección de registros con hello mismo nombre y Hola mismo tipo.</span><span class="sxs-lookup"><span data-stu-id="6c048-160">Azure DNS manages DNS records as record sets—hello collection of records with hello same name and hello same type.</span></span> <span data-ttu-id="6c048-161">Para un conjunto de registros de SRV, Hola "service" y "protocol" necesitan toobe especificado como parte del nombre de conjunto de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c048-161">For an SRV record set, hello 'service' and 'protocol' need toobe specified as part of hello record set name.</span></span> <span data-ttu-id="6c048-162">Hello otros parámetros SRV ('priority', 'weight', 'puerto' y 'target') se especifican por separado para cada registro de conjunto de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c048-162">hello other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in hello record set.</span></span>

<span data-ttu-id="6c048-163">Ejemplo de nombres de registros SRV (nombre de servicio "sip", protocolo "tcp"):</span><span class="sxs-lookup"><span data-stu-id="6c048-163">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="6c048-164">\_SIP. \_tcp (crea un conjunto en vértice de la zona de Hola de registros)</span><span class="sxs-lookup"><span data-stu-id="6c048-164">\_sip.\_tcp (creates a record set at hello zone apex)</span></span>
- <span data-ttu-id="6c048-165">\_sip.\_tcp.sipservice (crea un conjunto de registros con el nombre "sipservice")</span><span class="sxs-lookup"><span data-stu-id="6c048-165">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="6c048-166">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="6c048-166">**Recommended documents**</span></span>

<span data-ttu-id="6c048-167">[DNS zones and records](dns-zones-records.md)
 (Registros y zonas DNS)</span><span class="sxs-lookup"><span data-stu-id="6c048-167">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="6c048-168">
[Crear conjuntos de registros de DNS y los registros mediante Hola portal de Azure](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="6c048-168">
[Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="6c048-169">
[Tipo de registro SRV (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="6c048-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="6c048-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c048-170">Next steps</span></span>

* <span data-ttu-id="6c048-171">Más información sobre [Registros y zonas DNS](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="6c048-171">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="6c048-172">toostart mediante DNS de Azure, obtenga información acerca de cómo demasiado[crear una zona DNS](dns-getstarted-create-dnszone-portal.md) y [crear registros DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6c048-172">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="6c048-173">toomigrate una zona DNS existente, obtenga información acerca de cómo demasiado[importar y exportar un archivo de zona DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="6c048-173">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>

