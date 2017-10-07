---
title: aaaGuide toocreating un servicio de datos para hello Marketplace | Documentos de Microsoft
description: "Instrucciones detalladas de cómo toocreate, certificar e implementar un servicio de datos para la venta en hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 148f8638-ee80-4100-8d63-5afa4167ca1b
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 8917a43959834d15f70866297f98d24bb83e217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-mapping-an-existing-web-service-tooodata-through-csdls"></a><span data-ttu-id="9bdef-103">Ejemplos de la asignación existente de web tooOData de servicio a través de CSDLs</span><span class="sxs-lookup"><span data-stu-id="9bdef-103">Examples of mapping an existing web service tooOData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9bdef-104">**En este momento, ya no se pueden incorporar nuevos editores del Servicio de datos. No se aprobarán nuevos servicios de datos para mostrarse en lista.**</span><span class="sxs-lookup"><span data-stu-id="9bdef-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="9bdef-105">Si tiene una aplicación de negocio de SaaS desea toopublish en AppSource encontrará información más [aquí](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="9bdef-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="9bdef-106">Si tiene aplicaciones IaaS o desarrollador del servicio quiere como toopublish en Azure Marketplace también puede encontrar más información [aquí](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="9bdef-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="9bdef-107">Ejemplo: FunctionImport para los datos de "Raw" devueltos mediante "POST"</span><span class="sxs-lookup"><span data-stu-id="9bdef-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="9bdef-108">Utilice toocreate de datos de entrada sin formato nuevo subordinado y devolver su servidor había definido por la URL(location) o tooupdate parte de hello subordinado en el servidor de hello dirección URL.</span><span class="sxs-lookup"><span data-stu-id="9bdef-108">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="9bdef-109">Donde hello subordinado es una secuencia, es decir, datos no estructurada, p. ej.</span><span class="sxs-lookup"><span data-stu-id="9bdef-109">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="9bdef-110">un archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="9bdef-110">a text file.</span></span>  <span data-ttu-id="9bdef-111">Tenga en cuenta que POST no es idempotentes sin una ubicación.</span><span class="sxs-lookup"><span data-stu-id="9bdef-111">Beware POST in not idempotent without a location.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="AddUsageEvent" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Add usage event (data acquisition)</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="9bdef-112">Ejemplo: FunctionImport mediante "DELETE"</span><span class="sxs-lookup"><span data-stu-id="9bdef-112">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="9bdef-113">Usar DELETE tooremove un URI especificado.</span><span class="sxs-lookup"><span data-stu-id="9bdef-113">Use DELETE tooremove a specified URI.</span></span>

        <EntitySet Name="DeleteUsageFileEntitySet" EntityType="MyOffer.DeleteUsageFileEntity" />
        <FunctionImport Name="DeleteUsageFile" EntitySet="DeleteUsageFileEntitySet" ReturnType="Collection(MyOffer.DeleteUsageFileEntity)"  d:AllowedHttpMethods="DELETE" d:EncodeParameterValues="true” d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643" >
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Delete usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="DeleteUsageFileEntity" d:Map="//boolean">
        <Property Name="boolean" Type="String" Nullable="true" d:Map="./boolean" />
        </EntityType>

## <a name="example-functionimport-using-post"></a><span data-ttu-id="9bdef-114">Ejemplo: FunctionImport mediante "POST"</span><span class="sxs-lookup"><span data-stu-id="9bdef-114">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="9bdef-115">Utilice toocreate de datos de entrada sin formato nuevo subordinado y devolver su servidor había definido por la URL(location) o tooupdate parte de hello subordinado en el servidor de hello dirección URL.</span><span class="sxs-lookup"><span data-stu-id="9bdef-115">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="9bdef-116">Donde hello subordinado es una estructura.</span><span class="sxs-lookup"><span data-stu-id="9bdef-116">Where hello subordinate is a structure.</span></span> <span data-ttu-id="9bdef-117">Tenga en cuenta que POST no es idempotentes sin una ubicación.</span><span class="sxs-lookup"><span data-stu-id="9bdef-117">Beware POST is not idempotent without a location.</span></span>

        <EntitySet Name="CreateANewModelEntitySet2" EntityType=" MyOffer.CreateANewModelEntity2" />
        <FunctionImport Name="CreateModel" EntitySet="CreateANewModelEntitySet2" ReturnType="Collection(MyOffer.CreateANewModelEntity2)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Create A New Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-put"></a><span data-ttu-id="9bdef-118">Ejemplo: FunctionImport mediante "PUT"</span><span class="sxs-lookup"><span data-stu-id="9bdef-118">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="9bdef-119">Usar PUT toocreate subordinado nueva o subordinado completo de hello tooupdate en un servidor definido dirección URL.</span><span class="sxs-lookup"><span data-stu-id="9bdef-119">Use PUT toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="9bdef-120">Donde hello subordinado es una estructura, PUT es idempotente para varias repeticiones dará como resultado Hola mismo estado, es decir</span><span class="sxs-lookup"><span data-stu-id="9bdef-120">Where hello subordinate is a structure, PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="9bdef-121">x = 5.</span><span class="sxs-lookup"><span data-stu-id="9bdef-121">x=5.</span></span>  <span data-ttu-id="9bdef-122">Put debe usarse con hello completas de contenidos de hello especificada recursos.</span><span class="sxs-lookup"><span data-stu-id="9bdef-122">Put should be used with hello full content of hello specified resource.</span></span>

        <EntitySet Name="UpdateAnExistingModelEntitySet" EntityType="MyOffer.UpdateAnExistingModelEntity" />
        <FunctionImport Name="UpdateModel" EntitySet="UpdateAnExistingModelEntitySet" ReturnType="Collection(MyOffer.UpdateAnExistingModelEntity)" d:EncodeParameterValues="true" d:AllowedHttpMethods="PUT" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Update an Existing Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="UpdateAnExistingModelEntity" d:Map="//string">
        <Property Name="string"     Type="String" Nullable="true" d:Map="./string" />
        </EntityType>


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="9bdef-123">Ejemplo: FunctionImport para los datos de "Raw" devueltos mediante "PUT"</span><span class="sxs-lookup"><span data-stu-id="9bdef-123">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="9bdef-124">Usar toocreate colocar sin formato de datos una nueva subordinada o subordinado de tooupdate Hola todo en una dirección URL de servidor definido.</span><span class="sxs-lookup"><span data-stu-id="9bdef-124">Use PUT Raw data toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="9bdef-125">Donde hello subordinado es una secuencia, es decir, datos no estructurada, p. ej.</span><span class="sxs-lookup"><span data-stu-id="9bdef-125">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="9bdef-126">un archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="9bdef-126">a text file.</span></span>  <span data-ttu-id="9bdef-127">PUT es idempotente para varias repeticiones dará como resultado Hola mismo estado, es decir</span><span class="sxs-lookup"><span data-stu-id="9bdef-127">PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="9bdef-128">x = 5.</span><span class="sxs-lookup"><span data-stu-id="9bdef-128">x=5.</span></span>  <span data-ttu-id="9bdef-129">Put debe usarse con hello completas de contenidos de hello especificada recursos.</span><span class="sxs-lookup"><span data-stu-id="9bdef-129">Put should be used with hello full content of hello specified resource.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="CancelBuild” ReturnType="Raw(text/plain)" d:AllowedHttpMethods="PUT" d:EncodeParameterValues="true" d:BaseUri=” http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Cancel Build</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="9bdef-130">Ejemplo: FunctionImport para los datos de "Raw" devueltos mediante "GET"</span><span class="sxs-lookup"><span data-stu-id="9bdef-130">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="9bdef-131">Use obtener sin procesar datos tooreturn subordinado que no está estructurado, es decir, texto.</span><span class="sxs-lookup"><span data-stu-id="9bdef-131">Use GET Raw data tooreturn a subordinate that is unstructured, i.e. text.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="GetModelUsageFile" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="GET" d:BaseUri="https://cmla.cloudapp.net/api2/model/builder/build?buildId={buildId}&amp;apiVersion={apiVersion}">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Download A Models Usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Accept" d:Value="application/xml,application/xhtml+xml,text/html;" />
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="9bdef-132">Ejemplo: FunctionImport para "Paging" a través de los datos devueltos</span><span class="sxs-lookup"><span data-stu-id="9bdef-132">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="9bdef-133">Use la paginación RESTful de implementación a través de sus datos con GET.</span><span class="sxs-lookup"><span data-stu-id="9bdef-133">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="9bdef-134">Paginación predeterminada se establece too100 filas por página de datos.</span><span class="sxs-lookup"><span data-stu-id="9bdef-134">Default paging is set too100 row per page of data.</span></span>

        <EntitySet Name=”CropEntitySet" EntityType="MyOffer.CropEntity" />
        <FunctionImport    Name="GetCropReport" EntitySet="CropEntitySet” ReturnType="Collection(MyOffer.CropEntity)" d:EmitSelfLink="false" d:EncodeParameterValues="true" d:Paging="SkipTake" d:MaxPageSize="100" d:BaseUri="http://api.mydata.org/Crop? report={report}&amp;series={series}&amp;start={$skip}&amp;size=100">
        <Parameter Name="report" Type="Int32" Mode="In" Nullable="false" d:SampleValues="4"  d:enum="1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19"  />
        <Parameter Name="series"    Type="String"    Mode="In" Nullable="false" d:SampleValues="FARM" />
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="text/xml;charset=UTF-8" />
        </d:Headers>
        <d:Namespaces>
        <d:Namespace d:Prefix="diffgr" d:Uri="urn:schemas-microsoft-com:xml-diffgram-v1" />
        </d:Namespaces>
        </FunctionImport>

## <a name="see-also"></a><span data-ttu-id="9bdef-135">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="9bdef-135">See Also</span></span>
* <span data-ttu-id="9bdef-136">Si está interesado en conocer Hola proceso general de asignación de OData y su propósito, lea este artículo [asignación de OData del servicio de datos](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definiciones, estructuras e instrucciones.</span><span class="sxs-lookup"><span data-stu-id="9bdef-136">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="9bdef-137">Si está interesado en el aprendizaje y nodos de descripción Hola específicos y sus parámetros, lea este artículo [nodos de asignación de datos de servicio OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para las definiciones y explicaciones, ejemplos y contexto de casos de uso.</span><span class="sxs-lookup"><span data-stu-id="9bdef-137">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="9bdef-138">toohello tooreturn lo prescrito, ruta de acceso para publicar un servicio de datos de toohello Azure Marketplace, lea este artículo [Guía de publicación de servicio de datos](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="9bdef-138">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

