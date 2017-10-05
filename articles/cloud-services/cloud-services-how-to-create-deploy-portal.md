---
title: "Creación e implementación de un servicio en la nube | Microsoft Docs"
description: Aprenda a crear e implementar un servicio en la nube mediante el Portal de Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: e5ce666f1d826c7901c9fd5e7fafe6171139c3ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="03900-103">Creación e implementación de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="03900-103">How to create and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03900-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="03900-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="03900-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="03900-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="03900-106">Azure Portal le ofrece dos formas de crear e implementar un servicio en la nube: *Creación rápida* y *Creación personalizada*.</span><span class="sxs-lookup"><span data-stu-id="03900-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="03900-107">En este artículo se explica cómo usar el método Creación rápida para crear un nuevo servicio en la nube y, a continuación, cómo usar **Cargar** para cargar e implementar un paquete de servicios en la nube en Azure.</span><span class="sxs-lookup"><span data-stu-id="03900-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="03900-108">Cuando usa este método, el Portal de Azure pone a su disposición los vínculos pertinentes para completar todos los requisitos que vaya necesitando sobre la marcha.</span><span class="sxs-lookup"><span data-stu-id="03900-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="03900-109">Si está listo para implementar su servicio en la nube una vez creado, puede hacer las dos cosas a la vez usando Creación personalizada.</span><span class="sxs-lookup"><span data-stu-id="03900-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="03900-110">Si tiene pensado publicar su servicio en la nube desde Visual Studio Team Services (VSTS), use Creación rápida y, a continuación, configure la publicación VSTS desde Creación rápida de Azure o el panel.</span><span class="sxs-lookup"><span data-stu-id="03900-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from the Azure Quickstart or the dashboard.</span></span> <span data-ttu-id="03900-111">Para más información, consulte [Entrega continua en Azure con Visual Studio Team Services][TFSTutorialForCloudService] o la ayuda de la página **Inicio rápido**.</span><span class="sxs-lookup"><span data-stu-id="03900-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="03900-112">Conceptos</span><span class="sxs-lookup"><span data-stu-id="03900-112">Concepts</span></span>
<span data-ttu-id="03900-113">Necesita tres componentes para implementar una aplicación como servicio en la nube en Azure:</span><span class="sxs-lookup"><span data-stu-id="03900-113">Three components are required to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="03900-114">**Definición de servicio**</span><span class="sxs-lookup"><span data-stu-id="03900-114">**Service Definition**</span></span>  
  <span data-ttu-id="03900-115">El archivo de definición de servicio en la nube (.csdef) define el modelo de servicio, incluyendo el número de roles.</span><span class="sxs-lookup"><span data-stu-id="03900-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="03900-116">**Configuración de servicio**</span><span class="sxs-lookup"><span data-stu-id="03900-116">**Service Configuration**</span></span>  
  <span data-ttu-id="03900-117">El archivo de configuración de servicio en la nube (.cscfg) proporciona opciones de configuración para los roles de servicio en la nube e individuales, incluyendo el número de instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="03900-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="03900-118">**Paquete de servicio**</span><span class="sxs-lookup"><span data-stu-id="03900-118">**Service Package**</span></span>  
  <span data-ttu-id="03900-119">El paquete de servicio (.cspkg) contiene el código y las configuraciones de la aplicación y el archivo de definición de servicio.</span><span class="sxs-lookup"><span data-stu-id="03900-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="03900-120">Puede obtener más información acerca de estas y cómo crear un paquete [aquí](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="03900-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="03900-121">Preparación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="03900-121">Prepare your app</span></span>
<span data-ttu-id="03900-122">Antes de implementar un servicio en la nube, debe crear el paquete de servicio en la nube (.cspkg) desde su código de aplicación y un archivo de configuración de servicio en la nube (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="03900-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="03900-123">El SDK de Azure proporciona herramientas para preparar estos archivos de implementación necesarios.</span><span class="sxs-lookup"><span data-stu-id="03900-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="03900-124">Puede instalar el SDK desde la página [Descargas de Azure](https://azure.microsoft.com/downloads/) , en el idioma en que prefiera implementar su código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="03900-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="03900-125">Hay tres características del servicio en la nube que requieren configuraciones especiales antes de exportar un paquete de servicio:</span><span class="sxs-lookup"><span data-stu-id="03900-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="03900-126">Si desea implementar un servicio en la nube que utilice Capa de sockets seguros (SSL) para el cifrado de datos, [configure la aplicación](cloud-services-configure-ssl-certificate-portal.md#modify) para SSL.</span><span class="sxs-lookup"><span data-stu-id="03900-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="03900-127">Si desea configurar una conexión de Escritorio remoto a instancias de rol, [configure los roles](cloud-services-role-enable-remote-desktop-new-portal.md) para Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="03900-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="03900-128">Si desea configurar una supervisión exhaustiva para su servicio en la nube, habilite Diagnósticos de Azure para el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="03900-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="03900-129">*Supervisión mínima* (nivel predeterminado de supervisión) usa contadores de rendimiento recopilados de los sistemas operativos host para las instancias de rol (máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="03900-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="03900-130">*supervisión detallada* recopila métricas adicionales basadas en los datos del rendimiento dentro de las instancias de rol para permitir un análisis más profundo de los problemas que se producen durante el procesamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03900-130">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="03900-131">Para obtener información acerca de cómo habilitar Diagnósticos de Azure, consulte [Habilitación de Diagnósticos en Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="03900-131">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="03900-132">Para crear un servicio en la nube con implementaciones de roles web o de trabajo, debe [crear el paquete de servicio](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="03900-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="03900-133">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="03900-133">Before you begin</span></span>
* <span data-ttu-id="03900-134">Si no ha instalado el SDK de Azure, haga clic en **Instalación de SDK de Azure** para abrir la [página Descargas de Azure](https://azure.microsoft.com/downloads/)y, a continuación, descargue el SDK en el idioma en que prefiera desarrollar el código.</span><span class="sxs-lookup"><span data-stu-id="03900-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="03900-135">(Tendrá la oportunidad de hacer esto más tarde).</span><span class="sxs-lookup"><span data-stu-id="03900-135">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="03900-136">Si hay instancias de rol que necesitan certificados, créelos.</span><span class="sxs-lookup"><span data-stu-id="03900-136">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="03900-137">Los servicios en la nube requieren un archivo .pfx con una clave privada.</span><span class="sxs-lookup"><span data-stu-id="03900-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="03900-138">Puede cargar los certificados en Azure al crear e implementar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="03900-138">You can upload the certificates to Azure as you create and deploy the cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="03900-139">Creación e implementación</span><span class="sxs-lookup"><span data-stu-id="03900-139">Create and deploy</span></span>
1. <span data-ttu-id="03900-140">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="03900-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="03900-141">Haga clic en **Nuevo > Compute**, luego desplácese hacia abajo y haga clic en **Servicio en la nube**.</span><span class="sxs-lookup"><span data-stu-id="03900-141">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span></span>

    ![Publicación del servicio en la nube](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="03900-143">En la nueva hoja **Servicio en la nube**, escriba un valor para **Nombre DNS**.</span><span class="sxs-lookup"><span data-stu-id="03900-143">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span></span>
4. <span data-ttu-id="03900-144">Cree un nuevo **Grupo de recursos** o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="03900-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="03900-145">Seleccione una **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="03900-145">Select a **Location**.</span></span>
6. <span data-ttu-id="03900-146">Haga clic en **Paquete**.</span><span class="sxs-lookup"><span data-stu-id="03900-146">Click **Package**.</span></span> <span data-ttu-id="03900-147">Se abrirá la hoja **Upload a package** (Cargar un paquete).</span><span class="sxs-lookup"><span data-stu-id="03900-147">This will open the **Upload a package** blade.</span></span> <span data-ttu-id="03900-148">Rellene todos los campos obligatorios.</span><span class="sxs-lookup"><span data-stu-id="03900-148">Fill in the required fields.</span></span> <span data-ttu-id="03900-149">Si cualquiera de los roles contiene una sola instancia, asegúrese de que la casilla **Implementar aunque uno o varios roles contengan una sola instancia** esté seleccionada.</span><span class="sxs-lookup"><span data-stu-id="03900-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="03900-150">Asegúrese de que la opción **Iniciar implementación** esté seleccionada.</span><span class="sxs-lookup"><span data-stu-id="03900-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="03900-151">Haga clic en **Aceptar** para cerrar la hoja **Cargar un paquete**.</span><span class="sxs-lookup"><span data-stu-id="03900-151">Click **OK** which will close the **Upload a package** blade.</span></span>
9. <span data-ttu-id="03900-152">Si no tiene ningún certificado para agregar, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="03900-152">If you do not have any certificates to add, click **Create**.</span></span>

    ![Publicación del servicio en la nube](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="03900-154">Carga de un certificado</span><span class="sxs-lookup"><span data-stu-id="03900-154">Upload a certificate</span></span>
<span data-ttu-id="03900-155">Si el paquete de implementación se [configuró para usar certificados](cloud-services-configure-ssl-certificate-portal.md#modify), puede cargar el certificado ahora.</span><span class="sxs-lookup"><span data-stu-id="03900-155">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span></span>

1. <span data-ttu-id="03900-156">Seleccione **Certificados** y, en la hoja **Agregar certificados**, seleccione el archivo .pfx del certificado SSL y proporcione la **contraseña** del certificado,</span><span class="sxs-lookup"><span data-stu-id="03900-156">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span></span>
2. <span data-ttu-id="03900-157">Haga clic en **Adjuntar certificado** y luego en **Aceptar** en la hoja **Agregar certificados**.</span><span class="sxs-lookup"><span data-stu-id="03900-157">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span></span>
3. <span data-ttu-id="03900-158">Haga clic en **Crear** en la hoja **Servicio en la nube**.</span><span class="sxs-lookup"><span data-stu-id="03900-158">Click **Create** on the **Cloud Service** blade.</span></span> <span data-ttu-id="03900-159">Cuando la implementación haya llegado al estado **Listo** , puede continuar con los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="03900-159">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span></span>

    ![Publicación del servicio en la nube](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="03900-161">Compruebe que la implementación se haya completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="03900-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="03900-162">Haga clic en la instancia de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="03900-162">Click the cloud service instance.</span></span>

    <span data-ttu-id="03900-163">El estado debería mostrar que el servicio está **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="03900-163">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="03900-164">En **Essentials**, haga clic en la **URL del sitio** para abrir el servicio en la nube en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="03900-164">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="03900-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03900-166">Next steps</span></span>
* <span data-ttu-id="03900-167">[Configuración general de su servicio en la nube](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03900-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="03900-168">Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03900-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="03900-169">[Administración de su servicio en la nube](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03900-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="03900-170">Configuración de [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03900-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
