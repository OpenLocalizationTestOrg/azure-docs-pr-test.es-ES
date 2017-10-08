---
title: aaaUse un entorno de servicio de aplicaciones de Azure
description: "Cómo publicar toocreate y escalar aplicaciones en un entorno de servicio de aplicaciones de Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a>Uso de una instancia de App Service Environment #

## <a name="overview"></a>Información general ##

Azure App Service Environment es una implementación de Azure App Service en una subred de Azure Virtual Network de un cliente. Consta de:

- **Front-end**: servidores front-end de hello es donde finaliza HTTP/HTTPS en un entorno de servicio de aplicaciones (ASE).
- **Los trabajadores**: los trabajos de hello son recursos de Hola que permite hospedar las aplicaciones.
- **Base de datos**: base de datos de hello contiene información que define el entorno de Hola.
- **Almacenamiento**: almacenamiento de hello es toohost usado Hola publicado por el cliente aplicaciones.

> [!NOTE]
> Hay dos versiones de App Service Environment: ASEv1 y ASEv2. En ASEv1, debe administrar los recursos de hello antes de utilizarlas. toolearn cómo tooconfigure y administrar ASEv1, vea [configurar un v1 de entorno de servicio de aplicaciones][ConfigureASEv1]. Hola resto de este artículo se centra en ASEv2.
>
>

Puede implementar un entorno ASE (ASEv1 y ASEv2) con una VIP externa o interna para acceso a las aplicaciones. implementación de Hello con una VIP externa se suele denominar una ASE externo. versión interna de Hola se denomina hello ILB ASE porque utiliza un equilibrador de carga interno (ILB). vea toolearn más información acerca de hello ASE de ILB, [crear y usar una ASE de ILB][MakeILBASE].

## <a name="create-a-web-app-in-an-ase"></a>Creación de una aplicación web en ASE ##

toocreate una aplicación web en un ASE, utilice Hola mismo proceso que cuando se crea, normalmente, pero con algunas pequeñas diferencias. Al crear un nuevo plan de App Service:

- En lugar de elegir una ubicación geográfica en qué toodeploy la aplicación, debe elegir un ASE como su ubicación.
- Todos los planes de App Service que se creen en ASE deben tener un plan de tarifa aislado.

Si no tienes un ASE, puede crear una siguiendo las instrucciones de hello en [crear un entorno de servicio de aplicaciones][MakeExternalASE].

toocreate una aplicación web en un ASE:

1. Seleccione **Nuevo** > **Web y móvil** > **Aplicación web**.

2. Escriba un nombre para la aplicación web de Hola. Si ya ha seleccionado un plan de servicio de aplicaciones en un ASE, nombre de dominio de hello para la aplicación hello refleja el nombre de dominio de Hola de hello ASE.

    ![Selección del nombre de la aplicación web][1]

3. Seleccione una suscripción.

4. Escriba un nombre para un nuevo grupo de recursos, o seleccione **utilizar existente** y seleccione uno de la lista desplegable de Hola.

5. Seleccione un plan de App Service existente en ASE o cree uno nuevo siguiendo estos pasos:

    a. Seleccione **Crear nuevo**.

    b. Escriba el nombre de hello para el plan de servicio de aplicaciones.

    c. Seleccione su ASE Hola **ubicación** lista desplegable.

    d. Seleccione un plan de tarifa **Aislado**. Elija **Seleccionar**.

    e. Seleccione **Aceptar**.
    
    ![Planes de tarifa aislados][2]

6. Seleccione **Crear**.

## <a name="how-scale-works"></a>Cómo funciona escalar ##

Cada aplicación de App Service se ejecuta en un plan de App Service. modelo de contenedor de Hello es entornos contienen los planes de servicio de aplicaciones, y los planes de servicio de aplicaciones contienen aplicaciones. Al escalar una aplicación, escalar Hola plan de servicio de aplicaciones y, por tanto, ajustar todas las aplicaciones de hello en hello mismo plan.

En ASEv2, al escalar un plan de servicio de aplicaciones, infraestructura de hello necesitado se agrega automáticamente. Hay un retraso tooscale operaciones mientras se agrega la infraestructura de Hola. En ASEv1, infraestructura de hello necesitado debe agregarse antes de poder crear o escalar horizontalmente su plan de servicio de aplicaciones. 

En para varios inquilinos Hola servicio de aplicaciones, ajuste de escala es normalmente inmediata porque un grupo de recursos es toosupport disponible. En un entorno ASE, no hay ningún búfer de este tipo y los recursos se asignan según sea necesario.

En un ASE, se puede escalar too100 instancias. Todas esas 100 instancias pueden estar en un solo plan de App Service o estar distribuidos en varios planes de App Service.

## <a name="ip-addresses"></a>Direcciones IP ##

Servicio de aplicaciones tiene Hola capacidad tooallocate una aplicación de tooan de dirección IP dedicada. Esta capacidad está disponible después de configurar SSL basado en IP, como se describe en [enlazar una existente personalizado SSL certificado tooAzure aplicaciones web][ConfigureSSL]. Sin embargo, en ASE, hay una excepción importante. No se puede agregar la dirección IP adicional direcciones toobe utilizado para SSL basado en IP en un ASE de ILB.

En ASEv1, necesita direcciones IP de tooallocate hello como recursos antes de utilizarlas. En ASEv2, utilizarlos desde la aplicación tal como se hace en multiempresa Hola servicio de aplicaciones. Siempre hay una dirección de reserva en ASEv2 too30 direcciones de IP. Cada vez que usa una, se agrega otra, para que siempre haya una dirección disponible lista para su uso. Un tiempo de retraso es necesario tooallocate otra dirección IP, lo que impide que agregar IP direcciones en rápida sucesión.

## <a name="front-end-scaling"></a>Escalado de front-end ##

En ASEv2, al escalar horizontalmente los planes de servicio de aplicaciones, los trabajadores se agregan automáticamente toosupport ellos. Cada ASE se crea con dos servidores front-end. Además, servidores front-end de hello automáticamente escala horizontalmente a una velocidad de un front-end para cada 15 instancias en los planes de servicio de aplicaciones. Por ejemplo, si tiene 15 instancias, tiene tres Front-Ends. Si escalar instancias too30, a continuación, tiene cuatro front-end y así sucesivamente.

Este número de servidores front-end debe ser más que suficiente en la mayoría de los casos. Sin embargo, puede escalar horizontalmente a mayor velocidad. Puede cambiar la proporción de hello tooas baja como un front-end para cada cinco instancias. Hay una carga para cambiar la proporción de Hola. Para más información, consulte [Precios de Azure App Service][Pricing].

Recursos de front-end son extremo HTTP/HTTPS de Hola para hello ASE. Con la configuración de front-end de predeterminada hello, uso de memoria por front-end es constantemente aproximadamente 60 por ciento. Las cargas de trabajo no se ejecutan en Front-End. Hello factor clave para un front-end con sentido tooscale es CPU hello, que depende principalmente de tráfico HTTPS.

## <a name="app-access"></a>Acceso a las aplicaciones ##

En un ASE externo, el dominio de Hola que se utiliza al crear aplicaciones es diferente de multiempresa Hola servicio de aplicaciones. Incluye el nombre de Hola de hello ASE. Para obtener más información acerca de cómo toocreate un ASE externos, vea [crear un entorno de servicio de aplicaciones][MakeExternalASE]. nombre de dominio de Hello en un ASE externo aspecto *.&lt; asename&gt;. p.azurewebsites.net*. Por ejemplo, si su ASE se denomina _externo ase_ y hospedar una aplicación denominada _contoso_ en ese ASE llegan al hello las siguientes direcciones URL:

- contoso.external-ase.p.azurewebsites.net
- contoso.scm.external-ase.p.azurewebsites.net

Hola de dirección URL contoso.scm.external ase.p.azurewebsites.net es consola Kudu de tooaccess usado Hola o para la publicación de implementar la aplicación mediante el uso de web. Para obtener información sobre la consola de Kudu hello, consulte [consola Kudu para el servicio de aplicaciones de Azure][Kudu]. consola de Hello Kudu ofrece una interfaz de usuario web para depuración, cargar archivos, editar los archivos y mucho más.

En un ASE ILB, determina el dominio de Hola durante la implementación. Para obtener más información sobre cómo toocreate un ILB ASE, consulte [crear y usar una ASE de ILB][MakeILBASE]. Si especifica el nombre de dominio de hello _ilb ase.info_, Hola aplicaciones en que ASE use ese dominio durante la creación de la aplicación. Para la aplicación hello denominado _contoso_, hello las direcciones URL son:

- contoso.ilb-ase.info
- contoso.scm.ilb-ase.info

## <a name="publishing"></a>Publicación ##

Al igual que con para varios inquilinos Hola servicio de aplicaciones, en un ASE puede publicar con:

- Implementación web.
- FTP.
- Integración continua.
- Arrastrar y colocar en la consola de Kudu Hola.
- Un IDE como Visual Studio, Eclipse o IntelliJ IDEA.

Con un ASE externo, estas opciones de publicación se comportan Hola igual. Para más información, consulte [Implementación en Azure App Service][AppDeploy]. 

Hola principal diferencia con la publicación es con sentido tooan ASE de ILB. Con un ASE ILB, publicación de extremos de hello todo sólo está disponibles mediante hello ILB. Hola ILB está en una dirección IP privada en la subred de ASE hello en red virtual de Hola. Si no tiene acceso de red toohello ILB, no se puede publicar las aplicaciones de ese ASE. Como se indicó en [crear y usar una ASE de ILB][MakeILBASE], necesita tooconfigure DNS para las aplicaciones de hello en sistema Hola. Incluye el punto de conexión de hello SCM. Si no se han definido correctamente, no puede llevar a cabo la publicación. El IDE también necesita toohello de acceso de red toohave ILB en orden toopublish tooit directamente.

Sistemas de CI basados en Internet, como GitHub y Visual Studio Team Services, no funcionan con un ASE ILB porque el extremo de publicación de hello no es accesible de Internet. En su lugar, deberá toouse un sistema de elementos de configuración que utiliza un modelo de extracción, por ejemplo, Dropbox.

publicación de extremos de Hola para las aplicaciones en un ASE ILB usa dominio Hola ese Hola con que ase de ILB se creó. Puede verlo en el perfil de publicación de la aplicación hello y en la hoja de portal de la aplicación hello (en **Introducción** > **Essentials** y también en **propiedades**). 

## <a name="pricing"></a>Precios ##

Hola precios SKU llama **Isolated** se creó para su uso únicamente con ASEv2. Todos los planes de servicio de aplicaciones que se hospedan en ASEv2 están en hello Isolated precios SKU. Las tarifas del plan Isolated de App Service pueden variar por región. 

Además de planes de toohello precio para el servicio de aplicación, hay una tarifa plana ASE propio. no cambia con tamaño de Hola de su ASE Hello tarifa plana y paga por la infraestructura de hello ASE en el valor predeterminado es escalar velocidad 1 adicionales front-end para cada 15 instancias del plan de servicio de aplicaciones.  

Si la velocidad de escala predeterminada de Hola de 1 front-end para cada 15 instancias del plan de servicio de aplicaciones no es lo suficientemente rápido, puede ajustar la proporción de hello en el que se agrega servidores front-end u Hola tamaño de hello front-end.  Al ajustar la proporción de Hola o tamaño, paga por los núcleos de front-end de Hola que no se debe agregar de forma predeterminada.  

Por ejemplo, si está ajustando too10 de relación de escala de hello, se agrega un front-end para cada 10 instancias en los planes de servicio de aplicaciones. tarifa fija Hola cubre una tasa de escala de un front-end para cada 15 instancias. Con una proporción de escala de 10, pago de una cuota Hola tercer front-end que ha agregado para hello 10 instancias del plan de servicio de aplicaciones. No es necesario toopay para él cuando llegue a 15 instancias porque se agrega automáticamente.

Si Ajustar tamaño de Hola de núcleos de hello front-end too2 pero no se ajustan proporción de hello, a continuación, se paga por Hola núcleos adicionales.  Se crea un ASE con 2 front-ends, de modo que, aunque por debajo del umbral de escalado automático de hello que pagaría por 2 núcleos adicionales si aumenta el tamaño de hello too2 core front-end.

Para más información, consulte [Precios de Azure App Service][Pricing].

## <a name="delete-an-ase"></a>Eliminar un entorno ASE ##

toodelete un ASE: 

1. Use **eliminar** en parte superior de Hola de hello **entono** hoja. 

2. Escriba el nombre de Hola de su tooconfirm ASE que desea que toodelete lo. Cuando se elimina un ASE, eliminar todo el contenido de hello en él también de. 

    ![Eliminación de ASE][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
