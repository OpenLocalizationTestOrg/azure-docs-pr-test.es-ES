---
title: "Incorporación de un certificado SSL a la aplicación Azure App Service | Microsoft Docs"
description: "Obtenga información sobre cómo agregar un certificado SSL a la aplicación App Service."
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
ms.openlocfilehash: 191dd7240ad15b4936a72bc27a2d0162350f3afb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="d3137-103">Compra y configuración de un certificado SSL para el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="d3137-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="d3137-104">En este tutorial, protegerá su aplicación web comprando un certificado SSL para su instancia de  **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)** almacenándolo de forma segura en [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)y asociándolo a un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="d3137-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-to-azure"></a><span data-ttu-id="d3137-105">Paso 1: Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="d3137-105">Step 1 - Log in to Azure</span></span>

<span data-ttu-id="d3137-106">Inicie sesión en Azure Portal: http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="d3137-106">Log in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="d3137-107">Paso 2: Realización de un pedido de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="d3137-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="d3137-108">Puede hacer un pedido de certificado SSL creando un [certificado de App Service](https://portal.azure.com/#create/Microsoft.SSL) en **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="d3137-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span></span>

![Creación de certificados](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="d3137-110">Escriba un **nombre** descriptivo para su certificado SSL y especifique el **nombre de dominio**.</span><span class="sxs-lookup"><span data-stu-id="d3137-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="d3137-111">Esta es una de las partes más importantes del proceso de compra.</span><span class="sxs-lookup"><span data-stu-id="d3137-111">This is one of the most critical parts of the purchase process.</span></span> <span data-ttu-id="d3137-112">Asegúrese de especificar el nombre de host correcto (dominio personalizado) que desea proteger con este certificado.</span><span class="sxs-lookup"><span data-stu-id="d3137-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span></span> <span data-ttu-id="d3137-113">**NO** anexe el nombre de host con WWW.</span><span class="sxs-lookup"><span data-stu-id="d3137-113">**DO NOT** append the Host name with WWW.</span></span> 
>

<span data-ttu-id="d3137-114">Seleccione la **suscripción**, el **grupo de recursos** y la **SKU de certificado**.</span><span class="sxs-lookup"><span data-stu-id="d3137-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="d3137-115">Los certificados de App Services solo pueden utilizarlas otras instancias de App Service en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="d3137-115">App Service Certificates can only be used by other App Services within the same subscription.</span></span>  
>

## <a name="step-3---store-the-certificate-in-azure-key-vault"></a><span data-ttu-id="d3137-116">Paso 3: Almacenamiento del certificado en Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="d3137-116">Step 3 - Store the certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="d3137-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) es un servicio de Azure que ayuda a proteger claves criptográficas y secretos que emplean servicios y aplicaciones en la nube.</span><span class="sxs-lookup"><span data-stu-id="d3137-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="d3137-118">Una vez completada la compra del certificado SSL, debe abrir la hoja de recursos [Certificados de App Service](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders).</span><span class="sxs-lookup"><span data-stu-id="d3137-118">Once the SSL Certificate purchase is complete, you need to open [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![insertar imagen de listo para almacenar en KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="d3137-120">Observará que el estado del certificado es "**Emisión pendiente**", ya que hay algunos pasos más que debe completar antes de poder empezar a usar este certificado.</span><span class="sxs-lookup"><span data-stu-id="d3137-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span></span>

<span data-ttu-id="d3137-121">Haga clic en "**Configuración del certificado**" dentro de la hoja Propiedades del certificado y haga clic en "**Paso 1: Almacenar**" para almacenar este certificado en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d3137-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="d3137-122">En la hoja **Estado de Key Vault**, haga clic en **Repositorio de Key Vault** para elegir un almacén de claves existente para almacenar este certificado. **También puede hacer clic en Crear nuevo almacén de claves** para generar el nuevo almacén de claves dentro de la misma suscripción y del mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3137-122">From **Key Vault Status** Blade, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="d3137-123">Azure Key Vault tiene gastos mínimos por almacenar este certificado.</span><span class="sxs-lookup"><span data-stu-id="d3137-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="d3137-124">Para obtener más información, consulte **[Detalles de precios de Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="d3137-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="d3137-125">Una vez que haya seleccionado el repositorio de Key Vault donde almacenar este certificado, la opción **Almacenar** debería mostrar el mensaje "correcto".</span><span class="sxs-lookup"><span data-stu-id="d3137-125">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span></span>

![insert image of store success in KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-the-domain-ownership"></a><span data-ttu-id="d3137-127">Paso 4: Comprobación de la propiedad del dominio</span><span class="sxs-lookup"><span data-stu-id="d3137-127">Step 4 - Verify the Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="d3137-128">Los tres tipos de comprobación de dominios compatibles con los certificados de App Service son Comprobación de dominio, Comprobación de correo y Comprobación manual.</span><span class="sxs-lookup"><span data-stu-id="d3137-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="d3137-129">Estos se explican con más detalle en la sección [Avanzado](#advanced).</span><span class="sxs-lookup"><span data-stu-id="d3137-129">These are explained in more details in the [Advanced section](#advanced).</span></span>

<span data-ttu-id="d3137-130">En la hoja **Configuración del certificado** que usó en el paso 3, haga clic en **Paso 2: Comprobación**.</span><span class="sxs-lookup"><span data-stu-id="d3137-130">From the same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="d3137-131">**Comprobación de dominio** es el proceso más cómodo, pero **SOLO SI** **[adquirió el dominio personalizado en Azure App Service](custom-dns-web-site-buydomains-web-app.md)**.</span><span class="sxs-lookup"><span data-stu-id="d3137-131">**Domain Verification** This is the most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="d3137-132">Haga clic en el botón **Comprobar** para completar este paso.</span><span class="sxs-lookup"><span data-stu-id="d3137-132">Click on **Verify** button to complete this step.</span></span>

![insert image of domain verification](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="d3137-134">Después de hacer clic en **Comprobar**, use el botón **Actualizar** hasta que la opción **Comprobar** muestre el mensaje "correcto".</span><span class="sxs-lookup"><span data-stu-id="d3137-134">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span></span>

![insert image of verify success in KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-to-app-service-app"></a><span data-ttu-id="d3137-136">Paso 5: Asignación del certificado a la aplicación de App Service</span><span class="sxs-lookup"><span data-stu-id="d3137-136">Step 5 - Assign Certificate to App Service App</span></span>

> [!NOTE]
> <span data-ttu-id="d3137-137">Antes de realizar los pasos de esta sección, debe haber asociado un nombre de dominio personalizado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d3137-137">Before performing the steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="d3137-138">Para más información, consulte **[Configuración de un nombre de dominio personalizado para una aplicación web](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="d3137-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="d3137-139">En **[Azure Portal](https://portal.azure.com/)**, haga clic en la opción **App Service** del lado izquierdo de la página.</span><span class="sxs-lookup"><span data-stu-id="d3137-139">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="d3137-140">Haga clic en el nombre de la aplicación a la que desea asignar este certificado.</span><span class="sxs-lookup"><span data-stu-id="d3137-140">Click the name of your app to which you want to assign this certificate.</span></span>

<span data-ttu-id="d3137-141">En **Configuración**, haga clic en **Certificados SSL**.</span><span class="sxs-lookup"><span data-stu-id="d3137-141">In the **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="d3137-142">Haga clic en **Importar certificado de App Service** y seleccione el certificado que acaba de comprar.</span><span class="sxs-lookup"><span data-stu-id="d3137-142">Click **Import App Service Certificate** and select the certificate that you just purchased.</span></span>

![insertar imagen de Importar certificado](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="d3137-144">En la sección **Enlaces SSL**, haga clic en **Agregar enlaces** y use las listas desplegables para seleccionar el nombre de dominio que va a proteger con SSL, así como el certificado que pretende utilizar.</span><span class="sxs-lookup"><span data-stu-id="d3137-144">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="d3137-145">Es posible que también desee seleccionar el uso de **[Indicación de nombre de servidor (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** (SNI) o SSL basada en IP.</span><span class="sxs-lookup"><span data-stu-id="d3137-145">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![insertar imagen de enlaces de SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="d3137-147">Haga clic en **Agregar enlace** para guardar los cambios y habilitar SSL.</span><span class="sxs-lookup"><span data-stu-id="d3137-147">Click **Add Binding** to save the changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="d3137-148">Si ha seleccionado **SSL basada en IP** y su dominio personalizado se ha configurado con un registro D, debe realizar los siguientes pasos adicionales.</span><span class="sxs-lookup"><span data-stu-id="d3137-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span></span> <span data-ttu-id="d3137-149">Estos se explican con más detalle en la sección [Avanzado](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="d3137-149">These are explained in more details in the [Advanced section](#Advanced).</span></span>

<span data-ttu-id="d3137-150">Llegados a este punto, debería ser capaz de visitar su aplicación con `HTTPS://` en lugar de `HTTP://`, para comprobar que el certificado se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="d3137-150">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="d3137-151">Paso 6: Tareas de administración</span><span class="sxs-lookup"><span data-stu-id="d3137-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="d3137-152">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d3137-152">Azure CLI</span></span>

<span data-ttu-id="d3137-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Enlace de un certificado SSL personalizado a una aplicación web")]</span><span class="sxs-lookup"><span data-stu-id="d3137-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span> 

### <a name="powershell"></a><span data-ttu-id="d3137-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3137-154">PowerShell</span></span>

<span data-ttu-id="d3137-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Enlace de un certificado SSL personalizado a una aplicación web")]</span><span class="sxs-lookup"><span data-stu-id="d3137-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="advanced"></a><span data-ttu-id="d3137-156">Avanzado</span><span class="sxs-lookup"><span data-stu-id="d3137-156">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="d3137-157">Comprobación de la propiedad del dominio</span><span class="sxs-lookup"><span data-stu-id="d3137-157">Verifying Domain Ownership</span></span>

<span data-ttu-id="d3137-158">Hay dos tipos más de comprobación de dominio que admiten los certificados de App Service: Comprobación de correo electrónico y Comprobación manual.</span><span class="sxs-lookup"><span data-stu-id="d3137-158">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="d3137-159">Comprobación de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="d3137-159">Mail Verification</span></span>

<span data-ttu-id="d3137-160">El correo electrónico de comprobación ya se envió a las direcciones de correo electrónico asociadas a este dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="d3137-160">Verification email has already been sent to the Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="d3137-161">Para completar el paso de comprobación de correo electrónico, abra el mensaje y haga clic en el vínculo de comprobación.</span><span class="sxs-lookup"><span data-stu-id="d3137-161">To complete the Email verification step, open the email and click the verification link.</span></span>

![insert image of email verification](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="d3137-163">Si necesita reenviar el correo electrónico de comprobación, haga clic en el botón **Reenviar correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="d3137-163">If you need to resend the verification email, click the **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="d3137-164">Comprobación manual</span><span class="sxs-lookup"><span data-stu-id="d3137-164">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3137-165">Comprobación de página web HTML (solo funciona con la SKU de certificados estándar)</span><span class="sxs-lookup"><span data-stu-id="d3137-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="d3137-166">Creación de un archivo HTML denominado "**starfield.html**"</span><span class="sxs-lookup"><span data-stu-id="d3137-166">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="d3137-167">El contenido de este archivo debe ser exactamente el mismo nombre del token de comprobación de dominio</span><span class="sxs-lookup"><span data-stu-id="d3137-167">Content of this file should be the exact name of the Domain Verification Token.</span></span> <span data-ttu-id="d3137-168">(puede copiar el token de la hoja Estado de comprobación de dominio).</span><span class="sxs-lookup"><span data-stu-id="d3137-168">(You can copy the token from the Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="d3137-169">Cargue este archivo en la raíz del servidor web que hospeda el dominio `/.well-known/pki-validation/starfield.html`.</span><span class="sxs-lookup"><span data-stu-id="d3137-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="d3137-170">Haga clic en **Actualizar** para poner al día el estado del certificado después de completar la comprobación.</span><span class="sxs-lookup"><span data-stu-id="d3137-170">Click **Refresh** to update the certificate status after verification is completed.</span></span> <span data-ttu-id="d3137-171">La comprobación podría tardar unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="d3137-171">It might take few minutes for verification to complete.</span></span>

> [!TIP]
> <span data-ttu-id="d3137-172">Realice el proceso en un terminal usando `curl -G http://<domain>/.well-known/pki-validation/starfield.html`; la respuesta debería contener `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="d3137-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="d3137-173">Comprobación del registro TXT de DNS</span><span class="sxs-lookup"><span data-stu-id="d3137-173">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="d3137-174">Mediante el administrador de DNS, cree un registro TXT en el subdominio `@` con valor igual al token de comprobación de dominio.</span><span class="sxs-lookup"><span data-stu-id="d3137-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span></span>
1. <span data-ttu-id="d3137-175">Haga clic en **Actualizar** para poner al día el estado del certificado después de completar la comprobación.</span><span class="sxs-lookup"><span data-stu-id="d3137-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="d3137-176">Debe crear un registro TXT en `@.<domain>` con valor `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="d3137-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-to-app-service-app"></a><span data-ttu-id="d3137-177">Asignación del certificado a la aplicación de App Service</span><span class="sxs-lookup"><span data-stu-id="d3137-177">Assign Certificate to App Service App</span></span>

<span data-ttu-id="d3137-178">Si ha seleccionado **SSL basada en IP** y su dominio personalizado se ha configurado con un registro D, debe realizar los siguientes pasos adicionales:</span><span class="sxs-lookup"><span data-stu-id="d3137-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span></span>

<span data-ttu-id="d3137-179">Después de haber configurado un enlace SSL basado en IP, se asigna una dirección IP dedicada a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d3137-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="d3137-180">Podrá encontrar esta dirección IP en la página **Dominio personalizado** de la configuración de su aplicación, justo arriba de la sección **Nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="d3137-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="d3137-181">Figurará como **Dirección IP externa**.</span><span class="sxs-lookup"><span data-stu-id="d3137-181">It is listed as **External IP Address**</span></span>

![insertar imagen de SSL de IP](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="d3137-183">Tenga en cuenta que esta dirección IP será distinta de la dirección IP virtual que ha usado previamente para configurar el registro D de su dominio.</span><span class="sxs-lookup"><span data-stu-id="d3137-183">Note that this IP address is different than the virtual IP address used previously to configure the A record for your domain.</span></span> <span data-ttu-id="d3137-184">Si lo ha configurado para usar una SSL basada en SNI, o bien no lo ha configurado para usar SSL, esta entrada no contendrá ninguna dirección.</span><span class="sxs-lookup"><span data-stu-id="d3137-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="d3137-185">Mediante las herramientas proporcionadas por su registrador de nombres de dominio, modifique el registro D de su nombre de dominio personalizado para que apunte a la dirección IP del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="d3137-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span></span>

## <a name="rekey-and-sync-the-certificate"></a><span data-ttu-id="d3137-186">Regeneración de la clave del certificado y sincronización de este</span><span class="sxs-lookup"><span data-stu-id="d3137-186">Rekey and Sync the Certificate</span></span>

<span data-ttu-id="d3137-187">Si necesita regenerar la clave del certificado, seleccione la opción **Regenerar clave y sincronizar** en la hoja **Propiedades del certificado**.</span><span class="sxs-lookup"><span data-stu-id="d3137-187">If you ever need to Rekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="d3137-188">Haga clic en el botón **Regenerar clave** para iniciar el proceso.</span><span class="sxs-lookup"><span data-stu-id="d3137-188">Click **Rekey** Button to initiate the process.</span></span> <span data-ttu-id="d3137-189">Este proceso puede tardar de 1 a 10 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="d3137-189">This process can take 1-10 minutes to complete.</span></span>

![insertar imagen de SSL de regeneración de claves](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="d3137-191">La regeneración de claves del certificado renovará el certificado con un nuevo certificado emitido desde la entidad de certificación.</span><span class="sxs-lookup"><span data-stu-id="d3137-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3137-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d3137-192">Next Steps</span></span>

* [<span data-ttu-id="d3137-193">Adición de una red de entrega de contenido</span><span class="sxs-lookup"><span data-stu-id="d3137-193">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)