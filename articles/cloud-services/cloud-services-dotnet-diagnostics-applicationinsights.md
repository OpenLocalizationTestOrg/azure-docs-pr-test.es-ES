---
title: Servicios en la nube con Application Insights aaaTroubleshoot | Documentos de Microsoft
description: "Obtenga información acerca de cómo emite tootroubleshoot servicio en la nube mediante el uso de datos de Application Insights tooprocess diagnósticos de Azure."
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a>Solucionar problemas de Servicios en la nube con Application Insights
Con [Azure SDK 2.8](https://azure.microsoft.com/downloads/) y 1.5 de extensión de diagnósticos de Azure, puede enviar datos de diagnóstico de Azure para su servicio en la nube directamente tooApplication visión. Hola registros recopilados con diagnósticos de Azure&mdash;incluidos los registros de aplicaciones, los registros de eventos de Windows, registros de ETW y los contadores de rendimiento&mdash;pueden enviarse tooApplication visión. A continuación, puede visualizar esta información en el portal de Application Insights Hola interfaz de usuario. A continuación, puede usar Hola Application Insights SDK tooget visiones métricas y los registros que proceden de su aplicación, así como sistema de Hola y datos de nivel de infraestructura que provienen de diagnósticos de Azure.

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a>Configurar diagnósticos de Azure toosend datos tooApplication visión
Siga estos tooset de pasos de la nube servicio proyecto toosend diagnósticos de Azure datos tooApplication visión.

1. En el Explorador de soluciones de Visual Studio, haga clic en un rol y seleccione **propiedades** Diseñador de roles de tooopen Hola.

    ![Propiedades de rol del Explorador de soluciones][1]

2. Hola **diagnósticos** sección Hola del Diseñador de roles, seleccione hello **enviar datos de diagnóstico tooApplication visión** opción.

    ![Diseñador de roles enviar diagnósticos información sobre los datos tooapplication][2]

3. En el cuadro de diálogo de Hola que aparece, seleccione el recurso de Application Insights de Hola que desea que los datos de diagnóstico de Azure toosend Hola a. cuadro de diálogo de Hello permite tooselect un recurso de Application Insights existente desde su suscripción o toomanually especificar una clave de instrumentación para un recurso de Application Insights. Para más información sobre la creación de un recurso de Application Insights, consulte [Creación de recursos en Application Insights](../application-insights/app-insights-create-new-resource.md).

    ![seleccionar recurso de application insights][3]

    Cuando haya agregado el recurso de Application Insights hello, clave de instrumentación de Hola para ese recurso se almacena como un valor de configuración de servicio con el nombre de hello **APPINSIGHTS_INSTRUMENTATIONKEY**. Puede cambiar esta opción para cada configuración de servicio o de entorno. toodo por lo tanto, seleccione una configuración diferente de hello **configuración del servicio** lista y especificar una nueva clave de instrumentación para dicha configuración.

    ![seleccionar configuración de servicio][4]

    Hola **APPINSIGHTS_INSTRUMENTATIONKEY** valor de configuración se utiliza por extensión de diagnósticos de Visual Studio tooconfigure Hola con información de recursos de Application Insights adecuada de Hola durante la publicación. valor de configuración de Hello es una manera cómoda de definir las claves de instrumentación distintos para diferentes configuraciones del servicio. Visual Studio se traduzca esa configuración e insertarlo en hello diagnósticos pública configuración de la extensión durante Hola proceso de publicación. proceso de hello toosimplify de configuración de extensión de diagnósticos de hello con PowerShell, salida del paquete Hola desde Visual Studio también contiene Hola XML de configuración pública con clave de instrumentación de Application Insights adecuado de Hola. archivos de configuración pública de Hola se crean en la carpeta de extensiones de Hola y seguir el patrón de hello *PaaSDiagnostics.&lt; RoleName&gt;. PubConfig.xml*. Todas las implementaciones basadas en PowerShell pueden usar este patrón toomap cada rol de tooa de configuración.

4) tooconfigure diagnósticos de Azure toosend todos los registros de nivel de error y los contadores de rendimiento recopilados por hello diagnósticos de Azure agente tooApplication visión, habilitar hello **enviar datos de diagnóstico tooApplication visión** opción. 

    Si desea que toofurther configurar qué datos se envían información de tooApplication, debe editar manualmente hello *diagnostics.wadcfgx* archivo para cada rol. Vea [configurar diagnósticos de Azure toosend datos tooApplication visión](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn más sobre cómo actualizar manualmente la configuración de Hola.

Al servicio de nube de hello toosend configurado los diagnósticos de Azure datos tooapplication visión, puede implementarla tooAzure normalmente, asegurándose de hello extensión de diagnósticos de Azure está habilitada. Para más información, consulte el artículo de [Publicación de un servicio en la nube con Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a>Visualización de datos de Diagnósticos de Azure en Application Insights
Hola telemetría de diagnóstico de Azure se muestra en hello Application Insights recurso configurado para el servicio de nube.

Tipos de registro de diagnósticos de Azure asignan conceptos de visión tooApplication de las siguientes maneras:

* Los contadores de rendimiento se muestran como métricas personalizadas en Application Insights.
* Los registros de eventos de Windows se muestran como seguimientos y eventos personalizados en Application Insights.
* Los registros de aplicación, los registros de ETW y los registros de infraestructura de diagnóstico se muestran como seguimientos en Application Insights.

tooview datos de diagnóstico de Azure en Application Insights, siga uno de los procedimientos de hello:

* Use [explorer métricas](../application-insights/app-insights-metrics-explorer.md) toovisualize cualquier rendimiento personalizados contadores o los recuentos de diferentes tipos de eventos de registro de eventos de Windows.

    ![Métricas personalizadas en el Explorador de métricas][5]

* Use [búsqueda](../application-insights/app-insights-diagnostic-search.md) toosearch a través de los registros de seguimiento de hello enviados por diagnósticos de Azure. Por ejemplo, si ha provocado una excepción no controlada Hola rol toocrash y reciclaje, obtener información acerca de la excepción de Hola aparecerá en hello *aplicación* canal de *registro de eventos de Windows*. Puede usar búsqueda toolook en hello error de registro de eventos de Windows y realizar seguimiento de pila completo de Hola para hello excepción toohelp buscar Hola causa del problema de Hola.

    ![Buscar seguimientos][6]

## <a name="next-steps"></a>Pasos siguientes
* [Agregar servicio de nube de hello Application Insights SDK tooyour](../application-insights/app-insights-cloudservices.md) toosend datos acerca de las solicitudes, excepciones, las dependencias y cualquier telemetría personalizada de la aplicación. Cuando se combina con datos de diagnóstico de Azure de hello, esta información se puede obtener una vista completa de la aplicación y del sistema, todo ello en Hola mismo recurso de Application Insight.  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
