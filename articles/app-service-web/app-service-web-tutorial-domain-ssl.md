---
title: "aplicación web de dominio personalizado de aaaAdd y SSL tooan Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprepare Azure web producción toogo de aplicación mediante la adición de la marca de la empresa. Asignar Hola dominio personalizado nombre (dominio personal) tooyour web app y protéjala con un certificado SSL personalizado."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a><span data-ttu-id="44b7b-104">Agregar dominio personalizado y la aplicación web de Azure de SSL tooan</span><span class="sxs-lookup"><span data-stu-id="44b7b-104">Add custom domain and SSL tooan Azure web app</span></span>

<span data-ttu-id="44b7b-105">Este tutorial muestra cómo tooquickly asignar una aplicación de web de Azure de tooyour de nombre de dominio personalizado y, a continuación, protegerla con un certificado SSL personalizado.</span><span class="sxs-lookup"><span data-stu-id="44b7b-105">This tutorial shows you how tooquickly map a custom domain name tooyour Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="44b7b-106">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="44b7b-106">Before you begin</span></span>

<span data-ttu-id="44b7b-107">Antes de ejecutar este ejemplo, instalar hello [CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) localmente.</span><span class="sxs-lookup"><span data-stu-id="44b7b-107">Before running this sample, install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="44b7b-108">También necesita página de configuración de acceso administrativo toohello DNS para el proveedor de dominio respectivo.</span><span class="sxs-lookup"><span data-stu-id="44b7b-108">You also need administrative access toohello DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="44b7b-109">Por ejemplo, tooadd `www.contoso.com`, necesita toobe tooconfigure capaz de entradas DNS para `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="44b7b-109">For example, tooadd `www.contoso.com`, you need toobe able tooconfigure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="44b7b-110">Por último, deberá válido. Archivo PFX _y_ su contraseña de certificado SSL de Hola que desee tooupload y enlazar.</span><span class="sxs-lookup"><span data-stu-id="44b7b-110">Lastly, you need a valid .PFX file _and_ its password for hello SSL certificate you want tooupload and bind.</span></span> <span data-ttu-id="44b7b-111">Este certificado SSL debe ser el nombre de dominio personalizado de hello toosecure configurado que desee.</span><span class="sxs-lookup"><span data-stu-id="44b7b-111">This SSL certificate should be configured toosecure hello custom domain name you want.</span></span> <span data-ttu-id="44b7b-112">Hola ejemplo anterior, debe proteger el certificado SSL `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="44b7b-112">In hello above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="44b7b-113">Paso 1: Creación de una aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="44b7b-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="44b7b-114">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="44b7b-114">Log in tooAzure</span></span>

<span data-ttu-id="44b7b-115">Estamos ahora continuo toouse hello Azure CLI 2.0 en un recurso de ventana de terminal toocreate Hola necesarios toohost nuestra aplicación Node.js en Azure.</span><span class="sxs-lookup"><span data-stu-id="44b7b-115">We are now going toouse hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost our Node.js app in Azure.</span></span>  <span data-ttu-id="44b7b-116">Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="44b7b-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="44b7b-117">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="44b7b-117">Create a resource group</span></span>   
<span data-ttu-id="44b7b-118">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="44b7b-118">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="44b7b-119">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran recursos de Azure como aplicaciones web, bases de datos y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="44b7b-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="44b7b-120">toosee los posibles valores pueden usar para `---location`, usar hello `az appservice list-locations` comando de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="44b7b-120">toosee what possible values you can use for `---location`, use hello `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="44b7b-121">Creación de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="44b7b-121">Create an App Service plan</span></span>

<span data-ttu-id="44b7b-122">Crear un plan de servicio de aplicaciones con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="44b7b-122">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="44b7b-123">Hello en el ejemplo siguiente se crea un plan de servicio de aplicaciones denominado `myAppServicePlan` con hello **básica** nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="44b7b-123">hello following example creates an App Service plan named `myAppServicePlan` using hello **Basic** pricing tier.</span></span>

<span data-ttu-id="44b7b-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="44b7b-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="44b7b-125">Cuando se ha creado el plan de servicio de aplicación Hola, Hola CLI de Azure muestra información toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="44b7b-125">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a><span data-ttu-id="44b7b-126">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="44b7b-126">Create a web app</span></span>

<span data-ttu-id="44b7b-127">Ahora que ha creado un plan de servicio de aplicaciones, cree una aplicación web dentro de hello `myAppServicePlan` plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="44b7b-127">Now that an App Service plan has been created, create a web app within hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="44b7b-128">proporciona de aplicación web de Hola que está un hospedaje toodeploy de espacio en el código como le proporciona una dirección URL de hello tooview implementado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44b7b-128">hello web app gives your a hosting space toodeploy your code as well as provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="44b7b-129">Hola de uso [crear web de servicio de aplicaciones az](/cli/azure/appservice/web#create) comando toocreate hello web app.</span><span class="sxs-lookup"><span data-stu-id="44b7b-129">Use hello [az appservice web create](/cli/azure/appservice/web#create) command toocreate hello web app.</span></span> 

<span data-ttu-id="44b7b-130">En el siguiente comando de hello, sustituir por su propio nombre de aplicación único donde verá hello `<app_name>` marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="44b7b-130">In hello command below, please substitute your own unique app name where you see hello `<app_name>` placeholder.</span></span> <span data-ttu-id="44b7b-131">Este nombre único se utilizará como parte de Hola Hola predeterminado del nombre de dominio para la aplicación web de hello, por lo que el nombre de hello necesita toobe único en todas las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="44b7b-131">This unique name will be used as hello part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="44b7b-132">Más adelante puede asignar cualquier aplicación de web de toohello de entrada DNS personalizado antes de exponer tooyour a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="44b7b-132">You can later map any custom DNS entry toohello web app before you expose it tooyour users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="44b7b-133">Cuando se ha creado la aplicación web de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="44b7b-133">When hello web app has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

<span data-ttu-id="44b7b-134">De salida JSON, Hola `defaultHostName` muestra el nombre de dominio predeterminado de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="44b7b-134">From hello JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="44b7b-135">En el explorador, navegue toothis dirección.</span><span class="sxs-lookup"><span data-stu-id="44b7b-135">In your browser, navigate toothis address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="44b7b-137">Paso 2: Configuración de la asignación de DNS</span><span class="sxs-lookup"><span data-stu-id="44b7b-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="44b7b-138">En este paso, agregará una asignación de nombre de dominio predeterminado de la aplicación web de tooyour de dominio personalizado, `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="44b7b-138">In this step, you add a mapping from a custom domain tooyour web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="44b7b-139">Normalmente, este paso se realiza en el sitio web de su proveedor de dominios.</span><span class="sxs-lookup"><span data-stu-id="44b7b-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="44b7b-140">El sitio web de cada registrador de dominios es ligeramente diferente, por lo que debe consultar la documentación de su proveedor.</span><span class="sxs-lookup"><span data-stu-id="44b7b-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="44b7b-141">Sin embargo, estas son algunas directrices generales.</span><span class="sxs-lookup"><span data-stu-id="44b7b-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-tootoodns-management-page"></a><span data-ttu-id="44b7b-142">Navegar por la página de administración de tootooDNS</span><span class="sxs-lookup"><span data-stu-id="44b7b-142">Navigate tootooDNS management page</span></span>

<span data-ttu-id="44b7b-143">En primer lugar, inicie sesión en el sitio Web del registrador de dominios tooyour.</span><span class="sxs-lookup"><span data-stu-id="44b7b-143">First, log in tooyour domain registrar's website.</span></span>  

<span data-ttu-id="44b7b-144">A continuación, Buscar página Hola para administrar registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="44b7b-144">Then, find hello page for managing DNS records.</span></span> <span data-ttu-id="44b7b-145">Busque vínculos o áreas del sitio de hello con la etiqueta **nombre de dominio**, **DNS**, o **gestión de nombre de servidor**.</span><span class="sxs-lookup"><span data-stu-id="44b7b-145">Look for links or areas of hello site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="44b7b-146">A menudo, puede encontrar Hola vínculo Ver información de su cuenta y, a continuación, buscando un vínculo como **Mis dominios**.</span><span class="sxs-lookup"><span data-stu-id="44b7b-146">Often, you can find hello link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="44b7b-147">Una vez que haya encontrado esta página, busque un vínculo que le permita agregar o editar registros DNS.</span><span class="sxs-lookup"><span data-stu-id="44b7b-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="44b7b-148">Podría aparecer como **Archivo de zona** o **Registros DNS**, o bien como un vínculo de **Configuración avanzada**.</span><span class="sxs-lookup"><span data-stu-id="44b7b-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="44b7b-149">Creación de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="44b7b-149">Create a CNAME record</span></span>

<span data-ttu-id="44b7b-150">Agregar un registro CNAME que asigna el nombre de dominio de la aplicación de hello subdominio deseado nombre tooyour web predeterminado (`<app_name>.azurewebsites.net`, donde `<app_name>` es el nombre único de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="44b7b-150">Add a CNAME record that maps hello desired subdomain name tooyour web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="44b7b-151">Para hello `www.contoso.com` ejemplo, crear un CNAME que asigna hello `www` hostname demasiado`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="44b7b-151">For hello `www.contoso.com` example, you create a CNAME that maps hello `www` hostname too`<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a><span data-ttu-id="44b7b-152">Paso 3: configurar el dominio personalizado de hello en la aplicación web</span><span class="sxs-lookup"><span data-stu-id="44b7b-152">Step 3 - Configure hello custom domain on your web app</span></span>

<span data-ttu-id="44b7b-153">Cuando termine de configurar la asignación de nombre de host de hello en el sitio Web del proveedor de su dominio, le dominio personalizado de hello tooconfigure listo en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="44b7b-153">When you finish configuring hello hostname mapping in your domain provider's website, you're ready tooconfigure hello custom domain on your web app.</span></span> <span data-ttu-id="44b7b-154">Hola de uso [agregar az servicio de aplicaciones web config hostname](/cli/azure/appservice/web/config/hostname#add) comando tooadd esta configuración.</span><span class="sxs-lookup"><span data-stu-id="44b7b-154">Use hello [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command tooadd this configuration.</span></span> 

<span data-ttu-id="44b7b-155">En el siguiente comando de hello, sustituya `<app_name>` con el nombre de aplicación único y < your_custom_domain > con el nombre de dominio personalizado completo hello (p. ej. `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="44b7b-155">In hello command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with hello fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="44b7b-156">dominio personalizado de Hello ahora está totalmente asignado tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="44b7b-156">hello custom domain now is fully mapped tooyour web app.</span></span> <span data-ttu-id="44b7b-157">En el explorador, navegue toohello nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="44b7b-157">In your browser, navigate toohello custom domain name.</span></span> <span data-ttu-id="44b7b-158">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="44b7b-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a><span data-ttu-id="44b7b-160">Paso 4: enlazar una aplicación de web de tooyour de certificado SSL personalizada</span><span class="sxs-lookup"><span data-stu-id="44b7b-160">Step 4 - Bind a custom SSL certificate tooyour web app</span></span>

<span data-ttu-id="44b7b-161">Ahora tiene una aplicación web de Azure, con nombre de dominio de Hola que desee en la barra de direcciones del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="44b7b-161">You now have an Azure web app, with hello domain name you want in hello browser's address bar.</span></span> <span data-ttu-id="44b7b-162">Sin embargo, si navega toohello `https://<your_custom_domain>` ahora, obtendrá un error de certificado.</span><span class="sxs-lookup"><span data-stu-id="44b7b-162">However, if you navigate toohello `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="44b7b-164">Este error se produce porque la aplicación web no tiene todavía un enlace de certificado SSL que coincida con el nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="44b7b-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="44b7b-165">Sin embargo, no recibirá un error si se desplaza demasiado`https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="44b7b-165">However, you don't get an error if you navigate too`https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="44b7b-166">Esto es porque la aplicación, así como todas las aplicaciones de servicio de aplicaciones de Azure, está protegido con un certificado SSL para Hola Hola `*.azurewebsites.net` dominio comodín de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="44b7b-166">This is because your app, as well as all Azure App Service apps, is secured with hello SSL certificate for hello `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="44b7b-167">En Ordenar tooaccess su aplicación web por el nombre de dominio personalizado, deberá certificado SSL de toobind hello para la aplicación web de toohello de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="44b7b-167">In order tooaccess your web app by your custom domain name, you need toobind hello SSL certificate for your custom domain toohello web app.</span></span> <span data-ttu-id="44b7b-168">Esto lo hará en este paso.</span><span class="sxs-lookup"><span data-stu-id="44b7b-168">You will do it in this step.</span></span> 

### <a name="upload-hello-ssl-certificate"></a><span data-ttu-id="44b7b-169">Cargar el certificado SSL de Hola</span><span class="sxs-lookup"><span data-stu-id="44b7b-169">Upload hello SSL certificate</span></span>

<span data-ttu-id="44b7b-170">Cargar certificado SSL de hello para la aplicación web de tooyour de dominio personalizado mediante el uso de hello [configuración ssl carga de az servicio de aplicaciones web](/cli/azure/appservice/web/config/ssl#upload) comando.</span><span class="sxs-lookup"><span data-stu-id="44b7b-170">Upload hello SSL certificate for your custom domain tooyour web app by using hello [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="44b7b-171">En el siguiente comando de hello, sustituya `<app_name>` con el nombre de aplicación único, `<path_to_ptx_file>` con hello tooyour de ruta de acceso. Archivo PFX, y `<password>` con la contraseña del certificado.</span><span class="sxs-lookup"><span data-stu-id="44b7b-171">In hello command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with hello path tooyour .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="44b7b-172">Cuando se carga el certificado de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="44b7b-172">When hello certificate is uploaded, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

<span data-ttu-id="44b7b-173">De salida JSON, Hola `thumbprint` muestra la huella digital del certificado cargado.</span><span class="sxs-lookup"><span data-stu-id="44b7b-173">From hello JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="44b7b-174">Copie su valor para el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="44b7b-174">Copy its value for hello next step.</span></span>

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a><span data-ttu-id="44b7b-175">Enlazar la aplicación web de hello cargado SSL certificado toohello</span><span class="sxs-lookup"><span data-stu-id="44b7b-175">Bind hello uploaded SSL certificate toohello web app</span></span>

<span data-ttu-id="44b7b-176">La aplicación web tiene ahora el nombre de dominio personalizado de Hola que desee, y también tiene un certificado SSL que protege ese dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="44b7b-176">Your web app now has hello custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="44b7b-177">Hello solo lo izquierdo toodo es toobind Hola los certificados cargados toohello web app.</span><span class="sxs-lookup"><span data-stu-id="44b7b-177">hello only thing left toodo is toobind hello uploaded certificate toohello web app.</span></span> <span data-ttu-id="44b7b-178">Hacer esto mediante el uso de hello [el enlace de ssl de az servicio de aplicaciones web config](/cli/azure/appservice/web/config/ssl#bind) comando.</span><span class="sxs-lookup"><span data-stu-id="44b7b-178">You do this by using hello [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="44b7b-179">En el siguiente comando de hello, sustituya `<app_name>` con el nombre de aplicación único y `<thumbprint-from-previous-output>` con la huella digital de certificado de Hola que obtiene del comando anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="44b7b-179">In hello command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with hello certificate thumbprint that you get from hello previous command.</span></span> 

<span data-ttu-id="44b7b-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="44b7b-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="44b7b-181">Una vez certificado hello tooyour enlazado web app, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="44b7b-181">When hello certificate is bound tooyour web app, hello Azure CLI shows information similar toohello following example:</span></span>

<span data-ttu-id="44b7b-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="44b7b-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="44b7b-183">En el explorador, navegue extremo tooHTTPS de nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="44b7b-183">In your browser, navigate tooHTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="44b7b-184">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="44b7b-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="44b7b-186">Más recursos</span><span class="sxs-lookup"><span data-stu-id="44b7b-186">More resources</span></span>

<span data-ttu-id="44b7b-187">[Comprar y configurar un nombre de dominio personalizado en Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Compra y configuración de un certificado SSL para Azure App Service](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="44b7b-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
