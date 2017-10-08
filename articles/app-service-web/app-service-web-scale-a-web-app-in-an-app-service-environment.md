---
title: "aaaHow tooScale una aplicación en un entorno de servicio de aplicaciones"
description: "Escalado de una aplicación en un entorno del Servicio de aplicaciones"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a>Escalado de aplicaciones en un entorno del Servicio de aplicaciones
Hola servicio de aplicaciones de Azure hay puede escalar normalmente tres cosas:

* plan de precios
* tamaño de trabajo 
* número de instancias.

En un ASE no hay ninguna necesidad de tooselect o cambiar Hola plan de precios.  En términos de capacidades ya está en un nivel de capacidad de precios Premium.  

Con sentido tooworker tamaños, Hola, administrador ASE puede asignar tamaño Hola de toobe de recursos de proceso de hello utilizado para cada grupo de trabajo.  Eso significa que puede tener el grupo de trabajo 1 con recursos de proceso P4 y el grupo de trabajo 2 con recursos de proceso P1, si lo desea.  No tiene toobe en orden de tamaño.  Para obtener detalles sobre tamaños de Hola y su plan de tarifa vea aquí el documento de hello [tarifas de servicio de aplicación de Azure][AppServicePricing].  Esto deja Hola desarrollo para aplicaciones web y planes de servicio de aplicación en un entorno de servicio de aplicaciones toobe:

* selección de grupo de trabajo
* número de instancias

Cambiar cualquiera de los elementos se realiza a través de hello adecuados se muestra su ASE hospedados planes de servicio de aplicación de la interfaz de usuario.  

![][1]

No se puede escalar más allá de número de Hola de recursos de proceso disponibles en el grupo de trabajo de Hola que ASP se encuentra en la página ASP.  Si se necesitan recursos de proceso de ese grupo de trabajo debe tooget su tooadd de administrador ASE ellos.  Para obtener información alrededor de volver a configurar su ASE lea información Hola aquí: [cómo tooConfigure un entorno de servicio de aplicaciones][HowtoConfigureASE].  También puede tootake aprovechar Hola ASE de escalado automático características tooadd capacidad basada en programación o las métricas.  tooget vea más detalles sobre la configuración de escalado automático para el propio entorno Hola ASE [cómo tooconfigure Autoescala para un entorno de servicio de aplicaciones][ASEAutoscale].

Puede crear aplicaciones de varios planes de servicio mediante los recursos de proceso de los grupos de trabajo diferente, o puede usar Hola el mismo grupo de trabajo.  Por ejemplo si tiene (10) de los recursos de proceso disponibles en el trabajo del grupo 1, puede elegir toocreate plan de servicio de una aplicación con recursos de proceso (6) y planificar un segundo servicio de aplicación que utiliza (4) de los recursos de proceso.

### <a name="scaling-hello-number-of-instances"></a>Número de hello escalado de instancias
Cuando cree su aplicación web por primera vez en un Entorno del Servicio de aplicaciones, comenzará con una instancia.  También puede, a continuación, recursos de la aplicación de proceso de escalado horizontal tooadditional instancias tooprovide adicional.   

Si su ASE tiene suficiente capacidad, entonces esto es bastante sencillo.  Vaya tooyour Plan de servicio de aplicaciones que contiene sitios de Hola que desee tooscale seguridad y seleccione escala.  Se abrirá Hola donde puede establecer la escala de hello para la página ASP o configurar reglas de escalado automático para la página ASP manualmente la interfaz de usuario.  basta con establece la aplicación de escala de toomanually ***escalar*** demasiado***un recuento de instancias que especifique manualmente***.  Desde aquí arrastre quantity de toohello deseado del control deslizante de Hola o escríbalo en el regulador de hello cuadro siguiente toohello.  

![][2] 

reglas de escalado automático de Hola para un ASP en un trabajo de ASE Hola igual a como lo hacen normalmente.  Puede seleccionar ***Porcentaje de CPU*** en ***Escalar por*** y crear reglas de escalado automático para el ASP según el porcentaje de CPU, o puede crear reglas más complejas con ***reglas de programación y rendimiento***.  toosee completar más detalles sobre cómo configurar la Guía de Hola de uso de escalado automático aquí [escalar una aplicación de servicio de aplicaciones de Azure][AppScale]. 

### <a name="worker-pool-selection"></a>selección de grupo de trabajo
Como se indicó anteriormente, selección de grupo de trabajo de Hola se accede desde Hola interfaz de usuario de ASP.  Abrir la hoja de Hola para hello ASP que desee tooscale y seleccione el grupo de trabajo.  Verá todos los grupos de trabajo de Hola que configuró en el entorno de servicio de aplicaciones.  Si tienes un grupo de trabajo solo una, a continuación, solo verá un grupo de hello enumerado.  toochange qué trabajo bloque ASP está en, basta con seleccionar grupo de trabajo de hello desea que su toomove al Plan de servicio de aplicaciones.  

![][3]

Antes de mover la página ASP de tooanother de grupo de uno trabajo es importante toomake seguro de que tendrá la capacidad adecuada para la página ASP.  En lista de Hola de grupos de trabajo, no solo se muestra el nombre del grupo de trabajo de hello pero también puede ver el número de trabajadores están disponibles en ese grupo de trabajo.  Asegúrese de que hay suficiente toocontain disponibles instancias su Plan de servicio de aplicaciones.  Si se necesitan más recursos de proceso en el grupo de trabajo de hello desea toomove para, a continuación, obtener su tooadd de administrador ASE ellos.  

> [!NOTE]
> Mover que un ASP de grupo de uno trabajo provocará frío inicia de aplicaciones de hello en que ASP.  Esto puede causar solicitudes toorun lenta como la aplicación está fría iniciado en recursos de proceso nuevo Hola.  Hello arranque en frío se puede evitar mediante el uso de hello [aplicación activa la capacidad de] [ AppWarmup] en el servicio de aplicación de Azure.  módulo de inicialización de la aplicación Hello descrita en el artículo hello también funciona para arranques en frío porque el proceso de inicialización de hello también se invoca cuando las aplicaciones están inactivas iniciado en nuevos recursos de proceso. 
> 
> 

## <a name="getting-started"></a>Introducción
tooget iniciado con el entorno de servicio de aplicación, vea [cómo tooCreate un entorno de servicio de aplicaciones][HowtoCreateASE]

Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure][AzureAppService].

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
