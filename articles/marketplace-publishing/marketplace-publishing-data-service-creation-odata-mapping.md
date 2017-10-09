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
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a>Asignación de un tooOData de servicio web existente a través de CSDL
> [!IMPORTANT]
> **En este momento, ya no se pueden incorporar nuevos editores del Servicio de datos. No se aprobarán nuevos servicios de datos para mostrarse en lista.** Si tiene una aplicación de negocio de SaaS desea toopublish en AppSource encontrará información más [aquí](https://appsource.microsoft.com/partners). Si tiene aplicaciones IaaS o desarrollador del servicio quiere como toopublish en Azure Marketplace también puede encontrar más información [aquí](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Este artículo ofrece información general acerca de cómo toouse un toomap un tooan de servicio existente servicio compatible de OData CSDL. Se explica cómo el documento de asignación de Hola de toocreate (CSDL) que transforma la solicitud de entrada de Hola de Hola cliente a través de una llamada al servicio y Hola había salida a cliente de toohello (datos) a través de una fuente compatible de OData. Microsoft Azure Marketplace expone los usuarios finales de servicios toohello mediante Protocolo de OData de Hola. Los proveedores de contenido (propietarios de los datos) exponen los servicios de diversas formas, como REST, SOAP, etc.

## <a name="what-is-a-csdl-and-its-structure"></a>¿Qué es un CSDL y cuál es su estructura?
Un CSDL (lenguaje de definición de esquemas conceptuales) es una especificación que define cómo un servicio web toodescribe o base de datos en común service XML palabras toohello Azure Marketplace.

Información general simple de hello **flujo de solicitud:**

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

Hola **flujo de datos** en hello dirección opuesta:

  `Client <- Azure Marketplace <- Content Provider’s WebService`

**Figura 1** con los diagramas de cómo un cliente puede obtener datos de un proveedor de contenido (el servicio), vaya a través de hello Azure Marketplace.  Hola CSDL se utiliza por solicitud de hello asignación/transformación componente toohandle hello y pasan datos entre los servicios y Hola que solicita el cliente del proveedor de hello contenido.

*Figura 1: Flujo detallado desde la solicitud del proveedor de toocontent de cliente a través de Azure Marketplace*

  ![dibujo](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

Para obtener información sobre Atom, Pub Atom y protocolo de OData de hello en qué compilación de las extensiones de Azure Marketplace de hello, consulte: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)

Extracto desde encima de vínculo: *"hello de Open Data protocol (OData de ahora en adelante denominado tooas) de hello sirve protocolo tooprovide basado en REST para operaciones de estilo CRUD (crear, leer, actualizar y eliminar) con los recursos que se exponen como servicios de datos. Un "servicio de datos" es un punto de conexión donde hay datos expuestos desde una o más "colecciones", cada una de las cuales con cero o más "entradas", que consisten en pares de tipo nombre-valor. OData está publicada por Microsoft en estándares OASIS (Organization para hello Advancement of Standards estructurado de información) para que cualquiera que desea toocan crear servidores, clientes o herramientas que no tengan derechos de autor o restricciones."*

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a>Tres partes esenciales que tienen toobe definida por hello CSDL son:
* Hola **extremo** de proveedor de servicios de hello hello Web dirección (URI) del servicio de Hola
* Hola **parámetros de datos** que se pasa como entrada toohello proveedor de servicios de definiciones de Hola de parámetros de Hola se envía el servicio del proveedor de toohello contenido toohello tipo de datos.
* **Esquema** de datos de Hola que se devuelve el esquema de Hola toohello solicitar servicio de datos de Hola se entregan al servicio del proveedor de hello contenido, incluidos los tipos de contenedor, colecciones o tablas, variables y columnas y los datos.

Hola siguiente diagrama muestra un resumen del flujo de Hola desde donde hello cliente entra en hello OData (servicio de llamada toohello del proveedor de contenido web) de la instrucción toogetting Hola resultados/auxiliar de datos de.

  ![dibujo](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a>Pasos:
1. El cliente envía la solicitud a través de la llamada al servicio junto con los parámetros de entrada definidos en XML toohello Azure Marketplace
2. CSDL es toovalidate usado Hola llamada al servicio.
   * Hello con formato de llamada de servicio, a continuación, envía toohello servicio de proveedores de contenido hello Azure Marketplace
3. ejecuta hello Webservice y valida los acción Hola de hello verbo Http (es decir, GET) se devuelven datos de hello tooAzure Marketplace que Hola solicitó los datos (si existe) es expone en formato XML toohello cliente usando Hola asignación definida en hello CSDL.
4. Hola cliente se envía datos de hello (si existe) en formato XML o JSON

## <a name="definitions"></a>Definiciones
### <a name="odata-atom-pub"></a>OData ATOM Pub
Establezca una publicación ATOM de extensión toohello donde cada entrada representa una fila de un resultado. elemento de contenido de Hola de entrada de hello está toocontain mejorada Hola valores de fila de hello – como pares clave / valor. Puede encontrar más información en este vínculo: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)

### <a name="csdl---conceptual-schema-definition-language"></a>CSDL: lenguaje de definición de esquemas conceptuales
Permitir definir funciones (SPROC) y entidades expuestas a través de una base de datos. Puede encontrar más información en este vínculo: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)  

> [!TIP]
> Haga clic en hello **otras versiones** lista desplegable y seleccione una versión si no ve el artículo de Hola.
> 
> 

### <a name="edm---entry-data-model"></a>EDM: modelo de datos de entrada
* Información general: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* Presentación técnica: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* Tipos de datos: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

siguiente Hello muestra hello detallada tooRight izquierdo flujo desde donde hello cliente entra en hello OData (servicio de llamada toohello del proveedor de contenido web) de la instrucción toogetting Hola resultados/auxiliar de datos:

  ![dibujo](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a>Aspectos básicos de CSDL
Un CSDL (lenguaje de definición de esquemas conceptuales) es una especificación que define cómo un servicio web toodescribe o base de datos en común service XML palabras toohello Azure Marketplace. Describe el CSDL Hola crítico piezas que **hace posible pasar Hola de datos de origen de datos de hello toohello Azure Marketplace.** los elementos principales de Hola se describen a continuación:

* Información de interfaz que describe todas las funciones disponibles al público (nodo FunctionImport).
* Información de tipo de datos para todas las solicitudes de mensajes (entrada) y respuestas de mensajes (salidas) (nodos EntityContainer/EntitySet/EntityType).
* Información sobre toobe de protocolo de transporte de Hola de enlace usa (nodo de encabezado)
* Información de dirección para la localización de hello especifica servicio (BaseURI (atributo)

En pocas palabras, Hola CSDL representa un contrato de independiente de la plataforma y el lenguaje entre el solicitante de servicio de Hola y proveedor de servicios de Hola. Con hello CSDL, un cliente puede localizar un servicio de base de datos o servicio web e invocar cualquiera de sus funciones disponibles públicamente.

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a>Relacionados con una base de datos CSDL tooa o una colección
**Hola especificación de CSDL**

CSDL es la gramática de XML para describir un servicio web. especificación del Hola se divide en 4 elementos principales: EntitySet, FunctionImport; Espacio de nombres y EntityType.

toomake este toounderstand más fácil de abstracción permite relacionar una tabla de tooa CSDL.

Recuerde:

  CSDL representa un contrato independiente de la plataforma y el lenguaje entre hello **solicitante de servicio** hello y **proveedor de servicios**. Con el CSDL, un **cliente** puede ubicar un **servicio web o un servicio de base de datos** e invocar cualquiera de sus **funciones** disponibles al público.

Para un Hola de servicio de datos cuatro partes de un CSDL pueden considerarse en términos de una base de datos, la tabla, la columna y el procedimiento almacenado.

Relacione estos elementos de la siguiente manera en un servicio de datos:

* EntityContainer ~=  Base de datos
* EntitySet ~= Tabla
* EntityType ~= Columnas
* FunctionImport ~= Procedimiento almacenado

**Verbos HTTP permitidos**

* GET-devuelve valores de base de datos de hello (devuelve una colección)
* Usar POST: toopass datos tooand opcional los valores devueltos de Hola db (crear una nueva entrada en la colección de hello, valor devuelto/URI del Id.)
* ELIMINAR: elimina datos de Hola DB (se elimina una colección)
* PUT: actualiza los datos de una base de datos (reemplaza una colección o crea una).

## <a name="metadatamapping-document"></a>Documento de asignación/metadatos
documento de metadatos y asignación de Hello es usado toomap web existentes del proveedor de contenido de servicios para que se puede exponer como un servicio web OData por sistema de Azure Marketplace de Hola. Se basa en CSDL e implementa algunas extensiones tooCSDL tooaccommodate hello las necesidades de REST según los servicios web expuestos a través de Azure Marketplace. extensiones de Hola se encuentran en hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) espacio de nombres.

Un ejemplo de Hola CSDL: (copiar y pegar Hola ejemplo CSDL en un editor XML siguiente y cambiar toomatch su servicio.  A continuación, pegue en asignación de CSDL en DataService pestaña al crear el servicio en hello [Portal de publicación de Azure Marketplace](https://publish.windowsazure.com)).

**Términos:** referentes Hola CSDL términos toohello [Portal de publicación](https://publish.windowsazure.com) términos de la interfaz de usuario (PPUI).

* Ofrecer "Title" Hola PPUI relaciona tooMyWebOffer
* MyCompany en hello PPUI relaciona demasiado**Publisher DisplayName** en hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) interfaz de usuario
* La API relaciona tooa Web o servicio de datos (un Plan en hello PPUI)

**Jerarquía:** una empresa (proveedor de contenido) es propietaria de ofertas que tienen planes, es decir, servicios, que se alinean con una API.

### <a name="webservice-csdl-example"></a>Ejemplo de CSDL de servicio web
Se conecta el servicio tooa que está exponiendo un extremo de la aplicación web (por ejemplo, una aplicación de C#)

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
> Ver más ejemplos de servicio Web de CSDL en el artículo hello [tooOData de servicio a través de CSDLs de web de ejemplos de asignación existente](marketplace-publishing-data-service-creation-odata-mapping-examples.md)
> 
> 

### <a name="dataservice-csdl-example"></a>Ejemplo de CSDL de servicio de datos
Conecta el servicio tooa que está exponiendo una tabla de base de datos o vista como un punto de conexión de ejemplo siguiente se muestra dos que interfaces API para la base de datos en función de CSDL de API (puede usar vistas en lugar de tablas).

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

## <a name="see-also"></a>Otras referencias
* Si está interesado en el aprendizaje y nodos de descripción Hola específicos y sus parámetros, lea este artículo [nodos de asignación de datos de servicio OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para las definiciones y explicaciones, ejemplos y contexto de casos de uso.
* Si está interesado en Revisar ejemplos, lea este artículo [ejemplos de asignación de datos de servicios OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee código de ejemplo y comprender la sintaxis del código y el contexto.
* toohello tooreturn lo prescrito, ruta de acceso para publicar un servicio de datos de toohello Azure Marketplace, lea este artículo [Guía de publicación de servicio de datos](marketplace-publishing-data-service-creation.md).

