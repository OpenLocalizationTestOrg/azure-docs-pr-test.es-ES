---
title: "Configuración de entornos de ensayo para aplicaciones web en Azure App Service | Microsoft Docs"
description: "Aprenda a utilizar la publicación de ensayo para aplicaciones web en el Servicio de aplicaciones de Azure."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: ca27c55eaaceb3109b1450c550330dfc416fdf55
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="d0d13-103">Configuración de entornos de ensayo en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d0d13-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="d0d13-104">Al implementar la aplicación web, la aplicación web en Linux, el back-end móvil y la aplicación de API en [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), puede implementar en una ranura de implementación independiente en lugar de en la ranura de producción predeterminada al ejecutar en el modo del plan de App Service **Estándar** o **Premium**.</span><span class="sxs-lookup"><span data-stu-id="d0d13-104">When you deploy your web app, web app on Linux, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="d0d13-105">Las ranuras de implementación son realmente aplicaciones activas con sus propios nombres de host.</span><span class="sxs-lookup"><span data-stu-id="d0d13-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="d0d13-106">Los elementos de contenido y configuraciones de aplicaciones se pueden intercambiar entre dos ranuras de implementación, incluida la ranura de producción.</span><span class="sxs-lookup"><span data-stu-id="d0d13-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="d0d13-107">La implementación de la aplicación en un espacio de implementación ofrece las ventajas siguientes:</span><span class="sxs-lookup"><span data-stu-id="d0d13-107">Deploying your application to a deployment slot has the following benefits:</span></span>

* <span data-ttu-id="d0d13-108">Puede validar los cambios en la aplicación en una ranura de implementación de ensayo antes de intercambiarla con la ranura de producción.</span><span class="sxs-lookup"><span data-stu-id="d0d13-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span></span>
* <span data-ttu-id="d0d13-109">La implementación de una aplicación en una ranura en primer lugar y su intercambio con la de la producción garantiza que todas las instancias de la ranura estén activas antes de colocarse en producción.</span><span class="sxs-lookup"><span data-stu-id="d0d13-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="d0d13-110">Esto elimina tiempos de inactividad a la hora de implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="d0d13-111">El redireccionamiento del tráfico es impecable y no se anulan las solicitudes como consecuencia de las operaciones de intercambio.</span><span class="sxs-lookup"><span data-stu-id="d0d13-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="d0d13-112">Este flujo de trabajo completo puede automatizarse mediante la configuración de [Intercambio automático](#Auto-Swap) .</span><span class="sxs-lookup"><span data-stu-id="d0d13-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="d0d13-113">Después del intercambio, la ranura con la aplicación de ensayo anterior ahora ocupa la aplicación de producción anterior.</span><span class="sxs-lookup"><span data-stu-id="d0d13-113">After a swap, the slot with previously staged app now has the previous production app.</span></span> <span data-ttu-id="d0d13-114">Si los cambios intercambiados en el espacio de producción no son los esperados, puede realizar el mismo intercambio inmediatamente para volver a obtener el "último sitio en buen estado".</span><span class="sxs-lookup"><span data-stu-id="d0d13-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span></span>

<span data-ttu-id="d0d13-115">Cada modo del plan del Servicio de aplicaciones admite un número distinto de espacios de implementación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="d0d13-116">Para averiguar el número de ranuras compatibles con el modo de la aplicación, consulte [Precios de App Service](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="d0d13-116">To find out the number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="d0d13-117">Cuando la aplicación tiene varias ranuras, no puede cambiar el modo.</span><span class="sxs-lookup"><span data-stu-id="d0d13-117">When your app has multiple slots, you cannot change the mode.</span></span>
* <span data-ttu-id="d0d13-118">El escalado no está disponible para los espacios que no son de producción.</span><span class="sxs-lookup"><span data-stu-id="d0d13-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="d0d13-119">No se admite la administración de recursos vinculados en los espacios que no sean de producción.</span><span class="sxs-lookup"><span data-stu-id="d0d13-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="d0d13-120">Solo en el [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715) puede evitar este impacto potencial en un espacio de producción si mueve temporalmente el espacio de no producción a un modo del plan del Servicio de aplicaciones diferente.</span><span class="sxs-lookup"><span data-stu-id="d0d13-120">In the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving the non-production slot to a different App Service plan mode.</span></span> <span data-ttu-id="d0d13-121">Tenga en cuenta que el espacio de no producción debe compartir una vez más el mismo modo con el espacio de producción antes de que pueda intercambiar los dos espacios.</span><span class="sxs-lookup"><span data-stu-id="d0d13-121">Note that the non-production slot must once again share the same mode with the production slot before you can swap the two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="d0d13-122">Incorporación de una ranura de implementación</span><span class="sxs-lookup"><span data-stu-id="d0d13-122">Add a deployment slot</span></span>
<span data-ttu-id="d0d13-123">La aplicación debe estar ejecutándose en el modo **Estándar** o **Premium** para que pueda habilitar varias ranuras de implementación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-123">The app must be running in the **Standard** or **Premium** mode in order for you to enable multiple deployment slots.</span></span>

1. <span data-ttu-id="d0d13-124">En [Azure Portal](https://portal.azure.com/), abra la [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-124">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="d0d13-125">Elija la opción **Ranuras de implementación** y, a continuación, haga clic en **Agregar ranura**.</span><span class="sxs-lookup"><span data-stu-id="d0d13-125">Choose the **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Agregar una nueva ranura de implementación][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="d0d13-127">Si la aplicación ya no está en el modo **Estándar** o **Premium**, recibirá un mensaje que indica los modos compatibles para habilitar la publicación de ensayo.</span><span class="sxs-lookup"><span data-stu-id="d0d13-127">If the app is not already in the **Standard** or **Premium** mode, you will receive a message indicating the supported modes for enabling staged publishing.</span></span> <span data-ttu-id="d0d13-128">Llegados a este punto, tiene la opción de seleccionar **Actualizar** e ir a la pestaña **Escala** de la aplicación antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="d0d13-128">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="d0d13-129">En la hoja **Agregar una ranura**, asigne un nombre a la ranura y seleccione si la configuración de la aplicación se debe clonar de otra ranura de implementación existente.</span><span class="sxs-lookup"><span data-stu-id="d0d13-129">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="d0d13-130">Haga clic en la marca de verificación para continuar.</span><span class="sxs-lookup"><span data-stu-id="d0d13-130">Click the check mark to continue.</span></span>
   
    ![Origen de configuración][ConfigurationSource1]
   
    <span data-ttu-id="d0d13-132">La primera vez que agrega un espacio solo tendrá dos opciones: clonar la configuración del espacio predeterminado en producción o no.</span><span class="sxs-lookup"><span data-stu-id="d0d13-132">The first time you add a slot, you will only have two choices: clone configuration from the default slot in production or not at all.</span></span>
    <span data-ttu-id="d0d13-133">Después de haber creado varios espacios, podrá clonar la configuración de un espacio que no sea el de producción:</span><span class="sxs-lookup"><span data-stu-id="d0d13-133">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span></span>
   
    ![Orígenes de configuración][MultipleConfigurationSources]
4. <span data-ttu-id="d0d13-135">En la hoja de recursos de la aplicación, haga clic en **Ranuras de implementación** y, a continuación, haga clic en una ranura de implementación para abrir la hoja de recursos de esa ranura, con un conjunto de métricas y una configuración como cualquier otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="d0d13-136">El nombre de la ranura se muestra en la parte superior de la hoja para recordarle que está viendo la ranura de implementación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-136">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span></span>
   
    ![Título de la ranura de implementación][StagingTitle]
5. <span data-ttu-id="d0d13-138">Haga clic en la dirección URL de la aplicación en la hoja del espacio.</span><span class="sxs-lookup"><span data-stu-id="d0d13-138">Click the app URL in the slot's blade.</span></span> <span data-ttu-id="d0d13-139">Observe que el espacio de implementación tiene su propio nombre de host y que se trata también de una aplicación activa.</span><span class="sxs-lookup"><span data-stu-id="d0d13-139">Notice the deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="d0d13-140">Para limitar el acceso público a la ranura de implementación, consulte [Aplicación web del Servicio de aplicaciones: bloquear acceso web a ranuras de implementación que no son de producción](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="d0d13-140">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="d0d13-141">No hay ningún contenido después de la creación de un espacio de implementación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="d0d13-142">Puede implementar el espacio desde una rama de repositorio diferente o desde un repositorio completamente diferente.</span><span class="sxs-lookup"><span data-stu-id="d0d13-142">You can deploy to the slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="d0d13-143">También puede cambiar la configuración del espacio.</span><span class="sxs-lookup"><span data-stu-id="d0d13-143">You can also change the slot's configuration.</span></span> <span data-ttu-id="d0d13-144">Utilice el perfil de publicación o las credenciales de implementación asociadas al espacio de implementación para ver las actualizaciones del contenido.</span><span class="sxs-lookup"><span data-stu-id="d0d13-144">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span></span>  <span data-ttu-id="d0d13-145">Por ejemplo, [puede publicar en esta ranura mediante Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="d0d13-145">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="d0d13-146">Configuración de ranuras de implementación</span><span class="sxs-lookup"><span data-stu-id="d0d13-146">Configuration for deployment slots</span></span>
<span data-ttu-id="d0d13-147">Cuando crea un clon de la configuración de otro espacio de implementación, la configuración clonada se puede editar.</span><span class="sxs-lookup"><span data-stu-id="d0d13-147">When you clone configuration from another deployment slot, the cloned configuration is editable.</span></span> <span data-ttu-id="d0d13-148">Además, algunos elementos de configuración seguirán el contenido a través de un intercambio (no son específicos del espacio) mientras que otros elementos de configuración permanecerán en el mismo espacio después de un intercambio (son específicos del espacio).</span><span class="sxs-lookup"><span data-stu-id="d0d13-148">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span></span> <span data-ttu-id="d0d13-149">Las listas siguientes muestran la configuración que cambiará al intercambiar las ranuras.</span><span class="sxs-lookup"><span data-stu-id="d0d13-149">The following lists show the configuration that will change when you swap slots.</span></span>

<span data-ttu-id="d0d13-150">**Configuraciones que se intercambian**:</span><span class="sxs-lookup"><span data-stu-id="d0d13-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="d0d13-151">Configuración general: por ejemplo, versión de framework, 32 o 64 bits, Web Sockets</span><span class="sxs-lookup"><span data-stu-id="d0d13-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="d0d13-152">Configuración de la aplicación (puede configurarse para ajustarse a un espacio)</span><span class="sxs-lookup"><span data-stu-id="d0d13-152">App settings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="d0d13-153">Cadenas de conexión (puede configurarse para ajustarse a un espacio)</span><span class="sxs-lookup"><span data-stu-id="d0d13-153">Connection strings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="d0d13-154">Asignaciones de controlador</span><span class="sxs-lookup"><span data-stu-id="d0d13-154">Handler mappings</span></span>
* <span data-ttu-id="d0d13-155">Configuración de supervisión y diagnóstico</span><span class="sxs-lookup"><span data-stu-id="d0d13-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="d0d13-156">Contenido de WebJobs</span><span class="sxs-lookup"><span data-stu-id="d0d13-156">WebJobs content</span></span>

<span data-ttu-id="d0d13-157">**Configuraciones que no se intercambian**:</span><span class="sxs-lookup"><span data-stu-id="d0d13-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="d0d13-158">Extremos de publicación</span><span class="sxs-lookup"><span data-stu-id="d0d13-158">Publishing endpoints</span></span>
* <span data-ttu-id="d0d13-159">Nombres de dominio personalizados</span><span class="sxs-lookup"><span data-stu-id="d0d13-159">Custom Domain Names</span></span>
* <span data-ttu-id="d0d13-160">Certificados SSL y enlaces</span><span class="sxs-lookup"><span data-stu-id="d0d13-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="d0d13-161">Configuración de escala</span><span class="sxs-lookup"><span data-stu-id="d0d13-161">Scale settings</span></span>
* <span data-ttu-id="d0d13-162">Programadores de WebJobs</span><span class="sxs-lookup"><span data-stu-id="d0d13-162">WebJobs schedulers</span></span>

<span data-ttu-id="d0d13-163">Para establecer una configuración de aplicación o una cadena de conexión que se ajuste a una ranura (no intercambiada), obtenga acceso a la hoja **Configuración de la aplicación** para una ranura específica y seleccione el cuadro **Configuración de ranura** para los elementos de configuración que se deben ajustar la ranura.</span><span class="sxs-lookup"><span data-stu-id="d0d13-163">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span></span> <span data-ttu-id="d0d13-164">Tenga en cuenta que marcar un elemento de configuración como ranura específica tiene el efecto de establecer ese elemento como no intercambiable en todas las ranuras de implementación asociadas con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-164">Note that marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span></span>

![Configuración de ranura][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="d0d13-166">Intercambio de ranuras de implementación</span><span class="sxs-lookup"><span data-stu-id="d0d13-166">Swap deployment slots</span></span> 
<span data-ttu-id="d0d13-167">Puede intercambiar ranuras de implementación en la vista **Información general** o **Ranuras de implementación** de la hoja de recursos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-167">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0d13-168">Antes de colocar una aplicación de una ranura de implementación en producción, asegúrese de que todos los valores específicos que no son de ranura están configurados exactamente como desea que estén en el destino de intercambio.</span><span class="sxs-lookup"><span data-stu-id="d0d13-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span></span>
> 
> 

1. <span data-ttu-id="d0d13-169">Para intercambiar las ranuras de implementación, haga clic en el botón **Intercambiar** en la barra de comandos de la aplicación o en la barra de comandos de una ranura de implementación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-169">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span></span>
   
    ![Botón de cambio][SwapButtonBar]

2. <span data-ttu-id="d0d13-171">Asegúrese de que el origen y el destino del intercambio estén correctamente establecidos.</span><span class="sxs-lookup"><span data-stu-id="d0d13-171">Make sure that the swap source and swap target are set properly.</span></span> <span data-ttu-id="d0d13-172">Normalmente, el destino de intercambio es la ranura de producción.</span><span class="sxs-lookup"><span data-stu-id="d0d13-172">Usually, the swap target is the production slot.</span></span> <span data-ttu-id="d0d13-173">Haga clic en **Aceptar** para completar la operación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-173">Click **OK** to complete the operation.</span></span> <span data-ttu-id="d0d13-174">Cuando termine la operación, los espacios de implementación se habrán intercambiado.</span><span class="sxs-lookup"><span data-stu-id="d0d13-174">When the operation finishes, the deployment slots have been swapped.</span></span>

    ![Intercambio completo](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="d0d13-176">Para el tipo de intercambio **Intercambio con vista previa**, consulte [Intercambio con vista previa (intercambio en varias fases)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="d0d13-176">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="d0d13-177">Intercambio con vista previa (intercambio en varias fases)</span><span class="sxs-lookup"><span data-stu-id="d0d13-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="d0d13-178">Intercambio con vista previa o en varias fases simplifican la validación de elementos de configuración específicos de ranura, como cadenas de conexión.</span><span class="sxs-lookup"><span data-stu-id="d0d13-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="d0d13-179">Para las cargas de trabajo críticas, desea validar que la aplicación se comporte según lo esperado al aplicarse la configuración de la ranura de producción, debiendo llevar a cabo dicha validación *antes* de que la aplicación se coloque en producción.</span><span class="sxs-lookup"><span data-stu-id="d0d13-179">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span></span> <span data-ttu-id="d0d13-180">Intercambio con vista previa es lo que necesita.</span><span class="sxs-lookup"><span data-stu-id="d0d13-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="d0d13-181">El intercambio con vista previa no se admite en las aplicaciones web en Linux.</span><span class="sxs-lookup"><span data-stu-id="d0d13-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="d0d13-182">Al usar la opción **Intercambio con vista previa** (consulte [Intercambiar ranuras de implementación](#Swap)), App Service hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d0d13-182">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span></span>

- <span data-ttu-id="d0d13-183">Mantiene la ranura de destino sin cambios para que la carga de trabajo existente en esa ranura (p. ej., producción) no se vea afectada.</span><span class="sxs-lookup"><span data-stu-id="d0d13-183">Keeps the destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="d0d13-184">Aplica los elementos de configuración de la ranura de destino a la ranura de origen, incluidas las cadenas de conexión específicas de ranura y la configuración de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-184">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="d0d13-185">Reinicia los procesos de trabajo en la ranura de origen con estos elementos de configuración ya mencionados.</span><span class="sxs-lookup"><span data-stu-id="d0d13-185">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="d0d13-186">Al completar el intercambio: se mueve la ranura de origen previamente activada en la ranura de destino.</span><span class="sxs-lookup"><span data-stu-id="d0d13-186">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span></span> <span data-ttu-id="d0d13-187">La ranura de destino se mueve en la ranura de origen como en un intercambio manual.</span><span class="sxs-lookup"><span data-stu-id="d0d13-187">The destination slot is moved into the source slot as in a manual swap.</span></span>
- <span data-ttu-id="d0d13-188">Al cancelar el intercambio: se vuelven a aplicar los elementos de configuración de la ranura de origen a la ranura de origen.</span><span class="sxs-lookup"><span data-stu-id="d0d13-188">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span></span>

<span data-ttu-id="d0d13-189">Puede previsualizar exactamente cómo se comportará la aplicación con la configuración de la ranura de destino.</span><span class="sxs-lookup"><span data-stu-id="d0d13-189">You can preview exactly how the app will behave with the destination slot's configuration.</span></span> <span data-ttu-id="d0d13-190">Una vez completada la validación, completará el intercambio en un paso independiente.</span><span class="sxs-lookup"><span data-stu-id="d0d13-190">Once you complete validation, you complete the swap in a separate step.</span></span> <span data-ttu-id="d0d13-191">Este paso tiene la ventaja añadida de que la ranura de origen ya se ha activado con la configuración deseada y los clientes no experimentarán tiempos de inactividad.</span><span class="sxs-lookup"><span data-stu-id="d0d13-191">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="d0d13-192">En los cmdlets de Azure PowerShell se incluyen ejemplos para los cmdlets de Azure PowerShell disponibles para el intercambio de varias fases se incluyen para la sección de ranuras de implementación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-192">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="d0d13-193">Configuración de intercambio automático</span><span class="sxs-lookup"><span data-stu-id="d0d13-193">Configure Auto Swap</span></span>
<span data-ttu-id="d0d13-194">El intercambio automático optimiza los escenarios de DevOps donde desee implementar continuamente la aplicación sin arranques en frío ni tiempos de inactividad para los clientes finales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-194">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span></span> <span data-ttu-id="d0d13-195">Cuando se configura una ranura de implementación para el intercambio automático en producción, cada vez que inserte una actualización de código para esa ranura, App Service coloca automáticamente la aplicación en producción, una vez que ya esté activa en la ranura.</span><span class="sxs-lookup"><span data-stu-id="d0d13-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0d13-196">Al habilitar el intercambio automático para una ranura, asegúrese de que la configuración de ranura sea exactamente la configuración prevista para la ranura de destino (normalmente la ranura de producción).</span><span class="sxs-lookup"><span data-stu-id="d0d13-196">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="d0d13-197">El intercambio automático no se admite en aplicaciones web en Linux.</span><span class="sxs-lookup"><span data-stu-id="d0d13-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="d0d13-198">Es fácil configurar el intercambio automático para un espacio.</span><span class="sxs-lookup"><span data-stu-id="d0d13-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="d0d13-199">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d0d13-199">Follow the steps below:</span></span>

1. <span data-ttu-id="d0d13-200">En **Ranuras de implementación**, seleccione una ranura que no sea de producción y elija **Configuración de la aplicación** en la hoja de recursos de esa ranura.</span><span class="sxs-lookup"><span data-stu-id="d0d13-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="d0d13-201">Seleccione **Activado** para **Intercambio automático**, elija la ranura de destino deseada en **Ranura de intercambio automático** y haga clic en **Guardar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="d0d13-201">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span></span> <span data-ttu-id="d0d13-202">Asegúrese de que la configuración del espacio sea exactamente la configuración prevista para el espacio de destino.</span><span class="sxs-lookup"><span data-stu-id="d0d13-202">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span></span>
   
    <span data-ttu-id="d0d13-203">La ficha **Notificaciones** parpadeará en color verde indicando que se ha completado con **éxito** una vez finalizada la operación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-203">The **Notifications** tab will flash a green **SUCCESS** once the operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="d0d13-204">Para probar el intercambio automático para la aplicación, puede seleccionar primero una ranura de destino que no sea de producción en **Ranura de intercambio automático** para familiarizarse con la característica.</span><span class="sxs-lookup"><span data-stu-id="d0d13-204">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="d0d13-205">Ejecute una inserción de código para este espacio de implementación.</span><span class="sxs-lookup"><span data-stu-id="d0d13-205">Execute a code push to that deployment slot.</span></span> <span data-ttu-id="d0d13-206">El intercambio automático se realizará después de un breve tiempo y la actualización se reflejará en la dirección URL del espacio de destino.</span><span class="sxs-lookup"><span data-stu-id="d0d13-206">Auto Swap will happen after a short time and the update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="to-rollback-a-production-app-after-swap"></a><span data-ttu-id="d0d13-207">Para revertir una aplicación de producción después de un intercambio</span><span class="sxs-lookup"><span data-stu-id="d0d13-207">To rollback a production app after swap</span></span>
<span data-ttu-id="d0d13-208">Si se identifican errores en producción después del intercambio de espacios, revierta los espacios a sus estados anteriores. Para ello, intercambie los mismos dos espacios inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="d0d13-208">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="d0d13-209">Preparación personalizada antes del intercambio</span><span class="sxs-lookup"><span data-stu-id="d0d13-209">Custom warm-up before swap</span></span>
<span data-ttu-id="d0d13-210">Es posible que algunas aplicaciones necesiten acciones de preparación personalizadas.</span><span class="sxs-lookup"><span data-stu-id="d0d13-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="d0d13-211">El elemento de configuración `applicationInitialization` en el archivo web.config permite especificar acciones de inicialización personalizadas antes de recibir una solicitud.</span><span class="sxs-lookup"><span data-stu-id="d0d13-211">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span></span> <span data-ttu-id="d0d13-212">La operación de intercambio esperará a que se complete la preparación personalizada.</span><span class="sxs-lookup"><span data-stu-id="d0d13-212">The swap operation will wait for this custom warm-up to complete.</span></span> <span data-ttu-id="d0d13-213">He aquí un fragmento de ejemplo del archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="d0d13-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="to-delete-a-deployment-slot"></a><span data-ttu-id="d0d13-214">Para eliminar una ranura de implementación</span><span class="sxs-lookup"><span data-stu-id="d0d13-214">To delete a deployment slot</span></span>
<span data-ttu-id="d0d13-215">En la hoja para una ranura de implementación, abra la hoja de la ranura de implementación, haga clic en **Información general** (la página predeterminada) y haga clic en **Eliminar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="d0d13-215">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span></span>  

![Eliminación de una ranura de implementación][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="d0d13-217">Cmdlets de PowerShell de Azure para espacios de implementación</span><span class="sxs-lookup"><span data-stu-id="d0d13-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="d0d13-218">Azure PowerShell es un módulo que proporciona cmdlets para administrar Azure mediante Windows PowerShell, incluida la compatibilidad para administrar ranuras de implementación de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d0d13-218">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="d0d13-219">Para obtener información acerca de cómo instalar y configurar Azure PowerShell y cómo autenticar Azure PowerShell con su suscripción de Azure, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d0d13-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="d0d13-220">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="d0d13-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="d0d13-221">Creación de una ranura de implementación</span><span class="sxs-lookup"><span data-stu-id="d0d13-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a><span data-ttu-id="d0d13-222">Inicio de un intercambio con vista previa (intercambio en varias fases) y aplicación de configuración de la ranura de destino a la ranura de origen</span><span class="sxs-lookup"><span data-stu-id="d0d13-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration to source slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="d0d13-223">Cancelación de un intercambio pendiente (intercambio con vista previa) y restauración de configuración de la ranura de origen</span><span class="sxs-lookup"><span data-stu-id="d0d13-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="d0d13-224">Intercambio de ranuras de implementación</span><span class="sxs-lookup"><span data-stu-id="d0d13-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="d0d13-225">Eliminación de una ranura de implementación</span><span class="sxs-lookup"><span data-stu-id="d0d13-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="d0d13-226">Comandos de la interfaz de la línea de comandos de Azure (CLI de Azure) para ranuras de implementación</span><span class="sxs-lookup"><span data-stu-id="d0d13-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="d0d13-227">La CLI de Azure proporciona comandos de varias plataformas para trabajar con Azure, incluida la compatibilidad para administrar ranuras de implementación de App Service.</span><span class="sxs-lookup"><span data-stu-id="d0d13-227">The Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="d0d13-228">Para obtener instrucciones acerca de cómo instalar y configurar la CLI de Azure, incluyendo la información acerca de cómo conectar la CLI de Azure a su suscripción de Azure, consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d0d13-228">For instructions on installing and configuring the Azure CLI, including information on how to connect Azure CLI to your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="d0d13-229">Para mostrar los comandos disponibles para el Servicio de aplicaciones de Azure en la CLI de Azure, llame a `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="d0d13-229">To list the commands available for Azure App Service in the Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="d0d13-230">Para los comandos de la [CLI de Azure 2.0](https://github.com/Azure/azure-cli) de espacios de implementación, consulte [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="d0d13-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="d0d13-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="d0d13-231">azure site list</span></span>
<span data-ttu-id="d0d13-232">Para obtener información sobre las aplicaciones de la suscripción actual, llame a **azure site list**, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d0d13-232">For information about the apps in the current subscription, call **azure site list**, as in the following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="d0d13-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="d0d13-233">azure site create</span></span>
<span data-ttu-id="d0d13-234">Para crear una ranura de implementación, llame a **azure site create** y especifique el nombre de una aplicación existente y el de la ranura que se vaya a crear, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d0d13-234">To create a deployment slot, call **azure site create** and specify the name of an existing app and the name of the slot to create, as in the following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="d0d13-235">Para habilitar el control de código fuente en la nueva ranura, use la opción **--git** , como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d0d13-235">To enable source control for the new slot, use the **--git** option, as in the following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="d0d13-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="d0d13-236">azure site swap</span></span>
<span data-ttu-id="d0d13-237">Para hacer que la ranura de implementación actualizada se convierta en la aplicación de producción, utilice el comando **azure site swap** para realizar una operación de intercambio, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d0d13-237">To make the updated deployment slot the production app, use the **azure site swap** command to perform a swap operation, as in the following example.</span></span> <span data-ttu-id="d0d13-238">La aplicación de producción no experimentará tiempos de inactividad ni arranques en frío.</span><span class="sxs-lookup"><span data-stu-id="d0d13-238">The production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="d0d13-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="d0d13-239">azure site delete</span></span>
<span data-ttu-id="d0d13-240">Para eliminar una ranura de implementación que ya no sea necesaria, utilice el comando **azure site delete** , como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d0d13-240">To delete a deployment slot that is no longer needed, use the **azure site delete** command, as in the following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="d0d13-241">Vea una aplicación web en acción.</span><span class="sxs-lookup"><span data-stu-id="d0d13-241">See a web app in action.</span></span> <span data-ttu-id="d0d13-242">[Pruebe el Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/) inmediatamente y cree una aplicación de inicio de corta duración; no se requiere tarjeta de crédito ni se establece ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="d0d13-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d0d13-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d0d13-243">Next Steps</span></span>
<span data-ttu-id="d0d13-244">[Aplicación web de Azure App Service: bloquear el acceso web a las ranuras de implementación que no son de producción](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introducción a App Service en Linux](./app-service-linux-intro.md)
[Evaluación gratuita de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="d0d13-244">[Azure App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction to App Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

