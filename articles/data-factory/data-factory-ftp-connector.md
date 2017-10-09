---
title: aaaMove datos desde un servidor FTP mediante el uso de Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos desde un servidor FTP mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="84653-103">Movimiento de datos de un servidor FTP mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="84653-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="84653-104">Este artículo explica cómo toouse Hola actividad de copia de datos de Data Factory de Azure toomove desde un servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="84653-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="84653-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="84653-106">Puede copiar datos desde un almacén de datos de receptor FTP server tooany compatible.</span><span class="sxs-lookup"><span data-stu-id="84653-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="84653-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="84653-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="84653-108">Solo almacena la migración de datos de un datos tooother de servidor FTP, pero no mover los datos de otros datos almacena tooan FTP server admite actualmente factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="84653-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="84653-109">Admite servidores FTP tanto locales como en la nube.</span><span class="sxs-lookup"><span data-stu-id="84653-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="84653-110">actividad de copia de Hello no eliminar el archivo de origen de hello cuando este destino toohello copió correctamente.</span><span class="sxs-lookup"><span data-stu-id="84653-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="84653-111">Si necesita toodelete archivo de código fuente de Hola después de una copia correcta, cree un archivo de hello toodelete de actividad personalizada y usa la actividad hello en canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="84653-112">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="84653-112">Enable connectivity</span></span>
<span data-ttu-id="84653-113">Si va a mover datos desde un **locales** el almacén de datos en la nube de servidor tooa FTP (por ejemplo, tooAzure almacenamiento de blobs), instalar y usar Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="84653-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="84653-114">Hola Data Management Gateway es un agente de cliente que está instalado en el equipo local, y permite recurso local tooan tooconnect de servicios de nube.</span><span class="sxs-lookup"><span data-stu-id="84653-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="84653-115">Para más información, vea [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="84653-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="84653-116">Para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola y utilizarlo, vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="84653-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="84653-117">Usar servidor de hello puerta de enlace tooconnect tooan FTP, aunque Hola servidor en una infraestructura de Azure como una máquina virtual (VM) de servicio (IaaS).</span><span class="sxs-lookup"><span data-stu-id="84653-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="84653-118">Es puerta de enlace de posibles tooinstall Hola Hola igual en local machine o IaaS VM como Hola servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="84653-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="84653-119">Sin embargo, se recomienda instalar la puerta de enlace de hello en un equipo independiente o contención de recursos de IaaS VM tooavoid y para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="84653-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="84653-120">Cuando se instala la puerta de enlace de hello en un equipo independiente, máquina Hola debe ser servidor FTP puede tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="84653-121">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="84653-121">Get started</span></span>
<span data-ttu-id="84653-122">Puede crear una canalización con una actividad de copia que mueva datos desde un origen FTP mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="84653-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="84653-123">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar de factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="84653-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="84653-124">Para ver un tutorial rápido, consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="84653-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="84653-125">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="84653-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="84653-126">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="84653-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="84653-127">Si usa herramientas de Hola o las API, lleve a cabo Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="84653-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="84653-128">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="84653-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="84653-129">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="84653-130">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="84653-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="84653-131">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="84653-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="84653-132">Al usar herramientas o las API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="84653-133">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos FTP, vea hello [ejemplo de JSON: copiar los datos de blob FTP server tooAzure](#json-example-copy-data-from-ftp-server-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="84653-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="84653-134">Para obtener más información sobre toouse de formatos de compresión de archivos y compatible, consulte [compresión de archivos y formatos de factoría de datos de Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="84653-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="84653-135">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son entidades de factoría de datos usado toodefine tooFTP específico.</span><span class="sxs-lookup"><span data-stu-id="84653-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="84653-136">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="84653-136">Linked service properties</span></span>
<span data-ttu-id="84653-137">Hello en la tabla siguiente describe el servicio FTP vinculada de tooan específico de elementos JSON.</span><span class="sxs-lookup"><span data-stu-id="84653-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="84653-138">Propiedad</span><span class="sxs-lookup"><span data-stu-id="84653-138">Property</span></span> | <span data-ttu-id="84653-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="84653-139">Description</span></span> | <span data-ttu-id="84653-140">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="84653-140">Required</span></span> | <span data-ttu-id="84653-141">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="84653-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="84653-142">type</span><span class="sxs-lookup"><span data-stu-id="84653-142">type</span></span> |<span data-ttu-id="84653-143">Establecer este tooFtpServer.</span><span class="sxs-lookup"><span data-stu-id="84653-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="84653-144">Sí</span><span class="sxs-lookup"><span data-stu-id="84653-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="84653-145">host</span><span class="sxs-lookup"><span data-stu-id="84653-145">host</span></span> |<span data-ttu-id="84653-146">Especificar nombre de Hola o dirección IP del servidor FTP de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="84653-147">Sí</span><span class="sxs-lookup"><span data-stu-id="84653-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="84653-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="84653-148">authenticationType</span></span> |<span data-ttu-id="84653-149">Especifique el tipo de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-149">Specify hello authentication type.</span></span> |<span data-ttu-id="84653-150">Sí</span><span class="sxs-lookup"><span data-stu-id="84653-150">Yes</span></span> |<span data-ttu-id="84653-151">Basic, Anonymous</span><span class="sxs-lookup"><span data-stu-id="84653-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="84653-152">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="84653-152">username</span></span> |<span data-ttu-id="84653-153">Especifique el usuario de Hola que tiene el servidor de acceso toohello FTP.</span><span class="sxs-lookup"><span data-stu-id="84653-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="84653-154">No</span><span class="sxs-lookup"><span data-stu-id="84653-154">No</span></span> |&nbsp; |
| <span data-ttu-id="84653-155">Contraseña</span><span class="sxs-lookup"><span data-stu-id="84653-155">password</span></span> |<span data-ttu-id="84653-156">Especifique la contraseña de hello para el usuario hello (usuario).</span><span class="sxs-lookup"><span data-stu-id="84653-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="84653-157">No</span><span class="sxs-lookup"><span data-stu-id="84653-157">No</span></span> |&nbsp; |
| <span data-ttu-id="84653-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="84653-158">encryptedCredential</span></span> |<span data-ttu-id="84653-159">Especificar servidor de hello cifrado credencial tooaccess Hola FTP.</span><span class="sxs-lookup"><span data-stu-id="84653-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="84653-160">No</span><span class="sxs-lookup"><span data-stu-id="84653-160">No</span></span> |&nbsp; |
| <span data-ttu-id="84653-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="84653-161">gatewayName</span></span> |<span data-ttu-id="84653-162">Especifique el nombre de Hola de puerta de enlace de hello en el servidor FTP local de Data Management Gateway tooconnect tooan.</span><span class="sxs-lookup"><span data-stu-id="84653-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="84653-163">No</span><span class="sxs-lookup"><span data-stu-id="84653-163">No</span></span> |&nbsp; |
| <span data-ttu-id="84653-164">puerto</span><span class="sxs-lookup"><span data-stu-id="84653-164">port</span></span> |<span data-ttu-id="84653-165">Especificar puerto hello en qué Hola FTP está escuchando el servidor.</span><span class="sxs-lookup"><span data-stu-id="84653-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="84653-166">No</span><span class="sxs-lookup"><span data-stu-id="84653-166">No</span></span> |<span data-ttu-id="84653-167">21</span><span class="sxs-lookup"><span data-stu-id="84653-167">21</span></span> |
| <span data-ttu-id="84653-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="84653-168">enableSsl</span></span> |<span data-ttu-id="84653-169">Especifique si toouse FTP sobre un canal SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="84653-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="84653-170">No</span><span class="sxs-lookup"><span data-stu-id="84653-170">No</span></span> |<span data-ttu-id="84653-171">true</span><span class="sxs-lookup"><span data-stu-id="84653-171">true</span></span> |
| <span data-ttu-id="84653-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="84653-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="84653-173">Especifique si, cuando se utiliza FTP a través de canal SSL/TLS, se validación de certificado de servidor tooenable SSL.</span><span class="sxs-lookup"><span data-stu-id="84653-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="84653-174">No</span><span class="sxs-lookup"><span data-stu-id="84653-174">No</span></span> |<span data-ttu-id="84653-175">true</span><span class="sxs-lookup"><span data-stu-id="84653-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="84653-176">Uso de la autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="84653-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="84653-177">Uso del nombre de usuario y la contraseña en texto sin formato para la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="84653-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="84653-178">Uso de puerto, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="84653-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="84653-179">Uso de encryptedCredential para la autenticación y la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="84653-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="84653-180">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="84653-180">Dataset properties</span></span>
<span data-ttu-id="84653-181">Para ver una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, consulte [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="84653-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="84653-182">Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="84653-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="84653-183">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="84653-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="84653-184">Proporciona información de tipo de conjunto de datos toohello específica.</span><span class="sxs-lookup"><span data-stu-id="84653-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="84653-185">Hola **typeProperties** sección para un conjunto de datos de tipo **FileShare** tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="84653-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="84653-186">Propiedad</span><span class="sxs-lookup"><span data-stu-id="84653-186">Property</span></span> | <span data-ttu-id="84653-187">Descripción</span><span class="sxs-lookup"><span data-stu-id="84653-187">Description</span></span> | <span data-ttu-id="84653-188">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="84653-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84653-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="84653-189">folderPath</span></span> |<span data-ttu-id="84653-190">Carpeta de toohello subruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="84653-190">Subpath toohello folder.</span></span> <span data-ttu-id="84653-191">Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="84653-192">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="84653-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="84653-193">Puede combinar esta propiedad con **partitionBy** según las rutas de carpeta toohave empezar y terminar fechas y horas.</span><span class="sxs-lookup"><span data-stu-id="84653-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="84653-194">Sí</span><span class="sxs-lookup"><span data-stu-id="84653-194">Yes</span></span> |
| <span data-ttu-id="84653-195">fileName</span><span class="sxs-lookup"><span data-stu-id="84653-195">fileName</span></span> |<span data-ttu-id="84653-196">Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="84653-197">Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="84653-198">Cuando **fileName** no se especifica para un conjunto de datos de salida, nombre de hello del archivo hello generado está en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="84653-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="84653-199">Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="84653-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="84653-200">No</span><span class="sxs-lookup"><span data-stu-id="84653-200">No</span></span> |
| <span data-ttu-id="84653-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="84653-201">fileFilter</span></span> |<span data-ttu-id="84653-202">Especificar un tooselect de toobe utiliza un subconjunto de archivos de filtro en hello **folderPath**, en lugar de todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="84653-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="84653-203">Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).</span><span class="sxs-lookup"><span data-stu-id="84653-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="84653-204">Ejemplo 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="84653-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="84653-205">Ejemplo 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="84653-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="84653-206">**fileFilter** es aplicable a un conjunto de datos FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="84653-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="84653-207">Esta propiedad no es compatible con el sistema de archivos distribuido de Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="84653-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="84653-208">No</span><span class="sxs-lookup"><span data-stu-id="84653-208">No</span></span> |
| <span data-ttu-id="84653-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="84653-209">partitionedBy</span></span> |<span data-ttu-id="84653-210">Usar toospecify dinámico **folderPath** y **fileName** para datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="84653-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="84653-211">Por ejemplo, puede especificar una propiedad **folderPath** que tenga parámetros para cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="84653-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="84653-212">No</span><span class="sxs-lookup"><span data-stu-id="84653-212">No</span></span> |
| <span data-ttu-id="84653-213">formato</span><span class="sxs-lookup"><span data-stu-id="84653-213">format</span></span> | <span data-ttu-id="84653-214">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="84653-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="84653-215">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="84653-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="84653-216">Para obtener más información, vea hello [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [el formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), y [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) secciones.</span><span class="sxs-lookup"><span data-stu-id="84653-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="84653-217">Si desea toocopy archivos tal como están entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="84653-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="84653-218">No</span><span class="sxs-lookup"><span data-stu-id="84653-218">No</span></span> |
| <span data-ttu-id="84653-219">compresión</span><span class="sxs-lookup"><span data-stu-id="84653-219">compression</span></span> | <span data-ttu-id="84653-220">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="84653-221">Los tipos admitidos son: **GZip**, **Deflate**, **BZip2** y **ZipDeflate**, y los niveles que se admiten son: **Optimal** (Óptimo) y **Fastest** (Más rápido).</span><span class="sxs-lookup"><span data-stu-id="84653-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="84653-222">Para obtener más información, consulte el artículo sobre [formatos de archivo y compresión en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="84653-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="84653-223">No</span><span class="sxs-lookup"><span data-stu-id="84653-223">No</span></span> |
| <span data-ttu-id="84653-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="84653-224">useBinaryTransfer</span></span> |<span data-ttu-id="84653-225">Especifique si el modo de transferencia de archivo binario de hello toouse.</span><span class="sxs-lookup"><span data-stu-id="84653-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="84653-226">Hola valores son true para el modo binario (Esto es el valor predeterminado de hello) y false para ASCII.</span><span class="sxs-lookup"><span data-stu-id="84653-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="84653-227">Esta propiedad solo puede usarse cuando hello asociado servicio vinculado de tipo es de tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="84653-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="84653-228">No</span><span class="sxs-lookup"><span data-stu-id="84653-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="84653-229">**fileName** y **fileFilter** no pueden usarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="84653-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="84653-230">Utilice hello partionedBy propiedad</span><span class="sxs-lookup"><span data-stu-id="84653-230">Use hello partionedBy property</span></span>
<span data-ttu-id="84653-231">Como se mencionó en la sección anterior de hello, puede especificar un dinámico **folderPath** y **fileName** para datos de serie temporal con hello **partitionedBy** propiedad.</span><span class="sxs-lookup"><span data-stu-id="84653-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="84653-232">toolearn acerca de los conjuntos de datos de series de tiempo, la programación y sectores, consulte [crear conjuntos de datos](data-factory-create-datasets.md), [ejecución y programación](data-factory-scheduling-and-execution.md), y [crear canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="84653-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="84653-233">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="84653-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="84653-234">En este ejemplo, {Slice} se reemplaza con el valor de Hola de variable del sistema SliceStart de factoría de datos, en hello formato (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="84653-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="84653-235">Hola SliceStart refiere a tiempo toostart de segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="84653-236">ruta de acceso de carpeta de Hello es diferente para cada segmento.</span><span class="sxs-lookup"><span data-stu-id="84653-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="84653-237">(Por ejemplo, wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104).</span><span class="sxs-lookup"><span data-stu-id="84653-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="84653-238">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="84653-238">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="84653-239">En este ejemplo, se extraen en variables independientes que usan Hola Hola año, mes, día y hora de SliceStart **folderPath** y **fileName** propiedades.</span><span class="sxs-lookup"><span data-stu-id="84653-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="84653-240">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="84653-240">Copy activity properties</span></span>
<span data-ttu-id="84653-241">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="84653-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="84653-242">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="84653-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="84653-243">Propiedades disponibles en hello **typeProperties** sección de Hola actividad en hello en otra parte, varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="84653-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="84653-244">Para la actividad de copia de hello, propiedades de tipo de hello varían en función de tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="84653-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="84653-245">En la actividad de copia, cuando el origen de hello es de tipo **FileSystemSource**, Hola después de la propiedad está disponible en **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="84653-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="84653-246">Propiedad</span><span class="sxs-lookup"><span data-stu-id="84653-246">Property</span></span> | <span data-ttu-id="84653-247">Descripción</span><span class="sxs-lookup"><span data-stu-id="84653-247">Description</span></span> | <span data-ttu-id="84653-248">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="84653-248">Allowed values</span></span> | <span data-ttu-id="84653-249">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="84653-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="84653-250">recursive</span><span class="sxs-lookup"><span data-stu-id="84653-250">recursive</span></span> |<span data-ttu-id="84653-251">Indica si los datos de hello es de lectura de forma recursiva de las subcarpetas de hello, o solo de la carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="84653-252">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="84653-252">True, False (default)</span></span> |<span data-ttu-id="84653-253">No</span><span class="sxs-lookup"><span data-stu-id="84653-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="84653-254">Ejemplo de JSON: copiar los datos de servidor FTP tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="84653-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="84653-255">Este ejemplo se muestra cómo toocopy datos desde un tooAzure de servidor FTP almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="84653-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="84653-256">Sin embargo, los datos pueden copiarse directamente Hola indicado en los receptores de tooany de hello [admite almacenes de datos y formatos](data-factory-data-movement-activities.md#supported-data-stores-and-formats), mediante el uso de actividad de copia de hello de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="84653-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="84653-257">Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="84653-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="84653-258">Un servicio vinculado de tipo [FtpServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="84653-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="84653-259">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="84653-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="84653-260">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="84653-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="84653-261">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="84653-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="84653-262">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="84653-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="84653-263">ejemplo de Hola copia datos de un tooan de servidor FTP blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="84653-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="84653-264">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="84653-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="84653-265">Servicio vinculado FTP</span><span class="sxs-lookup"><span data-stu-id="84653-265">FTP linked service</span></span>

<span data-ttu-id="84653-266">En este ejemplo se utiliza la autenticación básica, con el nombre de usuario de hello y una contraseña en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="84653-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="84653-267">También puede utilizar uno de hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="84653-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="84653-268">Autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="84653-268">Anonymous authentication</span></span>
* <span data-ttu-id="84653-269">Autenticación básica con credenciales cifradas</span><span class="sxs-lookup"><span data-stu-id="84653-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="84653-270">FTP sobre SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="84653-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="84653-271">Vea hello [servicio vinculado de FTP](#linked-service-properties) sección para diferentes tipos de autenticación que se puede usar.</span><span class="sxs-lookup"><span data-stu-id="84653-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="84653-272">Servicio vinculado de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="84653-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="84653-273">Conjunto de datos de entrada FTP</span><span class="sxs-lookup"><span data-stu-id="84653-273">FTP input dataset</span></span>

<span data-ttu-id="84653-274">Este conjunto de datos hace referencia la carpeta FTP toohello `mysharedfolder` y el archivo `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="84653-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="84653-275">Hola canalización copias hello toohello destino del archivo.</span><span class="sxs-lookup"><span data-stu-id="84653-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="84653-276">Establecer **externo** demasiado**true** informa a servicio de factoría de datos de Hola ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="84653-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="84653-277">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="84653-277">Azure Blob output dataset</span></span>

<span data-ttu-id="84653-278">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="84653-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="84653-279">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="84653-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="84653-280">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de Hola Hola hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="84653-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="84653-281">Actividad de copia en una canalización con el origen del sistema de archivos y el receptor de blob</span><span class="sxs-lookup"><span data-stu-id="84653-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="84653-282">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida, y es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="84653-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="84653-283">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**FileSystemSource**, hello y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="84653-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="84653-284">columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="84653-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="84653-285">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="84653-285">Next steps</span></span>
<span data-ttu-id="84653-286">Vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="84653-286">See hello following articles:</span></span>

* <span data-ttu-id="84653-287">toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos y toooptimize de diversas formas, vea hello [copiar actividad Guía de rendimiento y optimización](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="84653-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="84653-288">Para obtener instrucciones paso a paso para crear una canalización con una actividad de copia, consulte hello [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="84653-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
