---
title: aaaHow tooConfigure v1 de un entorno de servicio de aplicaciones
description: "Configuración, administración y supervisión de hello v1 de entorno del servicio de aplicaciones"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: b5a1da49-4cab-460d-b5d2-edd086ec32f4
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: f9539a72517276d8a1e340a408841561e8b8f56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-an-app-service-environment-v1"></a>Configuración de una instancia de App Service Environment v1

> [!NOTE]
> Este artículo trata sobre Hola v1 de entorno del servicio de aplicaciones.  Hay una versión más reciente de hello entorno del servicio de aplicación que es más fácil toouse y se ejecuta en una infraestructura más eficaz. toolearn más información acerca de la nueva versión de hello iniciar con hello [toohello Introducción entono](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Información general
A grandes rasgos, un entorno de Azure App Service Environment consta de varios componentes principales:

* Recursos de proceso que se ejecutan en el entorno del servicio de aplicación Hola servicio hospedado
* Storage
* Una base de datos
* Una Red virtual de Azure (VNet) implementada según el modelo clásico (V1) o según el modelo de Resource Manager (V2) 
* Una subred con el servicio de entorno del servicio de aplicaciones hospedadas de hello en ella se está ejecutando

### <a name="compute-resources"></a>Recursos de proceso
Usar recursos de proceso de hello los cuatro grupos de recursos.  Cada entorno del Servicio de aplicaciones (ASE) tiene un conjunto de servidores front-end y tres posibles grupos de trabajo. No es necesario toouse todos los grupos de trabajo tres--si lo desea, puede utilizar uno o dos.

hosts de Hello en grupos de recursos de hello (front-end y los trabajadores) no son directamente accesibles tootenants. No se puede usar el protocolo de escritorio remoto (RDP) tooconnect toothem, cambiar su aprovisionamiento o actuar como un administrador en ellos.

Puede establecer el tamaño y la cantidad de grupos de recursos. En un ASE tiene cuatro opciones de tamaño cuyos nombres van de P1 a P4. Para obtener detalles sobre los tamaños y sus precios, consulte [Precios de Servicio de aplicaciones](../app-service/app-service-value-prop-what-is.md).
Cambiar la cantidad de Hola o tamaño se llama a una operación de escala.  Solo puede haber una operación de escalado en curso en un momento determinado.

**Front-end**: servidores front-end de hello es puntos de conexión de hello HTTP/HTTPS para las aplicaciones que se mantienen en su ASE. No ejecutar cargas de trabajo en hello servidores front-end.

* Un ASE comienza con dos P2, lo cual es suficiente para cargas de trabajo de desarrollo y pruebas y cargas de trabajo de producción de bajo nivel. Se recomienda encarecidamente P3s para tooheavy moderado las cargas de trabajo de producción.
* Tooheavy moderado cargas de trabajo de producción, se recomienda que haya al menos cuatro tooensure P3s hay suficiente servidores front-end que se ejecuta cuando se produce un mantenimiento programado. Las actividades de mantenimiento programado desactivan un front-end cada vez. Esto reduce la capacidad global de los servidores front-end disponibles durante las actividades de mantenimiento.
* Servidores front-end puede tardar hasta tooan hora tooprovision. 
* Para optimizar las más escala, debe supervisar el porcentaje de CPU de hello, porcentaje de memoria y las métricas de solicitudes activas de grupo de servidores front-end de Hola. Si los porcentajes de CPU o memoria de hello están por encima del 70 por ciento cuando se ejecuta P3s, agregar más servidores front-end. Si el valor de solicitudes activas de hello calcula el promedio too15, too20 000, 000 solicitudes por front-end, también debe agregar más servidores front-end. Hola objetivo global es tookeep CPU y uso de memoria por debajo de 70% y calcular el promedio de espera toobelow 15.000 solicitudes por front-end si estás ejecutando P3s de solicitudes activas.  

**Los trabajadores**: los trabajos de hello son donde las aplicaciones se ejecutan realmente. Al escalar una planes de servicio de aplicación, que utiliza los trabajadores de hello asociado el grupo de trabajo.

* No es posible agregar trabajo de manera instantánea. Puede ocupar tooan hora tooprovision.
* Ajuste de escala de tamaño de Hola de un recurso de proceso para cualquier grupo tardará < 1 hora por cada dominio de actualización. Hay 20 dominios de actualización en un ASE. Si aplica una escala de tamaño de proceso de Hola de un grupo de trabajo con 10 instancias, pueden tardar too10 horas toocomplete.
* Si cambia el tamaño de Hola Hola de recursos de proceso que se utilizan en un grupo de trabajo, hará que los arranques en frío de hello las aplicaciones que se ejecutan en ese grupo de trabajo.

Hola toochange Calcular tamaño de recurso de un grupo de trabajo que no se está ejecutando ninguna aplicación de forma más rápida de Hello es:

* Reducir la cantidad de Hola de trabajadores too2.  escala mínima de Hello hacia abajo de tamaño en el portal de hello es 2. Tardará unos toodeallocate minutos las instancias. 
* Tamaño y número de instancias de proceso seleccione Hola de nuevo. Desde aquí, tardará too2 horas toocomplete.

Si las aplicaciones requieren un tamaño mayor de recursos de proceso, no podrá aprovechar las instrucciones anteriores Hola. En lugar de cambiar el tamaño de Hola de grupo de trabajo de Hola que hospeda las aplicaciones, puede rellenar otro grupo de trabajo con los trabajadores del tamaño deseado de Hola y mover las aplicaciones a través del grupo de toothat.

* Crear instancias adicionales de Hola de hello necesario calcular tamaño en otro grupo de trabajo. Esto le llevará una tooan toocomplete de hora.
* Volver a asignar los planes de servicio de aplicaciones que hospedan aplicaciones de Hola que necesitan un grupo de trabajo de mayor tamaño toohello recién configurado. Se trata de una operación rápida que debería tardar menos de un minuto toocomplete.  
* Reducir el primer grupo de trabajo Hola si ya no necesita esas instancias no utilizadas. Esta operación tarda unos toocomplete minutos.

**Escalado automático**: una de las herramientas de Hola que le permitirá toomanage su consumo de recursos de proceso es escalado automático. Este se puede aplicar a grupos de trabajo o servidores front-end. Puede realizar acciones como aumentar las instancias de cualquier tipo de grupo de mañana hello y reducir por noche Hola. O quizás que agregue instancias al número de Hola de trabajadores que están disponibles en un grupo de trabajo cae por debajo de un umbral determinado.

Se requiere si desea que las reglas de escalado automático de tooset alrededor de métricas de grupo de recursos de proceso, tenga en tiempo de presentación de la cuenta que el aprovisionamiento. Para obtener más información acerca de la escala automática entornos del servicio de aplicación, consulte [cómo escalado automático tooconfigure en un entorno de servicio de aplicaciones][ASEAutoscale].

### <a name="storage"></a>Storage
Cada ASE se configura con 500 GB de almacenamiento. Este espacio se utiliza en todas las aplicaciones de Hola Hola ASE. Este espacio de almacenamiento es una parte del programa Hola ASE y no puede estar desactivado toouse el espacio de almacenamiento. Si está realizando el enrutamiento de red virtual de ajustes tooyour o seguridad, necesita toostill permitir acceso tooAzure almacenamiento--u Hola ASE no puede funcionar.

### <a name="database"></a>Base de datos
base de datos de Hello contiene información de Hola que define el entorno de hello, así como detalles de hello acerca de las aplicaciones de Hola que se ejecutan dentro de él. Demasiado, esto es una parte de hello suscripción mantenidos en Azure. No es algo que tiene una capacidad directa toomanipulate. Si está realizando el enrutamiento de red virtual de ajustes tooyour o seguridad, necesita toostill permitir acceso tooSQL Azure--u Hola ASE no puede funcionar.

### <a name="network"></a>Red
Hola red virtual que se utiliza con su ASE puede ser uno de los que realizó cuando creaste Hola ASE o uno que haya realizado antes de tiempo. Cuando se crea la subred de Hola durante la creación de ASE, fuerza toobe Hola ASE Hola mismo grupo de recursos como la red virtual de Hola. Si necesita Hola grupo de recursos utilizado por la toobe ASE diferente de la red virtual, deberá toocreate su ASE utilizando una plantilla de administrador de recursos.

Hay algunas restricciones en la red virtual de Hola que se usa para un ASE:

* red virtual de Hello debe ser una red virtual regional.
* Es necesario toobe una subred con 8 o más direcciones donde se implementa ASE Hola.
* Después de una subred es toohost usado un ASE, intervalo de direcciones de Hola de subred de hello no se puede cambiar. Por este motivo, se recomienda que dicha subred hello contiene al menos 64 direcciones tooaccommodate crecimiento futuro ASE.
* Puede haber nada en la subred de hello pero ASE Hola.

A diferencia de servicio de hello hospedado que contiene ASE hello, Hola [red virtual] [ virtualnetwork] y subred están bajo control de usuario.  Puede administrar la red virtual a través de la interfaz de usuario de red Virtual de Hola o PowerShell.  Un ASE se puede implementar en una red virtual según el modelo clásico o según el modelo de Resource Manager.  portal de Hola y experiencias de API son ligeramente diferentes entre clásico y el Administrador de recursos VNets pero se Hola Hola experiencia ASE igual.

Hola red virtual que es usado toohost un ASE puede usar cualquier direcciones IP RFC1918 privadas o puede usar direcciones IP públicas.  Si desea toouse un intervalo IP que no está cubierto por RFC1918 (10.0.0.0/8, 172.16.0.0/12 y 192.168.0.0/16) debe toocreate su toobe de red virtual y subred utilizada por su ASE por delante de la creación de ASE.

Dado que esta capacidad coloca Hola servicio de aplicaciones de Azure en la red virtual, significa que las aplicaciones que se hospedan en su ASE ahora pueden tener acceso a recursos que están disponibles a través de ExpressRoute o redes privadas virtuales (VPN) de sitio a sitio directamente. aplicaciones de Hola que están dentro de su entorno de servicio de aplicaciones no requieren adicionales red características tooaccess recursos disponibles toohello red virtual que hospeda el entorno de servicio de aplicaciones. Esto significa que no es necesario tooresources de tooget de toouse la integración de red virtual o las conexiones híbridas en o red virtual tooyour conectado. Todavía puede usar tanto de esas características aunque tooaccess recursos en redes que no están conectados tooyour de red virtual.

Por ejemplo, puede utilizar toointegrate de integración de la red virtual con una red virtual que está en su suscripción, pero no está conectado toohello red virtual que se encuentra su ASE en. Todavía también puede usar recursos de tooaccess de conexiones híbridas que se encuentran en otras redes, exactamente igual que normalmente.  

Si tiene la red virtual configurada con una VPN de ExpressRoute, debe tener en cuenta algunas de sus necesidades de enrutamiento de hello tiene un ASE. Existen algunas configuraciones de rutas definidas por el usuario (UDR) que son incompatibles con un ASE. Para información detallada respecto a la ejecución de un ASE en una red virtual con ExpressRoute, consulte el artículo sobre la [ejecución de un entorno de App Service en una red virtual con ExpressRoute][ExpressRoute].

#### <a name="securing-inbound-traffic"></a>Protección del tráfico de entrada
Hay dos toocontrol métodos principales ASE tooyour de tráfico de entrada.  Puede usar toocontrol Groups(NSGs) de seguridad de red qué IP direcciones pueden tener acceso a su ASE como se describe aquí [cómo el tráfico en un entorno de servicio de aplicaciones de la entrada de toocontrol](app-service-app-service-environment-control-inbound-traffic.md) y también puede configurar su ASE con una carga interno Balancer(ILB).  Estas características también pueden utilizarse conjuntamente si desea tener acceso de toorestrict con NSG tooyour ASE de ILB.

Cuando se crea un ASE, este creará a una dirección VIP de la red virtual.  Hay dos tipos de direcciones VIP, internas y externas.  Cuando se crea un ASE con una dirección VIP externa, se podrá acceder a las aplicaciones del ASE a través de una dirección IP enrutable de Internet. Si selecciona una dirección VIP interna, el ASE se configurara con un ILB y no podrá acceder directamente a ella a través de Internet.  Un ASE del ILB seguirá necesitando una dirección VIP externa pero solo se utilizará para la administración de Azure y el acceso de mantenimiento.  

Durante la creación de ILB ASE proporcionan subdominio hello usa hello ILB ASE y tendrá toomanage su propio DNS para el subdominio de Hola que especifique.  Porque establecer nombre de subdominio Hola debe certificado de hello toomanage usado para el acceso HTTPS.  Después de ASE creación que está pide certificado de hello tooprovide.  lee toolearn más información acerca de crear y usar una ASE de ILB [mediante un equilibrador de carga interno con un entorno de servicio de aplicaciones][ILBASE]. 

## <a name="portal"></a>Portal
Puede administrar y supervisar el entorno de servicio de aplicaciones mediante el uso de hello UI Hola portal de Azure. Si tienes un ASE, son probablemente toosee Hola símbolos de servicio de aplicaciones en la barra lateral. Este símbolo es toorepresent usado entornos del servicio de aplicación Hola portal de Azure:

![Símbolo del entorno del Servicio de aplicaciones][1]

tooopen Hola de interfaz de usuario que se muestra todos los entornos de servicio de aplicación, puede usar Hola icono o en el botón de contenido adicional de hello seleccione (">" símbolos) final Hola de hello sidebar tooselect entornos del servicio de aplicación. Al seleccionar uno de los ASEs Hola enumerados, abra Hola interfaz de usuario utilizado toomonitor y administrarlo.

![Interfaz de usuario para supervisar y administrar el entorno del Servicio de aplicaciones][2]

La primera hoja muestra algunas de las propiedades del ASE junto con un gráfico de métrica por grupo de recursos. Algunas de las propiedades de Hola que aparecen en hello **Essentials** bloque también son hipervínculos que se abrirán una hoja de Hola que está asociado a él. Por ejemplo, puede seleccionar hello **red Virtual** tooopen de nombre una interfaz de usuario de hello asociados con la red virtual de Hola que su ASE se ejecuta en. Los **planes de App Service** y las **aplicaciones** abren hojas que muestran los elementos que se encuentran en el ASE.  

### <a name="monitoring"></a>Supervisión
gráficos de Hello permiten toosee una variedad de estadísticas de rendimiento de cada grupo de recursos. Para el grupo de servidores front-end de hello, puede supervisar Hola promedio de CPU y memoria. Para los grupos de trabajo, puede supervisar cantidad Hola que se usa y la cantidad de Hola que está disponible.

Use varios servicios de aplicación pueden hacer planes de los trabajadores de hello en un grupo de trabajo. carga de trabajo de Hello no se distribuye en Hola de igual forma al igual que con los servidores front-end de hello, por lo que el uso de CPU y memoria de hello no proporcionan la mayor parte de manera Hola de información útil. Es más importante tootrack cuántos trabajos que ha usado y están disponibles, especialmente si está administrando este sistema para que otros usuarios toouse.  

También puede utilizar todas las métricas de Hola que pueden realizar el seguimiento en hello gráficos tooset las alertas. Cómo configurar alertas aquí Hola funciona igual como en otros lugares en el servicio de aplicaciones. Puede establecer una alerta de cualquier hello **alertas** UI parte o de obtención de detalles de todas las métricas de interfaz de usuario y seleccione **Agregar alerta**.

![Interfaz de usuario de métricas][3]

métricas de Hola que acabamos de describir son métricas de entorno del servicio de aplicaciones de Hola. También hay métricas que están disponibles en el nivel del plan de servicio de aplicaciones de Hola. Aquí es dónde la supervisión de la CPU y de la memoria tiene más sentido.

En un ASE todas Hola que planes de servicio de aplicaciones son planes de servicio de aplicaciones dedicados. Esto significa que Hola únicas aplicaciones que se ejecutan en hosts asignados de hello toothat plan de servicio de aplicaciones son aplicaciones de hello en ese plan de servicio de aplicaciones. detalles de toosee en su plan de servicio de aplicaciones, abrirá el plan de servicio de aplicaciones desde cualquiera de las listas de Hola Hola ASE interfaz de usuario o de **planes de servicio de aplicaciones de examinar** (que enumeran todas ellas).   

### <a name="settings"></a>Settings
En la hoja de hello ASE, hay un **configuración** sección que contiene varias funciones importantes:

**Configuración de** > **propiedades**: Hola **configuración** hoja se abre automáticamente cuando se activa la hoja de ASE. En hello superior es **propiedades**. Hay una serie de elementos aquí toowhat redundante que se ven en **Essentials**, pero lo que resulta muy útil es **dirección IP Virtual**, así como **direcciones IP saliente**.

![Hoja de configuración y propiedades][4]

**Settings** > **Direcciones IP**: Al crear una aplicación de capa de sockets seguros (SSL) de IP en el ASE, necesita una dirección SSL de IP. En orden tooobtain uno, su ASE tiene direcciones IP SSL que posee y que se pueden asignar. Cuando se crea un ASE, este tiene una dirección SSL de IP para este propósito, pero puede agregar más. Hay un cargo de dirección SSL de IP adicionales, como se muestra en [de precios de servicio de aplicaciones] [ AppServicePricing] (en la sección de hello en las conexiones SSL). precio adicional Hello es hello precio de IP SSL.

**Configuración de** > **el grupo de servidores de Front-End** / **los grupos de trabajo**: cada uno de estos módulos de grupo de recursos ofrece información de toosee de capacidad de hello solo en ese grupo de recursos , además tooproviding controla la escala de toofully ese grupo de recursos.  

hoja de base de Hola para cada grupo de recursos proporciona un gráfico con métricas para ese grupo de recursos. Al igual que con gráficos de Hola de hoja de ASE hello, puede entrar en el gráfico de Hola y configurar alertas según sea necesario. Establecer una alerta de hoja de ASE de Hola para un grupo de recursos específico Hola lo mismo que hacerlo desde el grupo de recursos de Hola. Desde el grupo de trabajo de hello **configuración** hoja, tiene hello tooall de acceso a aplicaciones o planes de servicio de aplicaciones que se ejecutan en este grupo de trabajo.

![Interfaz de usuario de configuración de grupo de trabajo][5]

### <a name="portal-scale-capabilities"></a>Funcionalidad de escalado del portal
Hay tres operaciones de escala:

* Cambiar el número de Hola de direcciones IP en hello ASE que están disponibles para el uso de SSL de IP.
* Cambiar tamaño de Hola Hola de recurso de proceso que se utiliza en un grupo de recursos.
* Cambiar el número de Hola de recursos de proceso que se utilizan en un grupo de recursos, ya sea manualmente o a través de escalado automático.

En el portal de hello, hay tres toocontrol formas cuántos servidores que tienen en los grupos de recursos:

* Una operación de escala de hoja de ASE principal hello en la parte superior de Hola. Puede realizar varias escala toohello front-end y los grupos de trabajo de los cambios de configuración. Todas se aplican como una única operación.
* Una operación de escala manual de grupo de recursos individuales de hello **escala** hoja, que se encuentra en **configuración**.
* Escala automática, que se configura desde el grupo de recursos individuales de hello **escala** hoja.

operación de escalado de hello toouse de hoja de ASE hello, arrastre quantity de toohello de control deslizante de Hola que desea y guarda. Esta interfaz de usuario también admite cambiar tamaño de Hola.  

![Interfaz de usuario de escalado][6]

capacidades de manual o de escalado automático de Hola de toouse en un grupo de recursos específico, vaya demasiado**configuración** > **el grupo de servidores de Front-End** / **los grupos de trabajo** como adecuados. A continuación, se abrirán grupo Hola que desea toochange. Vaya demasiado**configuración** > **horizontalmente** o **configuración** > **escalar vertical**. Hola **horizontalmente** hoja permite toocontrol cantidad de instancia. **Escalar vertical** permite toocontrol tamaño del recurso.  

![Interfaz de usuario de configuración de escalado][7]

## <a name="fault-tolerance-considerations"></a>Consideraciones de tolerancia a errores
Puede configurar un toouse entono too55 recursos de proceso total. Esos 55 recursos de proceso, 50 solo puede ser toohost usa las cargas de trabajo. motivo Hello es doble. Hay un mínimo de 2 recursos de proceso front-end.  Esto deja una asignación de grupo de trabajo de too53 toosupport Hola. Tolerancia a errores tooprovide orden, necesita toohave un recurso de proceso adicional que se asigna según toohello siguientes reglas:

* Cada grupo de trabajo necesita al menos 1 recurso de proceso adicional que no está disponible toobe asigna una carga de trabajo.
* Cuando la cantidad de Hola de recursos de proceso en un grupo de trabajo está por encima de un determinado valor, otro recurso de proceso es necesario para la tolerancia a errores. No es el caso de hello en el grupo de servidores front-end de Hola.

Dentro de cualquier grupo de trabajo único, los requisitos de tolerancia a errores de hello son que para un determinado valor de X recursos asignados tooa grupo de trabajo:

* Si X es entre 2 y 20, cantidad de hello utilizable de recursos de proceso que puede usar para cargas de trabajo es x-1.
* Si X es entre 21 y 40, cantidad de hello utilizable de recursos de proceso que puede usar para cargas de trabajo es X-2.
* Si X es entre 41 y 53, cantidad de hello utilizable de recursos de proceso que puede usar para cargas de trabajo es X-3.

superficie mínima de Hello tiene 2 servidores front-end y 2 trabajos.  Con hello por encima de las instrucciones a continuación, presentamos unos tooclarify de ejemplos:  

* Si tiene 30 trabajos en un único grupo, 28 de ellos puede ser usado toohost cargas de trabajo.
* Si tiene 2 trabajos en un único grupo, 1 puede ser usado toohost cargas de trabajo.
* Si tiene 20 trabajadores en un único grupo, 19 puede ser usado toohost cargas de trabajo.  
* Si tienes 21 trabajadores en un único grupo, sigue solo 19 pueden ser utilizados toohost cargas de trabajo.  

aspecto de la tolerancia a errores de Hello es importante, pero debe tookeep en cuenta que escala superior a determinados umbrales. Si desea que tooadd más capacidad de pasar de 20 instancias y, a continuación, vaya too22 o superior como 21 no se agrega más capacidad. Hola que mismo puede decirse de pasar por encima de 40, donde el número siguiente de Hola que agrega capacidad es 42.  

## <a name="deleting-an-app-service-environment"></a>Eliminación de un entorno del Servicio de aplicaciones
Si desea toodelete un entorno de servicio de aplicaciones, a continuación, simplemente utilice hello **eliminar** acción en la parte superior de Hola de hoja de entorno del servicio de aplicaciones de Hola. Al hacerlo, podrá nombre de hello tooenter solicitadas de su tooconfirm de entorno de servicio de aplicaciones que realmente desea toodo esto. Tenga en cuenta que cuando se elimina un entorno de servicio de aplicaciones, se eliminen todas de hello contenido también.  

![Eliminación de la interfaz de usuario de un entorno del Servicio de aplicaciones][9]  

## <a name="getting-started"></a>Introducción
tooget iniciado con el entorno de servicio de aplicación, consulte [cómo toocreate un entorno de servicio de aplicaciones](app-service-web-how-to-create-an-app-service-environment.md).

Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-configure-an-app-service-environment/ase-icon.png
[2]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-aseblade.png
[3]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolchart.png
[4]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-properties.png
[5]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolblade.png
[6]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-scalecommand.png
[7]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolscale.png
[8]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-pricingtiers.png
[9]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-deletease.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
