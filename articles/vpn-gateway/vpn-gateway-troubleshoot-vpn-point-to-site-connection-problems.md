---
title: "problemas de conexión de aaaTroubleshoot point-to-site Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot problemas de conexión de punto a sitio."
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
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="3fe75-103">Solución de problemas: conexión de punto a sitio de Azure</span><span class="sxs-lookup"><span data-stu-id="3fe75-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="3fe75-104">En este artículo se enumeran problemas comunes de conexión de punto a sitio que puede experimentar.</span><span class="sxs-lookup"><span data-stu-id="3fe75-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="3fe75-105">También se tratan las posibles causas de estos problemas y sus soluciones.</span><span class="sxs-lookup"><span data-stu-id="3fe75-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="3fe75-106">Error de cliente de VPN: no se encontró un certificado</span><span class="sxs-lookup"><span data-stu-id="3fe75-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="3fe75-107">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-107">Symptom</span></span>

<span data-ttu-id="3fe75-108">Cuando intente tooconnect tooan red virtual de Azure mediante el uso de cliente VPN de hello, recibirá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="3fe75-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="3fe75-109">**No se encuentra un certificado que se puede usar con este protocolo de autenticación extendido. (Error 798)**</span><span class="sxs-lookup"><span data-stu-id="3fe75-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="3fe75-110">Causa</span><span class="sxs-lookup"><span data-stu-id="3fe75-110">Cause</span></span>

<span data-ttu-id="3fe75-111">Este problema se produce si no está presente en el certificado de cliente hello **certificados - actual\Personal\Certificados**.</span><span class="sxs-lookup"><span data-stu-id="3fe75-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="3fe75-112">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-112">Solution</span></span>

<span data-ttu-id="3fe75-113">Asegúrese de que ese certificado de cliente de Hola se instala en hello ubicación Hola o almacén de certificados (Certmgr.msc) siguiente:</span><span class="sxs-lookup"><span data-stu-id="3fe75-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="3fe75-114">**Certificados - Usuario actual\Personal\Certificados**</span><span class="sxs-lookup"><span data-stu-id="3fe75-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="3fe75-115">Para obtener más información acerca de cómo tooinstall Hola certificado de cliente, consulte [generar y exportar certificados para las conexiones point-to-site](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="3fe75-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3fe75-116">Cuando se importa el certificado de cliente de hello, no seleccione hello **Habilitar protección segura de clave privada** opción.</span><span class="sxs-lookup"><span data-stu-id="3fe75-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="3fe75-117">Error del cliente VPN: se ha recibido el mensaje de saludo con formato incorrecto o inesperado</span><span class="sxs-lookup"><span data-stu-id="3fe75-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="3fe75-118">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-118">Symptom</span></span>

<span data-ttu-id="3fe75-119">Cuando intente tooconnect tooan red virtual de Azure mediante el uso de cliente VPN de hello, recibirá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="3fe75-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="3fe75-120">**mensaje de Hola recibido fue inesperado o con formato incorrecto. (Error 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="3fe75-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="3fe75-121">Causa</span><span class="sxs-lookup"><span data-stu-id="3fe75-121">Cause</span></span>

<span data-ttu-id="3fe75-122">Este problema se produce si la clave pública del certificado de raíz hello no se cargará en la puerta de enlace de VPN de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="3fe75-123">También puede producirse si la clave de hello está dañado o caducado.</span><span class="sxs-lookup"><span data-stu-id="3fe75-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="3fe75-124">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-124">Solution</span></span>

<span data-ttu-id="3fe75-125">tooresolve este problema, comprobar el estado de Hola de raíz de hello certificados en hello Azure toosee portal si se ha revocado.</span><span class="sxs-lookup"><span data-stu-id="3fe75-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="3fe75-126">Si no se revoque, intente reupload y un certificado de raíz de toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="3fe75-127">Para más información, vea [Crear certificados](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="3fe75-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="3fe75-128">Error de cliente de VPN: una cadena de certificados se ha procesado pero ha finalizado</span><span class="sxs-lookup"><span data-stu-id="3fe75-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="3fe75-129">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-129">Symptom</span></span> 

<span data-ttu-id="3fe75-130">Cuando intente tooconnect tooan red virtual de Azure mediante el uso de cliente VPN de hello, recibirá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="3fe75-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="3fe75-131">**Una cadena de certificados ha procesado pero termina en un certificado raíz que no es de confianza para proveedor de confianza de Hola.**</span><span class="sxs-lookup"><span data-stu-id="3fe75-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="3fe75-132">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-132">Solution</span></span>

1. <span data-ttu-id="3fe75-133">Asegúrese de que ese Hola siguientes certificados están en la ubicación correcta de hello:</span><span class="sxs-lookup"><span data-stu-id="3fe75-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="3fe75-134">Certificate</span><span class="sxs-lookup"><span data-stu-id="3fe75-134">Certificate</span></span> | <span data-ttu-id="3fe75-135">La ubicación</span><span class="sxs-lookup"><span data-stu-id="3fe75-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="3fe75-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="3fe75-136">AzureClient.pfx</span></span>  | <span data-ttu-id="3fe75-137">Usuario actual\Personal\Certificados</span><span class="sxs-lookup"><span data-stu-id="3fe75-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="3fe75-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="3fe75-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="3fe75-139">Usuario actual\Entidades de certificación raíz de confianza</span><span class="sxs-lookup"><span data-stu-id="3fe75-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="3fe75-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="3fe75-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="3fe75-141">Equipo local\Entidades de certificación raíz de confianza</span><span class="sxs-lookup"><span data-stu-id="3fe75-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="3fe75-142">Si los certificados de hello ya están en la ubicación de hello, intente toodelete certificados de Hola y vuelva a instalarlos.</span><span class="sxs-lookup"><span data-stu-id="3fe75-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="3fe75-143">Hola  **azuregateway -*GUID*. cloudapp.net** certificado está en el paquete de configuración de cliente VPN de Hola que descargó desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe75-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="3fe75-144">Puede usar archivadores tooextract Hola archivos del paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="3fe75-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="3fe75-145">Error en la descarga del archivo. No se ha especificado el URI de destino</span><span class="sxs-lookup"><span data-stu-id="3fe75-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="3fe75-146">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-146">Symptom</span></span>

<span data-ttu-id="3fe75-147">Recepción Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="3fe75-147">You receive hello following error message:</span></span>

<span data-ttu-id="3fe75-148">**Error en la descarga del archivo. No se ha especificado el URI de destino.**</span><span class="sxs-lookup"><span data-stu-id="3fe75-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="3fe75-149">Causa</span><span class="sxs-lookup"><span data-stu-id="3fe75-149">Cause</span></span> 

<span data-ttu-id="3fe75-150">Este problema se produce debido a un tipo de puerta de enlace incorrecto.</span><span class="sxs-lookup"><span data-stu-id="3fe75-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="3fe75-151">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-151">Solution</span></span>

<span data-ttu-id="3fe75-152">debe ser el tipo de puerta de enlace VPN de Hola **VPN**, y debe ser Hola tipo VPN **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="3fe75-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="3fe75-153">Error de cliente de VPN: error de script personalizado de VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="3fe75-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="3fe75-154">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-154">Symptom</span></span>

<span data-ttu-id="3fe75-155">Cuando intente tooconnect tooan red virtual de Azure mediante el uso de cliente VPN de hello, recibirá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="3fe75-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="3fe75-156">**Secuencia de comandos personalizada (enrutamiento de la tabla tooupdate) no se pudo. (Error 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="3fe75-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="3fe75-157">Causa</span><span class="sxs-lookup"><span data-stu-id="3fe75-157">Cause</span></span>

<span data-ttu-id="3fe75-158">Este problema puede producirse si está tratando de conexión de VPN de sitio a punto de hello tooopen mediante un acceso directo.</span><span class="sxs-lookup"><span data-stu-id="3fe75-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="3fe75-159">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-159">Solution</span></span> 

<span data-ttu-id="3fe75-160">Abra el paquete VPN de hello directamente en lugar de abrirlo en acceso directo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="3fe75-161">No se puede instalar el cliente VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="3fe75-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="3fe75-162">Causa</span><span class="sxs-lookup"><span data-stu-id="3fe75-162">Cause</span></span> 

<span data-ttu-id="3fe75-163">Un certificado adicional es necesario tootrust puerta de enlace VPN de hello para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="3fe75-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="3fe75-164">certificado de Hola se incluye en el paquete de configuración de cliente VPN de Hola que se genera a partir de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe75-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="3fe75-165">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-165">Solution</span></span>

<span data-ttu-id="3fe75-166">Extraer el paquete de configuración de cliente VPN de Hola y busque el archivo .cer de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="3fe75-167">Hola tooinstall certificados, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3fe75-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="3fe75-168">Abra mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="3fe75-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="3fe75-169">Agregar hello **certificados** complemento.</span><span class="sxs-lookup"><span data-stu-id="3fe75-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="3fe75-170">Seleccione hello **equipo** de la cuenta de equipo local Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="3fe75-171">Menú contextual hello **entidades de certificación raíz de confianza** nodo.</span><span class="sxs-lookup"><span data-stu-id="3fe75-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="3fe75-172">Haga clic en **All-Task** > **importación**y examinar toohello CER ha extraído del paquete de configuración de cliente VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="3fe75-173">Reinicie el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="3fe75-174">Pruebe el cliente VPN de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="3fe75-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="3fe75-175">Error de portal de Azure: error de puerta de enlace VPN toosave Hola y Hola datos no son válidos</span><span class="sxs-lookup"><span data-stu-id="3fe75-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="3fe75-176">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-176">Symptom</span></span>

<span data-ttu-id="3fe75-177">Al probar cambios de hello toosave para puerta de enlace VPN de Hola Hola portal de Azure, recibirá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="3fe75-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="3fe75-178">**Puerta de enlace de red virtual de error toosave &lt;* nombre de puerta de enlace*&gt;.</span><span class="sxs-lookup"><span data-stu-id="3fe75-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="3fe75-179">Los datos del certificado &lt;*identificador de certificado*&gt; no son válidos.**</span><span class="sxs-lookup"><span data-stu-id="3fe75-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="3fe75-180">Causa</span><span class="sxs-lookup"><span data-stu-id="3fe75-180">Cause</span></span> 

<span data-ttu-id="3fe75-181">Este problema puede producirse si Hola raíz certificado clave pública que ha cargado contiene un carácter no válido, como un espacio.</span><span class="sxs-lookup"><span data-stu-id="3fe75-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="3fe75-182">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-182">Solution</span></span>

<span data-ttu-id="3fe75-183">Asegúrese de que los datos de hello en el certificado de hello no contienen caracteres no válidos, como los saltos de línea (retorno de carro).</span><span class="sxs-lookup"><span data-stu-id="3fe75-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="3fe75-184">valor de Hello completo debe ser una línea larga.</span><span class="sxs-lookup"><span data-stu-id="3fe75-184">hello entire value should be one long line.</span></span> <span data-ttu-id="3fe75-185">Hola después de texto es un ejemplo de certificado de hello:</span><span class="sxs-lookup"><span data-stu-id="3fe75-185">hello following text is a sample of hello certificate:</span></span>

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

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="3fe75-186">Error de portal de Azure: error de puerta de enlace VPN toosave Hola y Hola nombre de recurso no es válido</span><span class="sxs-lookup"><span data-stu-id="3fe75-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="3fe75-187">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-187">Symptom</span></span>

<span data-ttu-id="3fe75-188">Al probar cambios de hello toosave para puerta de enlace VPN de Hola Hola portal de Azure, recibirá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="3fe75-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="3fe75-189">**Puerta de enlace de red virtual de error toosave &lt;* nombre de puerta de enlace*&gt;.</span><span class="sxs-lookup"><span data-stu-id="3fe75-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="3fe75-190">Nombre del recurso &lt; *nombre del certificado intentas tooupload* &gt; es válida **.</span><span class="sxs-lookup"><span data-stu-id="3fe75-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="3fe75-191">Causa</span><span class="sxs-lookup"><span data-stu-id="3fe75-191">Cause</span></span>

<span data-ttu-id="3fe75-192">Este problema se produce porque el nombre hello del certificado de hello contiene un carácter no válido, como un espacio.</span><span class="sxs-lookup"><span data-stu-id="3fe75-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="3fe75-193">Error de Azure Portal: error de descarga de archivo de paquete de VPN 503</span><span class="sxs-lookup"><span data-stu-id="3fe75-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="3fe75-194">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-194">Symptom</span></span>

<span data-ttu-id="3fe75-195">Al probar el paquete de configuración de cliente VPN de toodownload hello, recibirá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="3fe75-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="3fe75-196">**Error al archivo de hello toodownload. Detalles del error: error 503. Hola servidor está ocupado.**</span><span class="sxs-lookup"><span data-stu-id="3fe75-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="3fe75-197">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-197">Solution</span></span>

<span data-ttu-id="3fe75-198">Este error puede deberse a un problema de red temporal.</span><span class="sxs-lookup"><span data-stu-id="3fe75-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="3fe75-199">Paquete de VPN de hello toodownload vuelva a intentar tras unos minutos.</span><span class="sxs-lookup"><span data-stu-id="3fe75-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="3fe75-200">Actualización de puerta de enlace VPN de Azure: P2S todos los clientes son tooconnect no se puede</span><span class="sxs-lookup"><span data-stu-id="3fe75-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="3fe75-201">Causa</span><span class="sxs-lookup"><span data-stu-id="3fe75-201">Cause</span></span>

<span data-ttu-id="3fe75-202">Si el certificado de hello es más del 50 por ciento a través de su duración, se deshaga certificado Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="3fe75-203">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-203">Solution</span></span>

<span data-ttu-id="3fe75-204">tooresolve este problema, cree y redistribuir los clientes VPN de toohello de nuevos certificados.</span><span class="sxs-lookup"><span data-stu-id="3fe75-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="3fe75-205">Demasiados clientes de VPN conectados a la vez</span><span class="sxs-lookup"><span data-stu-id="3fe75-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="3fe75-206">Para cada puerta de enlace VPN, el número máximo de Hola de conexiones permitidas es 128.</span><span class="sxs-lookup"><span data-stu-id="3fe75-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="3fe75-207">Puede ver el número total de Hola de clientes conectados en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe75-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="3fe75-208">Point-to-site VPN incorrectamente agrega una ruta para una tabla de rutas toohello 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="3fe75-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="3fe75-209">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-209">Symptom</span></span>

<span data-ttu-id="3fe75-210">Al marcar la conexión VPN en el cliente de point-to-site Hola Hola, cliente VPN de Hola debe agregar una ruta hacia Hola red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe75-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="3fe75-211">servicio auxiliar IP de Hello debe agregar una ruta para subred Hola Hola de clientes de VPN.</span><span class="sxs-lookup"><span data-stu-id="3fe75-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="3fe75-212">Hola intervalo de cliente VPN pertenece tooa subred más pequeño de 10.0.0.0/8, como 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="3fe75-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="3fe75-213">En lugar de una ruta para 10.0.12.0/24, se agrega una ruta para 10.0.0.0/8 con una prioridad más alta.</span><span class="sxs-lookup"><span data-stu-id="3fe75-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="3fe75-214">Esta ruta incorrecta interrumpe la conectividad con otras redes locales que es posible que pertenezca tooanother subred dentro de intervalo de 10.0.0.0/8 hello, como 10.50.0.0/24, que no tienen una ruta específica definida.</span><span class="sxs-lookup"><span data-stu-id="3fe75-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="3fe75-215">Causa</span><span class="sxs-lookup"><span data-stu-id="3fe75-215">Cause</span></span>

<span data-ttu-id="3fe75-216">Este comportamiento es así por diseño para los clientes Windows.</span><span class="sxs-lookup"><span data-stu-id="3fe75-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="3fe75-217">Si el cliente de hello usa el protocolo PPP IPCP de hello, que obtiene dirección IP de hello para la interfaz de túnel de hello del servidor de hello (Hola puerta de enlace VPN en este caso).</span><span class="sxs-lookup"><span data-stu-id="3fe75-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="3fe75-218">Sin embargo, debido a una limitación en el protocolo de Hola, cliente hello no tiene máscara de subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="3fe75-219">Porque no hay ningún otro tooget de manera, cliente hello intenta tooguess máscara de subred de hello en función de la clase hello de dirección IP de la interfaz de túnel de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="3fe75-220">Por lo tanto, se agrega una ruta en función de hello después de asignación estática:</span><span class="sxs-lookup"><span data-stu-id="3fe75-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="3fe75-221">Si la dirección pertenece A tooclass--> Aplicar prefijo/8</span><span class="sxs-lookup"><span data-stu-id="3fe75-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="3fe75-222">Si la dirección pertenece tooclass--> B aplicar /16</span><span class="sxs-lookup"><span data-stu-id="3fe75-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="3fe75-223">Si la dirección pertenece tooclass C--> aplicar /24</span><span class="sxs-lookup"><span data-stu-id="3fe75-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="3fe75-224">El cliente de VPN no puede acceder a recursos compartidos de archivos de red</span><span class="sxs-lookup"><span data-stu-id="3fe75-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="3fe75-225">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-225">Symptom</span></span>

<span data-ttu-id="3fe75-226">cliente VPN de Hola ha conectado toohello red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe75-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="3fe75-227">Sin embargo, el cliente de hello no puede tener acceso a recursos compartidos de red.</span><span class="sxs-lookup"><span data-stu-id="3fe75-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="3fe75-228">Causa</span><span class="sxs-lookup"><span data-stu-id="3fe75-228">Cause</span></span>

<span data-ttu-id="3fe75-229">Hola protocolo SMB se utiliza para el acceso de recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="3fe75-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="3fe75-230">Cuando se inicia la conexión de Hola, cliente VPN de hello agrega credenciales de la sesión de Hola y Hola produzcan.</span><span class="sxs-lookup"><span data-stu-id="3fe75-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="3fe75-231">Una vez establecida la conexión de Hola, cliente de Hola se ve obligado a credenciales almacenadas en caché toouse hello para la autenticación Kerberos.</span><span class="sxs-lookup"><span data-stu-id="3fe75-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="3fe75-232">Este proceso inicia consultas toohello Key Distribution Center (un controlador de dominio) tooget un token.</span><span class="sxs-lookup"><span data-stu-id="3fe75-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="3fe75-233">Porque Hola cliente se conecta desde Hola Internet, no sea controlador de dominio pueda tooreach Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="3fe75-234">Por lo tanto, cliente hello no puede conmutar por error de Kerberos tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="3fe75-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="3fe75-235">Hola solo tiempo ese cliente Hola se recibirá un mensaje para una credencial es cuando tiene un certificado válido (con SAN = UPN) emitido por hello toowhich de dominio se ha unido.</span><span class="sxs-lookup"><span data-stu-id="3fe75-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="3fe75-236">cliente de Hello también debe estar conectada físicamente toohello red de dominio.</span><span class="sxs-lookup"><span data-stu-id="3fe75-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="3fe75-237">En este caso, el cliente de Hola intenta certificado de hello toouse y llega toohello controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="3fe75-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="3fe75-238">A continuación, Hola Key Distribution Center devuelve un error de "KDC_ERR_C_PRINCIPAL_UNKNOWN".</span><span class="sxs-lookup"><span data-stu-id="3fe75-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="3fe75-239">cliente de Hello es forzada toofail sobre tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="3fe75-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="3fe75-240">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-240">Solution</span></span>

<span data-ttu-id="3fe75-241">toowork sobre el problema de hello, deshabilitar Hola almacenamiento en caché de credenciales de dominio de la siguiente subclave del registro de hello:</span><span class="sxs-lookup"><span data-stu-id="3fe75-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="3fe75-242">No se puede encontrar la conexión de hello point-to-site VPN en Windows después de reinstalar el cliente VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="3fe75-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="3fe75-243">Síntoma</span><span class="sxs-lookup"><span data-stu-id="3fe75-243">Symptom</span></span>

<span data-ttu-id="3fe75-244">Quitar la conexión de hello point-to-site VPN y, a continuación, vuelva a instalar el cliente VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="3fe75-245">En esta situación, Hola conexión VPN no está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="3fe75-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="3fe75-246">No ve la conexión de VPN de Hola Hola **las conexiones de red** configuración de Windows.</span><span class="sxs-lookup"><span data-stu-id="3fe75-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="3fe75-247">Solución</span><span class="sxs-lookup"><span data-stu-id="3fe75-247">Solution</span></span>

<span data-ttu-id="3fe75-248">problema de hello tooresolve, delete Hola antiguo VPN cliente archivos de configuración de **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, y, a continuación, vuelva a ejecutar el instalador del cliente VPN Hola.</span><span class="sxs-lookup"><span data-stu-id="3fe75-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
