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
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C: Collecting Logs (Azure Active Directory B2C: recopilación de registros)

En este artículo se proporcionan los pasos para recopilar registros de Azure AD B2C de forma que pueda diagnosticar problemas con sus directivas personalizadas.

>[!NOTE]
>Actualmente, hello registros de actividad detallado aquí descritos están diseñados **sólo** tooaid en el desarrollo de directivas personalizadas. No use el modo de desarrollo en producción.  Registros de recopilación de todas las notificaciones enviadas tooand desde proveedores de identidades de Hola durante el desarrollo.  Si se utiliza en producción, desarrollador Hola asume la responsabilidad de PII (privada información de identificación) recopilado en registro de información de la aplicación hello que les pertenecen.  Estos registros detallados solo se recopilan cuando se coloca la directiva de hello en **modo de desarrollo**.


## <a name="use-application-insights"></a>Uso de Application Insights

B2C de Azure AD admite una característica para enviar datos tooApplication visión.  Application Insights proporciona una manera toodiagnose excepciones y visualizar los problemas de rendimiento de la aplicación.

### <a name="setup-application-insights"></a>Configuración de Application Insights

1. Vaya toohello [portal de Azure](https://portal.azure.com). Asegúrese de que está en el inquilino de hello con su suscripción de Azure (no el inquilino de Azure AD B2C).
1. Haga clic en **+ nuevo** en el menú de navegación izquierdo de Hola.
1. Busque y seleccione **Application Insights** y, a continuación, haga clic en **Crear**.
1. Rellene el formulario de Hola y haga clic en **crear**. Seleccione **General** para hello **tipo de aplicación**.
1. Una vez que se ha creado el recurso de hello, abra el recurso de Application Insights Hola.
1. Buscar **propiedades** en Hola menú izquierdo y haga clic en él.
1. Hola copia **clave de instrumentación** y guardar para la sección siguiente Hola.

### <a name="set-up-hello-custom-policy"></a>Configurar la directiva personalizada de Hola

1. Abra el archivo de RP hello (por ejemplo, SignUpOrSignin.xml).
1. Agregar Hola después atributos toohello `<TrustFrameworkPolicy>` elemento:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. Si no existe ya, agregue un nodo secundario `<UserJourneyBehaviors>` toohello `<RelyingParty>` nodo. Debe estar inmediatamente después de hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Agregar Hola después de nodo como un elemento secundario de hello `<UserJourneyBehaviors>` elemento. Asegúrese de que tooreplace `{Your Application Insights Key}` con hello **clave de instrumentación** obtenida de Application Insights en la sección anterior de Hola.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`indica la telemetría de hello ApplicationInsights tooexpedite a través de la canalización de procesamiento de hello, bueno para el desarrollo, pero está restringido en grandes volúmenes.
  * `ClientEnabled="true"`envía el script del lado cliente hello ApplicationInsights para realizar el seguimiento de errores de cliente y la vista de página (no es necesarios).
  * `ServerEnabled="true"`envía Hola existente JSON UserJourneyRecorder como una visión tooApplication de evento personalizado.
Sample:

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

3. Cargar directiva Hola.

### <a name="see-hello-logs-in-application-insights"></a>Ver registros de hello en Application Insights

>[!NOTE]
> Hay un breve retraso (inferior a cinco minutos) antes de que pueda ver nuevos registros en Application Insights.

1. Abra el recurso de Application Insights de Hola que creó en hello [portal de Azure](https://portal.azure.com).
1. Hola **Introducción** menú, haga clic en **análisis**.
1. Abra una nueva pestaña en Application Insights.
1. Esta es una lista de consultas, puede usar registros de hello toosee

| Consultar | Descripción |
|---------------------|--------------------|
traces | Ver todos los registros de hello generados por Azure AD B2C |
traces \| where timestamp > ago(1d) | Ver todos los registros de hello generados por Azure AD B2C para hello último día

las entradas de Hello pueden ser largos.  Exportar tooCSV para obtener una visión más cercano.

Puede aprender más acerca de la herramienta de análisis de hello [aquí](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>Comunidad de Hello ha desarrollado un a los desarrolladores del Visor toohelp identidad de usuario del proceso.  No está admitido por Microsoft y está disponible estrictamente tal cual.  Lee de la instancia de Application Insights y proporciona una vista de estructura bien Hola viaje eventos de usuarios.  Obtener el código fuente de hello e implementarlo en su propia solución.

>[!NOTE]
>Actualmente, hello registros de actividad detallado aquí descritos están diseñados **sólo** tooaid en el desarrollo de directivas personalizadas. No use el modo de desarrollo en producción.  Registros de recopilación de todas las notificaciones enviadas tooand desde proveedores de identidades de Hola durante el desarrollo.  Si se utiliza en producción, desarrollador Hola asume la responsabilidad de PII (privada información de identificación) recopilado en registro de información de la aplicación hello que les pertenecen.  Estos registros detallados solo se recopilan cuando se coloca la directiva de hello en **modo de desarrollo**.

[Github Repository for Unsupported Custom Policy Samples and Related tools](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies) (Repositorio de Github con ejemplos de directivas personalizadas no admitidas y herramientas relacionadas)



## <a name="next-steps"></a>Pasos siguientes

Explorar datos hello en toohelp Application Insights que comprenda cómo Hola identidad experiencia Framework B2C subyacente funciona toodeliver experiencias de su propia identidad.
