---
title: aaaGuide toocreating un servicio de datos para hello Marketplace | Documentos de Microsoft
description: "Instrucciones detalladas de cómo toocreate, certificar e implementar un servicio de datos para la venta en hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a><span data-ttu-id="ce6ac-103">Asignación de un tooOData de servicio web existente a través de CSDL</span><span class="sxs-lookup"><span data-stu-id="ce6ac-103">Mapping an existing web service tooOData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ce6ac-104">**En este momento, ya no se pueden incorporar nuevos editores del Servicio de datos. No se aprobarán nuevos servicios de datos para mostrarse en lista.**</span><span class="sxs-lookup"><span data-stu-id="ce6ac-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="ce6ac-105">Si tiene una aplicación de negocio de SaaS desea toopublish en AppSource encontrará información más [aquí](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="ce6ac-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="ce6ac-106">Si tiene aplicaciones IaaS o desarrollador del servicio quiere como toopublish en Azure Marketplace también puede encontrar más información [aquí](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="ce6ac-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="ce6ac-107">Este artículo ofrece información general acerca de cómo toouse un toomap un tooan de servicio existente servicio compatible de OData CSDL.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-107">This article gives an overview on how toouse a CSDL toomap an existing service tooan OData compatible service.</span></span> <span data-ttu-id="ce6ac-108">Se explica cómo el documento de asignación de Hola de toocreate (CSDL) que transforma la solicitud de entrada de Hola de Hola cliente a través de una llamada al servicio y Hola había salida a cliente de toohello (datos) a través de una fuente compatible de OData.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-108">It explains how toocreate hello mapping document (CSDL) that transforms hello input request from hello client via a service call and hello output (data) back toohello client via an OData compatible feed.</span></span> <span data-ttu-id="ce6ac-109">Microsoft Azure Marketplace expone los usuarios finales de servicios toohello mediante Protocolo de OData de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-109">Microsoft’s Azure Marketplace exposes services toohello end-users by using hello OData protocol.</span></span> <span data-ttu-id="ce6ac-110">Los proveedores de contenido (propietarios de los datos) exponen los servicios de diversas formas, como REST, SOAP, etc.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="ce6ac-111">¿Qué es un CSDL y cuál es su estructura?</span><span class="sxs-lookup"><span data-stu-id="ce6ac-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="ce6ac-112">Un CSDL (lenguaje de definición de esquemas conceptuales) es una especificación que define cómo un servicio web toodescribe o base de datos en común service XML palabras toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span>

<span data-ttu-id="ce6ac-113">Información general simple de hello **flujo de solicitud:**</span><span class="sxs-lookup"><span data-stu-id="ce6ac-113">Simple overview of hello **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="ce6ac-114">Hola **flujo de datos** en hello dirección opuesta:</span><span class="sxs-lookup"><span data-stu-id="ce6ac-114">hello **data flow** is in hello opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="ce6ac-115">**Figura 1** con los diagramas de cómo un cliente puede obtener datos de un proveedor de contenido (el servicio), vaya a través de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through hello Azure Marketplace.</span></span>  <span data-ttu-id="ce6ac-116">Hola CSDL se utiliza por solicitud de hello asignación/transformación componente toohandle hello y pasan datos entre los servicios y Hola que solicita el cliente del proveedor de hello contenido.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-116">hello CSDL is used by hello Mapping/Transformation component toohandle hello request and data pass between hello content provider’s service(s) and hello requesting client.</span></span>

<span data-ttu-id="ce6ac-117">*Figura 1: Flujo detallado desde la solicitud del proveedor de toocontent de cliente a través de Azure Marketplace*</span><span class="sxs-lookup"><span data-stu-id="ce6ac-117">*Figure 1: Detailed flow from requesting client toocontent provider via Azure Marketplace*</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="ce6ac-119">Para obtener información sobre Atom, Pub Atom y protocolo de OData de hello en qué compilación de las extensiones de Azure Marketplace de hello, consulte: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-119">For background on Atom, Atom Pub, and hello OData protocol upon which hello Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="ce6ac-120">Extracto desde encima de vínculo: *"hello de Open Data protocol (OData de ahora en adelante denominado tooas) de hello sirve protocolo tooprovide basado en REST para operaciones de estilo CRUD (crear, leer, actualizar y eliminar) con los recursos que se exponen como servicios de datos. Un "servicio de datos" es un punto de conexión donde hay datos expuestos desde una o más "colecciones", cada una de las cuales con cero o más "entradas", que consisten en pares de tipo nombre-valor. OData está publicada por Microsoft en estándares OASIS (Organization para hello Advancement of Standards estructurado de información) para que cualquiera que desea toocan crear servidores, clientes o herramientas que no tengan derechos de autor o restricciones."*</span><span class="sxs-lookup"><span data-stu-id="ce6ac-120">Excerpt from above link: *“hello purpose of hello Open Data protocol (hereafter referred tooas OData) is tooprovide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for hello Advancement of Structured Information Standards) Standards so that anyone that wants toocan build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a><span data-ttu-id="ce6ac-121">Tres partes esenciales que tienen toobe definida por hello CSDL son:</span><span class="sxs-lookup"><span data-stu-id="ce6ac-121">Three Critical Pieces that have toobe defined by hello CSDL are:</span></span>
* <span data-ttu-id="ce6ac-122">Hola **extremo** de proveedor de servicios de hello hello Web dirección (URI) del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="ce6ac-122">hello **endpoint** of hello Service Provider hello Web Address (URI) of hello Service</span></span>
* <span data-ttu-id="ce6ac-123">Hola **parámetros de datos** que se pasa como entrada toohello proveedor de servicios de definiciones de Hola de parámetros de Hola se envía el servicio del proveedor de toohello contenido toohello tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-123">hello **data parameters** being passed as input toohello Service Provider hello definitions of hello parameters being sent toohello Content Provider’s service down toohello data type.</span></span>
* <span data-ttu-id="ce6ac-124">**Esquema** de datos de Hola que se devuelve el esquema de Hola toohello solicitar servicio de datos de Hola se entregan al servicio del proveedor de hello contenido, incluidos los tipos de contenedor, colecciones o tablas, variables y columnas y los datos.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-124">**Schema** of hello data being returned toohello Requesting Service hello schema of hello data being delivered by hello Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="ce6ac-125">Hola siguiente diagrama muestra un resumen del flujo de Hola desde donde hello cliente entra en hello OData (servicio de llamada toohello del proveedor de contenido web) de la instrucción toogetting Hola resultados/auxiliar de datos de.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-125">hello following diagram shows an overview of hello flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back.</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="ce6ac-127">Pasos:</span><span class="sxs-lookup"><span data-stu-id="ce6ac-127">Steps:</span></span>
1. <span data-ttu-id="ce6ac-128">El cliente envía la solicitud a través de la llamada al servicio junto con los parámetros de entrada definidos en XML toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ce6ac-128">Client sends request via Service call complete with Input Parameters defined in XML toohello Azure Marketplace</span></span>
2. <span data-ttu-id="ce6ac-129">CSDL es toovalidate usado Hola llamada al servicio.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-129">CSDL is used toovalidate hello Service call.</span></span>
   * <span data-ttu-id="ce6ac-130">Hello con formato de llamada de servicio, a continuación, envía toohello servicio de proveedores de contenido hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ce6ac-130">hello Formatted Service Call is then sent toohello Content Providers Service by hello Azure Marketplace</span></span>
3. <span data-ttu-id="ce6ac-131">ejecuta hello Webservice y valida los acción Hola de hello verbo Http (es decir, GET) se devuelven datos de hello tooAzure Marketplace que Hola solicitó los datos (si existe) es expone en formato XML toohello cliente usando Hola asignación definida en hello CSDL.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-131">hello Webservice executes and preforms hello action of hello Http Verb (i.e. GET) hello data is returned tooAzure Marketplace where hello requested data (if any) is exposes in XML Format toohello Client using hello Mapping defined in hello CSDL.</span></span>
4. <span data-ttu-id="ce6ac-132">Hola cliente se envía datos de hello (si existe) en formato XML o JSON</span><span class="sxs-lookup"><span data-stu-id="ce6ac-132">hello Client is sent hello data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="ce6ac-133">Definiciones</span><span class="sxs-lookup"><span data-stu-id="ce6ac-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="ce6ac-134">OData ATOM Pub</span><span class="sxs-lookup"><span data-stu-id="ce6ac-134">OData ATOM pub</span></span>
<span data-ttu-id="ce6ac-135">Establezca una publicación ATOM de extensión toohello donde cada entrada representa una fila de un resultado.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-135">An extension toohello ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="ce6ac-136">elemento de contenido de Hola de entrada de hello está toocontain mejorada Hola valores de fila de hello – como pares clave / valor.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-136">hello content part of hello entry is enhanced toocontain hello values of hello row – as key value pairs.</span></span> <span data-ttu-id="ce6ac-137">Puede encontrar más información en este vínculo: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="ce6ac-138">CSDL: lenguaje de definición de esquemas conceptuales</span><span class="sxs-lookup"><span data-stu-id="ce6ac-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="ce6ac-139">Permitir definir funciones (SPROC) y entidades expuestas a través de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="ce6ac-140">Puede encontrar más información en este vínculo: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="ce6ac-141">Haga clic en hello **otras versiones** lista desplegable y seleccione una versión si no ve el artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-141">Click hello **other versions** dropdown and select a version if you don’t see hello article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="ce6ac-142">EDM: modelo de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="ce6ac-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="ce6ac-143">Información general: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="ce6ac-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="ce6ac-144">Presentación técnica: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="ce6ac-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="ce6ac-145">Tipos de datos: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="ce6ac-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="ce6ac-146">siguiente Hello muestra hello detallada tooRight izquierdo flujo desde donde hello cliente entra en hello OData (servicio de llamada toohello del proveedor de contenido web) de la instrucción toogetting Hola resultados/auxiliar de datos:</span><span class="sxs-lookup"><span data-stu-id="ce6ac-146">hello following shows hello detailed Left tooRight flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back:</span></span>

  ![dibujo](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="ce6ac-148">Aspectos básicos de CSDL</span><span class="sxs-lookup"><span data-stu-id="ce6ac-148">CSDL Basics</span></span>
<span data-ttu-id="ce6ac-149">Un CSDL (lenguaje de definición de esquemas conceptuales) es una especificación que define cómo un servicio web toodescribe o base de datos en común service XML palabras toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span> <span data-ttu-id="ce6ac-150">Describe el CSDL Hola crítico piezas que **hace posible pasar Hola de datos de origen de datos de hello toohello Azure Marketplace.**</span><span class="sxs-lookup"><span data-stu-id="ce6ac-150">CSDL describes hello critical pieces that **makes hello passing of data from hello Data Source toohello Azure Marketplace possible.**</span></span> <span data-ttu-id="ce6ac-151">los elementos principales de Hola se describen a continuación:</span><span class="sxs-lookup"><span data-stu-id="ce6ac-151">hello main pieces are described here:</span></span>

* <span data-ttu-id="ce6ac-152">Información de interfaz que describe todas las funciones disponibles al público (nodo FunctionImport).</span><span class="sxs-lookup"><span data-stu-id="ce6ac-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="ce6ac-153">Información de tipo de datos para todas las solicitudes de mensajes (entrada) y respuestas de mensajes (salidas) (nodos EntityContainer/EntitySet/EntityType).</span><span class="sxs-lookup"><span data-stu-id="ce6ac-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="ce6ac-154">Información sobre toobe de protocolo de transporte de Hola de enlace usa (nodo de encabezado)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-154">Binding information about hello transport protocol toobe used (Header Node)</span></span>
* <span data-ttu-id="ce6ac-155">Información de dirección para la localización de hello especifica servicio (BaseURI (atributo)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-155">Address information for locating hello specified service (BaseURI attribute)</span></span>

<span data-ttu-id="ce6ac-156">En pocas palabras, Hola CSDL representa un contrato de independiente de la plataforma y el lenguaje entre el solicitante de servicio de Hola y proveedor de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-156">In a nutshell, hello CSDL represents a platform- and language-independent contract between hello service requestor and hello service provider.</span></span> <span data-ttu-id="ce6ac-157">Con hello CSDL, un cliente puede localizar un servicio de base de datos o servicio web e invocar cualquiera de sus funciones disponibles públicamente.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-157">Using hello CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a><span data-ttu-id="ce6ac-158">Relacionados con una base de datos CSDL tooa o una colección</span><span class="sxs-lookup"><span data-stu-id="ce6ac-158">Relating a CSDL tooa Database or a Collection</span></span>
<span data-ttu-id="ce6ac-159">**Hola especificación de CSDL**</span><span class="sxs-lookup"><span data-stu-id="ce6ac-159">**hello CSDL Specification**</span></span>

<span data-ttu-id="ce6ac-160">CSDL es la gramática de XML para describir un servicio web.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="ce6ac-161">especificación del Hola se divide en 4 elementos principales: EntitySet, FunctionImport; Espacio de nombres y EntityType.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-161">hello specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="ce6ac-162">toomake este toounderstand más fácil de abstracción permite relacionar una tabla de tooa CSDL.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-162">toomake this abstraction easier toounderstand lets relate a CSDL tooa table.</span></span>

<span data-ttu-id="ce6ac-163">Recuerde:</span><span class="sxs-lookup"><span data-stu-id="ce6ac-163">Remember;</span></span>

  <span data-ttu-id="ce6ac-164">CSDL representa un contrato independiente de la plataforma y el lenguaje entre hello **solicitante de servicio** hello y **proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-164">CSDL represents a platform- and language-independent contract between hello **service requestor** and hello **service provider**.</span></span> <span data-ttu-id="ce6ac-165">Con el CSDL, un **cliente** puede ubicar un **servicio web o un servicio de base de datos** e invocar cualquiera de sus **funciones** disponibles al público.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="ce6ac-166">Para un Hola de servicio de datos cuatro partes de un CSDL pueden considerarse en términos de una base de datos, la tabla, la columna y el procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-166">For a Data Service hello four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="ce6ac-167">Relacione estos elementos de la siguiente manera en un servicio de datos:</span><span class="sxs-lookup"><span data-stu-id="ce6ac-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="ce6ac-168">EntityContainer ~=  Base de datos</span><span class="sxs-lookup"><span data-stu-id="ce6ac-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="ce6ac-169">EntitySet ~= Tabla</span><span class="sxs-lookup"><span data-stu-id="ce6ac-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="ce6ac-170">EntityType ~= Columnas</span><span class="sxs-lookup"><span data-stu-id="ce6ac-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="ce6ac-171">FunctionImport ~= Procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="ce6ac-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="ce6ac-172">**Verbos HTTP permitidos**</span><span class="sxs-lookup"><span data-stu-id="ce6ac-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="ce6ac-173">GET-devuelve valores de base de datos de hello (devuelve una colección)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-173">GET – returns values from hello db (returns a Collection)</span></span>
* <span data-ttu-id="ce6ac-174">Usar POST: toopass datos tooand opcional los valores devueltos de Hola db (crear una nueva entrada en la colección de hello, valor devuelto/URI del Id.)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-174">POST – used toopass data tooand optional return values from hello db (Create a new entry in hello collection, return id/URI)</span></span>
* <span data-ttu-id="ce6ac-175">ELIMINAR: elimina datos de Hola DB (se elimina una colección)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-175">DELETE – Deletes data from hello DB (Deletes a collection)</span></span>
* <span data-ttu-id="ce6ac-176">PUT: actualiza los datos de una base de datos (reemplaza una colección o crea una).</span><span class="sxs-lookup"><span data-stu-id="ce6ac-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="ce6ac-177">Documento de asignación/metadatos</span><span class="sxs-lookup"><span data-stu-id="ce6ac-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="ce6ac-178">documento de metadatos y asignación de Hello es usado toomap web existentes del proveedor de contenido de servicios para que se puede exponer como un servicio web OData por sistema de Azure Marketplace de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-178">hello metadata/mapping document is used toomap a content provider’s existing web services so that it can be exposed as an OData web service by hello Azure Marketplace system.</span></span> <span data-ttu-id="ce6ac-179">Se basa en CSDL e implementa algunas extensiones tooCSDL tooaccommodate hello las necesidades de REST según los servicios web expuestos a través de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-179">It is based on CSDL and implements a few extensions tooCSDL tooaccommodate hello needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="ce6ac-180">extensiones de Hola se encuentran en hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-180">hello extensions are found in hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="ce6ac-181">Un ejemplo de Hola CSDL: (copiar y pegar Hola ejemplo CSDL en un editor XML siguiente y cambiar toomatch su servicio.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-181">An example of hello CSDL follows:  (Copy and paste hello below example CSDL into an XML editor and change toomatch your Service.</span></span>  <span data-ttu-id="ce6ac-182">A continuación, pegue en asignación de CSDL en DataService pestaña al crear el servicio en hello [Portal de publicación de Azure Marketplace](https://publish.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="ce6ac-182">Then paste into CSDL Mapping under DataService tab when creating your service in hello  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="ce6ac-183">**Términos:** referentes Hola CSDL términos toohello [Portal de publicación](https://publish.windowsazure.com) términos de la interfaz de usuario (PPUI).</span><span class="sxs-lookup"><span data-stu-id="ce6ac-183">**Terms:** Relating hello CSDL terms toohello [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="ce6ac-184">Ofrecer "Title" Hola PPUI relaciona tooMyWebOffer</span><span class="sxs-lookup"><span data-stu-id="ce6ac-184">Offer “Title” in hello PPUI relates tooMyWebOffer</span></span>
* <span data-ttu-id="ce6ac-185">MyCompany en hello PPUI relaciona demasiado**Publisher DisplayName** en hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="ce6ac-185">MyCompany in hello PPUI relates too**Publisher Display Name** in hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="ce6ac-186">La API relaciona tooa Web o servicio de datos (un Plan en hello PPUI)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-186">Your API relates tooa Web or Data Service (a Plan in hello PPUI)</span></span>

<span data-ttu-id="ce6ac-187">**Jerarquía:** una empresa (proveedor de contenido) es propietaria de ofertas que tienen planes, es decir, servicios, que se alinean con una API.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="ce6ac-188">Ejemplo de CSDL de servicio web</span><span class="sxs-lookup"><span data-stu-id="ce6ac-188">WebService CSDL Example</span></span>
<span data-ttu-id="ce6ac-189">Se conecta el servicio tooa que está exponiendo un extremo de la aplicación web (por ejemplo, una aplicación de C#)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-189">Connects tooa service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> <span data-ttu-id="ce6ac-190">Ver más ejemplos de servicio Web de CSDL en el artículo hello [tooOData de servicio a través de CSDLs de web de ejemplos de asignación existente](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="ce6ac-190">View more CSDL Web Service examples in hello article [Examples of mapping an existing web service tooOData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="ce6ac-191">Ejemplo de CSDL de servicio de datos</span><span class="sxs-lookup"><span data-stu-id="ce6ac-191">DataService CSDL Example</span></span>
<span data-ttu-id="ce6ac-192">Conecta el servicio tooa que está exponiendo una tabla de base de datos o vista como un punto de conexión de ejemplo siguiente se muestra dos que interfaces API para la base de datos en función de CSDL de API (puede usar vistas en lugar de tablas).</span><span class="sxs-lookup"><span data-stu-id="ce6ac-192">Connects tooa service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a><span data-ttu-id="ce6ac-193">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ce6ac-193">See Also</span></span>
* <span data-ttu-id="ce6ac-194">Si está interesado en el aprendizaje y nodos de descripción Hola específicos y sus parámetros, lea este artículo [nodos de asignación de datos de servicio OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para las definiciones y explicaciones, ejemplos y contexto de casos de uso.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-194">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="ce6ac-195">Si está interesado en Revisar ejemplos, lea este artículo [ejemplos de asignación de datos de servicios OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee código de ejemplo y comprender la sintaxis del código y el contexto.</span><span class="sxs-lookup"><span data-stu-id="ce6ac-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="ce6ac-196">toohello tooreturn lo prescrito, ruta de acceso para publicar un servicio de datos de toohello Azure Marketplace, lea este artículo [Guía de publicación de servicio de datos](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="ce6ac-196">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

