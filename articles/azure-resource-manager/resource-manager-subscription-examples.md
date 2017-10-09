---
title: "aaaScenarios y ejemplos para la regulación de suscripción | Documentos de Microsoft"
description: "Proporciona ejemplos de cómo tooimplement regulación de suscripción de Azure para los escenarios comunes."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: e8fbeeb8-d7a1-48af-804f-6fe1a6024bcb
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: f750e834519c8e64f57f87e2067801feb38b5c29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Ejemplos de implementación de plantillas scaffold empresariales de Azure
Este tema ofrecen ejemplos de cómo una empresa puede implementar recomendaciones de Hola para un [scaffold Azure enterprise](resource-manager-subscription-governance.md). Usa una compañía ficticia denominada Contoso tooillustrate mejores prácticas para los escenarios comunes.

## <a name="background"></a>Fondo
Contoso es una empresa en todo el mundo que proporciona soluciones de la cadena de suministro de los clientes de todo el contenido de un modelo de "Software como servicio" modelo tooa empaquetado implementado en local.  Software que desarrollan todo mundo Hola con centros de desarrollo importante en India, Estados Unidos de Hola y Canadá.

parte de ISV de Hola de empresa de Hola se divide en varias unidades de negocio independientes que administran productos en un significativos para el negocio. Cada unidad de negocio tiene sus propios arquitectos, directores de producto y desarrolladores.

unidad de negocio de servicios de tecnología de empresa (ETS) Hola proporciona la capacidad de TI centralizada y administra varios centros de datos donde las unidades de negocio hospedan sus aplicaciones. Junto con la administración de centros de datos de hello, hello organización ETS proporciona y administra la colaboración centralizada (por ejemplo, correo electrónico y sitios Web) y servicios de red y telefonía. También se encargan de las cargas de trabajo orientadas al cliente de las unidades de negocio más pequeñas que no disponen de personal de operaciones.

Hola siguiendo los roles se utiliza en este tema:

* Dave es el Administrador de Azure ETS Hola.
* Alice es Director de desarrollo de Contoso en la unidad de negocio de cadena de suministro de Hola.

Contoso requiere la aplicación de toobuild una línea de negocio y una aplicación orientado al cliente. Ha decidido toorun Hola aplicaciones en Azure. Dave lee hello [regulador prescriptiva suscripción](resource-manager-subscription-governance.md) tema, y está ahora listo tooimplement recomendaciones Hola.

## <a name="scenario-1-line-of-business-application"></a>Escenario 1: aplicación de línea de negocio
Contoso está generando un toobe de sistema (BitBucket) de administración de código fuente utilizada por los desarrolladores de Hola a todos.  aplicación Hello infraestructura como servicio (IaaS) utiliza para hospedar y consta de servidores web y un servidor de base de datos. Los desarrolladores tengan acceso a servidores en sus entornos de desarrollo, pero no necesita acceso toohello servidores en Azure. Contoso ETS desea propietario de la aplicación hello tooallow y aplicación de hello toomanage de equipo. aplicación Hello sólo está disponible mientras se encuentre en la red corporativa de Contoso. Dave debe tooset la suscripción de Hola para esta aplicación. suscripción de Hello también hospedará otro software relacionados con el desarrollador en hello futuras.  

### <a name="naming-standards--resource-groups"></a>Estándares de nomenclatura y grupos de recursos
David crea una suscripción de herramientas de desarrollo de toosupport que son comunes a todas las unidades de negocio de Hola. Debe toocreate nombres descriptivos para la suscripción de Hola y grupos de recursos (por aplicación hello y redes de hello). Crea Hola los grupos de suscripción y los recursos siguientes:

| Elemento | Nombre | Descripción |
| --- | --- | --- |
| La suscripción |Contoso ETS DeveloperTools Production |Admite las herramientas de desarrollo comunes. |
| Grupo de recursos |rgBitBucket |Contiene Hola aplicación web y servidor de base de datos |
| Grupo de recursos |rgCoreNetworks |Contiene las redes virtuales hello y conexión de puerta de enlace de sitio a sitio |

### <a name="role-based-access-control"></a>Control de acceso basado en rol
Después de crear su suscripción, Dave desea tooensure que Hola equipos adecuados y los propietarios de aplicaciones pueden tener acceso a sus recursos. David identifica que cada equipo tiene requisitos diferentes. Utiliza grupos Hola que se han sincronizado desde tooAzure de Active Directory (AD) local de Contoso Active Directory y proporciona el nivel adecuado de Hola de equipos de toohello de acceso.

Dave asigna Hola después de roles para la suscripción de hello:

| Rol | Asignado demasiado| Descripción |
| --- | --- | --- |
| [Propietario](../active-directory/role-based-access-built-in-roles.md#owner) |Identificador administrado del servicio AD de Contoso |Este identificador se controla con acceso Just-In-Time (JIT) a través de la herramienta de administración de identidades de Contoso. Asimismo, garantiza que se audite por completo el acceso del propietario de la suscripción. |
| [Administrador de seguridad](../active-directory/role-based-access-built-in-roles.md#security-manager) |Departamento de administración de riesgos y seguridad |Este rol permite toolook de usuarios en hello Azure Security Center y el estado de Hola de recursos de Hola. |
| [Colaborador de la red](../active-directory/role-based-access-built-in-roles.md#network-contributor) |Equipo de red |Esta función permite Hola sitio tooSite VPN de Contoso red equipo toomanage y Hola redes virtuales. |
| *Rol personalizado* |Propietario de la aplicación |David crea un rol que concede Hola capacidad toomodify recursos en grupo de recursos de Hola. Para obtener más información, vea el artículo [Roles personalizados en RBAC de Azure](../active-directory/role-based-access-control-custom-roles.md). |

### <a name="policies"></a>Directivas
Dave tiene Hola según los requisitos para administrar recursos de suscripción de hello:

* Dado que las herramientas de desarrollo Hola admiten los desarrolladores a través de Hola a todos, no desea que los usuarios de tooblock desde la creación de recursos en cualquier región. Sin embargo, debe tooknow donde se crean los recursos.
* Además, le preocupan los costos. Por lo tanto, quiere tooprevent propietarios de las aplicaciones de creación de máquinas virtuales innecesariamente costosas.  
* Dado que esta aplicación atiende a los desarrolladores en muchas unidades de negocio, quiere tootag cada recurso con el propietario de unidad y la aplicación de empresa de Hola. Mediante el uso de estas etiquetas, ETS puede facturar a los equipos adecuados de Hola.

Crea los siguientes hello [las directivas del Administrador de recursos](resource-manager-policy.md):

| Campo | Efecto | Descripción |
| --- | --- | --- |
| location |audit |Creación de hello de recursos de Hola en cualquier región de auditoría |
| type |deny |Deniega la creación de máquinas virtuales de serie G. |
| etiquetas |deny |Exige la etiqueta de propietario de la aplicación. |
| etiquetas |deny |Exige la etiqueta de centro de costos. |
| etiquetas |append |Anexe el nombre de etiqueta **unidad de negocio** y el valor **ETS** tooall recursos |

### <a name="resource-tags"></a>Etiquetas del recurso
Dave es consciente de que debe toohave información específica en el centro de costo de hello bill tooidentify hello para la implementación de BitBucket Hola. Además, Dave desea tooknow que todos los recursos que pertenezcan ETS de Hola.

Agrega siguiente hello [etiquetas](resource-group-using-tags.md) toohello grupos de recursos y recursos.

| Nombre de etiqueta | Valor de etiqueta |
| --- | --- |
| ApplicationOwner |nombre de Hola de hello quien administra esta aplicación. |
| CostCenter |Centro de costo de Hello del grupo de Hola que paga para hello consumo de Azure. |
| BusinessUnit |**ETS** (unidad de negocio Hola asociada Hola suscripción) |

### <a name="core-network"></a>Red principal
Hola ETS Contoso propuesto de la información de equipo de administración de riesgos y de seguridad revisa Dave planear toomove Hola aplicación tooAzure. Desean tooensure que no es de aplicación hello expone toohello internet.  Dave también tiene aplicaciones de desarrollador que Hola futuras serán tooAzure movida. Estas aplicaciones requieren interfaces públicas.  toomeet estos requisitos, proporciona redes virtuales externas e internas tanto el acceso toorestrict de un grupo de seguridad de red.

Crea Hola recursos siguientes:

| Tipo de recurso | Nombre | Descripción |
| --- | --- | --- |
| Red virtual |vnInternal |Utilizado con hello BitBucket aplicación y está conectado a través de la red corporativa del tooContoso de ExpressRoute.  Una subred (sbBitBucket) proporciona la aplicación hello con un espacio de direcciones IP específico. |
| Virtual Network |vnExternal |Está disponible para las aplicaciones futuras que requieran puntos de conexión orientados al público. |
| Grupo de seguridad de red (NSG) |nsgBitBucket |Se asegura de que Hola se minimiza la superficie expuesta a ataques de esta carga de trabajo al permitir conexiones solo en el puerto 443 para la subred de Hola donde la aplicación hello vive (sbBitBucket). |

### <a name="resource-locks"></a>Bloqueos de recursos
Dave reconoce que la conectividad de Hola desde la red virtual interna toohello de red corporativa de Contoso debe protegerse de cualquier script ejercer o eliminación accidental.

Crea los siguientes hello [bloqueo de recurso](resource-group-lock-resources.md):

| Tipo de bloqueo | Recurso | Descripción |
| --- | --- | --- |
| **CanNotDelete** |vnInternal |Impide que los usuarios eliminando red virtual de Hola o subredes, pero no impide la adición de Hola de nuevas subredes. |

### <a name="azure-automation"></a>Azure Automation
Dave no tiene nada tooautomate para esta aplicación. Aunque creó una cuenta de Azure Automation, por ahora, no la utilizará.

### <a name="azure-security-center"></a>Azure Security Center
Administración de servicios de TI de Contoso debe tooquickly identifican ni controlan las amenazas. También desean toounderstand los problemas que existan.  

toofulfill estos requisitos, Dave habilita hello [Azure Security Center](../security-center/security-center-intro.md)y proporciona la función de administrador de seguridad de acceso toohello.

## <a name="scenario-2-customer-facing-app"></a>Escenario 2: aplicación orientada al cliente
liderazgo de negocio de Hello en la unidad de negocio de cadena de suministro de hello ha identificado varios compromiso de tooincrease de oportunidades con los clientes de Contoso mediante el uso de una tarjeta de fidelización. Equipo de Alicia debe crear esta aplicación y decide que Azure aumenta su toomeet capacidad hello las necesidades del negocio. Alice funciona con Dave desde tooconfigure dos suscripciones de ETS para desarrollar y usar esta aplicación.

### <a name="azure-subscriptions"></a>Suscripciones de Azure
Dave inicia sesión en toohello Azure Enterprise Portal y ve que ese departamento de cadena de suministro de hello ya existe.  Sin embargo, como este proyecto es el primer proyecto de desarrollo hello para el equipo de cadena de suministro de hello en Azure, Dave reconoce Hola necesidad de una nueva cuenta de equipo de desarrollo de Alicia.  Crea la cuenta de "I+d" hello para su equipo y asigna acceso tooAlice. Alice inicia sesión a través de hello portal de Azure y crea dos suscripciones: servidores de desarrollo de una toohold hello y servidores de producción de hello uno toohold.  Sigue estándares de nomenclatura de hello establecido previamente al crear Hola siguientes suscripciones:

| Uso de la suscripción | Nombre |
| --- | --- |
| Desarrollo |SupplyChain ResearchDevelopment LoyaltyCard Development |
| Producción |SupplyChain Operations LoyaltyCard Production |

### <a name="policies"></a>Directivas
Dave y Alice analizar aplicación hello e identifican que esta aplicación solo sirve a clientes de la región de Norteamérica Hola.  Alicia y su equipo plan de Azure toouse entorno de servicio de aplicaciones y aplicaciones de Azure SQL toocreate Hola. Máquinas virtuales de toocreate pueden necesitar durante el desarrollo.  Alicia quiere tooensure que sus desarrolladores tienen recursos de hello necesitan tooexplore y examinar problemas sin extrayendo ETS.

Para hello **suscripción desarrollo**, crean Hola después de la directiva:

| Campo | Efecto | Descripción |
| --- | --- | --- |
| location |audit |Creación de hello de recursos de Hola en cualquier región de auditoría. |

No limitar el tipo de Hola de sku que puede crear un usuario en el desarrollo y no requieren etiquetas para los grupos de recursos o los recursos.

Para hello **suscripción de producción**, crean hello las siguientes directivas:

| Campo | Efecto | Descripción |
| --- | --- | --- |
| location |deny |Denegar el permiso de creación de hello de todos los recursos fuera de centros de datos de hello Estados Unidos. |
| etiquetas |deny |Exige la etiqueta de propietario de la aplicación. |
| etiquetas |deny |Exige la etiqueta de departamento. |
| etiquetas |append |Agregar grupo de recursos de tooeach de etiqueta que indica el entorno de producción. |

No limite tipo hello de sku que puede crear un usuario en producción.

### <a name="resource-tags"></a>Etiquetas del recurso
Dave es consciente de que debe grupos de negocios correcto de Hola de tooidentify de toohave información específica para la facturación y la propiedad. Por ello, define las etiquetas de recurso para los grupos de recursos y recursos.

| Nombre de etiqueta | Valor de etiqueta |
| --- | --- |
| ApplicationOwner |nombre de Hola de hello quien administra esta aplicación. |
| department |Centro de costo de Hello del grupo de Hola que paga para hello consumo de Azure. |
| EnvironmentType |**Producción** (aunque Hola suscripción incluye **producción** en nombre de hello, incluyendo esta etiqueta permite facilitar su identificación cuando se examinan los recursos en el portal de Hola o de facturación de Hola.) |

### <a name="core-networks"></a>Redes principales
Hola ETS Contoso propuesto de la información de equipo de administración de riesgos y de seguridad revisa Dave planear toomove Hola aplicación tooAzure. Desean tooensure que Hola aplicaciones de tarjeta de fidelización correctamente está aislada y protegido en una red de la red Perimetral.  Este requisito, Alicia y Dave toofulfill crear un hello de tooisolate de grupo de seguridad de red aplicaciones de tarjeta de fidelización y una red virtual externa desde la red corporativa de hello Contoso.  

Para hello **suscripción desarrollo**, crean:

| Tipo de recurso | Nombre | Descripción |
| --- | --- | --- |
| Red virtual |vnInternal |Para entornos de desarrollo de tarjeta de fidelización de Contoso hello y se conecta a través de la red corporativa del tooContoso de ExpressRoute. |

Para hello **suscripción de producción**, crean:

| Tipo de recurso | Nombre | Descripción |
| --- | --- | --- |
| Red virtual |vnExternal |Hospeda la aplicación de la tarjeta de fidelización de hello y no está conectado directamente tooContoso's ExpressRoute. Se inserta código a través de su sistema de código fuente directamente los servicios de PaaS de toohello. |
| Grupo de seguridad de red (NSG) |nsgBitBucket |Se asegura de que Hola superficie expuesta a ataques de esta carga de trabajo se minimiza solo tiene que permitir la comunicación de entrada en TCP 443.  Contoso también está investigando el uso de un firewall de aplicación web para agregar más protección. |

### <a name="resource-locks"></a>Bloqueos de recursos
Dave y Alice confieren y decida tooadd bloqueos de recursos en algunos de los recursos clave Hola Hola entorno tooprevent la eliminación accidental durante una inserción de código malicioso.

Crean Hola después de bloqueo:

| Tipo de bloqueo | Recurso | Descripción |
| --- | --- | --- |
| **CanNotDelete** |vnExternal |tooprevent a los usuarios de eliminación de red virtual de Hola o subredes. bloqueo de Hello impedir la adición de Hola de nuevas subredes. |

### <a name="azure-automation"></a>Azure Automation
Alicia y su equipo de desarrollo tienen runbooks amplio entorno de hello toomanage para esta aplicación. Hola runbooks permiten Hola adición o eliminación de nodos para la aplicación hello y otras tareas de DevOps.

toouse Estos runbooks, le permiten [automatización](../automation/automation-intro.md).

### <a name="azure-security-center"></a>Azure Security Center
Administración de servicios de TI de Contoso debe tooquickly identifican ni controlan las amenazas. También desean toounderstand los problemas que existan.  

toofulfill estos requisitos, Dave habilita Azure Security Center. Se asegura de que hello Azure Security Center es la supervisión de recursos de Hola y proporciona acceso a los equipos de seguridad y DevOps toohello.

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de cómo crear plantillas de administrador de recursos, consulte [las prácticas recomendadas para la creación de plantillas de Azure Resource Manager](resource-manager-template-best-practices.md).

