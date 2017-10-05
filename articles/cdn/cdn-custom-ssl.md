---
title: "Habilitación de HTTPS en un dominio personalizado de la red CDN de Azure | Microsoft Docs"
description: "Aprenda a habilitar HTTPS en un punto de conexión de la red CDN de Azure con un dominio personalizado."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="3464b-103">Habilitación de HTTPS en un dominio personalizado de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="3464b-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="3464b-104">La compatibilidad de HTTPS con los dominios personalizados de la red CDN de Azure permite entregar contenido seguro a través de SSL con su propio nombre de dominio para mejorar la seguridad de los datos mientras están en tránsito.</span><span class="sxs-lookup"><span data-stu-id="3464b-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span></span> <span data-ttu-id="3464b-105">El flujo de trabajo de un extremo a otro para habilitar HTTPS en un dominio personalizado se simplifica mediante la habilitación con un solo clic y la administración completa de certificados, y todo ello sin ningún costo adicional.</span><span class="sxs-lookup"><span data-stu-id="3464b-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="3464b-106">Es fundamental para garantizar tanto la privacidad como la integridad de todos los datos confidenciales de las aplicaciones web mientras están en tránsito.</span><span class="sxs-lookup"><span data-stu-id="3464b-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="3464b-107">El uso del protocolo HTTPS garantiza que la información confidencial se cifra cuando se envía a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="3464b-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="3464b-108">Proporciona confianza y autenticación, y protege las aplicaciones web de posibles ataques.</span><span class="sxs-lookup"><span data-stu-id="3464b-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="3464b-109">Actualmente, la red CDN de Azure admite HTTPS en un punto de conexión de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="3464b-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="3464b-110">Por ejemplo, si crea un punto de conexión de la red CDN desde la propia red CDN de Azure (p.ej., https://contoso.azureedge.net), HTTPS se habilita de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3464b-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="3464b-111">Ahora, con HTTPS de dominio personalizado, también se puede habilitar la entrega segura para un dominio personalizado (p. ej., https://www.contoso.com).</span><span class="sxs-lookup"><span data-stu-id="3464b-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="3464b-112">Algunos de los atributos clave de la característica de HTTPS son:</span><span class="sxs-lookup"><span data-stu-id="3464b-112">Some of the key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="3464b-113">Sin costo adicional: la adquisición o renovación de certificados no tiene costos y el tráfico HTTPS no supone un costo adicional.</span><span class="sxs-lookup"><span data-stu-id="3464b-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="3464b-114">Solo es preciso pagar por los GB de salida de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="3464b-114">You just pay for GB egress from the CDN.</span></span>

- <span data-ttu-id="3464b-115">Habilitación simple: el aprovisionamiento en un solo clic está disponible desde [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3464b-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3464b-116">También puede utilizar la API de REST u otras herramientas de desarrollo para habilitar la característica.</span><span class="sxs-lookup"><span data-stu-id="3464b-116">You can also use REST API or other developer tools to enable the feature.</span></span>

- <span data-ttu-id="3464b-117">Administración de certificados completa: toda la adquisición y administración de certificados se controla de manera automática.</span><span class="sxs-lookup"><span data-stu-id="3464b-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="3464b-118">Los certificados se aprovisionan y renuevan automáticamente antes de su expiración.</span><span class="sxs-lookup"><span data-stu-id="3464b-118">Certificates are automatically provisioned and renewed prior to expiration.</span></span> <span data-ttu-id="3464b-119">De esta forma desaparece completamente el riesgo de que se interrumpa el servicio como consecuencia de la expiración del certificado.</span><span class="sxs-lookup"><span data-stu-id="3464b-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="3464b-120">Antes de habilitar la compatibilidad con HTTPS, se debe haber establecido un [dominio personalizado de la red CDN de Azure](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="3464b-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-the-feature"></a><span data-ttu-id="3464b-121">Paso 1: Habilitar la característica</span><span class="sxs-lookup"><span data-stu-id="3464b-121">Step 1: Enabling the feature</span></span> 

1. <span data-ttu-id="3464b-122">En [Azure Portal](https://portal.azure.com), vaya a su perfil de CDN estándar o Premium de Verizon.</span><span class="sxs-lookup"><span data-stu-id="3464b-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="3464b-123">En la lista de puntos de conexión, haga clic en el que contiene el dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="3464b-123">In the list of endpoints, click the endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="3464b-124">Haga clic en el dominio personalizado en el que desea habilitar HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3464b-124">Click the custom domain for which you want to enable HTTPS.</span></span>

    ![Hoja de puntos de conexión](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="3464b-126">Haga clic en **Activado** para habilitar HTTPS y guardar el cambio.</span><span class="sxs-lookup"><span data-stu-id="3464b-126">Click **On** to enable HTTPS and save the change.</span></span>

    ![Cuadro de diálogo Personalizar HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="3464b-128">Paso 2: Validación de dominio</span><span class="sxs-lookup"><span data-stu-id="3464b-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="3464b-129">Para que HTTPS pueda activarse en un dominio personalizado, antes es preciso completar la validación del dominio.</span><span class="sxs-lookup"><span data-stu-id="3464b-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="3464b-130">Dispone de seis días laborables para aprobar el dominio.</span><span class="sxs-lookup"><span data-stu-id="3464b-130">You have 6 business days to approve the domain.</span></span> <span data-ttu-id="3464b-131">Si no se realiza la aprobación en 6 días laborables, la solicitud se cancelará.</span><span class="sxs-lookup"><span data-stu-id="3464b-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="3464b-132">Después de habilitar HTTPS en un dominio personalizado, nuestro proveedor de certificados HTTPS, DigiCert, validará la propiedad del dominio, para lo que se pondrá en contacto con el inscrito del dominio, para lo que usará la información de WHOIS del inscrito, a través del correo electrónico (de forma predeterminada) o del teléfono.</span><span class="sxs-lookup"><span data-stu-id="3464b-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="3464b-133">DigiCert también enviará el correo electrónico de comprobación a las siguientes direcciones.</span><span class="sxs-lookup"><span data-stu-id="3464b-133">DigiCert will also send the verification email to the below addresses.</span></span> <span data-ttu-id="3464b-134">Si la información del inscrito de WHOIS es privada, asegúrese de que puede realizar las aprobaciones directamente desde una de estas direcciones.</span><span class="sxs-lookup"><span data-stu-id="3464b-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="3464b-135">admin@<su-nombre-de-dominio.com> administrator@<su-nombre-de-dominio.com></span><span class="sxs-lookup"><span data-stu-id="3464b-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="3464b-136">webmaster@<su-nombre-de-dominio.com></span><span class="sxs-lookup"><span data-stu-id="3464b-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="3464b-137">hostmaster@<su-nombre-de-dominio.com></span><span class="sxs-lookup"><span data-stu-id="3464b-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="3464b-138">postmaster@<su-nombre-de-dominio.com></span><span class="sxs-lookup"><span data-stu-id="3464b-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="3464b-139">Al recibir el correo electrónico, tiene dos opciones de comprobación:</span><span class="sxs-lookup"><span data-stu-id="3464b-139">Upon receiving the email, you have two verification options:</span></span>

1. <span data-ttu-id="3464b-140">Puede aprobar todos los pedidos futuros realizados a través de la misma cuenta del mismo dominio de raíz, por ejemplo, consoto.com.</span><span class="sxs-lookup"><span data-stu-id="3464b-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span></span> <span data-ttu-id="3464b-141">Éste enfoque se recomienda si se planea agregar dominios personalizados en el futuro al mismo dominio raíz.</span><span class="sxs-lookup"><span data-stu-id="3464b-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span></span>
 
2. <span data-ttu-id="3464b-142">Se puede aprobar solo el nombre de host específico usado en esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="3464b-142">You can just approve the specific host name used in this request.</span></span> <span data-ttu-id="3464b-143">Para las solicitudes posteriores se requerirá una aprobación adicional.</span><span class="sxs-lookup"><span data-stu-id="3464b-143">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="3464b-144">Correo electrónico de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3464b-144">Example email:</span></span>
    
    ![Cuadro de diálogo Personalizar HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="3464b-146">Tras la aprobación, DigiCert agregará el nombre de dominio personalizado al certificado de SAN.</span><span class="sxs-lookup"><span data-stu-id="3464b-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span></span> <span data-ttu-id="3464b-147">El certificado tendrá una validez de un año y se renovará automáticamente antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="3464b-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a><span data-ttu-id="3464b-148">Paso 3: Esperar a la propagación y después empezar a usar la característica</span><span class="sxs-lookup"><span data-stu-id="3464b-148">Step 3: Wait for the propagation then start using your feature</span></span>

<span data-ttu-id="3464b-149">Una vez que el nombre de dominio se valide, la característica HTTPS del dominio personalizado tardará entre 6 y 8 horas en estar activa.</span><span class="sxs-lookup"><span data-stu-id="3464b-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span></span> <span data-ttu-id="3464b-150">Una vez completado el proceso, el estado de "personalizar HTTPS" de Azure Portal se establecerá en "Habilitado".</span><span class="sxs-lookup"><span data-stu-id="3464b-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span></span> <span data-ttu-id="3464b-151">HTTPS con el dominio personalizado ya está listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="3464b-151">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="3464b-152">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="3464b-152">Frequently asked questions</span></span>

1. <span data-ttu-id="3464b-153">*¿Quién es el proveedor de certificados y qué tipo de certificado se utiliza?*</span><span class="sxs-lookup"><span data-stu-id="3464b-153">*Who is the certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="3464b-154">Se usa el certificado SAN (nombres alternativos de firmantes) proporcionado por DigiCert.</span><span class="sxs-lookup"><span data-stu-id="3464b-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="3464b-155">Un certificado SAN puede proteger varios nombres de dominio completo con un solo certificado.</span><span class="sxs-lookup"><span data-stu-id="3464b-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="3464b-156">*¿Puedo usar mi certificado dedicado?*</span><span class="sxs-lookup"><span data-stu-id="3464b-156">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="3464b-157">Actualmente, no, pero está en nuestros planes.</span><span class="sxs-lookup"><span data-stu-id="3464b-157">Not currently, but it's on the roadmap.</span></span>

3. <span data-ttu-id="3464b-158">*¿Qué debo hacer si no recibo el correo electrónico de comprobación de dominio de DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="3464b-158">*What if I don't receive the domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="3464b-159">Si no recibe un correo electrónico en 24 horas, póngase en contacto con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3464b-159">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="3464b-160">*¿Son menos seguros los certificados SAN que los certificados dedicados?*</span><span class="sxs-lookup"><span data-stu-id="3464b-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="3464b-161">Los certificados SAN siguen los mismos estándares de cifrado y seguridad que los certificados dedicados.</span><span class="sxs-lookup"><span data-stu-id="3464b-161">A SAN cert follows the same encryption and security standards as a dedicated cert.</span></span> <span data-ttu-id="3464b-162">Todos los certificados SSL emitidos utilizan SHA-256 para mejorar la seguridad del servidor.</span><span class="sxs-lookup"><span data-stu-id="3464b-162">All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="3464b-163">*¿Puedo usar HTTPS de dominio personalizado con la red CDN de Azure de Akamai?*</span><span class="sxs-lookup"><span data-stu-id="3464b-163">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="3464b-164">Actualmente, esta característica solo está disponible en la red CDN de Azure de Verizon.</span><span class="sxs-lookup"><span data-stu-id="3464b-164">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="3464b-165">Estamos trabajando para que esta característica con esté disponible en la red CDN de Azure CDN de Akamai.</span><span class="sxs-lookup"><span data-stu-id="3464b-165">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3464b-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3464b-166">Next steps</span></span>

- <span data-ttu-id="3464b-167">Aprenda a configurar un [dominio personalizado en un punto de conexión de la red CDN de Azure](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="3464b-167">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


