---
title: "configuración de seguridad mezcla aaaSplit | Documentos de Microsoft"
description: "Configuración de certificados x409 para cifrado"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="b3aa9-103">Configuración de seguridad de división y combinación</span><span class="sxs-lookup"><span data-stu-id="b3aa9-103">Split-merge security configuration</span></span>
<span data-ttu-id="b3aa9-104">servicio de dividir y combinar de hello toouse, debe configurar correctamente la seguridad.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="b3aa9-105">Hola servicio forma parte de la característica de escalado flexible de Hola de base de datos de SQL de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="b3aa9-106">Para obtener más información, vea el [Tutorial del servicio de división y combinación de Escalado elástico](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="b3aa9-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="b3aa9-107">Configuración de certificados</span><span class="sxs-lookup"><span data-stu-id="b3aa9-107">Configuring certificates</span></span>
<span data-ttu-id="b3aa9-108">Los certificados se configuran de dos maneras.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="b3aa9-109">Hola tooConfigure certificado SSL</span><span class="sxs-lookup"><span data-stu-id="b3aa9-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="b3aa9-110">tooConfigure certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="b3aa9-111">certificados tooobtain</span><span class="sxs-lookup"><span data-stu-id="b3aa9-111">tooobtain certificates</span></span>
<span data-ttu-id="b3aa9-112">Se pueden obtener certificados de entidades de certificación pública (CA) o de hello [servicio de certificados de Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3aa9-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="b3aa9-113">Se trata de hello preferido métodos tooobtain certificados.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="b3aa9-114">Si esas opciones no están disponibles, puede generar **certificados autofirmados**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="b3aa9-115">Certificados de toogenerate de herramientas</span><span class="sxs-lookup"><span data-stu-id="b3aa9-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="b3aa9-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="b3aa9-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="b3aa9-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="b3aa9-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="b3aa9-118">herramientas de hello toorun</span><span class="sxs-lookup"><span data-stu-id="b3aa9-118">toorun hello tools</span></span>
* <span data-ttu-id="b3aa9-119">Desde el Símbolo del sistema para desarrolladores de Visual Studio, consulte [Símbolo del sistema de Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="b3aa9-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="b3aa9-120">Si está instalado, vaya a:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="b3aa9-121">Obtener Hola WDK de [Windows 8.1: descargar kits y herramientas](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="b3aa9-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="b3aa9-122">certificado SSL de tooconfigure Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="b3aa9-123">Un certificado SSL es necesario tooencrypt Hola comunicación y autenticar el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="b3aa9-124">Elegir el más apropiado de hello tres escenarios de Hola y ejecute todos sus pasos:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="b3aa9-125">Creación de un nuevo certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="b3aa9-126">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="b3aa9-127">Creación del archivo PFX para el certificado SSL autofirmado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="b3aa9-128">Cargar el certificado SSL tooCloud servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="b3aa9-129">Actualización del certificado SSL en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="b3aa9-130">Importación de la Entidad de certificación SSL</span><span class="sxs-lookup"><span data-stu-id="b3aa9-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="b3aa9-131">almacenar de un certificado existente de certificado de hello toouse</span><span class="sxs-lookup"><span data-stu-id="b3aa9-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="b3aa9-132">Exportación del certificado SSL desde el almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="b3aa9-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="b3aa9-133">Cargar el certificado SSL tooCloud servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="b3aa9-134">Actualización del certificado SSL en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="b3aa9-135">toouse un certificado existente en un archivo PFX</span><span class="sxs-lookup"><span data-stu-id="b3aa9-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="b3aa9-136">Cargar el certificado SSL tooCloud servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="b3aa9-137">Actualización del certificado SSL en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="b3aa9-138">certificados de cliente tooconfigure</span><span class="sxs-lookup"><span data-stu-id="b3aa9-138">tooconfigure client certificates</span></span>
<span data-ttu-id="b3aa9-139">Se requieren certificados de cliente en orden tooauthenticate solicitudes toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="b3aa9-140">Elegir el más apropiado de hello tres escenarios de Hola y ejecute todos sus pasos:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="b3aa9-141">Desactivación de los certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="b3aa9-142">Desactivación de la autenticación basada en certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="b3aa9-143">Emisión de nuevos certificados de cliente autofirmados</span><span class="sxs-lookup"><span data-stu-id="b3aa9-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="b3aa9-144">Creación de una Entidad de certificación autofirmada</span><span class="sxs-lookup"><span data-stu-id="b3aa9-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="b3aa9-145">Cargar certificado de CA tooCloud servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="b3aa9-146">Actualización de un certificado de Entidad de certificación en un archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="b3aa9-147">Emisión de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="b3aa9-148">Creación de archivos PFX para certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="b3aa9-149">Importación de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="b3aa9-150">Copia de las huellas digitales de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="b3aa9-151">Configurar a clientes permitido en hello archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="b3aa9-152">Uso de certificados de cliente existentes</span><span class="sxs-lookup"><span data-stu-id="b3aa9-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="b3aa9-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="b3aa9-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="b3aa9-154">Cargar certificado de CA tooCloud servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="b3aa9-155">Actualización de un certificado de Entidad de certificación en un archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="b3aa9-156">Copia de las huellas digitales de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="b3aa9-157">Configurar a clientes permitido en hello archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="b3aa9-158">Configuración de la comprobación de revocación de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="b3aa9-159">Direcciones IP permitidas</span><span class="sxs-lookup"><span data-stu-id="b3aa9-159">Allowed IP addresses</span></span>
<span data-ttu-id="b3aa9-160">Los puntos de conexión de servicio de acceso toohello pueden ser restringido toospecific intervalos de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="b3aa9-161">cifrado de tooconfigure para la tienda de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="b3aa9-162">Un certificado es credenciales de hello tooencrypt requiere que se almacenan en el almacén de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="b3aa9-163">Elegir el más apropiado de hello tres escenarios de Hola y ejecute todos sus pasos:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="b3aa9-164">Use un nuevo certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="b3aa9-165">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="b3aa9-166">Crear archivo PFX para certificado de cifrado autofirmado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="b3aa9-167">Cargar certificado de cifrado tooCloud servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="b3aa9-168">Actualización del certificado de cifrado en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="b3aa9-169">Usar un certificado existente del almacén de certificados de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="b3aa9-170">Exportar el certificado de cifrado del almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="b3aa9-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="b3aa9-171">Cargar certificado de cifrado tooCloud servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="b3aa9-172">Actualización del certificado de cifrado en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="b3aa9-173">Utilizar un certificado existente de un archivo PFX</span><span class="sxs-lookup"><span data-stu-id="b3aa9-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="b3aa9-174">Cargar certificado de cifrado tooCloud servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="b3aa9-175">Actualización del certificado de cifrado en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="b3aa9-176">configuración predeterminada de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-176">hello default configuration</span></span>
<span data-ttu-id="b3aa9-177">configuración predeterminada de Hello deniega el punto de conexión de todos los acceso toohello HTTP.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="b3aa9-178">Se trata de hello recomendado, ya que los puntos de conexión de hello solicitudes toothese pueden incluir información confidencial, como credenciales de base de datos.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="b3aa9-179">configuración predeterminada de Hello permite que el punto de conexión de todos los acceso toohello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="b3aa9-180">Esta configuración puede ser aún más restrictiva.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="b3aa9-181">Cambiar la configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-181">Changing hello Configuration</span></span>
<span data-ttu-id="b3aa9-182">grupo de reglas de control de acceso que se aplican tooand extremo Hello se configura una Hola  **<EndpointAcls>**  sección Hola **archivo de configuración de servicio**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="b3aa9-183">las reglas de Hello en un grupo de control de acceso están configuradas en un <AccessControl name=""> sección del archivo de configuración de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="b3aa9-184">formato de Hola se explica en la documentación de listas de Control de acceso de red.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="b3aa9-185">Por ejemplo, tooallow IP única en el punto de conexión de hello intervalo 100.100.0.0 too100.100.255.255 tooaccess Hola HTTPS, las reglas de hello sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="b3aa9-186">Prevención de la denegación de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-186">Denial of service prevention</span></span>
<span data-ttu-id="b3aa9-187">Hay dos mecanismos diferentes admiten toodetect y evitar los ataques de denegación de servicio:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="b3aa9-188">Restringir la cantidad de solicitudes simultáneas por host remoto (desactivado de manera predeterminada)</span><span class="sxs-lookup"><span data-stu-id="b3aa9-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="b3aa9-189">Restringir la velocidad de acceso por host remoto (activado de manera predeterminada)</span><span class="sxs-lookup"><span data-stu-id="b3aa9-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="b3aa9-190">Estos se basan en características de hello ampliamente documentados en seguridad IP dinámica en IIS.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="b3aa9-191">Al cambiar esta configuración tenga cuidado de no Hola siguientes factores:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="b3aa9-192">comportamiento de Hola de dispositivos de traducción de direcciones de red sobre la información del host remoto de Hola y servidores proxy</span><span class="sxs-lookup"><span data-stu-id="b3aa9-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="b3aa9-193">Se considera que cada recurso de tooany de solicitud en función de hello web (por ejemplo, cargar las secuencias de comandos, imágenes, etcetera)</span><span class="sxs-lookup"><span data-stu-id="b3aa9-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="b3aa9-194">Restricción de la cantidad de acceso simultáneos</span><span class="sxs-lookup"><span data-stu-id="b3aa9-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="b3aa9-195">configuración de Hola que configura este comportamiento es:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="b3aa9-196">Cambiar DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable esta protección.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="b3aa9-197">Restricción de la velocidad del acceso</span><span class="sxs-lookup"><span data-stu-id="b3aa9-197">Restricting rate of access</span></span>
<span data-ttu-id="b3aa9-198">configuración de Hola que configura este comportamiento es:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="b3aa9-199">Configurar Hola respuesta tooa denegó la solicitud</span><span class="sxs-lookup"><span data-stu-id="b3aa9-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="b3aa9-200">Hello siguiente configura Hola respuesta tooa denegado la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="b3aa9-201">Consulte la documentación de toohello de seguridad IP dinámica en IIS para ver otros valores compatibles.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="b3aa9-202">Operaciones para configurar certificados de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="b3aa9-203">Este tema es solo para referencia.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-203">This topic is for reference only.</span></span> <span data-ttu-id="b3aa9-204">Siga los pasos de configuración de Hola que se describen en:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="b3aa9-205">Configurar un certificado SSL de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="b3aa9-206">Configuración de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="b3aa9-207">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-207">Create a self-signed certificate</span></span>
<span data-ttu-id="b3aa9-208">Ejecute:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="b3aa9-209">toocustomize:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-209">toocustomize:</span></span>

* <span data-ttu-id="b3aa9-210">-n con la dirección URL del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-210">-n with hello service URL.</span></span> <span data-ttu-id="b3aa9-211">Caracteres comodín ("CN=*.cloudapp.net") y nombres alternativos ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") son compatibles.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="b3aa9-212">-e con fecha de expiración del certificado de hello crear una contraseña segura y especificarla cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="b3aa9-213">Creación del archivo PFX para el certificado SSL autofirmado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="b3aa9-214">Ejecute:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="b3aa9-215">Escriba la contraseña y, a continuación, exporte el certificado con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="b3aa9-216">Sí, exportar la clave privada de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-216">Yes, export hello private key</span></span>
* <span data-ttu-id="b3aa9-217">Exportar todas las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="b3aa9-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="b3aa9-218">Exportación del certificado SSL desde el almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="b3aa9-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="b3aa9-219">Busque el certificado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-219">Find certificate</span></span>
* <span data-ttu-id="b3aa9-220">Haga clic en Acciones -> Todas las tareas -> Exportar…</span><span class="sxs-lookup"><span data-stu-id="b3aa9-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="b3aa9-221">Exporte el certificado a un archivo .PFX con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="b3aa9-222">Sí, exportar la clave privada de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="b3aa9-223">Si es posible, incluir todos los certificados de ruta de certificación de Hola * exportar todas las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="b3aa9-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="b3aa9-224">Cargar el servicio de toocloud de certificados SSL</span><span class="sxs-lookup"><span data-stu-id="b3aa9-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="b3aa9-225">Cargar el certificado con hello existente o generados. Archivo PFX con hello par de claves de SSL:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="b3aa9-226">Escribir contraseña de hello proteger la información de clave privada de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="b3aa9-227">Actualización del certificado SSL en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="b3aa9-228">Actualizar el valor de huella digital de Hola de hello después de la configuración en el archivo de configuración de servicio de hello con la huella digital de hello del servicio de nube de hello certificado cargado toohello:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="b3aa9-229">Importación de la Entidad de certificación SSL</span><span class="sxs-lookup"><span data-stu-id="b3aa9-229">Import SSL certification authority</span></span>
<span data-ttu-id="b3aa9-230">Siga estos pasos en todas las cuentas/máquina que se comunicarán con el servicio de Hola:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="b3aa9-231">Haga doble clic en Hola. Archivo .cer en el Explorador de Windows</span><span class="sxs-lookup"><span data-stu-id="b3aa9-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="b3aa9-232">En el cuadro de diálogo de certificado de hello, haga clic en Instalar certificado...</span><span class="sxs-lookup"><span data-stu-id="b3aa9-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="b3aa9-233">Importar certificado Hola que almacenar entidades de certificación raíz de confianza</span><span class="sxs-lookup"><span data-stu-id="b3aa9-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="b3aa9-234">Desactivación de la autenticación basada en certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="b3aa9-235">Se admite solo basada en certificado autenticación de cliente y deshabilitarlo permitirá a los puntos de conexión del servicio de toohello de acceso público, a menos que otros mecanismos están en vigor (por ejemplo, Microsoft Azure Virtual Network).</span><span class="sxs-lookup"><span data-stu-id="b3aa9-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="b3aa9-236">Cambiar estos toofalse de configuración de característica del servicio configuración archivo tooturn Hola de hello:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="b3aa9-237">A continuación, copie Hola misma huella digital que Hola SSL de certificados en la configuración del certificado de entidad emisora de certificados de hello:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="b3aa9-238">Creación de una Entidad de certificación autofirmada</span><span class="sxs-lookup"><span data-stu-id="b3aa9-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="b3aa9-239">Ejecute hello siguiendo los pasos toocreate un tooact certificado autofirmado como una entidad de certificación:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="b3aa9-240">toocustomize,</span><span class="sxs-lookup"><span data-stu-id="b3aa9-240">toocustomize it</span></span>

* <span data-ttu-id="b3aa9-241">-e con fecha de expiración de certificación de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="b3aa9-242">Búsqueda de clave pública de Entidad de certificación</span><span class="sxs-lookup"><span data-stu-id="b3aa9-242">Find CA public key</span></span>
<span data-ttu-id="b3aa9-243">Todos los certificados de cliente se deben haber emitido por una entidad de certificación de confianza para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="b3aa9-244">Buscar hello toohello clave pública entidad de certificación que emite certificados de cliente de Hola que van toobe utilizado para la autenticación en tooupload de orden se toohello servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="b3aa9-245">Si no hay ningún archivo de hello con clave pública de hello, exportarlo desde el almacén de certificados de hello:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="b3aa9-246">Busque el certificado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-246">Find certificate</span></span>
  * <span data-ttu-id="b3aa9-247">Busque un certificado de cliente emitido por Hola misma entidad de certificación</span><span class="sxs-lookup"><span data-stu-id="b3aa9-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="b3aa9-248">Haga doble clic en el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="b3aa9-249">Seleccione la pestaña de la ruta de certificación de hello en el cuadro de diálogo de hello certificado.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="b3aa9-250">Haga doble clic en la entrada de la entidad emisora de certificados de hello en ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="b3aa9-251">Tomar notas Hola de propiedades de certificado.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="b3aa9-252">Hola cerrar **certificado** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="b3aa9-253">Busque el certificado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-253">Find certificate</span></span>
  * <span data-ttu-id="b3aa9-254">Busque Hola CA se ha mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="b3aa9-255">Haga clic en Acciones -> Todas las tareas -> Exportar…</span><span class="sxs-lookup"><span data-stu-id="b3aa9-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="b3aa9-256">Exporte el certificado a un archivo .CER con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="b3aa9-257">**No, no exportar la clave privada de Hola**</span><span class="sxs-lookup"><span data-stu-id="b3aa9-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="b3aa9-258">Si es posible, incluir todos los certificados de ruta de certificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="b3aa9-259">Exportar todas las propiedades extendidas.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="b3aa9-260">Cargar el servicio de toocloud de certificados de entidad emisora de certificados</span><span class="sxs-lookup"><span data-stu-id="b3aa9-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="b3aa9-261">Cargar el certificado con hello existente o generados. Archivo CER con clave pública de hello entidad emisora de certificados.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="b3aa9-262">Actualización de un certificado de Entidad de certificación en un archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="b3aa9-263">Actualizar el valor de huella digital de Hola de hello después de la configuración en el archivo de configuración de servicio de hello con la huella digital de hello del servicio de nube de hello certificado cargado toohello:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="b3aa9-264">Actualizar el valor de Hola de hello después de establecer con hello mismo huella digital:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="b3aa9-265">Emisión de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-265">Issue client certificates</span></span>
<span data-ttu-id="b3aa9-266">Cada servicio de hello tooaccess autorizados individuales debe tener un certificado de cliente emitido para his/hers exclusivo usar y debe elegir que posee tooprotect contraseña segura su clave privada.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="b3aa9-267">Hola pasos debe realizarse en Hola se generan y almacenan el mismo equipo donde hello certificado autofirmado de entidad emisora de certificados:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="b3aa9-268">Personalización:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-268">Customizing:</span></span>

* <span data-ttu-id="b3aa9-269">-n con un identificador de cliente de toohello que se autenticarán con este certificado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="b3aa9-270">-e con fecha de expiración del certificado de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="b3aa9-271">MyID.pvk y MyID.cer con nombres de archivo únicos para este certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="b3aa9-272">Este comando le solicitará una contraseña toobe creado y, a continuación, usar una vez.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="b3aa9-273">Utilice una contraseña segura.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="b3aa9-274">Creación de archivos PFX para certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="b3aa9-275">Para cada certificado de cliente generado, ejecute:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="b3aa9-276">Personalización:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="b3aa9-277">Escriba la contraseña y, a continuación, exporte el certificado con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="b3aa9-278">Sí, exportar la clave privada de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-278">Yes, export hello private key</span></span>
* <span data-ttu-id="b3aa9-279">Exportar todas las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="b3aa9-279">Export all extended properties</span></span>
* <span data-ttu-id="b3aa9-280">Hola toowhom individuales que se está emitiendo este certificado debe elegir la contraseña de la exportación de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="b3aa9-281">Importación de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-281">Import client certificate</span></span>
<span data-ttu-id="b3aa9-282">Cada usuario para el que se emitió un certificado de cliente debe importar el par de claves de hello en máquinas de Hola utilizará toocommunicate con el servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="b3aa9-283">Haga doble clic en Hola. Archivo PFX en el Explorador de Windows</span><span class="sxs-lookup"><span data-stu-id="b3aa9-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="b3aa9-284">Importar certificado Hola Personal para almacenar con al menos esta opción:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="b3aa9-285">Incluir todas las propiedades extendidas comprobadas</span><span class="sxs-lookup"><span data-stu-id="b3aa9-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="b3aa9-286">Copia de las huellas digitales de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="b3aa9-287">Cada usuario para el que se emitió un certificado de cliente debe seguir estos pasos en la huella digital de orden tooobtain Hola de his/hers certificado que se agregará al archivo de configuración de servicio de toohello:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="b3aa9-288">Ejecute certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="b3aa9-288">Run certmgr.exe</span></span>
* <span data-ttu-id="b3aa9-289">Seleccione la ficha Personal Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-289">Select hello Personal tab</span></span>
* <span data-ttu-id="b3aa9-290">Haga doble clic en el certificado de cliente de hello toobe usado para la autenticación</span><span class="sxs-lookup"><span data-stu-id="b3aa9-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="b3aa9-291">En hello certificado cuadro de diálogo que se abre, seleccione la ficha de detalles de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="b3aa9-292">Asegúrese de que Mostrar esté mostrando Todo</span><span class="sxs-lookup"><span data-stu-id="b3aa9-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="b3aa9-293">Campo de hello seleccione denominado huella digital en la lista de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="b3aa9-294">Copiar valor de Hola de huella digital de Hola ** eliminar los caracteres Unicode no visibles delante del primer dígito de Hola ** eliminar todos los espacios</span><span class="sxs-lookup"><span data-stu-id="b3aa9-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="b3aa9-295">Configurar a clientes de permitido en el archivo de configuración de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="b3aa9-296">Actualizar el valor de Hola de hello después de la configuración en el archivo de configuración de servicio de hello con una lista separada por comas de huellas digitales de Hola Hola de certificados de cliente permitidos el acceso toohello servicio:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="b3aa9-297">Configuración de la comprobación de revocación de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="b3aa9-298">configuración predeterminada de Hello no comprueba con hello entidad de certificación para el estado de revocación del certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="b3aa9-299">tooturn en hello comprueba si Hola entidad de certificación que emitió los certificados de cliente hello es compatible con esas comprobaciones, cambie Hola siguientes configuración con uno de los valores de hello definidos en hello X509RevocationMode enumeración:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="b3aa9-300">Crear archivo PFX para certificados de cifrado autofirmados</span><span class="sxs-lookup"><span data-stu-id="b3aa9-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="b3aa9-301">Para un certificado de cifrado, ejecute:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="b3aa9-302">Personalización:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="b3aa9-303">Escriba la contraseña y, a continuación, exporte el certificado con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="b3aa9-304">Sí, exportar la clave privada de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-304">Yes, export hello private key</span></span>
* <span data-ttu-id="b3aa9-305">Exportar todas las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="b3aa9-305">Export all extended properties</span></span>
* <span data-ttu-id="b3aa9-306">Necesitará Hola contraseña al cargar el servicio de nube de hello certificados toohello.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="b3aa9-307">Exportar el certificado de cifrado del almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="b3aa9-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="b3aa9-308">Busque el certificado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-308">Find certificate</span></span>
* <span data-ttu-id="b3aa9-309">Haga clic en Acciones -> Todas las tareas -> Exportar…</span><span class="sxs-lookup"><span data-stu-id="b3aa9-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="b3aa9-310">Exporte el certificado a un archivo .PFX con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="b3aa9-311">Sí, exportar la clave privada de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="b3aa9-312">Si es posible, incluir todos los certificados de ruta de certificación de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="b3aa9-313">Exportar todas las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="b3aa9-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="b3aa9-314">Cargar el servicio de toocloud de certificados de cifrado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="b3aa9-315">Cargar el certificado con hello existente o generados. Archivo PFX con el par de claves de cifrado de hello:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="b3aa9-316">Escribir contraseña de hello proteger la información de clave privada de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="b3aa9-317">Actualización del certificado de cifrado en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="b3aa9-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="b3aa9-318">Actualizar el valor de huella digital de Hola de hello después de la configuración en el archivo de configuración de servicio de hello con la huella digital de hello del servicio de nube de hello certificado cargado toohello:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="b3aa9-319">Operaciones comunes de certificado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-319">Common certificate operations</span></span>
* <span data-ttu-id="b3aa9-320">Configurar un certificado SSL de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="b3aa9-321">Configuración de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="b3aa9-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="b3aa9-322">Busque el certificado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-322">Find certificate</span></span>
<span data-ttu-id="b3aa9-323">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-323">Follow these steps:</span></span>

1. <span data-ttu-id="b3aa9-324">Ejecute mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="b3aa9-325">Archivo -> Agregar o quitar complemento…</span><span class="sxs-lookup"><span data-stu-id="b3aa9-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="b3aa9-326">Seleccione **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="b3aa9-327">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-327">Click **Add**.</span></span>
5. <span data-ttu-id="b3aa9-328">Elija la ubicación del almacén de certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="b3aa9-329">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="b3aa9-329">Click **Finish**.</span></span>
7. <span data-ttu-id="b3aa9-330">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-330">Click **OK**.</span></span>
8. <span data-ttu-id="b3aa9-331">Expanda **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="b3aa9-332">Expanda el nodo del almacén de certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="b3aa9-333">Expandir nodo de hello certificado secundario.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="b3aa9-334">Seleccione un certificado en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="b3aa9-335">Exportación de certificado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-335">Export certificate</span></span>
<span data-ttu-id="b3aa9-336">Hola **Asistente para exportar certificados**:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="b3aa9-337">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-337">Click **Next**.</span></span>
2. <span data-ttu-id="b3aa9-338">Seleccione **Sí**, a continuación, **clave privada de exportación hello**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="b3aa9-339">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-339">Click **Next**.</span></span>
4. <span data-ttu-id="b3aa9-340">Seleccione el formato de archivo de salida que desee Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="b3aa9-341">Compruebe las opciones de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-341">Check hello desired options.</span></span>
6. <span data-ttu-id="b3aa9-342">Marque **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-342">Check **Password**.</span></span>
7. <span data-ttu-id="b3aa9-343">Escriba una contraseña segura y confírmela.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="b3aa9-344">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-344">Click **Next**.</span></span>
9. <span data-ttu-id="b3aa9-345">Escriba o busque un nombre de archivo donde toostore Hola certificado (utilice una. Extensión PFX).</span><span class="sxs-lookup"><span data-stu-id="b3aa9-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="b3aa9-346">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-346">Click **Next**.</span></span>
11. <span data-ttu-id="b3aa9-347">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="b3aa9-347">Click **Finish**.</span></span>
12. <span data-ttu-id="b3aa9-348">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="b3aa9-349">Importación de certificado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-349">Import certificate</span></span>
<span data-ttu-id="b3aa9-350">En el Asistente para importar certificados hello:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="b3aa9-351">Seleccione la ubicación del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="b3aa9-352">Seleccione **usuario actual** si solo los procesos que se ejecutan en usuario actual tendrá acceso a servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="b3aa9-353">Seleccione **equipo Local** si otros procesos en este equipo tendrá acceso a servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="b3aa9-354">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-354">Click **Next**.</span></span>
3. <span data-ttu-id="b3aa9-355">Si importa desde un archivo, confirme la ruta de acceso de archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="b3aa9-356">Si se importa un archivo .PFX:</span><span class="sxs-lookup"><span data-stu-id="b3aa9-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="b3aa9-357">Escribir contraseña de hello protege la clave privada de Hola</span><span class="sxs-lookup"><span data-stu-id="b3aa9-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="b3aa9-358">Seleccione las opciones de importación</span><span class="sxs-lookup"><span data-stu-id="b3aa9-358">Select import options</span></span>
5. <span data-ttu-id="b3aa9-359">Seleccionar certificados de "Ubicación" Hola después de la tienda</span><span class="sxs-lookup"><span data-stu-id="b3aa9-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="b3aa9-360">Haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-360">Click **Browse**.</span></span>
7. <span data-ttu-id="b3aa9-361">Seleccionar el almacén de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-361">Select hello desired store.</span></span>
8. <span data-ttu-id="b3aa9-362">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="b3aa9-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="b3aa9-363">Si se ha elegido el almacén de la entidad de certificación raíz de confianza de hello, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="b3aa9-364">Haga clic en **Aceptar** en todas las ventanas de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="b3aa9-365">Carga del certificado</span><span class="sxs-lookup"><span data-stu-id="b3aa9-365">Upload certificate</span></span>
<span data-ttu-id="b3aa9-366">Hola [Portal de Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="b3aa9-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="b3aa9-367">Seleccione **Servicios en la nube**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="b3aa9-368">Seleccione servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="b3aa9-369">En el menú superior de hello, haga clic en **certificados**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="b3aa9-370">En la barra de la parte inferior de hello, haga clic en **cargar**.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="b3aa9-371">Seleccione el archivo de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="b3aa9-372">Si es un. PFX archivo, escriba la contraseña de hello para la clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="b3aa9-373">Una vez completado, copie huella digital del certificado Hola de nueva entrada de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="b3aa9-374">Otras consideraciones de seguridad</span><span class="sxs-lookup"><span data-stu-id="b3aa9-374">Other security considerations</span></span>
<span data-ttu-id="b3aa9-375">configuración de SSL de Hello descrita en este documento cifrar la comunicación entre servicio hello y sus clientes cuando se usa el punto de conexión de hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="b3aa9-376">Esto es importante, porque las credenciales para el acceso a la base de datos y posiblemente otra información confidencial están incluidos en la comunicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="b3aa9-377">Sin embargo, tenga en cuenta que el servicio de hello continúa estado interno, incluidas las credenciales, en sus tablas internas de la base de datos de SQL de Microsoft Azure de Hola que ha proporcionado para el almacenamiento de metadatos en su suscripción de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="b3aa9-378">Esa base de datos se ha definido como parte de hello después de la configuración en el archivo de configuración de servicio (. Archivo CSCFG):</span><span class="sxs-lookup"><span data-stu-id="b3aa9-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="b3aa9-379">Las credenciales almacenadas en esta base de datos están cifradas.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="b3aa9-380">Sin embargo, como práctica recomendada, asegúrese de que los roles web y de trabajo de las implementaciones de servicio se mantienen toodate y segura tienen acceso toohello metadatos hello y base de datos certificado usado para el cifrado y descifrado de credenciales almacenadas.</span><span class="sxs-lookup"><span data-stu-id="b3aa9-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

