---
title: aaa "Habilitar HTTPS en un dominio personalizado de CDN de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable HTTPS en el punto de conexión de red CDN de Azure con un dominio personalizado."
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
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="1d4ba-103">Habilitación de HTTPS en un dominio personalizado de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="1d4ba-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="1d4ba-104">Compatibilidad con HTTPS para dominios personalizados de CDN de Azure permite toodeliver contenido seguro a través de SSL con su propia seguridad de dominio nombre tooimprove Hola de datos mientras están en tránsito.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-104">HTTPS support for Azure CDN custom domains enables you toodeliver secure content via SSL using your own domain name tooimprove hello security of data while in transit.</span></span> <span data-ttu-id="1d4ba-105">Hola tooenable de flujo de trabajo de extremo a extremo HTTPS para su dominio personalizado se simplifica mediante la habilitación de un solo clic, la administración de certificados completa y todo sin ningún coste adicional.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-105">hello end-to-end workflow tooenable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="1d4ba-106">Es privacidad de hello tooensure críticos y la integridad de los datos de todos los datos confidenciales de las aplicaciones web mientras están en tránsito.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-106">It's critical tooensure hello privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="1d4ba-107">Utilizando el protocolo HTTPS se asegura de que la información confidencial se cifra cuando se envía a través de Hola Hola internet.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-107">Using hello HTTPS protocol ensures that your sensitive data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="1d4ba-108">Proporciona confianza y autenticación, y protege las aplicaciones web de posibles ataques.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="1d4ba-109">Actualmente, la red CDN de Azure admite HTTPS en un punto de conexión de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="1d4ba-110">Por ejemplo, si crea un punto de conexión de la red CDN desde la propia red CDN de Azure (p.ej., https://contoso.azureedge.net), HTTPS se habilita de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="1d4ba-111">Ahora, con HTTPS de dominio personalizado, también se puede habilitar la entrega segura para un dominio personalizado (p. ej., https://www.contoso.com).</span><span class="sxs-lookup"><span data-stu-id="1d4ba-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="1d4ba-112">Algunos de los atributos de clave de Hola de característica HTTPS son:</span><span class="sxs-lookup"><span data-stu-id="1d4ba-112">Some of hello key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="1d4ba-113">Sin costo adicional: la adquisición o renovación de certificados no tiene costos y el tráfico HTTPS no supone un costo adicional.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="1d4ba-114">Solo paga por GB de salida de la red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-114">You just pay for GB egress from hello CDN.</span></span>

- <span data-ttu-id="1d4ba-115">Habilitación simple: haga clic en uno de aprovisionamiento está disponible en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1d4ba-115">Simple enablement: One click provisioning is available from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1d4ba-116">También puede utilizar la API de REST u otra característica de Hola de tooenable de herramientas de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-116">You can also use REST API or other developer tools tooenable hello feature.</span></span>

- <span data-ttu-id="1d4ba-117">Administración de certificados completa: toda la adquisición y administración de certificados se controla de manera automática.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="1d4ba-118">Los certificados se aprovisionan automáticamente y renuevan tooexpiration anterior.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-118">Certificates are automatically provisioned and renewed prior tooexpiration.</span></span> <span data-ttu-id="1d4ba-119">Esto quita completamente los riesgos de Hola de interrupción del servicio como resultado de un certificado que caduca.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-119">This completely removes hello risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="1d4ba-120">Tooenabling anterior la compatibilidad con HTTPS, debe ya se ha establecido un [dominio personalizado de CDN de Azure](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="1d4ba-120">Prior tooenabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-hello-feature"></a><span data-ttu-id="1d4ba-121">Paso 1: Habilitar la característica de Hola</span><span class="sxs-lookup"><span data-stu-id="1d4ba-121">Step 1: Enabling hello feature</span></span> 

1. <span data-ttu-id="1d4ba-122">Hola [portal de Azure](https://portal.azure.com), examinar el perfil de CDN estándar o premium Verizon de tooyour.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-122">In hello [Azure portal](https://portal.azure.com), browse tooyour Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="1d4ba-123">Hola lista de puntos de conexión, haga clic en punto de conexión de Hola que contiene el dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-123">In hello list of endpoints, click hello endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="1d4ba-124">Haga clic en el dominio personalizado de hello para el que desea tooenable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-124">Click hello custom domain for which you want tooenable HTTPS.</span></span>

    ![Hoja de puntos de conexión](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="1d4ba-126">Haga clic en **en** tooenable HTTPS y guardar el cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-126">Click **On** tooenable HTTPS and save hello change.</span></span>

    ![Cuadro de diálogo Personalizar HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="1d4ba-128">Paso 2: Validación de dominio</span><span class="sxs-lookup"><span data-stu-id="1d4ba-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="1d4ba-129">Para que HTTPS pueda activarse en un dominio personalizado, antes es preciso completar la validación del dominio.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="1d4ba-130">Tiene 6 business días tooapprove Hola dominio.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-130">You have 6 business days tooapprove hello domain.</span></span> <span data-ttu-id="1d4ba-131">Si no se realiza la aprobación en 6 días laborables, la solicitud se cancelará.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="1d4ba-132">Después de habilitar HTTPS en su dominio personalizado, el proveedor de certificados HTTPS DigiCert validará propiedad del dominio poniéndose en contacto persona registrada hello para el dominio, en función de la información del titular WHOIS, a través de correo electrónico (de forma predeterminada) o un teléfono.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting hello registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="1d4ba-133">DigiCert también enviará toohello de correo electrónico de comprobación de hello debajo de direcciones.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-133">DigiCert will also send hello verification email toohello below addresses.</span></span> <span data-ttu-id="1d4ba-134">Si la información del inscrito de WHOIS es privada, asegúrese de que puede realizar las aprobaciones directamente desde una de estas direcciones.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="1d4ba-135">admin@<su-nombre-de-dominio.com> administrator@<su-nombre-de-dominio.com></span><span class="sxs-lookup"><span data-stu-id="1d4ba-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="1d4ba-136">webmaster@<su-nombre-de-dominio.com></span><span class="sxs-lookup"><span data-stu-id="1d4ba-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="1d4ba-137">hostmaster@<su-nombre-de-dominio.com></span><span class="sxs-lookup"><span data-stu-id="1d4ba-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="1d4ba-138">postmaster@<su-nombre-de-dominio.com></span><span class="sxs-lookup"><span data-stu-id="1d4ba-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="1d4ba-139">Al recibir correo electrónico de hello, tienes dos opciones de comprobación:</span><span class="sxs-lookup"><span data-stu-id="1d4ba-139">Upon receiving hello email, you have two verification options:</span></span>

1. <span data-ttu-id="1d4ba-140">Puede aprobar todas las futuras pedidos realizados a través de hello misma cuenta para hello dominio raíz del mismo, por ejemplo, consoto.com. Éste es un enfoque recomendado si tiene previsto dominios personalizados adicionales de tooadd en futuras para Hola Hola dominio raíz del mismo.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-140">You can approve all future orders placed through hello same account for hello same root domain, e.g. consoto.com. This is a recommended approach if you are planning tooadd additional custom domains in hello future for hello same root domain.</span></span>
 
2. <span data-ttu-id="1d4ba-141">Solo puede aprobar el nombre de host específico de hello usado en esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-141">You can just approve hello specific host name used in this request.</span></span> <span data-ttu-id="1d4ba-142">Para las solicitudes posteriores se requerirá una aprobación adicional.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-142">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="1d4ba-143">Correo electrónico de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1d4ba-143">Example email:</span></span>
    
    ![Cuadro de diálogo Personalizar HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="1d4ba-145">Tras la aprobación, DigiCert agregará el certificado de SAN de toohello de nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-145">After approval, DigiCert will add your custom domain name toohello SAN certificate.</span></span> <span data-ttu-id="1d4ba-146">certificado de Hello será válida durante un año y se auto renovará antes de haya expirado.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-146">hello certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a><span data-ttu-id="1d4ba-147">Paso 3: Esperar a la propagación de hello, a continuación, empezar a usar la característica</span><span class="sxs-lookup"><span data-stu-id="1d4ba-147">Step 3: Wait for hello propagation then start using your feature</span></span>

<span data-ttu-id="1d4ba-148">Después de valida el nombre de dominio de hello ocupará too6-8 horas para hello dominio personalizado HTTPS característica toobe active.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-148">After hello domain name is validated it will take up too6-8 hours for hello custom domain HTTPS feature toobe active.</span></span> <span data-ttu-id="1d4ba-149">Una vez completado el proceso de hello, estado de "HTTPS personalizado" Hola Hola portal de Azure se establecerá demasiado "Enabled".</span><span class="sxs-lookup"><span data-stu-id="1d4ba-149">After hello process is complete, hello "custom HTTPS" status in hello Azure portal will be set too"Enabled".</span></span> <span data-ttu-id="1d4ba-150">HTTPS con el dominio personalizado ya está listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-150">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="1d4ba-151">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="1d4ba-151">Frequently asked questions</span></span>

1. <span data-ttu-id="1d4ba-152">*¿Quién es el proveedor de certificados de Hola y se utiliza el tipo de certificado?*</span><span class="sxs-lookup"><span data-stu-id="1d4ba-152">*Who is hello certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="1d4ba-153">Se usa el certificado SAN (nombres alternativos de firmantes) proporcionado por DigiCert.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-153">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="1d4ba-154">Un certificado SAN puede proteger varios nombres de dominio completo con un solo certificado.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-154">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="1d4ba-155">*¿Puedo usar mi certificado dedicado?*</span><span class="sxs-lookup"><span data-stu-id="1d4ba-155">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="1d4ba-156">No actualmente, pero su plan de hello en.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-156">Not currently, but it's on hello roadmap.</span></span>

3. <span data-ttu-id="1d4ba-157">*¿Qué ocurre si no recibo correo electrónico de comprobación de dominio Hola de DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="1d4ba-157">*What if I don't receive hello domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="1d4ba-158">Si no recibe un correo electrónico en 24 horas, póngase en contacto con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-158">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="1d4ba-159">*¿Son menos seguros los certificados SAN que los certificados dedicados?*</span><span class="sxs-lookup"><span data-stu-id="1d4ba-159">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="1d4ba-160">Un certificado SAN sigue Hola mismos estándares de cifrado y seguridad, como un certificado dedicado. Todos los certificados SSL emitidos utilizan SHA-256 para mejorar la seguridad del servidor.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-160">A SAN cert follows hello same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="1d4ba-161">*¿Puedo usar HTTPS de dominio personalizado con la red CDN de Azure de Akamai?*</span><span class="sxs-lookup"><span data-stu-id="1d4ba-161">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="1d4ba-162">Actualmente, esta característica solo está disponible en la red CDN de Azure de Verizon.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-162">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="1d4ba-163">Estamos trabajando en la compatibilidad con esta característica con Azure CDN de Akamai en los próximos meses de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d4ba-163">We are working on supporting this feature with Azure CDN from Akamai in hello coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1d4ba-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d4ba-164">Next steps</span></span>

- <span data-ttu-id="1d4ba-165">Obtenga información acerca de cómo tooset seguridad un [dominio personalizado en el punto de conexión de red CDN de Azure](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="1d4ba-165">Learn how tooset up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


