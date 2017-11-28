---
title: aaaMove datos de un origen HTTP - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo usar Data Factory de Azure del origen de datos de toomove desde una implementación local o una nube de HTTP."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="7bfbb-103">Movimiento de datos desde un origen HTTP mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7bfbb-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="7bfbb-104">En este artículo se describe cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un tooa de punto de conexión HTTP en local y la nube admite el almacén de datos del receptor.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud HTTP endpoint tooa supported sink data store.</span></span> <span data-ttu-id="7bfbb-105">En este artículo se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo que presenta una visión general de movimiento de datos con la lista de hello y actividad de copia de almacenes de datos que se admiten como orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="7bfbb-106">Factoría de datos actualmente admite sólo mover datos de un elemento HTTP origen tooother almacenes de datos, pero no mover los datos de otros datos almacena destino tooan HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-106">Data factory currently supports only moving data from an HTTP source tooother data stores, but not moving data from other data stores tooan HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="7bfbb-107">Escenarios admitidos y tipos de autenticación</span><span class="sxs-lookup"><span data-stu-id="7bfbb-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="7bfbb-108">Puede usar estos datos de tooretrieve de conector HTTP de **extremo HTTP/s en la nube y locales** mediante HTTP **obtener** o **POST** método.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-108">You can use this HTTP connector tooretrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="7bfbb-109">se admite los siguientes tipos de autenticación de Hello: **Anonymous**, **básica**, **implícita**, **Windows**, y  **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-109">hello following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="7bfbb-110">Observe Hola diferencia que existe entre este conector y hello [conector de tabla Web](data-factory-web-table-connector.md) es: hello este último es usado tooextract tabla contenida de la página web HTML.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-110">Note hello difference between this connector and hello [Web table connector](data-factory-web-table-connector.md) is: hello latter is used tooextract table content from web HTML page.</span></span>

<span data-ttu-id="7bfbb-111">Cuando se copian datos desde un punto de conexión HTTP en local, necesita instalar una puerta de enlace de administración de datos en hello local entorno/VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="7bfbb-112">Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7bfbb-113">Introducción</span><span class="sxs-lookup"><span data-stu-id="7bfbb-113">Getting started</span></span>
<span data-ttu-id="7bfbb-114">Puede crear una canalización con una actividad de copia que mueva datos desde un origen HTTP mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="7bfbb-115">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-115">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="7bfbb-116">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="7bfbb-117">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-117">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7bfbb-118">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="7bfbb-119">Para JSON muestrea los datos de toocopy de HTTP origen tooAzure almacenamiento de blobs, vea [ejemplos JSON](#json-examples) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-119">For JSON samples toocopy data from HTTP source tooAzure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7bfbb-120">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="7bfbb-120">Linked service properties</span></span>
<span data-ttu-id="7bfbb-121">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooHTTP vinculado.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-121">hello following table provides description for JSON elements specific tooHTTP linked service.</span></span>

| <span data-ttu-id="7bfbb-122">Propiedad</span><span class="sxs-lookup"><span data-stu-id="7bfbb-122">Property</span></span> | <span data-ttu-id="7bfbb-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="7bfbb-123">Description</span></span> | <span data-ttu-id="7bfbb-124">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7bfbb-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7bfbb-125">type</span><span class="sxs-lookup"><span data-stu-id="7bfbb-125">type</span></span> | <span data-ttu-id="7bfbb-126">propiedad de tipo Hello debe establecerse en: `Http`.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-126">hello type property must be set to: `Http`.</span></span> | <span data-ttu-id="7bfbb-127">Sí</span><span class="sxs-lookup"><span data-stu-id="7bfbb-127">Yes</span></span> |
| <span data-ttu-id="7bfbb-128">url</span><span class="sxs-lookup"><span data-stu-id="7bfbb-128">url</span></span> | <span data-ttu-id="7bfbb-129">Basar la dirección URL toohello servidor Web</span><span class="sxs-lookup"><span data-stu-id="7bfbb-129">Base URL toohello Web Server</span></span> | <span data-ttu-id="7bfbb-130">Sí</span><span class="sxs-lookup"><span data-stu-id="7bfbb-130">Yes</span></span> |
| <span data-ttu-id="7bfbb-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="7bfbb-131">authenticationType</span></span> | <span data-ttu-id="7bfbb-132">Especifica el tipo de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-132">Specifies hello authentication type.</span></span> <span data-ttu-id="7bfbb-133">Los valores permitidos son: **Anonymous**, **Basic**, **Digest**, **Windows** y **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="7bfbb-134">Consulte toosections por debajo de esta tabla en más propiedades y ejemplos JSON para esos tipos de autenticación, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-134">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="7bfbb-135">Sí</span><span class="sxs-lookup"><span data-stu-id="7bfbb-135">Yes</span></span> |
| <span data-ttu-id="7bfbb-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="7bfbb-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="7bfbb-137">Especifique si el servidor de tooenable SSL la validación de certificados si el origen es el servidor de Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="7bfbb-137">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="7bfbb-138">No, el valor predeterminado es True.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-138">No, default is true</span></span> |
| <span data-ttu-id="7bfbb-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="7bfbb-139">gatewayName</span></span> | <span data-ttu-id="7bfbb-140">Nombre de hello Data Management Gateway tooconnect tooan local de origen HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-140">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="7bfbb-141">Sí si va a copiar datos desde un origen HTTP local.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="7bfbb-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="7bfbb-142">encryptedCredential</span></span> | <span data-ttu-id="7bfbb-143">Credenciales cifradas tooaccess Hola extremo HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-143">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="7bfbb-144">Generado automáticamente al configurar la información de autenticación de hello en copia asistente o hello ClickOnce cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-144">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="7bfbb-145">No.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-145">No.</span></span> <span data-ttu-id="7bfbb-146">Se aplica solo cuando se copian datos desde un servidor HTTP local.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="7bfbb-147">Vea [mover datos entre orígenes locales y en la nube Hola con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obtener más información acerca de cómo establecer las credenciales de origen de datos del conector local HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-147">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="7bfbb-148">Uso de la autenticación Basic, Digest o Windows</span><span class="sxs-lookup"><span data-stu-id="7bfbb-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="7bfbb-149">Establecer `authenticationType` como `Basic`, `Digest`, o `Windows`y especifique Hola propiedades siguientes, además de Hola el genérico de conector HTTP los descritos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="7bfbb-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="7bfbb-150">Propiedad</span><span class="sxs-lookup"><span data-stu-id="7bfbb-150">Property</span></span> | <span data-ttu-id="7bfbb-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="7bfbb-151">Description</span></span> | <span data-ttu-id="7bfbb-152">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7bfbb-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7bfbb-153">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="7bfbb-153">username</span></span> | <span data-ttu-id="7bfbb-154">Nombre de usuario tooaccess Hola extremo HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-154">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="7bfbb-155">Sí</span><span class="sxs-lookup"><span data-stu-id="7bfbb-155">Yes</span></span> |
| <span data-ttu-id="7bfbb-156">Contraseña</span><span class="sxs-lookup"><span data-stu-id="7bfbb-156">password</span></span> | <span data-ttu-id="7bfbb-157">Contraseña de usuario de hello (nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-157">Password for hello user (username).</span></span> | <span data-ttu-id="7bfbb-158">Sí</span><span class="sxs-lookup"><span data-stu-id="7bfbb-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="7bfbb-159">Ejemplo: Uso de la autenticación Basic, Digest o Windows</span><span class="sxs-lookup"><span data-stu-id="7bfbb-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="7bfbb-160">Uso de la autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="7bfbb-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="7bfbb-161">establecer la autenticación básica toouse, `authenticationType` como `ClientCertificate`y especifique Hola propiedades siguientes, además de Hola el genérico de conector HTTP los descritos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="7bfbb-161">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="7bfbb-162">Propiedad</span><span class="sxs-lookup"><span data-stu-id="7bfbb-162">Property</span></span> | <span data-ttu-id="7bfbb-163">Descripción</span><span class="sxs-lookup"><span data-stu-id="7bfbb-163">Description</span></span> | <span data-ttu-id="7bfbb-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7bfbb-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7bfbb-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="7bfbb-165">embeddedCertData</span></span> | <span data-ttu-id="7bfbb-166">contenido codificado en Base64 Hola de datos binarios del archivo de intercambio de información Personal (PFX) Hola.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-166">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="7bfbb-167">Especifique cualquier hello `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-167">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="7bfbb-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="7bfbb-168">certThumbprint</span></span> | <span data-ttu-id="7bfbb-169">Hola huella digital del certificado de Hola que se instaló en el almacén de certificados de la máquina de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-169">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="7bfbb-170">Se aplica solo cuando se copian datos desde un origen HTTP local.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="7bfbb-171">Especifique cualquier hello `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-171">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="7bfbb-172">Contraseña</span><span class="sxs-lookup"><span data-stu-id="7bfbb-172">password</span></span> | <span data-ttu-id="7bfbb-173">Contraseña asociada con el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-173">Password associated with hello certificate.</span></span> | <span data-ttu-id="7bfbb-174">No</span><span class="sxs-lookup"><span data-stu-id="7bfbb-174">No</span></span> |

<span data-ttu-id="7bfbb-175">Si usa `certThumbprint` para hello y autenticación de certificado está instalado en el almacén personal de hello del equipo local de hello, necesita que el servicio de puerta de enlace de toohello de toogrant Hola permiso de lectura:</span><span class="sxs-lookup"><span data-stu-id="7bfbb-175">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="7bfbb-176">Inicie Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="7bfbb-177">Agregar hello **certificados** complemento ese Hola destinos **equipo Local**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-177">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="7bfbb-178">Expanda **Certificados**, **Personal** y haga clic en **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="7bfbb-179">Haga clic en certificado Hola almacén personal de Hola y seleccione **todas las tareas**->**administrar claves privadas...**</span><span class="sxs-lookup"><span data-stu-id="7bfbb-179">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="7bfbb-180">En hello **seguridad** ficha, agregue la cuenta de usuario de hello en que se ejecuta el servicio de Host de Data Management Gateway con certificado de toohello de acceso de lectura de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-180">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="7bfbb-181">Ejemplo: Uso del certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="7bfbb-181">Example: using client certificate</span></span>
<span data-ttu-id="7bfbb-182">Esto vincula vínculos de servicio el servidor de web HTTP de datos generador tooan local.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-182">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="7bfbb-183">Utiliza un certificado de cliente que se instala en la máquina de hello con Data Management Gateway instalado.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-183">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="7bfbb-184">Ejemplo: Uso del certificado de cliente en un archivo</span><span class="sxs-lookup"><span data-stu-id="7bfbb-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="7bfbb-185">Esto vincula vínculos de servicio el servidor de web HTTP de datos generador tooan local.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-185">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="7bfbb-186">Utiliza un archivo de certificado de cliente en la máquina de hello con Data Management Gateway instalado.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-186">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="7bfbb-187">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="7bfbb-187">Dataset properties</span></span>
<span data-ttu-id="7bfbb-188">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-188">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7bfbb-189">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="7bfbb-190">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-190">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="7bfbb-191">sección typeProperties Hello para el conjunto de datos de tipo **Http** tiene Hola propiedades siguientes</span><span class="sxs-lookup"><span data-stu-id="7bfbb-191">hello typeProperties section for dataset of type **Http** has hello following properties</span></span>

| <span data-ttu-id="7bfbb-192">Propiedad</span><span class="sxs-lookup"><span data-stu-id="7bfbb-192">Property</span></span> | <span data-ttu-id="7bfbb-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="7bfbb-193">Description</span></span> | <span data-ttu-id="7bfbb-194">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7bfbb-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7bfbb-195">type</span><span class="sxs-lookup"><span data-stu-id="7bfbb-195">type</span></span> | <span data-ttu-id="7bfbb-196">Tipo de hello del conjunto de datos de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-196">Specified hello type of hello dataset.</span></span> <span data-ttu-id="7bfbb-197">debe establecerse demasiado`Http`.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-197">must be set too`Http`.</span></span> | <span data-ttu-id="7bfbb-198">Sí</span><span class="sxs-lookup"><span data-stu-id="7bfbb-198">Yes</span></span> |
| <span data-ttu-id="7bfbb-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="7bfbb-199">relativeUrl</span></span> | <span data-ttu-id="7bfbb-200">Un recurso de toohello de dirección URL relativo al que contiene los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-200">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="7bfbb-201">Cuando no se especifica la ruta de acceso, se usa solo dirección URL de hello especificada en definición de servicio vinculado de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-201">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="7bfbb-202">dirección URL dinámica tooconstruct, puede usar [funciones de factoría de datos y las variables del sistema](data-factory-functions-variables.md), por ejemplo, "relativeUrl": "$$Text.Format ('/ my/informe? mes = {0:yyyy}-{0:MM} & fmt = csv', SliceStart)".</span><span class="sxs-lookup"><span data-stu-id="7bfbb-202">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="7bfbb-203">No</span><span class="sxs-lookup"><span data-stu-id="7bfbb-203">No</span></span> |
| <span data-ttu-id="7bfbb-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="7bfbb-204">requestMethod</span></span> | <span data-ttu-id="7bfbb-205">Método HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-205">Http method.</span></span> <span data-ttu-id="7bfbb-206">Los valores permitidos son **GET** o **POST**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="7bfbb-207">No.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-207">No.</span></span> <span data-ttu-id="7bfbb-208">El valor predeterminado es `GET`.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-208">Default is `GET`.</span></span> |
| <span data-ttu-id="7bfbb-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="7bfbb-209">additionalHeaders</span></span> | <span data-ttu-id="7bfbb-210">Encabezados de solicitud HTTP adicionales.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="7bfbb-211">No</span><span class="sxs-lookup"><span data-stu-id="7bfbb-211">No</span></span> |
| <span data-ttu-id="7bfbb-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="7bfbb-212">requestBody</span></span> | <span data-ttu-id="7bfbb-213">Cuerpo de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-213">Body for HTTP request.</span></span> | <span data-ttu-id="7bfbb-214">No</span><span class="sxs-lookup"><span data-stu-id="7bfbb-214">No</span></span> |
| <span data-ttu-id="7bfbb-215">formato</span><span class="sxs-lookup"><span data-stu-id="7bfbb-215">format</span></span> | <span data-ttu-id="7bfbb-216">Si desea que toosimply **recuperar datos de Hola de extremo HTTP como-es** sin analizarlo, omita esta configuración de formato.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-216">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="7bfbb-217">Si desea tooparse Hola HTTP respuesta contenido durante la copia, se admite los siguientes tipos de formato de Hola: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-217">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="7bfbb-218">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="7bfbb-219">No</span><span class="sxs-lookup"><span data-stu-id="7bfbb-219">No</span></span> |
| <span data-ttu-id="7bfbb-220">compresión</span><span class="sxs-lookup"><span data-stu-id="7bfbb-220">compression</span></span> | <span data-ttu-id="7bfbb-221">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-221">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="7bfbb-222">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="7bfbb-223">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="7bfbb-224">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="7bfbb-225">No</span><span class="sxs-lookup"><span data-stu-id="7bfbb-225">No</span></span> |

### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="7bfbb-226">Ejemplo: usar el método de hello GET (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="7bfbb-226">Example: using hello GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a><span data-ttu-id="7bfbb-227">Ejemplo: utilizar el método POST de Hola</span><span class="sxs-lookup"><span data-stu-id="7bfbb-227">Example: using hello POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="7bfbb-228">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="7bfbb-228">Copy activity properties</span></span>
<span data-ttu-id="7bfbb-229">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-229">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7bfbb-230">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="7bfbb-231">Propiedades disponibles en hello **typeProperties** sección de actividad de hello en hello varían con cada tipo de actividad en otra parte.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-231">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="7bfbb-232">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-232">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="7bfbb-233">Actualmente, al origen de hello en la actividad de copia es de tipo **HttpSource**, Hola propiedades siguientes se admite.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-233">Currently, when hello source in copy activity is of type **HttpSource**, hello following properties are supported.</span></span>

| <span data-ttu-id="7bfbb-234">Propiedad</span><span class="sxs-lookup"><span data-stu-id="7bfbb-234">Property</span></span> | <span data-ttu-id="7bfbb-235">Descripción</span><span class="sxs-lookup"><span data-stu-id="7bfbb-235">Description</span></span> | <span data-ttu-id="7bfbb-236">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="7bfbb-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="7bfbb-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="7bfbb-237">httpRequestTimeout</span></span> | <span data-ttu-id="7bfbb-238">Hola (TimeSpan) de tiempo de espera de solicitud tooget una respuesta de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-238">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="7bfbb-239">Es tooget Hola de tiempo de espera una respuesta, datos de respuesta no Hola el tooread del tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-239">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="7bfbb-240">No.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-240">No.</span></span> <span data-ttu-id="7bfbb-241">Valor predeterminado: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="7bfbb-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="7bfbb-242">Formatos de archivo y de compresión admitidos</span><span class="sxs-lookup"><span data-stu-id="7bfbb-242">Supported file and compression formats</span></span>
<span data-ttu-id="7bfbb-243">Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="7bfbb-244">Ejemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="7bfbb-244">JSON examples</span></span>
<span data-ttu-id="7bfbb-245">Hola de ejemplo siguiente proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-245">hello following example provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7bfbb-246">Muestra cómo tooAzure almacenamiento de blobs del origen de datos de toocopy de HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-246">They show how toocopy data from HTTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="7bfbb-247">Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-247">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a><span data-ttu-id="7bfbb-248">Ejemplo: Copiar los datos de origen HTTP tooAzure almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="7bfbb-248">Example: Copy data from HTTP source tooAzure Blob Storage</span></span>
<span data-ttu-id="7bfbb-249">solución de factoría de datos de este ejemplo de Hola contiene Hola siguiendo las entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="7bfbb-249">hello Data Factory solution for this sample contains hello following Data Factory entities:</span></span>

1. <span data-ttu-id="7bfbb-250">Un servicio vinculado de tipo [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="7bfbb-251">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="7bfbb-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="7bfbb-252">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="7bfbb-253">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="7bfbb-254">Una [canalización](data-factory-create-pipelines.md) con actividad de copia que usa [HttpSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7bfbb-255">ejemplo de Hola copia datos de un tooan de origen HTTP blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-255">hello sample copies data from an HTTP source tooan Azure blob every hour.</span></span> <span data-ttu-id="7bfbb-256">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-256">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="7bfbb-257">Servicio vinculado HTTP</span><span class="sxs-lookup"><span data-stu-id="7bfbb-257">HTTP linked service</span></span>
<span data-ttu-id="7bfbb-258">Este ejemplo usa Hola HTTP vinculado servicio con la autenticación anónima.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-258">This example uses hello HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="7bfbb-259">Para los diferentes tipos de autenticación que se pueden usar, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="7bfbb-260">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="7bfbb-260">Azure Storage linked service</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="http-input-dataset"></a><span data-ttu-id="7bfbb-261">Conjunto de datos de entrada HTTP</span><span class="sxs-lookup"><span data-stu-id="7bfbb-261">HTTP input dataset</span></span>
<span data-ttu-id="7bfbb-262">Establecer **externo** demasiado**true** informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-262">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="7bfbb-263">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="7bfbb-263">Azure Blob output dataset</span></span>

<span data-ttu-id="7bfbb-264">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-264">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="7bfbb-265">Canalización con actividad de copia</span><span class="sxs-lookup"><span data-stu-id="7bfbb-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="7bfbb-266">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-266">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="7bfbb-267">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**HttpSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-267">In hello pipeline JSON definition, hello **source** type is set too**HttpSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="7bfbb-268">Vea [HttpSource](#copy-activity-properties) para lista de Hola de propiedades admitidas por hello HttpSource.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-268">See [HttpSource](#copy-activity-properties) for hello list of properties supported by hello HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

> [!NOTE]
> <span data-ttu-id="7bfbb-269">columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7bfbb-269">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7bfbb-270">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="7bfbb-270">Performance and Tuning</span></span>
<span data-ttu-id="7bfbb-271">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="7bfbb-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
