---
title: "aaaCreate una aplicación web en un entorno de servicio de aplicaciones v1"
description: "Obtenga información acerca de cómo toocreate las aplicaciones web y planes de servicio de aplicaciones en un entorno de servicio de aplicaciones v1"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a>Creación de una aplicación web en una instancia de App Service Environment v1

> [!NOTE]
> Este artículo trata sobre Hola v1 de entorno del servicio de aplicaciones.  Hay una versión más reciente de hello entorno del servicio de aplicación que es más fácil toouse y se ejecuta en una infraestructura más eficaz. toolearn más información acerca de la nueva versión de hello iniciar con hello [toohello Introducción entono](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Información general
Este tutorial muestra cómo toocreate web aplicaciones y los planes de servicio de aplicaciones en un [entono v1](app-service-app-service-environment-intro.md) (ASE). 

> [!NOTE]
> Si desea toolearn cómo toocreate una aplicación web, pero no es necesario toodo en un entorno de servicio de aplicaciones, consulte [crear una aplicación web de .NET](app-service-web-get-started-dotnet.md) o uno de hello relacionados con tutoriales de otros lenguajes y marcos.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
En este tutorial se supone que ha creado un entorno del Servicio de aplicaciones. Si no es así, consulte [Creación de un entorno del Servicio de aplicaciones](app-service-web-how-to-create-an-app-service-environment.md). 

## <a name="create-a-web-app"></a>Creación de una aplicación web
1. Hola [Portal de Azure](https://portal.azure.com/), haga clic en **nuevo > Web y móvil > aplicación Web**. 
   
    ![][1]
2. Seleccione su suscripción.  
   
    Si tiene varias suscripciones a tener en cuenta que toocreate una aplicación en el entorno de servicio de aplicaciones, necesita toouse Hola misma suscripción que utilizó al crear el entorno de Hola. 
3. Seleccione o cree un grupo de recursos.
   
    *Grupos de recursos* , es posible toomanage relacionados con recursos de Azure como una unidad y son útiles al establecer *el control de acceso basado en roles* reglas (RBAC) para las aplicaciones. Para más información, consulte [Información general de Azure Resource Manager][ResourceGroups]. 
4. Seleccione o cree un plan del Servicio de aplicaciones.
   
    Los *planes de App Service* son conjuntos administrados de aplicaciones web.  Normalmente cuando se selecciona precios, precio Hola cobrado es toohello aplicado un plan de servicio de aplicaciones en lugar de aplicaciones individuales de toohello. En un ASE se paga por el proceso de hello asignar toohello ASE instancias en lugar de lo que ha enumerado con ASP.  tooscale número Hola de instancias de una aplicación web se escalar instancias Hola de su plan de servicio de aplicaciones y afecta a todas las aplicaciones web hello en ese plan.  Algunas características, como los espacios del sitio o la integración de red virtual también tienen restricciones en la cantidad de plan de Hola.  Para obtener más información, consulte [Información general sobre los planes de Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)
   
    Puede identificar Hola que planes de servicio de aplicaciones en su ASE examinando la ubicación de Hola que se indica en el nombre del plan Hola.  
   
    ![][5]
   
    Si desea toouse un plan de servicio de aplicaciones que ya existe en el entorno de servicio de aplicaciones, seleccione ese plan. Si desea toocreate un nuevo plan de servicio de aplicaciones, vea Hola pasos de la sección de este tutorial, [crear un plan de servicio de aplicaciones en un entorno de servicio de aplicaciones](#createplan).
5. Escriba nombre de hello para la aplicación web y, a continuación, haga clic en **crear**. 
   
    Si su ASE usa una dirección URL de hello VIP externa de una aplicación en un ASE es: [*sitename*]. [ *nombre de su entorno de servicio de aplicación*]. p.azurewebsites.net en lugar de [*sitename*]. azurewebsites.net
   
    Si su ASE usa una dirección URL de VIP interno, a continuación, Hola de una aplicación que trata de ASE: [*sitename*]. [ *subdominio especificado durante la creación de ASE*]   
    Después de seleccionar la página ASP durante la creación de ASE verá subdominio Hola actualizar a continuación **nombre**

## <a name="createplan"></a> Creación de un plan del Servicio de aplicaciones
Cuando crea un plan del Servicio de aplicaciones en un entorno del Servicio de aplicaciones, sus opciones de trabajo son diferentes dado que no hay trabajos compartidos en un ASE.  los trabajos de Hello tiene toouse son hello las que se han asignado toohello ASE Administrador de Hola.  Esto significa que toocreate un nuevo plan, debe toohave más trabajadores asignados tooyour ASE grupo de trabajo que el número total de Hola de instancias a través de todos los planes que ya se encuentran en ese grupo de trabajo de.  Si no tiene suficiente trabajadores en su toocreate de grupo de trabajo de ASE su plan, debe toowork con su tooget de administración de ASE que les agregan.

Otra diferencia con planes de servicio de aplicaciones hospedadas por un entorno de servicio de aplicaciones es la falta de Hola de selección de precios.  Si tiene un entorno de servicio de aplicaciones se paga por los recursos de proceso utilizados por el sistema de hello y no tiene cargos agregados para planes de hello en ese entorno.  Normalmente, cuando crea un plan del Servicio de aplicaciones, selecciona el plan de precios que determina su facturación.  Un entorno del Servicio de aplicaciones es esencialmente una ubicación privada donde puede crear contenido.  Se paga por el entorno de Hola y toohost no su contenido.

Hello instrucciones siguientes muestran cómo toocreate un servicio de aplicación del plan mientras está creando una aplicación web, como se explica en la sección anterior de Hola de tutorial Hola.

1. Haga clic en **crear nuevo** en Hola plan selección interfaz de usuario y proporcione un nombre para el plan tal como haría normalmente fuera un ASE.
2. Seleccione ASE de Hola que desee toouse desde el selector de ubicación.
   
    Como un entorno del Servicio de aplicaciones es básicamente una ubicación de implementación privada, se muestra en Ubicación. 
   
    ![][2]
   
    Después de la selección de un ASE en el selector de ubicación de hello, Hola actualizaciones de interfaz de usuario de creación de plan de servicio de aplicaciones.  ubicación de Hola ahora muestra nombre Hola de hello sistema ASE y región Hola está en, y Hola selector de plan de precios se sustituye por un selector de grupo de trabajo.  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a>Selección de un grupo de trabajo
Normalmente en el servicio de aplicación de Azure y fuera de un entorno de servicio de aplicaciones, hay 3 tamaños de proceso que están disponibles con la selección de Hola de un plan de precios dedicado.  De manera similar, para un ASE puede definir los conjuntos de too3 de trabajadores y especificar el tamaño de proceso de Hola que se usa para ese grupo de trabajo.  ¿Qué significa eso para los inquilinos de hello ASE es que en lugar de seleccionar un plan de precios con un tamaño de proceso para el plan de servicio de aplicaciones, seleccione lo que se denomina un *grupo de trabajo*.  

selección de grupo de trabajo de Hello interfaz de usuario muestra el tamaño de proceso de hello usa para ese grupo de trabajo por debajo del nombre de Hola.  Hello cantidad disponible hace referencia toohow muchas instancias están disponibles para su uso en ese grupo de proceso.  grupo total de Hello realmente puede tener más instancias de que este número, pero este valor hace referencia toosimply están cuántos no en uso.  Si necesita tooadjust tooadd de su entorno de servicio de aplicaciones de proceso más recursos, vea [cómo configurar el entorno de servicio de aplicación](app-service-web-configure-an-app-service-environment.md).

![][4]

En este ejemplo puede ver que solo hay dos grupos de trabajo disponibles. Eso es porque el Administrador de ASE Hola solo asigna hosts en los grupos de trabajo de dos.  Hola en tercer lugar, aparecerían cuando hay máquinas virtuales asignadas a ella.  

## <a name="after-web-app-creation"></a>Después de la creación de la aplicación web
Hay algunas consideraciones para ejecutar aplicaciones web y administrar planes de servicio de aplicaciones en un ASE que necesitan toobe tener en cuenta.  

Tal y como se indicó anteriormente, propietario de Hola de hello ASE es responsable de tamaño de hello del sistema de Hola y así también son responsables de garantizar que no hay suficientes hello toohost de capacidad había deseada planes de servicio de aplicaciones. Si no hay ningún trabajador disponible, no podrá ser capaz de toocreate su plan de servicio de aplicaciones.  Este es también true tooscaling seguridad de la aplicación web.  Si necesita más instancias, tendrás que tooget su tooadd de administración del entorno de servicio de aplicaciones más trabajos.

Después de crear la aplicación web y el plan de servicio de aplicaciones es una buena idea tooscale, configúrelo.  En un ASE siempre debe toohave al menos 2 instancias de la tolerancia a errores tooprovide plan servicio de aplicaciones para las aplicaciones.  Ajuste de escala en un servicio de aplicaciones de plan en un ASE es Hola igual como lo hace normalmente a través de hello plan de servicio de aplicaciones interfaz de usuario.  Para obtener más información acerca de cómo escalar, [cómo tooscale una aplicación web en un entorno de servicio de aplicaciones](app-service-web-scale-a-web-app-in-an-app-service-environment.md)

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
