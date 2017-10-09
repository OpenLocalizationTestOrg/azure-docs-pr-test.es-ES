---
title: "aaaKey características y conceptos de pila de Azure | Documentos de Microsoft"
description: "Obtenga información sobre las características clave de Hola y conceptos de pila de Azure."
services: azure-stack
documentationcenter: 
author: Heathl17
manager: byronr
editor: 
ms.assetid: 09ca32b7-0e81-4a27-a6cc-0ba90441d097
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: helaw
ms.openlocfilehash: a9cb3b99dc67a12976ca61b6678f047caab48543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="key-features-and-concepts-in-azure-stack"></a>Características y conceptos clave de Azure Stack
Si le tooMicrosoft nueva pila de Azure, estos términos y las descripciones de características pueden resultar útiles.

## <a name="personas"></a>Personas
Hay dos tipos de usuarios para la pila de Microsoft Azure, operador de hello en la nube (proveedor) y de inquilinos de hello (consumidor).

* A **operador nube** puede configurar la pila de Azure y administrar ofertas, planes, servicios, cuotas y precios recursos tooprovide de sus inquilinos.  Operadores de la nube también administración la capacidad y responden tooalerts.  
* A **inquilino** (también denominado tooas un usuario) consume services que Hola ofertas de administrador en la nube. Los inquilinos pueden aprovisionar, supervisar y administrar los servicios a los que se han suscrito, como Aplicaciones Web, Almacenamiento y Máquinas virtuales.

## <a name="portal"></a>Portal
métodos principales de saludo de la interacción con la pila de Microsoft Azure son portal de administración de hello, portal de usuarios y PowerShell.

cada uno de ellos portales de la pila de Azure de Hola se basan en instancias independientes del Administrador de recursos de Azure.  Un operador en la nube usa Hola administrador portal toomanage pila de Azure y toodo cosas como crear a inquilino ofertas.  portal de usuarios de Hello (también la portal del inquilino hello tooas que se hace referencia) proporciona una experiencia de autoservicio para el consumo de recursos de nube, como máquinas virtuales, las cuentas de almacenamiento y las aplicaciones Web. Para obtener más información, consulte [uso de portales de administrador y usuario de la pila de Azure de hello](azure-stack-manage-portals.md).

## <a name="identity"></a>Identidad 
Azure Stack usa Azure Active Directory (AAD) o los Servicios de federación de Active Directory (AD FS) como proveedor de identidades.  

### <a name="azure-active-directory"></a>Azure Active Directory
Azure Active Directory es el proveedor de identidades multiinquilino basado en la nube de Microsoft.  Mayoría de los escenarios híbridos usa Azure Active Directory como almacén de identidades de Hola.

### <a name="active-directory-federation-services"></a>Servicios de federación de Active Directory
Puede elegir toouse Active Directory Federation Services (AD FS) para las implementaciones desconectadas de la pila de Azure.  Pila de Azure, proveedores de recursos y las otras aplicaciones funcionen mucho Hola igual con AD FS como lo hacen con Azure Active Directory. Azure Stack incluye su propia instancia de AD FS y Active Directory, así como una API de Active Directory Graph. Kit de desarrollo de pila de Azure admite Hola AD FS los escenarios siguientes:

- Inicie sesión en la implementación de toohello mediante AD FS.
- Creación de una máquina virtual con secretos en Key Vault.
- Creación de un almacén para almacenar secretos y acceder a ellos.
- Creación de roles personalizados de RBAC en la suscripción.
- Asignar a usuarios roles tooRBAC en recursos
- Creación de roles RBAC de todo el sistema a través de Azure PowerShell.
- Inicio de sesión como usuario a través de Azure PowerShell.
- Crear servicio de las entidades de seguridad utilizan toosign en tooAzure PowerShell


## <a name="regions-services-plans-offers-and-subscriptions"></a>Regiones, servicios, planes, ofertas y suscripciones
En la pila de Azure, servicios se entregan tootenants con las regiones, suscripciones, ofertas y planes. Los inquilinos puedan suscribirse toomultiple ofertas. Las ofertas pueden tener uno o varios planes, y los planes pueden tener uno o varios servicios.

![](media/azure-stack-key-features/image4.png)

Ejemplo de jerarquía de toooffers de suscripciones del inquilino, cada uno con distintos planes y servicios.

### <a name="regions"></a>Regiones
Las regiones de Azure Stack son un elemento básico de escala y administración. Una organización puede tener varias regiones con recursos disponibles en cada región. Las regiones también pueden tener distintas ofertas de servicio disponibles. En Azure Stack Development Kit, solo se admite una única región, a la que se asigna el nombre *local* automáticamente.

### <a name="services"></a>Services
Pila de Microsoft Azure permite proveedores toodeliver una amplia variedad de servicios y aplicaciones, como máquinas virtuales, las bases de datos de SQL Server, SharePoint, Exchange y mucho más.

### <a name="plans"></a>Planes
Los planes son agrupaciones de uno o varios servicios. Como proveedor, crear planes de inquilinos de tooyour toooffer. A su vez, los inquilinos suscribirán tooyour ofertas toouse Hola planes y servicios que se incluyen.

Cada servicio agregado tooa plan puede configurarse con toohelp de configuración de cuota, administrar la capacidad de la nube. Las cuotas pueden incluir restricciones, como límites de máquinas virtuales, CPU y RAM, y se aplican por suscripción de usuario. Las cuotas se pueden diferenciar por su ubicación. Por ejemplo, un plan que contiene servicios Compute Services de la Región A puede tener una cuota de dos máquinas virtuales, 4 GB de RAM y 10 núcleos de CPU.

Al crear una oferta, el Administrador de servicios de hello puede incluir un **plan base**. Estos planes base se incluyen de forma predeterminada cuando un inquilino suscribe toothat oferta. Cuando un usuario se suscribe (y se crea la suscripción de hello), usuario de hello tiene proveedores de recursos de acceso tooall Hola especificados en esos planes base (con las cuotas correspondientes de hello).

También puede incluir el Administrador de servicios de Hello **planes de complemento** en una oferta. Planes de complemento no se incluyen de forma predeterminada en la suscripción de Hola. Planes de complemento son planes adicionales (cuotas) disponibles en una oferta que un propietario de la suscripción puede agregar suscripciones de tootheir.

### <a name="offers"></a>Ofertas
Ofertas son grupos de uno o más planes de ese toobuy tootenants presente de proveedores (suscribirse a). Por ejemplo, la Oferta Alfa puede incluir el Plan A (que contiene un conjunto de servicios Compute Services) y el Plan B (que contiene un conjunto de servicios de almacenamiento y Network Services).

Una oferta incluye un conjunto de planes de base y los administradores de servicios pueden crear planes de complemento que los inquilinos pueden agregar suscripción tootheir.

### <a name="subscriptions"></a>Suscripciones
Una suscripción es la forma en que los inquilinos compran las ofertas. Una suscripción es una combinación de un inquilino con una oferta. Un inquilino puede tener suscripciones toomultiple ofertas. Cada suscripción aplica a una oferta de tooonly. Las suscripciones de un inquilino determinan los planes y servicios a los que pueden acceder.

Las suscripciones ayudan a los proveedores a organizar los recursos y servicios de la nube, y a acceder a ellos.

Para que el Administrador de hello, se crea una suscripción de proveedor predeterminado durante la implementación. Esta suscripción puede ser usado toomanage pila de Azure, implementar más proveedores de recursos y crear ofertas y planes para inquilinos. No debe ser aplicaciones y cargas de trabajo de cliente toorun utilizado. 

## <a name="azure-resource-manager"></a>Administrador de recursos de Azure
Con Azure Resource Manager, puede trabajar con los recursos de la infraestructura en un modelo declarativo basado en plantillas.   Proporciona una única interfaz que puede usar toodeploy y administrar los componentes de la solución. Para obtener información completa e instrucciones, consulte hello [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

### <a name="resource-groups"></a>Grupos de recursos
Los grupos de recursos son colecciones de recursos, servicios y aplicaciones (y cada recurso tiene un tipo, como máquinas virtuales, redes virtuales, IP públicas, cuentas de almacenamiento y sitios web). Cada recurso debe estar en un grupo de recursos, por lo que los grupos de recursos ayudan a organizar los recursos de manera lógica, por ejemplo, por carga de trabajo o ubicación.  En Microsoft Azure Stack, los recursos, como los planes y ofertas, también se administran en grupos de recursos.
 
### <a name="azure-resource-manager-templates"></a>Plantillas de Azure Resource Manager
Con Azure Resource Manager, puede crear una plantilla (en formato JSON) que defina la implementación y configuración de la aplicación. Esta plantilla se conoce como una plantilla de Azure Resource Manager y proporciona una implementación de toodefine de manera declarativa. Mediante una plantilla, puede implementar la aplicación a lo largo del ciclo de vida de aplicación Hola repetidamente y estar seguro de que los recursos se implementan en un estado coherente.

## <a name="resource-providers-rps"></a>Proveedores de recursos (RP)
Proveedores de recursos son servicios web que foundation de Hola de formulario para todos los servicios de IaaS y PaaS basado en Azure. Administrador de recursos de Azure se basa en diferentes RPs tooprovide acceso tooservices.

Hay cuatro RP fundamentales: de red, de proceso, Storage y KeyVault. Cada uno de estos RP le ayuda a configurar y controlar sus respectivos recursos. Los administradores de servicios también pueden agregar nuevos proveedores de recursos personalizados.

### <a name="compute-rp"></a>RP de proceso
Hola proveedor de recursos de proceso (PRC) permite la pila de Azure los inquilinos toocreate sus propias máquinas virtuales. Hola CRP incluye Hola capacidad toocreate las máquinas virtuales, así como las extensiones de máquina Virtual. Hola servicio de extensión de la máquina Virtual le ayuda a proporcionar capacidades de IaaS para máquinas virtuales Windows y Linux.  Por ejemplo, puede utilizar Hola CRP tooprovision una máquina virtual Linux y ejecutar scripts de Bash durante hello tooconfigure de implementación virtual.

### <a name="network-rp"></a>RP de red
Hola proveedor de recursos de red (NRP) ofrece una serie de características Software Defined Networking (SDN) y virtualización de función de red (NFV) para la nube privada de Hola.  Puede usar recursos de hello NRP toocreate como grupos de seguridad de red, direcciones IP públicas, los equilibradores de carga de software, redes virtuales.

### <a name="storage-rp"></a>RP de almacenamiento
Hola RP de almacenamiento ofrece cuatro servicios de almacenamiento de Azure coherente: blob, tabla, cola y la administración de cuentas. También ofrece una almacenamiento en la nube administración servicio toofacilitate servicio Administración del proveedor de servicios de almacenamiento de Azure coherente. Almacenamiento de Azure proporciona Hola flexibilidad toostore y recuperar grandes cantidades de datos no estructurados, como documentos y archivos multimedia con los Blobs de Azure, y NoSQL estructurado según datos con tablas de Azure. Para obtener más información sobre el almacenamiento de Azure, consulte [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md).

#### <a name="blob-storage"></a>Almacenamiento de blobs
Almacenamiento de blobs almacena cualquier conjunto de datos. Un blob puede ser un tipo cualquiera de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación. El almacenamiento de tablas almacena conjuntos de datos estructurados. Almacenamiento de tabla es un almacén de datos del atributo de clave NoSQL, que permite el desarrollo rápido y las cantidades de toolarge de acceso rápido de datos. El almacenamiento de colas ofrece una solución de mensajería confiable para el procesamiento de flujos de trabajo y para la comunicación entre los componentes de los servicios en la nube.

Cada blob se organiza en un contenedor. Los contenedores también proporcionan un toogroups de directivas de seguridad de un modo útil tooassign de objetos. Una cuenta de almacenamiento puede contener cualquier número de contenedores y un contenedor puede contener cualquier número de blobs, seguridad de límite de capacidad de 500 TB toohello de cuenta de almacenamiento de Hola. Blob Storage ofrece tres tipos de blobs: blobs en bloques, blobs en anexos y blobs en páginas (discos). Los blobs en bloques están optimizados para el streaming y para el almacenamiento de objetos en la nube, y constituyen una opción idónea para almacenar documentos, archivos multimedia y copias de seguridad, entre otros. Anexar blobs de blobs de tooblock similares, pero están optimizados para las operaciones de anexión. Se puede actualizar un blob en anexos agregando un nuevo extremo toohello de bloque. Anexar blobs son una buena elección para escenarios como la del registro, donde nuevos datos necesitan toobe escribe solo toohello final del blob de Hola. Blobs en páginas se optimización para representar los discos de IaaS y admitir aleatorio escribe y puede ser up too1 TB. Un disco IaaS asociado a una red de máquinas virtuales de Azure es un VHD almacenado como blob en páginas.

#### <a name="table-storage"></a>Almacenamiento de tablas
Este tipo de almacenamiento se basa en un almacén de claves/atributos NoSQL de Microsoft con un diseño sin esquema que lo diferencia de las bases de datos relacionales tradicionales. Puesto que los esquemas de falta de almacenes de datos, es fácil tooadapt necesidades de los datos como Hola de evolucionar de la aplicación. Almacenamiento de tabla es fácil toouse, por lo que los desarrolladores pueden crear aplicaciones rápidamente. Este tipo de almacenamiento se basa en un almacén de clave-atributo, lo que significa que cada valor de una tabla se almacena con un nombre de propiedad tipado. nombre de la propiedad de Hello puede usarse para filtrar y especificar criterios de selección. Una colección de propiedades y sus valores, componen una entidad. Desde esquemas de falta de almacenamiento de tabla, las dos entidades de Hola misma tabla puede contener diferentes colecciones de propiedades y esas propiedades pueden ser de tipos diferentes. Puede usar la tabla almacenamiento toostore flexible conjuntos de datos, como los datos de usuario para aplicaciones web, libretas de direcciones, información del dispositivo y cualquier otro tipo de metadatos que necesite el servicio. Puede almacenar cualquier número de entidades en una tabla y una cuenta de almacenamiento puede contener cualquier número de tablas, una toohello el límite de capacidad de la cuenta de almacenamiento de Hola.

#### <a name="queue-storage"></a>Queue Storage
El almacenamiento en cola de Azure proporciona mensajería en la nube entre componentes de aplicaciones. A la hora de diseñar aplicaciones para escala, los componentes de las mismas suelen desacoplarse para poder escalarlos de forma independiente. Almacenamiento de cola ofrece mensajería asincrónica para la comunicación entre componentes de aplicaciones, si se están ejecutando en la nube de hello, en el escritorio de hello, en un servidor local o en un dispositivo móvil. Además, este tipo de almacenamiento admite la administración de tareas asincrónicas y la creación de flujos de trabajo de procesos.

### <a name="keyvault"></a>KeyVault
Hola KeyVault RP proporciona administración y auditoría de secretos, como contraseñas y certificados. Por ejemplo, puede usar un inquilino Hola KeyVault RP tooprovide administrador contraseñas o claves durante la implementación de máquina virtual.

## <a name="role-based-access-control-rbac"></a>Control de acceso basado en roles (RBAC)
Puede usar RBAC toogrant sistema acceso tooauthorized usuarios, grupos y servicios mediante la asignación de roles con un nivel de recurso individual, el grupo de recursos o la suscripción. Cada rol define el nivel de acceso de hello que un usuario, un grupo o un servicio tiene sobre los recursos de la pila de Microsoft Azure.

RBAC de Azure tiene tres funciones básicas que se aplican a tipos de recursos de tooall: propietario, Colaborador y lector. Propietario tiene recursos de tooall de acceso completo incluido hello toodelegate derecho acceso tooothers. Colaborador puede crear y administrar todos los tipos de recursos de Azure, pero no se puede conceder acceso tooothers. El lector solo puede ver los recursos existentes de Azure. rest Hola de roles RBAC hello en Azure que admita la administración de recursos específicos de Azure. Por ejemplo, hello colaborador de la máquina Virtual rol permite la creación y administración de máquinas virtuales pero no permite la administración de red virtual de Hola o la subred de Hola que hello de la máquina virtual se conecta a.

## <a name="usage-data"></a>Datos de uso
Pila de Microsoft Azure recopila y agrega los datos de uso de todos los proveedores de recursos y los transmite tooAzure para su procesamiento por comercio de Azure. datos de uso de Hello recopilados en la pila de Azure pueden verse a través de una API de REST. Hay una API de inquilinos para Azure coherente, así como delegado API de proveedor y proveedor de datos de uso de tooget en todas las suscripciones de inquilinos. Estos datos pueden ser utilizado toointegrate con una herramienta externa o un servicio de facturación o de anulación. Una vez que se ha procesado el uso por comercio de Azure, puede verse en hello Azure portal de facturación.

## <a name="in-development-build-of-azure-stack-development-kit"></a>Compilación en desarrollo de Azure Stack Development Kit
Compilaciones de desarrollo permiten pioneros evaluar la versión más reciente de Hola de hello Kit de desarrollo de pila de Azure. Se trata de las generaciones incrementales en función de la versión principal más reciente de Hola. Mientras que las versiones principales continuará toobe libera cada pocos meses, compilaciones de hello en desarrollo se versión intermitentemente entre Hola principal libera.

Compilaciones de desarrollo proporcionará Hola siguientes ventajas:
- Corrección de errores
- Nuevas características
- Otra mejoras

## <a name="next-steps"></a>Pasos siguientes
[Implementar Azure Stack Development Kit](azure-stack-deploy.md)

