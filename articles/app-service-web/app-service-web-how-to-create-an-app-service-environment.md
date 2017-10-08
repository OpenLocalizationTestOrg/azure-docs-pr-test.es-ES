---
title: aaaHow tooCreate v1 de un entorno de servicio de aplicaciones
description: "Descripción del flujo de creación de una instancia de App Service Environment v1"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>¿Cómo tooCreate v1 de un entorno de servicio de aplicaciones 

> [!NOTE]
> Este artículo trata sobre Hola v1 de entorno del servicio de aplicaciones. Hay una versión más reciente de hello entorno del servicio de aplicación que es más fácil toouse y se ejecuta en una infraestructura más eficaz. toolearn más información acerca de la nueva versión de hello iniciar con hello [toohello Introducción entono](../app-service/app-service-environment/intro.md).
> 

### <a name="overview"></a>Información general
Hola entorno de servicio de aplicación (ASE) es una opción de servicio Premium de servicio de aplicaciones de Azure que ofrece una funcionalidad mejorada de la configuración que no está disponible en las marcas de varios inquilinos de Hola. característica de ASE Hola básicamente implementa Hola servicio de aplicaciones de Azure en red virtual de un cliente. toogain que ofrece un mayor conocimiento de las capacidades de Hola por entornos del servicio de aplicación lee hello [¿qué es un entorno de servicio de aplicaciones] [ WhatisASE] documentación.

### <a name="before-you-create-your-ase"></a>Antes de crear su ASE
Es importante toobe consciente de cosas hello que no se puede cambiar. Los aspectos que no se pueden cambiar sobre ASE una vez creado son:

* Ubicación
* La suscripción
* Grupo de recursos
* Red virtual usada
* La subred usada 
* Tamaño de la subred

Al seleccionar una red virtual y especificar una subred, asegurarse de que es lo suficientemente grande como tooaccomodate crecimiento futuro. 

### <a name="creating-an-app-service-environment-v1"></a>Creación de una instancia de App Service Environment v1
toocreate un v1 de entorno del servicio de aplicaciones necesita toosearch hello Azure Marketplace para ***entono v1***, o yendo a través de New -> Web + Mobile -> entorno del servicio de aplicaciones. toocreate una ASEv1:

1. Proporcione el nombre de Hola de su ASE. nombre de Hola que se especifica para ASE de Hola se utilizará para hello las aplicaciones creadas en hello ASE. Si el nombre del programa Hola ASE es appsvcenvdemo nombre de subdominio de hello sería. *appsvcenvdemo.p.azurewebsites.net*. Por tanto, si creó una aplicación llamada *mytestapp*, se podría obtener acceso a ella en *mytestapp.appsvcenvdemo.p.azurewebsites.net*. No puede utilizar el espacio en blanco en nombre de Hola de su ASE. Si utiliza caracteres en mayúsculas en el nombre de hello, nombre de dominio de hello será versión en minúsculas total de Hola de ese nombre. Si usa un ILB, su nombre ASE no se usa en su subdominio pero, en su lugar, se indica explícitamente durante la creación del ASE.
   
    ![][1]
2. Seleccione su suscripción. suscripción de Hello utilizada para su ASE también es hello uno que va a crear todas las aplicaciones en ese ASE con. No se puede colocar su ASE en una red virtual que se encuentra en otra suscripción
3. Seleccione o especifique un nuevo grupo de recursos. grupo de recursos de Hello destinado a su ASE se debe Hola igual que se usa para la red virtual. Si selecciona una red virtual existente, selección de grupos de recursos de Hola para su ASE será tooreflect actualizado de la red virtual.
   
    ![][2]
4. Realice las selecciones de red virtual y ubicación. Puede elegir toocreate una red virtual nueva o seleccione una red virtual existente. Si selecciona una red virtual nueva, puede especificar un nombre y una ubicación. Hello red virtual nueva tendrá Hola dirección intervalo 192.168.250.0/23 y una subred denominada **predeterminado** que se define como 192.168.250.0/24. Puede seleccionar también simplemente una red virtual de Resource Manager o clásica creadas previamente. Hola selección del tipo de dirección VIP determina si su ASE puede tener acceso directamente desde Hola internet (externa), o si utiliza un equilibrador de carga interno (ILB). más información acerca de esto leer toolearn [mediante un equilibrador de carga interno con un entorno de servicio de aplicaciones][ILBASE]. Si se selecciona un tipo de dirección VIP de externo puede seleccionar cuántos sistema externo de Hola de direcciones IP se crea con fines de IPSSL. Si selecciona interno debe subdominio de hello toospecify que va a utilizar su ASE. Se pueden implementar los ASE en redes virtuales que usen *o bien* intervalos de direcciones públicas *o bien* espacios de direcciones de RFC1918 (es decir, direcciones privadas). En orden toouse una red virtual con un intervalo de direcciones públicas, deberá toocreate Hola red virtual antes de tiempo. Cuando se selecciona una red virtual existente debe toocreate una subred nueva durante la creación de ASE. **No puede usar una subred creada previamente en el portal de Hola. Puede crear un ASE con una subred creada previamente si crea su ASE con una plantilla de Resource Manager.** toocreate un ASE desde una plantilla use información de hello aquí, [creación de un entorno de servicio de aplicaciones desde plantilla] [ ILBAseTemplate] y, a continuación, [crear un entorno de servicio de aplicaciones de ILB de plantilla] [ASEfromTemplate].

### <a name="details"></a>Detalles
Se crea un ASE con 2 servidores front-end y 2 trabajos. Hola front-Ends actúan como extremos HTTP/HTTPS de Hola y enviar tráfico de los trabajadores de toohello que son roles de Hola que permite hospedar las aplicaciones. Puede ajustar la cantidad de hello después de la creación de ASE y puede incluso configurar reglas de escalado automático en estos grupos de recursos. Para obtener más detalles de escalado manual, administración y supervisión de un entorno de servicio de aplicaciones vaya aquí: [cómo tooconfigure un entorno de servicio de aplicaciones][ASEConfig] 

Solo Hola una ASE puede existir en subred hello usa Hola ASE. subred de Hello no se puede usar para algo distinto de hello ASE

### <a name="after-app-service-environment-v1-creation"></a>Después de la creación de una instancia de App Service Environment v1
Después de la creación de ASE puede ajustar:

* La cantidad de servidores front-end (mínimo: 2)
* La cantidad de trabajos (mínimo: 2)
* Cantidad de direcciones IP disponibles para SSL de IP
* Los tamaños de recursos utilizados por hello roles de trabajo o servidores front-end de proceso (el tamaño mínimo de Front-End es P2)

Existen más detalles alrededor de ajuste de escala, administración y supervisión de los entornos del servicio de aplicación aquí manual: [cómo tooconfigure un entorno de servicio de aplicaciones][ASEConfig] 

Para obtener información sobre el escalado automático no hay una guía aquí: [cómo tooconfigure Autoescala para un entorno de servicio de aplicaciones][ASEAutoscale]

Existen dependencias adicionales que no están disponibles para la personalización, como la base de datos de Hola y almacenamiento. Éstas son controlando de Azure y se incluyen con el sistema de Hola. es compatible con el almacenamiento de sistema de Hello too500 GB para Hola todo entorno de servicio de aplicación y base de datos de Hola se ajusta por Azure según sea necesario mediante la escala de hello del sistema de Hola.

## <a name="getting-started"></a>Introducción
Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

tooget partió v1 de entorno del servicio de aplicaciones, consulte [Introducción toohello v1 de entorno del servicio de aplicaciones][WhatisASE]

Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
