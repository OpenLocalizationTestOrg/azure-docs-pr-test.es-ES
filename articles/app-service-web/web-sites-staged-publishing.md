---
title: aaaSet entornos de ensayo para aplicaciones web en el servicio de aplicaciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse provisionalmente la publicación de las aplicaciones web de servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="b7ff3-103">Configuración de entornos de ensayo en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b7ff3-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="b7ff3-104">Cuando se implementan la aplicación web, la aplicación web en Linux, móvil back-end y aplicación de API demasiado[servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714), puede implementar tooa ranura de implementación independiente en lugar de la ranura de producción de hello predeterminada cuando se ejecuta en hello **estándar**o **Premium** modo de plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-104">When you deploy your web app, web app on Linux, mobile back end, and API app too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy tooa separate deployment slot instead of hello default production slot when running in hello **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="b7ff3-105">Las ranuras de implementación son realmente aplicaciones activas con sus propios nombres de host.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="b7ff3-106">Elementos de contenido y las configuraciones de aplicación se pueden intercambiar entre dos ranuras de implementación, incluida la zona de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-106">App content and configurations elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="b7ff3-107">Implementación de la ranura de implementación de aplicación tooa tiene Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b7ff3-107">Deploying your application tooa deployment slot has hello following benefits:</span></span>

* <span data-ttu-id="b7ff3-108">Puede validar los cambios de la aplicación en una ranura de implementación de ensayo antes de cambiarlo a ranura de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-108">You can validate app changes in a staging deployment slot before swapping it with hello production slot.</span></span>
* <span data-ttu-id="b7ff3-109">Implementar una ranura de aplicación tooa primero y cambiarlo a producción garantizan que todas las instancias de la ranura de Hola se activa antes de que se va a intercambiar en producción.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-109">Deploying an app tooa slot first and swapping it into production ensures that all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="b7ff3-110">Esto elimina tiempos de inactividad a la hora de implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="b7ff3-111">Hola redireccionamiento del tráfico es perfecto y no se anulan solicitudes como resultado de las operaciones de intercambio.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-111">hello traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="b7ff3-112">Este flujo de trabajo completo puede automatizarse mediante la configuración de [Intercambio automático](#Auto-Swap) .</span><span class="sxs-lookup"><span data-stu-id="b7ff3-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="b7ff3-113">Después de un intercambio, ranura Hola con aplicación previamente por fases ahora tiene aplicación de producción de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-113">After a swap, hello slot with previously staged app now has hello previous production app.</span></span> <span data-ttu-id="b7ff3-114">Si hay cambios de hello pasados a la ranura de producción de hello no según lo esperado, puede realizar Hola que mismo intercambio inmediatamente tooget su "último sitio conocido" realizar copias.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-114">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good site" back.</span></span>

<span data-ttu-id="b7ff3-115">Cada modo del plan del Servicio de aplicaciones admite un número distinto de espacios de implementación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="b7ff3-116">toofind out número Hola de ranuras se admite el modo de la aplicación, consulte [precios del servicio de aplicación](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-116">toofind out hello number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="b7ff3-117">Cuando la aplicación tiene varias ranuras, no se puede cambiar el modo de saludo.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-117">When your app has multiple slots, you cannot change hello mode.</span></span>
* <span data-ttu-id="b7ff3-118">El escalado no está disponible para los espacios que no son de producción.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="b7ff3-119">No se admite la administración de recursos vinculados en los espacios que no sean de producción.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="b7ff3-120">Hola [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715) solo, puede evitar este posible impacto en una ranura de producción moviendo temporalmente el modo de plan de hello ranura de producción no tooa otro servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-120">In hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving hello non-production slot tooa different App Service plan mode.</span></span> <span data-ttu-id="b7ff3-121">Tenga en cuenta esa ranura no sea de producción de hello debe compartir una vez más Hola mismo modo con la ranura de producción de hello antes de que se pueden intercambiar las ranuras de hello dos.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-121">Note that hello non-production slot must once again share hello same mode with hello production slot before you can swap hello two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="b7ff3-122">Incorporación de una ranura de implementación</span><span class="sxs-lookup"><span data-stu-id="b7ff3-122">Add a deployment slot</span></span>
<span data-ttu-id="b7ff3-123">debe estar ejecutando la aplicación Hello en hello **estándar** o **Premium** modo en orden para tooenable varias ranuras de implementación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-123">hello app must be running in hello **Standard** or **Premium** mode in order for you tooenable multiple deployment slots.</span></span>

1. <span data-ttu-id="b7ff3-124">Hola [Portal de Azure](https://portal.azure.com/), abra la aplicación [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-124">In hello [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="b7ff3-125">Elija hello **ranuras de implementación** opción, a continuación, haga clic en **agregar ranura**.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-125">Choose hello **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Agregar una nueva ranura de implementación][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="b7ff3-127">Si la aplicación hello no está ya en hello **estándar** o **Premium** modo, recibirá un mensaje que indica los modos de hello compatibles para habilitar la publicación de ensayo.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-127">If hello app is not already in hello **Standard** or **Premium** mode, you will receive a message indicating hello supported modes for enabling staged publishing.</span></span> <span data-ttu-id="b7ff3-128">En este punto, tiene Hola opción tooselect **actualizar** y navegue toohello **escala** pestaña de la aplicación antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-128">At this point, you have hello option tooselect **Upgrade** and navigate toohello **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="b7ff3-129">Hola **agregar una ranura** hoja, asigne un nombre a la ranura de Hola y seleccione si tooclone configuración de la aplicación de otra ranura de implementación existente.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-129">In hello **Add a slot** blade, give hello slot a name, and select whether tooclone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="b7ff3-130">Haga clic en hello toocontinue de marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-130">Click hello check mark toocontinue.</span></span>
   
    ![Origen de configuración][ConfigurationSource1]
   
    <span data-ttu-id="b7ff3-132">Hello primera vez que agrega una ranura, solo tendrá dos opciones: configuración de clonación de ranura de predeterminado de hello en producción o no en absoluto.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-132">hello first time you add a slot, you will only have two choices: clone configuration from hello default slot in production or not at all.</span></span>
    <span data-ttu-id="b7ff3-133">Después de haber creado varias ranuras, será capaz de tooclone configuración de una ranura distinto de hello en producción:</span><span class="sxs-lookup"><span data-stu-id="b7ff3-133">After you have created several slots, you will be able tooclone configuration from a slot other than hello one in production:</span></span>
   
    ![Orígenes de configuración][MultipleConfigurationSources]
4. <span data-ttu-id="b7ff3-135">En la hoja de recursos de la aplicación, haga clic en **ranuras de implementación**, a continuación, haga clic en un tooopen de ranura de implementación hoja de recursos de la ranura, con un conjunto de métricas y la configuración al igual que cualquier otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot tooopen that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="b7ff3-136">Hello nombre de ranura de Hola se muestra en parte superior de Hola de hello hoja tooremind que está viendo Hola ranura de implementación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-136">hello name of hello slot is shown at hello top of hello blade tooremind you that you are viewing hello deployment slot.</span></span>
   
    ![Título de la ranura de implementación][StagingTitle]
5. <span data-ttu-id="b7ff3-138">Haga clic en la URL de la aplicación hello en la hoja de la ranura de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-138">Click hello app URL in hello slot's blade.</span></span> <span data-ttu-id="b7ff3-139">Observe la ranura de implementación de hello tiene su propio nombre de host y también es una aplicación activa.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-139">Notice hello deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="b7ff3-140">ranura de implementación de toolimit acceso público toohello, consulte [aplicación de servicio Web App: ranuras de implementación de producción toonon de bloque web acceso](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-140">toolimit public access toohello deployment slot, see [App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="b7ff3-141">No hay ningún contenido después de la creación de un espacio de implementación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="b7ff3-142">Puede implementar toohello ranura de una rama del repositorio diferente o un repositorio totalmente diferente.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-142">You can deploy toohello slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="b7ff3-143">También puede cambiar la configuración de la ranura de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-143">You can also change hello slot's configuration.</span></span> <span data-ttu-id="b7ff3-144">Hola Use Publicar perfil o la implementación de las credenciales asociadas con la ranura de implementación de hello las actualizaciones de contenido.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-144">Use hello publish profile or deployment credentials associated with hello deployment slot for content updates.</span></span>  <span data-ttu-id="b7ff3-145">Por ejemplo, puede [publicar ranura toothis con git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-145">For example, you can [publish toothis slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="b7ff3-146">Configuración de ranuras de implementación</span><span class="sxs-lookup"><span data-stu-id="b7ff3-146">Configuration for deployment slots</span></span>
<span data-ttu-id="b7ff3-147">Al clonar la configuración de otra ranura de implementación, configuración clonado hello es editable.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-147">When you clone configuration from another deployment slot, hello cloned configuration is editable.</span></span> <span data-ttu-id="b7ff3-148">Además, algunos elementos de configuración seguirá contenido Hola a través de un intercambio (no ranura específico) mientras que otros elementos de configuración permanecerá en hello misma ranura después de un intercambio (específico de la ranura).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-148">Furthermore, some configuration elements will follow hello content across a swap (not slot specific) while other configuration elements will stay in hello same slot after a swap (slot specific).</span></span> <span data-ttu-id="b7ff3-149">Hello listas siguientes se muestra configuración de Hola que cambiará cuando intercambia las ranuras.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-149">hello following lists show hello configuration that will change when you swap slots.</span></span>

<span data-ttu-id="b7ff3-150">**Configuraciones que se intercambian**:</span><span class="sxs-lookup"><span data-stu-id="b7ff3-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="b7ff3-151">Configuración general: por ejemplo, versión de framework, 32 o 64 bits, Web Sockets</span><span class="sxs-lookup"><span data-stu-id="b7ff3-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="b7ff3-152">Configuración de la aplicación (puede ser configurado toostick tooa ranura)</span><span class="sxs-lookup"><span data-stu-id="b7ff3-152">App settings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="b7ff3-153">Cadenas de conexión (puede estar configurado toostick tooa ranura)</span><span class="sxs-lookup"><span data-stu-id="b7ff3-153">Connection strings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="b7ff3-154">Asignaciones de controlador</span><span class="sxs-lookup"><span data-stu-id="b7ff3-154">Handler mappings</span></span>
* <span data-ttu-id="b7ff3-155">Configuración de supervisión y diagnóstico</span><span class="sxs-lookup"><span data-stu-id="b7ff3-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="b7ff3-156">Contenido de WebJobs</span><span class="sxs-lookup"><span data-stu-id="b7ff3-156">WebJobs content</span></span>

<span data-ttu-id="b7ff3-157">**Configuraciones que no se intercambian**:</span><span class="sxs-lookup"><span data-stu-id="b7ff3-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="b7ff3-158">Extremos de publicación</span><span class="sxs-lookup"><span data-stu-id="b7ff3-158">Publishing endpoints</span></span>
* <span data-ttu-id="b7ff3-159">Nombres de dominio personalizados</span><span class="sxs-lookup"><span data-stu-id="b7ff3-159">Custom Domain Names</span></span>
* <span data-ttu-id="b7ff3-160">Certificados SSL y enlaces</span><span class="sxs-lookup"><span data-stu-id="b7ff3-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="b7ff3-161">Configuración de escala</span><span class="sxs-lookup"><span data-stu-id="b7ff3-161">Scale settings</span></span>
* <span data-ttu-id="b7ff3-162">Programadores de WebJobs</span><span class="sxs-lookup"><span data-stu-id="b7ff3-162">WebJobs schedulers</span></span>

<span data-ttu-id="b7ff3-163">tooconfigure una configuración o conexión cadena toostick tooa ranura de aplicación (no intercambiada) Hola acceso **configuración de la aplicación** hoja de una ranura específico, a continuación, seleccione hello **ranura configuración** cuadro Hola elementos de configuración que deben pegar ranura Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-163">tooconfigure an app setting or connection string toostick tooa slot (not swapped), access hello **Application Settings** blade for a specific slot, then select hello **Slot Setting** box for hello configuration elements that should stick hello slot.</span></span> <span data-ttu-id="b7ff3-164">Tenga en cuenta que un elemento de configuración marcar como ranura específico tiene el efecto de Hola de establecimiento de ese elemento como no intercambiables en todas las ranuras de implementación de hello asociadas con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-164">Note that marking a configuration element as slot specific has hello effect of establishing that element as not swappable across all hello deployment slots associated with hello app.</span></span>

![Configuración de ranura][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="b7ff3-166">Intercambio de ranuras de implementación</span><span class="sxs-lookup"><span data-stu-id="b7ff3-166">Swap deployment slots</span></span> 
<span data-ttu-id="b7ff3-167">Puede intercambiar las ranuras de implementación en hello **Introducción** o **ranuras de implementación** vista de hoja de recursos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-167">You can swap deployment slots in hello **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7ff3-168">Antes de intercambiar una aplicación desde una ranura de implementación en producción, asegúrese de que todas las configuraciones específicas de ranura no están configuradas exactamente como se desee toohave en el destino de intercambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want toohave it in hello swap target.</span></span>
> 
> 

1. <span data-ttu-id="b7ff3-169">las ranuras de implementación de tooswap, haga clic en hello **intercambiar** botón de barra de comandos de Hola de aplicación hello o en la barra de comandos de Hola de una ranura de implementación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-169">tooswap deployment slots, click hello **Swap** button in hello command bar of hello app or in hello command bar of a deployment slot.</span></span>
   
    ![Botón de cambio][SwapButtonBar]

2. <span data-ttu-id="b7ff3-171">Asegúrese de que ese destino de origen y de intercambio de intercambio de hello están establecidos correctamente.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-171">Make sure that hello swap source and swap target are set properly.</span></span> <span data-ttu-id="b7ff3-172">Normalmente, el destino de intercambio de hello es ranura de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-172">Usually, hello swap target is hello production slot.</span></span> <span data-ttu-id="b7ff3-173">Haga clic en **Aceptar** operación de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-173">Click **OK** toocomplete hello operation.</span></span> <span data-ttu-id="b7ff3-174">Cuando finaliza la operación de hello, se intercambiaron las ranuras de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-174">When hello operation finishes, hello deployment slots have been swapped.</span></span>

    ![Intercambio completo](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="b7ff3-176">Para hello **intercambio con vista previa** intercambiar tipo, consulte [intercambio con vista previa (intercambio de varias fase)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-176">For hello **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="b7ff3-177">Intercambio con vista previa (intercambio en varias fases)</span><span class="sxs-lookup"><span data-stu-id="b7ff3-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="b7ff3-178">Intercambio con vista previa o en varias fases simplifican la validación de elementos de configuración específicos de ranura, como cadenas de conexión.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="b7ff3-179">Para las cargas de trabajo críticas, desea toovalidate que Hola aplicación se comporta según lo esperado cuando se aplica la configuración de la ranura de producción de hello, y debe realizar esta validación *antes de* aplicación hello se intercambia en producción.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-179">For mission-critical workloads, you want toovalidate that hello app behaves as expected when hello production slot's configuration is applied, and you must perform such validation *before* hello app is swapped into production.</span></span> <span data-ttu-id="b7ff3-180">Intercambio con vista previa es lo que necesita.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="b7ff3-181">El intercambio con vista previa no se admite en las aplicaciones web en Linux.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="b7ff3-182">Cuando usas hello **intercambio con vista previa** opción (vea [intercambiar ranuras de implementación](#Swap)), servicio de aplicación Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b7ff3-182">When you use hello **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does hello following:</span></span>

- <span data-ttu-id="b7ff3-183">No se ve afectado mantiene Hola destino ranura sin modificar por lo que carga de trabajo existente en esa ranura (p. ej., producción).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-183">Keeps hello destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="b7ff3-184">Se aplica a los elementos de configuración de Hola de hello ranura toohello origen ranura de destino, incluidas las cadenas de conexión específica de la ranura de Hola y configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-184">Applies hello configuration elements of hello destination slot toohello source slot, including hello slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="b7ff3-185">Reinicia los procesos de trabajo de hello en la ranura de origen Hola con estos elementos de configuración mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-185">Restarts hello worker processes on hello source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="b7ff3-186">Cuando complete el intercambio de hello: ranura de movimientos Hola previa warmed el origen en la ranura de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-186">When you complete hello swap: Moves hello pre-warmed-up source slot into hello destination slot.</span></span> <span data-ttu-id="b7ff3-187">ranura de destino de Hola se mueve a la ranura de origen de hello como en un intercambio manual.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-187">hello destination slot is moved into hello source slot as in a manual swap.</span></span>
- <span data-ttu-id="b7ff3-188">Al cancelar el intercambio de hello: vuelve a aplicar los elementos de configuración de Hola de ranura de origen de hello origen ranura toohello.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-188">When you cancel hello swap: Reapplies hello configuration elements of hello source slot toohello source slot.</span></span>

<span data-ttu-id="b7ff3-189">Puede ver exactamente cómo se comportará aplicación hello con la configuración de la ranura de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-189">You can preview exactly how hello app will behave with hello destination slot's configuration.</span></span> <span data-ttu-id="b7ff3-190">Cuando se haya completado la validación, completar intercambio hello en un paso independiente.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-190">Once you complete validation, you complete hello swap in a separate step.</span></span> <span data-ttu-id="b7ff3-191">Este paso ha Hola ventaja adicional que la ranura de origen de hello ya está activa con la configuración deseada de Hola y los clientes no experimentarán ningún tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-191">This step has hello added advantage that hello source slot is already warmed up with hello desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="b7ff3-192">Ejemplos de hello cmdlets de PowerShell de Azure disponibles para el intercambio de varias fase se incluyen en hello cmdlets de PowerShell de Azure para la sección de ranuras de implementación.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-192">Samples for hello Azure PowerShell cmdlets available for multi-phase swap are included in hello Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="b7ff3-193">Configuración de intercambio automático</span><span class="sxs-lookup"><span data-stu-id="b7ff3-193">Configure Auto Swap</span></span>
<span data-ttu-id="b7ff3-194">Optimiza de intercambio automático escenarios de DevOps donde desea toocontinuously implementa su aplicación con cero arranque en frío y sin tiempo de inactividad para los clientes finales de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-194">Auto Swap streamlines DevOps scenarios where you want toocontinuously deploy your app with zero cold start and zero downtime for end customers of hello app.</span></span> <span data-ttu-id="b7ff3-195">Cuando se configura una ranura de implementación para el intercambio automático al entorno de producción, cada vez que realice una inserción su ranura toothat de actualización de código, servicio de aplicaciones automáticamente intercambiará aplicación hello en producción cuando ya se activa en la ranura de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update toothat slot, App Service will automatically swap hello app into production after it has already warmed up in hello slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7ff3-196">Cuando se habilita para una ranura de intercambio automático, asegúrese de que configuración de la ranura de hello es exactamente la configuración del Hola prevista para la ranura de destino hello (normalmente ranura de producción de hello).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-196">When you enable Auto Swap for a slot, make sure hello slot configuration is exactly hello configuration intended for hello target slot (usually hello production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="b7ff3-197">El intercambio automático no se admite en aplicaciones web en Linux.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="b7ff3-198">Es fácil configurar el intercambio automático para un espacio.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="b7ff3-199">Siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="b7ff3-199">Follow hello steps below:</span></span>

1. <span data-ttu-id="b7ff3-200">En **Ranuras de implementación**, seleccione una ranura que no sea de producción y elija **Configuración de la aplicación** en la hoja de recursos de esa ranura.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="b7ff3-201">Seleccione **en** para **intercambio automático**, seleccione la ranura de destino deseado de hello en **la ranura de intercambio automático**y haga clic en **guardar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-201">Select **On** for **Auto Swap**, select hello desired target slot in **Auto Swap Slot**, and click **Save** in hello command bar.</span></span> <span data-ttu-id="b7ff3-202">Asegúrese de que configuración de ranura de hello es exactamente la configuración del Hola destinada a la ranura de destino Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-202">Make sure configuration for hello slot is exactly hello configuration intended for hello target slot.</span></span>
   
    <span data-ttu-id="b7ff3-203">Hola **notificaciones** ficha parpadeará en un color verde **correcto** una vez completada la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-203">hello **Notifications** tab will flash a green **SUCCESS** once hello operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="b7ff3-204">tootest intercambio automático de la aplicación, primero puede seleccionar una ranura de destino no es de producción en **la ranura de intercambio automático** toobecome familiarizado con la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-204">tootest Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** toobecome familiar with hello feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="b7ff3-205">Ejecutar una ranura de implementación de toothat de inserción de código.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-205">Execute a code push toothat deployment slot.</span></span> <span data-ttu-id="b7ff3-206">El intercambio automático se realizará después de unos minutos y actualización de Hola se verán reflejado en la dirección URL de la ranura de destino.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-206">Auto Swap will happen after a short time and hello update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a><span data-ttu-id="b7ff3-207">toorollback una aplicación de producción después del intercambio</span><span class="sxs-lookup"><span data-stu-id="b7ff3-207">toorollback a production app after swap</span></span>
<span data-ttu-id="b7ff3-208">Si se identifican errores en producción después de un intercambio de ranura, poner las ranuras de hello tootheir atrás intercambio previo Estados intercambiando las ranuras de hello dos mismos inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-208">If any errors are identified in production after a slot swap, roll hello slots back tootheir pre-swap states by swapping hello same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="b7ff3-209">Preparación personalizada antes del intercambio</span><span class="sxs-lookup"><span data-stu-id="b7ff3-209">Custom warm-up before swap</span></span>
<span data-ttu-id="b7ff3-210">Es posible que algunas aplicaciones necesiten acciones de preparación personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="b7ff3-211">Hola `applicationInitialization` elemento de configuración en el archivo web.config permite toospecify inicialización personalizada acciones toobe realiza antes de que se recibe una solicitud.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-211">hello `applicationInitialization` configuration element in web.config allows you toospecify custom initialization actions toobe performed before a request is received.</span></span> <span data-ttu-id="b7ff3-212">operación de intercambio de Hello esperará este toocomplete preparación personalizado.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-212">hello swap operation will wait for this custom warm-up toocomplete.</span></span> <span data-ttu-id="b7ff3-213">He aquí un fragmento de ejemplo del archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a><span data-ttu-id="b7ff3-214">toodelete una ranura de implementación</span><span class="sxs-lookup"><span data-stu-id="b7ff3-214">toodelete a deployment slot</span></span>
<span data-ttu-id="b7ff3-215">En la hoja de Hola de una ranura de implementación, hoja de la ranura de implementación de hello abierto, haga clic en **Introducción** (página predeterminada de hello) y haga clic en **eliminar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-215">In hello blade for a deployment slot, open hello deployment slot's blade, click **Overview** (hello default page), and click **Delete** in hello command bar.</span></span>  

![Eliminación de una ranura de implementación][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="b7ff3-217">Cmdlets de PowerShell de Azure para espacios de implementación</span><span class="sxs-lookup"><span data-stu-id="b7ff3-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="b7ff3-218">Azure PowerShell es un módulo que proporciona cmdlets toomanage Azure a través de Windows PowerShell, incluida la compatibilidad para administrar las ranuras de implementación de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-218">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="b7ff3-219">Para obtener información sobre cómo instalar y configurar Azure PowerShell y sobre la autenticación de Azure PowerShell con su suscripción de Azure, consulte [cómo tooinstall y configurar Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How tooinstall and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="b7ff3-220">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="b7ff3-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="b7ff3-221">Creación de una ranura de implementación</span><span class="sxs-lookup"><span data-stu-id="b7ff3-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a><span data-ttu-id="b7ff3-222">Iniciar un intercambio con revisión (intercambio de varias fase) y aplicar la ranura de toosource de configuración de ranura de destino</span><span class="sxs-lookup"><span data-stu-id="b7ff3-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration toosource slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="b7ff3-223">Cancelación de un intercambio pendiente (intercambio con vista previa) y restauración de configuración de la ranura de origen</span><span class="sxs-lookup"><span data-stu-id="b7ff3-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="b7ff3-224">Intercambio de ranuras de implementación</span><span class="sxs-lookup"><span data-stu-id="b7ff3-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="b7ff3-225">Eliminación de una ranura de implementación</span><span class="sxs-lookup"><span data-stu-id="b7ff3-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="b7ff3-226">Comandos de la interfaz de la línea de comandos de Azure (CLI de Azure) para ranuras de implementación</span><span class="sxs-lookup"><span data-stu-id="b7ff3-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="b7ff3-227">Hola CLI de Azure proporciona comandos entre plataformas y para trabajar con Azure, incluida la compatibilidad para administrar las ranuras de implementación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-227">hello Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="b7ff3-228">Para obtener instrucciones sobre cómo instalar y configurar hello CLI de Azure, incluida la información acerca de cómo tooconnect CLI de Azure tooyour suscripción de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-228">For instructions on installing and configuring hello Azure CLI, including information on how tooconnect Azure CLI tooyour Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="b7ff3-229">comandos de hello toolist disponibles para el servicio de aplicaciones de Azure en hello CLI de Azure, llame a `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-229">toolist hello commands available for Azure App Service in hello Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="b7ff3-230">Para los comandos de la [CLI de Azure 2.0](https://github.com/Azure/azure-cli) de espacios de implementación, consulte [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="b7ff3-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="b7ff3-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="b7ff3-231">azure site list</span></span>
<span data-ttu-id="b7ff3-232">Para obtener información acerca de las aplicaciones de hello en la suscripción actual de hello, llame a **lista de sitios de azure**, como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-232">For information about hello apps in hello current subscription, call **azure site list**, as in hello following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="b7ff3-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="b7ff3-233">azure site create</span></span>
<span data-ttu-id="b7ff3-234">toocreate una ranura de implementación, llame a **crear sitio azure** y especifique el nombre hello de una aplicación existente y el nombre de Hola de hello ranura toocreate, como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-234">toocreate a deployment slot, call **azure site create** and specify hello name of an existing app and hello name of hello slot toocreate, as in hello following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="b7ff3-235">control de código fuente de tooenable para la nueva ranura hello, use Hola **--git** opción, como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-235">tooenable source control for hello new slot, use hello **--git** option, as in hello following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="b7ff3-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="b7ff3-236">azure site swap</span></span>
<span data-ttu-id="b7ff3-237">toomake Hola aplicación de producción de hello de ranura de implementación actualizadas, use hello **intercambio de sitio de azure** comando tooperform una operación de intercambio, como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-237">toomake hello updated deployment slot hello production app, use hello **azure site swap** command tooperform a swap operation, as in hello following example.</span></span> <span data-ttu-id="b7ff3-238">aplicación de producción de Hello no experimentará tiempo improductivo, ni sufrirá un arranque en frío.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-238">hello production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="b7ff3-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="b7ff3-239">azure site delete</span></span>
<span data-ttu-id="b7ff3-240">toodelete una ranura de implementación que ya no es necesario, utilice hello **delete de sitio de azure** comando, como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-240">toodelete a deployment slot that is no longer needed, use hello **azure site delete** command, as in hello following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="b7ff3-241">Vea una aplicación web en acción.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-241">See a web app in action.</span></span> <span data-ttu-id="b7ff3-242">[Pruebe el Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/) inmediatamente y cree una aplicación de inicio de corta duración; no se requiere tarjeta de crédito ni se establece ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="b7ff3-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b7ff3-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b7ff3-243">Next Steps</span></span>
<span data-ttu-id="b7ff3-244">[Web de servicio de aplicaciones de Azure aplicación: bloquear ranuras de implementación de web access producción toonon](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introducción tooApp servicio en Linux](./app-service-linux-intro.md)
[evaluación gratuita de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="b7ff3-244">[Azure App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service on Linux](./app-service-linux-intro.md)
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

