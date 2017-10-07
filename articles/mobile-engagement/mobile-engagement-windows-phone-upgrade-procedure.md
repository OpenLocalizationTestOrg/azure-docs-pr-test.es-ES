---
title: "Procedimientos de actualización de Phone Silverlight SDK aaaWindows"
description: "Procedimientos de actualización de SDK de Windows Phone Silverlight para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a>Procedimientos de actualización del SDK de Windows Phone Silverlight
Si ya ha integrado una versión anterior de nuestro SDK en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.

Puede tener toofollow varios procedimientos si ejecutado varias versiones de hello SDK. Por ejemplo, si migra desde 0.10.1 too0.11.0 tiene toofirst siga Hola "de 0.9.0 too0.10.1" procedimiento, a continuación, Hola "de 0.10.1 too0.11.0" procedimiento.

## <a name="from-200-too330"></a>Desde 2.0.0 too3.3.0
### <a name="test-logs"></a>Registros de prueba
Registros de la consola producidos por hello SDK ahora pueden habilitada, deshabilitada o filtrado. toocustomize, propiedad de hello actualización `EngagementAgent.Instance.TestLogEnabled` tooone del valor de hello disponible de hello `EngagementTestLogLevel` enumeración, por ejemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a>Desde 1.1.1 too2.0.0
Hello siguiente describe cómo toomigrate una integración con el SDK de hello Capptain servicio ofrecido por Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain e interacción móvil no se Hola los mismos servicios y procedimiento Hola indicado a continuación sólo resalta cómo toomigrate Hola aplicación cliente. Migrar Hola SDK en la aplicación hello no migrará los datos de hello Capptain toohello Mobile Engagement servidores
> 
> 

Si va a migrar desde una versión anterior, por favor, consulte hello Capptain sitio web toomigrate too1.1.1 en primer lugar, aplique Hola procedimiento

### <a name="nuget-package"></a>Paquete de NuGet
Reemplace **Capptain.WindowsPhone** por el paquete Nuget **MicrosoftAzure.MobileEngagement**.

### <a name="applying-mobile-engagement"></a>Aplicar Mobile Engagement
Hola SDK utiliza el término de hello `Engagement`. Necesita tooupdate su toomatch proyecto este cambio.

Debe toouninstall el paquete de nuget Capptain actual. Tenga en cuenta que se van a quitar todos los cambios de la carpeta recursos de Capptain. Si desea que tookeep esos archivos, a continuación, haga una copia de ellos.

Después de eso, instale el nuevo paquete de nuget de Microsoft Azure Engagement hello en el proyecto. Puede encontrarlo directamente en [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement). Este reemplaza acción todos los archivos de recursos utilizados por la interacción y agrega Hola nueva contratación DLL tooyour referencias del proyecto.

Eliminando las referencias de Capptain DLL tienen tooclean las referencias del proyecto. Si no hace esto, versión de Hola de Capptain entrarán en conflicto y se producirán errores.

Si ha personalizado los recursos de Capptain, copie el contenido de los archivos antiguos y péguelos en los nuevos archivos de contratación Hola. Tenga en cuenta que los archivos xaml y cs tienen toobe actualizado.

Una vez completados estos pasos solo tiene tooreplace Capptain las referencias anteriores a por nuevas referencias de contratación Hola.

1. Todos los espacios de nombres de Capptain tienen toobe actualizado.
   
    Antes de la migración:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Después de la migración:
   
        using Microsoft.Azure.Engagement;
2. Todas las clases de Capptain que contengan "Capptain" deberían contener "Engagement".
   
    Antes de la migración:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Después de la migración:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. En el caso de los archivos xaml, también cambian el espacio de nombres y los atributos de Capptain.
   
    Antes de la migración:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Después de la migración:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Para hello otros recursos como imágenes de Capptain, tenga en cuenta que también han tenido toouse cuyo nombre ha cambiado "Interacción".

### <a name="application-id--sdk-key"></a>Identificador de aplicación o clave SDK
Engagement usa una cadena de conexión. Toospecify no tiene un identificador de la aplicación y una clave SDK con Mobile Engagement, solo tendrá toospecify una cadena de conexión. Esta se puede configurar en el archivo EngagementConfiguration.

configuración de la interacción de Hola se puede establecer el `Resources\EngagementConfiguration.xml` archivo del proyecto.

Editar este archivo toospecify:

* La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.

Si desea que toospecify en tiempo de ejecución en su lugar, se puede llamar a siguiente Hola método antes de la inicialización de agente de interacción de hello:

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

cadena de conexión de Hello para la aplicación se muestra en hello Portal clásico de Azure.

### <a name="items-name-change"></a>Cambio de nombre de elementos
Todos los elementos con el nombre *capptain* han cambiado a *engagement*. De forma similar para *Capptain* demasiado*interacción*.

Ejemplos de elementos Capptain que se usan habitualmente:

* CapptainConfiguration ahora se llama EngagementConfiguration
* CapptainAgent ahora se llama EngagementAgent
* CapptainReach ahora se llama EngagementReach
* CapptainHttpConfig ahora se llama EngagementHttpConfig
* GetCapptainPageName ahora se llama GetEngagementPageName

Tenga en cuenta que el cambio de nombre también afecta a los métodos invalidados.

