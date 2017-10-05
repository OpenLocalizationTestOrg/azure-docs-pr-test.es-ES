---
title: 'Movimiento de datos desde un origen HTTP: Azure | Microsoft Docs'
description: Aprenda a mover datos desde un origen HTTP local o en la nube mediante Azure Data Factory.
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
ms.openlocfilehash: 3cc1bd293868b0bb093f617ac12e16c26780fc89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="f5702-103">Movimiento de datos desde un origen HTTP mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f5702-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="f5702-104">En este artículo se describe el uso de la actividad de copia en Azure Data Factory para mover datos desde un punto de conexión HTTP local o en la nube a un almacén de datos receptor compatible.</span><span class="sxs-lookup"><span data-stu-id="f5702-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud HTTP endpoint to a supported sink data store.</span></span> <span data-ttu-id="f5702-105">Este artículo se basa en el artículo sobre las [actividades de movimiento de datos](data-factory-data-movement-activities.md), que presenta una introducción general del movimiento de datos con la actividad de copia la lista de almacenes de datos compatibles como orígenes/receptores.</span><span class="sxs-lookup"><span data-stu-id="f5702-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="f5702-106">Data Factory solo admite actualmente el movimiento de datos desde un origen HTTP a otros almacenes de datos, pero no de otros almacenes de datos a un destino HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5702-106">Data factory currently supports only moving data from an HTTP source to other data stores, but not moving data from other data stores to an HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="f5702-107">Escenarios admitidos y tipos de autenticación</span><span class="sxs-lookup"><span data-stu-id="f5702-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="f5702-108">Puede usar este conector HTTP para recuperar datos de **un punto de conexión HTTP/s local o en la nube** mediante el método HTTP **GET** o **POST**.</span><span class="sxs-lookup"><span data-stu-id="f5702-108">You can use this HTTP connector to retrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="f5702-109">Se admiten los siguientes tipos de autenticación: **Anonymous**, **Basic**, **Digest**, **Windows** y **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="f5702-109">The following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="f5702-110">Observe la diferencia entre este conector y el [conector de tabla web](data-factory-web-table-connector.md): el último se usa para extraer contenido de la tabla desde una página web HTML.</span><span class="sxs-lookup"><span data-stu-id="f5702-110">Note the difference between this connector and the [Web table connector](data-factory-web-table-connector.md) is: the latter is used to extract table content from web HTML page.</span></span>

<span data-ttu-id="f5702-111">Al copiar datos de un punto de conexión HTTP local, deberá instalar una instancia de Data Management Gateway en la máquina virtual de Azure o en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="f5702-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="f5702-112">Consulte el artículo sobre cómo [mover datos entre ubicaciones locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener información acerca de Data Management Gateway, así como instrucciones paso a paso sobre cómo configurar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f5702-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f5702-113">Introducción</span><span class="sxs-lookup"><span data-stu-id="f5702-113">Getting started</span></span>
<span data-ttu-id="f5702-114">Puede crear una canalización con una actividad de copia que mueva datos desde un origen HTTP mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="f5702-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="f5702-115">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="f5702-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="f5702-116">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="f5702-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="f5702-117">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="f5702-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f5702-118">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso para crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="f5702-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="f5702-119">Para obtener ejemplos de JSON para copiar datos desde un origen HTTP a Azure Blob Storage, consulte la sección [Ejemplos de JSON](#json-examples) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="f5702-119">For JSON samples to copy data from HTTP source to Azure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f5702-120">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="f5702-120">Linked service properties</span></span>
<span data-ttu-id="f5702-121">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5702-121">The following table provides description for JSON elements specific to HTTP linked service.</span></span>

| <span data-ttu-id="f5702-122">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f5702-122">Property</span></span> | <span data-ttu-id="f5702-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="f5702-123">Description</span></span> | <span data-ttu-id="f5702-124">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f5702-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5702-125">type</span><span class="sxs-lookup"><span data-stu-id="f5702-125">type</span></span> | <span data-ttu-id="f5702-126">La propiedad type debe establecerse en: `Http`.</span><span class="sxs-lookup"><span data-stu-id="f5702-126">The type property must be set to: `Http`.</span></span> | <span data-ttu-id="f5702-127">Sí</span><span class="sxs-lookup"><span data-stu-id="f5702-127">Yes</span></span> |
| <span data-ttu-id="f5702-128">url</span><span class="sxs-lookup"><span data-stu-id="f5702-128">url</span></span> | <span data-ttu-id="f5702-129">Dirección URL base para el servidor web</span><span class="sxs-lookup"><span data-stu-id="f5702-129">Base URL to the Web Server</span></span> | <span data-ttu-id="f5702-130">Sí</span><span class="sxs-lookup"><span data-stu-id="f5702-130">Yes</span></span> |
| <span data-ttu-id="f5702-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f5702-131">authenticationType</span></span> | <span data-ttu-id="f5702-132">Especifica el tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="f5702-132">Specifies the authentication type.</span></span> <span data-ttu-id="f5702-133">Los valores permitidos son: **Anonymous**, **Basic**, **Digest**, **Windows** y **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="f5702-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="f5702-134">Consulte en las secciones después de esta tabla más propiedades y ejemplos de JSON para esos tipos de autenticación respectivamente.</span><span class="sxs-lookup"><span data-stu-id="f5702-134">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="f5702-135">Sí</span><span class="sxs-lookup"><span data-stu-id="f5702-135">Yes</span></span> |
| <span data-ttu-id="f5702-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="f5702-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="f5702-137">Especifique si desea habilitar la validación del certificado SSL de servidor si el origen es el servidor web HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f5702-137">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="f5702-138">No, el valor predeterminado es True.</span><span class="sxs-lookup"><span data-stu-id="f5702-138">No, default is true</span></span> |
| <span data-ttu-id="f5702-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f5702-139">gatewayName</span></span> | <span data-ttu-id="f5702-140">Nombre de la instancia de Data Management Gateway para conectarse a un origen HTTP local.</span><span class="sxs-lookup"><span data-stu-id="f5702-140">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="f5702-141">Sí si va a copiar datos desde un origen HTTP local.</span><span class="sxs-lookup"><span data-stu-id="f5702-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="f5702-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="f5702-142">encryptedCredential</span></span> | <span data-ttu-id="f5702-143">Credenciales cifradas para acceder al punto de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5702-143">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="f5702-144">Generadas automáticamente cuando se configura la información de autenticación en el Asistente para copia o en el cuadro de diálogo emergente de ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="f5702-144">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="f5702-145">No.</span><span class="sxs-lookup"><span data-stu-id="f5702-145">No.</span></span> <span data-ttu-id="f5702-146">Se aplica solo cuando se copian datos desde un servidor HTTP local.</span><span class="sxs-lookup"><span data-stu-id="f5702-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="f5702-147">Consulte [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para más detalles sobre cómo establecer las credenciales para un origen de datos de conector HTTP local.</span><span class="sxs-lookup"><span data-stu-id="f5702-147">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="f5702-148">Uso de la autenticación Basic, Digest o Windows</span><span class="sxs-lookup"><span data-stu-id="f5702-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="f5702-149">Establezca `authenticationType` como `Basic`, `Digest` o `Windows`, y especifique las siguientes propiedades además de las genéricas del conector HTTP descritas antes:</span><span class="sxs-lookup"><span data-stu-id="f5702-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="f5702-150">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f5702-150">Property</span></span> | <span data-ttu-id="f5702-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="f5702-151">Description</span></span> | <span data-ttu-id="f5702-152">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f5702-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5702-153">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="f5702-153">username</span></span> | <span data-ttu-id="f5702-154">Nombre de usuario para acceder al punto de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5702-154">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="f5702-155">Sí</span><span class="sxs-lookup"><span data-stu-id="f5702-155">Yes</span></span> |
| <span data-ttu-id="f5702-156">contraseña</span><span class="sxs-lookup"><span data-stu-id="f5702-156">password</span></span> | <span data-ttu-id="f5702-157">Contraseña para el usuario (nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="f5702-157">Password for the user (username).</span></span> | <span data-ttu-id="f5702-158">Sí</span><span class="sxs-lookup"><span data-stu-id="f5702-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="f5702-159">Ejemplo: Uso de la autenticación Basic, Digest o Windows</span><span class="sxs-lookup"><span data-stu-id="f5702-159">Example: using Basic, Digest, or Windows authentication</span></span>

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

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="f5702-160">Uso de la autenticación ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="f5702-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="f5702-161">Para usar la autenticación básica, establezca `authenticationType` como `ClientCertificate`, y especifique las siguientes propiedades además de las genéricas del conector HTTP descritas antes:</span><span class="sxs-lookup"><span data-stu-id="f5702-161">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="f5702-162">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f5702-162">Property</span></span> | <span data-ttu-id="f5702-163">Descripción</span><span class="sxs-lookup"><span data-stu-id="f5702-163">Description</span></span> | <span data-ttu-id="f5702-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f5702-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5702-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="f5702-165">embeddedCertData</span></span> | <span data-ttu-id="f5702-166">El contenido con codificación Base64 de datos binarios del archivo de intercambio de información personal (PFX).</span><span class="sxs-lookup"><span data-stu-id="f5702-166">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="f5702-167">Especifique `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="f5702-167">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="f5702-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="f5702-168">certThumbprint</span></span> | <span data-ttu-id="f5702-169">La huella digital del certificado que se instaló en el almacén de certificados de la máquina de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f5702-169">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="f5702-170">Se aplica solo cuando se copian datos desde un origen HTTP local.</span><span class="sxs-lookup"><span data-stu-id="f5702-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="f5702-171">Especifique `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="f5702-171">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="f5702-172">contraseña</span><span class="sxs-lookup"><span data-stu-id="f5702-172">password</span></span> | <span data-ttu-id="f5702-173">Contraseña asociada con el certificado.</span><span class="sxs-lookup"><span data-stu-id="f5702-173">Password associated with the certificate.</span></span> | <span data-ttu-id="f5702-174">No</span><span class="sxs-lookup"><span data-stu-id="f5702-174">No</span></span> |

<span data-ttu-id="f5702-175">Si utiliza `certThumbprint` para la autenticación y el certificado está instalado en el almacén personal del equipo local, necesita conceder el permiso de lectura al servicio de puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="f5702-175">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="f5702-176">Inicie Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="f5702-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="f5702-177">Agregue el complemento **Certificados** que tenga como destino **Equipo local**.</span><span class="sxs-lookup"><span data-stu-id="f5702-177">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="f5702-178">Expanda **Certificados**, **Personal** y haga clic en **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="f5702-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="f5702-179">Haga clic con el botón derecho en el certificado del almacén personal y seleccione **Todas las tareas**->**Administrar claves privadas**.</span><span class="sxs-lookup"><span data-stu-id="f5702-179">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="f5702-180">En la pestaña **Seguridad**, agregue la cuenta de usuario en que se ejecuta el servicio de host de Data Management Gateway con acceso de lectura al certificado.</span><span class="sxs-lookup"><span data-stu-id="f5702-180">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="f5702-181">Ejemplo: Uso del certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="f5702-181">Example: using client certificate</span></span>
<span data-ttu-id="f5702-182">Este servicio vinculado vincula su factoría de datos a un servidor de web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="f5702-182">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="f5702-183">Utiliza un certificado de cliente que está instalado en la máquina con Data Management Gateway instalado.</span><span class="sxs-lookup"><span data-stu-id="f5702-183">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="f5702-184">Ejemplo: Uso del certificado de cliente en un archivo</span><span class="sxs-lookup"><span data-stu-id="f5702-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="f5702-185">Este servicio vinculado vincula su factoría de datos a un servidor de web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="f5702-185">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="f5702-186">Utiliza un archivo de certificado de cliente en la máquina con Data Management Gateway instalado.</span><span class="sxs-lookup"><span data-stu-id="f5702-186">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="f5702-187">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="f5702-187">Dataset properties</span></span>
<span data-ttu-id="f5702-188">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="f5702-188">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f5702-189">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="f5702-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f5702-190">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="f5702-190">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f5702-191">La sección typeProperties del conjunto de datos de tipo **Http** tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="f5702-191">The typeProperties section for dataset of type **Http** has the following properties</span></span>

| <span data-ttu-id="f5702-192">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f5702-192">Property</span></span> | <span data-ttu-id="f5702-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="f5702-193">Description</span></span> | <span data-ttu-id="f5702-194">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f5702-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f5702-195">type</span><span class="sxs-lookup"><span data-stu-id="f5702-195">type</span></span> | <span data-ttu-id="f5702-196">Especifica el tipo del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="f5702-196">Specified the type of the dataset.</span></span> <span data-ttu-id="f5702-197">Se debe establecer en `Http`.</span><span class="sxs-lookup"><span data-stu-id="f5702-197">must be set to `Http`.</span></span> | <span data-ttu-id="f5702-198">Sí</span><span class="sxs-lookup"><span data-stu-id="f5702-198">Yes</span></span> |
| <span data-ttu-id="f5702-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="f5702-199">relativeUrl</span></span> | <span data-ttu-id="f5702-200">Dirección URL relativa al recurso que contiene los datos.</span><span class="sxs-lookup"><span data-stu-id="f5702-200">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="f5702-201">Cuando no se especifica la ruta de acceso, se solo se usa la dirección URL especificada en la definición de servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="f5702-201">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="f5702-202">Para construir una dirección URL dinámica, puede usar [funciones y variables de sistema de Data Factory](data-factory-functions-variables.md), como "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span><span class="sxs-lookup"><span data-stu-id="f5702-202">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="f5702-203">No</span><span class="sxs-lookup"><span data-stu-id="f5702-203">No</span></span> |
| <span data-ttu-id="f5702-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="f5702-204">requestMethod</span></span> | <span data-ttu-id="f5702-205">Método HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5702-205">Http method.</span></span> <span data-ttu-id="f5702-206">Los valores permitidos son **GET** o **POST**.</span><span class="sxs-lookup"><span data-stu-id="f5702-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="f5702-207">No.</span><span class="sxs-lookup"><span data-stu-id="f5702-207">No.</span></span> <span data-ttu-id="f5702-208">El valor predeterminado es `GET`.</span><span class="sxs-lookup"><span data-stu-id="f5702-208">Default is `GET`.</span></span> |
| <span data-ttu-id="f5702-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="f5702-209">additionalHeaders</span></span> | <span data-ttu-id="f5702-210">Encabezados de solicitud HTTP adicionales.</span><span class="sxs-lookup"><span data-stu-id="f5702-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="f5702-211">No</span><span class="sxs-lookup"><span data-stu-id="f5702-211">No</span></span> |
| <span data-ttu-id="f5702-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="f5702-212">requestBody</span></span> | <span data-ttu-id="f5702-213">Cuerpo de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5702-213">Body for HTTP request.</span></span> | <span data-ttu-id="f5702-214">No</span><span class="sxs-lookup"><span data-stu-id="f5702-214">No</span></span> |
| <span data-ttu-id="f5702-215">formato</span><span class="sxs-lookup"><span data-stu-id="f5702-215">format</span></span> | <span data-ttu-id="f5702-216">Si desea simplemente **recuperar los datos del punto de conexión HTTP tal cual** sin analizarlos, omita esta configuración de formato.</span><span class="sxs-lookup"><span data-stu-id="f5702-216">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="f5702-217">Si desea analizar el contenido de la respuesta HTTP durante la copia, se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="f5702-217">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="f5702-218">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="f5702-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="f5702-219">No</span><span class="sxs-lookup"><span data-stu-id="f5702-219">No</span></span> |
| <span data-ttu-id="f5702-220">compresión</span><span class="sxs-lookup"><span data-stu-id="f5702-220">compression</span></span> | <span data-ttu-id="f5702-221">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="f5702-221">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="f5702-222">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="f5702-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="f5702-223">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="f5702-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="f5702-224">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="f5702-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="f5702-225">No</span><span class="sxs-lookup"><span data-stu-id="f5702-225">No</span></span> |

### <a name="example-using-the-get-default-method"></a><span data-ttu-id="f5702-226">Ejemplo: Uso del método GET (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="f5702-226">Example: using the GET (default) method</span></span>

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

### <a name="example-using-the-post-method"></a><span data-ttu-id="f5702-227">Ejemplo: Uso del método POST</span><span class="sxs-lookup"><span data-stu-id="f5702-227">Example: using the POST method</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="f5702-228">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="f5702-228">Copy activity properties</span></span>
<span data-ttu-id="f5702-229">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f5702-229">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f5702-230">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="f5702-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="f5702-231">Por otra parte, las propiedades disponibles en la sección **typeProperties** de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="f5702-231">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="f5702-232">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="f5702-232">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="f5702-233">En este momento, cuando el origen de la actividad de copia es de tipo **HttpSource**, se admiten las siguientes propiedades.</span><span class="sxs-lookup"><span data-stu-id="f5702-233">Currently, when the source in copy activity is of type **HttpSource**, the following properties are supported.</span></span>

| <span data-ttu-id="f5702-234">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f5702-234">Property</span></span> | <span data-ttu-id="f5702-235">Descripción</span><span class="sxs-lookup"><span data-stu-id="f5702-235">Description</span></span> | <span data-ttu-id="f5702-236">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f5702-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="f5702-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="f5702-237">httpRequestTimeout</span></span> | <span data-ttu-id="f5702-238">El tiempo que la solicitud HTTP espera (TimeSpan) a obtener una respuesta.</span><span class="sxs-lookup"><span data-stu-id="f5702-238">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="f5702-239">Es el tiempo de espera para obtener una respuesta, no para leer los datos de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="f5702-239">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="f5702-240">No.</span><span class="sxs-lookup"><span data-stu-id="f5702-240">No.</span></span> <span data-ttu-id="f5702-241">Valor predeterminado: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="f5702-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="f5702-242">Formatos de archivo y de compresión admitidos</span><span class="sxs-lookup"><span data-stu-id="f5702-242">Supported file and compression formats</span></span>
<span data-ttu-id="f5702-243">Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="f5702-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="f5702-244">Ejemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="f5702-244">JSON examples</span></span>
<span data-ttu-id="f5702-245">En el siguiente ejemplo, se proporcionan definiciones JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f5702-245">The following example provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f5702-246">Se muestra cómo copiar datos del origen HTTP a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f5702-246">They show how to copy data from HTTP source to Azure Blob Storage.</span></span> <span data-ttu-id="f5702-247">Sin embargo, los datos se pueden copiar **directamente** de cualquiera de los orígenes a cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5702-247">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-to-azure-blob-storage"></a><span data-ttu-id="f5702-248">Ejemplo: Copia de datos desde el origen HTTP a Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="f5702-248">Example: Copy data from HTTP source to Azure Blob Storage</span></span>
<span data-ttu-id="f5702-249">La solución Data Factory de este ejemplo contiene las siguientes entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="f5702-249">The Data Factory solution for this sample contains the following Data Factory entities:</span></span>

1. <span data-ttu-id="f5702-250">Un servicio vinculado de tipo [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f5702-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="f5702-251">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="f5702-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f5702-252">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f5702-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="f5702-253">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f5702-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f5702-254">Una [canalización](data-factory-create-pipelines.md) con actividad de copia que usa [HttpSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f5702-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f5702-255">En el ejemplo se copian datos de un origen HTTP a un blob de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="f5702-255">The sample copies data from an HTTP source to an Azure blob every hour.</span></span> <span data-ttu-id="f5702-256">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="f5702-256">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="f5702-257">Servicio vinculado HTTP</span><span class="sxs-lookup"><span data-stu-id="f5702-257">HTTP linked service</span></span>
<span data-ttu-id="f5702-258">En este ejemplo se usa el servicio vinculado HTTP con autenticación anónima.</span><span class="sxs-lookup"><span data-stu-id="f5702-258">This example uses the HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="f5702-259">Para los diferentes tipos de autenticación que se pueden usar, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f5702-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="f5702-260">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="f5702-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="f5702-261">Conjunto de datos de entrada HTTP</span><span class="sxs-lookup"><span data-stu-id="f5702-261">HTTP input dataset</span></span>
<span data-ttu-id="f5702-262">Si se establece **external** en **true**, se informa al servicio Data Factory que el conjunto de datos es externo a Data Factory y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="f5702-262">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="f5702-263">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="f5702-263">Azure Blob output dataset</span></span>

<span data-ttu-id="f5702-264">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="f5702-264">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="f5702-265">Canalización con actividad de copia</span><span class="sxs-lookup"><span data-stu-id="f5702-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="f5702-266">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="f5702-266">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f5702-267">En la definición de la canalización JSON, el tipo **source** se establece en **HttpSource** y el tipo **sink**, en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f5702-267">In the pipeline JSON definition, the **source** type is set to **HttpSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="f5702-268">Consulte [HttpSource](#copy-activity-properties) para obtener la lista de propiedades admitidas por HttpSource.</span><span class="sxs-lookup"><span data-stu-id="f5702-268">See [HttpSource](#copy-activity-properties) for the list of properties supported by the HttpSource.</span></span>

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
        "description": "Copy from an HTTP source to an Azure blob",
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
> <span data-ttu-id="f5702-269">Para asignar columnas del conjunto de datos de origen a las del conjunto de datos del receptor, consulte el artículo sobre la [asignación de columnas del conjunto de datos en Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f5702-269">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f5702-270">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="f5702-270">Performance and Tuning</span></span>
<span data-ttu-id="f5702-271">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="f5702-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
