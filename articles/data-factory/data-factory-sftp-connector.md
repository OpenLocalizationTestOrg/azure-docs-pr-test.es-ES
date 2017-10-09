---
title: aaaMove datos del servidor SFTP con Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos desde una implementación local o un servidor SFTP de nubes mediante Data Factory de Azure."
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
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="f52fa-103">Movimiento de datos de un servidor FTP mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f52fa-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="f52fa-104">En este artículo se describe cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un tooa de servidor SFTP en local y la nube admite el almacén de datos del receptor.</span><span class="sxs-lookup"><span data-stu-id="f52fa-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud SFTP server tooa supported sink data store.</span></span> <span data-ttu-id="f52fa-105">En este artículo se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo que presenta una visión general de movimiento de datos con la lista de hello y actividad de copia de almacenes de datos que se admiten como orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="f52fa-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="f52fa-106">Factoría de datos admite actualmente solo mover almacena los datos de un servidor de SFTP tooother datos, pero no para mover los datos de otros datos de los almacenes servidor SFTP de tooan.</span><span class="sxs-lookup"><span data-stu-id="f52fa-106">Data factory currently supports only moving data from an SFTP server tooother data stores, but not for moving data from other data stores tooan SFTP server.</span></span> <span data-ttu-id="f52fa-107">Admite servidores SFTP tanto locales como de nube.</span><span class="sxs-lookup"><span data-stu-id="f52fa-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="f52fa-108">Actividad de copia no elimina archivos de origen de Hola cuando este destino toohello copió correctamente.</span><span class="sxs-lookup"><span data-stu-id="f52fa-108">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="f52fa-109">Si necesita toodelete archivo de código fuente de hello después de una copia correcta, cree un archivo de actividad personalizada toodelete hello y usar actividad hello en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-109">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="f52fa-110">Escenarios admitidos y tipos de autenticación</span><span class="sxs-lookup"><span data-stu-id="f52fa-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="f52fa-111">Puede usar estos datos SFTP conector toocopy de **ambos servidores SFTP y servidores SFTP local en la nube**.</span><span class="sxs-lookup"><span data-stu-id="f52fa-111">You can use this SFTP connector toocopy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="f52fa-112">**Básico** y **SshPublicKey** se admiten los tipos de autenticación cuando se conecta el servidor de toohello SFTP.</span><span class="sxs-lookup"><span data-stu-id="f52fa-112">**Basic** and **SshPublicKey** authentication types are supported when connecting toohello SFTP server.</span></span>

<span data-ttu-id="f52fa-113">Cuando se copian datos desde un servidor local de SFTP, necesita instalar una puerta de enlace de administración de datos en hello local entorno/VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="f52fa-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="f52fa-114">Vea [Data Management Gateway](data-factory-data-management-gateway.md) para obtener detalles sobre la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on hello gateway.</span></span> <span data-ttu-id="f52fa-115">Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola y usarlo.</span><span class="sxs-lookup"><span data-stu-id="f52fa-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f52fa-116">Introducción</span><span class="sxs-lookup"><span data-stu-id="f52fa-116">Getting started</span></span>
<span data-ttu-id="f52fa-117">Puede crear una canalización con una actividad de copia que mueva los datos desde un origen SFTP mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="f52fa-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="f52fa-118">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="f52fa-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="f52fa-119">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="f52fa-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="f52fa-120">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="f52fa-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f52fa-121">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="f52fa-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="f52fa-122">Para JSON muestrea los datos de toocopy de tooAzure de servidor SFTP almacenamiento de blobs, vea [ejemplo de JSON: copiar los datos de blob SFTP server tooAzure](#json-example-copy-data-from-sftp-server-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="f52fa-122">For JSON samples toocopy data from SFTP server tooAzure Blob Storage, see [JSON Example: Copy data from SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f52fa-123">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="f52fa-123">Linked service properties</span></span>
<span data-ttu-id="f52fa-124">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooFTP vinculado.</span><span class="sxs-lookup"><span data-stu-id="f52fa-124">hello following table provides description for JSON elements specific tooFTP linked service.</span></span>

| <span data-ttu-id="f52fa-125">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f52fa-125">Property</span></span> | <span data-ttu-id="f52fa-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="f52fa-126">Description</span></span> | <span data-ttu-id="f52fa-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f52fa-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f52fa-128">type</span><span class="sxs-lookup"><span data-stu-id="f52fa-128">type</span></span> | <span data-ttu-id="f52fa-129">se debe establecer propiedad de tipo Hello demasiado`Sftp`.</span><span class="sxs-lookup"><span data-stu-id="f52fa-129">hello type property must be set too`Sftp`.</span></span> |<span data-ttu-id="f52fa-130">Sí</span><span class="sxs-lookup"><span data-stu-id="f52fa-130">Yes</span></span> |
| <span data-ttu-id="f52fa-131">host</span><span class="sxs-lookup"><span data-stu-id="f52fa-131">host</span></span> | <span data-ttu-id="f52fa-132">Nombre o dirección IP del servidor SFTP de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-132">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="f52fa-133">Sí</span><span class="sxs-lookup"><span data-stu-id="f52fa-133">Yes</span></span> |
| <span data-ttu-id="f52fa-134">puerto</span><span class="sxs-lookup"><span data-stu-id="f52fa-134">port</span></span> |<span data-ttu-id="f52fa-135">Puerto en qué Hola SFTP servidor está escuchando.</span><span class="sxs-lookup"><span data-stu-id="f52fa-135">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="f52fa-136">es el valor predeterminado de Hello: 21</span><span class="sxs-lookup"><span data-stu-id="f52fa-136">hello default value is: 21</span></span> |<span data-ttu-id="f52fa-137">No</span><span class="sxs-lookup"><span data-stu-id="f52fa-137">No</span></span> |
| <span data-ttu-id="f52fa-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f52fa-138">authenticationType</span></span> |<span data-ttu-id="f52fa-139">Especifique el tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="f52fa-139">Specify authentication type.</span></span> <span data-ttu-id="f52fa-140">Valores permitidos: **Básica**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="f52fa-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="f52fa-141">Consulte demasiado[mediante la autenticación básica](#using-basic-authentication) y [utilizando SSH autenticación de clave pública](#using-ssh-public-key-authentication) secciones en más propiedades y ejemplos JSON, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="f52fa-141">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="f52fa-142">Sí</span><span class="sxs-lookup"><span data-stu-id="f52fa-142">Yes</span></span> |
| <span data-ttu-id="f52fa-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="f52fa-143">skipHostKeyValidation</span></span> | <span data-ttu-id="f52fa-144">Especificar si tooskip validación de clave de host.</span><span class="sxs-lookup"><span data-stu-id="f52fa-144">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="f52fa-145">No.</span><span class="sxs-lookup"><span data-stu-id="f52fa-145">No.</span></span> <span data-ttu-id="f52fa-146">Hola valor predeterminado: false</span><span class="sxs-lookup"><span data-stu-id="f52fa-146">hello default value: false</span></span> |
| <span data-ttu-id="f52fa-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="f52fa-147">hostKeyFingerprint</span></span> | <span data-ttu-id="f52fa-148">Especifique la huella dactilar de Hola de clave de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-148">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="f52fa-149">Sí si hello `skipHostKeyValidation` se establece toofalse.</span><span class="sxs-lookup"><span data-stu-id="f52fa-149">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="f52fa-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f52fa-150">gatewayName</span></span> |<span data-ttu-id="f52fa-151">Nombre de hello Data Management Gateway tooconnect tooan local servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="f52fa-151">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="f52fa-152">Sí, si va a copiar datos desde un servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="f52fa-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="f52fa-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="f52fa-153">encryptedCredential</span></span> | <span data-ttu-id="f52fa-154">Servidor de credenciales cifradas tooaccess Hola SFTP.</span><span class="sxs-lookup"><span data-stu-id="f52fa-154">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="f52fa-155">Generado automáticamente cuando se especifica la autenticación básica (nombre de usuario y contraseña) o SshPublicKey (nombre de usuario + ruta de acceso de clave privada o contenido) en copia asistente o hello ClickOnce cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="f52fa-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="f52fa-156">No.</span><span class="sxs-lookup"><span data-stu-id="f52fa-156">No.</span></span> <span data-ttu-id="f52fa-157">Se aplica solo cuando se copian datos desde un servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="f52fa-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="f52fa-158">Uso de autenticación básica</span><span class="sxs-lookup"><span data-stu-id="f52fa-158">Using basic authentication</span></span>

<span data-ttu-id="f52fa-159">establecer la autenticación básica toouse, `authenticationType` como `Basic`y especifique Hola propiedades siguientes, además de Hola conector SFTP genérico que introdujo en la última sección de hello:</span><span class="sxs-lookup"><span data-stu-id="f52fa-159">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="f52fa-160">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f52fa-160">Property</span></span> | <span data-ttu-id="f52fa-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="f52fa-161">Description</span></span> | <span data-ttu-id="f52fa-162">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f52fa-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f52fa-163">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="f52fa-163">username</span></span> | <span data-ttu-id="f52fa-164">Usuario que tiene el servidor de acceso toohello SFTP.</span><span class="sxs-lookup"><span data-stu-id="f52fa-164">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="f52fa-165">Sí</span><span class="sxs-lookup"><span data-stu-id="f52fa-165">Yes</span></span> |
| <span data-ttu-id="f52fa-166">Contraseña</span><span class="sxs-lookup"><span data-stu-id="f52fa-166">password</span></span> | <span data-ttu-id="f52fa-167">Contraseña de usuario de hello (nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="f52fa-167">Password for hello user (username).</span></span> | <span data-ttu-id="f52fa-168">Sí</span><span class="sxs-lookup"><span data-stu-id="f52fa-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="f52fa-169">Ejemplo: Autenticación básica</span><span class="sxs-lookup"><span data-stu-id="f52fa-169">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="f52fa-170">Ejemplo: Autenticación básica con credenciales cifradas</span><span class="sxs-lookup"><span data-stu-id="f52fa-170">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="f52fa-171">Uso de autenticación de clave pública SSH</span><span class="sxs-lookup"><span data-stu-id="f52fa-171">Using SSH public key authentication</span></span>

<span data-ttu-id="f52fa-172">establecer toouse SSH autenticación de clave pública, `authenticationType` como `SshPublicKey`y especifique Hola propiedades siguientes, además de Hola conector SFTP genérico que introdujo en la última sección de hello:</span><span class="sxs-lookup"><span data-stu-id="f52fa-172">toouse SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="f52fa-173">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f52fa-173">Property</span></span> | <span data-ttu-id="f52fa-174">Descripción</span><span class="sxs-lookup"><span data-stu-id="f52fa-174">Description</span></span> | <span data-ttu-id="f52fa-175">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f52fa-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f52fa-176">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="f52fa-176">username</span></span> |<span data-ttu-id="f52fa-177">Usuario que tiene el servidor de acceso toohello SFTP</span><span class="sxs-lookup"><span data-stu-id="f52fa-177">User who has access toohello SFTP server</span></span> |<span data-ttu-id="f52fa-178">Sí</span><span class="sxs-lookup"><span data-stu-id="f52fa-178">Yes</span></span> |
| <span data-ttu-id="f52fa-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="f52fa-179">privateKeyPath</span></span> | <span data-ttu-id="f52fa-180">Especifique la ruta de acceso absoluta toohello archivo de clave privada que puede tener acceso esa puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f52fa-180">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="f52fa-181">Especifique cualquier hello `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="f52fa-181">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="f52fa-182">Se aplica solo cuando se copian datos desde un servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="f52fa-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="f52fa-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="f52fa-183">privateKeyContent</span></span> | <span data-ttu-id="f52fa-184">Una cadena serializada de contenido de clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-184">A serialized string of hello private key content.</span></span> <span data-ttu-id="f52fa-185">Hola Asistente para copiar puede leer el archivo de clave privada de Hola y extraer contenido de clave privada de hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f52fa-185">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="f52fa-186">Si está utilizando cualquier otra herramienta/SDK, use en su lugar la propiedad privateKeyPath de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-186">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="f52fa-187">Especifique cualquier hello `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="f52fa-187">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="f52fa-188">passPhrase</span><span class="sxs-lookup"><span data-stu-id="f52fa-188">passPhrase</span></span> | <span data-ttu-id="f52fa-189">Especificar clave privada de hello paso contraseña/frase toodecrypt Hola si el archivo de clave de hello está protegido por una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="f52fa-189">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="f52fa-190">Sí, si el archivo de clave privada de hello está protegido por una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="f52fa-190">Yes if hello private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="f52fa-191">El conector de SFTP solo admite la clave OpenSSH.</span><span class="sxs-lookup"><span data-stu-id="f52fa-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="f52fa-192">Asegúrese de que el archivo de clave es un formato correcto Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-192">Make sure your key file is in hello proper format.</span></span> <span data-ttu-id="f52fa-193">Puede usar la herramienta Putty tooconvert desde el formato de tooOpenSSH. ppk.</span><span class="sxs-lookup"><span data-stu-id="f52fa-193">You can use Putty tool tooconvert from .ppk tooOpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="f52fa-194">Ejemplo: Autenticación de SshPublicKey mediante el valor de filePath de clave privada</span><span class="sxs-lookup"><span data-stu-id="f52fa-194">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="f52fa-195">Ejemplo: Autenticación de SshPublicKey mediante contenido de clave privada</span><span class="sxs-lookup"><span data-stu-id="f52fa-195">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="f52fa-196">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="f52fa-196">Dataset properties</span></span>
<span data-ttu-id="f52fa-197">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f52fa-197">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f52fa-198">Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="f52fa-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="f52fa-199">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="f52fa-199">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="f52fa-200">Proporciona información de tipo de conjunto de datos toohello específica.</span><span class="sxs-lookup"><span data-stu-id="f52fa-200">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="f52fa-201">Hola typeProperties sección un conjunto de datos de tipo **FileShare** conjunto de datos tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="f52fa-201">hello typeProperties section for a dataset of type **FileShare** dataset has hello following properties:</span></span>

| <span data-ttu-id="f52fa-202">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f52fa-202">Property</span></span> | <span data-ttu-id="f52fa-203">Descripción</span><span class="sxs-lookup"><span data-stu-id="f52fa-203">Description</span></span> | <span data-ttu-id="f52fa-204">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f52fa-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f52fa-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="f52fa-205">folderPath</span></span> |<span data-ttu-id="f52fa-206">Carpeta de toohello de ruta de acceso de Sub.</span><span class="sxs-lookup"><span data-stu-id="f52fa-206">Sub path toohello folder.</span></span> <span data-ttu-id="f52fa-207">Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-207">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="f52fa-208">Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="f52fa-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="f52fa-209">Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin.</span><span class="sxs-lookup"><span data-stu-id="f52fa-209">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="f52fa-210">Sí</span><span class="sxs-lookup"><span data-stu-id="f52fa-210">Yes</span></span> |
| <span data-ttu-id="f52fa-211">fileName</span><span class="sxs-lookup"><span data-stu-id="f52fa-211">fileName</span></span> |<span data-ttu-id="f52fa-212">Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-212">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="f52fa-213">Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-213">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="f52fa-214">Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato:</span><span class="sxs-lookup"><span data-stu-id="f52fa-214">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="f52fa-215">Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="f52fa-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="f52fa-216">No</span><span class="sxs-lookup"><span data-stu-id="f52fa-216">No</span></span> |
| <span data-ttu-id="f52fa-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="f52fa-217">fileFilter</span></span> |<span data-ttu-id="f52fa-218">Especifique un filtro toobe utiliza tooselect un subconjunto de archivos en folderPath hello en lugar de todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="f52fa-218">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="f52fa-219">Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).</span><span class="sxs-lookup"><span data-stu-id="f52fa-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="f52fa-220">Ejemplos 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="f52fa-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="f52fa-221">Ejemplo 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="f52fa-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="f52fa-222">fileFilter es aplicable a un conjunto de datos FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="f52fa-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="f52fa-223">Esta propiedad no es compatible con HDFS.</span><span class="sxs-lookup"><span data-stu-id="f52fa-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="f52fa-224">No</span><span class="sxs-lookup"><span data-stu-id="f52fa-224">No</span></span> |
| <span data-ttu-id="f52fa-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="f52fa-225">partitionedBy</span></span> |<span data-ttu-id="f52fa-226">partitionedBy puede ser usado toospecify un folderPath dinámico, nombre de archivo de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="f52fa-226">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="f52fa-227">Por ejemplo, folderPath se parametriza por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="f52fa-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="f52fa-228">No</span><span class="sxs-lookup"><span data-stu-id="f52fa-228">No</span></span> |
| <span data-ttu-id="f52fa-229">formato</span><span class="sxs-lookup"><span data-stu-id="f52fa-229">format</span></span> | <span data-ttu-id="f52fa-230">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="f52fa-230">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="f52fa-231">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="f52fa-231">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="f52fa-232">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="f52fa-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="f52fa-233">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="f52fa-233">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="f52fa-234">No</span><span class="sxs-lookup"><span data-stu-id="f52fa-234">No</span></span> |
| <span data-ttu-id="f52fa-235">compresión</span><span class="sxs-lookup"><span data-stu-id="f52fa-235">compression</span></span> | <span data-ttu-id="f52fa-236">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-236">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="f52fa-237">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="f52fa-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="f52fa-238">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="f52fa-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="f52fa-239">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="f52fa-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="f52fa-240">No</span><span class="sxs-lookup"><span data-stu-id="f52fa-240">No</span></span> |
| <span data-ttu-id="f52fa-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="f52fa-241">useBinaryTransfer</span></span> |<span data-ttu-id="f52fa-242">Especifica si se usará el modo de transferencia binario.</span><span class="sxs-lookup"><span data-stu-id="f52fa-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="f52fa-243">Su valor es true para el modo binario y false para ASCII.</span><span class="sxs-lookup"><span data-stu-id="f52fa-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="f52fa-244">Valor predeterminado: true.</span><span class="sxs-lookup"><span data-stu-id="f52fa-244">Default value: True.</span></span> <span data-ttu-id="f52fa-245">Esta propiedad solo puede usarse cuando el tipo de servicio vinculado asociado es: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="f52fa-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="f52fa-246">No</span><span class="sxs-lookup"><span data-stu-id="f52fa-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="f52fa-247">filename y fileFilter no pueden usarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="f52fa-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="f52fa-248">Uso de la propiedad partitionedBy</span><span class="sxs-lookup"><span data-stu-id="f52fa-248">Using partionedBy property</span></span>
<span data-ttu-id="f52fa-249">Como se mencionó en la sección anterior de hello, puede especificar un folderPath dinámico, nombre de archivo de datos de serie temporal con partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="f52fa-249">As mentioned in hello previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="f52fa-250">Puede hacerlo con macros de la factoría de datos de Hola y variable del sistema SliceStart, SliceEnd que indican un período de tiempo lógico para un segmento de datos determinado Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-250">You can do so with hello Data Factory macros and hello system variable SliceStart, SliceEnd that indicate hello logical time period for a given data slice.</span></span>

<span data-ttu-id="f52fa-251">toolearn acerca de los conjuntos de datos de series de tiempo, la programación y sectores, consulte [crear conjuntos de datos](data-factory-create-datasets.md), [ejecución y programación](data-factory-scheduling-and-execution.md), y [crear canalizaciones](data-factory-create-pipelines.md) artículos.</span><span class="sxs-lookup"><span data-stu-id="f52fa-251">toolearn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="f52fa-252">Muestra 1:</span><span class="sxs-lookup"><span data-stu-id="f52fa-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="f52fa-253">En este ejemplo {Slice} se reemplaza con el valor de Hola de variable del sistema SliceStart factoría de datos en formato de hello (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="f52fa-253">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="f52fa-254">Hola SliceStart refiere a tiempo toostart de segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-254">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="f52fa-255">Hola folderPath es diferente para cada segmento.</span><span class="sxs-lookup"><span data-stu-id="f52fa-255">hello folderPath is different for each slice.</span></span> <span data-ttu-id="f52fa-256">Ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="f52fa-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="f52fa-257">Ejemplo 2:</span><span class="sxs-lookup"><span data-stu-id="f52fa-257">Sample 2:</span></span>

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
<span data-ttu-id="f52fa-258">En este ejemplo, year, month, day y time de SliceStart se extraen en variables independientes que se usan en las propiedades folderPath y fileName.</span><span class="sxs-lookup"><span data-stu-id="f52fa-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="f52fa-259">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="f52fa-259">Copy activity properties</span></span>
<span data-ttu-id="f52fa-260">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f52fa-260">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f52fa-261">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="f52fa-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="f52fa-262">Mientras que hello las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="f52fa-262">Whereas, hello properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="f52fa-263">Para la actividad de copia, propiedades de tipo de hello varían en función de tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="f52fa-263">For Copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="f52fa-264">Formatos de archivo y de compresión admitidos</span><span class="sxs-lookup"><span data-stu-id="f52fa-264">Supported file and compression formats</span></span>
<span data-ttu-id="f52fa-265">Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="f52fa-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a><span data-ttu-id="f52fa-266">Ejemplo JSON: Copiar los datos de blob de tooAzure servidor SFTP</span><span class="sxs-lookup"><span data-stu-id="f52fa-266">JSON Example: Copy data from SFTP server tooAzure blob</span></span>
<span data-ttu-id="f52fa-267">Hello en el ejemplo siguiente se proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f52fa-267">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f52fa-268">Muestra cómo tooAzure almacenamiento de blobs del origen de datos de toocopy de SFTP.</span><span class="sxs-lookup"><span data-stu-id="f52fa-268">They show how toocopy data from SFTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="f52fa-269">Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f52fa-269">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f52fa-270">Este ejemplo proporciona fragmentos JSON.</span><span class="sxs-lookup"><span data-stu-id="f52fa-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="f52fa-271">No incluye instrucciones paso a paso para la creación de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-271">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="f52fa-272">Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="f52fa-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="f52fa-273">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="f52fa-273">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="f52fa-274">Un servicio vinculado de tipo [sftp](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f52fa-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="f52fa-275">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="f52fa-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="f52fa-276">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f52fa-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="f52fa-277">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f52fa-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="f52fa-278">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f52fa-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f52fa-279">ejemplo de Hola copia datos de una tooan del servidor SFTP blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="f52fa-279">hello sample copies data from an SFTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="f52fa-280">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="f52fa-280">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="f52fa-281">**Servicio vinculado de SFTP**</span><span class="sxs-lookup"><span data-stu-id="f52fa-281">**SFTP linked service**</span></span>

<span data-ttu-id="f52fa-282">En este ejemplo se utiliza la autenticación básica hello con nombre de usuario y una contraseña en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="f52fa-282">This example uses hello basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="f52fa-283">También puede utilizar uno de hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="f52fa-283">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="f52fa-284">Autenticación básica con credenciales cifradas</span><span class="sxs-lookup"><span data-stu-id="f52fa-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="f52fa-285">Autenticación de la clave pública SSH</span><span class="sxs-lookup"><span data-stu-id="f52fa-285">SSH public key authentication</span></span>

<span data-ttu-id="f52fa-286">Para los diferentes tipos de autenticación que se pueden usar, consulte la sección [Propiedades del servicio vinculado de FTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f52fa-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="f52fa-287">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="f52fa-287">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="f52fa-288">**Conjunto de datos de entrada de SFTP**</span><span class="sxs-lookup"><span data-stu-id="f52fa-288">**SFTP input dataset**</span></span>

<span data-ttu-id="f52fa-289">Este conjunto de datos hace referencia a carpeta SFTP toohello `mysharedfolder` y el archivo `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="f52fa-289">This dataset refers toohello SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="f52fa-290">Hola canalización copias hello toohello destino del archivo.</span><span class="sxs-lookup"><span data-stu-id="f52fa-290">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="f52fa-291">Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-291">Setting "external": "true" informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="f52fa-292">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="f52fa-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="f52fa-293">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="f52fa-293">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f52fa-294">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="f52fa-294">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="f52fa-295">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f52fa-295">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="f52fa-296">**Canalización con actividad de copia**</span><span class="sxs-lookup"><span data-stu-id="f52fa-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="f52fa-297">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="f52fa-297">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="f52fa-298">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**FileSystemSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f52fa-298">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="f52fa-299">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="f52fa-299">Performance and Tuning</span></span>
<span data-ttu-id="f52fa-300">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="f52fa-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f52fa-301">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f52fa-301">Next Steps</span></span>
<span data-ttu-id="f52fa-302">Vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="f52fa-302">See hello following articles:</span></span>

* <span data-ttu-id="f52fa-303">[Tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso para la creación de una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="f52fa-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
