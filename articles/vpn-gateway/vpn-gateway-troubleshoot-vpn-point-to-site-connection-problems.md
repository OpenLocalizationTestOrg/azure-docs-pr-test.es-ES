---
title: "Solución de problemas de conexión de punto a sitio de Azure | Microsoft Docs"
description: "Obtenga información sobre cómo solucionar problemas de conexión de punto a sitio."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: de37c8ffd47a2b8e201d18e3a20b5325d528ad59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="95b5f-103">Solución de problemas: conexión de punto a sitio de Azure</span><span class="sxs-lookup"><span data-stu-id="95b5f-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="95b5f-104">En este artículo se enumeran problemas comunes de conexión de punto a sitio que puede experimentar.</span><span class="sxs-lookup"><span data-stu-id="95b5f-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="95b5f-105">También se tratan las posibles causas de estos problemas y sus soluciones.</span><span class="sxs-lookup"><span data-stu-id="95b5f-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="95b5f-106">Error de cliente de VPN: no se encontró un certificado</span><span class="sxs-lookup"><span data-stu-id="95b5f-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="95b5f-107">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-107">Symptom</span></span>

<span data-ttu-id="95b5f-108">Al intentar conectar a una red virtual de Azure mediante el cliente de VPN, aparece el mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="95b5f-108">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="95b5f-109">**No se encuentra un certificado que se puede usar con este protocolo de autenticación extendido. (Error 798)**</span><span class="sxs-lookup"><span data-stu-id="95b5f-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="95b5f-110">Causa</span><span class="sxs-lookup"><span data-stu-id="95b5f-110">Cause</span></span>

<span data-ttu-id="95b5f-111">Este problema se produce si el certificado de cliente no está en **Certificados - Usuario actual\Personal\Certificados**.</span><span class="sxs-lookup"><span data-stu-id="95b5f-111">This problem occurs if the client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="95b5f-112">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-112">Solution</span></span>

<span data-ttu-id="95b5f-113">Asegúrese de que el certificado de cliente está instalado en la siguiente ubicación del almacén de certificados (Certmgr.msc):</span><span class="sxs-lookup"><span data-stu-id="95b5f-113">Make sure that the client certificate is installed in the following location of the Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="95b5f-114">**Certificados - Usuario actual\Personal\Certificados**</span><span class="sxs-lookup"><span data-stu-id="95b5f-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="95b5f-115">Para más información sobre cómo instalar el certificado de cliente, consulte [Generación y exportación de certificados para conexiones de punto a sitio](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="95b5f-115">For more information about how to install the client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="95b5f-116">Al importar el certificado de cliente, no seleccione la opción **Habilitar la protección de clave privada de alta seguridad**.</span><span class="sxs-lookup"><span data-stu-id="95b5f-116">When you import the client certificate, do not select the **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-the-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="95b5f-117">Error de cliente de VPN: no se esperaba el mensaje recibido o tiene un formato incorrecto</span><span class="sxs-lookup"><span data-stu-id="95b5f-117">VPN client error: The message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="95b5f-118">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-118">Symptom</span></span>

<span data-ttu-id="95b5f-119">Al intentar conectar a una red virtual de Azure mediante el cliente de VPN, aparece el mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="95b5f-119">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="95b5f-120">**Mensaje recibido inesperado o con formato incorrecto. (Error 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="95b5f-120">**The message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="95b5f-121">Causa</span><span class="sxs-lookup"><span data-stu-id="95b5f-121">Cause</span></span>

<span data-ttu-id="95b5f-122">Este problema se produce si la clave pública del certificado raíz no se carga a la puerta de enlace VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="95b5f-122">This problem occurs if the root certificate public key is not uploaded into the Azure VPN gateway.</span></span> <span data-ttu-id="95b5f-123">También se puede producir si la clave está dañada o expiró.</span><span class="sxs-lookup"><span data-stu-id="95b5f-123">It can also occur if the key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="95b5f-124">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-124">Solution</span></span>

<span data-ttu-id="95b5f-125">Para resolver este problema, compruebe el estado del certificado raíz en Azure Portal para ver si se revocó.</span><span class="sxs-lookup"><span data-stu-id="95b5f-125">To resolve this problem, check the status of the root certificate in the Azure portal to see whether it was revoked.</span></span> <span data-ttu-id="95b5f-126">Si no se ha revocado, pruebe a eliminar el certificado raíz y a volver a cargarlo.</span><span class="sxs-lookup"><span data-stu-id="95b5f-126">If it is not revoked, try to delete the root certificate and reupload.</span></span> <span data-ttu-id="95b5f-127">Para más información, vea [Crear certificados](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="95b5f-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="95b5f-128">Error de cliente de VPN: una cadena de certificados se ha procesado pero ha finalizado</span><span class="sxs-lookup"><span data-stu-id="95b5f-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="95b5f-129">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-129">Symptom</span></span> 

<span data-ttu-id="95b5f-130">Al intentar conectar a una red virtual de Azure mediante el cliente de VPN, aparece el mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="95b5f-130">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="95b5f-131">**Se ha procesado una cadena de certificados, pero termina en un certificado raíz en el que el proveedor de confianza no confía**</span><span class="sxs-lookup"><span data-stu-id="95b5f-131">**A certificate chain processed but terminated in a root certificate which is not trusted by the trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="95b5f-132">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-132">Solution</span></span>

1. <span data-ttu-id="95b5f-133">Asegúrese de que los certificados siguientes están en la ubicación correcta:</span><span class="sxs-lookup"><span data-stu-id="95b5f-133">Make sure that the following certificates are in the correct location:</span></span>

    | <span data-ttu-id="95b5f-134">Certificate</span><span class="sxs-lookup"><span data-stu-id="95b5f-134">Certificate</span></span> | <span data-ttu-id="95b5f-135">La ubicación</span><span class="sxs-lookup"><span data-stu-id="95b5f-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="95b5f-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="95b5f-136">AzureClient.pfx</span></span>  | <span data-ttu-id="95b5f-137">Usuario actual\Personal\Certificados</span><span class="sxs-lookup"><span data-stu-id="95b5f-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="95b5f-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="95b5f-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="95b5f-139">Usuario actual\Entidades de certificación raíz de confianza</span><span class="sxs-lookup"><span data-stu-id="95b5f-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="95b5f-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="95b5f-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="95b5f-141">Equipo local\Entidades de certificación raíz de confianza</span><span class="sxs-lookup"><span data-stu-id="95b5f-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="95b5f-142">Si los certificados ya están en la ubicación, pruebe a eliminarlos y a volver a instalarlos.</span><span class="sxs-lookup"><span data-stu-id="95b5f-142">If the certificates are already in the location, try to delete the certificates and reinstall them.</span></span> <span data-ttu-id="95b5f-143">El certificado **azuregateway-*GUID*.cloudapp.net** se encuentra en el paquete de configuración del cliente de VPN descargado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="95b5f-143">The **azuregateway-*GUID*.cloudapp.net** certificate is in the VPN client configuration package that you downloaded from the Azure portal.</span></span> <span data-ttu-id="95b5f-144">Puede usar archivadores de archivos para extraer los archivos del paquete.</span><span class="sxs-lookup"><span data-stu-id="95b5f-144">You can use file archivers to extract the files from the package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="95b5f-145">Error en la descarga del archivo. No se ha especificado el URI de destino</span><span class="sxs-lookup"><span data-stu-id="95b5f-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="95b5f-146">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-146">Symptom</span></span>

<span data-ttu-id="95b5f-147">Aparece el siguiente mensaje de error:</span><span class="sxs-lookup"><span data-stu-id="95b5f-147">You receive the following error message:</span></span>

<span data-ttu-id="95b5f-148">**Error en la descarga del archivo. No se ha especificado el URI de destino.**</span><span class="sxs-lookup"><span data-stu-id="95b5f-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="95b5f-149">Causa</span><span class="sxs-lookup"><span data-stu-id="95b5f-149">Cause</span></span> 

<span data-ttu-id="95b5f-150">Este problema se produce debido a un tipo de puerta de enlace incorrecto.</span><span class="sxs-lookup"><span data-stu-id="95b5f-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="95b5f-151">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-151">Solution</span></span>

<span data-ttu-id="95b5f-152">El tipo de puerta de enlace de la VPN debe ser **VPN** y el tipo de VPN **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="95b5f-152">The VPN gateway type must be **VPN**, and the VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="95b5f-153">Error de cliente de VPN: error de script personalizado de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="95b5f-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="95b5f-154">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-154">Symptom</span></span>

<span data-ttu-id="95b5f-155">Al intentar conectar a una red virtual de Azure mediante el cliente de VPN, aparece el mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="95b5f-155">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="95b5f-156">**Error de script personalizado (para actualizar la tabla de enrutamiento). (Error 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="95b5f-156">**Custom script (to update your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="95b5f-157">Causa</span><span class="sxs-lookup"><span data-stu-id="95b5f-157">Cause</span></span>

<span data-ttu-id="95b5f-158">Este problema puede producirse si está intentando abrir la conexión VPN de sitio a punto mediante un acceso directo.</span><span class="sxs-lookup"><span data-stu-id="95b5f-158">This problem might occur if you are trying to open the site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="95b5f-159">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-159">Solution</span></span> 

<span data-ttu-id="95b5f-160">Abra el paquete VPN directamente en lugar de hacerlo desde el acceso directo.</span><span class="sxs-lookup"><span data-stu-id="95b5f-160">Open the VPN package directly instead of opening it from the shortcut.</span></span>

## <a name="cannot-install-the-vpn-client"></a><span data-ttu-id="95b5f-161">No se puede instalar el cliente de VPN</span><span class="sxs-lookup"><span data-stu-id="95b5f-161">Cannot install the VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="95b5f-162">Causa</span><span class="sxs-lookup"><span data-stu-id="95b5f-162">Cause</span></span> 

<span data-ttu-id="95b5f-163">Es necesario que un certificado adicional confíe en la puerta de enlace de la VPN de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="95b5f-163">An additional certificate is required to trust the VPN gateway for your virtual network.</span></span> <span data-ttu-id="95b5f-164">El certificado está incluido en el paquete de configuración del cliente de VPN que se genera desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="95b5f-164">The certificate is included in the VPN client configuration package that is generated from the Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="95b5f-165">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-165">Solution</span></span>

<span data-ttu-id="95b5f-166">Extraiga el paquete de configuración del cliente de VPN y busque el archivo .cer.</span><span class="sxs-lookup"><span data-stu-id="95b5f-166">Extract the VPN client configuration package, and find the .cer file.</span></span> <span data-ttu-id="95b5f-167">Para instalar el certificado, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="95b5f-167">To install the certificate, follow these steps:</span></span>

1. <span data-ttu-id="95b5f-168">Abra mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="95b5f-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="95b5f-169">Agregue el complemento **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="95b5f-169">Add the **Certificates** snap-in.</span></span>
3. <span data-ttu-id="95b5f-170">Seleccione la cuenta **Equipo** del equipo local.</span><span class="sxs-lookup"><span data-stu-id="95b5f-170">Select the **Computer** account for the local computer.</span></span>
4. <span data-ttu-id="95b5f-171">Haga clic con el botón derecho en el nodo **Entidades de certificación raíz de confianza**.</span><span class="sxs-lookup"><span data-stu-id="95b5f-171">Right-click the **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="95b5f-172">Haga clic en **All-Task** > **Import** (Importar) y vaya al archivo .cer que extrajo del paquete de configuración del cliente de VPN.</span><span class="sxs-lookup"><span data-stu-id="95b5f-172">Click **All-Task** > **Import**, and browse to the .cer file you extracted from the VPN client configuration package.</span></span>
5. <span data-ttu-id="95b5f-173">Reinicie el equipo.</span><span class="sxs-lookup"><span data-stu-id="95b5f-173">Restart the computer.</span></span> 
6. <span data-ttu-id="95b5f-174">Intente instalar el cliente de VPN.</span><span class="sxs-lookup"><span data-stu-id="95b5f-174">Try to install the VPN client.</span></span>

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-data-is-invalid"></a><span data-ttu-id="95b5f-175">Error de Azure Portal: error al guardar la puerta de enlace de la VPN y los datos no son válidos</span><span class="sxs-lookup"><span data-stu-id="95b5f-175">Azure portal error: Failed to save the VPN gateway, and the data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="95b5f-176">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-176">Symptom</span></span>

<span data-ttu-id="95b5f-177">Al intentar guardar los cambios de la puerta de enlace de la VPN en Azure Portal, aparece el mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="95b5f-177">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span>

<span data-ttu-id="95b5f-178">**Error al guardar la puerta de enlace de red &lt;*nombre de puerta de enlace*&gt;.</span><span class="sxs-lookup"><span data-stu-id="95b5f-178">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="95b5f-179">Los datos del certificado &lt;*identificador de certificado*&gt; no son válidos.**</span><span class="sxs-lookup"><span data-stu-id="95b5f-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="95b5f-180">Causa</span><span class="sxs-lookup"><span data-stu-id="95b5f-180">Cause</span></span> 

<span data-ttu-id="95b5f-181">Este problema puede producirse si la clave pública del certificado raíz que se ha cargado contiene un carácter no válido, por ejemplo, un espacio.</span><span class="sxs-lookup"><span data-stu-id="95b5f-181">This problem might occur if the root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="95b5f-182">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-182">Solution</span></span>

<span data-ttu-id="95b5f-183">Asegúrese de que los datos del certificado no contienen caracteres no válidos como saltos de línea (retornos de carro).</span><span class="sxs-lookup"><span data-stu-id="95b5f-183">Make sure that the data in the certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="95b5f-184">El valor completo debe estar en una línea larga.</span><span class="sxs-lookup"><span data-stu-id="95b5f-184">The entire value should be one long line.</span></span> <span data-ttu-id="95b5f-185">El siguiente texto es un ejemplo del certificado:</span><span class="sxs-lookup"><span data-stu-id="95b5f-185">The following text is a sample of the certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-resource-name-is-invalid"></a><span data-ttu-id="95b5f-186">Error de Azure Portal: error al guardar la puerta de enlace de la VPN y el nombre del recurso no es válido</span><span class="sxs-lookup"><span data-stu-id="95b5f-186">Azure portal error: Failed to save the VPN gateway, and the resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="95b5f-187">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-187">Symptom</span></span>

<span data-ttu-id="95b5f-188">Al intentar guardar los cambios de la puerta de enlace de la VPN en Azure Portal, aparece el mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="95b5f-188">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span> 

<span data-ttu-id="95b5f-189">**Error al guardar la puerta de enlace de red &lt;*nombre de puerta de enlace*&gt;.</span><span class="sxs-lookup"><span data-stu-id="95b5f-189">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="95b5f-190">El nombre del recurso &lt;*nombre del certificado que intenta cargar*&gt; no es válido**.</span><span class="sxs-lookup"><span data-stu-id="95b5f-190">Resource name &lt;*certificate name you try to upload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="95b5f-191">Causa</span><span class="sxs-lookup"><span data-stu-id="95b5f-191">Cause</span></span>

<span data-ttu-id="95b5f-192">Este problema se produce porque el nombre del certificado contiene un carácter no válido, como un espacio.</span><span class="sxs-lookup"><span data-stu-id="95b5f-192">This problem occurs because the name of the certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="95b5f-193">Error de Azure Portal: error de descarga de archivo de paquete de VPN 503</span><span class="sxs-lookup"><span data-stu-id="95b5f-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="95b5f-194">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-194">Symptom</span></span>

<span data-ttu-id="95b5f-195">Al intentar descargar el paquete de configuración del cliente de VPN, aparece el mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="95b5f-195">When you try to download the VPN client configuration package, you receive the following error message:</span></span>

<span data-ttu-id="95b5f-196">**No se pudo descargar el archivo. Detalles del error: error 503. El servidor está ocupado.**</span><span class="sxs-lookup"><span data-stu-id="95b5f-196">**Failed to download the file. Error details: error 503. The server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="95b5f-197">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-197">Solution</span></span>

<span data-ttu-id="95b5f-198">Este error puede deberse a un problema de red temporal.</span><span class="sxs-lookup"><span data-stu-id="95b5f-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="95b5f-199">Vuelva a intentar descargar el paquete VPN pasados unos minutos.</span><span class="sxs-lookup"><span data-stu-id="95b5f-199">Try to download the VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-to-connect"></a><span data-ttu-id="95b5f-200">Actualización de puerta de enlace de la VPN de Azure: todos los clientes de punto a sitio no se pueden conectar</span><span class="sxs-lookup"><span data-stu-id="95b5f-200">Azure VPN Gateway upgrade: All P2S clients are unable to connect</span></span>

### <a name="cause"></a><span data-ttu-id="95b5f-201">Causa</span><span class="sxs-lookup"><span data-stu-id="95b5f-201">Cause</span></span>

<span data-ttu-id="95b5f-202">Si el certificado cubre más del 50 por ciento durante su vigencia, se deshace.</span><span class="sxs-lookup"><span data-stu-id="95b5f-202">If the certificate is more than 50 percent through its lifetime, the certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="95b5f-203">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-203">Solution</span></span>

<span data-ttu-id="95b5f-204">Para resolver este problema, cree y redistribuya los nuevos certificados a los clientes de VPN.</span><span class="sxs-lookup"><span data-stu-id="95b5f-204">To resolve this problem, create and redistribute new certificates to the VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="95b5f-205">Demasiados clientes de VPN conectados a la vez</span><span class="sxs-lookup"><span data-stu-id="95b5f-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="95b5f-206">Para cada puerta de enlace de la VPN, el número máximo de conexiones permitidas es 128.</span><span class="sxs-lookup"><span data-stu-id="95b5f-206">For each VPN gateway, the maximum number of allowable connections is 128.</span></span> <span data-ttu-id="95b5f-207">Puede ver el número total de clientes conectados en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="95b5f-207">You can see the total number of connected clients in the Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-to-the-route-table"></a><span data-ttu-id="95b5f-208">La VPN de punto a sitio agrega de forma incorrecta una ruta para 10.0.0.0/8 a la tabla de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="95b5f-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 to the route table</span></span>

### <a name="symptom"></a><span data-ttu-id="95b5f-209">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-209">Symptom</span></span>

<span data-ttu-id="95b5f-210">Al marcar la conexión VPN en el cliente de punto a sitio, el cliente de VPN no debe agregar una ruta hacia la red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="95b5f-210">When you dial the VPN connection on the point-to-site client, the VPN client should add a route toward the Azure virtual network.</span></span> <span data-ttu-id="95b5f-211">La aplicación auxiliar de IP debe agregar una ruta para la subred de los clientes de VPN.</span><span class="sxs-lookup"><span data-stu-id="95b5f-211">The IP helper service should add a route for the subnet of the VPN clients.</span></span> 

<span data-ttu-id="95b5f-212">El intervalo de cliente de VPN pertenece a una subred más pequeña de 10.0.0.0/8, como 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="95b5f-212">The VPN client range belongs to a smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="95b5f-213">En lugar de una ruta para 10.0.12.0/24, se agrega una ruta para 10.0.0.0/8 con una prioridad más alta.</span><span class="sxs-lookup"><span data-stu-id="95b5f-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="95b5f-214">Esta ruta incorrecta interrumpe la conectividad con otras redes locales que pueden pertenecer a otra subred del intervalo 10.0.0.0/8, por ejemplo, 10.50.0.0/24, que no tienen una ruta concreta definida.</span><span class="sxs-lookup"><span data-stu-id="95b5f-214">This incorrect route breaks connectivity with other on-premises networks that might belong to another subnet within the 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="95b5f-215">Causa</span><span class="sxs-lookup"><span data-stu-id="95b5f-215">Cause</span></span>

<span data-ttu-id="95b5f-216">Este comportamiento es así por diseño para los clientes Windows.</span><span class="sxs-lookup"><span data-stu-id="95b5f-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="95b5f-217">Cuando el cliente usa el protocolo PPP IPCP, obtiene la dirección IP de la interfaz de túnel del servidor (la puerta de enlace de la VPN en este caso).</span><span class="sxs-lookup"><span data-stu-id="95b5f-217">When the client uses the PPP IPCP protocol, it obtains the IP address for the tunnel interface from the server (the VPN gateway in this case).</span></span> <span data-ttu-id="95b5f-218">Pero debido a una limitación del protocolo, el cliente no tiene la máscara de subred.</span><span class="sxs-lookup"><span data-stu-id="95b5f-218">However, because of a limitation in the protocol, the client does not have the subnet mask.</span></span> <span data-ttu-id="95b5f-219">Dado que no hay ninguna otra manera de obtenerla, el cliente intenta adivinar la máscara de subred en función de la clase de la dirección IP de la interfaz de túnel.</span><span class="sxs-lookup"><span data-stu-id="95b5f-219">Because there is no other way to get it, the client tries to guess the subnet mask based on the class of the tunnel interface IP address.</span></span> 

<span data-ttu-id="95b5f-220">Por lo tanto, se agrega una ruta en función de la siguiente asignación estática:</span><span class="sxs-lookup"><span data-stu-id="95b5f-220">Therefore, a route is added based on the following static mapping:</span></span> 

<span data-ttu-id="95b5f-221">Si la dirección pertenece a la clase A --> se aplica /8</span><span class="sxs-lookup"><span data-stu-id="95b5f-221">If address belongs to class A --> apply /8</span></span>

<span data-ttu-id="95b5f-222">Si la dirección pertenece a la clase B --> se aplica /16</span><span class="sxs-lookup"><span data-stu-id="95b5f-222">If address belongs to class B --> apply /16</span></span>

<span data-ttu-id="95b5f-223">Si la dirección pertenece a la clase C --> se aplica /24</span><span class="sxs-lookup"><span data-stu-id="95b5f-223">If address belongs to class C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="95b5f-224">El cliente de VPN no puede acceder a recursos compartidos de archivos de red</span><span class="sxs-lookup"><span data-stu-id="95b5f-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="95b5f-225">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-225">Symptom</span></span>

<span data-ttu-id="95b5f-226">El cliente de VPN se ha conectado a la red virtual de Azure,</span><span class="sxs-lookup"><span data-stu-id="95b5f-226">The VPN client has connected to the Azure virtual network.</span></span> <span data-ttu-id="95b5f-227">pero no puede acceder a recursos compartidos de red.</span><span class="sxs-lookup"><span data-stu-id="95b5f-227">However, the client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="95b5f-228">Causa</span><span class="sxs-lookup"><span data-stu-id="95b5f-228">Cause</span></span>

<span data-ttu-id="95b5f-229">El protocolo SMB se usa para el acceso a recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="95b5f-229">The SMB protocol is used for file share access.</span></span> <span data-ttu-id="95b5f-230">Cuando se inicia la conexión, el cliente de VPN agrega las credenciales de sesión y se produce el error.</span><span class="sxs-lookup"><span data-stu-id="95b5f-230">When the connection is initiated, the VPN client adds the session credentials and the failure occurs.</span></span> <span data-ttu-id="95b5f-231">Una vez establecida la conexión, el cliente se ve obligado a usar las credenciales almacenadas en caché para la autenticación Kerberos.</span><span class="sxs-lookup"><span data-stu-id="95b5f-231">After the connection is established, the client is forced to use the cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="95b5f-232">Este proceso inicia consultas al Centro de distribución de claves (un controlador de dominio) para obtener un token.</span><span class="sxs-lookup"><span data-stu-id="95b5f-232">This process initiates queries to the Key Distribution Center (a domain controller) to get a token.</span></span> <span data-ttu-id="95b5f-233">Como el cliente se conecta desde Internet, es posible que no pueda alcanzar el controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="95b5f-233">Because the client connects from the Internet, it might not be able to reach the domain controller.</span></span> <span data-ttu-id="95b5f-234">Por lo tanto, el cliente no pueden conmutar por error desde Kerberos a NTLM.</span><span class="sxs-lookup"><span data-stu-id="95b5f-234">Therefore, the client cannot fail over from Kerberos to NTLM.</span></span> 

<span data-ttu-id="95b5f-235">El único momento en que el cliente debe escribir una credencial es cuando tiene un certificado válido (con SAN=UPN) emitido por el dominio al que está unido.</span><span class="sxs-lookup"><span data-stu-id="95b5f-235">The only time that the client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by the domain to which it is joined.</span></span> <span data-ttu-id="95b5f-236">El cliente también debe estar conectado físicamente a la red de dominios.</span><span class="sxs-lookup"><span data-stu-id="95b5f-236">The client also must be physically connected to the domain network.</span></span> <span data-ttu-id="95b5f-237">En este caso, el cliente intenta usar el certificado y llega al controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="95b5f-237">In this case, the client tries to use the certificate and reaches out to the domain controller.</span></span> <span data-ttu-id="95b5f-238">Luego, el Centro de distribución de claves devuelve un error "KDC_ERR_C_PRINCIPAL_UNKNOWN".</span><span class="sxs-lookup"><span data-stu-id="95b5f-238">Then the Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="95b5f-239">El cliente se ve forzado a conmutar por error a NTLM.</span><span class="sxs-lookup"><span data-stu-id="95b5f-239">The client is forced to fail over to NTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="95b5f-240">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-240">Solution</span></span>

<span data-ttu-id="95b5f-241">Para solucionar el problema, deshabilite el almacenamiento en caché de credenciales de dominio desde la subclave del Registro siguiente:</span><span class="sxs-lookup"><span data-stu-id="95b5f-241">To work around the problem, disable the caching of domain credentials from the following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set the value to 1 


## <a name="cannot-find-the-point-to-site-vpn-connection-in-windows-after-reinstalling-the-vpn-client"></a><span data-ttu-id="95b5f-242">No se puede encontrar la conexión VPN de punto a sitio en Windows después de volver a instalar el cliente de VPN</span><span class="sxs-lookup"><span data-stu-id="95b5f-242">Cannot find the point-to-site VPN connection in Windows after reinstalling the VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="95b5f-243">Síntoma</span><span class="sxs-lookup"><span data-stu-id="95b5f-243">Symptom</span></span>

<span data-ttu-id="95b5f-244">Se quita la conexión VPN de punto a sitio y luego se vuelve a instalar el cliente de VPN.</span><span class="sxs-lookup"><span data-stu-id="95b5f-244">You remove the point-to-site VPN connection and then reinstall the VPN client.</span></span> <span data-ttu-id="95b5f-245">En esta situación, la conexión VPN no se configura correctamente.</span><span class="sxs-lookup"><span data-stu-id="95b5f-245">In this situation, the VPN connection is not configured successfully.</span></span> <span data-ttu-id="95b5f-246">No se ve la conexión VPN en el valor **Conexiones de red** de Windows.</span><span class="sxs-lookup"><span data-stu-id="95b5f-246">You do not see the VPN connection in the **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="95b5f-247">Solución</span><span class="sxs-lookup"><span data-stu-id="95b5f-247">Solution</span></span>

<span data-ttu-id="95b5f-248">Para resolver el problema, elimine los archivos de configuración antiguos del cliente de VPN de **C:\Usuarios\Nombre de usuario\AppData\Roaming\Microsoft\Network\Connections** y luego vuelva a ejecutar el instalador del cliente de VPN.</span><span class="sxs-lookup"><span data-stu-id="95b5f-248">To resolve the problem, delete the old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run the VPN client installer again.</span></span>
