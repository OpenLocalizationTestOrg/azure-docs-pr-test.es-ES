---
title: aaaCreating y el uso de un equilibrador de carga interno con un entorno de servicio de aplicaciones | Documentos de Microsoft
description: "Creación y uso de ASE con un ILB"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a>Uso de un equilibrador de carga interno con un entorno del Servicio de aplicaciones

> [!NOTE] 
> Este artículo trata sobre Hola v1 de entorno del servicio de aplicaciones. Hay una versión más reciente de hello entorno del servicio de aplicación que es más fácil toouse y se ejecuta en una infraestructura más eficaz. toolearn más información acerca de la nueva versión de hello iniciar con hello [toohello Introducción entono](../app-service/app-service-environment/intro.md).
>

características del entorno de servicio de aplicación (ASE) Hello es una opción de servicio Premium de servicio de aplicaciones de Azure que ofrece una funcionalidad mejorada de la configuración que no está disponible en las marcas de varios inquilinos de Hola. característica de ASE Hola básicamente implementa Hola servicio de aplicaciones de Azure en su Network(VNet) Virtual de Azure. toogain que ofrece un mayor conocimiento de las capacidades de Hola por entornos del servicio de aplicación lee hello [¿qué es un entorno de servicio de aplicaciones] [ WhatisASE] documentación. Si no sabe ventajas de Hola de operar en una red virtual leen hello [P+F de red Virtual de Azure][virtualnetwork]. 

## <a name="overview"></a>Información general
Un ASE puede implementarse con un punto de conexión accesible por Internet o con una dirección IP en la red virtual. En orden tooset Hola IP direcciones tooa dirección de red virtual debe toodeploy su ASE con un Balancer(ILB) de carga interno. Cuando el ASE se configura con un ILB, tiene que proporcionar lo siguiente:

* Su propio dominio o subdominio. toomake más sencilla, en este documento se da por supuesto subdominio pero puede configurarlo en ambos casos. 
* certificado de Hola que se usa para HTTPS
* La administración de DNS del subdominio. 

A cambio, podrá realizar todo esto:

* las aplicaciones de intranet de host, como línea de aplicaciones empresariales, forma segura en hello en la nube que acceden a través de un sitio tooSite o ExpressRoute VPN
* aplicaciones de host en la nube de Hola que no aparecen en los servidores DNS públicos
* Crear aplicaciones de back-end sin conexión a Internet con las que puedan integrarse de forma segura sus aplicaciones de front-end.

#### <a name="disabled-functionality"></a>Funcionalidad deshabilitada
Sin embargo, cuando utilice un ASE con un ILB, no podrá realizar algunas operaciones; estas son algunas de ellas:

* Utilizar una SSL de IP.
* asignar direcciones IP toospecific aplicaciones
* adquisición y el uso de un certificado con una aplicación a través del portal de Hola. Por supuesto todavía puede obtener certificados directamente con una entidad de certificación y usar con las aplicaciones, pero no a través de hello portal de Azure.

## <a name="creating-an-ilb-ase"></a>Creación de un ASE con un ILB
Apenas hay diferencias entre crear un ASE con un ILB y del modo habitual. Para obtener una explicación más detallada acerca de cómo crear un ASE leer [cómo tooCreate un entorno de servicio de aplicaciones][HowtoCreateASE]. Hola toocreate de proceso es un ASE ILB Hola igual entre crear una red virtual durante la creación de ASE o para seleccionar una red virtual existente. toocreate una ASE de ILB: 

1. Hola seleccione portal Azure **nuevo -> Web + Mobile -> entorno del servicio de aplicaciones**
2. Seleccione su suscripción.
3. Elija un grupo de recursos o cree uno.
4. Cree una red virtual o seleccione una.
5. Crear una subred si se selecciona una VNet
6. Seleccione **Virtual/ubicación de red-> configuración de redes virtuales** conjunto hello tooInternal tipo VIP y
7. Proporcione el nombre de subdominio (se trata de subdominio Hola utilizado para las aplicaciones creadas en esta ASE)
8. Seleccione Aceptar y, después, Crear.

![][1]

En la hoja de la red Virtual de Hola hay una opción de configuración de redes virtuales. Aquí podrá seleccionar una dirección VIP externa o interna. valor predeterminado de Hello es externo. Si se ha configurado tooExternal su ASE usará a una VIP accesible de internet. Si selecciona Interna, el ASE se configurará con un ILB en una dirección IP de su red virtual. 

Después de seleccionar interno, Hola tooadd capacidad más direcciones IP tooyour que ase se quita y en su lugar deberá subdominio de hello tooprovide de hello ASE. En un ASE con un hello VIP externa nombre de hello ASE se utiliza en subdominio Hola para las aplicaciones creadas en esa ASE. Si se llamara a su ASE ***contosotest*** y se llamó a la aplicación en ese ASE ***MiPrueba*** , el subdominio Hola será del formato de hello ***contosotest.p.azurewebsites.net*** y Hello dirección URL para esa aplicación sería ***mytest.contosotest.p.azurewebsites.net***. Si establece Hola VIP tipo tooInternal, el nombre de ASE no se usa en el subdominio de Hola para hello ASE. Especifique el subdominio de hello explícitamente. Si era el subdominio ***contoso.corp.net*** y realiza una aplicación en que ASE denominado ***timereporting*** Hola, a continuación, la dirección URL para que la aplicación sería ***timereporting.contoso.corp.net***.

## <a name="apps-in-an-ilb-ase"></a>Aplicaciones en un ASE con un ILB
Crear una aplicación en un ASE de ILB se Hola igual que crear una aplicación en un ASE normalmente. 

1. Hola seleccione portal Azure **nuevo -> Web + Mobile -> Web** o **Mobile** o **API App**
2. Escriba el nombre de la aplicación.
3. Seleccione la suscripción.
4. Elija un grupo de recursos o cree uno.
5. Seleccione o cree un plan del Servicio de aplicaciones (ASP). Si crea un nuevo archivo ASP, a continuación, seleccione su ASE como ubicación de Hola y el grupo de trabajo de hello seleccione desea su toobe ASP creado en. Cuando creas Hola ASP seleccione su ASE como ubicación de Hola y el grupo de trabajo de Hola. Cuando se especifica nombre Hola de aplicación hello en que verá ese subdominio hello el nombre de la aplicación se reemplazó por subdominio Hola para su ASE. 
6. Seleccione Crear. Debe seleccionar hello **toodashboard Pin** casilla de verificación si desea tooshow de aplicación hello en el panel. 

![][2]

En la aplicación hello de nombre de subdominio Hola obtiene subdominio de hello tooreflect actualizada de su ASE. 

## <a name="post-ilb-ase-creation-validation"></a>Validación posterior a la creación del ASE con un ILB
Una ASE de ILB es ligeramente diferente que hello no - ILB ASE. Como ya se indicó necesitan toomanage su propio DNS y también tienen tooprovide su propio certificado para las conexiones HTTPS. 

Después de crear su ASE observará ese subdominio hello muestra subdominio de Hola que especificó y no hay un nuevo elemento en hello **configuración** menú denominado **ILB certificado**. Hola ASE se crea con un certificado autofirmado que resulta más fácil tootest HTTPS. Hello portal le indicará que debe tooprovide su propio certificado para HTTPS pero se trata de toodrive toohave un certificado que va con el subdominio. 

![][3]

Si simplemente está tratando de cosas y no sabe cómo toocreate un certificado, puede utilizar MMC de IIS de Hola toocreate de aplicación de consola a sí mismo certificado autofirmado. Una vez que se crea puede exportarlo como un archivo .pfx y, a continuación, cargarlo en hello ILB IU del certificado. Cuando no es seguro debido certificado de toohello incapacidad toovalidate Hola acceso a un sitio protegido con un certificado autofirmado, el explorador le proporcionará una advertencia que Hola sitio que tiene acceso. Si desea tooavoid dicha advertencia que necesita un certificado debidamente firmado que coincide con el subdominio y tiene una cadena de confianza que es reconocido por el explorador.

![][6]

Si desea tootry Hola flujo con sus propios certificados y probar ASE de tooyour acceso HTTP y HTTPS:

1. Vaya tooASE interfaz de usuario después de crea ASE **ASE -> Configuración -> certificados de ILB**
2. Establezca el certificado de ILB seleccionando el archivo de certificado .pfx y proporcione la contraseña. Este paso tarda un poco al tooprocess y se mostrará el mensaje de Hola que está en curso una operación de escalado.
3. Obtener la dirección ILB de Hola para su ASE (**ASE -> Propiedades -> dirección IP Virtual**)
4. Genere una aplicación web en ASE cuando lo haya creado. 
5. Crear una máquina virtual si no dispone de uno en esa red virtual (no en Hola misma subred que Hola ASE o interrupción de cosas)
6. Establezca el DNS del subdominio. Puede usar un carácter comodín con el subdominio en su DNS o si desea toodo algunas pruebas sencillas, editar el archivo de hosts de hello en la dirección IP virtual tooset web app nombre tooVIP. Si su ASE tenía el nombre de subdominio Hola. ilbase.com y se realizan Hola mytestapp de aplicación web de forma que se puede solucionar en mytestapp.ilbase.com después que establecer en el archivo de hosts. (En Windows hello hosts archivo está en C:\Windows\System32\drivers\etc\)
7. Utilizar un explorador en esa máquina virtual e ir toohttp://mytestapp.ilbase.com (o lo que el nombre de la aplicación web con el subdominio)
8. Usar un explorador en esa máquina virtual y seguir toohttps://mytestapp.ilbase.com tendrá falta de hello tooaccept de seguridad si utiliza un certificado autofirmado. 

dirección IP de Hello para el ILB aparece en las propiedades como Hola dirección IP Virtual

![][4]

## <a name="using-an-ilb-ase"></a>Uso de un ASE con un ILB
#### <a name="network-security-groups"></a>Grupos de seguridad de red
Una aislamiento de red de ASE de ILB habilita para las aplicaciones como aplicaciones de hello no son accesibles o incluso conocidos por Hola internet. Esta posibilidad es perfecta para hospedar sitios de intranet como aplicaciones de línea de negocio. Cuando necesite acceso toorestrict incluso más aún sirve Groups(NSGs) de seguridad de red toocontrol acceso Hola a nivel de red. 

Si desea toouse NSG toofurther restringir el acceso, a continuación, necesita toomake seguro que no interrumpir la comunicación de Hola necesita ese ASE hello en orden toooperate. Incluso aunque Hola acceso HTTP/HTTPS solamente a través de Hola ILB utiliza Hola Hola ASE que ase todavía depende del recurso fuera de hello red virtual. toosee es el acceso a la red siguen siendo necesarias vistazo información de hello en el documento de hello en [tooan de controlar el tráfico entrante entono] [ ControlInbound] y documento de hello en [red Detalles de configuración para los entornos del servicio de aplicación con ExpressRoute][ExpressRoute]. 

tooconfigure sus NSG necesita tooknow Hola IP dirección que usa Azure toomanage su ASE. Esa dirección IP también es dirección IP saliente Hola desde su ASE si realiza las solicitudes de internet. dirección IP saliente de Hola para su ASE permanecerá estático para la vida de su ASE Hola. Si elimina y vuelve a crear el ASE, recibirá una nueva dirección IP. toofind esta dirección IP vaya demasiado**configuración -> propiedades** y buscar hello **dirección IP saliente**. 

![][5]

#### <a name="general-ilb-ase-management"></a>Administración general de ASE con un ILB
Administrar un ASE de ILB es en gran medida Hola igual que administrar un ASE normalmente. Necesita tooscale su toohost de grupos de trabajo más instancias ASP y escalar sus cantidades de toohandle aumentado de servidores Front-End de tráfico HTTP/HTTPS. Para obtener información general sobre la administración de configuración de Hola de un ASE, lea el documento de hello en [configurar un entorno de servicio de aplicaciones][ASEConfig]. 

los elementos de administración adicional de Hello son la administración de certificados y la administración de DNS. Es necesario tooobtain y cargar el certificado de hello usa para HTTPS después de la creación de ILB ASE y reemplazarla antes de que expire. Debido a que Azure posee el dominio base Hola podemos proporcionar certificados para ASEs con una VIP externa. Puesto que subdominio Hola utilizado por una ASE de ILB puede ser cualquier cosa, necesitará tooprovide su propio certificado para HTTPS. 

#### <a name="dns-configuration"></a>Configuración de DNS
Cuando se usa un Hola VIP externa que DNS está administrado por Azure. Cualquier aplicación creada en su ASE se agrega automáticamente tooAzure DNS que es un DNS público. En un ASE ILB tiene toomanage su propio DNS. Para un subdominio determinado como contoso.corp.net necesita toocreate para que registros de DNS A esa dirección de punto tooyour ILB:

    * 
    *.scm ftp publish 


## <a name="getting-started"></a>Introducción
Todos los artículos y cómo-para para entornos del servicio de aplicación están disponibles en hello [archivo Léame para entornos de aplicaciones de servicio](../app-service/app-service-app-service-environments-readme.md).

tooget iniciado con el entorno de servicio de aplicación, consulte [Introducción tooApp entornos del servicio][WhatisASE]

Para obtener más información acerca de la plataforma de servicio de aplicaciones de Azure de hello, consulte [servicio de aplicaciones de Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
