---
title: Enlazar un certificado SSL personalizado a Azure Web Apps | Microsoft Docs
description: "Aprenda a enlazar un certificado SSL personalizado a aplicaciones web, back-ends para aplicaciones móviles o aplicaciones de API en Azure App Service."
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
ms.openlocfilehash: 15c31ae5451a31dff2df08047ee43e75edacc127
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="bc81e-103">Enlazar un certificado SSL personalizado a Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="bc81e-103">Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="bc81e-104">Azure Web Apps proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="bc81e-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="bc81e-105">En este tutorial se muestra cómo enlazar un certificado SSL personalizado adquirido de una entidad de certificación de confianza para [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc81e-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="bc81e-106">Cuando haya terminado, podrá acceder a la aplicación web en el punto de conexión HTTPS de su dominio DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="bc81e-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![Aplicación web con certificado SSL personalizado](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="bc81e-108">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="bc81e-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bc81e-109">Actualizar el plan de tarifa de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bc81e-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="bc81e-110">Enlazar el certificado SSL personalizado con App Service</span><span class="sxs-lookup"><span data-stu-id="bc81e-110">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="bc81e-111">Implementar HTTPS en la aplicación</span><span class="sxs-lookup"><span data-stu-id="bc81e-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="bc81e-112">Automatizar el enlace de certificado SSL con scripts</span><span class="sxs-lookup"><span data-stu-id="bc81e-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="bc81e-113">Si necesita un certificado SSL personalizado, puede obtener uno directamente en Azure Portal y enlazarlo a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-113">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="bc81e-114">Siga el tutorial [Incorporación de un certificado SSL a la aplicación App Service](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="bc81e-114">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc81e-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bc81e-115">Prerequisites</span></span>

<span data-ttu-id="bc81e-116">Para completar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="bc81e-116">To complete this tutorial:</span></span>

- [<span data-ttu-id="bc81e-117">Crear una aplicación de App Service</span><span class="sxs-lookup"><span data-stu-id="bc81e-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="bc81e-118">Asignar un nombre DNS personalizado a la aplicación web</span><span class="sxs-lookup"><span data-stu-id="bc81e-118">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="bc81e-119">Adquirir un certificado SSL de una entidad de certificación de confianza</span><span class="sxs-lookup"><span data-stu-id="bc81e-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="bc81e-120">Requisitos para el certificado SSL</span><span class="sxs-lookup"><span data-stu-id="bc81e-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="bc81e-121">Para usar un certificado en App Service, el certificado debe cumplir los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="bc81e-121">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="bc81e-122">Estar firmado por una entidad de certificación de confianza</span><span class="sxs-lookup"><span data-stu-id="bc81e-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="bc81e-123">Haberse exportado como archivo PFX protegido por contraseña</span><span class="sxs-lookup"><span data-stu-id="bc81e-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="bc81e-124">Contener una clave privada con una longitud de al menos 2048 bits</span><span class="sxs-lookup"><span data-stu-id="bc81e-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="bc81e-125">Contener todos los certificados intermedios de la cadena de certificados</span><span class="sxs-lookup"><span data-stu-id="bc81e-125">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="bc81e-126">Los **certificados de criptografía de curva elíptica (ECC)** pueden funcionar con App Service, pero están fuera del ámbito de este artículo.</span><span class="sxs-lookup"><span data-stu-id="bc81e-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="bc81e-127">Trabaje con la entidad de certificación sobre los pasos exactos para crear certificados ECC.</span><span class="sxs-lookup"><span data-stu-id="bc81e-127">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="bc81e-128">Preparar la aplicación web</span><span class="sxs-lookup"><span data-stu-id="bc81e-128">Prepare your web app</span></span>

<span data-ttu-id="bc81e-129">Para enlazar un certificado SSL personalizado a la aplicación web, su [plan de App Service](https://azure.microsoft.com/pricing/details/app-service/) debe estar en el nivel **Básico**, **Estándar** o **Premium**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-129">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="bc81e-130">En este paso, asegúrese de que la aplicación web se encuentra en el plan de tarifa compatible.</span><span class="sxs-lookup"><span data-stu-id="bc81e-130">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="bc81e-131">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="bc81e-131">Log in to Azure</span></span>

<span data-ttu-id="bc81e-132">Abra el [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bc81e-132">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="bc81e-133">Navegar a la aplicación web</span><span class="sxs-lookup"><span data-stu-id="bc81e-133">Navigate to your web app</span></span>

<span data-ttu-id="bc81e-134">En el menú izquierdo, haga clic en **App Services** y luego en el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-134">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![Seleccionar la aplicación web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="bc81e-136">Ha llegado a la página de administración de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-136">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="bc81e-137">Comprobar el plan de tarifa</span><span class="sxs-lookup"><span data-stu-id="bc81e-137">Check the pricing tier</span></span>

<span data-ttu-id="bc81e-138">En el panel de navegación izquierdo de la página de la aplicación web, desplácese a la sección **Configuración** y seleccione **Escalar verticalmente (plan de App Service)**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-138">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menú Escalar verticalmente](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="bc81e-140">Asegúrese de que la aplicación web no está en el nivel **Gratis** ni **Compartido**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-140">Check to make sure that your web app is not in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="bc81e-141">El nivel actual de la aplicación web aparece resaltado con un cuadro azul oscuro.</span><span class="sxs-lookup"><span data-stu-id="bc81e-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="bc81e-143">El SSL personalizado no es compatible con los niveles **Gratis** y **Compartido**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-143">Custom SSL is not supported in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="bc81e-144">Si tiene que escalar verticalmente, siga los pasos de la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="bc81e-144">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="bc81e-145">Si no, cierre la página **Elija su plan de tarifa** y vaya directamente a las secciones sobre cómo [cargar y enlazar el certificado SSL](#upload).</span><span class="sxs-lookup"><span data-stu-id="bc81e-145">Otherwise, close the **Choose your pricing tier** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="bc81e-146">Escalar verticalmente el plan de App Service</span><span class="sxs-lookup"><span data-stu-id="bc81e-146">Scale up your App Service plan</span></span>

<span data-ttu-id="bc81e-147">Seleccione uno de los niveles, **Básico**, **Estándar** o **Premium**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-147">Select one of the **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="bc81e-148">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-148">Click **Select**.</span></span>

![Elegir plan de tarifa](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="bc81e-150">Cuando vea la siguiente notificación, significará que la operación de escalado se habrá completado.</span><span class="sxs-lookup"><span data-stu-id="bc81e-150">When you see the following notification, the scale operation is complete.</span></span>

![Notificación de escalado vertical](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="bc81e-152">Enlazar el certificado SSL</span><span class="sxs-lookup"><span data-stu-id="bc81e-152">Bind your SSL certificate</span></span>

<span data-ttu-id="bc81e-153">Está listo para cargar el certificado SSL en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-153">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="bc81e-154">Combinación de certificados intermedios</span><span class="sxs-lookup"><span data-stu-id="bc81e-154">Merge intermediate certificates</span></span>

<span data-ttu-id="bc81e-155">Si la entidad emisora de certificados ofrece varios certificados en la cadena de certificados, debe combinar los certificados en orden.</span><span class="sxs-lookup"><span data-stu-id="bc81e-155">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="bc81e-156">Para ello, abra cada certificado que ha recibido en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="bc81e-156">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="bc81e-157">Cree un archivo para el certificado combinado, denominado _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="bc81e-157">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="bc81e-158">En un editor de texto, copie el contenido de cada certificado en este archivo.</span><span class="sxs-lookup"><span data-stu-id="bc81e-158">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="bc81e-159">El orden de los certificados debe ser como la siguiente plantilla:</span><span class="sxs-lookup"><span data-stu-id="bc81e-159">The order of your certificates should look like the following template:</span></span>

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

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="bc81e-160">Exportar el certificado a PFX</span><span class="sxs-lookup"><span data-stu-id="bc81e-160">Export certificate to PFX</span></span>

<span data-ttu-id="bc81e-161">Exporte el certificado SSL personalizado con la clave privada con la que se generó la solicitud de certificado.</span><span class="sxs-lookup"><span data-stu-id="bc81e-161">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="bc81e-162">Si la solicitud de certificado se genera con OpenSSL, se crea un archivo de clave privada.</span><span class="sxs-lookup"><span data-stu-id="bc81e-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="bc81e-163">Para exportar el certificado a PFX, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="bc81e-163">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="bc81e-164">Reemplace los marcadores de posición _&lt;private-key-file>_ y _&lt;merged-certificate-file>_.</span><span class="sxs-lookup"><span data-stu-id="bc81e-164">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="bc81e-165">Cuando se le pida, defina una contraseña de exportación.</span><span class="sxs-lookup"><span data-stu-id="bc81e-165">When prompted, define an export password.</span></span> <span data-ttu-id="bc81e-166">Esta contraseña deberá usarla al cargar el certificado SSL posteriormente en App Service.</span><span class="sxs-lookup"><span data-stu-id="bc81e-166">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="bc81e-167">Si usó IIS o _Certreq.exe_ para generar la solicitud de certificado, instale el certificado en la máquina local y luego [exporte el certificado a PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="bc81e-167">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="bc81e-168">Cargar el certificado SSL</span><span class="sxs-lookup"><span data-stu-id="bc81e-168">Upload your SSL certificate</span></span>

<span data-ttu-id="bc81e-169">Para cargar el certificado SSL, haga clic en **Certificados SSL** en el panel de navegación izquierdo de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-169">To upload your SSL certificate, click **SSL certificates** in the left navigation of your web app.</span></span>

<span data-ttu-id="bc81e-170">Haga clic en **Cargar certificado**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="bc81e-171">En **Archivo de certificado PFX**, seleccione el archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="bc81e-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="bc81e-172">En **Contraseña del certificado**, escriba la contraseña que creó al exportar el archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="bc81e-172">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="bc81e-173">Haga clic en **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-173">Click **Upload**.</span></span>

![Carga del certificado](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="bc81e-175">Cuando App Service termina de cargar el certificado, este aparece en la página **Certificados SSL**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-175">When App Service finishes uploading your certificate, it appears in the **SSL certificates** page.</span></span>

![Certificado cargado](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="bc81e-177">Enlazar el certificado SSL</span><span class="sxs-lookup"><span data-stu-id="bc81e-177">Bind your SSL certificate</span></span>

<span data-ttu-id="bc81e-178">En la sección **Enlaces SSL**, haga clic en **Agregar enlace**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-178">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="bc81e-179">En la página **Agregar enlace SSL**, use las listas desplegables para seleccionar el nombre de dominio que va a proteger, así como el certificado que pretende utilizar.</span><span class="sxs-lookup"><span data-stu-id="bc81e-179">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="bc81e-180">Si ha cargado el certificado pero no ve los nombres de dominio en la lista desplegable **Nombre de host**, pruebe a actualizar la página del explorador.</span><span class="sxs-lookup"><span data-stu-id="bc81e-180">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="bc81e-181">En **Tipo de SSL**, seleccione si se va a usar **[Indicación de nombre de servidor (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** o SSL basada en IP.</span><span class="sxs-lookup"><span data-stu-id="bc81e-181">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="bc81e-182">**SSL basada en SNI**: pueden agregarse varios enlaces SSL basados en SNI.</span><span class="sxs-lookup"><span data-stu-id="bc81e-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="bc81e-183">Esta opción permite que varios certificados SSL protejan varios dominios en una misma dirección IP.</span><span class="sxs-lookup"><span data-stu-id="bc81e-183">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="bc81e-184">Los exploradores más modernos (como Internet Explorer, Chrome, Firefox y Opera) admiten SNI (encontrará información de compatibilidad con exploradores más completa en [Indicación de nombre de servidor](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="bc81e-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="bc81e-185">**SSL basada en IP**: solo pueden agregarse enlaces SSL basados en IP.</span><span class="sxs-lookup"><span data-stu-id="bc81e-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="bc81e-186">Esta opción solo permite que un único certificado SSL proteja una dirección IP dedicada.</span><span class="sxs-lookup"><span data-stu-id="bc81e-186">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="bc81e-187">Para proteger varios dominios, debe protegerlos todos con el mismo certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="bc81e-187">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="bc81e-188">Se trata de la opción tradicional para enlaces SSL.</span><span class="sxs-lookup"><span data-stu-id="bc81e-188">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="bc81e-189">Haga clic en **Agregar enlace**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-189">Click **Add Binding**.</span></span>

![Enlazar certificado SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="bc81e-191">Cuando App Service termina de cargar el certificado, este aparece en la sección **Enlaces SSL**.</span><span class="sxs-lookup"><span data-stu-id="bc81e-191">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![Certificado enlazado a la aplicación web](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="bc81e-193">Reasignar un registro D en SSL de IP</span><span class="sxs-lookup"><span data-stu-id="bc81e-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="bc81e-194">Si no usa SSL basado en IP en la aplicación web, vaya directamente a [Probar HTTPS para el dominio personalizado](#test).</span><span class="sxs-lookup"><span data-stu-id="bc81e-194">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="bc81e-195">De manera predeterminada, la aplicación web usa una dirección IP pública compartida.</span><span class="sxs-lookup"><span data-stu-id="bc81e-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="bc81e-196">Cuando se enlaza un certificado con SSL basada en IP, App Service crea otra dirección IP dedicada para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="bc81e-197">Si ha asignado un registro D a la aplicación web, actualice el registro de dominio con esta nueva dirección IP dedicada.</span><span class="sxs-lookup"><span data-stu-id="bc81e-197">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="bc81e-198">La página **Dominio personalizado** de la aplicación web se actualiza con la nueva dirección IP dedicada.</span><span class="sxs-lookup"><span data-stu-id="bc81e-198">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="bc81e-199">[Copie esta dirección IP](app-service-web-tutorial-custom-domain.md#info) y luego [reasigne el registro D](app-service-web-tutorial-custom-domain.md#map-an-a-record) a esta nueva dirección IP.</span><span class="sxs-lookup"><span data-stu-id="bc81e-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="bc81e-200">Probar HTTPS</span><span class="sxs-lookup"><span data-stu-id="bc81e-200">Test HTTPS</span></span>

<span data-ttu-id="bc81e-201">Ahora todo lo que queda por hacer es asegurarse de que HTTPS funciona para el dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="bc81e-201">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="bc81e-202">En varios exploradores, vaya a `https://<your.custom.domain>` para ver que atiende la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-202">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![Navegación en el portal a la aplicación de Azure](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="bc81e-204">Si la aplicación web genera errores de validación del certificado, probablemente se esté usando un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="bc81e-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="bc81e-205">Si no es así, puede que haya olvidado certificados intermedios cuando exportó el certificado al archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="bc81e-205">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="bc81e-206">Aplicación de HTTPS</span><span class="sxs-lookup"><span data-stu-id="bc81e-206">Enforce HTTPS</span></span>

<span data-ttu-id="bc81e-207">App Service *no* exige HTTPS, por lo que cualquier usuario todavía puede acceder a la aplicación web mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="bc81e-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="bc81e-208">Para aplicar HTTPS en su aplicación web, defina una regla de reescritura en el archivo _web.config_ de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-208">To enforce HTTPS for your web app, define a rewrite rule in the _web.config_ file for your web app.</span></span> <span data-ttu-id="bc81e-209">App Service usa este archivo, independientemente de la plataforma del lenguaje de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-209">App Service uses this file, regardless of the language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="bc81e-210">Hay una redirección específica del lenguaje de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="bc81e-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="bc81e-211">ASP.NET MVC puede usar el filtro [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) en lugar de la regla de reescritura en _web.config_.</span><span class="sxs-lookup"><span data-stu-id="bc81e-211">ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in _web.config_.</span></span>

<span data-ttu-id="bc81e-212">Si es un desarrollador de .NET, debe estar relativamente familiarizado con este archivo.</span><span class="sxs-lookup"><span data-stu-id="bc81e-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="bc81e-213">Se encuentra en la raíz de la solución.</span><span class="sxs-lookup"><span data-stu-id="bc81e-213">It is in the root of your solution.</span></span>

<span data-ttu-id="bc81e-214">Además, si desarrolla con PHP, Node.js, Python o Java, existe la posibilidad de que generemos este archivo en su nombre en App Service.</span><span class="sxs-lookup"><span data-stu-id="bc81e-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="bc81e-215">Conéctese al punto de conexión FTP de la aplicación web. Para ello, siga las instrucciones que se ofrecen en [Implementación de la aplicación en Azure App Service mediante FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="bc81e-215">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="bc81e-216">Este archivo debe encontrarse en _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="bc81e-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="bc81e-217">Si no es así, cree un archivo _web.config_ en esta carpeta con el siguiente XML:</span><span class="sxs-lookup"><span data-stu-id="bc81e-217">If not, create a _web.config_ file in this folder with the following XML:</span></span>

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

<span data-ttu-id="bc81e-218">Para un archivo _web.config_ existente, copie el elemento entero `<rule>` en el elemento `configuration/system.webServer/rewrite/rules` de su archivo _web.config_.</span><span class="sxs-lookup"><span data-stu-id="bc81e-218">For an existing _web.config_ file, copy the entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="bc81e-219">Si hay otros elementos `<rule>` en su archivo _web.config_, sustituya el elemento `<rule>` copiado antes de los otros elementos `<rule>`.</span><span class="sxs-lookup"><span data-stu-id="bc81e-219">If there are other `<rule>` elements in your _web.config_, place the copied `<rule>` element before the other `<rule>` elements.</span></span>

<span data-ttu-id="bc81e-220">Esta regla devuelve un código HTTP 301 (redirección permanente) al protocolo HTTPS siempre que el usuario realiza una solicitud HTTP en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-220">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="bc81e-221">Por ejemplo, se redirige de `http://contoso.com` a `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="bc81e-221">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

<span data-ttu-id="bc81e-222">Para obtener más información sobre el módulo URL Rewrite de IIS, consulte la documentación de [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) .</span><span class="sxs-lookup"><span data-stu-id="bc81e-222">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="bc81e-223">Exigencia de HTTPS para Web Apps en Linux</span><span class="sxs-lookup"><span data-stu-id="bc81e-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="bc81e-224">App Service en Linux *no* exige HTTPS, por lo que cualquier usuario todavía puede acceder a la aplicación web mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="bc81e-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="bc81e-225">Para exigir HTTPS en su aplicación web, defina una regla de reescritura en el archivo _.htaccess_ de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-225">To enforce HTTPS for your web app, define a rewrite rule in the _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="bc81e-226">Conéctese al punto de conexión FTP de la aplicación web. Para ello, siga las instrucciones que se ofrecen en [Implementación de la aplicación en Azure App Service mediante FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="bc81e-226">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="bc81e-227">En _/home/site/wwwroot_, cree un archivo _.htaccess_ con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="bc81e-227">In _/home/site/wwwroot_, create an _.htaccess_ file with the following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="bc81e-228">Esta regla devuelve un código HTTP 301 (redirección permanente) al protocolo HTTPS siempre que el usuario realiza una solicitud HTTP en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bc81e-228">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="bc81e-229">Por ejemplo, se redirige de `http://contoso.com` a `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="bc81e-229">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="bc81e-230">Automatizar con scripts</span><span class="sxs-lookup"><span data-stu-id="bc81e-230">Automate with scripts</span></span>

<span data-ttu-id="bc81e-231">Puede automatizar enlaces SSL de la aplicación web con scripts, mediante la [CLI de Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bc81e-231">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="bc81e-232">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="bc81e-232">Azure CLI</span></span>

<span data-ttu-id="bc81e-233">El comando siguiente carga un archivo PFX exportado y obtiene la huella digital.</span><span class="sxs-lookup"><span data-stu-id="bc81e-233">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="bc81e-234">El comando siguiente usa la huella digital del comando anterior para agregar un enlace SSL basado en SNI.</span><span class="sxs-lookup"><span data-stu-id="bc81e-234">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="bc81e-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc81e-235">Azure PowerShell</span></span>

<span data-ttu-id="bc81e-236">El comando siguiente carga un archivo PFX exportado y agrega un enlace SSL basado en SNI.</span><span class="sxs-lookup"><span data-stu-id="bc81e-236">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="bc81e-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bc81e-237">Next steps</span></span>

<span data-ttu-id="bc81e-238">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="bc81e-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bc81e-239">Actualizar el plan de tarifa de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bc81e-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="bc81e-240">Enlazar el certificado SSL personalizado con App Service</span><span class="sxs-lookup"><span data-stu-id="bc81e-240">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="bc81e-241">Implementar HTTPS en la aplicación</span><span class="sxs-lookup"><span data-stu-id="bc81e-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="bc81e-242">Automatizar el enlace de certificado SSL con scripts</span><span class="sxs-lookup"><span data-stu-id="bc81e-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="bc81e-243">Para aprender a usar Azure Content Delivery Network, avance al siguiente tutorial.</span><span class="sxs-lookup"><span data-stu-id="bc81e-243">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bc81e-244">Incorporación de una red de entrega de contenido a Azure App Service</span><span class="sxs-lookup"><span data-stu-id="bc81e-244">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
