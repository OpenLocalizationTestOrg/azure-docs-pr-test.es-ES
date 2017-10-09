---
title: "Aplicación visión tootroubleshoot personalizado directivas - Azure AD B2C | Documentos de Microsoft"
description: "¿Cómo toosetup Application Insights tootrace Hola ejecución de directivas personalizadas"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="94597-103">Azure Active Directory B2C: Collecting Logs (Azure Active Directory B2C: recopilación de registros)</span><span class="sxs-lookup"><span data-stu-id="94597-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="94597-104">En este artículo se proporcionan los pasos para recopilar registros de Azure AD B2C de forma que pueda diagnosticar problemas con sus directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="94597-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="94597-105">Actualmente, hello registros de actividad detallado aquí descritos están diseñados **sólo** tooaid en el desarrollo de directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="94597-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="94597-106">No use el modo de desarrollo en producción.</span><span class="sxs-lookup"><span data-stu-id="94597-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="94597-107">Registros de recopilación de todas las notificaciones enviadas tooand desde proveedores de identidades de Hola durante el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="94597-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="94597-108">Si se utiliza en producción, desarrollador Hola asume la responsabilidad de PII (privada información de identificación) recopilado en registro de información de la aplicación hello que les pertenecen.</span><span class="sxs-lookup"><span data-stu-id="94597-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="94597-109">Estos registros detallados solo se recopilan cuando se coloca la directiva de hello en **modo de desarrollo**.</span><span class="sxs-lookup"><span data-stu-id="94597-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="94597-110">Uso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="94597-110">Use Application Insights</span></span>

<span data-ttu-id="94597-111">B2C de Azure AD admite una característica para enviar datos tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="94597-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="94597-112">Application Insights proporciona una manera toodiagnose excepciones y visualizar los problemas de rendimiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94597-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="94597-113">Configuración de Application Insights</span><span class="sxs-lookup"><span data-stu-id="94597-113">Setup Application Insights</span></span>

1. <span data-ttu-id="94597-114">Vaya toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="94597-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="94597-115">Asegúrese de que está en el inquilino de hello con su suscripción de Azure (no el inquilino de Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="94597-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="94597-116">Haga clic en **+ nuevo** en el menú de navegación izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="94597-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="94597-117">Busque y seleccione **Application Insights** y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="94597-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="94597-118">Rellene el formulario de Hola y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="94597-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="94597-119">Seleccione **General** para hello **tipo de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="94597-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="94597-120">Una vez que se ha creado el recurso de hello, abra el recurso de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="94597-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="94597-121">Buscar **propiedades** en Hola menú izquierdo y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="94597-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="94597-122">Hola copia **clave de instrumentación** y guardar para la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="94597-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="94597-123">Configurar la directiva personalizada de Hola</span><span class="sxs-lookup"><span data-stu-id="94597-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="94597-124">Abra el archivo de RP hello (por ejemplo, SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="94597-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="94597-125">Agregar Hola después atributos toohello `<TrustFrameworkPolicy>` elemento:</span><span class="sxs-lookup"><span data-stu-id="94597-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="94597-126">Si no existe ya, agregue un nodo secundario `<UserJourneyBehaviors>` toohello `<RelyingParty>` nodo.</span><span class="sxs-lookup"><span data-stu-id="94597-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="94597-127">Debe estar inmediatamente después de hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="94597-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="94597-128">Agregar Hola después de nodo como un elemento secundario de hello `<UserJourneyBehaviors>` elemento.</span><span class="sxs-lookup"><span data-stu-id="94597-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="94597-129">Asegúrese de que tooreplace `{Your Application Insights Key}` con hello **clave de instrumentación** obtenida de Application Insights en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="94597-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="94597-130">`DeveloperMode="true"`indica la telemetría de hello ApplicationInsights tooexpedite a través de la canalización de procesamiento de hello, bueno para el desarrollo, pero está restringido en grandes volúmenes.</span><span class="sxs-lookup"><span data-stu-id="94597-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="94597-131">`ClientEnabled="true"`envía el script del lado cliente hello ApplicationInsights para realizar el seguimiento de errores de cliente y la vista de página (no es necesarios).</span><span class="sxs-lookup"><span data-stu-id="94597-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="94597-132">`ServerEnabled="true"`envía Hola existente JSON UserJourneyRecorder como una visión tooApplication de evento personalizado.</span><span class="sxs-lookup"><span data-stu-id="94597-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="94597-133">Sample:</span><span class="sxs-lookup"><span data-stu-id="94597-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="94597-134">Cargar directiva Hola.</span><span class="sxs-lookup"><span data-stu-id="94597-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="94597-135">Ver registros de hello en Application Insights</span><span class="sxs-lookup"><span data-stu-id="94597-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="94597-136">Hay un breve retraso (inferior a cinco minutos) antes de que pueda ver nuevos registros en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="94597-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="94597-137">Abra el recurso de Application Insights de Hola que creó en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="94597-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="94597-138">Hola **Introducción** menú, haga clic en **análisis**.</span><span class="sxs-lookup"><span data-stu-id="94597-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="94597-139">Abra una nueva pestaña en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="94597-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="94597-140">Esta es una lista de consultas, puede usar registros de hello toosee</span><span class="sxs-lookup"><span data-stu-id="94597-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="94597-141">Consultar</span><span class="sxs-lookup"><span data-stu-id="94597-141">Query</span></span> | <span data-ttu-id="94597-142">Descripción</span><span class="sxs-lookup"><span data-stu-id="94597-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="94597-143">traces</span><span class="sxs-lookup"><span data-stu-id="94597-143">traces</span></span> | <span data-ttu-id="94597-144">Ver todos los registros de hello generados por Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="94597-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="94597-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="94597-145">traces \\</span></span>| <span data-ttu-id="94597-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="94597-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="94597-147">Ver todos los registros de hello generados por Azure AD B2C para hello último día</span><span class="sxs-lookup"><span data-stu-id="94597-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="94597-148">las entradas de Hello pueden ser largos.</span><span class="sxs-lookup"><span data-stu-id="94597-148">hello entries may be long.</span></span>  <span data-ttu-id="94597-149">Exportar tooCSV para obtener una visión más cercano.</span><span class="sxs-lookup"><span data-stu-id="94597-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="94597-150">Puede aprender más acerca de la herramienta de análisis de hello [aquí](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="94597-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="94597-151">Comunidad de Hello ha desarrollado un a los desarrolladores del Visor toohelp identidad de usuario del proceso.</span><span class="sxs-lookup"><span data-stu-id="94597-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="94597-152">No está admitido por Microsoft y está disponible estrictamente tal cual.</span><span class="sxs-lookup"><span data-stu-id="94597-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="94597-153">Lee de la instancia de Application Insights y proporciona una vista de estructura bien Hola viaje eventos de usuarios.</span><span class="sxs-lookup"><span data-stu-id="94597-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="94597-154">Obtener el código fuente de hello e implementarlo en su propia solución.</span><span class="sxs-lookup"><span data-stu-id="94597-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="94597-155">Actualmente, hello registros de actividad detallado aquí descritos están diseñados **sólo** tooaid en el desarrollo de directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="94597-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="94597-156">No use el modo de desarrollo en producción.</span><span class="sxs-lookup"><span data-stu-id="94597-156">Do not use development mode in production.</span></span>  <span data-ttu-id="94597-157">Registros de recopilación de todas las notificaciones enviadas tooand desde proveedores de identidades de Hola durante el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="94597-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="94597-158">Si se utiliza en producción, desarrollador Hola asume la responsabilidad de PII (privada información de identificación) recopilado en registro de información de la aplicación hello que les pertenecen.</span><span class="sxs-lookup"><span data-stu-id="94597-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="94597-159">Estos registros detallados solo se recopilan cuando se coloca la directiva de hello en **modo de desarrollo**.</span><span class="sxs-lookup"><span data-stu-id="94597-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

<span data-ttu-id="94597-160">[Github Repository for Unsupported Custom Policy Samples and Related tools](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies) (Repositorio de Github con ejemplos de directivas personalizadas no admitidas y herramientas relacionadas)</span><span class="sxs-lookup"><span data-stu-id="94597-160">[Github Repository for Unsupported Custom Policy Samples and Related tools](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)</span></span>



## <a name="next-steps"></a><span data-ttu-id="94597-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94597-161">Next Steps</span></span>

<span data-ttu-id="94597-162">Explorar datos hello en toohelp Application Insights que comprenda cómo Hola identidad experiencia Framework B2C subyacente funciona toodeliver experiencias de su propia identidad.</span><span class="sxs-lookup"><span data-stu-id="94597-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
