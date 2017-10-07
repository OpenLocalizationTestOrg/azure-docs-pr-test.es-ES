---
title: aaaBind SSL personalizada existente tooAzure las aplicaciones Web de certificados | Documentos de Microsoft
description: "Obtenga información acerca de tootoobind una aplicación personalizada de web tooyour de certificado SSL, un back-end de aplicación móvil o una aplicación de API en el servicio de aplicación de Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a><span data-ttu-id="8e1b7-103">Enlazar un tooAzure de certificado SSL personalizado aplicaciones Web existente</span><span class="sxs-lookup"><span data-stu-id="8e1b7-103">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>

<span data-ttu-id="8e1b7-104">Azure Web Apps proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="8e1b7-105">Este tutorial muestra cómo toobind un SSL personalizado de certificado que ha adquirido en una entidad de certificación de confianza demasiado[aplicaciones Web de Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e1b7-105">This tutorial shows you how toobind a custom SSL certificate that you purchased from a trusted certificate authority too[Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="8e1b7-106">Cuando haya terminado, podrá tooaccess capaz de tu aplicación web en el punto de conexión de hello HTTPS del dominio DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-106">When you're finished, you'll be able tooaccess your web app at hello HTTPS endpoint of your custom DNS domain.</span></span>

![Aplicación web con certificado SSL personalizado](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="8e1b7-108">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="8e1b7-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8e1b7-109">Actualizar el plan de tarifa de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8e1b7-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="8e1b7-110">Enlazar el tooApp de certificado SSL servicio personalizado</span><span class="sxs-lookup"><span data-stu-id="8e1b7-110">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="8e1b7-111">Implementar HTTPS en la aplicación</span><span class="sxs-lookup"><span data-stu-id="8e1b7-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="8e1b7-112">Automatizar el enlace de certificado SSL con scripts</span><span class="sxs-lookup"><span data-stu-id="8e1b7-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="8e1b7-113">Si necesita tooget un certificado SSL personalizado, puede obtenerla en hello portal de Azure directamente y enlazar tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-113">If you need tooget a custom SSL certificate, you can get one in hello Azure portal directly and bind it tooyour web app.</span></span> <span data-ttu-id="8e1b7-114">Siga hello [tutorial de certificados del servicio de aplicación](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="8e1b7-114">Follow hello [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e1b7-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8e1b7-115">Prerequisites</span></span>

<span data-ttu-id="8e1b7-116">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="8e1b7-116">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="8e1b7-117">Crear una aplicación de App Service</span><span class="sxs-lookup"><span data-stu-id="8e1b7-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="8e1b7-118">Asignar una aplicación de web de tooyour de nombre DNS personalizada</span><span class="sxs-lookup"><span data-stu-id="8e1b7-118">Map a custom DNS name tooyour web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="8e1b7-119">Adquirir un certificado SSL de una entidad de certificación de confianza</span><span class="sxs-lookup"><span data-stu-id="8e1b7-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="8e1b7-120">Requisitos para el certificado SSL</span><span class="sxs-lookup"><span data-stu-id="8e1b7-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="8e1b7-121">toouse un certificado de servicio de aplicaciones, el certificado de hello debe cumplir Hola todos los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="8e1b7-121">toouse a certificate in App Service, hello certificate must meet all hello following requirements:</span></span>

* <span data-ttu-id="8e1b7-122">Estar firmado por una entidad de certificación de confianza</span><span class="sxs-lookup"><span data-stu-id="8e1b7-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="8e1b7-123">Haberse exportado como archivo PFX protegido por contraseña</span><span class="sxs-lookup"><span data-stu-id="8e1b7-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="8e1b7-124">Contener una clave privada con una longitud de al menos 2048 bits</span><span class="sxs-lookup"><span data-stu-id="8e1b7-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="8e1b7-125">Contiene todos los certificados intermedios de la cadena de certificados de Hola</span><span class="sxs-lookup"><span data-stu-id="8e1b7-125">Contains all intermediate certificates in hello certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="8e1b7-126">Los **certificados de criptografía de curva elíptica (ECC)** pueden funcionar con App Service, pero están fuera del ámbito de este artículo.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="8e1b7-127">Trabajar con la entidad emisora de certificados en certificados de hello pasos exactos toocreate ECC.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-127">Work with your certificate authority on hello exact steps toocreate ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="8e1b7-128">Preparar la aplicación web</span><span class="sxs-lookup"><span data-stu-id="8e1b7-128">Prepare your web app</span></span>

<span data-ttu-id="8e1b7-129">toobind un SSL personalizado de certificados tooyour web app, su [plan de servicio de aplicaciones](https://azure.microsoft.com/pricing/details/app-service/) debe estar en hello **básica**, **estándar**, o **Premium** capa.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-129">toobind a custom SSL certificate tooyour web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in hello **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="8e1b7-130">En este paso, asegúrese de que la aplicación web se Hola admite nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-130">In this step, you make sure that your web app is in hello supported pricing tier.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="8e1b7-131">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="8e1b7-131">Log in tooAzure</span></span>

<span data-ttu-id="8e1b7-132">Abra hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8e1b7-132">Open hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-tooyour-web-app"></a><span data-ttu-id="8e1b7-133">Navegar por la aplicación web de tooyour</span><span class="sxs-lookup"><span data-stu-id="8e1b7-133">Navigate tooyour web app</span></span>

<span data-ttu-id="8e1b7-134">Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de hello de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-134">From hello left menu, click **App Services**, and then click hello name of your web app.</span></span>

![Seleccionar la aplicación web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="8e1b7-136">Ha llegado a página de administración de hello de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-136">You have landed in hello management page of your web app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="8e1b7-137">Hola de comprobación de nivel de precios</span><span class="sxs-lookup"><span data-stu-id="8e1b7-137">Check hello pricing tier</span></span>

<span data-ttu-id="8e1b7-138">En la navegación del lado izquierdo de saludo de la página de aplicación web, desplácese toohello **configuración** sección y seleccione **escalar verticalmente (plan de servicio de aplicaciones)**.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-138">In hello left-hand navigation of your web app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menú Escalar verticalmente](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="8e1b7-140">Comprobar toomake seguro de que la aplicación web no está en hello **libre** o **Shared** capa.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-140">Check toomake sure that your web app is not in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="8e1b7-141">El nivel actual de la aplicación web aparece resaltado con un cuadro azul oscuro.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="8e1b7-143">SSL personalizado no se admite en hello **libre** o **Shared** capa.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-143">Custom SSL is not supported in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="8e1b7-144">Si necesita tooscale seguridad, siga los pasos de hello en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-144">If you need tooscale up, follow hello steps in hello next section.</span></span> <span data-ttu-id="8e1b7-145">De lo contrario, cierre hello **elegir el nivel de precios** página y omitir demasiado[cargar y enlazar el certificado SSL](#upload).</span><span class="sxs-lookup"><span data-stu-id="8e1b7-145">Otherwise, close hello **Choose your pricing tier** page and skip too[Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="8e1b7-146">Escalar verticalmente el plan de App Service</span><span class="sxs-lookup"><span data-stu-id="8e1b7-146">Scale up your App Service plan</span></span>

<span data-ttu-id="8e1b7-147">Seleccione uno de hello **básica**, **estándar**, o **Premium** niveles.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-147">Select one of hello **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="8e1b7-148">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-148">Click **Select**.</span></span>

![Elegir plan de tarifa](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="8e1b7-150">Cuando vea Hola siguientes a la notificación, la operación de escalado de hello está completa.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-150">When you see hello following notification, hello scale operation is complete.</span></span>

![Notificación de escalado vertical](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="8e1b7-152">Enlazar el certificado SSL</span><span class="sxs-lookup"><span data-stu-id="8e1b7-152">Bind your SSL certificate</span></span>

<span data-ttu-id="8e1b7-153">Se está tooupload preparado su aplicación web SSL certificado tooyour.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-153">You are ready tooupload your SSL certificate tooyour web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="8e1b7-154">Combinación de certificados intermedios</span><span class="sxs-lookup"><span data-stu-id="8e1b7-154">Merge intermediate certificates</span></span>

<span data-ttu-id="8e1b7-155">Si la entidad emisora de certificados ofrece varios certificados en la cadena de certificados de hello, deberá toomerge certificados de hello en orden.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-155">If your certificate authority gives you multiple certificates in hello certificate chain, you need toomerge hello certificates in order.</span></span> 

<span data-ttu-id="8e1b7-156">toodo esto, abra cada certificado que haya recibido en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-156">toodo this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="8e1b7-157">Crear un archivo de certificado combinada de hello, denominado _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-157">Create a file for hello merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="8e1b7-158">En un editor de texto, copie el contenido de Hola de cada certificado en este archivo.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-158">In a text editor, copy hello content of each certificate into this file.</span></span> <span data-ttu-id="8e1b7-159">orden de Hola de los certificados debería ser similar Hola después de plantilla:</span><span class="sxs-lookup"><span data-stu-id="8e1b7-159">hello order of your certificates should look like hello following template:</span></span>

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a><span data-ttu-id="8e1b7-160">Exportar certificado tooPFX</span><span class="sxs-lookup"><span data-stu-id="8e1b7-160">Export certificate tooPFX</span></span>

<span data-ttu-id="8e1b7-161">Exporte el certificado SSL combinado con clave privada de Hola que la solicitud de certificado se generó con.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-161">Export your merged SSL certificate with hello private key that your certificate request was generated with.</span></span>

<span data-ttu-id="8e1b7-162">Si la solicitud de certificado se genera con OpenSSL, se crea un archivo de clave privada.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="8e1b7-163">tooexport su tooPFX de certificado, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-163">tooexport your certificate tooPFX, run hello following command.</span></span> <span data-ttu-id="8e1b7-164">Reemplace los marcadores de posición de hello _ &lt;archivo de clave privada >_ y _ &lt;archivo de certificado combinado >_.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-164">Replace hello placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="8e1b7-165">Cuando se le pida, defina una contraseña de exportación.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-165">When prompted, define an export password.</span></span> <span data-ttu-id="8e1b7-166">Deberá usar esta contraseña al cargar la SSL certificado tooApp servicio más adelante.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-166">You'll use this password when uploading your SSL certificate tooApp Service later.</span></span>

<span data-ttu-id="8e1b7-167">Si usa IIS o _Certreq.exe_ toogenerate su solicitud de certificado, la instalación Hola certificado tooyour local machine y, a continuación, [exportar Hola certificado tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="8e1b7-167">If you used IIS or _Certreq.exe_ toogenerate your certificate request, install hello certificate tooyour local machine, and then [export hello certificate tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="8e1b7-168">Cargar el certificado SSL</span><span class="sxs-lookup"><span data-stu-id="8e1b7-168">Upload your SSL certificate</span></span>

<span data-ttu-id="8e1b7-169">tooupload su certificado SSL, haga clic en **certificados SSL** Hola a la izquierda de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-169">tooupload your SSL certificate, click **SSL certificates** in hello left navigation of your web app.</span></span>

<span data-ttu-id="8e1b7-170">Haga clic en **Cargar certificado**.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="8e1b7-171">En **Archivo de certificado PFX**, seleccione el archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="8e1b7-172">En **contraseña del certificado**, escriba la contraseña Hola que creó al exportar el archivo PFX de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-172">In **Certificate password**, type hello password that you created when you exported hello PFX file.</span></span>

<span data-ttu-id="8e1b7-173">Haga clic en **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-173">Click **Upload**.</span></span>

![Carga del certificado](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="8e1b7-175">Cuando el servicio de aplicación termina de cargar el certificado, aparece en hello **certificados SSL** página.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-175">When App Service finishes uploading your certificate, it appears in hello **SSL certificates** page.</span></span>

![Certificado cargado](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="8e1b7-177">Enlazar el certificado SSL</span><span class="sxs-lookup"><span data-stu-id="8e1b7-177">Bind your SSL certificate</span></span>

<span data-ttu-id="8e1b7-178">Hola **enlaces SSL** sección, haga clic en **Agregar enlace**.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-178">In hello **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="8e1b7-179">Hola **Agregar enlace SSL** , utilice toosecure de nombre de dominio de hello listas desplegables tooselect Hola y Hola certificado toouse.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-179">In hello **Add SSL Binding** page, use hello dropdowns tooselect hello domain name toosecure, and hello certificate toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="8e1b7-180">Si se ha cargado el certificado pero no ve los nombres de dominio de Hola Hola **Hostname** lista desplegable, pruebe a actualizar la página del explorador Hola.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-180">If you have uploaded your certificate but don't see hello domain name(s) in hello **Hostname** dropdown, try refreshing hello browser page.</span></span>
>
>

<span data-ttu-id="8e1b7-181">En **SSL tipo**, seleccione si toouse ** [indicación de nombre de servidor (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication) ** o SSL basado en IP.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-181">In **SSL Type**, select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="8e1b7-182">**SSL basada en SNI**: pueden agregarse varios enlaces SSL basados en SNI.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="8e1b7-183">Esta opción permite que varios toosecure de certificados SSL varios dominios en hello misma dirección IP.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-183">This option allows multiple SSL certificates toosecure multiple domains on hello same IP address.</span></span> <span data-ttu-id="8e1b7-184">Los exploradores más modernos (como Internet Explorer, Chrome, Firefox y Opera) admiten SNI (encontrará información de compatibilidad con exploradores más completa en [Indicación de nombre de servidor](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="8e1b7-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="8e1b7-185">**SSL basada en IP**: solo pueden agregarse enlaces SSL basados en IP.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="8e1b7-186">Esta opción permite toosecure de certificados SSL solo una dirección IP pública dedicada.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-186">This option allows only one SSL certificate toosecure a dedicated public IP address.</span></span> <span data-ttu-id="8e1b7-187">toosecure varios dominios, deben protegerlos todos mediante Hola mismo certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-187">toosecure multiple domains, you must secure them all using hello same SSL certificate.</span></span> <span data-ttu-id="8e1b7-188">Esta es la opción tradicional de hello para el enlace de SSL.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-188">This is hello traditional option for SSL binding.</span></span>

<span data-ttu-id="8e1b7-189">Haga clic en **Agregar enlace**.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-189">Click **Add Binding**.</span></span>

![Enlazar certificado SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="8e1b7-191">Cuando el servicio de aplicación termina de cargar el certificado, aparece en hello **enlaces SSL** secciones.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-191">When App Service finishes uploading your certificate, it appears in hello **SSL bindings** sections.</span></span>

![Certificado enlazado tooweb aplicación](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="8e1b7-193">Reasignar un registro D en SSL de IP</span><span class="sxs-lookup"><span data-stu-id="8e1b7-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="8e1b7-194">Si no usa SSL basado en IP en la aplicación web, omitir demasiado[HTTPS de prueba para su dominio personalizado](#test).</span><span class="sxs-lookup"><span data-stu-id="8e1b7-194">If you don't use IP-based SSL in your web app, skip too[Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="8e1b7-195">De manera predeterminada, la aplicación web usa una dirección IP pública compartida.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="8e1b7-196">Cuando se enlaza un certificado con SSL basada en IP, App Service crea otra dirección IP dedicada para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="8e1b7-197">Si ha asignado una aplicación de web de un registro tooyour, actualizar el registro de dominio con esta dirección IP nueva y dedicada.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-197">If you have mapped an A record tooyour web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="8e1b7-198">La aplicación web **dominio personalizado** página se actualiza con la dirección IP de hello nueva y dedicada.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-198">Your web app's **Custom domain** page is updated with hello new, dedicated IP address.</span></span> <span data-ttu-id="8e1b7-199">[Copie esta dirección IP](app-service-web-tutorial-custom-domain.md#info), a continuación, [Hola de reasignación de un registro](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis nueva dirección IP.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap hello A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="8e1b7-200">Probar HTTPS</span><span class="sxs-lookup"><span data-stu-id="8e1b7-200">Test HTTPS</span></span>

<span data-ttu-id="8e1b7-201">Todo lo que ha dejado toodo ahora es toomake seguro de que funciona HTTPS para su dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-201">All that's left toodo now is toomake sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="8e1b7-202">En distintos exploradores, examinar demasiado`https://<your.custom.domain>` toosee que sirve de seguridad de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-202">In various browsers, browse too`https://<your.custom.domain>` toosee that it serves up your web app.</span></span>

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="8e1b7-204">Si la aplicación web genera errores de validación del certificado, probablemente se esté usando un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="8e1b7-205">Si no es el caso de hello, que ha dejado los certificados intermedios al exportar el archivo PFX del certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-205">If that's not hello case, you may have left out intermediate certificates when you export your certificate toohello PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="8e1b7-206">Aplicación de HTTPS</span><span class="sxs-lookup"><span data-stu-id="8e1b7-206">Enforce HTTPS</span></span>

<span data-ttu-id="8e1b7-207">App Service *no* exige HTTPS, por lo que cualquier usuario todavía puede acceder a la aplicación web mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="8e1b7-208">tooenforce HTTPS para la aplicación web, definir una regla de reescritura en hello _web.config_ archivo de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-208">tooenforce HTTPS for your web app, define a rewrite rule in hello _web.config_ file for your web app.</span></span> <span data-ttu-id="8e1b7-209">Servicio de aplicaciones usa este archivo, independientemente del marco del lenguaje de saludo de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-209">App Service uses this file, regardless of hello language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="8e1b7-210">Hay una redirección específica del lenguaje de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="8e1b7-211">ASP.NET MVC puede usar hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtro en lugar de la regla de reescritura de hello en _web.config_.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-211">ASP.NET MVC can use hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of hello rewrite rule in _web.config_.</span></span>

<span data-ttu-id="8e1b7-212">Si es un desarrollador de .NET, debe estar relativamente familiarizado con este archivo.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="8e1b7-213">Se encuentra en la raíz de saludo de la solución.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-213">It is in hello root of your solution.</span></span>

<span data-ttu-id="8e1b7-214">Además, si desarrolla con PHP, Node.js, Python o Java, existe la posibilidad de que generemos este archivo en su nombre en App Service.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="8e1b7-215">Conectar el punto de conexión de la aplicación web tooyour FTP siguiendo las instrucciones de hello en [implementar el servicio de aplicaciones mediante FTP/S de aplicación tooAzure](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="8e1b7-215">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="8e1b7-216">Este archivo debe encontrarse en _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="8e1b7-217">Si no es así, cree una _web.config_ archivo en esta carpeta con hello continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="8e1b7-217">If not, create a _web.config_ file in this folder with hello following XML:</span></span>

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="8e1b7-218">Para una existente _web.config_ de archivos, copiar todo hello `<rule>` elemento en su _web.config_del `configuration/system.webServer/rewrite/rules` elemento.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-218">For an existing _web.config_ file, copy hello entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="8e1b7-219">Si hay otras `<rule>` elementos en su _web.config_, Hola lugar copian `<rule>` elemento antes de hello otro `<rule>` elementos.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-219">If there are other `<rule>` elements in your _web.config_, place hello copied `<rule>` element before hello other `<rule>` elements.</span></span>

<span data-ttu-id="8e1b7-220">Esta regla devuelve un protocolo HTTPS de toohello HTTP 301 (Redireccionamiento) cada vez que el usuario de hello hace que una aplicación de web de tooyour de solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-220">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="8e1b7-221">Por ejemplo, redirige desde `http://contoso.com` demasiado`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-221">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

<span data-ttu-id="8e1b7-222">Para obtener más información sobre el módulo URL Rewrite para IIS de hello, vea hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentación.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-222">For more information on hello IIS URL Rewrite module, see hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="8e1b7-223">Exigencia de HTTPS para Web Apps en Linux</span><span class="sxs-lookup"><span data-stu-id="8e1b7-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="8e1b7-224">App Service en Linux *no* exige HTTPS, por lo que cualquier usuario todavía puede acceder a la aplicación web mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="8e1b7-225">tooenforce HTTPS para la aplicación web, definir una regla de reescritura en hello _.htaccess_ archivo de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-225">tooenforce HTTPS for your web app, define a rewrite rule in hello _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="8e1b7-226">Conectar el punto de conexión de la aplicación web tooyour FTP siguiendo las instrucciones de hello en [implementar el servicio de aplicaciones mediante FTP/S de aplicación tooAzure](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="8e1b7-226">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="8e1b7-227">En _/home/site/wwwroot_, cree un _.htaccess_ archivo con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="8e1b7-227">In _/home/site/wwwroot_, create an _.htaccess_ file with hello following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="8e1b7-228">Esta regla devuelve un protocolo HTTPS de toohello HTTP 301 (Redireccionamiento) cada vez que el usuario de hello hace que una aplicación de web de tooyour de solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-228">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="8e1b7-229">Por ejemplo, redirige desde `http://contoso.com` demasiado`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-229">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="8e1b7-230">Automatizar con scripts</span><span class="sxs-lookup"><span data-stu-id="8e1b7-230">Automate with scripts</span></span>

<span data-ttu-id="8e1b7-231">Puede automatizar enlaces SSL para su aplicación web con secuencias de comandos, mediante hello [CLI de Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e1b7-231">You can automate SSL bindings for your web app with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="8e1b7-232">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="8e1b7-232">Azure CLI</span></span>

<span data-ttu-id="8e1b7-233">Hola siguiente comando carga un archivo PFX exportado y obtiene la huella digital de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-233">hello following command uploads an exported PFX file and gets hello thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="8e1b7-234">Hello siguiente comando agrega un enlace SSL basado en SNI, con huella digital de hello del comando anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-234">hello following command adds an SNI-based SSL binding, using hello thumbprint from hello previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="8e1b7-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e1b7-235">Azure PowerShell</span></span>

<span data-ttu-id="8e1b7-236">Hello siguiente comando carga un archivo PFX exportado y agrega un enlace SSL basado en SNI.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-236">hello following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="8e1b7-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e1b7-237">Next steps</span></span>

<span data-ttu-id="8e1b7-238">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="8e1b7-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8e1b7-239">Actualizar el plan de tarifa de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8e1b7-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="8e1b7-240">Enlazar el tooApp de certificado SSL servicio personalizado</span><span class="sxs-lookup"><span data-stu-id="8e1b7-240">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="8e1b7-241">Implementar HTTPS en la aplicación</span><span class="sxs-lookup"><span data-stu-id="8e1b7-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="8e1b7-242">Automatizar el enlace de certificado SSL con scripts</span><span class="sxs-lookup"><span data-stu-id="8e1b7-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="8e1b7-243">Avanzar toohello siguiente tutorial toolearn cómo toouse red de entrega de contenido de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e1b7-243">Advance toohello next tutorial toolearn how toouse Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8e1b7-244">Agregar un servicio de aplicaciones de Azure tooan de red de entrega de contenido (CDN)</span><span class="sxs-lookup"><span data-stu-id="8e1b7-244">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
