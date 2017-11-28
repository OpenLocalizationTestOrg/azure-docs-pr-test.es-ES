---
title: "aaaAdd SSL certificate tooyour aplicación de servicio de aplicaciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd SSL certificate tooyour aplicación de servicio de aplicaciones."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="f902f-103">Compra y configuración de un certificado SSL para el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="f902f-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="f902f-104">En este tutorial, protegerá su aplicación web comprando un certificado SSL para su instancia de  **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)** almacenándolo de forma segura en [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)y asociándolo a un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="f902f-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-tooazure"></a><span data-ttu-id="f902f-105">Paso 1: inicio de sesión tooAzure</span><span class="sxs-lookup"><span data-stu-id="f902f-105">Step 1 - Log in tooAzure</span></span>

<span data-ttu-id="f902f-106">Inicie sesión en toohello portal de Azure en http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="f902f-106">Log in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="f902f-107">Paso 2: Realización de un pedido de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="f902f-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="f902f-108">Puede hacer un pedido de certificado SSL al crear un nuevo [certificado de servicio de aplicación](https://portal.azure.com/#create/Microsoft.SSL) en hello **portal de Azure**.</span><span class="sxs-lookup"><span data-stu-id="f902f-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In hello **Azure portal**.</span></span>

![Creación de certificados](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="f902f-110">Escriba descriptivo **nombre** para la SSL de los certificados y escriba hello **nombre de dominio**</span><span class="sxs-lookup"><span data-stu-id="f902f-110">Enter a friendly **Name** for your SSL certificate and enter hello **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="f902f-111">Este es uno de los elementos más importantes de hello del proceso de compra de Hola.</span><span class="sxs-lookup"><span data-stu-id="f902f-111">This is one of hello most critical parts of hello purchase process.</span></span> <span data-ttu-id="f902f-112">Asegúrese de que tooenter corrija el nombre de host (dominio personalizado) que desea que tooprotect con este certificado.</span><span class="sxs-lookup"><span data-stu-id="f902f-112">Make sure tooenter correct host name (custom domain) that you want tooprotect with this certificate.</span></span> <span data-ttu-id="f902f-113">**NO** anexar el nombre de Host de hello con World Wide Web.</span><span class="sxs-lookup"><span data-stu-id="f902f-113">**DO NOT** append hello Host name with WWW.</span></span> 
>

<span data-ttu-id="f902f-114">Seleccione la **suscripción**, el **grupo de recursos** y la **SKU de certificado**.</span><span class="sxs-lookup"><span data-stu-id="f902f-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="f902f-115">Certificados de servicio de aplicación solo puede usarse por otros servicios de aplicación dentro de hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="f902f-115">App Service Certificates can only be used by other App Services within hello same subscription.</span></span>  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a><span data-ttu-id="f902f-116">Paso 3: almacenar el certificado de hello en el almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="f902f-116">Step 3 - Store hello certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="f902f-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) es un servicio de Azure que ayuda a proteger claves criptográficas y secretos que emplean servicios y aplicaciones en la nube.</span><span class="sxs-lookup"><span data-stu-id="f902f-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="f902f-118">Una vez completada la Hola compra de certificado SSL, necesita tooopen [certificados de servicio de aplicación](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) hoja de recursos.</span><span class="sxs-lookup"><span data-stu-id="f902f-118">Once hello SSL Certificate purchase is complete, you need tooopen [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![Insertar imagen de toostore listo en KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="f902f-120">Observará que el estado del certificado es **"Emisión pendiente"** ya que hay algunos pasos más necesita toocomplete antes de poder empezar a usar este certificado.</span><span class="sxs-lookup"><span data-stu-id="f902f-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need toocomplete before you can start using this certificate.</span></span>

<span data-ttu-id="f902f-121">Haga clic en **configuración de certificado** dentro de la hoja de propiedades del certificado y haga clic en **paso 1: almacén de** toostore este certificado en el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="f902f-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** toostore this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="f902f-122">De **clave de almacén de estado** hoja, haga clic en **repositorio de almacén de claves** toochoose un toostore de almacén de claves existente este certificado **o crear nuevo almacén de claves** toocreate nueva clave de seguridad del almacén en el mismo grupo de recursos y de suscripción.</span><span class="sxs-lookup"><span data-stu-id="f902f-122">From **Key Vault Status** Blade, click **Key Vault Repository** toochoose an existing Key Vault toostore this certificate **OR Create New Key Vault** toocreate new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="f902f-123">Azure Key Vault tiene gastos mínimos por almacenar este certificado.</span><span class="sxs-lookup"><span data-stu-id="f902f-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="f902f-124">Para obtener más información, consulte **[Detalles de precios de Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="f902f-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="f902f-125">Una vez haya seleccionado toostore de repositorio de almacén de claves de hello en este certificado, Hola **almacén** opción debería mostrar correcto.</span><span class="sxs-lookup"><span data-stu-id="f902f-125">Once you have selected hello Key Vault Repository toostore this certificate in, hello **Store** option should show success.</span></span>

![insert image of store success in KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a><span data-ttu-id="f902f-127">Paso 4: comprobar Hola propiedad del dominio</span><span class="sxs-lookup"><span data-stu-id="f902f-127">Step 4 - Verify hello Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="f902f-128">Los tres tipos de comprobación de dominios compatibles con los certificados de App Service son Comprobación de dominio, Comprobación de correo y Comprobación manual.</span><span class="sxs-lookup"><span data-stu-id="f902f-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="f902f-129">Estos se explican con más detalle en hello [avanzada sección](#advanced).</span><span class="sxs-lookup"><span data-stu-id="f902f-129">These are explained in more details in hello [Advanced section](#advanced).</span></span>

<span data-ttu-id="f902f-130">De Hola mismo **configuración de certificado** hoja usa en el paso 3, haga clic en **paso 2: comprobar**.</span><span class="sxs-lookup"><span data-stu-id="f902f-130">From hello same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="f902f-131">**Comprobación del dominio** se trata de proceso más conveniente de hello **sólo si** tiene  **[adquirido su dominio personalizado de servicio de aplicaciones de Azure.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="f902f-131">**Domain Verification** This is hello most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="f902f-132">Haga clic en **compruebe** botón toocomplete este paso.</span><span class="sxs-lookup"><span data-stu-id="f902f-132">Click on **Verify** button toocomplete this step.</span></span>

![insert image of domain verification](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="f902f-134">Después de hacer clic **compruebe**, usar hello **actualizar** botón hasta hello **compruebe** opción debería mostrar correcto.</span><span class="sxs-lookup"><span data-stu-id="f902f-134">After clicking **Verify**, use hello **Refresh** button until hello **Verify** option should show success.</span></span>

![insert image of verify success in KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a><span data-ttu-id="f902f-136">Paso 5: asignar tooApp de certificado del servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f902f-136">Step 5 - Assign Certificate tooApp Service App</span></span>

> [!NOTE]
> <span data-ttu-id="f902f-137">Antes de realizar los pasos de hello en esta sección, debe tener asociado un nombre de dominio personalizado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f902f-137">Before performing hello steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="f902f-138">Para más información, consulte **[Configuración de un nombre de dominio personalizado para una aplicación web](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="f902f-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="f902f-139">Hola  **[portal de Azure](https://portal.azure.com/)**, haga clic en hello **servicio de aplicaciones** opción izquierda Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="f902f-139">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="f902f-140">Haga clic en el nombre de Hola de su toowhich de aplicación que desea tooassign este certificado.</span><span class="sxs-lookup"><span data-stu-id="f902f-140">Click hello name of your app toowhich you want tooassign this certificate.</span></span>

<span data-ttu-id="f902f-141">Hola **configuración**, haga clic en **certificados SSL**.</span><span class="sxs-lookup"><span data-stu-id="f902f-141">In hello **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="f902f-142">Haga clic en **importar certificado de servicio de aplicación** y seleccione Hola certificado que acaba de comprar.</span><span class="sxs-lookup"><span data-stu-id="f902f-142">Click **Import App Service Certificate** and select hello certificate that you just purchased.</span></span>

![insertar imagen de Importar certificado](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="f902f-144">Hola **enlaces ssl** sección haga clic en **agregar enlaces**, utilice toosecure de nombre de dominio de hello listas desplegables tooselect Hola con SSL y Hola toouse de certificado.</span><span class="sxs-lookup"><span data-stu-id="f902f-144">In hello **ssl bindings** section Click on **Add bindings**, and use hello dropdowns tooselect hello domain name toosecure with SSL, and hello certificate toouse.</span></span> <span data-ttu-id="f902f-145">También puede seleccionar si toouse  **[indicación de nombre de servidor (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  o SSL basada en IP.</span><span class="sxs-lookup"><span data-stu-id="f902f-145">You may also select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![insertar imagen de enlaces de SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="f902f-147">Haga clic en **Agregar enlace** toosave Hola cambios y habilitar SSL.</span><span class="sxs-lookup"><span data-stu-id="f902f-147">Click **Add Binding** toosave hello changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="f902f-148">Si seleccionó **SSL basada en IP** y su dominio personalizado se configura mediante un registro, debe realizar pasos adicionales de Hola.</span><span class="sxs-lookup"><span data-stu-id="f902f-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps.</span></span> <span data-ttu-id="f902f-149">Estos se explican con más detalle en hello [avanzada sección](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="f902f-149">These are explained in more details in hello [Advanced section](#Advanced).</span></span>

<span data-ttu-id="f902f-150">En este momento, también debe ser capaz de toovisit la aplicación con `HTTPS://` en lugar de `HTTP://` tooverify que Hola certificado se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="f902f-150">At this point, you should be able toovisit your app using `HTTPS://` instead of `HTTP://` tooverify that hello certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="f902f-151">Paso 6: Tareas de administración</span><span class="sxs-lookup"><span data-stu-id="f902f-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="f902f-152">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f902f-152">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="f902f-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f902f-153">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="f902f-154">Avanzado</span><span class="sxs-lookup"><span data-stu-id="f902f-154">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="f902f-155">Comprobación de la propiedad del dominio</span><span class="sxs-lookup"><span data-stu-id="f902f-155">Verifying Domain Ownership</span></span>

<span data-ttu-id="f902f-156">Hay dos tipos más de comprobación de dominio que admiten los certificados de App Service: Comprobación de correo electrónico y Comprobación manual.</span><span class="sxs-lookup"><span data-stu-id="f902f-156">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="f902f-157">Comprobación de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="f902f-157">Mail Verification</span></span>

<span data-ttu-id="f902f-158">Correo electrónico de comprobación ya se ha enviado toohello que direcciones de correo electrónico asociado a este dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="f902f-158">Verification email has already been sent toohello Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="f902f-159">paso de verificación de correo electrónico de hello toocomplete, abra el correo electrónico de Hola y haga clic en vínculo de comprobación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f902f-159">toocomplete hello Email verification step, open hello email and click hello verification link.</span></span>

![insert image of email verification](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="f902f-161">Si necesita correo electrónico de comprobación de hello tooresend, haga clic en hello **reenviar correo electrónico** botón.</span><span class="sxs-lookup"><span data-stu-id="f902f-161">If you need tooresend hello verification email, click hello **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="f902f-162">Comprobación manual</span><span class="sxs-lookup"><span data-stu-id="f902f-162">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f902f-163">Comprobación de página web HTML (solo funciona con la SKU de certificados estándar)</span><span class="sxs-lookup"><span data-stu-id="f902f-163">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="f902f-164">Creación de un archivo HTML denominado "**starfield.html**"</span><span class="sxs-lookup"><span data-stu-id="f902f-164">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="f902f-165">Contenido de este archivo debe ser Hola nombre exacto de hello Token de comprobación del dominio.</span><span class="sxs-lookup"><span data-stu-id="f902f-165">Content of this file should be hello exact name of hello Domain Verification Token.</span></span> <span data-ttu-id="f902f-166">(Puede copiar token Hola de hello hoja de estado de comprobación de dominio)</span><span class="sxs-lookup"><span data-stu-id="f902f-166">(You can copy hello token from hello Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="f902f-167">Cargar este archivo en la raíz de Hola de servidor de web de Hola que aloja el dominio`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="f902f-167">Upload this file at hello root of hello web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="f902f-168">Haga clic en **actualizar** estado una vez completada la comprobación del certificado de hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="f902f-168">Click **Refresh** tooupdate hello certificate status after verification is completed.</span></span> <span data-ttu-id="f902f-169">Pueden tardar varios minutos para toocomplete de comprobación.</span><span class="sxs-lookup"><span data-stu-id="f902f-169">It might take few minutes for verification toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="f902f-170">Compruebe en un formulario mediante terminal `curl -G http://<domain>/.well-known/pki-validation/starfield.html` respuesta Hola debe contener hello `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="f902f-170">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello response should contain hello `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="f902f-171">Comprobación del registro TXT de DNS</span><span class="sxs-lookup"><span data-stu-id="f902f-171">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="f902f-172">Con el Administrador de DNS, crear un registro TXT en hello `@` subdominio con valor toohello igual Token de comprobación del dominio.</span><span class="sxs-lookup"><span data-stu-id="f902f-172">Using your DNS manager, Create a TXT record on hello `@` subdomain with value equal toohello Domain Verification Token.</span></span>
1. <span data-ttu-id="f902f-173">Haga clic en **"Actualizar"** tooupdate Hola estado una vez completada la comprobación del certificado.</span><span class="sxs-lookup"><span data-stu-id="f902f-173">Click **“Refresh”** tooupdate hello Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="f902f-174">Necesita un registro TXT toocreate en `@.<domain>` con valor `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="f902f-174">You need toocreate a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-tooapp-service-app"></a><span data-ttu-id="f902f-175">Asignar tooApp de certificado del servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f902f-175">Assign Certificate tooApp Service App</span></span>

<span data-ttu-id="f902f-176">Si seleccionó **SSL basada en IP** y su dominio personalizado se configura mediante un registro, debe realizar pasos adicionales de hello:</span><span class="sxs-lookup"><span data-stu-id="f902f-176">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps:</span></span>

<span data-ttu-id="f902f-177">Después de configurar el enlace SSL basado en una dirección IP, una dirección IP dedicada se asigna tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="f902f-177">After you have configured an IP based SSL binding, a dedicated IP address is assigned tooyour app.</span></span> <span data-ttu-id="f902f-178">Puede encontrar esta dirección IP en hello **dominio personalizado** página en la configuración de la aplicación, justo encima de hello **los nombres de host** sección.</span><span class="sxs-lookup"><span data-stu-id="f902f-178">You can find this IP address on hello **Custom domain** page under settings of your app, right above hello **Hostnames** section.</span></span> <span data-ttu-id="f902f-179">Figurará como **Dirección IP externa**.</span><span class="sxs-lookup"><span data-stu-id="f902f-179">It is listed as **External IP Address**</span></span>

![insertar imagen de SSL de IP](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="f902f-181">Tenga en cuenta que esta dirección IP es diferente de la dirección IP virtual de hello había usado anteriormente registro tooconfigure hello para el dominio.</span><span class="sxs-lookup"><span data-stu-id="f902f-181">Note that this IP address is different than hello virtual IP address used previously tooconfigure hello A record for your domain.</span></span> <span data-ttu-id="f902f-182">Si se configuran toouse SSL basada en SNI o no están configurado toouse SSL, no se mostrará ninguna dirección para esta entrada.</span><span class="sxs-lookup"><span data-stu-id="f902f-182">If you are configured toouse SNI based SSL, or are not configured toouse SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="f902f-183">Mediante herramientas de hello proporcionadas por el registrador de nombres de dominio, modificar un registro para la dirección IP de dominio personalizado nombre toopoint toohello del paso anterior Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="f902f-183">Using hello tools provided by your domain name registrar, modify hello A record for your custom domain name toopoint toohello IP address from hello previous step.</span></span>

## <a name="rekey-and-sync-hello-certificate"></a><span data-ttu-id="f902f-184">Regeneración de claves y sincronización Hola certificado</span><span class="sxs-lookup"><span data-stu-id="f902f-184">Rekey and Sync hello Certificate</span></span>

<span data-ttu-id="f902f-185">Si alguna vez necesitas tooRekey su certificado, seleccione **regenerar y sincronización** opción de **propiedades de certificado** hoja.</span><span class="sxs-lookup"><span data-stu-id="f902f-185">If you ever need tooRekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="f902f-186">Haga clic en **regenerar** botón proceso de hello tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="f902f-186">Click **Rekey** Button tooinitiate hello process.</span></span> <span data-ttu-id="f902f-187">Este proceso puede tardar toocomplete 1-10 minutos.</span><span class="sxs-lookup"><span data-stu-id="f902f-187">This process can take 1-10 minutes toocomplete.</span></span>

![insertar imagen de SSL de regeneración de claves](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="f902f-189">El certificado de regeneración de claves agrupa el certificado Hola con un nuevo certificado emitido por la entidad emisora de certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="f902f-189">Rekeying your certificate rolls hello certificate with a new certificate issued from hello certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f902f-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f902f-190">Next Steps</span></span>

* [<span data-ttu-id="f902f-191">Adición de una red de entrega de contenido</span><span class="sxs-lookup"><span data-stu-id="f902f-191">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)