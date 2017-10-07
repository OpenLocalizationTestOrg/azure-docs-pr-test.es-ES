---
title: aaaGovernance en Azure | Documentos de Microsoft
description: "Obtenga información acerca de los servicios informáticos en la nube que incluyen una amplia selección de instancias de proceso y servicios que se pueden escalar arriba y abajo automáticamente toomeet hello las necesidades de su aplicación o enterprise."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: TomSh
ms.openlocfilehash: 956e82e92f4232c24069bdb79fed5315f1d6486f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="governance-in-azure"></a>Sistema de gobierno en Azure

Somos conscientes de que la seguridad es trabajo en la nube de Hola y la importancia que tiene que buscar información precisa y oportuna sobre la seguridad de Azure. Uno de hello mejor motivos toouse Azure para las aplicaciones y servicios es tootake aprovechar su amplia gama de capacidades y herramientas de seguridad. Estas herramientas y capacidades que esté soluciones seguras toocreate posibles en la plataforma Windows Azure segura de Hola.

toohelp que comprender mejor matriz Hola de controles de regulación implementado en Microsoft Azure desde ambos clientes de Hola y se escriben las perspectivas de las operaciones de Microsoft, este artículo, "Gobierno en Azure", que proporciona información completa sobre Hola Características de regulación disponibles con Microsoft Azure.

## <a name="azure-platform"></a>Plataforma Azure

Azure es una plataforma de servicios en la nube pública que admite una amplia variedad de sistemas operativos, lenguajes de programación, marcos, herramientas, bases de datos y dispositivos. Se pueden ejecutar contenedores de Linux con integración de Docker, compilar aplicaciones con JavaScript, Python, .NET, PHP, Java y Node.js, y crear back-ends para dispositivos iOS, Android y Windows. Servicios de nube pública de Azure admiten Hola mismas tecnologías millones de desarrolladores y profesionales de TI ya se basan en y de confianza.

Al compilar en, o migrar los activos de TI a, un proveedor de servicios de nube pública depende de tooprotect de capacidades de la organización sus aplicaciones y datos con controles de Hola y de servicios de hello proporcionan seguridad de hello toomanage de basados en la nube activos.

Diseño de la infraestructura de Azure de hello facility tooapplications para hospedar simultáneamente millones de clientes y proporciona una base de confianza en los que las empresas pueden satisfacer sus requisitos de seguridad. Además, Azure ofrece muchas opciones de seguridad y Hola capacidad toocontrol ellas para que puedan personalizar requisitos únicos Hola de seguridad toomeet de las implementaciones de su organización.

En este documento se explica cómo las funcionalidades de gobierno de Azure pueden ayudarlo a cumplir estos requisitos.

## <a name="abstract"></a>Descripción breve

Regulación de la nube de Microsoft Azure proporciona una auditoría integrado y un nuevo enfoque de consultoría para revisar y avisa de las organizaciones de su uso de hello plataforma Windows Azure. Regulación de la nube de Microsoft Azure hace referencia procesos de toma de decisiones toohello, criterios y las directivas implicadas en la planificación de hello, arquitectura, adquisición, implementación, operación y administración de una nube de informática.

toocreate un plan para la regulación de la nube de Microsoft Azure, debe tootake obtener información detallada sobre Hola personas, procesos y tecnologías actualmente en vigor y, a continuación, marcos de trabajo de compilación que facilitan a TI tooconsistently admiten las necesidades empresariales al proporcionar final usuarios con hello flexibilidad toouse Hola eficaces características de Microsoft Azure.

En este artículo se describe cómo puede lograr un nivel elevado de gobierno de los recursos de TI en Microsoft Azure. Este documento puede ayudarle a entender las características de seguridad y gobernanza de hello integradas en tooMicrosoft Azure.

siguiente Hola es los problemas de control principal Hola descritos en este documento:

- Implementación de directivas, procesos y procedimientos según los objetivos de la organización

- Seguridad y cumplimiento continuo con las normas de las organizaciones

- Supervisión y alertas

## <a name="implementation-of-policies-processes-and-procedures"></a>Implementación de directivas, procesos y procedimientos 

Administración ha establecido la implementación de toooversee de roles y responsabilidades de directiva de seguridad de información de Hola y continuidad de las operaciones a través de Azure. Asimismo, es responsable de supervisar la seguridad y los procedimientos de continuidad en sus respectivos equipos (incluidos los terceros), así como de facilitar el cumplimiento con las directivas de seguridad, los procesos y las normas.

Estos son factores Hola evolucionados:

- Account Provisioning (Aprovisionamiento de cuentas)

- Controles de suscripción

- Control de acceso basado en rol

- Administración de recursos

- Seguimiento de recursos

- Control de recursos críticos

- El acceso de API tooBilling información

- Controles de red

## <a name="account-provisioning"></a>Aprovisionamiento de cuentas

Definir cuenta jerarquía es un paso importante toouse y estructura de los servicios de Azure dentro de una empresa y es la estructura de regulación de hello core. En el caso de los clientes con el contrato enterprise de hello, los clientes pueden subdividir entorno hello en departamentos, cuentas y, por último, las suscripciones.

![Account Provisioning (Aprovisionamiento de cuentas)](./media/governance-in-azure/security-governance-in-azure-fig1.png)

Si no tiene un contrato enterprise, considere la posibilidad de usar [etiquetas Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) en la jerarquía de toodefine nivel de suscripción. Una suscripción de Azure es la unidad básica de Hola donde se encuentran todos los recursos. También define varios límites en Azure, como el número de núcleos, recursos, etc. Las suscripciones pueden contener [grupos de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), que pueden incluir recursos. En estos tres niveles se aplican los principios de [RBAC](https://docs.microsoft.com/azure/api-management/api-management-role-based-access-control).

Cada empresa es diferente y jerarquía de hello mediante etiquetas de Azure en el caso de los clientes de empresa no permite gran flexibilidad en cómo se organiza Azure dentro de la empresa de Hola. Antes de implementar recursos en Microsoft Azure, debe jerarquía de modelo y comprender el impacto de hello en facturación, el acceso a los recursos y la complejidad.

## <a name="subscription-controls"></a>Controles de suscripción

La suscripción controla cómo se notifica y factura el uso de los recursos. Las suscripciones pueden estar configuradas para que la facturación y los pagos sean independientes. Como mencionamos anteriormente, en una cuenta de Azure podemos tenemos varias suscripciones. Las suscripciones pueden ser utilizados toodetermine Hola recursos de Azure uso de varios departamentos de una empresa.

Por ejemplo, una compañía tiene departamentos de TI, de recursos humanos y de marketing con diferentes proyectos en marcha. Según el uso de Hola de recursos de Azure como máquinas virtuales por cada departamento, pueden facturarán según corresponda. Por este podemos controlar Finanzas Hola de cada departamento.

Las suscripciones de Azure establecen tres parámetros:

- Un identificador de suscriptor único

- Una ubicación de facturación

- Conjunto de recursos disponibles

Para un usuario individual, que incluye un Id. de cuenta de Microsoft, servicios de una tarjeta de crédito hello y número de serie completa de Azure--aunque Microsoft aplica límites de consumo, según el tipo de suscripción de Hola.

Las jerarquías de inscripción Azure definen cómo se estructuran los servicios en un contrato Enterprise. Hola Enterprise Portal permite a los clientes acceder a los toodivide tooAzure recursos asociados con un contrato Enterprise, en función de necesidades únicas de la organización de jerarquías flexibles tooan personalizable. patrón de la jerarquía de Hello debe coincidir con administración y la estructura geográfica de una organización para que Hola asociados facturación y acceso a los recursos puede tenerse con precisión.

patrones de alto nivel de Hello tres son unidad funcional, business, y departamentos geográficos, utilizando como una construcción administrativa para explicar las agrupaciones. Dentro de cada departamento, las cuentas pueden tener suscripciones asignadas, con lo que se generan silos de facturación y varios límites importantes en Azure (por ejemplo, número de máquinas virtuales, cuentas de almacenamiento, etc.).

![Controles de suscripción](./media/governance-in-azure/security-governance-in-azure-fig2.png)


En lo que respecta a las organizaciones con un contrato Enterprise, las suscripciones de Azure siguen una jerarquía de cuatro niveles:

- Administrador de inscripciones de la empresa

- Administrador de departamentos

- Propietario de cuenta

- Administrador de servicios

Esta jerarquía rige siguiente hello:

- Relación de facturación

- Administración de cuentas

- Rol tooartifacts de Control de acceso basado en (RBAC)

- Límites

- Límites

  - Uso y facturación (lista de tarifas basada en números de oferta)

  - límites

  - Virtual Network

- Adjunta too1 AAD (1 AAD asociarse a muchas suscripciones)

- Cuenta de inscripción enterprise tooan asociado

## <a name="role-based-access-controls"></a>Controles de acceso basado en rol

Cuando inicialmente se lanzó Azure acceso controles tooa suscripción fueron básicos: administrador o Coadministrador. Obtener acceso a la suscripción tooa en hello clásico modelo implicado acceso tooall Hola recursos en el portal de Hola. Esta falta de un control específico ha provocado la proliferación de toohello de tooprovide un nivel de control de acceso razonable de suscripciones para una inscripción de Azure.

![Controles de acceso basado en rol](./media/governance-in-azure/security-governance-in-azure-fig3.png)

Esta proliferación de suscripciones ya no es necesaria. Con control de acceso basado en roles, puede asignar a usuarios a roles toostandard (por ejemplo, "lectura" comunes y los tipos de "escritor" de roles). También se pueden definir reglas personalizadas.

El [control de acceso basado en rol (RBAC) de Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) permite realizar una administración detallada del acceso en Azure. Usar RBAC, puede conceder únicamente cantidad de Hola de acceso que los usuarios necesitan tooperform sus trabajos. Las empresas orientada a servicios de seguridad deben centrarse en conceder a los empleados que necesitan los permisos exactos Hola. Demasiados permisos exponen un tooattackers de cuenta. Si se conceden muy pocos, los empleados no podrán realizar su trabajo de manera eficaz. Gracias al control de acceso basado en roles (RBAC) de Azure, podrá abordar este problema, ya que es posible realizar una administración avanzada del acceso para Azure. RBAC ayuda toosegregate tareas dentro de su equipo y conceder únicamente Hola una cantidad de toousers de acceso que necesitan tooperform sus trabajos. En lugar de proporcionar a todos los empleados permisos no restringidos en los recursos o la suscripción de Azure, puede permitir solo determinadas acciones.

Por ejemplo, un empleado de uso RBAC toolet administrar máquinas virtuales en una suscripción, mientras que otro puede administrar SQL bases de datos dentro de Hola misma suscripción.

RBAC de Azure tiene tres funciones básicas que se aplican a tipos de recursos de tooall:

- **Propietario** tiene acceso completo tooall recursos incluidos hello toodelegate derecho acceso tooothers.

- **Colaborador** puede crear y administrar todos los tipos de recursos de Azure, pero no se puede conceder acceso tooothers.

- **lector** solo puede ver los recursos existentes de Azure.

rest Hola de roles RBAC hello en Azure que admita la administración de recursos específicos de Azure. Por ejemplo, hello rol Colaborador de máquina Virtual permite toocreate de usuario de Hola y administrar máquinas virtuales. No ofrece su red virtual de acceso toohello o subred Hola Hola máquina virtual se conecta a.

[Funciones integradas de RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) listas Hola roles disponibles en Azure. Especifica las operaciones de Hola y ámbito que cada rol integrado concede toousers.

Conceda el acceso mediante la asignación de hello adecuado RBAC rol toousers, grupos y aplicaciones en un ámbito determinado. ámbito de Hola de una asignación de roles puede ser una suscripción, un grupo de recursos o un único recurso. Un rol asignado en un ámbito primario también concede acceso toohello los elementos secundarios incluidos en él.

Por ejemplo, un usuario con el grupo de recursos de acceso tooa puede administrar todos los recursos de hello contiene, como sitios Web, máquinas virtuales y subredes.

RBAC de Azure solo admite operaciones de administración de recursos de Azure en Hola Hola portal de Azure y las API del Administrador de recursos de Azure. No todas las operaciones de nivel de datos para recursos de Azure pueden autorizarse. Por ejemplo, puede autorizar a alguien toomanage cuentas de almacenamiento, pero no toohello blobs o tablas dentro de una cuenta de almacenamiento no pueden. De forma similar, una base de datos SQL se puede administrar, pero no Hola tablas dentro de él.

Si desea más detalles sobre cómo RBAC ayuda a administrar el acceso, consulte [¿Qué es el control de acceso basado en rol?](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)

También puede [crear un rol personalizado](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) en el Control de acceso de Azure Role-Based (RBAC) si ninguna de las funciones integradas de Hola cumple su acceso específico es necesario. Roles personalizados pueden crearse con [Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell), [interfaz de línea de comandos (CLI) de Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-azure-cli), hello y [API de REST](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-rest). Al igual que las funciones integradas, funciones personalizadas pueden asignarse toousers, grupos y las aplicaciones en la suscripción, el grupo de recursos y ámbitos de recursos.

Dentro de cada suscripción, puede conceder too2000 asignaciones de rol.

## <a name="resource-management"></a>Administración de recursos

Solo el modelo de implementación clásica Hola originalmente había proporcionado por Azure. En este modelo, cada recurso existía independientemente; no había forma de toogroup relacionados con recursos juntos. En su lugar, se tenía toomanually realizar un seguimiento de los recursos que se compone de la solución o aplicación y recuerde toomanage ellas en un planteamiento coordinado.

toodeploy una solución, había tooeither crear cada recurso individualmente a través del portal clásico de Hola o crear una secuencia de comandos que implementan todos los recursos de hello en el orden correcto de Hola. toodelete una solución, había toodelete cada recurso individualmente. No se podía aplicar ni actualizar fácilmente las directivas de control de acceso para los recursos relacionados. Por último, no pudo aplicar etiquetas tooresources toolabel con los términos que le ayudarán a supervisar los recursos y administración la facturación.

En 2014, Azure introdujo al administrador de recursos que agrega el concepto de Hola de un grupo de recursos. Un grupo de recursos es un contenedor para los recursos que comparten un ciclo de vida común. modelo de implementación del Administrador de recursos de Hello ofrece varias ventajas:

- Puede implementar, administrar y supervisar todos los servicios de hello para la solución como un grupo, en lugar de controlar estos servicios individualmente.

- Puede implementar la solución repetidamente a lo largo del ciclo de vida y tener la seguridad de que los recursos se implementan de forma coherente.

- Puede aplicar tooall de control de acceso a recursos en el grupo de recursos y las directivas se aplican automáticamente cuando los recursos nuevos se agregan toohello grupo de recursos.

- Puede aplicar etiquetas tooresources toologically organizar todos los recursos de hello en su suscripción.

- Puede usar la infraestructura de hello toodefine de JavaScript Object Notation (JSON) para su solución. archivo de Hello JSON se conoce como una plantilla de administrador de recursos.

- Puede definir las dependencias de hello entre los recursos, por lo que se implementan en el orden correcto de Hola.

![Administración de recursos](./media/governance-in-azure/security-governance-in-azure-fig4.png)

El Administrador de recursos permite tooput recursos en grupos significativos para la afinidad de facturación o natural de administración. Como se mencionó anteriormente, Azure tiene dos modelos de implementación. En versiones anteriores de hello [modelo clásico](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model), unidad básica de Hola de administración fue suscripción Hola. Era difícil toobreak recursos dentro de una suscripción, que llevó toohello creación de un gran número de suscripciones. Con el modelo del Administrador de recursos de hello, hemos visto Introducción Hola de grupos de recursos.

Un grupo de recursos es un contenedor que almacena los recursos relacionados con una solución de Azure. [grupo de recursos de Hello](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) puede incluir todos los recursos de hello para la solución de hello, o sólo aquellos recursos que desea toomanage como un grupo. Decida cómo desea que los recursos de tooallocate tooresource grupos basan en lo que le resulte hello más conveniente para su organización.

Para más recomendaciones sobre platillas, consulte [Procedimientos recomendados para crear plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

El Administrador de recursos Azure analiza las dependencias de recursos de tooensure se crean en el orden correcto de Hola. Si un recurso se basa en un valor de otro recurso (por ejemplo, una máquina virtual que necesita una cuenta de almacenamiento para los discos), establezca una dependencia.

>[!Note]
>Para obtener más información, consulte [Definición de dependencias en plantillas del Administrador de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-define-dependencies).

También puede usar Hola plantilla de infraestructura de actualizaciones de toohello. Por ejemplo, puede agregar una solución de tooyour de recursos y agregar reglas de configuración para los recursos de Hola que ya estén implementados. Si la plantilla de hello especifica la creación de un recurso pero ese recurso ya existe, el Administrador de recursos de Azure realiza una actualización en lugar de crear un nuevo recurso. Azure Resource Manager actualizaciones Hola existente asset toohello mismo estado tal y como sería como nuevo.

El Administrador de recursos proporciona extensiones para escenarios cuando necesite operaciones adicionales como la instalación de software que no se incluye en el programa de instalación de Hola.

## <a name="resource-tracking"></a>Seguimiento de recursos

Como los usuarios de su organización Agregar suscripción de recursos de toohello, se convierte en recursos tooassociate cada vez más importante con el departamento adecuados de Hola, cliente y entorno. Puede adjuntar tooresources de metadatos a través de las etiquetas. Usa [etiquetas](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) tooprovide información acerca de los recursos de Hola o propietario de Hola. Las etiquetas permiten toonot solo agregado y agrupar los recursos de varias maneras, pero usan esos datos para fines de Hola de anulación.

Utilizar etiquetas cuando tiene un conjunto complejo de grupos de recursos y recursos y necesita toovisualize esos recursos en forma de Hola que le resulte Hola mayoría tooyou de sentido. Por ejemplo, podría etiquetar recursos que no sirven para una función similar en su organización o pertenecen toohello mismo departamento.

Sin etiquetas, los usuarios de su organización pueden crear varios recursos que pueden ser difíciles de toolater identifican y administración. Por ejemplo, podría desear toodelete todos los recursos de Hola para un proyecto. Si no se etiquetan esos recursos para el proyecto de hello, debe encontrarlos manualmente. Etiquetado puede ser un aspecto importante para usted tooreduce costos innecesarios en su suscripción.

Recursos no es necesario tooreside Hola mismo tooshare de grupo de recursos una etiqueta. Puede crear su propios tooensure de taxonomía de etiqueta que todos los usuarios de su organización usan etiquetas comunes en lugar de los usuarios sin darse cuenta aplicar etiquetas ligeramente diferentes (por ejemplo, "departamento" en lugar de "departamento").

Las directivas de recursos permiten toocreate reglas estándar para su organización. Puede crear directivas que se aseguran de recursos se etiquetan con los valores adecuados de Hola.

> [!Note]
> Para más información, consulte [Aplicación de directivas de recursos para etiquetas](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags).

También puede ver recursos etiquetados a través de hello portal de Azure.

Hola [informe de uso de](https://docs.microsoft.com/azure/billing/billing-understand-your-bill) para la suscripción incluye nombres de etiquetas y valores, lo que le permite toobreak los costos por etiquetas.

> [!Note]
> Para obtener más información acerca de las etiquetas, vea [mediante etiquetas tooorganize los recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

Hola siguientes limitaciones aplica tootags:

- Cada recurso o grupo de recursos puede tener un máximo de 15 pares de clave/valor de etiquetas. Esta limitación aplica solo recurso o grupo de recursos de toohello tootags aplicado directamente. Un grupo de recursos puede contener muchos recursos con 15 pares de clave/valor de etiquetas cada uno.

- nombre de etiqueta de Hello es limitado too512 caracteres.

- valor de etiqueta de Hello es limitado too256 caracteres.

- Grupo de recursos de etiquetas aplicadas toohello no son heredadas por recursos hello en ese grupo de recursos.

Si tiene más de 15 valores que necesita tooassociate con un recurso, use una cadena JSON para el valor de etiqueta de Hola. Hola cadena JSON puede contener muchos valores que son la clave de etiqueta única tooa aplicada.

### <a name="tags-and-billing"></a>Etiquetas y facturación

Las etiquetas permiten toogroup los datos de facturación. Por ejemplo, si se ejecutan varias máquinas virtuales para organizaciones diferentes, utilice Hola etiquetas toogroup uso por el centro de costo. También puede utilizar etiquetas toocategorize costos por el entorno de tiempo de ejecución; Hola, como uso de facturación para las máquinas virtuales que se ejecutan en el entorno de producción.

Puede recuperar información acerca de las etiquetas a través de hello [uso de recursos de Azure y RateCard APIs](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) o archivo de valores separados por comas (CSV) de uso de hello. Descargar archivo de uso de hello de hello [portal de cuentas de Azure](https://account.windowsazure.com/) o [portal EA](https://ea.azure.com/).

>[!Note]
> Para obtener más información acerca de la información de toobilling de acceso mediante programación, vea [obtener información sobre el consumo de recursos de Microsoft Azure](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview). Para las operaciones de API de REST, vea [Referencia de API de REST de facturación de Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).

Cuando se descarga el uso de hello CSV para servicios que admiten etiquetas con la facturación, las etiquetas de hello aparecen en la columna de etiquetas de Hola.

## <a name="critical-resource-controls"></a>Controles de recursos críticos

A medida que su organización agrega la suscripción a toohello los servicios principales, se convierte en tooensure cada vez más importante que dichos servicios estén disponibles tooavoid interrupción del negocio. [Bloqueos de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) permiten operaciones de toorestrict en los recursos de gran valor donde modificarlos o eliminarlos tendría un gran impacto en las aplicaciones o la infraestructura de nube. Puede aplicar bloqueos tooa suscripción, el grupo de recursos o el recurso. Normalmente, se aplican bloqueos toofoundational recursos, como redes virtuales y las puertas de enlace, las cuentas de almacenamiento.

Además, en estos momentos, admiten dos valores: CanNotDelete y ReadOnly. CanNotDelete significa que los usuarios (con los derechos adecuados hello) todavía pueden lee o modificar un recurso pero no puede eliminarlo. ReadOnly significa que los usuarios autorizados no pueden eliminar o modificar un recurso.

Bloqueos del Administrador de recursos se aplican solo toooperations que se producen en el plano de administración de hello, que consta de las operaciones enviadas demasiado<https://management.azure.com>. bloqueos hello no restringen cómo recursos realizan sus propias funciones. Los cambios de recursos están restringidos, pero no así las operaciones de recursos. Por ejemplo, un bloqueo de solo lectura en una base de datos de SQL no le permitirá eliminar o modificar la base de datos de hello, pero no impiden crear, actualizar o eliminar datos en la base de datos de Hola.

Aplicar **ReadOnly** puede provocar resultados toounexpected porque algunas operaciones que parezcan como lectura operaciones requieren acciones adicionales. Por ejemplo, colocar una **ReadOnly** bloqueo en una cuenta de almacenamiento impide que todos los usuarios de la lista de claves de Hola. lista de Hello operación de claves se controla a través de una solicitud POST porque Hola devuelve las claves están disponibles para las operaciones de escritura.

![Controles de recursos críticos](./media/governance-in-azure/security-governance-in-azure-fig5.png)

Para obtener otro ejemplo, colocar un bloqueo de solo lectura en un recurso de servicio de aplicaciones evita Explorador de servidores de Visual Studio muestre archivos de recursos de hello porque esa interacción requiere acceso de escritura.

A diferencia de control de acceso basado en roles, se usa administración bloqueos tooapply una restricción a través de todos los usuarios y roles. toolearn acerca de cómo establecer permisos para usuarios y roles, consulte [el Control de acceso basado en roles de Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure).

Cuando se aplica un bloqueo en un ámbito primario, todos los recursos dentro de ese ámbito heredan Hola mismo bloqueo. Incluso los recursos que se agreguen posteriormente heredan bloqueo Hola de hello primario. bloqueo de más restrictivo de Hello en la herencia de hello tiene prioridad.

bloqueos de administración toocreate o delete, debe tener acceso tooMicrosoft.Authorization/ _o Microsoft.Authorization/locks/_ acciones. De hello funciones integradas solo **propietario** y **Administrador de acceso de usuario** se conceden a esas acciones.

## <a name="api-access-toobilling-information"></a>Información de toobilling de acceso de API

Usar datos de uso y los recursos de toopull de las API de facturación de Azure en las herramientas de análisis de datos preferido. Hola, uso de recursos de Azure y RateCard APIs pueden ayudarle a predecir de forma precisa y administrar los costos. Hola API se implementan como un proveedor de recursos y la parte de la familia de Hola de API que expone hello Azure Resource Manager.

### <a name="azure-resource-usage-api-preview"></a>API de uso de recursos de Azure (versión preliminar)

Hola utilice Azure [API de uso de recursos](https://msdn.microsoft.com/library/azure/mt219003) tooget los datos de consumo de Azure estimado. Hola API incluye:

- **Control de acceso basada en roles de Azure** -configurar el acceso de directivas en hello [portal de Azure](https://portal.azure.com/) o a través [cmdlets de PowerShell de Azure](https://docs.microsoft.com/powershell/azure/overview) toospecify aplicaciones o que los usuarios puede obtener acceso datos de uso de la suscripción de toohello. Los autores de llamadas deben utilizar tokens de Azure Active Directory estándar para la autenticación. Agregar Hola llamador tooeither Hola lector de facturación, lector, propietario o Colaborador rol tooget acceso toohello datos de uso para una suscripción de Azure específica.

- **Agregaciones cada hora o diarias** : los autores de llamadas pueden especificar si desean sus datos de uso de Azure en depósitos cada hora o diarios. valor predeterminado de Hello es diaria.

- **Metadatos de la instancia (incluye las etiquetas del recurso)** : obtener detalles de nivel de instancia como Hola uri de recurso completo (/ subscriptions / {Id. de suscripción} /..), Hola información del grupo de recursos y las etiquetas del recurso. Estos metadatos le ayuda a determinista y asignar mediante programación el uso por etiquetas de hello, para casos de uso como carga entre.

- **Metadatos de recursos** -detalles de recursos como nombre de medidor de hello, medidor de la categoría, subcategoría de medidor, unidad y región permiten llamador Hola una mejor comprensión de lo que se consumió. También estamos trabajando terminología de metadatos de recursos tooalign en hello portal de Azure, Azure uso CSV, CSV, de facturación de EA y otras experiencias de acceso público, toolet correlacionar los datos a través de experiencias.

- **Uso para todos los tipos de ofertas**: los datos de uso están disponibles para todos los tipos de ofertas, incluidos el pago por uso, MSDN, compromiso monetario, crédito monetario y EA.

**API de RateCard de recursos de Azure (versión preliminar)**

Use hello Azure recursos RateCard API tooget Hola lista disponibles de recursos de Azure y estimado información sobre precios de cada uno de ellos. Hola API incluye:

- **Control de acceso basado en roles Azure** : configurar las directivas de acceso en hello portal de Azure o a través de toospecify de cmdlets de PowerShell de Azure que los usuarios o aplicaciones pueden obtener acceso a los datos de RateCard toohello. Los autores de llamadas deben utilizar tokens de Azure Active Directory estándar para la autenticación. Agregar Hola llamador tooeither Hola lector, el propietario o Colaborador rol tooget acceso toohello datos de uso para una suscripción de Azure.

- **Compatibilidad con ofertas de pago por uso, MSDN, compromiso monetario y crédito monetario (no compatible con EA)**: esta API proporciona información de tarifas de nivel de oferta de Azure. autor de llamada de Hola de esta API debe pasar las tasas y detalles de tooget información del recurso de la oferta de Hola. Estamos tasas EA tooprovide actualmente no es posible porque EA ofertas han personalizado las tasas por la inscripción. Estos son algunos de los escenarios de Hola que son posibles con combinación de Hola de uso de Hola y Hola RateCard APIs:

- **Azure gastará durante el mes de hello** -combinación de Hola de uso de hello uso y RateCard APIs tooget una mejor percepción en la nube dedicar durante los meses de Hola. Puede analizar Hola cada hora y las estimaciones de depósitos diarias de uso y carga.

- **Configurar alertas** : usar hello uso y hello tooget RateCard APIs estimación de consumo de la nube y los cargos y configurar alertas basada en moneda o basada en recursos.

- **Predecir factura** : Get su consumo estimado y la nube invierte y aplican toopredict algoritmos de aprendizaje qué factura Hola sería final Hola de hello ciclo de facturación automático.

- **Consumo previo análisis de costos** : usar Hola API RateCard toopredict sería la cantidad de la factura para su uso esperado cuando se mueve el tooAzure de las cargas de trabajo. Si tiene cargas de trabajo existentes en otras nubes o nubes privadas, también se puede asignar su uso con hello Azure tasas tooget dedique una mejor estimación de Azure. Esto deja de estimación Hola toopivot de capacidad en la oferta y comparar entre tipos de oferta distintos de hello más allá de pago por uso, como un compromiso monetario y crédito monetario. Hola API también le ofrece Hola capacidad toosee costo diferencias por región y permitiéndole toodo un toohelp de análisis de hipótesis costo tomar decisiones de implementación.

- **Análisis de escenarios condicionales** -puede determinar si es más cargas de trabajo de toorun rentable en otra región o en otra configuración del programa Hola a recursos de Azure. Recursos de Azure los costos pueden diferir según Hola región de Azure que está usando.

- También puede determinar si otro tipo de oferta de Azure ofrece una mejor tarifa en un recurso de Azure.

## <a name="networking-controls"></a>Controles de red

Tooresources de acceso pueden ser internos (dentro de la red de organización de hello) o externos (a través de internet de Hola). Es fácil para los usuarios en sus organización tooinadvertently put recursos en lugar de hello incorrecto y posiblemente abrirlos toomalicious acceso. Al igual que con forma local o dispositivos, las empresas deben agregar tooensure controles adecuados que Azure a los usuarios tomar decisiones correctas de Hola.

![Controles de red](./media/governance-in-azure/security-governance-in-azure-fig6.png)

Para el gobierno de suscripciones, identificamos los recursos principales que proporcionan un control de acceso básico. recursos principales de Hello constan de:

### <a name="network-connectivity"></a>Conectividad de red

Las [redes virtuales](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) son objetos de contenedor de las subredes. Aunque no es estrictamente necesario, a menudo se usa al conectarse a recursos corporativos de aplicaciones toointernal. Hola habilita de servicio de red Virtual de Azure toosecurely conectar otro tooeach de recursos de Azure con redes virtuales (redes virtuales).

Una red virtual es una representación de su propia red en la nube de Hola. Una red virtual es un aislamiento lógico de hello nube de Azure dedicada tooyour suscripción. También puede conectar la red local de tooyour de redes virtuales.

A continuación, se muestran las funcionalidades de las redes virtuales de Azure:

- **Aislamiento**: las redes virtuales están completamente aisladas entre sí. Puede crear redes virtuales independientes para el desarrollo, pruebas y producción ese Hola use bloques de direcciones CIDR mismo. Por el contrario, puede crear varias redes virtuales que usan diferentes bloques de direcciones CIDR y que conectan redes entre sí. También puede segmentar una red virtual en varias subredes. Azure proporciona resolución de nombres interna para las máquinas virtuales y las instancias de rol de servicios de nube conectado tooa red virtual. Opcionalmente puede configurar una red virtual toouse sus propios servidores DNS, en lugar de utilizar la resolución de nombres interna Azure.

- **Conectividad a Internet**: instancias de rol de todas las máquinas virtuales (VM) de Azure y servicios en la nube conectado tooa red virtual tiene acceso a toohello Internet, de forma predeterminada. También puede habilitar recursos de toospecific de acceso de entrada, según sea necesario.

- **Conectividad de los recursos de Azure**: recursos de Azure como servicios en la nube y máquinas virtuales pueden ser toohello conectado misma red virtual. los recursos de Hello pueden conectarse tooeach otro uso privado de direcciones IP, incluso si están en subredes diferentes. Azure proporciona el enrutamiento predeterminado entre subredes, las redes virtuales y redes locales, por lo que no tiene tooconfigure y administrar rutas.

- **Conectividad de red virtual**: redes virtuales pueden ser conectado tooeach otros, habilitar recursos conectado tooany toocommunicate de red virtual con cualquier recurso de cualquier otra red virtual.

- **Conectividad local**: redes virtuales pueden ser redes de local tooon conectado a través de conexiones de red privada entre la red y Azure, o a través de una conexión de VPN de sitio a sitio a través de Internet de Hola.

- **Filtrado de tráfico**: el tráfico de red de entrada y salida de las instancias de rol de Cloud Services y las máquinas virtuales se puede filtrar por dirección IP y puerto de origen, dirección IP y puerto de destino, y por protocolo.

- **Enrutamiento**: de manera opcional, puede invalidar el enrutamiento predeterminado de Azure mediante la configuración de sus propias rutas, o bien utilizando rutas BGP a través de una puerta de enlace de red.

## <a name="network-access-controls"></a>Controles de acceso a la red

[Grupos de seguridad de red](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) son similares a un servidor de seguridad y proporcionar reglas para cómo un recurso puede "hablar" a través de red de Hola. Proporciona un control granular sobre cómo ni Hola mismo si una subred (o la máquina virtual) se pueden conectar toohello Internet u otras subredes en red virtual.

Un grupo de seguridad de red (NSG) contiene una lista de reglas de seguridad que permiten o deniegan tooresources de tráfico de red conectados a redes virtuales tooAzure (VNet). Los NSG pueden ser toosubnets asociado, máquinas virtuales individuales (clásico), o interfaces de red individuales (NIC) adjunta tooVMs (Administrador de recursos).

Cuando un NSG está asociado tooa subred, Hola reglas aplican tooall recursos toohello conectado subred. Tráfico puede restringir aún más mediante la asociación también un tooa NSG VM o NIC.

## <a name="security-and-continuous-compliance-with-organizational-standards"></a>Seguridad y cumplimiento continuo con las normas de las organizaciones

Cada empresa tiene necesidades distintas y todas obtendrán diferentes ventajas de las soluciones en la nube. No obstante, los clientes de todos los tipos tienen Hola mismas preocupaciones básicas acerca de cómo mover toohello en la nube. Desean tooretain control de sus datos, y desean que toobe de datos mantiene segura y privada, al tiempo que mantiene la transparencia y cumplimiento de normas.

Esto es lo que buscan los clientes de un proveedor de nube:

- **Proteger nuestros datos** mientras la confirmación de que puede proporcionar en la nube Hola mayor seguridad de los datos y control administrativo, líderes de TI todavía se refiere a que en la nube toohello migrar ellos dejará toohackers más vulnerables a su actual soluciones internas.

- **Mantener la privacidad de los datos**: los servicios en la nube privada conllevan desafíos específicos para las empresas en materia de privacidad. Como las empresas buscar toohello en la nube toosave en los costos de infraestructura y mejoran su flexibilidad, también preocuparse perder el control de donde se almacenan sus datos, que tiene acceso a ella y cómo se usa.

- **Nos ofrecen control** incluso a medida sacan partido de hello en la nube toodeploy más soluciones innovadoras, compañías preocupan perder el control de sus datos. divulgaciones reciente Hola de acceso a datos del cliente, a través de medios legales y muy legales, los organismos gubernamentales realizar algunas CIO precavido a la hora de almacenar sus datos en la nube de Hola.

- **Fomentar la transparencia** aunque seguridad, privacidad y control son responsables de toobusiness importante, también desean capacidad hello tooindependently comprobar cómo sus datos se almacenan, se accede y segura.

- **Mantener el cumplimiento de** a medida que las empresas amplían el uso de tecnologías de nube, complejidad de Hola y el ámbito de las normas y reglas siguen tooevolve. Las empresas necesitan tooknow que se cumplirá los estándares de cumplimiento normativo y ese cumplimiento evolucionará como normativa cambian con el tiempo.

## <a name="security-configuration-monitoring-and-alerting"></a>Configuración, supervisión y alertas de seguridad

Los suscriptores de Azure pueden administrar sus entornos de nube desde diversos dispositivos, incluidas estaciones de trabajo de administración, equipos de desarrollador e incluso dispositivos de usuario final con privilegios que tengan permisos específicos para la tarea. En algunos casos, las funciones administrativas se realizan a través de consolas basadas en web como Hola portal de Azure. En otros casos, puede haber tooAzure conexiones directas desde sistemas locales a través de redes privadas virtuales (VPN), servicios de Terminal Server, protocolos de aplicaciones de cliente o (mediante programación) hello API de administración de servicio de Azure (SMAPI). Además, los puntos de conexión de cliente pueden estar unidos a un dominio o aislados y no administrados, como tabletas o smartphones.

Aunque varias capacidades de administración y acceso proporcionan un amplio conjunto de opciones, esta variabilidad puede agregar la implementación en la nube tooa riesgo significativo. Puede ser difícil toomanage, realizar un seguimiento y auditar las acciones administrativas. Esta variabilidad también puede presentar las amenazas de seguridad a través de extremos de tooclient de acceso no reguladas que se usan para administrar servicios en la nube. El uso de estaciones de trabajo personales o generales para desarrollar y administrar infraestructuras abre la puerta a amenazas impredecibles que se producen tanto en la exploración web (por ejemplo, ataques a los sitios web más utilizados) como en el correo electrónico (tales como ingeniería social y suplantación de identidad [phishing]).

Supervisión, registro y auditoría de proporcionan una base para el seguimiento y la descripción de las actividades administrativas, pero puede que no siempre sea factible tooaudit todas las acciones en completar detalle debido toohello cantidad de datos generado. Eficacia de Hola Hola de directivas de administración de auditoría es un procedimiento recomendado, sin embargo.

Seguridad de Azure regulación de AD DS GPO toocontrol interfaces de Windows de todos los administradores de hello, como el uso compartido de archivos. Incluya las estaciones de trabajo de administración de procesos de auditoría, supervisión y registro. Realice un seguimiento del acceso y uso de los administradores y programadores.

### <a name="azure-security-center"></a>Azure Security Center

Hola [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) proporciona una vista central de estado de seguridad de Hola de recursos en las suscripciones de Hola y se ofrecen recomendaciones que le ayudan a evitar que los recursos en peligro. Pueden habilitar directivas más granulares (por ejemplo, aplicar directivas toospecific grupos de recursos que permiten su riesgo de toohello de posición que se dirección de hello enterprise tootailor).

![Azure Security Center](./media/governance-in-azure/security-governance-in-azure-fig7.png)

Security Center proporciona funcionalidades de administración de directivas y supervisión de la seguridad integradas en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad. Después de habilitar [las directivas de seguridad](https://docs.microsoft.com/azure/security-center/security-center-policies) para obtener recursos de una suscripción, el centro de seguridad analiza la seguridad de Hola de sus tooidentify posibles vulnerabilidades de recursos. La información acerca de la configuración de la red está disponible de inmediato.

Azure Security Center representa una combinación de procedimientos recomendados, análisis y administración de directivas de seguridad para todos los recursos de una suscripción de Azure. Esta herramienta eficaz y fácil de toouse permite a los equipos de seguridad y tooprevent los responsables de riesgo, detectar y responder toosecurity amenazas como automáticamente recopila y analiza los datos de seguridad de los recursos de Azure, red de Hola y soluciones de socios comerciales, como los programas antimalware y firewalls.

Además, el centro de seguridad de Azure se aplica análisis avanzado, incluido el aprendizaje automático y análisis del comportamiento aprovechando la inteligencia de amenazas globales de hello productos y servicios, Hola Microsoft Digital crímenes unidad (DCU), Microsoft Microsoft Security Response Center (MSRC) y las fuentes externas. [Controles de seguridad](https://www.credera.com/blog/credera-site/azure-governance-part-4-other-tools-in-the-toolbox/) pueden aplicarse ampliamente en nivel de suscripción de Hola o reduce toospecific, requisitos granular aplicados tooindividual recursos a través de la definición de la directiva.

Por último, Azure Security Center analiza el estado de seguridad de recursos en función de esas directivas y utiliza este paneles de detalle de tooprovide e intentos de alertas para eventos como la detección de malware o conexión de IP malintencionada.

>[!Note]
> Para obtener más información acerca de cómo obtener recomendaciones tooapply, leer [implementar recomendaciones de seguridad en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-recommendations).

Centro de seguridad recopila datos de sus máquinas virtuales tooassess su estado de seguridad, proporcionar recomendaciones de seguridad y alerta toothreats. La primera vez que se accede al Centro de seguridad la recopilación de datos se habilita en todas las máquinas virtuales de la suscripción. Se recomienda utilizar el conjunto de datos, pero puede cancelar voluntariamente por [deshabilitar la recopilación de datos](https://docs.microsoft.com/azure/security-center/security-center-faq) Hola directiva de centro de seguridad.

Por último, el centro de seguridad de Azure es una plataforma abierta que permite a los socios de Microsoft y software de toocreate de proveedores de software independientes que se conecta a Azure Security Center tooenhance sus capacidades.

Centro de seguridad de Azure supervisa hello Azure recursos siguientes:

- Máquinas virtuales (se incluye Cloud Services)

- Redes virtuales de Azure

- Servicio de SQL Azure

- Soluciones de asociados integradas en la suscripción de Azure, como un firewall de aplicaciones web en las máquinas virtuales y en [App Service Environment](https://docs.microsoft.com/azure/app-service/app-service-app-service-environments-readme)

### <a name="operations-management-suite"></a>Operations Management Suite

Hola de desarrollo de software OMS y seguridad de la información del equipo de servicio y [programa de gobernanza](https://github.com/Microsoft/azure-docs/blob/master/articles/log-analytics/log-analytics-security.md) es compatible con sus requisitos empresariales y cumple las normativas y toolaws tal y como se describe en [Microsoft Azure Trust Center ](https://azure.microsoft.com/support/trust-center/) y [compatibilidad del centro de confianza de Microsoft](https://www.microsoft.com/TrustCenter/Compliance/default.aspx). En estas páginas también se describe cómo OMS establece los requisitos de seguridad, identifica los controles de seguridad, y administra y supervisa los riesgos. Cada año, revisamos las directivas, los estándares, los procedimientos y las instrucciones.

Cada miembro del equipo de desarrollo de OMS recibe cursos formales sobre seguridad de aplicaciones. Internamente, utilizamos un sistema de control de versiones para el desarrollo de software. Cada proyecto de software está protegido por el sistema de control de versiones de Hola.

Microsoft cuenta con un equipo de seguridad y cumplimiento normativo que supervisa y evalúa todos los servicios de Microsoft. Los responsables de seguridad de información constituyen equipo hello y no están asociados con hello ingeniería departamentos que desarrollar OMS. los responsables de seguridad Hola tienen su propia cadena de administración y realizar evaluaciones independientes de productos y la seguridad de tooensure de servicios y la conformidad.

Operations Management Suite (también conocido como OMS) es una colección de servicios de administración que se diseñaron en nube de Hola desde el inicio de Hola. En lugar de implementar y administrar recursos locales, los componentes de OMS se hospedan en su totalidad en Azure. La configuración es mínima, y puede estar listo y rindiendo literalmente en cuestión de minutos.

![Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig8.png)

Solo porque servicios OMS se ejecutan en nube de hello no significa que no se puede administrar eficazmente el entorno local.

Colocar a un agente en todas las ventanas o equipo de Linux en su centro de datos y enviará tooLog de datos donde se pueden analizar junto con todos los demás datos de análisis recopilados desde la nube o en los servicios locales. Usar copia de seguridad de Azure y Azure Site Recovery tooleverage hello en la nube para la copia de seguridad y alta disponibilidad para en recursos locales.

Runbooks de nube de hello normalmente no puede acceder a los recursos locales, pero puede instalar un agente en uno o más equipos demasiado que va a hospedar runbooks en su centro de datos. Cuando se inicia un runbook, simplemente especifique si desea toorun en nube de Hola o en un trabajo local.

un conjunto de servicios que se ejecutan en Azure proporciona funcionalidad básica de Hola de OMS. Cada servicio proporciona una función de administración específico y puede combinar escenarios de administración diferente de tooachieve de servicios.

![Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig9.JPG)

Operations Manager de Azure amplía sus funcionalidades proporcionando soluciones de administración. Las [soluciones de administración](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) son conjuntos de lógica preempaquetados que implementan un escenario de administración concreto aprovechando uno o varios servicios de OMS.

![Operations Manager de Azure](./media/governance-in-azure/security-governance-in-azure-fig10.png)

Diferentes soluciones están disponibles de Microsoft y de asociados de negocios que puede agregar fácilmente tooyour suscripción de Azure tooincrease Hola valo su inversión de OMS.

Como partner, puede crear su propias soluciones toosupport sus aplicaciones y servicios y proporcionarlos toousers a través de hello Azure Marketplace o plantillas de inicio rápido.

## <a name="performance-alerting-and-monitoring"></a>Supervisión y alertas de rendimiento

### <a name="alerting"></a>Alertas

Las alertas son un método de supervisión de los registros, los eventos o las métricas de recursos de Azure, con la intención de recibir una notificación cuando una condición especificada se cumple.

**Alertas en los distintos servicios de Azure**

Las alertas están disponibles en los diferentes servicios, incluidos:

- Application Insights: admite las alertas de métricas y pruebas web.

>[!Note]
> Vea [Definición de alertas en Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-alerts) y [Supervisión de la disponibilidad y la capacidad de respuesta de cualquier sitio web](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability).

- Análisis de registros (Operations Management Suite): Habilita el enrutamiento del Hola de actividad y registros de diagnóstico tooLog análisis. Operations Management Suite permite métrica, registro y otros tipos de alerta.

>[!Note]
> Para obtener más información, consulte la sección Alertas de [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts).

- Azure Monitor: admite alertas basadas en valores de métricas y en eventos de registro de actividades. Puede usar hello [API de REST de Azure Monitor](https://msdn.microsoft.com/library/dn931943.aspx) toomanage alertas.

>[!Note]
> Para obtener más información, consulte [mediante Hola portal de Azure, PowerShell o las alertas de toocreate de interfaz de línea de comandos de hello](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal).

### <a name="monitoring"></a>Supervisión

Los problemas de rendimiento de la aplicación en la nube pueden afectar a su negocio. Con varios componentes interconectados y versiones frecuentes, las degradaciones pueden ocurrir en cualquier momento. Y si va a desarrollar una aplicación, los usuarios normalmente se encontrarán con problemas que no se han detectado durante las pruebas. Debe saber acerca de estos problemas de inmediato y dispone de herramientas para diagnosticar y solucionar problemas de Hola. Microsoft Azure tiene una gama de herramientas para identificar estos problemas.

**¿Cómo puedo supervisar mis aplicaciones en la nube de Azure?**

Hay una gama de herramientas para la supervisión de servicios y aplicaciones de Azure. Algunas de sus características se superponen. Se trata en parte por motivos históricos y en parte debido toohello desenfoque entre el desarrollo y el funcionamiento de una aplicación.

Estos son herramientas principales de hello:

- **Azure Monitor** es una herramienta básica para la supervisión de servicios que se ejecutan en Azure. Proporciona datos de nivel de la infraestructura sobre rendimiento Hola de un servicio y Hola que rodea el entorno. Si va a administrar las aplicaciones en Azure, decida si tooscale hacia arriba o hacia abajo de recursos, a continuación, Monitor de Azure ofrece lo que usa toostart.

- **Application Insights** puede utilizarse para el desarrollo y como una solución de supervisión de producción. Funciona mediante la instalación de un paquete en la aplicación y, por tanto, ofrece una perspectiva más interna de lo que está sucediendo. Los datos incluyen tiempos de respuesta de dependencias, seguimientos de excepciones, instantáneas de depuración y perfiles de ejecución. Proporciona herramientas inteligentes eficaces para analizar todos los esta telemetría ambos toohelp depurar una aplicación y toohelp entender lo que hacen los usuarios con él. Puede saber si un pico en tiempos de respuesta es due toosomething en una aplicación o algún problema de recursos externo. Si utiliza Visual Studio y aplicación hello es erróneo, se pueden tomar toohello derecho problema las líneas de código para que pueda corregirlos.

- **Análisis de registros** está destinado a aquellos que necesitan tootune rendimiento y plan de mantenimiento en aplicaciones que se ejecutan en producción. Se basa en Azure. Recopila y agrega los datos de muchos orígenes, aunque con un retraso de 10 minutos de too15. Proporciona una solución integral de administración de TI para Azure, entornos locales e infraestructuras de terceros basadas en la nube (por ejemplo, Amazon Web Services). Proporciona herramientas más enriquecidas tooanalyze datos a través de varios orígenes, permite que las consultas más complejas a través de todos los registros y proactivamente pueden emitir alertas en las condiciones especificadas. Incluso puede recopilar datos personalizados en su repositorio central para que pueda consultarlos y visualizarlos.

- **System Center Operations Manager (SCOM)** está diseñado para administrar y supervisar grandes instalaciones de la nube. Es posible que ya esté familiarizado con esta solución como una herramienta de administración para nubes locales basadas en Windows Sever e Hyper-V, pero también se puede integrar con aplicaciones de Azure y administrarlas. Entre otras cosas, puede instalar Application Insights en las aplicaciones dinámicas existentes. Si una aplicación deja de funcionar, se lo notifica en cuestión de segundos.


## <a name="next-steps"></a>Pasos siguientes

- [Procedimientos recomendados para crear plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)

- [Ejemplos de implementación de un sistema de gobierno de suscripciones de Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-examples)

- [Microsoft Azure Government](https://docs.microsoft.com/azure/azure-government/)
