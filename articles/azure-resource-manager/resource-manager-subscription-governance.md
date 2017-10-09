---
title: "prácticas recomendadas de aaaBest para las empresas mover tooAzure | Documentos de Microsoft"
description: "Describe el scaffolding que las empresas pueden usar tooensure un entorno seguro y fácil de administrar."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: 8692f37e-4d33-4100-b472-a8da37ce628f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: d1402cf21d0cf740e44c03fc345ecd39a6e1680c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-enterprise-scaffold---prescriptive-subscription-governance"></a>Scaffolding empresarial de Azure: gobierno de suscripción preceptivo
Cada vez más empresas adoptan nube pública de Hola para su agilidad y flexibilidad. Se usan los ingresos toogenerate de puntos fuertes de la nube de Hola u optimizar los recursos para la empresa de Hola. Microsoft Azure proporciona un gran número de servicios que las empresas pueden ensamblar como bloques de creación tooaddress una amplia gama de aplicaciones y cargas de trabajo. 

Sin embargo, saber dónde toobegin a menudo es difícil. Después de decidir toouse Azure, unas cuantas preguntas que suelen surgirán:

* "¿Cómo puedo cumplir los requisitos legales de soberanía de datos en determinados países?"
* "¿Cómo puedo asegurarme de que alguien no modifique por error un sistema importante?"
* "¿Cómo puedo saber lo que cada recurso admite para poder tenerlo en cuenta y realizar la facturación de forma adecuada?"

es una tarea desalentadora potenciales Hola de una suscripción vacía con ningún raíles de protección. Este espacio en blanco puede dificultar su tooAzure de movimiento.

En este artículo se proporciona un punto de partida para profesionales técnicos tooaddress Hola necesidad de gobierno y equilibrar con hello necesario para la agilidad. Introduce el concepto de Hola de un scaffold empresarial que le guía a las organizaciones implementar y administrar sus suscripciones de Azure. 

## <a name="need-for-governance"></a>Necesidad de contar con un sistema de gobierno
Al mover tooAzure, debe resolver tema Hola de regulación temprano tooensure Hola uso correcto de nube de hello dentro de empresa de Hola. Desafortunadamente, tiempo de Hola y burocracia de creación de un sistema de regulación completa significa que algunos grupos de negocios ir directamente a toovendors sin la participación de TI empresarial. Este enfoque puede dejar Hola empresarial abra toovulnerabilities si no se administran correctamente los recursos de Hola. características de Hola de nube pública de hello - agilidad, la flexibilidad y precios basados en consumo - son importantes toobusiness grupos que necesitan tooquickly cumplir con las exigencias de Hola de clientes (internos y externos). Pero, TI empresarial necesita tooensure que están protegidos eficazmente los datos y sistemas.

En la vida real, scaffolding es la base de Hola de toocreate usado de la estructura de Hola. scaffolding de Hola guía directrices generales de Hola y proporciona puntos de anclaje para montar más permanente toobe de sistemas. Un scaffold enterprise es Hola mismo: un conjunto de controles flexibles y capacidades de Azure que proporcionan estructura toohello entorno y delimitadores para servicios basados en la nube pública de Hola. Proporciona generadores de hello (TI y grupos de negocios) un toocreate foundation y adjuntar nuevos servicios.

scaffolding de Hola se basa en las prácticas que hemos recopilado desde muchas contrataciones con los clientes de distintos tamaños. Intervalo de esos clientes desde pequeñas organizaciones desarrollar soluciones en las empresas de hello en la nube tooFortune 500 y fabricantes independientes de software que migrar y desarrollan soluciones de nube de Hola. Hola scaffold enterprise es toosupport flexible toobe "creado específicamente para ello" cargas de trabajo de TI tradicionales y cargas de trabajo de agile; como por ejemplo, los desarrolladores que crean aplicaciones de software como-servicio (SaaS) se basan en las capacidades de Azure.

scaffolding de empresa de Hola es toobe previsto Hola foundation de cada nueva suscripción dentro de Azure. Permite a los administradores tooensure las cargas de trabajo cumple Hola mínimos requisitos de gobierno de una organización sin impedir que cumple rápidamente sus propios objetivos los grupos de negocios y los desarrolladores.

> [!IMPORTANT]
> La gobernanza es fundamental toohello correcto de Azure. Este artículo Hola implementación técnica de scaffolding de una empresa pero solo afecta a proceso más amplio de Hola y las relaciones entre los componentes de Hola. Control de políticas fluye a lo largo de la parte superior de Hola y se determina por qué Hola empresa desea tooachieve. Naturalmente, creación de hello de un modelo de gobernanza de Azure incluye los representantes de TI, pero lo más importante es que debería tener fuerte representación de líderes de grupo de negocios y la administración de riesgos y de seguridad. Final de hello, un scaffold enterprise es sobre la mitigación de negocio riesgo toofacilitate misión y objetivos de la organización.
> 
> 

Hola siguiendo la imagen describe los componentes de Hola de scaffolding Hola. foundation Hola se basa en un plan sólido para departamentos, cuentas y suscripciones. pilares de Hello constan de las directivas del Administrador de recursos y los estándares de nomenclatura seguros. resto de Hola de scaffolding Hola procede principales capacidades de Azure y características que permiten un entorno seguro y fácil de administrar.

![Componentes de una plantilla scaffold](./media/resource-manager-subscription-governance/components.png)

> [!NOTE]
> Azure ha crecido rápidamente desde que se presentara en el 2008. Este crecimiento requiere equipos de ingeniería en Microsoft toorethink su enfoque para administrar e implementar servicios. modelo de Hello Azure Resource Manager se introdujo en 2014 y reemplaza el modelo de implementación clásica de Hola. El Administrador de recursos permite a las organizaciones toomore fácilmente implementar, organizar y controlar los recursos de Azure. Además, con esta herramienta se pueden crear recursos de forma paralela, de modo que es posible implementar más rápido soluciones complejas e interdependientes. También incluye el control de acceso granular y los recursos de tootag de capacidad de hello con metadatos. Microsoft recomienda crear todos los recursos a través del modelo de administrador de recursos de Hola. scaffolding de Hello enterprise está expresamente diseñado para modelo de administrador de recursos de Hola.
> 
> 

## <a name="define-your-hierarchy"></a>Definición de la jerarquía
base de Hola de scaffolding hello es Hola inscripción Enterprise de Azure (hello y Enterprise Portal). inscripción enterprise de Hello define la forma de Hola y el uso de los servicios de Azure dentro de una empresa y es la estructura de regulación de hello core. En el contrato enterprise de hello, los clientes pueden toofurther subdividir entorno hello en departamentos, cuentas y, por último, las suscripciones. Una suscripción de Azure es la unidad básica de Hola donde se encuentran todos los recursos. También define varios límites en Azure, como el número de núcleos, recursos, etc.

![Jerarquía](./media/resource-manager-subscription-governance/agreement.png)

Cada empresa es diferente y jerarquía de hello en la imagen anterior de hello permite gran flexibilidad en cómo se organiza Azure dentro de la empresa de Hola. Antes de implementar la orientación de hello contenida en este documento, debe modelar la jerarquía y comprender el impacto de hello en facturación, el acceso a los recursos y la complejidad.

Hola los tres patrones comunes para las inscripciones de Azure son:

* Hola **funcional** patrón
  
    ![functional](./media/resource-manager-subscription-governance/functional.png)
* Hola **unidad de negocio** patrón 
  
    ![Patrón de unidad de negocio](./media/resource-manager-subscription-governance/business.png)
* Hola **geográfica** patrón
  
    ![Patrón geográfico](./media/resource-manager-subscription-governance/geographic.png)

Aplicar scaffold hello en hello suscripción tooextend nivel Hola requisitos de gobierno de empresa de hello en una suscripción de Hola.

## <a name="naming-standards"></a>Estándares de nomenclatura
primer pilar de Hola de scaffolding Hola de nomenclatura estándar. Estándares de nomenclatura bien diseñados le permiten tooidentify recursos en el portal de hello, en una factura y dentro de los scripts. Es probable que ya tenga estándares de nomenclatura para la infraestructura local. Al agregar entorno de Azure tooyour, debe extenderlos tooyour de estándares de nomenclatura de recursos de Azure. Estándar de nomenclatura facilitar una administración más eficaz del entorno de Hola a todos los niveles.

> [!TIP]
> Convenciones de nomenclatura:
> * Revise y adoptar siempre que sea posible hello [Guía de patrones y prácticas](../guidance/guidance-naming-conventions.md). que lo ayudará a decidirse por un estándar de nomenclatura significativo.
> * Alterne el uso de mayúsculas y minúsculas en los nombres de recursos (por ejemplo, miGrupoDeRecursos y NombreDeLaRedVirtual). Nota: Hay determinados recursos, como cuentas de almacenamiento, donde hello única opción es toouse minúscula (y ningún otro carácter especial).
> * Considere el uso de Azure Resource Manager directivas (descritas en la sección siguiente de hello) tooenforce estándares de nomenclatura.
> 
> Hello sugerencias anteriores ayudarán a implementar una convención de nomenclatura coherente.

## <a name="policies-and-auditing"></a>Directivas y auditoría
pilar de segundo Hola de scaffolding Hola implica la creación de [directivas de Azure Resource Manager](resource-manager-policy.md) y [auditoría de registro de actividad de hello](resource-group-audit.md). Las directivas del Administrador de recursos ofrecen toomanage riesgo de capacidad de hello en Azure. Puede definir directivas que garanticen la soberanía de datos restringiendo, aplicando o auditando determinadas acciones. 

* Las directivas son un sistema de **permisos** predeterminado. Para controlar las acciones, definir y asignar directivas tooresources que deniegan o auditar las acciones en los recursos.
* Las directivas se describen a través de las definiciones de directiva en un lenguaje de definición de directivas (condiciones If-Then).
* Las directivas se crean con archivos JSON (notación de objetos JavaScript). Después de definir una directiva, puede asignarlo ámbito determinado de tooa: suscripción, el grupo de recursos o el recurso.

Las directivas tienen varias acciones que permiten una escenarios de tooyour enfoque específica. Hola acciones son:

* **Denegar**: solicitud de recursos de Hola de bloques
* **Auditoría**: permite la solicitud de hello pero agrega un registro de actividad de toohello de línea (que puede ser utilizados tooprovide alertas o runbooks tootrigger)
* **Anexar**: agrega información toohello recurso especificado. Por ejemplo, si no hay una etiqueta CostCenter en un recurso, agregue dicha etiqueta con un valor predeterminado.

### <a name="common-uses-of-resource-manager-policies"></a>Usos comunes de las directivas de Resource Manager
Directivas de administrador de recursos de Azure son una herramienta eficaz en hello Kit de herramientas de Azure. Le permiten tooavoid costos inesperados, tooidentify un centro de costos para los recursos a través de etiquetado y tooensure que se cumplen los requisitos de cumplimiento. Cuando las directivas se combinan con las características de auditoría integradas de hello, puede forma soluciones complejas y flexibles. Las directivas permiten a las compañías tooprovide controles para las cargas de trabajo de "TI tradicional" y las cargas de trabajo de "Ágiles"; como por ejemplo, desarrollo de aplicaciones de cliente. Hola modelos más comunes que se puede encontrar las directivas son:

* **Datos de cumplimiento de replicación geográfica soberanía** -Azure proporciona regiones a través de Hola a todos. Las empresas a menudo desea toocontrol donde se crean los recursos (si tooensure soberanía de datos o simplemente tooensure recursos se crean toohello Cierre final consumidores de recursos de hello).
* **Administración de costos**: una suscripción de Azure puede contener recursos de muchos tipos y escala. Las organizaciones a menudo desea tooensure dicho estándar suscripciones evite el uso de recursos innecesariamente grandes, lo que pueden costar cientos de dólares, un mes o más.
* **Predeterminado gobierno a través de etiquetas necesarias** -requerir etiquetas es una de las características de alta deseado y más comunes de Hola. Mediante las directivas del Administrador de recursos de Azure las empresas están tooensure puede que un recurso está correctamente etiquetado. Hello más comunes las etiquetas son: tipo de departamento, el propietario del recurso y el entorno (por ejemplo - producción, pruebas, desarrollo)

**Ejemplos**

Suscripción de TI tradicional para aplicaciones de línea de negocio

* Aplique las etiquetas Department y Owner en todos los recursos.
* Restringir creación de recursos toohello región América del Norte
* Restringir la capacidad de hello toocreate serie G las máquinas virtuales y clústeres de HDInsight

Entorno del método ágil para una unidad de negocio que va a crear aplicaciones en la nube

* requisitos de toomeet datos soberanía, permite la creación de hello de recursos solo en una región específica.
* Aplique la etiqueta Environment en todos los recursos. Si se crea un recurso sin una etiqueta, anexe hello **entorno: desconocido** etiqueta toohello recursos.
* Realice la auditoría cuando los recursos se creen fuera de Norteamérica, pero no la impida.
* Realice la auditoría cuando se creen recursos de alto costo.

> [!TIP]
> uso más común de las directivas del Administrador de recursos entre organizaciones Hello es toocontrol *donde* recursos pueden crearse y *qué* se pueden crear tipos de recursos. Además controla tooproviding en *donde* y *qué*, muchos recursos de tooensure de directivas de uso de las empresas tienen hello toobill de los metadatos adecuados para su uso. Se recomienda aplicar directivas en el nivel de suscripción de Hola para:
> 
> * Soberanía de datos y cumplimiento geográfico
> * Administración de costos
> * Etiquetas obligatorias (se determinan según la necesidad de la empresa, como BillTo y Application Owner)
> 
> Puede aplicar más directivas en niveles inferiores del ámbito.
> 
> 

### <a name="audit---what-happened"></a>Auditoría: ¿qué ha ocurrido?
tooview cómo funciona el entorno, deberá tooaudit la actividad de usuario. La mayoría de los tipos de recursos de Azure crean registros de diagnóstico que se pueden analizar a través de una herramienta de registro o en Azure Operations Management Suite. Puede recopilar registros de actividad a través de varias de las suscripciones de tooprovide, un departamento o la vista de la empresa. Los registros de auditoría son una herramienta de diagnóstico importante y un eventos de mecanismo fundamental tootrigger Hola entorno de Azure.

Registros de actividad de las implementaciones del Administrador de recursos permiten hello toodetermine **operations** que tuvo lugar y quién las realizó. Además, pueden recopilarse y agregarse mediante herramientas como Log Analytics.

## <a name="resource-tags"></a>Etiquetas del recurso
Como los usuarios de su organización Agregar suscripción de recursos de toohello, se convierte en recursos tooassociate cada vez más importante con el departamento adecuados de Hola, cliente y entorno. Puede adjuntar tooresources de metadatos a través de [etiquetas](resource-group-using-tags.md). Usar etiquetas tooprovide información acerca de los recursos de Hola o propietario de Hola. Las etiquetas permiten toonot solo agregado y agrupar los recursos de varias maneras, pero usan esos datos para fines de Hola de anulación. Puede etiquetar recursos con los pares de clave-valor too15. 

Las etiquetas del recurso son flexibles y deberían recursos toomost adjunto. Ejemplos de etiquetas de recursos comunes:

* BillTo
* Department (o Business Unit)
* Environment (Production, Stage y Development)
* Tier (Web Tier y Application Tier)
* Application Owner
* ProjectName

![etiquetas](./media/resource-manager-subscription-governance/resource-group-tagging.png)

Consulte [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md) (Convenciones de nomenclatura recomendadas para los recursos de Azure).

> [!TIP]
> Considere la posibilidad de utilizar una directiva que exija etiquetar los siguientes recursos:
> 
> * Grupos de recursos
> * Almacenamiento
> * Máquinas virtuales
> * Servidores web y entornos de servicios de aplicaciones
> 
> Esta estrategia etiquetada identifica a través de las suscripciones de los metadatos son necesarios para business hello, finanzas, seguridad, administración de riesgos y la administración general del entorno de Hola. 

## <a name="resource-group"></a>Grupos de recursos
El Administrador de recursos permite tooput recursos en grupos significativos para la afinidad de facturación o natural de administración. Como se mencionó anteriormente, Azure tiene dos modelos de implementación. Hola modelo clásico anterior, la unidad básica de administración de hello fue suscripción Hola. Era difícil toobreak recursos dentro de una suscripción, que llevó toohello creación de un gran número de suscripciones. Con el modelo del Administrador de recursos de hello, hemos visto Introducción Hola de grupos de recursos. Los grupos de recursos son contenedores de recursos que tienen un ciclo de vida común o comparten un atributo como "Todos los servidores SQL Server" o "Aplicación A".

Grupos de recursos no pueden estar contenidos dentro de otros y recursos sólo pueden pertenecer el grupo de recursos de tooone. Puede aplicar determinadas acciones en todos los recursos de un grupo de recursos. Por ejemplo, al eliminar un grupo de recursos quita todos los recursos en el grupo de recursos de Hola. Normalmente, se coloca una aplicación entera o sistema relacionadas en hello mismo grupo de recursos. Por ejemplo, una aplicación de tres niveles se denomina aplicación Web de Contoso contendría servidor de hello web, servidor de aplicaciones y SQL server en hello mismo grupo de recursos.

> [!TIP]
> Cómo organizar los grupos de recursos puede variar de las cargas de trabajo de "TI tradicional" demasiado las cargas de trabajo de "TI ágil":
> 
> * "Tradicional TI" cargas de trabajo normalmente se agrupan por elementos de hello mismo ciclo de vida, por ejemplo, una aplicación. Si se agrupan las aplicaciones, se podrán administrar las aplicaciones de forma individual.
> * "Agile TI" cargas de trabajo suelen toofocus en las aplicaciones de nube orientado al cliente externa. grupos de recursos de Hello deben reflejar las capas de Hola de implementación (por ejemplo, el nivel de Web, nivel de aplicación) y la administración.
> 
> La comprensión de la carga de trabajo lo ayudará a desarrollar una estrategia de grupo de recursos.

## <a name="role-based-access-control"></a>Control de acceso basado en rol
Probablemente se esté preguntando "que deben tener acceso tooresources?" y cómo puede controlar dicho acceso. Permitir o impedir el acceso toohello portal de Azure y controlar el acceso tooresources en el portal de hello es fundamental. 

Cuando inicialmente se lanzó Azure acceso controles tooa suscripción fueron básicos: administrador o Coadministrador. Obtener acceso a la suscripción tooa en hello clásico modelo implicado acceso tooall Hola recursos en el portal de Hola. Esta falta de un control específico ha provocado la proliferación de toohello de tooprovide un nivel de control de acceso razonable de suscripciones para una inscripción de Azure.

Esta proliferación de suscripciones ya no es necesaria. Con control de acceso basado en roles, puede asignar a usuarios a roles toostandard (por ejemplo, "lectura" comunes y los tipos de "escritor" de roles). También se pueden definir reglas personalizadas.

> [!TIP]
> control de acceso basado en roles de tooimplement:
> * Conectar su identidad corporativa almacén (normalmente Active Directory) tooAzure Active Directory utilizando Hola herramienta AD Connect.
> * Controlar Hola administrador o Coadministrador de una suscripción mediante una identidad administrada. **No** asignar administrador o Coadministrador tooa nuevo propietario de la suscripción. En su lugar, use RBAC roles tooprovide **propietario** derechos tooa grupo o un usuario.
> * Agregar grupo de usuarios de Azure tooa (por ejemplo, los propietarios de X de aplicaciones) en Active Directory. Utilizar Hola grupo sincronizados tooprovide grupo miembros Hola derechos adecuados toomanage Hola grupo de recursos que contiene la aplicación hello.
> * Siga el principio Hola Hola para conceder **privilegios mínimos** toodo necesario Hola espera el trabajo. Por ejemplo:
>   * Grupo de implementación: Un grupo que sea capaz de toodeploy únicamente los recursos.
>   * Administración de máquinas virtuales: Un grupo que es capaz de toorestart las máquinas virtuales (para las operaciones)
> 
> Estas sugerencias lo ayudarán a administrar el acceso de los usuarios en la totalidad de su suscripción.

## <a name="azure-resource-locks"></a>Bloqueos de recursos de Azure
A medida que su organización agrega la suscripción a toohello los servicios principales, se convierte en tooensure cada vez más importante que dichos servicios estén disponibles tooavoid interrupción del negocio. [Bloqueos de recursos](resource-group-lock-resources.md) permiten operaciones de toorestrict en los recursos de gran valor donde modificarlos o eliminarlos tendría un gran impacto en las aplicaciones o la infraestructura de nube. Puede aplicar bloqueos tooa suscripción, el grupo de recursos o el recurso. Normalmente, se aplican bloqueos toofoundational recursos, como redes virtuales y las puertas de enlace, las cuentas de almacenamiento. 

Además, en estos momentos, admiten dos valores: CanNotDelete y ReadOnly. CanNotDelete significa que los usuarios (con los derechos adecuados hello) todavía pueden lee o modificar un recurso pero no puede eliminarlo. ReadOnly significa que los usuarios autorizados no pueden eliminar o modificar un recurso.

bloqueos de administración toocreate o delete, debe tener acceso demasiado`Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*` acciones.
De las funciones integradas de hello, solo el propietario y el Administrador de acceso de usuario se conceden dichas acciones.

> [!TIP]
> Las opciones de red principales deben protegerse con bloqueos. La eliminación accidental de una puerta de enlace VPN de sitio a sitio podría ser desastroso tooan suscripción de Azure. Azure no permite toodelete una red virtual que está en uso, pero más restricciones de la aplicación es útil medida de precaución. 
> 
> * Red virtual: CanNotDelete
> * Grupo de seguridad de red: CanNotDelete
> * Directivas: CanNotDelete
> 
> Las directivas también son mantenimiento toohello fundamental de los controles adecuados. Le recomendamos que aplique una **CanNotDelete** bloquear toopolices que están en uso.

## <a name="core-networking-resources"></a>Recursos de red principales
Tooresources de acceso pueden ser internos (dentro de la red de organización de hello) o externos (a través de internet de Hola). Es fácil para los usuarios en sus organización tooinadvertently put recursos en lugar de hello incorrecto y posiblemente abrirlos toomalicious acceso. Al igual que con los dispositivos locales, las empresas deben agregar tooensure controles adecuados que Azure a los usuarios tomar decisiones correctas de Hola. Para el gobierno de suscripciones, identificamos los recursos principales que proporcionan un control de acceso básico. recursos principales de Hello constan de:

* Las **redes virtuales** son objetos de contenedor de las subredes. Aunque no es estrictamente necesario, a menudo se usa al conectarse a recursos corporativos de aplicaciones toointernal.
* **Grupos de seguridad de red** similar firewall tooa y proporcionan las reglas de cómo un recurso puede "hablar" a través de red de Hola. Proporciona un control granular sobre cómo ni Hola mismo si una subred (o la máquina virtual) se pueden conectar toohello Internet u otras subredes en red virtual.

![Redes principales](./media/resource-manager-subscription-governance/core-network.png)

> [!TIP]
> En el caso de las redes:
> * Crear redes virtuales dedicadas tooexternal orientada a las cargas de trabajo y las cargas de trabajo interna. Este enfoque reduce la posibilidad de Hola de forma inadvertida colocar máquinas virtuales que están diseñadas para las cargas de trabajo internos en un espacio con orientación externo.
> * Configurar el acceso de toolimit de grupos de seguridad de red. Como mínimo, bloquear toohello de acceso a internet desde las redes virtuales internas y la red corporativa toohello de bloque acceso de redes virtuales externas.
> 
> Estas sugerencias lo ayudarán a implementar recursos de red seguros.

### <a name="automation"></a>Automation
Administrar los recursos de manera individual es un proceso lento y potencialmente propenso a errores en determinadas operaciones. Azure proporciona varias funciones de automatización, como Azure Automation, Logic Apps y Azure Functions. [Automatización de Azure](../automation/automation-intro.md) permite a los administradores toocreate y definir runbooks toohandle las tareas comunes en la administración de recursos. Puede crear runbooks mediante un editor de código de PowerShell o uno de tipo gráfico. Puede generar flujos de trabajo complejos de varias fases. Automatización de Azure suele ser toohandle usado tareas comunes, como apagar los recursos no utilizados o creación de recursos en desencadenador específico de respuesta tooa sin necesidad de intervención humana.

> [!TIP]
> En el caso de la automatización:
> * Crear una cuenta de automatización de Azure y revisar Hola los runbooks disponibles (línea de comandos y gráfica) disponibles en hello [Galería de runbooks](../automation/automation-runbook-gallery.md).
> * Importe y personalice los runbooks claves para utilizarlos.
> 
> Un escenario común es la capacidad de máquinas virtuales hello tooStart/apagado según una programación. Hay runbooks de ejemplo están disponibles en la Galería de Hola que controlar este escenario y mostrarle cómo tooexpand lo.
> 
> 

## <a name="azure-security-center"></a>Azure Security Center
Quizás uno de adopción de hello mayor bloqueadores toocloud ha sido preocupaciones Hola sobre seguridad. Los administradores de riesgos de TI y departamentos de seguridad deben tooensure que los recursos de Azure están protegidos. 

Hola [Azure Security Center](../security-center/security-center-intro.md) proporciona una vista central de estado de seguridad de Hola de recursos en las suscripciones de Hola y se ofrecen recomendaciones que le ayudan a evitar que los recursos en peligro. Pueden habilitar directivas más granulares (por ejemplo, aplicar directivas toospecific grupos de recursos que permiten su riesgo de toohello de posición que se dirección de hello enterprise tootailor). Por último, el centro de seguridad de Azure es una plataforma abierta que permite a los socios de Microsoft y software de toocreate de proveedores de software independientes que se conecta a Azure Security Center tooenhance sus capacidades. 

> [!TIP]
> Azure Security Center está habilitado de forma predeterminada en todas las suscripciones. Sin embargo, debe habilitar la recopilación de datos de máquinas virtuales tooallow Azure Security Center tooinstall su agente y empezar a recopilar datos.
> 
> ![recopilación de datos](./media/resource-manager-subscription-governance/data-collection.png)
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Ahora que ha aprendido sobre la regulación de la suscripción, es el tiempo toosee estas recomendaciones en la práctica. Vea [Examples of implementing Azure subscription governance](resource-manager-subscription-examples.md) (Ejemplos de implementación de un sistema de gobierno de suscripciones).

