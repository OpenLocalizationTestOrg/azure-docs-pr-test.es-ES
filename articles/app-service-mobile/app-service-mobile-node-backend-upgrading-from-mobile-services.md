---
title: "Actualización de Servicios móviles a Servicio de aplicaciones de Azure - Node.js"
description: "Aprenda a actualizar fácilmente la aplicación de Servicios móviles a una aplicación móvil del Servicio de aplicaciones."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ce0572e85c258aa377c3eea7923d43a30c935bb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-to-app-service"></a><span data-ttu-id="086a3-103">Actualización del Servicio móvil de Azure de Node.js existente a Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="086a3-103">Upgrade your existing Node.js Azure Mobile Service to App Service</span></span>
<span data-ttu-id="086a3-104">Aplicaciones móviles del Servicio de aplicaciones es una nueva forma de crear aplicaciones móviles con Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="086a3-104">App Service Mobile is a new way to build mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="086a3-105">Para más información, vea [¿Qué es Aplicaciones móviles?].</span><span class="sxs-lookup"><span data-stu-id="086a3-105">To learn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="086a3-106">En este tema se describe cómo actualizar una aplicación back-end de Node.js existente en Servicios móviles de Azure a una nueva instancia de Aplicaciones móviles del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="086a3-106">This topic describes how to upgrade an existing Node.js backend application from Azure Mobile Services to a new App Service Mobile Apps.</span></span> <span data-ttu-id="086a3-107">Cuando realice esta migración, la aplicación de Servicios móviles existente puede continuar funcionando.</span><span class="sxs-lookup"><span data-stu-id="086a3-107">While you perform this upgrade, your existing Mobile Services application can continue to operate.</span></span>  <span data-ttu-id="086a3-108">Si necesita actualizar una aplicación back-end de Node.js, consulte [Actualización de Mobile Services de .NET](app-service-mobile-net-upgrading-from-mobile-services.md).</span><span class="sxs-lookup"><span data-stu-id="086a3-108">If you need to upgrade a Node.js backend application, refer to [Upgrading your .NET Mobile Services](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="086a3-109">Cuando un back-end móvil se actualiza a Servicio de aplicaciones de Azure, accede a todas las características de Servicio de aplicaciones y se factura conforme a los [precios del Servicio de aplicaciones], no según los precios de Servicios móviles.</span><span class="sxs-lookup"><span data-stu-id="086a3-109">When a mobile backend is upgraded to Azure App Service, it has access to all App Service features and are billed according to [App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="086a3-110">Migración frente a actualización</span><span class="sxs-lookup"><span data-stu-id="086a3-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="086a3-111">Se recomienda [realizar una migración](app-service-mobile-migrating-from-mobile-services.md) antes de pasar por una actualización.</span><span class="sxs-lookup"><span data-stu-id="086a3-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="086a3-112">De este modo, puede colocar las dos versiones de la aplicación en el mismo Plan del Servicio de aplicaciones y no incurrir en ningún coste adicional.</span><span class="sxs-lookup"><span data-stu-id="086a3-112">This way, you can put both versions of your application on the same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a><span data-ttu-id="086a3-113">Mejoras en el SDK de servidor para Node.js de Aplicaciones móviles</span><span class="sxs-lookup"><span data-stu-id="086a3-113">Improvements in Mobile Apps Node.js server SDK</span></span>
<span data-ttu-id="086a3-114">La actualización al nuevo [SDK de Aplicaciones móviles](https://www.npmjs.com/package/azure-mobile-apps) ofrece muchas mejoras, entre las que se incluyen:</span><span class="sxs-lookup"><span data-stu-id="086a3-114">Upgrading to the new [Mobile Apps SDK](https://www.npmjs.com/package/azure-mobile-apps) provides a lot of improvements, including:</span></span>

* <span data-ttu-id="086a3-115">Basado en la [plataforma Express](http://expressjs.com/en/index.html), el nuevo SDK para Node es ligero y está diseñado para mantenerse al día con nuevas versiones de Node a medida que salen.</span><span class="sxs-lookup"><span data-stu-id="086a3-115">Based on the [Express framework](http://expressjs.com/en/index.html), the new Node SDK is light-weight and designed to keep up with new Node versions as they come out.</span></span> <span data-ttu-id="086a3-116">Puede personalizar el comportamiento de la aplicación con middleware de Express.</span><span class="sxs-lookup"><span data-stu-id="086a3-116">You can customize the application behavior with Express middleware.</span></span>
* <span data-ttu-id="086a3-117">Ofrece mejoras de rendimiento significativas en comparación con el SDK de Servicios móviles.</span><span class="sxs-lookup"><span data-stu-id="086a3-117">Significant performance improvements compared to the Mobile Services SDK.</span></span>
* <span data-ttu-id="086a3-118">Ahora puede hospedar un sitio web junto con el back-end móvil; asimismo, es fácil agregar el Azure Mobile SDK a cualquier aplicación v4 existente.</span><span class="sxs-lookup"><span data-stu-id="086a3-118">You can now host a website together with your mobile backend; similarly, it's easy to add the Azure Mobile SDK to any existing express.v4 application.</span></span>
* <span data-ttu-id="086a3-119">Creado para desarrollo multiplataforma y local, el SDK de Aplicaciones móviles se puede desarrollar y ejecutar localmente en plataformas Windows, Linux y OSX.</span><span class="sxs-lookup"><span data-stu-id="086a3-119">Built for cross-platform and local development, the Mobile Apps SDK can be developed and run locally on Windows, Linux, and OSX platforms.</span></span> <span data-ttu-id="086a3-120">Ahora es fácil usar técnicas de desarrollo comunes de Node como, por ejemplo, ejecutar pruebas [Mocha](https://mochajs.org/) antes de la implementación.</span><span class="sxs-lookup"><span data-stu-id="086a3-120">It's now easy to use common Node development techniques like running [Mocha](https://mochajs.org/) tests prior to deployment.</span></span>

## <span data-ttu-id="086a3-121"><a name="overview"></a>Información general básica de actualización</span><span class="sxs-lookup"><span data-stu-id="086a3-121"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="086a3-122">Para facilitar la actualización de un back-end de Node.js, el Servicio de aplicaciones de Azure ha proporcionado un paquete de compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="086a3-122">To aid in upgrading a Node.js backend, Azure App Service has provided a compatibility package.</span></span>  <span data-ttu-id="086a3-123">Tras la actualización, tendrá un nuevo sitio que se puede implementar en un nuevo sitio del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="086a3-123">After upgrade, you will have a niew site that can be deployed to a new App Service site.</span></span>

<span data-ttu-id="086a3-124">Los SDK de cliente de Servicios móviles **no** son compatibles con el nuevo SDK de servidor de Aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="086a3-124">The Mobile Services client SDKs are **not** compatible with the new Mobile Apps server SDK.</span></span> <span data-ttu-id="086a3-125">A fin de ofrecer continuidad del servicio para la aplicación, no debe publicar cambios en un sitio que actualmente presta servicio a clientes publicados.</span><span class="sxs-lookup"><span data-stu-id="086a3-125">In order to provide continuity of service for your app, you should not publish changes to a site currently serving published clients.</span></span> <span data-ttu-id="086a3-126">En su lugar, debe crear una aplicación móvil que actúe como duplicado.</span><span class="sxs-lookup"><span data-stu-id="086a3-126">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="086a3-127">Puede colocar esta aplicación en el mismo Plan del Servicio de aplicaciones para evitar incurrir en costos financieros adicionales.</span><span class="sxs-lookup"><span data-stu-id="086a3-127">You can put this application on the same App Service plan to avoid incurring additional financial cost.</span></span>

<span data-ttu-id="086a3-128">Entonces tendrá dos versiones de la aplicación: una que permanece igual y presta servicio a las aplicaciones publicadas en su estado natural, y otra que después se puede actualizar y destinar a una nueva versión del cliente.</span><span class="sxs-lookup"><span data-stu-id="086a3-128">You will then have two versions of the application: one that stays the same and serves published apps in the wild, and the other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="086a3-129">Puede mover y probar el código a su ritmo, pero debe asegurarse de que las correcciones de errores se apliquen a ambas.</span><span class="sxs-lookup"><span data-stu-id="086a3-129">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied to both.</span></span> <span data-ttu-id="086a3-130">Cuando crea que la cantidad que elija de aplicaciones cliente en estado natural se han actualizado a la versión más reciente, puede eliminar si quiere la aplicación migrada original.</span><span class="sxs-lookup"><span data-stu-id="086a3-130">Once you feel that a desired number of client apps in the wild have updated to the latest version, you can delete the original migrated app if you desire.</span></span> <span data-ttu-id="086a3-131">No incurre en costos monetarios adicionales, si se hospeda en el mismo Plan del Servicio de aplicaciones que la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="086a3-131">It doesn't incur any additional monetary costs, if hosted in the same App Service plan as your Mobile App.</span></span>

<span data-ttu-id="086a3-132">El esquema completo del proceso de actualización es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="086a3-132">The full outline for the upgrade process is as follows:</span></span>

1. <span data-ttu-id="086a3-133">Descargue el servicio móvil de Azure existente (migrado).</span><span class="sxs-lookup"><span data-stu-id="086a3-133">Download your existing (migrated) Azure Mobile Service.</span></span>
2. <span data-ttu-id="086a3-134">Convierta el proyecto en una aplicación móvil de Azure mediante el paquete de compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="086a3-134">Convert the project to an Azure Mobile App using the compatibility package.</span></span>
3. <span data-ttu-id="086a3-135">Corrija cualquier diferencia (como la configuración de autenticación).</span><span class="sxs-lookup"><span data-stu-id="086a3-135">Correct any differences (such as authentication settings).</span></span>
4. <span data-ttu-id="086a3-136">Implemente el proyecto de aplicación móvil de Azure convertido en un nuevo Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="086a3-136">Deploy your converted Azure Mobile App project to a new App Service.</span></span>
5. <span data-ttu-id="086a3-137">Publique una nueva versión de la aplicación cliente que utilice la nueva aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="086a3-137">Release a new version of your client application that use the new Mobile App.</span></span>
6. <span data-ttu-id="086a3-138">(Opcional) Eliminar la aplicación de servicio móvil migrada original</span><span class="sxs-lookup"><span data-stu-id="086a3-138">(Optional) Delete your original migrated mobile service app.</span></span>

<span data-ttu-id="086a3-139">La eliminación puede tener lugar cuando no vea tráfico alguno en el servicio móvil migrado original.</span><span class="sxs-lookup"><span data-stu-id="086a3-139">Deletion can occur when you don't see any traffic on your original migrated mobile service.</span></span>

## <span data-ttu-id="086a3-140"><a name="install-npm-package"></a> Instalación de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="086a3-140"><a name="install-npm-package"></a> Install the Pre-requisites</span></span>
<span data-ttu-id="086a3-141">Debe instalar [Node] en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="086a3-141">You should install [Node] on your local machine.</span></span>  <span data-ttu-id="086a3-142">También debe instalar el paquete de compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="086a3-142">You should also install the compatibility package.</span></span>  <span data-ttu-id="086a3-143">Después de instalar Node, puede ejecutar el comando siguiente desde un nuevo cmd o símbolo del sistema de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="086a3-143">After Node is installed, you can run the following command from a new cmd or PowerShell prompt:</span></span>

```npm i -g azure-mobile-apps-compatibility```

## <span data-ttu-id="086a3-144"><a name="obtain-ams-scripts"></a> Obtención de los scripts de Servicios móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="086a3-144"><a name="obtain-ams-scripts"></a> Obtain your Azure Mobile Services Scripts</span></span>
* <span data-ttu-id="086a3-145">Inicie sesión en el [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="086a3-145">Log in to the [Azure Portal].</span></span>
* <span data-ttu-id="086a3-146">Mediante **Todos los recursos** o **App Services**, busque el sitio de Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="086a3-146">Using **All Resources** or **App Services**, find your Mobile Services site.</span></span>
* <span data-ttu-id="086a3-147">En el sitio, haga clic en **Herramientas** -> **Kudu** -> **Ir** para abrir el sitio de Kudu.</span><span class="sxs-lookup"><span data-stu-id="086a3-147">Within the site, click on **Tools** -> **Kudu** -> **Go** to open the Kudu site.</span></span>
* <span data-ttu-id="086a3-148">Haga clic en **Debug Console** -> **PowerShell** para abrir la consola de depuración.</span><span class="sxs-lookup"><span data-stu-id="086a3-148">Click on **Debug Console** -> **PowerShell** to open the Debug console.</span></span>
* <span data-ttu-id="086a3-149">Vaya a `site/wwwroot/App_Data/config` haciendo clic por turnos en cada directorio.</span><span class="sxs-lookup"><span data-stu-id="086a3-149">Navigate to `site/wwwroot/App_Data/config` by clicking on each directory in turn</span></span>
* <span data-ttu-id="086a3-150">Haga clic en el icono de descarga junto al directorio `scripts` .</span><span class="sxs-lookup"><span data-stu-id="086a3-150">Click on the download icon next to the `scripts` directory.</span></span>

<span data-ttu-id="086a3-151">Se descargarán los scripts en formato ZIP.</span><span class="sxs-lookup"><span data-stu-id="086a3-151">This will download the scripts in ZIP format.</span></span>  <span data-ttu-id="086a3-152">Cree un nuevo directorio en la máquina local y desempaquete el archivo `scripts.ZIP` dentro del directorio.</span><span class="sxs-lookup"><span data-stu-id="086a3-152">Create a new directory on your local machine and unpack the `scripts.ZIP` file within the directory.</span></span>  <span data-ttu-id="086a3-153">Se crea un directorio `scripts` .</span><span class="sxs-lookup"><span data-stu-id="086a3-153">This will create a `scripts` directory.</span></span>

## <span data-ttu-id="086a3-154"><a name="scaffold-app"></a> Realización de scaffold del nuevo back-end de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="086a3-154"><a name="scaffold-app"></a> Scaffold the new Azure Mobile Apps backend</span></span>
<span data-ttu-id="086a3-155">Ejecute el siguiente comando desde el directorio que contiene el directorio de scripts:</span><span class="sxs-lookup"><span data-stu-id="086a3-155">Run the following command from the directory containing the scripts directory:</span></span>

```scaffold-mobile-app scripts out```

<span data-ttu-id="086a3-156">Se crea un back-end de Aplicaciones móviles de Azure con scaffold en el directorio `out` .</span><span class="sxs-lookup"><span data-stu-id="086a3-156">This will create a scaffolded Azure Mobile Apps backend in the `out` directory.</span></span>  <span data-ttu-id="086a3-157">Aunque no es necesario, conviene comprobar el directorio `out` en un repositorio de código fuente de su elección.</span><span class="sxs-lookup"><span data-stu-id="086a3-157">Although not required, it's a good idea to check the `out` directory into a source code repository of your choice.</span></span>

## <span data-ttu-id="086a3-158"><a name="deploy-ama-app"></a> Implementación del back-end de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="086a3-158"><a name="deploy-ama-app"></a> Deploy your Azure Mobile Apps backend</span></span>
<span data-ttu-id="086a3-159">Durante la implementación, deberá realizar estos pasos:</span><span class="sxs-lookup"><span data-stu-id="086a3-159">During deployment, you will need to do the following:</span></span>

1. <span data-ttu-id="086a3-160">Cree una nueva aplicación móvil en el [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="086a3-160">Create a new Mobile App in the [Azure Portal].</span></span>
2. <span data-ttu-id="086a3-161">Ejecute el script `createViews.sql` en la base de datos conectada.</span><span class="sxs-lookup"><span data-stu-id="086a3-161">Run the `createViews.sql` script on your connected database.</span></span>
3. <span data-ttu-id="086a3-162">Vincule la base de datos que está vinculada a su servicio móvil a su nuevo Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="086a3-162">Link the database that is linked to your Mobile Service to your new App Service.</span></span>
4. <span data-ttu-id="086a3-163">Vincule otros recursos (como los Centros de notificaciones) al nuevo Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="086a3-163">Link any other resources (such as Notification Hubs) to the new App Service.</span></span>
5. <span data-ttu-id="086a3-164">Implemente el código generado en el nuevo sitio.</span><span class="sxs-lookup"><span data-stu-id="086a3-164">Deploy the generated code to your new site.</span></span>

### <a name="create-a-new-mobile-app"></a><span data-ttu-id="086a3-165">Creación de una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="086a3-165">Create a new Mobile App</span></span>
1. <span data-ttu-id="086a3-166">Inicie sesión en el [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="086a3-166">Log in at the [Azure Portal].</span></span>
2. <span data-ttu-id="086a3-167">Haga clic en **+NUEVO** > **Web y móvil** > **Aplicación móvil** y, después, proporcione un nombre para el back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="086a3-167">Click **+NEW** > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="086a3-168">En **Grupo de recursos**, seleccione un grupo de recursos existente o cree uno nuevo (con el mismo nombre que su aplicación).</span><span class="sxs-lookup"><span data-stu-id="086a3-168">For the **Resource Group**, select an existing resource group, or create a new one (using the same name as your app.)</span></span>

    <span data-ttu-id="086a3-169">Puede seleccionar un plan de Servicio de aplicaciones ya existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="086a3-169">You can either select another App Service plan or create a new one.</span></span> <span data-ttu-id="086a3-170">Para más información acerca de los planes de Servicio de aplicaciones y cómo crear un nuevo plan en un plan de tarifa diferente en la ubicación deseada, consulte [Introducción detallada sobre los planes del Servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="086a3-170">For more about App Services plans and how to create a new plan in a different pricing tier and in your desired location, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
4. <span data-ttu-id="086a3-171">Para **Plan del Servicio de aplicaciones**, se selecciona el plan predeterminado (en el [nivel estándar](https://azure.microsoft.com/pricing/details/app-service/)).</span><span class="sxs-lookup"><span data-stu-id="086a3-171">For the **App Service plan**, the default plan (in the [Standard tier](https://azure.microsoft.com/pricing/details/app-service/)) is selected.</span></span> <span data-ttu-id="086a3-172">También puede seleccionar otro plan o [crear uno](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="086a3-172">You can also  select a different plan, or [create a new one](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span></span> <span data-ttu-id="086a3-173">La configuración del plan del Servicio de aplicaciones determina la [ubicación, las características, el costo y los recursos de proceso](https://azure.microsoft.com/pricing/details/app-service/) asociados a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="086a3-173">The App Service plan's settings determine the [location, features, cost and compute resources](https://azure.microsoft.com/pricing/details/app-service/) associated with your app.</span></span>

    <span data-ttu-id="086a3-174">Después de decidir el plan, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="086a3-174">After you decide on the plan, click **Create**.</span></span> <span data-ttu-id="086a3-175">Esto crea el back-end de aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="086a3-175">This creates the Mobile App backend.</span></span>

### <a name="run-createviewssql"></a><span data-ttu-id="086a3-176">Ejecución de CreateViews.SQL</span><span class="sxs-lookup"><span data-stu-id="086a3-176">Run CreateViews.SQL</span></span>
<span data-ttu-id="086a3-177">La aplicación con scaffold contiene un archivo llamado `createViews.sql`.</span><span class="sxs-lookup"><span data-stu-id="086a3-177">The scaffolded app contains a file called `createViews.sql`.</span></span>  <span data-ttu-id="086a3-178">Este script debe ejecutarse con la base de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="086a3-178">This script must be executed against the target database.</span></span>  <span data-ttu-id="086a3-179">La cadena de conexión de la base de datos de destino puede obtenerse del servicio móvil migrado en la hoja **Configuración** en **Cadenas de conexión**.</span><span class="sxs-lookup"><span data-stu-id="086a3-179">The connection string for the target database can be obtained from your migrated mobile service from the **Settings** blade under **Connection Strings**.</span></span>  <span data-ttu-id="086a3-180">Se llama `MS_TableConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="086a3-180">It is named `MS_TableConnectionString`.</span></span>

<span data-ttu-id="086a3-181">Puede ejecutar este script desde SQL Server Management Studio o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="086a3-181">You can run this script from within SQL Server Management Studio or Visual Studio.</span></span>

### <a name="link-the-database-to-your-app-service"></a><span data-ttu-id="086a3-182">Vinculación de la base de datos al Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="086a3-182">Link the Database to your App Service</span></span>
<span data-ttu-id="086a3-183">Vincule la base de datos existente a su Servicio de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="086a3-183">Link the existing database to your App Service:</span></span>

* <span data-ttu-id="086a3-184">En el [Portal de Azure], abra el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="086a3-184">In the [Azure Portal], open your App Service.</span></span>
* <span data-ttu-id="086a3-185">Seleccione **Toda la configuración** -> **Conexiones de datos**.</span><span class="sxs-lookup"><span data-stu-id="086a3-185">Select **All Settings** -> **Data Connections**.</span></span>
* <span data-ttu-id="086a3-186">Haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="086a3-186">Click on **+ Add**.</span></span>
* <span data-ttu-id="086a3-187">En la lista desplegable, seleccione **Base de datos SQL**</span><span class="sxs-lookup"><span data-stu-id="086a3-187">In the drop-down, select **SQL Database**</span></span>
* <span data-ttu-id="086a3-188">En **SQL Database**, seleccione la base de datos existente y haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="086a3-188">Under **SQL Database**, select your existing database, then click on **Select**.</span></span>
* <span data-ttu-id="086a3-189">En **Cadena de conexión**, escriba el nombre de usuario y la contraseña de la base de datos y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="086a3-189">Under **Connection string**, enter the username and password for the database, then click on **OK**.</span></span>
* <span data-ttu-id="086a3-190">En la hoja **Add data connections** (Agregar conexiones de datos), haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="086a3-190">In the **Add data connections** blade, click on **OK**.</span></span>

<span data-ttu-id="086a3-191">El nombre de usuario y la contraseña se pueden ver en la cadena de conexión de la base de datos de destino del servicio móvil migrado.</span><span class="sxs-lookup"><span data-stu-id="086a3-191">The username and password can be found by viewing the Connection String for the target database in your migrated Mobile Service.</span></span>

### <a name="set-up-authentication"></a><span data-ttu-id="086a3-192">Configuración de la autenticación</span><span class="sxs-lookup"><span data-stu-id="086a3-192">Set up authentication</span></span>
<span data-ttu-id="086a3-193">El servicio Aplicaciones móviles de Azure le permite configurar la autenticación de Azure Active Directory, Facebook, Google, Microsoft y Twitter en el servicio.</span><span class="sxs-lookup"><span data-stu-id="086a3-193">Azure Mobile Apps allows you to configure Azure Active Directory, Facebook, Google, Microsoft and Twitter authentication within the service.</span></span>  <span data-ttu-id="086a3-194">La autenticación personalizada deberá desarrollarse por separado.</span><span class="sxs-lookup"><span data-stu-id="086a3-194">Custom authentication will need to be developed separately.</span></span>  <span data-ttu-id="086a3-195">Para más información, consulte la documentación sobre los [conceptos de autenticación] y el [inicio rápido de autenticación].</span><span class="sxs-lookup"><span data-stu-id="086a3-195">Refer to the [Authentication Concepts] documentation and [Authentication Quickstart] documentation for more information.</span></span>  

## <span data-ttu-id="086a3-196"><a name="updating-clients"></a>Actualización de los clientes móviles</span><span class="sxs-lookup"><span data-stu-id="086a3-196"><a name="updating-clients"></a>Update Mobile clients</span></span>
<span data-ttu-id="086a3-197">Cuando tenga un back-end de aplicación móvil operativo, podrá trabajar en una nueva versión de la aplicación cliente que lo usa.</span><span class="sxs-lookup"><span data-stu-id="086a3-197">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="086a3-198">Aplicaciones móviles incluye también una nueva versión de los SDK de cliente y, de forma similar a la actualización del servidor anterior, tendrá que quitar todas las referencias a los SDK de Servicios móviles antes de instalar las versiones de Aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="086a3-198">Mobile Apps also includes a new version of the client SDKs, and similar to the server upgrade above, you will need to remove all references to the Mobile Services SDKs before installing the Mobile Apps versions.</span></span>

<span data-ttu-id="086a3-199">Uno de los principales cambios entre las versiones es que los constructores ya no requieren una clave de aplicación.</span><span class="sxs-lookup"><span data-stu-id="086a3-199">One of the main changes between the versions is that the constructors no longer require an application key.</span></span>
<span data-ttu-id="086a3-200">Ahora basta con pasar la dirección URL de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="086a3-200">You now simply pass in the URL of your Mobile App.</span></span> <span data-ttu-id="086a3-201">Por ejemplo, en los clientes .NET, el constructor `MobileServiceClient` es ahora:</span><span class="sxs-lookup"><span data-stu-id="086a3-201">For example, on the .NET clients, the `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of the Mobile App
        );

<span data-ttu-id="086a3-202">Encontrará información sobre cómo instalar los nuevos SDK y cómo usar la nueva estructura a través de los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="086a3-202">You can read about installing the new SDKs and using the new structure via the links below:</span></span>

* [<span data-ttu-id="086a3-203">Versión de Android 2.2 o posterior</span><span class="sxs-lookup"><span data-stu-id="086a3-203">Android version 2.2 or later</span></span>](app-service-mobile-android-how-to-use-client-library.md)
* [<span data-ttu-id="086a3-204">iOS versión 3.0.0 o posterior</span><span class="sxs-lookup"><span data-stu-id="086a3-204">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="086a3-205">.NET (Windows/Xamarin) versión 2.0.0 o posterior</span><span class="sxs-lookup"><span data-stu-id="086a3-205">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)
* [<span data-ttu-id="086a3-206">Apache Cordova versión 2.0 o posterior</span><span class="sxs-lookup"><span data-stu-id="086a3-206">Apache Cordova version 2.0 or later</span></span>](app-service-mobile-cordova-how-to-use-client-library.md)

<span data-ttu-id="086a3-207">Si la aplicación hace uso de notificaciones de inserción, tome nota de las instrucciones de registro específicas para cada plataforma, ya que también ha habido algunos cambios al respecto.</span><span class="sxs-lookup"><span data-stu-id="086a3-207">If your application makes use of push notifications, make note of the specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="086a3-208">Cuando tenga la nueva versión de cliente lista, pruébela en el proyecto de servidor actualizado.</span><span class="sxs-lookup"><span data-stu-id="086a3-208">When you have the new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="086a3-209">Después de comprobar que funciona, puede publicar una nueva versión de la aplicación para clientes.</span><span class="sxs-lookup"><span data-stu-id="086a3-209">After validating that it works, you can release a new version of your application to customers.</span></span> <span data-ttu-id="086a3-210">Al final, cuando los clientes hayan tenido ocasión de recibir estas actualizaciones, puede eliminar la versión de Servicios móviles de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="086a3-210">Eventually, once your customers have had a chance to receive these updates, you can delete the Mobile Services version of your app.</span></span> <span data-ttu-id="086a3-211">Llegados a este punto, ha actualizado completamente a una aplicación móvil del Servicio de aplicaciones mediante el SDK de servidor de Aplicaciones móviles más reciente.</span><span class="sxs-lookup"><span data-stu-id="086a3-211">At this point, you have completely upgraded to an App Service Mobile App using the latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

<span data-ttu-id="086a3-212">[Azure portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="086a3-212">[Azure portal]: https://portal.azure.com/</span></span>
[Azure classic portal]: https://manage.windowsazure.com/
<span data-ttu-id="086a3-213">[¿Qué es Aplicaciones móviles?]: app-service-mobile-value-prop.md</span><span class="sxs-lookup"><span data-stu-id="086a3-213">[What are Mobile Apps?]: app-service-mobile-value-prop.md</span></span>
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications to your mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication to your mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How to use the .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services to an App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service to App Service]: app-service-mobile-migrating-from-mobile-services.md
<span data-ttu-id="086a3-214">[precios del Servicio de aplicaciones]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span><span class="sxs-lookup"><span data-stu-id="086a3-214">[App Service pricing]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span></span>
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
<span data-ttu-id="086a3-215">[conceptos de autenticación]: ../app-service/app-service-authentication-overview.md</span><span class="sxs-lookup"><span data-stu-id="086a3-215">[Authentication Concepts]: ../app-service/app-service-authentication-overview.md</span></span>
<span data-ttu-id="086a3-216">[inicio rápido de autenticación]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="086a3-216">[Authentication Quickstart]: app-service-mobile-auth.md</span></span>

<span data-ttu-id="086a3-217">[Portal de Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="086a3-217">[Azure Portal]: https://portal.azure.com/</span></span>
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston