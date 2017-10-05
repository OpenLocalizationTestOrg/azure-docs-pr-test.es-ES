---
title: "Configuración de seguridad de división y combinación | Microsoft Docs"
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
ms.openlocfilehash: 7e6ccf51a4b75eef16a7df5c1a1018954af8e5dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="fab79-103">Configuración de seguridad de división y combinación</span><span class="sxs-lookup"><span data-stu-id="fab79-103">Split-merge security configuration</span></span>
<span data-ttu-id="fab79-104">Para usar el servicio de división y combinación, debe configurar correctamente la seguridad.</span><span class="sxs-lookup"><span data-stu-id="fab79-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="fab79-105">El servicio forma parte de la característica de Escalado elástico de la Base de datos SQL de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fab79-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="fab79-106">Para obtener más información, vea el [Tutorial del servicio de división y combinación de Escalado elástico](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="fab79-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="fab79-107">Configuración de certificados</span><span class="sxs-lookup"><span data-stu-id="fab79-107">Configuring certificates</span></span>
<span data-ttu-id="fab79-108">Los certificados se configuran de dos maneras.</span><span class="sxs-lookup"><span data-stu-id="fab79-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="fab79-109">Configuración del certificado SSL</span><span class="sxs-lookup"><span data-stu-id="fab79-109">To Configure the SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="fab79-110">Configuración del certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-110">To Configure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="fab79-111">Obtención de certificados</span><span class="sxs-lookup"><span data-stu-id="fab79-111">To obtain certificates</span></span>
<span data-ttu-id="fab79-112">Los certificados se pueden obtener de Entidades de certificación (CA) públicas o desde el [Servicio de certificados de Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="fab79-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="fab79-113">Estos son los métodos preferidos para obtener certificados.</span><span class="sxs-lookup"><span data-stu-id="fab79-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="fab79-114">Si esas opciones no están disponibles, puede generar **certificados autofirmados**.</span><span class="sxs-lookup"><span data-stu-id="fab79-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="fab79-115">Herramientas para generar certificados</span><span class="sxs-lookup"><span data-stu-id="fab79-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="fab79-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="fab79-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="fab79-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="fab79-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="fab79-118">Ejecución de las herramientas</span><span class="sxs-lookup"><span data-stu-id="fab79-118">To run the tools</span></span>
* <span data-ttu-id="fab79-119">Desde el Símbolo del sistema para desarrolladores de Visual Studio, consulte [Símbolo del sistema de Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="fab79-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="fab79-120">Si está instalado, vaya a:</span><span class="sxs-lookup"><span data-stu-id="fab79-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="fab79-121">Obtenga el WDK de [Windows 8.1: descargar kits y herramientas](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="fab79-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="fab79-122">Configuración del certificado SSL</span><span class="sxs-lookup"><span data-stu-id="fab79-122">To configure the SSL certificate</span></span>
<span data-ttu-id="fab79-123">Se requiere un certificado SSL para cifrar la comunicación y autenticar el servidor.</span><span class="sxs-lookup"><span data-stu-id="fab79-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="fab79-124">Elija el escenario más aplicable entre los tres que aparecen a continuación y ejecute todos sus pasos:</span><span class="sxs-lookup"><span data-stu-id="fab79-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="fab79-125">Creación de un nuevo certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="fab79-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="fab79-126">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="fab79-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="fab79-127">Creación del archivo PFX para el certificado SSL autofirmado</span><span class="sxs-lookup"><span data-stu-id="fab79-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="fab79-128">Carga del certificado SSL en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-128">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="fab79-129">Actualización del certificado SSL en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="fab79-130">Importación de la Entidad de certificación SSL</span><span class="sxs-lookup"><span data-stu-id="fab79-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="fab79-131">Para utilizar un certificado existente desde el almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="fab79-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="fab79-132">Exportación del certificado SSL desde el almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="fab79-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="fab79-133">Carga del certificado SSL en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-133">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="fab79-134">Actualización del certificado SSL en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="fab79-135">Para utilizar un certificado existente en un archivo PFX</span><span class="sxs-lookup"><span data-stu-id="fab79-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="fab79-136">Carga del certificado SSL en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-136">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="fab79-137">Actualización del certificado SSL en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="fab79-138">Configuración del certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-138">To configure client certificates</span></span>
<span data-ttu-id="fab79-139">Se requieren certificados de cliente para autenticar solicitudes al servicio.</span><span class="sxs-lookup"><span data-stu-id="fab79-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="fab79-140">Elija el escenario más aplicable entre los tres que aparecen a continuación y ejecute todos sus pasos:</span><span class="sxs-lookup"><span data-stu-id="fab79-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="fab79-141">Desactivación de los certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="fab79-142">Desactivación de la autenticación basada en certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="fab79-143">Emisión de nuevos certificados de cliente autofirmados</span><span class="sxs-lookup"><span data-stu-id="fab79-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="fab79-144">Creación de una Entidad de certificación autofirmada</span><span class="sxs-lookup"><span data-stu-id="fab79-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="fab79-145">Carga de un certificado de Entidad de certificación en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-145">Upload CA Certificate to Cloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="fab79-146">Actualización de un certificado de Entidad de certificación en un archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="fab79-147">Emisión de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="fab79-148">Creación de archivos PFX para certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="fab79-149">Importación de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="fab79-150">Copia de las huellas digitales de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="fab79-151">Configuración de clientes autorizados en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-151">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="fab79-152">Uso de certificados de cliente existentes</span><span class="sxs-lookup"><span data-stu-id="fab79-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="fab79-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="fab79-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="fab79-154">Carga de un certificado de Entidad de certificación en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="fab79-155">Actualización de un certificado de Entidad de certificación en un archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="fab79-156">Copia de las huellas digitales de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="fab79-157">Configuración de clientes autorizados en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-157">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="fab79-158">Configuración de la comprobación de revocación de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="fab79-159">Direcciones IP permitidas</span><span class="sxs-lookup"><span data-stu-id="fab79-159">Allowed IP addresses</span></span>
<span data-ttu-id="fab79-160">El acceso a los extremos de servicio puede estar limitado a intervalos concretos de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="fab79-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="fab79-161">Configuración del cifrado para el almacén</span><span class="sxs-lookup"><span data-stu-id="fab79-161">To configure encryption for the store</span></span>
<span data-ttu-id="fab79-162">Se requiere un certificado para cifrar las credenciales que se almacenan en el almacén de metadatos.</span><span class="sxs-lookup"><span data-stu-id="fab79-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="fab79-163">Elija el escenario más aplicable entre los tres que aparecen a continuación y ejecute todos sus pasos:</span><span class="sxs-lookup"><span data-stu-id="fab79-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="fab79-164">Use un nuevo certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="fab79-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="fab79-165">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="fab79-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="fab79-166">Crear archivo PFX para certificado de cifrado autofirmado</span><span class="sxs-lookup"><span data-stu-id="fab79-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="fab79-167">Cargar el certificado de cifrado en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-167">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="fab79-168">Actualización del certificado de cifrado en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="fab79-169">Utilizar un certificado existente desde el almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="fab79-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="fab79-170">Exportar el certificado de cifrado del almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="fab79-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="fab79-171">Cargar el certificado de cifrado en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-171">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="fab79-172">Actualización del certificado de cifrado en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="fab79-173">Utilizar un certificado existente de un archivo PFX</span><span class="sxs-lookup"><span data-stu-id="fab79-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="fab79-174">Cargar el certificado de cifrado en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-174">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="fab79-175">Actualización del certificado de cifrado en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a><span data-ttu-id="fab79-176">La configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="fab79-176">The default configuration</span></span>
<span data-ttu-id="fab79-177">La configuración predeterminada deniega todo acceso al extremo HTTP.</span><span class="sxs-lookup"><span data-stu-id="fab79-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="fab79-178">Esta es la configuración recomendada, dado que las solicitudes a estos extremos pueden llevar información delicada, como pueden ser las credenciales de base de datos.</span><span class="sxs-lookup"><span data-stu-id="fab79-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="fab79-179">La configuración predeterminada permite todo acceso al extremo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fab79-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="fab79-180">Esta configuración puede ser aún más restrictiva.</span><span class="sxs-lookup"><span data-stu-id="fab79-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="fab79-181">Cambio de la configuración</span><span class="sxs-lookup"><span data-stu-id="fab79-181">Changing the Configuration</span></span>
<span data-ttu-id="fab79-182">El grupo de reglas de control de acceso que se aplican a un extremo se configuran en la sección **<EndpointAcls>** del **archivo de configuración de servicio**.</span><span class="sxs-lookup"><span data-stu-id="fab79-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="fab79-183">Las reglas de un grupo de control de acceso se configuran en una sección <AccessControl name=""> del archivo de configuración de servicio.</span><span class="sxs-lookup"><span data-stu-id="fab79-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="fab79-184">El formato se explica en la documentación de listas de control de acceso de red.</span><span class="sxs-lookup"><span data-stu-id="fab79-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="fab79-185">Por ejemplo, para permitir únicamente a las direcciones IP del intervalo comprendido entre 100.100.0.0 y 100.100.255.255 el acceso al extremo HTTPS, las reglas se parecerían a esta:</span><span class="sxs-lookup"><span data-stu-id="fab79-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="fab79-186">Prevención de la denegación de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-186">Denial of service prevention</span></span>
<span data-ttu-id="fab79-187">Existen dos mecanismos distintos compatibles para detectar y evitar los ataques de denegación de servicio:</span><span class="sxs-lookup"><span data-stu-id="fab79-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="fab79-188">Restringir la cantidad de solicitudes simultáneas por host remoto (desactivado de manera predeterminada)</span><span class="sxs-lookup"><span data-stu-id="fab79-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="fab79-189">Restringir la velocidad de acceso por host remoto (activado de manera predeterminada)</span><span class="sxs-lookup"><span data-stu-id="fab79-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="fab79-190">Estos mecanismos se basan en las características más documentadas en Seguridad de IP dinámica en IIS.</span><span class="sxs-lookup"><span data-stu-id="fab79-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="fab79-191">Cuando cambie esta configuración, tenga cuidado con los siguientes factores:</span><span class="sxs-lookup"><span data-stu-id="fab79-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="fab79-192">El comportamiento de los servidores proxy y los dispositivos de traducción de direcciones de red sobre la información de host remoto</span><span class="sxs-lookup"><span data-stu-id="fab79-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="fab79-193">Se considera cada solicitud a cualquier recurso en el rol web (por ejemplo, carga de scripts, imágenes, etc.)</span><span class="sxs-lookup"><span data-stu-id="fab79-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="fab79-194">Restricción de la cantidad de acceso simultáneos</span><span class="sxs-lookup"><span data-stu-id="fab79-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="fab79-195">Los ajustes que configuran este comportamiento son:</span><span class="sxs-lookup"><span data-stu-id="fab79-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="fab79-196">Cambie DynamicIpRestrictionDenyByConcurrentRequests a true para habilitar esta protección.</span><span class="sxs-lookup"><span data-stu-id="fab79-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="fab79-197">Restricción de la velocidad del acceso</span><span class="sxs-lookup"><span data-stu-id="fab79-197">Restricting rate of access</span></span>
<span data-ttu-id="fab79-198">Los ajustes que configuran este comportamiento son:</span><span class="sxs-lookup"><span data-stu-id="fab79-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="fab79-199">Configuración de la respuesta a una solicitud denegada</span><span class="sxs-lookup"><span data-stu-id="fab79-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="fab79-200">Los siguientes ajustes configuran la respuesta a una solicitud denegada:</span><span class="sxs-lookup"><span data-stu-id="fab79-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="fab79-201">Consulte la documentación para Seguridad de IP dinámica en IIS para otros valores compatibles.</span><span class="sxs-lookup"><span data-stu-id="fab79-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="fab79-202">Operaciones para configurar certificados de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="fab79-203">Este tema es solo para referencia.</span><span class="sxs-lookup"><span data-stu-id="fab79-203">This topic is for reference only.</span></span> <span data-ttu-id="fab79-204">Siga los pasos de configuración descritos en:</span><span class="sxs-lookup"><span data-stu-id="fab79-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="fab79-205">Configuración del certificado SSL</span><span class="sxs-lookup"><span data-stu-id="fab79-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="fab79-206">Configuración de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="fab79-207">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="fab79-207">Create a self-signed certificate</span></span>
<span data-ttu-id="fab79-208">Ejecute:</span><span class="sxs-lookup"><span data-stu-id="fab79-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="fab79-209">Personalizar:</span><span class="sxs-lookup"><span data-stu-id="fab79-209">To customize:</span></span>

* <span data-ttu-id="fab79-210">-n con la dirección URL de servicio.</span><span class="sxs-lookup"><span data-stu-id="fab79-210">-n with the service URL.</span></span> <span data-ttu-id="fab79-211">Caracteres comodín ("CN=*.cloudapp.net") y nombres alternativos ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") son compatibles.</span><span class="sxs-lookup"><span data-stu-id="fab79-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="fab79-212">-e con la fecha de caducidad del certificado Cree una contraseña segura y especifíquela cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="fab79-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="fab79-213">Creación del archivo PFX para el certificado SSL autofirmado</span><span class="sxs-lookup"><span data-stu-id="fab79-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="fab79-214">Ejecute:</span><span class="sxs-lookup"><span data-stu-id="fab79-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="fab79-215">Escriba la contraseña y, a continuación, exporte el certificado con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="fab79-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="fab79-216">Sí, exportar la clave privada</span><span class="sxs-lookup"><span data-stu-id="fab79-216">Yes, export the private key</span></span>
* <span data-ttu-id="fab79-217">Exportar todas las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="fab79-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="fab79-218">Exportación del certificado SSL desde el almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="fab79-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="fab79-219">Busque el certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-219">Find certificate</span></span>
* <span data-ttu-id="fab79-220">Haga clic en Acciones -> Todas las tareas -> Exportar…</span><span class="sxs-lookup"><span data-stu-id="fab79-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="fab79-221">Exporte el certificado a un archivo .PFX con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="fab79-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="fab79-222">Sí, exportar la clave privada</span><span class="sxs-lookup"><span data-stu-id="fab79-222">Yes, export the private key</span></span>
  * <span data-ttu-id="fab79-223">Incluir todos los certificados en la ruta de certificación si es posible *Exportar todas las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="fab79-223">Include all certificates in the certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="fab79-224">Carga del certificado SSL en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="fab79-225">Cargue el certificado con el archivo .PFX existente o generado con el par de claves SSL:</span><span class="sxs-lookup"><span data-stu-id="fab79-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="fab79-226">Escriba la contraseña para proteger la información de clave privada</span><span class="sxs-lookup"><span data-stu-id="fab79-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="fab79-227">Actualización del certificado SSL en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="fab79-228">Actualice el valor de huella digital de la siguiente configuración en el archivo de configuración de servicio con la huella digital del certificado cargado al servicio en la nube:</span><span class="sxs-lookup"><span data-stu-id="fab79-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="fab79-229">Importación de la Entidad de certificación SSL</span><span class="sxs-lookup"><span data-stu-id="fab79-229">Import SSL certification authority</span></span>
<span data-ttu-id="fab79-230">Siga estos pasos en todas las cuentas/máquinas que se comunicarán con el servicio:</span><span class="sxs-lookup"><span data-stu-id="fab79-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="fab79-231">Haga doble clic en el archivo .CER en el Explorador de Windows</span><span class="sxs-lookup"><span data-stu-id="fab79-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="fab79-232">En el cuadro de diálogo Certificado, haga clic en Instalar certificado...</span><span class="sxs-lookup"><span data-stu-id="fab79-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="fab79-233">Importe el certificado al almacén de Entidades de certificación de raíz de confianza</span><span class="sxs-lookup"><span data-stu-id="fab79-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="fab79-234">Desactivación de la autenticación basada en certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="fab79-235">Solo se admite la autenticación basada en certificado de cliente y deshabilitarla permitirá el acceso público a los extremos del servicio, a menos que existan otros mecanismos (por ejemplo, Red virtual de Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="fab79-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="fab79-236">Cambie esta configuración a falso en el archivo de configuración del servicio para deshabilitar la característica:</span><span class="sxs-lookup"><span data-stu-id="fab79-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="fab79-237">A continuación, copie la misma huella digital del certificado SSL en la configuración del certificado de CA:</span><span class="sxs-lookup"><span data-stu-id="fab79-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="fab79-238">Creación de una Entidad de certificación autofirmada</span><span class="sxs-lookup"><span data-stu-id="fab79-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="fab79-239">Ejecute los siguientes pasos para crear un certificado autofirmado que actúe como Entidad de certificación:</span><span class="sxs-lookup"><span data-stu-id="fab79-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="fab79-240">Para personalizarlo</span><span class="sxs-lookup"><span data-stu-id="fab79-240">To customize it</span></span>

* <span data-ttu-id="fab79-241">-e con la fecha de caducidad de la certificación</span><span class="sxs-lookup"><span data-stu-id="fab79-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="fab79-242">Búsqueda de clave pública de Entidad de certificación</span><span class="sxs-lookup"><span data-stu-id="fab79-242">Find CA public key</span></span>
<span data-ttu-id="fab79-243">Una Entidad de certificación de la confianza del servicio debe haber emitido todos los certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="fab79-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="fab79-244">Encuentre la clave pública para la Entidad de certificación que emitió los certificados de cliente que se van a usar para autenticación a fin de cargarla al servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="fab79-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="fab79-245">Si el archivo con la clave pública no está disponible, expórtelo desde el almacén de certificados:</span><span class="sxs-lookup"><span data-stu-id="fab79-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="fab79-246">Busque el certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-246">Find certificate</span></span>
  * <span data-ttu-id="fab79-247">Busque un certificado de cliente emitido por la misma Entidad de certificación</span><span class="sxs-lookup"><span data-stu-id="fab79-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="fab79-248">Haga doble clic en el certificado.</span><span class="sxs-lookup"><span data-stu-id="fab79-248">Double-click the certificate.</span></span>
* <span data-ttu-id="fab79-249">Seleccione la pestaña Ruta de certificación en el cuadro de diálogo Certificado.</span><span class="sxs-lookup"><span data-stu-id="fab79-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="fab79-250">Haga doble clic en la entrada de CA de la ruta.</span><span class="sxs-lookup"><span data-stu-id="fab79-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="fab79-251">Tome notas de las propiedades del certificado.</span><span class="sxs-lookup"><span data-stu-id="fab79-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="fab79-252">Cierre el cuadro de diálogo **Certificado** .</span><span class="sxs-lookup"><span data-stu-id="fab79-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="fab79-253">Busque el certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-253">Find certificate</span></span>
  * <span data-ttu-id="fab79-254">Busque la CA anotada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fab79-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="fab79-255">Haga clic en Acciones -> Todas las tareas -> Exportar…</span><span class="sxs-lookup"><span data-stu-id="fab79-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="fab79-256">Exporte el certificado a un archivo .CER con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="fab79-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="fab79-257">**No, no exportar la clave privada**</span><span class="sxs-lookup"><span data-stu-id="fab79-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="fab79-258">Incluir todos los certificados en la ruta de certificación si es posible.</span><span class="sxs-lookup"><span data-stu-id="fab79-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="fab79-259">Exportar todas las propiedades extendidas.</span><span class="sxs-lookup"><span data-stu-id="fab79-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="fab79-260">Carga de un certificado de Entidad de certificación en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="fab79-261">Cargue el certificado con el archivo .CER existente o generado con la clave pública de CA.</span><span class="sxs-lookup"><span data-stu-id="fab79-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="fab79-262">Actualización de un certificado de Entidad de certificación en un archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="fab79-263">Actualice el valor de huella digital de la siguiente configuración en el archivo de configuración de servicio con la huella digital del certificado cargado al servicio en la nube:</span><span class="sxs-lookup"><span data-stu-id="fab79-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="fab79-264">Actualice el valor de la siguiente configuración con la misma huella digital:</span><span class="sxs-lookup"><span data-stu-id="fab79-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="fab79-265">Emisión de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-265">Issue client certificates</span></span>
<span data-ttu-id="fab79-266">Cada persona autorizada a tener acceso al servicio debe tener un certificado de cliente emitido para su uso exclusivo y debe elegir su propia contraseña segura para proteger su clave privada.</span><span class="sxs-lookup"><span data-stu-id="fab79-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="fab79-267">Los siguientes pasos se deben ejecutar en la misma máquina donde se generó y almacenó el certificado de CA autofirmado:</span><span class="sxs-lookup"><span data-stu-id="fab79-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="fab79-268">Personalización:</span><span class="sxs-lookup"><span data-stu-id="fab79-268">Customizing:</span></span>

* <span data-ttu-id="fab79-269">-n con un identificador para el cliente que se autenticará con este certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="fab79-270">-e con la fecha de caducidad del certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="fab79-271">MyID.pvk y MyID.cer con nombres de archivo únicos para este certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="fab79-272">Este comando solicitará que se cree una contraseña y se use una vez.</span><span class="sxs-lookup"><span data-stu-id="fab79-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="fab79-273">Utilice una contraseña segura.</span><span class="sxs-lookup"><span data-stu-id="fab79-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="fab79-274">Creación de archivos PFX para certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="fab79-275">Para cada certificado de cliente generado, ejecute:</span><span class="sxs-lookup"><span data-stu-id="fab79-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="fab79-276">Personalización:</span><span class="sxs-lookup"><span data-stu-id="fab79-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="fab79-277">Escriba la contraseña y, a continuación, exporte el certificado con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="fab79-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="fab79-278">Sí, exportar la clave privada</span><span class="sxs-lookup"><span data-stu-id="fab79-278">Yes, export the private key</span></span>
* <span data-ttu-id="fab79-279">Exportar todas las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="fab79-279">Export all extended properties</span></span>
* <span data-ttu-id="fab79-280">La persona para quien se emite este certificado debe elegir la contraseña de exportación</span><span class="sxs-lookup"><span data-stu-id="fab79-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="fab79-281">Importación de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-281">Import client certificate</span></span>
<span data-ttu-id="fab79-282">Cada persona para quien se ha emitido un certificado de cliente debe importar el par de claves en las máquinas que usará para comunicarse con el servicio:</span><span class="sxs-lookup"><span data-stu-id="fab79-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="fab79-283">Haga doble clic en el archivo .PFX en el Explorador de Windows</span><span class="sxs-lookup"><span data-stu-id="fab79-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="fab79-284">Importe el certificado al almacén personal con al menos esta opción:</span><span class="sxs-lookup"><span data-stu-id="fab79-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="fab79-285">Incluir todas las propiedades extendidas comprobadas</span><span class="sxs-lookup"><span data-stu-id="fab79-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="fab79-286">Copia de las huellas digitales de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="fab79-287">Cada usuario para el que se ha emitido un certificado de cliente debe seguir estos pasos para obtener la huella digital de su certificado, el que se agregará al archivo de configuración de servicio:</span><span class="sxs-lookup"><span data-stu-id="fab79-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="fab79-288">Ejecute certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="fab79-288">Run certmgr.exe</span></span>
* <span data-ttu-id="fab79-289">Seleccione la pestaña Personal</span><span class="sxs-lookup"><span data-stu-id="fab79-289">Select the Personal tab</span></span>
* <span data-ttu-id="fab79-290">Haga doble clic en el certificado de cliente que se usará para la autenticación</span><span class="sxs-lookup"><span data-stu-id="fab79-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="fab79-291">En el cuadro de diálogo Certificado que se abre, seleccione la pestaña Detalles</span><span class="sxs-lookup"><span data-stu-id="fab79-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="fab79-292">Asegúrese de que Mostrar esté mostrando Todo</span><span class="sxs-lookup"><span data-stu-id="fab79-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="fab79-293">Seleccione el campo denominado Huella digital en la lista</span><span class="sxs-lookup"><span data-stu-id="fab79-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="fab79-294">Copie el valor de la huella digital ** Elimine los caracteres Unicode no visibles delante del primer dígito ** Elimine todos los espacios</span><span class="sxs-lookup"><span data-stu-id="fab79-294">Copy the value of the thumbprint ** Delete non-visible Unicode characters in front of the first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="fab79-295">Configuración de clientes autorizados en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="fab79-296">Actualice el valor de los siguientes ajustes en el archivo de configuración de servicio con una lista delimitada por comas de las huellas digitales de los certificados de cliente que tienen permitido el acceso al servicio:</span><span class="sxs-lookup"><span data-stu-id="fab79-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="fab79-297">Configuración de la comprobación de revocación de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="fab79-298">La configuración predeterminada no se comprueba con la Entidad de certificación para el estado de revocación de certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="fab79-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="fab79-299">Para activar las comprobaciones, si la Entidad de certificación que emitió los certificados de cliente admite dichas comprobaciones, cambie la siguiente configuración por uno de los valores definidos en la enumeración X509RevocationMode:</span><span class="sxs-lookup"><span data-stu-id="fab79-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="fab79-300">Crear archivo PFX para certificados de cifrado autofirmados</span><span class="sxs-lookup"><span data-stu-id="fab79-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="fab79-301">Para un certificado de cifrado, ejecute:</span><span class="sxs-lookup"><span data-stu-id="fab79-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="fab79-302">Personalización:</span><span class="sxs-lookup"><span data-stu-id="fab79-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="fab79-303">Escriba la contraseña y, a continuación, exporte el certificado con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="fab79-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="fab79-304">Sí, exportar la clave privada</span><span class="sxs-lookup"><span data-stu-id="fab79-304">Yes, export the private key</span></span>
* <span data-ttu-id="fab79-305">Exportar todas las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="fab79-305">Export all extended properties</span></span>
* <span data-ttu-id="fab79-306">Necesitará la contraseña al cargar el certificado en el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="fab79-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="fab79-307">Exportar el certificado de cifrado del almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="fab79-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="fab79-308">Busque el certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-308">Find certificate</span></span>
* <span data-ttu-id="fab79-309">Haga clic en Acciones -> Todas las tareas -> Exportar…</span><span class="sxs-lookup"><span data-stu-id="fab79-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="fab79-310">Exporte el certificado a un archivo .PFX con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="fab79-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="fab79-311">Sí, exportar la clave privada</span><span class="sxs-lookup"><span data-stu-id="fab79-311">Yes, export the private key</span></span>
  * <span data-ttu-id="fab79-312">Incluir todos los certificados en la ruta de certificación si es posible</span><span class="sxs-lookup"><span data-stu-id="fab79-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="fab79-313">Exportar todas las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="fab79-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="fab79-314">Cargar el certificado de cifrado en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fab79-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="fab79-315">Cargue el certificado con el archivo .PFX existente o generado con el par de claves de cifrado:</span><span class="sxs-lookup"><span data-stu-id="fab79-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="fab79-316">Escriba la contraseña para proteger la información de clave privada</span><span class="sxs-lookup"><span data-stu-id="fab79-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="fab79-317">Actualización del certificado de cifrado en el archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="fab79-318">Actualice el valor de huella digital de la siguiente configuración en el archivo de configuración de servicio con la huella digital del certificado cargado al servicio en la nube:</span><span class="sxs-lookup"><span data-stu-id="fab79-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="fab79-319">Operaciones comunes de certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-319">Common certificate operations</span></span>
* <span data-ttu-id="fab79-320">Configuración del certificado SSL</span><span class="sxs-lookup"><span data-stu-id="fab79-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="fab79-321">Configuración de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="fab79-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="fab79-322">Busque el certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-322">Find certificate</span></span>
<span data-ttu-id="fab79-323">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fab79-323">Follow these steps:</span></span>

1. <span data-ttu-id="fab79-324">Ejecute mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="fab79-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="fab79-325">Archivo -> Agregar o quitar complemento…</span><span class="sxs-lookup"><span data-stu-id="fab79-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="fab79-326">Seleccione **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="fab79-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="fab79-327">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fab79-327">Click **Add**.</span></span>
5. <span data-ttu-id="fab79-328">Elija la ubicación del almacén de certificados.</span><span class="sxs-lookup"><span data-stu-id="fab79-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="fab79-329">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="fab79-329">Click **Finish**.</span></span>
7. <span data-ttu-id="fab79-330">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fab79-330">Click **OK**.</span></span>
8. <span data-ttu-id="fab79-331">Expanda **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="fab79-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="fab79-332">Expanda el nodo del almacén de certificados.</span><span class="sxs-lookup"><span data-stu-id="fab79-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="fab79-333">Expanda el nodo secundario Certificado.</span><span class="sxs-lookup"><span data-stu-id="fab79-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="fab79-334">Seleccione un certificado en la lista.</span><span class="sxs-lookup"><span data-stu-id="fab79-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="fab79-335">Exportación de certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-335">Export certificate</span></span>
<span data-ttu-id="fab79-336">En el **asistente para exportar certificados**:</span><span class="sxs-lookup"><span data-stu-id="fab79-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="fab79-337">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="fab79-337">Click **Next**.</span></span>
2. <span data-ttu-id="fab79-338">Seleccione **Sí** y **Exportar la clave privada**.</span><span class="sxs-lookup"><span data-stu-id="fab79-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="fab79-339">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="fab79-339">Click **Next**.</span></span>
4. <span data-ttu-id="fab79-340">Seleccione el formato deseado del archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="fab79-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="fab79-341">Marque las opciones deseadas.</span><span class="sxs-lookup"><span data-stu-id="fab79-341">Check the desired options.</span></span>
6. <span data-ttu-id="fab79-342">Marque **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fab79-342">Check **Password**.</span></span>
7. <span data-ttu-id="fab79-343">Escriba una contraseña segura y confírmela.</span><span class="sxs-lookup"><span data-stu-id="fab79-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="fab79-344">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="fab79-344">Click **Next**.</span></span>
9. <span data-ttu-id="fab79-345">Escriba o busque un nombre de archivo donde almacenar el certificado (use una extensión .PFX).</span><span class="sxs-lookup"><span data-stu-id="fab79-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="fab79-346">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="fab79-346">Click **Next**.</span></span>
11. <span data-ttu-id="fab79-347">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="fab79-347">Click **Finish**.</span></span>
12. <span data-ttu-id="fab79-348">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fab79-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="fab79-349">Importación de certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-349">Import certificate</span></span>
<span data-ttu-id="fab79-350">En el asistente para importar certificados:</span><span class="sxs-lookup"><span data-stu-id="fab79-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="fab79-351">Seleccione la ubicación del almacén.</span><span class="sxs-lookup"><span data-stu-id="fab79-351">Select the store location.</span></span>
   
   * <span data-ttu-id="fab79-352">Seleccione **Usuario actual** , si solo los procesos en ejecución bajo el usuario actual tendrán acceso al servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="fab79-353">Seleccione **Máquina local** , si otros procesos de este equipo tendrán acceso al servicio</span><span class="sxs-lookup"><span data-stu-id="fab79-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="fab79-354">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="fab79-354">Click **Next**.</span></span>
3. <span data-ttu-id="fab79-355">Si se importa desde un archivo, confirme la ruta del archivo.</span><span class="sxs-lookup"><span data-stu-id="fab79-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="fab79-356">Si se importa un archivo .PFX:</span><span class="sxs-lookup"><span data-stu-id="fab79-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="fab79-357">Escriba la contraseña para proteger la clave privada</span><span class="sxs-lookup"><span data-stu-id="fab79-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="fab79-358">Seleccione las opciones de importación</span><span class="sxs-lookup"><span data-stu-id="fab79-358">Select import options</span></span>
5. <span data-ttu-id="fab79-359">Seleccione "Colocar" certificados en el siguiente almacén</span><span class="sxs-lookup"><span data-stu-id="fab79-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="fab79-360">Haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="fab79-360">Click **Browse**.</span></span>
7. <span data-ttu-id="fab79-361">Seleccione el almacén deseado.</span><span class="sxs-lookup"><span data-stu-id="fab79-361">Select the desired store.</span></span>
8. <span data-ttu-id="fab79-362">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="fab79-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="fab79-363">Si se eligió el almacén de Entidad de certificación raíz de confianza, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="fab79-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="fab79-364">Haga clic en **Aceptar** en todas las ventanas de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fab79-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="fab79-365">Carga del certificado</span><span class="sxs-lookup"><span data-stu-id="fab79-365">Upload certificate</span></span>
<span data-ttu-id="fab79-366">En el [Portal de Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="fab79-366">In the [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="fab79-367">Seleccione **Servicios en la nube**.</span><span class="sxs-lookup"><span data-stu-id="fab79-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="fab79-368">Seleccione el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="fab79-368">Select the cloud service.</span></span>
3. <span data-ttu-id="fab79-369">Haga clic en **Certificados**en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="fab79-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="fab79-370">En la barra inferior, haga clic en **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="fab79-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="fab79-371">Seleccione el archivo de certificado.</span><span class="sxs-lookup"><span data-stu-id="fab79-371">Select the certificate file.</span></span>
6. <span data-ttu-id="fab79-372">Si es un archivo .PFX, escriba la contraseña de la clave privada.</span><span class="sxs-lookup"><span data-stu-id="fab79-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="fab79-373">Una vez realizado, copie la huella digital del certificado desde la entrada nueva en la lista.</span><span class="sxs-lookup"><span data-stu-id="fab79-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="fab79-374">Otras consideraciones de seguridad</span><span class="sxs-lookup"><span data-stu-id="fab79-374">Other security considerations</span></span>
<span data-ttu-id="fab79-375">La configuración SSL descrita en este documento cifra la comunicación entre el servicio y sus clientes cuando se usa el extremo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fab79-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="fab79-376">Esto es importante, porque las credenciales para el acceso a la base de datos y potencialmente a otra información confidencial están contenidas en la comunicación.</span><span class="sxs-lookup"><span data-stu-id="fab79-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="fab79-377">Sin embargo, tenga en cuenta que el servicio persiste en el estado interno, incluidas credenciales, en sus tablas internas en la base de datos SQL de Microsoft Azure que ha proporcionado para el almacenamiento de metadatos en la suscripción de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fab79-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="fab79-378">Esa base de datos se definió como parte de los siguientes ajustes en el archivo de configuración de servicio (archivo .CSCFG):</span><span class="sxs-lookup"><span data-stu-id="fab79-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="fab79-379">Las credenciales almacenadas en esta base de datos están cifradas.</span><span class="sxs-lookup"><span data-stu-id="fab79-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="fab79-380">Sin embargo, como práctica recomendada, asegúrese de que los roles de web y de trabajo de sus implementaciones de servicio se mantienen actualizados y seguros, a medida que ambos tienen acceso a la base de datos de metadatos y el certificado usado para el cifrado y descifrado de credenciales almacenadas.</span><span class="sxs-lookup"><span data-stu-id="fab79-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

