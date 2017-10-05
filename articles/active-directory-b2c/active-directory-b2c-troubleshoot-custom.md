---
title: 'Application Insights para resolver problemas de las directivas personalizadas: Azure AD B2C | Microsoft Docs'
description: "cómo configurar Application Insights para realizar el seguimiento de la ejecución de las directivas personalizadas"
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
ms.openlocfilehash: 8c79df33cd5f04f490e2cc6372f7e8ac1c4d9bbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="734a2-103">Azure Active Directory B2C: Collecting Logs (Azure Active Directory B2C: recopilación de registros)</span><span class="sxs-lookup"><span data-stu-id="734a2-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="734a2-104">En este artículo se proporcionan los pasos para recopilar registros de Azure AD B2C de forma que pueda diagnosticar problemas con sus directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="734a2-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="734a2-105">Actualmente, los registros de actividad descritos aquí están diseñados **SOLO** para ayudar en el desarrollo de directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="734a2-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="734a2-106">No use el modo de desarrollo en producción.</span><span class="sxs-lookup"><span data-stu-id="734a2-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="734a2-107">Los registros recopilan todas las notificaciones que se envían y se reciben de los proveedores de identidad durante el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="734a2-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="734a2-108">Si se utilizan en producción, el programador asume la responsabilidad sobre la PII (información personal de identificación) recopilada en el registro de información de la instancia de App Insights que le pertenece.</span><span class="sxs-lookup"><span data-stu-id="734a2-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="734a2-109">Estos registros detallados solo se recopilan cuando la directiva se coloca en **MODO DE DESARROLLO**.</span><span class="sxs-lookup"><span data-stu-id="734a2-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="734a2-110">Uso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="734a2-110">Use Application Insights</span></span>

<span data-ttu-id="734a2-111">Azure AD B2C admite una característica para enviar datos a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="734a2-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="734a2-112">Application Insights proporciona un modo de diagnosticar excepciones y visualizar problemas de rendimiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="734a2-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="734a2-113">Configuración de Application Insights</span><span class="sxs-lookup"><span data-stu-id="734a2-113">Setup Application Insights</span></span>

1. <span data-ttu-id="734a2-114">Vaya al [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="734a2-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="734a2-115">Asegúrese de que se encuentra en el inquilino con su suscripción de Azure (no su inquilino de Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="734a2-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="734a2-116">Haga clic en **+ Nuevo** en el menú de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="734a2-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="734a2-117">Busque y seleccione **Application Insights** y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="734a2-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="734a2-118">Complete el formulario y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="734a2-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="734a2-119">Seleccione **General** para el **Tipo de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="734a2-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="734a2-120">Una vez creado el recurso, abra el recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="734a2-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="734a2-121">Busque **Propiedades** en el menú izquierdo y haga clic.</span><span class="sxs-lookup"><span data-stu-id="734a2-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="734a2-122">Copie la **Clave de instrumentación** y guárdela para la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="734a2-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="734a2-123">Configuración de la directiva personalizada</span><span class="sxs-lookup"><span data-stu-id="734a2-123">Set up the custom policy</span></span>

1. <span data-ttu-id="734a2-124">Abra el archivo RP (p. ej., SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="734a2-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="734a2-125">Agregue los siguientes atributos al elemento `<TrustFrameworkPolicy>`:</span><span class="sxs-lookup"><span data-stu-id="734a2-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="734a2-126">Si aún no existe, agregue un nodo secundario `<UserJourneyBehaviors>` al nodo `<RelyingParty>`.</span><span class="sxs-lookup"><span data-stu-id="734a2-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="734a2-127">Tiene que estar situado inmediatamente después de `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="734a2-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="734a2-128">Agregue el siguiente nodo como nodo secundario del elemento `<UserJourneyBehaviors>`.</span><span class="sxs-lookup"><span data-stu-id="734a2-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="734a2-129">Asegúrese de reemplazar `{Your Application Insights Key}` por la **Clave de instrumentación** que obtuvo de Application Insights en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="734a2-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="734a2-130">`DeveloperMode="true"` indica a ApplicationInsights que acelere la telemetría a través de la canalización de procesamiento, buena para el desarrollo, pero limitada en volúmenes elevados.</span><span class="sxs-lookup"><span data-stu-id="734a2-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="734a2-131">`ClientEnabled="true"` envía el script del lado cliente ApplicationInsights para realizar un seguimiento de la vista de página y de los errores del lado cliente (no es necesario).</span><span class="sxs-lookup"><span data-stu-id="734a2-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="734a2-132">`ServerEnabled="true"` envía el JSON UserJourneyRecorder como evento personalizado a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="734a2-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="734a2-133">Sample:</span><span class="sxs-lookup"><span data-stu-id="734a2-133">Sample:</span></span>

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

3. <span data-ttu-id="734a2-134">Cargue la directiva.</span><span class="sxs-lookup"><span data-stu-id="734a2-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="734a2-135">Visualización de registros en Application Insights</span><span class="sxs-lookup"><span data-stu-id="734a2-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="734a2-136">Hay un breve retraso (inferior a cinco minutos) antes de que pueda ver nuevos registros en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="734a2-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="734a2-137">Abra el recurso de Application Insights que ha creado en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="734a2-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="734a2-138">En el menú **Información general**, haga clic en **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="734a2-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="734a2-139">Abra una nueva pestaña en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="734a2-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="734a2-140">A continuación se muestra una lista de consultas que puede usar para ver los registros</span><span class="sxs-lookup"><span data-stu-id="734a2-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="734a2-141">Consultar</span><span class="sxs-lookup"><span data-stu-id="734a2-141">Query</span></span> | <span data-ttu-id="734a2-142">Descripción</span><span class="sxs-lookup"><span data-stu-id="734a2-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="734a2-143">traces</span><span class="sxs-lookup"><span data-stu-id="734a2-143">traces</span></span> | <span data-ttu-id="734a2-144">Ver todos los registros generados por Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="734a2-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="734a2-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="734a2-145">traces \\</span></span>| <span data-ttu-id="734a2-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="734a2-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="734a2-147">Ver todos los registros generados por Azure AD B2C para el último día</span><span class="sxs-lookup"><span data-stu-id="734a2-147">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="734a2-148">Las entradas pueden ser largas.</span><span class="sxs-lookup"><span data-stu-id="734a2-148">The entries may be long.</span></span>  <span data-ttu-id="734a2-149">Exporte a un archivo CSV para realizar un examen más detallado.</span><span class="sxs-lookup"><span data-stu-id="734a2-149">Export to CSV for a closer look.</span></span>

<span data-ttu-id="734a2-150">Puede obtener más información sobre estas herramientas de Analytics [aquí](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="734a2-150">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="734a2-151">La Comunidad ha desarrollado un visor de recorrido de usuario para ayudar a los desarrolladores de identidad.</span><span class="sxs-lookup"><span data-stu-id="734a2-151">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="734a2-152">No está admitido por Microsoft y está disponible estrictamente tal cual.</span><span class="sxs-lookup"><span data-stu-id="734a2-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="734a2-153">Lee de la instancia de Application Insights y proporciona una vista bien estructurada de los eventos de recorrido de usuario.</span><span class="sxs-lookup"><span data-stu-id="734a2-153">It reads from your Application Insights instance and provides a well-structure view of the user journey events.</span></span>  <span data-ttu-id="734a2-154">Proporciona el código fuente para implementarlo en su propia solución.</span><span class="sxs-lookup"><span data-stu-id="734a2-154">You obtain the source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="734a2-155">Actualmente, los registros de actividad descritos aquí están diseñados **SOLO** para ayudar en el desarrollo de directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="734a2-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="734a2-156">No use el modo de desarrollo en producción.</span><span class="sxs-lookup"><span data-stu-id="734a2-156">Do not use development mode in production.</span></span>  <span data-ttu-id="734a2-157">Los registros recopilan todas las notificaciones que se envían y se reciben de los proveedores de identidad durante el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="734a2-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="734a2-158">Si se utilizan en producción, el programador asume la responsabilidad sobre la PII (información personal de identificación) recopilada en el registro de información de la instancia de App Insights que le pertenece.</span><span class="sxs-lookup"><span data-stu-id="734a2-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="734a2-159">Estos registros detallados solo se recopilan cuando la directiva se coloca en **MODO DE DESARROLLO**.</span><span class="sxs-lookup"><span data-stu-id="734a2-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

<span data-ttu-id="734a2-160">[Github Repository for Unsupported Custom Policy Samples and Related tools](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies) (Repositorio de Github con ejemplos de directivas personalizadas no admitidas y herramientas relacionadas)</span><span class="sxs-lookup"><span data-stu-id="734a2-160">[Github Repository for Unsupported Custom Policy Samples and Related tools](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)</span></span>



## <a name="next-steps"></a><span data-ttu-id="734a2-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="734a2-161">Next Steps</span></span>

<span data-ttu-id="734a2-162">Explorar los datos de Application Insights para ayudarle a entender cómo funciona el marco de experiencia de identidad subyacente en B2C y poder entregar sus propias experiencias de identidad.</span><span class="sxs-lookup"><span data-stu-id="734a2-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
