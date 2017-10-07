---
title: aaaDesign Azure plantillas con soluciones complejas | Documentos de Microsoft
description: "Muestra los procedimientos recomendados para diseñar plantillas de Azure Resource Manager para escenarios complejos"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ce1141d6-ece7-4976-acea-1db1f775409e
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: aa45e9a46d79a6336b696cff8fd37f65fa449f11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-azure-resource-manager-templates-when-deploying-complex-solutions"></a>Diseño de patrones para plantillas de Azure Resource Manager cuando implementa soluciones complejas
Con un enfoque flexible basado en plantillas de Azure Resource Manager, puede implementar topologías complejas de forma rápida y coherente. Puede adaptar estas implementaciones fácilmente como variantes de tooaccommodate para escenarios de valores atípicos o clientes o core evolucionan ofertas.

Este tema forma parte de un artículo más extenso. Hola tooread completa papel, descargue [clase Azure recursos el Administrador de plantillas de consideraciones y prácticas comprobadas](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

Las plantillas combinan ventajas Hola de hello subyacente Azure Resource Manager con capacidad de adaptación de Hola y mejorar la legibilidad de JavaScript Object Notation (JSON). El uso de plantillas le permite:

* Implementar topologías y sus cargas de trabajo de forma coherente.
* Administrar juntos todos los recursos de una aplicación mediante grupos de recursos.
* Aplicar servicios, grupos y toousers de acceso basado en roles (RBAC) control toogrant acceso adecuado.
* Usar tareas de toostreamline asociaciones etiquetado como paquetes acumulativos de facturación.

Este artículo proporciona información detallada sobre escenarios de consumo, arquitectura y patrones de implementación identificados durante nuestras sesiones de diseño e implementaciones de plantillas reales con los clientes del equipo de asesoría de clientes de Azure (AzureCAT). Lejos de academic, estos métodos se ha comprobado prácticas informadas por desarrollo Hola de plantillas para el 12 de tecnologías de hello principales sistemas operativos basados en Linux, incluyendo: Apache Kafka, Apache Spark, Cloudera, Couchbase, Hortonworks HDP, Enterprise DataStax con la tecnología Apache Casandra, Elasticsearch, Jenkins, MongoDB, PostgreSQL, Redis y Nagios. 

Este artículo comparte estos toohelp prácticas demostradas diseñar plantillas de Azure Resource Manager de clase mundial.  

En nuestro trabajo con los clientes, hemos identificado varias experiencias de consumo de plantillas de Resource Manager en empresas, integradores de sistemas y proveedores de soluciones en la nube. Hello secciones siguientes proporcionan información general de escenarios y patrones comunes para distintos tipos de clientes.

## <a name="enterprises-and-system-integrators"></a>Empresas e integradores de sistemas
En las grandes organizaciones, observamos normalmente dos consumidores de plantillas de Resource Manager: los equipos de desarrollo de software internos y los grupos de TI corporativos. Hemos observado que los escenarios de Hola para hello SIs asignan toohello escenarios para las empresas, Hola por lo que se aplican las mismas consideraciones.

### <a name="internal-software-development-teams"></a>Equipos de desarrollo de software internos
Si su equipo desarrolla software toosupport su negocio, las plantillas proporcionan una manera fácil tooquickly implementar tecnologías para su uso en soluciones empresariales específicas. También puede utilizar plantillas toorapidly crear entornos de entrenamiento que permiten los conocimientos necesarios de toogain de los miembros de equipo.

Puede utilizar plantillas como-es ampliar o combinarlos tooaccommodate sus necesidades. El uso de etiquetado dentro de las plantillas permite proporcionar un resumen de facturación con diversas vistas como equipo, proyecto, individuo y educación.

A menudo, las empresas desean toocreate los equipos de desarrollo de software una plantilla para la implementación coherente de una solución. plantilla de Hello facilita las restricciones para que determinados elementos dentro de ese entorno permanecen fijas y no se puede invalidar. Por ejemplo, un banco puede requerir un tooinclude plantilla RBAC por lo que un programador no puede revisar una solución de banca cuenta de almacenamiento personal de toosend datos tooa.

### <a name="corporate-it"></a>Grupos de TI corporativos
Las organizaciones de TI corporativa suelen usar plantillas para ofrecer capacidad en la nube y funcionalidades hospedadas en la nube.

#### <a name="cloud-capacity"></a>Capacidad en la nube
Es una manera común de corporativa TI grupos tooprovide capacidad de la nube para que los equipos con "tamaños de camiseta", que son estándar oferta tamaños como pequeñas, medianas y grandes. ofertas de Hello camiseta tamaño pueden mezclar distintos tipos de recursos y las cantidades y proporcionan un nivel de estandarización que hace posible toouse plantillas. plantillas de Hello ofrecen una capacidad de una manera coherente que aplica las directivas corporativas y usa las organizaciones tooconsuming de anulación de etiquetado tooprovide.

Por ejemplo, puede que necesite tooprovide desarrollo, prueba o entornos de producción dentro de qué Hola los equipos de desarrollo de software pueden implementar sus soluciones. entorno de Hello tiene una topología de red predefinida y no se pueden cambiar elementos que Hola los equipos de desarrollo de software, como las reglas que rigen el acceso toohello internet y paquete inspección pública. También puede tener funciones específicas de la organización para estos entornos con derechos de acceso para el entorno de Hola.

#### <a name="cloud-hosted-capabilities"></a>Funcionalidades hospedadas en la nube
Puede utilizar plantillas toosupport hospedada en la nube funciones, incluidos los paquetes de software individuales o compuestas ofertas que se ofrecen toointernal líneas de negocios. Un ejemplo de una oferta compuesta sería el análisis como servicio: análisis, visualización y otras tecnologías, proporcionado en una configuración optimizada y conectada en una topología de red predefinida.

Capacidades hospedada en la nube se ven afectadas por hello consideraciones de seguridad y roles establecidas por la capacidad de la nube de hello oferta en que están integradas. Estas funcionalidades se ofrecen tal y como están o como un servicio administrado. Para este último de hello, son necesarios los roles de restricción de acceso tooenable acceso en el entorno de Hola para fines de administración.

## <a name="cloud-service-vendors"></a>Proveedores de servicios en la nube
Después de hablar toomany CSV, hemos identificado varios enfoques que puede realizar toodeploy servicios para sus clientes y los requisitos asociados.

### <a name="csv-hosted-offering"></a>Oferta hospeda por el CSV
Si hospeda su oferta en su propia suscripción de Azure, dos son los enfoques de hospedaje más comunes: realizar una implementación distinta para cada cliente o implementar unidades de escalado que respalden una infraestructura compartida usada para todos los clientes.

* **Implementaciones distintas para cada cliente.** Las implementaciones distintas por cliente requieren topologías fijas de diferentes configuraciones conocidas. Dichas implementaciones pueden tener diferentes tamaños de máquinas virtuales, un número variable de nodos y distintas cantidades de almacenamiento asociado. El etiquetado de las implementaciones se usa en el resumen de facturación de cada cliente. RBAC puede ser habilitado tooallow tooaspects de acceso de los clientes de su entorno de nube.
* **Unidades de escalado en entornos multiempresa compartidos.** Una plantilla puede representar una unidad de escalado en entornos multiempresa. Hola en este caso, la misma infraestructura es toosupport usado todos los clientes. las implementaciones de Hello representan un grupo de recursos que ofrecen un nivel de capacidad para hello hospedada que ofrece, como el número de usuarios y el número de transacciones. Estas unidades de escalado se aumentan o disminuyen según exija la demanda.

### <a name="csv-offering-injected-into-customer-subscription"></a>Oferta de CSV insertada en la suscripción del cliente
Puede que desee toodeploy el software en las suscripciones poseídas por los clientes finales. Puede utilizar distintas implementaciones de toodeploy de plantillas en la cuenta de Azure de un cliente.

Estas implementaciones utilizan RBAC para que pueda actualizar y administrar la implementación de hello dentro de la cuenta del cliente de Hola.

### <a name="azure-marketplace"></a>Azure Marketplace
tooadvertise y vender sus ofertas a través de un mercado, como Azure Marketplace, es posible desarrollar plantillas toodeliver distintos tipos de implementaciones que se ejecutan en la cuenta de Azure de un cliente. Estas distintas implementaciones pueden describirse normalmente como una talla de camiseta (pequeña, mediana, grande), el tipo de producto/público (comunidad, desarrollador, empresa) o el tipo de característica (básica, alta disponibilidad).  En algunos casos, estos tipos permiten toospecify determinados atributos de implementación de hello, como tipo de máquina virtual o el número de discos.

## <a name="oss-projects"></a>Proyectos de software de código abierto
Dentro de los proyectos de código abierto, plantillas de administrador de recursos permiten a una comunidad toodeploy una solución rápidamente mediante prácticas demostradas. Puede almacenar plantillas en un repositorio de GitHub para que la Comunidad de hello puede modificar con el tiempo. Los usuarios implementan estas plantillas en sus propias suscripciones de Azure.

Hello secciones siguientes identifican aspectos Hola necesita tooconsider antes de diseñar la solución.

## <a name="identifying-what-is-outside-and-inside-a-vm"></a>Identificación de lo que está dentro y fuera de una máquina virtual
Al diseñar la plantilla, resulta útil toolook en requisitos de hello en cuanto a lo que está fuera y dentro de hello las máquinas virtuales (VM):

* Exterior significa Hola máquinas virtuales y otros recursos de la implementación, como la topología de red de hello, etiquetado, referencias toohello certificados/secretos y control de acceso basado en roles. Todos estos recursos forman parte de la plantilla.
* Inside significa Hola software instalado y general deseado estado de configuración. Otros mecanismos, como extensiones de máquina virtual o scripts, se usan en su totalidad o en parte. Estos mecanismos pueden identificarse y ejecutados por plantilla de hello, pero no están en él.

Algunos ejemplos comunes de actividades "dentro del cuadro de Hola" incluiría:  

* Instalar o quitar características y roles de servidor
* Instalar y configurar el software en el nivel de nodo o el clúster de Hola
* Implementar sitios web en un servidor web
* Implementar esquemas de base de datos
* Administrar el Registro u otros tipos de valores de configuración
* Administrar archivos y directorios
* Iniciar, detener y administrar procesos y servicios
* Administrar cuentas de usuario y grupos locales
* Instalar y administrar paquetes (.msi, .exe, yum, etc.).
* Administrar variables de entorno
* Ejecutar scripts nativos (Windows PowerShell, bash, etc.)

### <a name="desired-state-configuration-dsc"></a>Configuración de estado deseado (DSC)
Pensar en estado interno de Hola de las máquinas virtuales más allá de la implementación, desea toomake seguro esta implementación no "desfase" de configuración de Hola que ha definido y protegido en el control de código fuente. Este enfoque garantiza que los desarrolladores o personal de operaciones no realiza el entorno de tooan de cambios ad hoc que no están puestas a prueba, probado o se registran en el control de código fuente. Este control es importante, porque los cambios manuales hello no están en control de código fuente. También no son parte de la implementación estándar de Hola y afectará a futuras implementaciones automatizadas de software de Hola.

Dejando a un lado los empleados internos, la configuración de estado deseado también es importante desde el punto de vista de la seguridad. Los piratas informáticos con regularidad están tratando de toocompromise y sistemas de software de vulnerabilidad de seguridad. Cuando se realiza correctamente, se archivos tooinstall comunes y se cambian Hola estado de un sistema en peligro. Utilizar la configuración de estado deseado, puede identificar diferencias entre Hola deseado y el estado real y restaurar una configuración conocida.

Existen extensiones de recursos hello más populares mecanismos para DSC - PowerShell DSC, Chef y Puppet. Cada una de estas extensiones puede implementar el estado inicial de saludo de la máquina virtual y también ser utilizado toomake seguro Hola deseado se mantiene el estado.

## <a name="common-template-scopes"></a>Ámbitos comunes de plantillas
En nuestra experiencia, hemos asistido al surgimiento de tres ámbitos de plantillas de soluciones principales. Estos tres ámbitos: capacidad, la capacidad y solución end-to-end: se describen en las secciones siguientes de Hola.

### <a name="capacity-scope"></a>Ámbito de capacidad
Un ámbito de capacidad ofrece un conjunto de recursos en una topología estándar que está preconfigurado toobe conforme a los Reglamentos y directivas. ejemplo de Hola más común es implementar un entorno de desarrollo estándar en un escenario de TI de las empresas o SI.

### <a name="capability-scope"></a>Ámbito de funcionalidad
Un ámbito de funcionalidad se centra en la implementación y configuración de una topología para una tecnología determinada. Los escenarios comunes incluyen tecnologías como SQL Server, Cassandra y Hadoop.

### <a name="end-to-end-solution-scope"></a>Ámbito de solución completa
Un ámbito de la solución-to-End es más allá de una única función de destino y en su lugar se encarga de entregar una solución de tooend end consta de varias funciones.  

Una plantilla con ámbito de solución se manifiesta como un conjunto de una o varias plantillas con ámbito de funcionalidad con recursos, lógica y estado deseado específicos de una solución. Un ejemplo de una plantilla de solución de ámbito es una plantilla de solución final tooend datos canalización. plantilla de Hello puede mezclar topología específica de la solución y el estado con varias plantillas de solución de ámbito de capacidad como Kafka, Storm y Hadoop.

## <a name="choosing-free-form-vs-known-configurations"></a>Elección de configuraciones conocidas frente a forma libre
Puede que piense inicialmente en una plantilla debe conceder a los consumidores mayor flexibilidad de hello, pero muchas consideraciones afecta al elegir Hola si las configuraciones de forma libre de toouse frente a configuraciones conocidas. Esta sección identifican los requisitos del cliente clave hello y consideraciones técnicas que en forma de enfoque de hello compartido en este documento.

### <a name="free-form-configurations"></a>Configuraciones de forma libre
En la superficie de hello, configuraciones de forma libre de sonido ideales. Permiten tooselect un tipo de máquina virtual y proporcionar un número arbitrario de nodos y discos para los nodos conectados, y hágalo como plantilla de tooa de parámetros. Sin embargo, este enfoque no es el ideal para algunos escenarios.

En [tamaños de máquinas virtuales](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), se identifican diferentes tipos de VM hello y los tamaños disponibles, y cada uno de número de Hola de durable discos (2, 4, 8, 16 ó 32) que se pueden adjuntar. Cada disco conectado proporciona 500 IOPS, y se pueden agrupar múltiplos de estos discos por un multiplicador de ese número de IOPS. Por ejemplo, 16 discos puede ser tooprovide agrupado 8.000 e/s por segundo. La agrupación se realiza con la configuración en el sistema operativo de hello, usando espacios de almacenamiento de Microsoft Windows o matriz redundante de discos independientes (RAID) de Linux.

Una configuración de forma libre permite selección Hola varias instancias de máquina virtual, VM de varios tipos y tamaños para esas instancias, de varios discos para hello tipo de máquina virtual, y uno o varios scripts de contenido VM de tooconfigure Hola.

Es frecuente que una implementación pueda tener varios tipos de nodos, como nodos maestros y de datos, por lo que esta flexibilidad se proporciona a menudo para cada tipo de nodo.

En cuanto comience toodeploy clústeres de importancia, comenzar toowork con estos escenarios complejos. Si estuviera implementando un clúster de Hadoop, por ejemplo, con 8 nodos maestros y los nodos de datos de 200 y agrupados 4 discos conectados en cada nodo principal y agrupados 16 discos conectados por nodo de datos, deberá 208 máquinas virtuales y 3,232 discos toomanage.

Una cuenta de almacenamiento limitar las solicitudes anteriores que su 20.000 identificado limitar las transacciones por segundo, por lo que debe buscar en la creación de particiones de cuenta de almacenamiento y usar cálculos número adecuado de hello toodetermine de almacenamiento cuentas tooaccommodate esta topología. Dada la gran cantidad de Hola de combinaciones compatibles con el enfoque de forma libre de hello, cálculos dinámicos se requiere toodetermine Hola a creación de particiones adecuada. Hola idioma de plantilla del Administrador de recursos de Azure no proporciona actualmente funciones matemáticas, por lo que debe realizar estos cálculos en el código, generar una plantilla única, codificado de forma rígida con detalles adecuados de Hola.

En escenarios de SI y TI empresarial, alguien debe mantener las plantillas de Hola y admitir topologías Hola implementado para una o varias organizaciones. Esta sobrecarga adicional, configuraciones y plantillas diferentes para cada cliente, está lejos de ser deseable.

Puede usar estos entornos de toodeploy plantillas de suscripción de Azure de su cliente, pero los equipos de TI corporativos y CSV normalmente implementarlos en sus propias suscripciones, con un toobill de la función de anulación sus clientes. En estos escenarios, objetivo hello es toodeploy capacidad para varios clientes a través de un grupo de suscripciones e implementaciones de mantener densamente rellenadas en hello suscripciones toominimize suscripción proliferación: es decir, más toomanage de suscripciones. Con tamaños de implementación dinámico, para lograr este tipo de densidad requiere una cuidadosa planificación y desarrollo adicional para el trabajo de la técnica scaffolding en nombre de organización de Hola.

Además, no se puede crear suscripciones a través de una llamada de API pero debe hacerlo manualmente a través del portal de Hola. A medida que aumenta el número de Hola de suscripciones, cualquier proliferación resultante de la suscripción requiere intervención humana: no se puede automatizar. Con tanta variabilidad en tamaños de Hola de las implementaciones, tendrás que toopre aprovisionar un número de suscripciones manualmente tooensure suscripciones están disponibles.

Teniendo en cuenta todos estos factores, una configuración verdaderamente de forma libre es menos atractiva que a primera vista.

### <a name="known-configurations--hello-t-shirt-sizing-approach"></a>Conoce las configuraciones: Hola enfoque de ajuste de tamaño de camiseta
En su lugar de ofrecer una plantilla que proporciona total flexibilidad y muchas variaciones, en nuestra experiencia un patrón común es tooprovide Hola capacidad tooselect conocida las configuraciones, en efecto, tamaños de camiseta estándar como espacio aislado, pequeño, mediano y grande. Otros ejemplos de tamaños de camiseta son ofertas de productos, como edición para la comunidad o edición para impresa.  En otros casos, pueden ser configuraciones de una tecnología específicas de la carga de trabajo, como MapReduce o NoSQL.

Muchas organizaciones de TI corporativa, proveedores de software de código abierto e integradores de sistemas permiten que sus ofertas estén disponibles de esta manera en entornos virtualizados locales (empresas) o como ofertas de software como servicio (SaaS) (CSV y OSV).

Este enfoque proporciona configuraciones bien conocidas de tamaños variables que están preconfiguradas para los clientes. Sin configuraciones conocidas, los clientes finales deben determinar el tamaño de clúster por sí solas, tener en cuenta las restricciones de recursos de plataforma y realice matemáticas tooidentify Hola resultante particiones de las cuentas de almacenamiento y otros recursos (vence toocluster tamaño y recursos restricciones). Conoce las configuraciones permiten el tamaño adecuado de camiseta de clientes tooeasily seleccione hello, es decir, una implementación determinada. Además toomaking una mejor experiencia de cliente hello, un pequeño número de configuraciones conocidas es más fácil toosupport y puede ayudarle a ofrecer un mayor nivel de densidad.

Un enfoque de configuración conocida centrado en los tamaños de camiseta también puede tener un número variable de nodos dentro de un mismo tamaño. Por ejemplo, un tamaño de camiseta pequeña puede estar entre 3 y 10 nodos.  tamaño de la camiseta de Hello podría tener diseñada tooaccommodate los nodos too10 y proporcionar Hola selecciones de forma libre de consumidor Hola capacidad toomake de tamaño máximo de toohello identificado.  

Un tamaño de la camiseta según el tipo de carga de trabajo, puede ser más forma libre de naturaleza en cuanto al número de Hola de nodos que se pueden implementar pero tendrán tamaño de nodo distintos de carga de trabajo y la configuración del software de hello en el nodo de Hola.

Tamaños de camiseta basados en las ofertas de productos, como community o Enterprise, puede tener tipos de recursos distintos y número máximo de nodos que se puede implementar, vinculados normalmente toolicensing consideraciones o disponibilidad de las características a través de diferentes ofertas de Hola.

También puede dar cabida a los clientes con variantes únicas mediante plantillas de hello basada en JSON. Cuando se trabaja con valores atípicos, puede incorporar planeamiento adecuado de Hola y consideraciones para el desarrollo, la compatibilidad y la administración de costos.

En función de los escenarios de consumo de plantilla de cliente de Hola y requisitos identificados en el inicio de Hola de este documento, hemos identificado un patrón para la descomposición de la plantilla.

## <a name="capacity-and-capability-scoped-solution-templates"></a>Plantillas de soluciones con ámbito de capacidad y de funcionalidad
Descomposición proporciona un desarrollo tootemplate enfoque modular que admite su reutilización, extensibilidad, pruebas y conjunto de herramientas. En esta sección se ofrece detalles sobre cómo un enfoque de descomposición puede ser aplicada tootemplates con un ámbito de capacidad o la capacidad.

En este enfoque, una plantilla principal recibe valores de parámetro de un consumidor de plantilla, a continuación, vincula tooseveral tipos de plantillas y las secuencias de comandos en un nivel inferior, tal y como se muestra a continuación. Parámetros, variables estáticas y variables generadas son valores de tooprovide usado dentro y fuera de plantillas de hello vinculado.

![Parámetros de plantilla](./media/best-practices-resource-manager-design-templates/template-parameters.png)

**Los parámetros se pasan tooa principal de plantillas, a continuación, plantillas de toolinked**

Hola siguiendo el enfoque de secciones en tipos de Hola de plantillas y secuencias de comandos que se descompone una única plantilla en. las secciones de Hello presentan enfoques para pasar información de estado entre las plantillas de Hola. Cada tipo de secuencia de comandos hello y plantilla en la imagen de Hola se describe junto con ejemplos. Para obtener un ejemplo contextual, vea "Integración: una implementación de ejemplo" más adelante en este documento.

### <a name="template-metadata"></a>Metadatos de plantilla
Metadatos de la plantilla (archivo de hello metadata.json) contienen los pares de clave/valor que describen una plantilla en JSON, que se puede leer los seres humanos y sistemas de software.

![Metadatos de plantilla](./media/best-practices-resource-manager-design-templates/template-metadata.png)

**Metadatos de la plantilla se describen en el archivo de hello metadata.json**

Agentes del software pueden recuperar el archivo de metadata.json hello y publicar información de hello y una plantilla de toohello de vínculo en una página web o el directorio. Los elementos incluyen *itemDisplayName*, *description*, *summary*, *githubUsername* y *dateUpdated*.

A continuación, se muestra un archivo de ejemplo en su totalidad.

    {
        "itemDisplayName": "PostgreSQL 9.3 on Ubuntu VMs",
        "description": "This template creates a PostgreSQL streaming-replication between a master and one or more slave servers each with 2 striped data disks. hello database servers are deployed into a private-only subnet with one publicly accessible jumpbox VM in a DMZ subnet with public IP.",
        "summary": "PostgreSQL stream-replication with multiple slave servers and a publicly accessible jumpbox VM",
        "githubUsername": "arsenvlad",
        "dateUpdated": "2015-04-24"
    }

### <a name="main-template"></a>Plantilla principal
plantilla principal Hola recibe parámetros de un usuario, usa esa variables de objeto complejo de toopopulate de información y ejecuta Hola vinculado plantillas.

![Plantilla principal](./media/best-practices-resource-manager-design-templates/main-template.png)

**plantilla de Hello principal recibe parámetros de un usuario**

Un parámetro proporcionado es un tipo de configuración conocida también conocido como parámetro de tamaño de hello camiseta debido a sus valores estándar como pequeña, mediana o grande. En la práctica, puede usar este parámetro de varias formas. Para obtener más información, vea "Plantilla de recursos de configuración conocida" más adelante en este documento.

Algunos recursos se implementan con independencia de la configuración conocida de hello especificada por un parámetro de usuario. Estos recursos se aprovisionan con una plantilla de recurso compartido único y se comparten con otras plantillas, por lo que la plantilla del recurso compartido de Hola se ejecuta primero.

Algunos recursos se implementan, opcionalmente, independientemente de la configuración conocida de hello especificado.

### <a name="shared-resources-template"></a>Plantilla de recursos compartidos
Esta plantilla proporciona los recursos que son comunes a todas las configuraciones conocidas. Contiene la red virtual de hello, conjuntos de disponibilidad y otros recursos que son necesarios, independientemente de la plantilla de configuración conocida de Hola que se implementa.

![Recursos de plantilla](./media/best-practices-resource-manager-design-templates/template-resources.png)

**Plantilla de recursos compartidos**

Nombres de los recursos, como el nombre de red virtual de hello, se basan en la plantilla principal Hola. Puede especificarlos como una variable dentro de dicha plantilla o recibirlos como un parámetro de usuario de hello, según sea necesario por su organización.

### <a name="optional-resources-template"></a>Plantilla de recursos opcionales
plantilla de recursos opcional Hello contiene recursos que se implementan mediante programación en función de valor de Hola de un parámetro o variable.

![Recursos opcionales](./media/best-practices-resource-manager-design-templates/optional-resources.png)

**Plantilla de recursos opcionales**

Por ejemplo, puede usar un tooconfigure de plantilla de recursos opcional un jumpbox que permite acceso indirecto tooa implementado entorno de hello Internet pública. Usaría un parámetro o variable tooidentify si se debe habilitar jumpbox Hola y Hola *concat* toobuild Hola destino nombre para la plantilla de hello, de la función como *jumpbox_enabled.json*. Vinculación de plantilla utilizaría Hola resultante tooinstall variable hello jumpbox.

Puede vincular la plantilla de recursos opcional Hola desde varios lugares:

* Cuando la implementación tooevery aplicables, crear un vínculo controlado por el parámetro de plantilla de recursos compartidos de Hola.
* Cuando tooselect aplicable conocida las configuraciones, por ejemplo, solo se instale en implementaciones a grandes escala: crear un vínculo controlada por la variable o controlados por el parámetro de plantilla de configuración conocida de Hola.

Si un recurso determinado es opcional pueden no está determinado por consumidor de la plantilla de hello sino más bien por el proveedor de la plantilla de Hola. Por ejemplo, puede que necesite toosatisfy un requisito de producto determinado o el complemento de producto (común para los CSV) o directivas tooenforce (común para SIs y TI empresarial grupos). En estos casos, puede usar una variable tooidentify si se deben implementar los recursos de Hola.

### <a name="known-configuration-resources-template"></a>Plantilla de recursos de configuración conocida
En la plantilla principal de hello, un parámetro puede ser tooallow expuesto Hola plantilla consumidor toospecify un toodeploy de configuración conocido deseada. A menudo, esta configuración conocida usa un enfoque de tamaño de camiseta, con un conjunto de tamaños de configuración fijos, como espacio aislado, pequeña, mediana y grande.

![Recursos de configuración conocida](./media/best-practices-resource-manager-design-templates/known-config.png)

**Plantilla de recursos de configuración conocida**

enfoque de tamaño de Hello camiseta es más frecuente, pero los parámetros de hello pueden representar cualquier conjunto de configuraciones conocidas. Por ejemplo, puede especificar un conjunto de entornos para una aplicación empresarial, como Desarrollo, Prueba y Producto. O bien se puede usar para un toorepresent de servicio de nube diferente escalar unidades, las versiones de producto o configuraciones de productos, como la Comunidad, Developer o Enterprise.

Al igual que con la plantilla del recurso compartido de hello, las variables se pasan plantilla configuraciones conocidas de toohello desde:

* Un usuario final, es decir, los parámetros de hello envían toohello principal de plantillas.
* Una organización, es decir, Hola variables de plantilla principal de Hola que representan requisitos internos o directivas de.

### <a name="member-resources-template"></a>Plantilla de recursos de miembros
Dentro de una configuración conocida, a menudo se incluyen uno o más tipos de nodos de miembros. Por ejemplo, con Hadoop tiene nodos maestros y de datos. Si instala MongoDB, tiene nodos de datos y un árbitro. Si implementa DataStax, tiene nodos de datos, así como una máquina virtual con OpsCenter instalado.

![Recursos de miembros](./media/best-practices-resource-manager-design-templates/member-resources.png)

**Plantilla de recursos de miembros**

Cada tipo de nodos puede tener distintos tamaños de máquinas virtuales, número de discos conectados, tooinstall de secuencias de comandos y configurar nodos hello, configuraciones de puerto para las máquinas virtuales de hello, número de instancias y otros detalles. Para que cada tipo de nodo obtiene su propia plantilla de recursos de miembro, que contiene Hola detalles para implementar y configurar una infraestructura, así como para ejecutar secuencias de comandos toodeploy y configure software de hello máquina virtual.

Para las máquinas virtuales se usan normalmente dos tipos de scripts: scripts ampliamente reutilizables y scripts personalizados.

### <a name="widely-reusable-scripts"></a>Scripts ampliamente reutilizables
Los scripts ampliamente reutilizables se pueden usar en varios tipos de plantillas. Uno de hello mejor ejemplos de estos scripts ampliamente reutilizables configura RAID en Linux toopool discos y obtener un mayor número de IOPS. Independientemente del software de hello instalándose Hola VM, esta secuencia de comandos proporciona la reutilización de prácticas demostradas para escenarios comunes.

![Scripts reutilizables](./media/best-practices-resource-manager-design-templates/reusable-scripts.png)

**Las plantillas de recursos de miembros pueden llamar a los scripts ampliamente reutilizables**

### <a name="custom-scripts"></a>Scripts personalizados
Las plantillas llaman habitualmente a uno o varios scripts que instalan y configuran software en las máquinas virtuales. Se considera un patrón común con topologías grandes donde se implementan varias instancias de uno o varios tipos de miembros. Se inicia un script de instalación para cada máquina virtual que se puede ejecutar en paralelo, seguido de un script de configuración al que se llama después de que se implementan todas las máquinas virtuales (o todas las máquinas virtuales de un tipo de miembro especificado).

![Scripts personalizados](./media/best-practices-resource-manager-design-templates/custom-scripts.png)

**Las plantillas de recursos de miembros pueden llamar a scripts de fin específico, como la configuración de una máquina virtual**

## <a name="capability-scoped-solution-template-example---redis"></a>Ejemplo de plantilla de solución con ámbito de funcionalidad: Redis
tooshow cómo podría funcionar una implementación, echemos un vistazo a un ejemplo práctico de creación de una plantilla que facilita la implementación de Hola y configuración de Redis en tamaños estándar de la camiseta.  

Para la implementación de hello, hay un conjunto de recursos compartidos (red virtual, cuenta de almacenamiento, los conjuntos de disponibilidad) y un recurso opcional (jumpbox). Hay varias configuraciones conocidas representadas como tamaños de camiseta (pequeña, mediana, grande), pero cada una con un único tipo de nodo. También hay dos scripts de fin específico (instalación, configuración).

### <a name="creating-hello-template-files"></a>Crear archivos de plantilla de Hola
Crea una plantilla principal denominada azuredeploy.json.

Crea una plantilla de recursos compartidos denominada resources.json.

Se crea una implementación de plantilla de recursos opcional tooenable Hola de un jumpbox, denominado jumpbox_enabled.json

Redis usa un solo tipo de nodo, así que crea una sola plantilla de recursos de miembros denominada node-resources.json.

Con Redis, desea tooinstall cada nodo individual y, a continuación, configurar el clúster de Hola.  Tiene scripts tooaccommodate Hola instalación y configurar, "Install.sh". de clúster redis y setup.sh de clúster de redis.

### <a name="linking-hello-templates"></a>Plantillas de hello vinculación
Vinculación de la plantilla principal de plantillas de hello vincula fuera de la plantilla de recursos compartidos de toohello, que establece Hola de red virtual.

Se agrega lógica dentro de los consumidores tooenable principal de plantillas de Hola de hello plantilla toospecify si se debe implementar un jumpbox. Un *habilitado* valor de hello *EnableJumpbox* parámetro indica que el cliente hello desea toodeploy una jumpbox. Cuando se proporciona este valor, la plantilla de hello concatena *_enabled* como un nombre de sufijo tooa Basar plantilla para la capacidad de jumpbox Hola.

plantilla principal Hola aplica hello *grandes* valor del parámetro como un nombre de plantilla de base de sufijo tooa tamaños camiseta y, a continuación, utiliza ese valor en un vínculo de la plantilla fuera demasiado*technology_on_os_large.json*.

topología de Hello podría parecerse a esta ilustración.

![Plantilla de Redis](./media/best-practices-resource-manager-design-templates/redis-template.png)

**Estructura de plantilla para una plantilla de Redis**

### <a name="configuring-state"></a>Estado de configuración
Para los nodos de hello en clúster de hello, hay dos pasos tooconfiguring estado de hello, representan secuencias de comandos específicos de propósito.  Redis "redis-clúster-install.sh" instala y configura clúster Hola "redis-clúster-setup.sh".

### <a name="supporting-different-size-deployments"></a>Soporte de implementaciones de diferentes tamaños
Dentro de las variables, plantilla de tamaño de hello camiseta especifica número Hola de nodos de cada tipo toodeploy para hello tamaño especificado (*grandes*). A continuación, implementa ese número de instancias de máquina virtual mediante bucles de recursos, proporcionar nombres únicos tooresources anexando un nombre de nodo con una secuencia numérica de *copyIndex()*. Realiza estos pasos tanto las máquinas virtuales de zona activa y activa, tal como se define en la plantilla del nombre del saludo camiseta

## <a name="decomposition-and-end-to-end-solution-scoped-templates"></a>Descomposición y plantillas con ámbito de solución completa
Una plantilla de solución con ámbito de solución completa se centra en proporcionar una solución completa.  Normalmente, este enfoque es una composición de varias plantillas con ámbito de funcionalidad con recursos, lógica y estado adicionales.

Como se resalta en la imagen de hello siguiente, hello mismo modelo que se usa para las plantillas de función con ámbito se extiende para plantillas con un ámbito de la solución de extremo a extremo.

Una plantilla de recursos compartidos y plantillas de recursos opcional sirven Hola misma función que en la capacidad de hello ámbito enfoques de plantilla, pero el ámbito de la solución de hello end tooend.

Como solución de tooend completa el ámbito plantillas también normalmente pueden tener tamaños de la camiseta, la plantilla de recursos de configuración conocido de hello refleja lo que se requiere para una determinada configuración conocida de solución de Hola.

tooone de vínculos de plantilla de recursos de configuración conocido de Hola o más capacidad de ámbito de plantillas de solución toohello relevante solución tooend, así como Hola plantillas de recursos de miembro que son necesarios para la solución de hello end tooend.

Como tamaño de la camiseta de Hola de solución de Hola puede ser diferente de la plantilla de ámbito de capacidad de hello individual, las variables dentro de hello conoce plantilla de recursos de configuración son utilizados tooprovide Hola los valores adecuados para la solución de capacidad de nivel inferior con ámbito plantillas toodeploy Hola camiseta tamaño adecuado.

![Completa](./media/best-practices-resource-manager-design-templates/end-to-end.png)

**modelo de Hello utilizado para la capacidad o plantillas de solución de capacidad de ámbito se pueden ampliar fácilmente para ámbitos de plantilla de solución de tooend final**

## <a name="preparing-templates-for-hello-marketplace"></a>Preparación de las plantillas para hello Marketplace
Hola anterior enfoque fácilmente dé cabida a escenarios donde las empresas y SIs, CSV tooeither desea implementar plantillas Hola por sí mismos o habilitar su toodeploy de clientes en su propio.

Otro escenario deseado está implementando una plantilla a través de marketplace de Hola.  Este enfoque de descomposición funciona en marketplace de hello, con algunos cambios menores.

Como se mencionó anteriormente, plantillas pueden ser tipos de implementación distintos de toooffer usado para la venta en marketplace Hola. Algunos tipos de implementaciones diferentes pueden ser tamaños de camiseta (pequeña, mediana, grande), tipo de producto/público (comunidad, desarrollador, empresa) o tipo de característica (básica, alta disponibilidad).

Como se muestra a continuación, Hola existente final tooend soluciones o la funcionalidad de plantillas de ámbito pueden ser fácilmente utiliza configuraciones conocidas de toolist Hola diferentes en marketplace Hola.

Hello parámetros toohello principal plantilla son primero modificar tooremove Hola entrante parámetro denominado tshirtSize.

Mientras toohello conoce plantilla de recursos de configuración asignan los tipos de implementación distintos de hello, también necesitan recursos comunes de Hola y encuentra la configuración de Hola plantilla de recursos compartidos y potencialmente los de las plantillas de recursos opcional.

Si desea toopublish el marketplace de toohello de plantilla, establecer distintas copias de la plantilla principal que reemplaza previamente hello como parámetro de entrada disponible de tshirtSize tooa variable incrustado en la plantilla de Hola.

![Marketplace](./media/best-practices-resource-manager-design-templates/marketplace.png)

**Adaptar una solución de ámbito de plantilla para la tienda de Hola**

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de cómo compartir el estado dentro y fuera de las plantillas, consulte [compartir el estado en las plantillas de Azure Resource Manager](best-practices-resource-manager-state.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

