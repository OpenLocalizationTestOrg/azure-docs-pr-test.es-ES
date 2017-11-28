---
title: "Guía de solución de problemas de Azure DNS | Microsoft Docs"
description: "Cómo solucionar problemas comunes con DNS de Azure"
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
ms.openlocfilehash: 1d9bb681a864bdc3e5a2f9c9a531d9566b16ada4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="ff281-103">Guía de solución de problemas de Azure DNS</span><span class="sxs-lookup"><span data-stu-id="ff281-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="ff281-104">Esta página proporciona información para solucionar problemas para preguntas que se plantean con frecuencia sobre Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ff281-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="ff281-105">Si estos pasos no resuelven el problema, también puede buscar o publicar su problema en nuestro [foro de soporte técnico de la comunidad en MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="ff281-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="ff281-106">Como alternativa, abra una solicitud de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff281-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="ff281-107">No puedo crear una zona DNS</span><span class="sxs-lookup"><span data-stu-id="ff281-107">I can't create a DNS zone</span></span>

<span data-ttu-id="ff281-108">Para resolver problemas habituales, pruebe uno o varios de los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ff281-108">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="ff281-109">Revise los registros de auditoría de Azure DNS para determinar el motivo del error.</span><span class="sxs-lookup"><span data-stu-id="ff281-109">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="ff281-110">Cada nombre de zona DNS debe ser único dentro de su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ff281-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="ff281-111">Es decir, dos zonas DNS con el mismo nombre no pueden compartir un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ff281-111">That is, two DNS zones with the same name cannot share a resource group.</span></span> <span data-ttu-id="ff281-112">Intente usar otro nombre de zona u otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ff281-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="ff281-113">Es posible que vea el mensaje "Se alcanzó o superó el número máximo de zonas en la suscripción {ID de la suscripción}".</span><span class="sxs-lookup"><span data-stu-id="ff281-113">You may see an error "You have reached or exceeded the maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="ff281-114">Use otra suscripción de Azure, elimine algunas zonas o póngase en contacto con el soporte técnico de Azure para aumentar el límite de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="ff281-114">Either use a different Azure subscription, delete some zones, or contact Azure Support to raise your subscription limit.</span></span>
4.  <span data-ttu-id="ff281-115">Es posible que vea el mensaje "La zona '{nombre de la zona}' no está disponible".</span><span class="sxs-lookup"><span data-stu-id="ff281-115">You may see an error "The zone '{zone name}' is not available."</span></span> <span data-ttu-id="ff281-116">Este error significa que Azure DNS no pudo asignar servidores de nombres para esta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="ff281-116">This error means that Azure DNS was unable to allocate name servers for this DNS zone.</span></span> <span data-ttu-id="ff281-117">Pruebe a usar otro nombre de zona.</span><span class="sxs-lookup"><span data-stu-id="ff281-117">Try using a different zone name.</span></span> <span data-ttu-id="ff281-118">O bien, si es el propietario del nombre de dominio, póngase en contacto con el soporte técnico de Azure, que puede asignarle servidores de nombres.</span><span class="sxs-lookup"><span data-stu-id="ff281-118">Alternatively, if you are the domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="ff281-119">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="ff281-119">**Recommended documents**</span></span>

<span data-ttu-id="ff281-120">[DNS zones and records](dns-zones-records.md)
 (Registros y zonas DNS)</span><span class="sxs-lookup"><span data-stu-id="ff281-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="ff281-121">
[Creación de una zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ff281-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="ff281-122">No puedo crear un registro de DNS</span><span class="sxs-lookup"><span data-stu-id="ff281-122">I can't create a DNS record</span></span>

<span data-ttu-id="ff281-123">Para resolver problemas habituales, pruebe uno o varios de los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ff281-123">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="ff281-124">Revise los registros de auditoría de Azure DNS para determinar el motivo del error.</span><span class="sxs-lookup"><span data-stu-id="ff281-124">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="ff281-125">¿El conjunto de registros ya existe?</span><span class="sxs-lookup"><span data-stu-id="ff281-125">Does the record set exist already?</span></span>  <span data-ttu-id="ff281-126">El DNS de Azure administra los registros mediante los *conjuntos* de registros, que son una colección de registros con el mismo nombre y el mismo tipo.</span><span class="sxs-lookup"><span data-stu-id="ff281-126">Azure DNS manages records using record *sets*, which are the collection of records of the same name and the same type.</span></span> <span data-ttu-id="ff281-127">Si ya existe un registro con el mismo nombre y tipo, para agregar otro registro de dicho tipo debe editar el conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="ff281-127">If a record with the same name and type already exists, then to add another such record you should edit the existing record set.</span></span>
3.  <span data-ttu-id="ff281-128">¿Está intentando crear un registro en el vértice de la zona DNS (la "raíz" de la zona)?</span><span class="sxs-lookup"><span data-stu-id="ff281-128">Are you trying to create a record at the DNS zone apex (the ‘root’ of the zone)?</span></span> <span data-ttu-id="ff281-129">Si es así, la convención de DNS es usar el carácter ‘@’ como nombre del registro.</span><span class="sxs-lookup"><span data-stu-id="ff281-129">If so, the DNS convention is to use the ‘@’ character as the record name.</span></span> <span data-ttu-id="ff281-130">Tenga en cuenta también que los estándares de DNS no permiten registros CNAME en el vértice de la zona.</span><span class="sxs-lookup"><span data-stu-id="ff281-130">Also note that the DNS standards do not permit CNAME records at the zone apex.</span></span>
4.  <span data-ttu-id="ff281-131">¿Tiene un conflicto de CNAME?</span><span class="sxs-lookup"><span data-stu-id="ff281-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="ff281-132">Los estándares de DNS no permiten un registro CNAME con el mismo nombre que un registro de cualquier otro tipo.</span><span class="sxs-lookup"><span data-stu-id="ff281-132">The DNS standards do not allow a CNAME record with the same name as a record of any other type.</span></span> <span data-ttu-id="ff281-133">Si tiene un CNAME existente, la creación de un registro con el mismo nombre, pero de un tipo diferente genera un error.</span><span class="sxs-lookup"><span data-stu-id="ff281-133">If you have an existing CNAME, creating a record with the same name of a different type fails.</span></span>  <span data-ttu-id="ff281-134">Del mismo modo, la creación de un CNAME genera un error si el nombre coincide con un registro existente de otro tipo.</span><span class="sxs-lookup"><span data-stu-id="ff281-134">Likewise, creating a CNAME fails if the name matches an existing record of a different type.</span></span> <span data-ttu-id="ff281-135">Elimine el conflicto quitando el otro registro o eligiendo otro nombre de registro.</span><span class="sxs-lookup"><span data-stu-id="ff281-135">Remove the conflict by removing the other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="ff281-136">¿Ha alcanzado el límite en el número de conjuntos de registros permitido en una zona DNS?</span><span class="sxs-lookup"><span data-stu-id="ff281-136">Have you reached the limit on the number of record sets permitted in a DNS zone?</span></span> <span data-ttu-id="ff281-137">En Azure Portal se muestra el número actual y el número máximo de conjuntos de registros, en las propiedades de la zona.</span><span class="sxs-lookup"><span data-stu-id="ff281-137">The current number of record sets and the maximum number of record sets are shown in the Azure portal, under the 'Properties' for the zone.</span></span> <span data-ttu-id="ff281-138">Si ha alcanzado este límite, elimine algunos conjuntos de registros o póngase en contacto con el soporte técnico de Azure para aumentar el límite de conjuntos de registros para esta zona y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="ff281-138">If you have reached this limit, then either delete some record sets or contact Azure Support to raise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="ff281-139">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="ff281-139">**Recommended documents**</span></span>

<span data-ttu-id="ff281-140">[DNS zones and records](dns-zones-records.md)
 (Registros y zonas DNS)</span><span class="sxs-lookup"><span data-stu-id="ff281-140">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="ff281-141">
[Creación de una zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ff281-141">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="ff281-142">No puedo resolver mi registro de DNS</span><span class="sxs-lookup"><span data-stu-id="ff281-142">I can't resolve my DNS record</span></span>

<span data-ttu-id="ff281-143">La resolución de nombres de DNS es un proceso de varios pasos que puede generar un error por diversos motivos.</span><span class="sxs-lookup"><span data-stu-id="ff281-143">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="ff281-144">Los pasos siguientes ayudan a investigar por qué se producen errores en la resolución de DNS para un registro de DNS en una zona hospedada en Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ff281-144">The following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="ff281-145">Confirme que los registros de DNS se hayan configurado correctamente en el DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff281-145">Confirm that the DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="ff281-146">Revise los registros de DNS en Azure Portal y compruebe que el nombre de la zona, el nombre del registro y el tipo de registro son correctos.</span><span class="sxs-lookup"><span data-stu-id="ff281-146">Review the DNS records in the Azure portal, checking that the zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="ff281-147">Confirme que los registros de DNS se resuelven correctamente en los servidores de nombres de DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff281-147">Confirm that the DNS records resolve correctly on the Azure DNS name servers.</span></span>
    - <span data-ttu-id="ff281-148">Si realiza consultas de DNS del equipo local, puede ver los resultados almacenados en caché que no reflejen el estado actual de los servidores de nombres.</span><span class="sxs-lookup"><span data-stu-id="ff281-148">If you make DNS queries from your local PC, you may see cached results that don’t reflect the current state of the name servers.</span></span>  <span data-ttu-id="ff281-149">Además, las redes corporativas suelen usan servidores proxy de DNS que impiden que las consultas de DNS se dirijan a servidores de nombres específicos.</span><span class="sxs-lookup"><span data-stu-id="ff281-149">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed to specific name servers.</span></span>  <span data-ttu-id="ff281-150">Para evitar estos problemas, utilice un servicio de resolución de nombres basado en web, como [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="ff281-150">To avoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="ff281-151">Asegúrese de especificar los servidores de nombres correctos para la zona DNS, que se muestran en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ff281-151">Be sure to specify the correct name servers for your DNS zone, as shown in the Azure portal.</span></span>
    - <span data-ttu-id="ff281-152">Compruebe que el nombre de DNS (tiene que especificar el nombre completo, incluido el nombre de zona) y el tipo de registro son correctos</span><span class="sxs-lookup"><span data-stu-id="ff281-152">Check that the DNS name is correct (you have to specify the fully qualified name, including the zone name) and the record type is correct</span></span>
3.  <span data-ttu-id="ff281-153">Confirme que el nombre de dominio del DNS se ha [delegado correctamente a los servidores de nombres de DNS de Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="ff281-153">Confirm that the DNS domain name has been correctly [delegated to the Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="ff281-154">Hay un [muchos sitios web de terceros que ofrecen la validación de la delegación de DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="ff281-154">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="ff281-155">Se trata de una prueba de delegación de *zona*, por lo que solo se debe escribir el nombre de la zona DNS, no el nombre de registro completo.</span><span class="sxs-lookup"><span data-stu-id="ff281-155">This test is a *zone* delegation test, so you should only enter the DNS zone name and not the fully qualified record name.</span></span>
4.  <span data-ttu-id="ff281-156">Una vez completado lo anterior, el registro de DNS ahora debe resolverse correctamente.</span><span class="sxs-lookup"><span data-stu-id="ff281-156">Having completed the above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="ff281-157">Para comprobarlo, puede volver a usar [digwebinterface](http://digwebinterface.com), pero esta vez con la configuración predeterminada del servidor de nombres.</span><span class="sxs-lookup"><span data-stu-id="ff281-157">To verify, you can again use [digwebinterface](http://digwebinterface.com), this time using the default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="ff281-158">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="ff281-158">**Recommended documents**</span></span>

[<span data-ttu-id="ff281-159">Delegación de un dominio en DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="ff281-159">Delegate a domain to Azure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-the-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="ff281-160">¿Cómo puedo especificar el "servicio" y el "protocolo" para un registro SRV?</span><span class="sxs-lookup"><span data-stu-id="ff281-160">How do I specify the ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="ff281-161">El DNS de Azure administra los registros de DNS como conjuntos de registros: la colección de registros con el mismo nombre y el mismo tipo.</span><span class="sxs-lookup"><span data-stu-id="ff281-161">Azure DNS manages DNS records as record sets—the collection of records with the same name and the same type.</span></span> <span data-ttu-id="ff281-162">Para un conjunto de registros SRV, el "servicio" y el "protocolo" deben especificarse como parte del nombre del conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="ff281-162">For an SRV record set, the 'service' and 'protocol' need to be specified as part of the record set name.</span></span> <span data-ttu-id="ff281-163">Los otros parámetros SRV (la "prioridad", el "peso", el "puerto" y el "destino") se especifican por separado para cada registro del conjunto.</span><span class="sxs-lookup"><span data-stu-id="ff281-163">The other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in the record set.</span></span>

<span data-ttu-id="ff281-164">Ejemplo de nombres de registros SRV (nombre de servicio "sip", protocolo "tcp"):</span><span class="sxs-lookup"><span data-stu-id="ff281-164">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="ff281-165">\_sip.\_tcp (crea un conjunto de registros en el vértice de la zona)</span><span class="sxs-lookup"><span data-stu-id="ff281-165">\_sip.\_tcp (creates a record set at the zone apex)</span></span>
- <span data-ttu-id="ff281-166">\_sip.\_tcp.sipservice (crea un conjunto de registros con el nombre "sipservice")</span><span class="sxs-lookup"><span data-stu-id="ff281-166">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="ff281-167">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="ff281-167">**Recommended documents**</span></span>

<span data-ttu-id="ff281-168">[DNS zones and records](dns-zones-records.md)
 (Registros y zonas DNS)</span><span class="sxs-lookup"><span data-stu-id="ff281-168">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="ff281-169">
[Creación de registros y conjuntos de registros de DNS mediante Azure Portal](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="ff281-169">
[Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="ff281-170">
[Tipo de registro SRV (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="ff281-170">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="ff281-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ff281-171">Next steps</span></span>

* <span data-ttu-id="ff281-172">Más información sobre [Registros y zonas DNS](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="ff281-172">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="ff281-173">Para empezar a usar DNS de Azure, vea cómo [crear una zona DNS](dns-getstarted-create-dnszone-portal.md) y [crear registros DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ff281-173">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="ff281-174">Para migrar una zona DNS existente, vea cómo [importar y exportar un archivo de zona DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="ff281-174">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>

