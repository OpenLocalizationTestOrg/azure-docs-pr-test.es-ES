---
title: "aaaCreate un entorno de servicio de aplicación de Azure externo"
description: "Explica cómo toocreate un entorno de servicio de aplicaciones mientras se crea una aplicación o independiente"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: f8619534ddd889ea65063733ac6ec11b206e799c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-external-app-service-environment"></a>Creación de una instancia externa de App Service Environment #

Azure App Service Environment es una implementación de Azure App Service en una subred de Azure Virtual Network (VNet). Hay dos toodeploy de formas en un entorno de servicio de aplicaciones (ASE):

- Con una dirección VIP en una dirección IP externa, a la que se suele hacer referencia como instancia externa de ASE.
- Con hello VIP en una dirección IP interna, suele denominar una ASE de ILB porque el extremo interno de hello es un equilibrador de carga interno (ILB).

Este artículo muestra cómo toocreate una ASE externo. Para obtener información general de hello ASE, consulte [un entorno de servicio de aplicaciones de introducción toohello][Intro]. Para obtener información sobre cómo toocreate un ILB ASE, consulte [crear y usar una ASE de ILB][MakeILBASE].

## <a name="before-you-create-your-ase"></a>Antes de crear su ASE ##

Después de crear su ASE, no se puede cambiar siguiente hello:

- Ubicación
- La suscripción
- Grupos de recursos
- Red virtual usada
- La subred usada
- Tamaño de la subred

> [!NOTE]
> Cuando elige una red virtual y especifique una subred, asegúrese de que es lo suficientemente grande como tooaccommodate crecimiento futuro. Se recomienda un tamaño de `/25` con ciento veintiocho direcciones.
>

## <a name="three-ways-toocreate-an-ase"></a>Tres formas toocreate un ASE ##

Hay tres formas toocreate un ASE:

- **Al crear un plan de App Service**. Este método crea Hola ASE y Hola plan de servicio de aplicaciones en un solo paso.
- **Como una acción independiente**. Este método crea una instancia de ASE independiente, es decir, que no contiene nada. Este método es un toocreate de proceso más avanzado un ASE. Se usa un ASE toocreate con un ILB.
- **A partir de una plantilla de Azure Resource Manager**. Este método es para usuarios avanzados. Para más información, vea [Creación de una instancia de ASE a partir de una plantilla][MakeASEfromTemplate].

Un ASE externo tiene una VIP pública, lo que significa que todas las aplicaciones de toohello de tráfico HTTP/HTTPS en hello ASE llega a una dirección IP accesible desde internet. Un ASE con un ILB tiene una dirección IP de subred de hello usa Hola ASE. Hello aplicaciones hospedadas en un ASE ILB no se exponen directamente toohello internet.

## <a name="create-an-ase-and-an-app-service-plan-together"></a>Creación de un ASE y de un plan de App Service juntos ##

Hola plan de servicio de aplicaciones es un contenedor de las aplicaciones. Cuando se crea una aplicación en App Service, seleccione o cree un plan de App Service. entornos de modelo del contenedor de Hello mantenga planes de servicio de aplicaciones y planes de servicio de aplicaciones las aplicaciones.

toocreate un ASE al crear un plan de servicio de aplicaciones:

1. Hola [portal de Azure](https://portal.azure.com/), seleccione **New** > **Web y móvil** > **aplicación Web**.

    ![Creación de la aplicación web][1]

2. Seleccione su suscripción. aplicación Hello y Hola ASE se crean en hello mismo las suscripciones.

3. Seleccione o cree un grupo de recursos. Con los grupos de recursos, puede administrar recursos de Azure relacionados como una unidad. Los grupos de recursos también son útiles cuando establece reglas de control de acceso basado en rol para las aplicaciones. Para obtener más información, vea hello [Introducción al administrador de recursos de Azure][ARMOverview].

4. Seleccione Hola plan de servicio de aplicaciones y, a continuación, seleccione **crear nuevo**.

    ![Nuevo plan de App Service][2]

5. Hola **ubicación** lista desplegable, región de hello seleccione dónde desea toocreate Hola ASE. Si selecciona una instancia de ASE existente, entonces no se crea ninguna. Hola plan de servicio de aplicaciones se crea en Hola ASE que seleccionó. 

6. Seleccione **tarifa**y elija una de hello **Isolated** precios SKU. Si elige una tarjeta de SKU **aislada** y una ubicación que no sea una instancia de ASE, significa que se va a crear una instancia de ASE en dicha ubicación. Seleccione toostart Hola proceso toocreate un ASE **seleccione**. Hola **Isolated** está disponible únicamente en combinación con un ASE SKU. Tampoco puede utilizar cualquier otra SKU de precios en una instancia de ASE distinta de la **aislada**.

    ![Selección del plan de tarifa][3]

7. Escriba el nombre de Hola para su ASE. Este nombre se utiliza en nombre direccionable de Hola para sus aplicaciones. Si el nombre de Hola de hello ASE es _appsvcenvdemo_, nombre de dominio de hello es *. appsvcenvdemo.p.azurewebsites.net*. Si crea una aplicación con nombre *mytestapp*, esta es direccionable a mytestapp.appsvcenvdemo.p.azurewebsites.net. No puede utilizar el espacio en blanco en el nombre de Hola. Si utiliza caracteres en mayúsculas, nombre de dominio de hello es versión en minúsculas total de Hola de ese nombre.

    ![Nombre del nuevo plan de App Service][4]

8. Especifique los detalles de redes virtuales de Azure. Seleccione **Crear nuevo** o **Seleccionar existente**. Hola opción tooselect una red virtual existente solo está disponible si tiene una red virtual en la región seleccionada de Hola. Si selecciona **crear nuevo**, escriba un nombre para la red virtual de Hola. Se crea una red virtual de Resource Manager con dicho nombre. Utiliza el espacio de direcciones de hello `192.168.250.0/23` en la región seleccionada de Hola. Si selecciona **Seleccionar existente**, tiene que:

    a. Seleccione el bloque de direcciones de red virtual de hello, si tiene más de uno.

    b. Escribir un nuevo nombre de subred.

    c. Seleccione el tamaño de Hola de subred Hola. *Recuerde tooselect un crecimiento futuro de tooaccommodate lo suficientemente grande como tamaño de su ASE.* Se recomienda un tamaño de `/25`, que tiene ciento veintiocho direcciones y puede controlar una instancia de ASE con un tamaño máximo. No se recomienda el tamaño de `/28`, por ejemplo, porque solo tiene dieciséis direcciones disponibles. La infraestructura usa al menos cinco direcciones. En una subred de tamaño `/28`, dispone de una escala máxima de once instancias.

    d. Seleccione el intervalo IP de subred de Hola.

9. Seleccione **crear** toocreate Hola ASE. Este proceso también crea el plan de servicio de aplicación hello y aplicación hello. Hola ASE, plan de servicio de aplicaciones y la aplicación están todos bajo Hola misma suscripción y también en Hola mismo grupo de recursos. Si su ASE necesita un grupo de recursos independiente, o si necesita una ASE de ILB, siga Hola pasos toocreate un ASE por sí mismo.

## <a name="create-an-ase-by-itself"></a>Creación de un ASE por sí mismo ##

Si crea una instancia de ASE independiente, esta no contendrá nada. Un ASE vacío sigue incurriendo en un cargo mensual para la infraestructura de Hola. Siga estos toocreate pasos un ASE con un ILB o toocreate un ASE en su propio grupo de recursos. Después de crear su ASE, puede crear aplicaciones en él mediante el uso de proceso normal de Hola. Seleccione el nuevo ASE como ubicación de Hola.

1. Búsqueda hello Azure Marketplace para **entono**, o seleccione **New** > **Web móvil** > **servicio de aplicaciones Entorno**. 

2. Escriba el nombre de Hola de su ASE. Este nombre se utiliza para las aplicaciones de hello creadas en hello ASE. Si es el nombre de hello *mynewdemoase*, nombre de subdominio de hello es *. mynewdemoase.p.azurewebsites.net*. Si crea una aplicación con nombre *mytestapp*, esta es direccionable a mytestapp.mynewdemoase.p.azurewebsites.net. No puede utilizar el espacio en blanco en el nombre de Hola. Si utiliza caracteres en mayúsculas, nombre de dominio de hello es Hola total minúsculas versión de Hola nombre. Si usa un ILB, el nombre la instancia de ASE no se usa en su subdominio pero, en su lugar, se indica explícitamente durante la creación de la instancia de ASE.

    ![Nomenclatura de ASE][5]

3. Seleccione su suscripción. Esta suscripción también es hello uno que usan todas las aplicaciones en hello ASE. No se puede colocar la instancia de ASE en una red virtual que se encuentra en otra suscripción.

4. Seleccione o especifique un nuevo grupo de recursos. grupo de recursos de Hello destinado a su ASE debe ser Hola uno mismo que se utiliza para la red virtual. Si selecciona una red virtual existente, selección de grupos de recursos de Hola para su ASE es tooreflect actualizado de la red virtual. *Puede crear un ASE con un grupo de recursos que es diferente del grupo de recursos de red virtual de hello si usa una plantilla de administrador de recursos.* toocreate un ASE desde una plantilla, consulte [crear un entorno de servicio de aplicaciones desde una plantilla de][MakeASEfromTemplate].

    ![Selección de grupo de recursos][6]

5. Seleccione la red virtual y la ubicación. Puede crear una red virtual o seleccionar una existente: 

    * Si selecciona una red virtual nueva, puede especificar un nombre y una ubicación. Hello red virtual nueva tiene Hola dirección intervalo 192.168.250.0/23 y una subred con el nombre predeterminado. subred de Hola se define como 192.168.250.0/24. Solo se puede seleccionar una red virtual de Resource Manager. Hola **VIP tipo** selección determina si su ASE puede tener acceso directamente desde internet (externo) de Hola o si usa un ILB. toolearn más información acerca de estas opciones, consulte [crear y usar un equilibrador de carga interno con un entorno de servicio de aplicaciones][MakeILBASE]. 

      * Si selecciona **externo** para hello **VIP tipo**, puede seleccionar cuántos sistema externo de Hola de direcciones IP se crea con fines de SSL basado en IP. 
    
      * Si selecciona **interno** para hello **VIP tipo**, debe especificar dominio Hola que usa su ASE. Puede implementar una instancia de ASE en una red virtual que utiliza intervalos de direcciones públicas o privadas. toouse una red virtual con un intervalo de direcciones públicas, deberá toocreate Hola red virtual antes de tiempo. 
    
    * Si selecciona una red virtual existente, se crea una nueva subred cuando se crea Hola ASE. *No puede usar una subred creada previamente en el portal de Hola. Puede crear una instancia de ASE con una subred existente si usa una plantilla de Resource Manager.* toocreate un ASE desde una plantilla, consulte [crear un entorno de servicio de aplicaciones desde una plantilla][MakeASEfromTemplate].

## <a name="app-service-environment-v1"></a>App Service Environment v1 ##

Todavía puede crear instancias de la primera versión de Hola de entorno del servicio de aplicación (ASEv1). toostart que procesar, Hola búsqueda Marketplace para **entono v1**. Crear ASE Hola Hola igual que crear Hola independiente ASE. Cuando termine, la instancia de ASEv1 tendrá dos servidores front-end y dos trabajos. Con ASEv1, debe administrar trabajos y los servidores front-end de Hola. No se agregan de forma automática al crear los planes de App Service. servidores front-end de Hello actúe como extremos HTTP/HTTPS de Hola y enviar tráfico toohello trabajadores. los trabajadores de Hello son roles de Hola que permite hospedar las aplicaciones. Puede ajustar la cantidad de Hola de servidores front-end y los trabajadores de la después de crear su ASE. 

toolearn más información sobre ASEv1, consulte [toohello Introducción entono v1][ASEv1Intro]. Para obtener más información sobre cómo ampliar, administrar y supervisar el ASEv1, consulte [cómo tooconfigure un entorno de servicio de aplicaciones][ConfigureASEv1].

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



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
