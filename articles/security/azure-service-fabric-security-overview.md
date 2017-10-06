---
title: "Introducción a la seguridad aaaAzure service fabric | Documentos de Microsoft"
description: "Este artículo proporciona información general de seguridad de servicio de Azure fabric hello."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: ec5355983c5d59f4e0c3b855965f03ac47f1a4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-overview"></a>Introducción a la seguridad de Azure Service Fabric
[Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) es una plataforma de sistemas distribuidos que resulta fácil toopackage, implementar y administrar servicios de micro escalables y confiables. Service Fabric aborda retos significativos de hello en desarrollar y administrar aplicaciones en la nube. Los desarrolladores y administradores pueden evitar problemas complejos de infraestructura y centrarse en su lugar en las cargas de trabajo más exigentes y críticas que son escalables, confiables y fáciles de administrar.

En este artículo de información general de seguridad de Azure Service Fabric se centra en hello siguientes áreas:

-   Protección de su clúster
-   Supervisión y diagnóstico
-   Seguridad en el uso de certificados
-   Control de acceso basado en roles (RBAC)
-   Protección de un clúster mediante la seguridad de Windows
-   Configuración de la seguridad de la aplicación en Service Fabric
-   Protección de la comunicación de los servicios en la seguridad de Azure Service Fabric

## <a name="securing-your-cluster"></a>Protección de su clúster
Azure Service Fabric es organizador de servicios a través de un clúster de máquinas, clústeres deben ser segura tooprevent no autorizado a los usuarios conecten clúster tooyour, especialmente cuando tiene las cargas de trabajo de producción en ejecución. Aunque es posible toocreate un clúster no seguro, si lo hace, permite a los usuarios anónimos tooconnect tooit, si expone toohello de puntos de conexión de administración pública de Internet.

Esta sección proporciona información general del programa Hola a escenarios de seguridad para los clústeres que se ejecutan en Azure o independiente y Hola tooimplement de varias tecnologías que se usan esos escenarios. escenarios de seguridad de clúster de Hello son:

-   Seguridad de nodo a nodo
-   Seguridad de cliente a nodo

### <a name="node-to-node-security"></a>Seguridad de nodo a nodo
Protege la comunicación entre máquinas virtuales de Hola o las máquinas de clúster de Hola. Esto garantiza que sólo los equipos que son clústeres de hello toojoin autorizados pueden participar en hospedaje de aplicaciones y servicios en clúster de Hola.

Los clústeres que se ejecutan en Azure o los independientes que se ejecutan en Windows pueden utilizar una [seguridad basada en certificados](https://msdn.microsoft.com/library/ff649801.aspx) o la [seguridad de Windows](https://msdn.microsoft.com/library/ff649396.aspx) para las máquinas con Windows Server.

**Seguridad basada en certificados de nodo a nodo**

Service Fabric utiliza los certificados de servidor X.509 que especifique como parte de las configuraciones de tipo de nodo de hello cuando se crea un clúster. En este artículo, se proporciona una descripción rápida de qué son estos certificados y [cómo se pueden adquirir o crear](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates).

Seguridad de los certificados se configura al crear el clúster de hello ya sea a través del portal de Azure hello, plantillas del Administrador de recursos de Azure o una plantilla JSON independiente. Puede especificar un certificado principal y uno secundario opcional que se utiliza para la sustitución del certificado. Hello certificados principales y secundarios que especifique deben ser diferentes de cliente de administración de Hola y certificados de cliente de solo lectura que especifique para [seguridad del nodo de cliente](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security).

### <a name="client-to-node-security"></a>Seguridad de cliente a nodo
Seguridad de toonode de cliente se configura mediante identidades de cliente. tooestablish confianza entre un clúster de hello y cliente, debe configurar Hola clúster tooknow qué identidades de cliente que puede confiar. Esto puede hacerse de dos maneras:

-   Especifique los usuarios del grupo de dominio Hola que pueden conectarse o
-   Especificar usuarios Hola de nodo del dominio que se pueden conectar.

Tejido de servicio admite dos tipos de control de acceso diferente para los clientes que están conectados tooa clúster de Service Fabric:

-   Administrador
-   Usuario

Control de acceso permite Hola para hello clúster administrador toolimit acceso toocertain tipos de operaciones de clúster para los diferentes grupos de usuarios, mejorar la seguridad de clúster de Hola. Los administradores tienen capacidades de toomanagement de acceso completa (incluidas las capacidades de lectura/escritura). Los usuarios, de forma predeterminada, tienen sólo capacidades de toomanagement de acceso de lectura (por ejemplo, capacidades de consulta) y las aplicaciones de tooresolve de capacidad de Hola y servicios.

**Seguridad basada en certificados de cliente a nodo**

Seguridad de los certificados de cliente para el nodo se configura al crear el clúster de hello ya sea a través de hello portal de Azure, plantillas de administrador de recursos o una plantilla JSON independiente mediante la especificación de un certificado de cliente de administración o un certificado de cliente. Hola Administrador cliente y al usuario los certificados de cliente que especifique deben ser diferentes de certificados principales y secundarias de Hola que especifique para la seguridad de nodo a nodo.

Los clientes se conectan mediante Hola certificado de administración de clúster de toohello tienen capacidades de toomanagement de acceso completo. Los clientes se conectan clúster toohello mediante certificado de cliente de usuario de solo lectura de hello tienen solo las capacidades de toomanagement de acceso de lectura. En otras palabras que estos certificados se usan para hello rol basa el control de acceso (RBAC).

Para lee de Azure [configurar un clúster usando una plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) toolearn cómo tooconfigure certificado seguridad en un clúster.

**Seguridad de Azure Active Directory (AAD) de cliente a nodo en Azure**

Clústeres que se ejecutan en Azure también pueden proteger el acceso toohello extremos de administración con Azure Active Directory (AAD). Vea [configurar un clúster usando una plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) para obtener información sobre cómo toocreate Hola artefactos necesarios de AAD, cómo toopopulate ellas durante las operaciones de clúster creación y cómo tooconnect toothose clústeres posteriormente.

AAD permite a las organizaciones (conocidas como los inquilinos) toomanage usuario acceso tooapplications, que se dividen en las aplicaciones con un inicio de sesión basado en web interfaz de usuario y las aplicaciones con una experiencia de cliente nativo.

Un clúster de Service Fabric ofrece tooits de puntos de entrada varias funciones de administración, incluidos Hola basada en web Service Fabric Explorer y Visual Studio. Como resultado, crea dos AAD aplicaciones toocontrol acceso toohello clúster, una aplicación web y una aplicación nativa.
Para los clústeres de Azure, se recomienda usar los clientes tooauthenticate de seguridad AAD y certificados para la seguridad de nodo a nodo.

Para los clústeres Windows Server independientes, se recomienda que utilice la seguridad de Windows con las cuentas administradas de grupo (GMA) si tiene Windows Server 2012 R2 y Active Directory. De lo contrario, use la seguridad de Windows con cuentas de Windows.

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Supervisión y diagnóstico para Azure Service Fabric
[Supervisión y diagnóstico](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview) son crítico toodeveloping, prueba e implementación de aplicaciones y servicios en cualquier entorno. Las soluciones de Service Fabric funcionan mejor cuando diseña e implementa la supervisión y el diagnóstico que ayudan a asegurarse de que las aplicaciones y los servicios funcionen según lo previsto en un entorno de desarrollo local o en producción.

Desde la perspectiva de seguridad, Hola objetivos principales de supervisión y diagnóstico es para:

-   Detectar y diagnosticar problemas de hardware y la infraestructura que podrían ser debido a los eventos de seguridad de tooa.
-   Detectar problemas de software y de aplicaciones que podrían proporcionar el indicador de riesgo (IoC).
-   Comprender los recursos consumo toohelp evitar involuntario de denegación de servicio.

Hola de flujo de trabajo general de supervisión y diagnóstico consta de tres pasos:

-   **Generación de eventos:** Esto incluye los eventos (registros, seguimientos de eventos personalizados) en la infraestructura de hello (clúster) y el nivel de aplicación / servicio. Obtenga más información sobre [eventos de nivel de infraestructura](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra) y [eventos de nivel de aplicación](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app) toounderstand lo que se proporciona y cómo tooadd más Instrumental.
-   **Agregación de eventos:** eventos generados necesitan toobe recopilan y se agregan antes de que se pueden mostrar. Normalmente, se recomienda usar [diagnósticos de Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad) (colección de registro basado en tooagent más similar) o [EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) (en-proceso de recopilación de registros).
-   **Análisis:** eventos necesitan toobe visualizado y esté accesible en algún formato, tooallow para su análisis y visualización según sea necesario. Hay varias plataformas excelentes que existen en el mercado de hello cuando se trata de toohello análisis y la visualización de datos de supervisión y diagnóstico. Hello dos que recomendamos son [OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms) y [Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights) debido tootheir una mejor integración con Service Fabric.

También puede usar [Monitor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) toomonitor muchas de Hola recursos de Azure en el que se crea un clúster de Service Fabric.

A continuación se proporciona es un servicio independiente que se puede ver el estado y la carga entre los servicios y el estado del informe para cualquier elemento de jerarquía del modelo de mantenimiento de Hola. Esto puede ayudar a evitar errores que no se detectan basados en la vista de Hola de un único servicio. Watchdogs también son un buena colocar el código toohost que lleva a cabo acciones correctoras sin interacción del usuario (por ejemplo, limpiar los archivos de registro de almacenamiento a determinados intervalos de tiempo). [Aquí](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/) puede encontrar la implementación de un servicio guardián de ejemplo.

## <a name="secure-using-certificates"></a>Seguridad en el uso de certificados
Uso de certificados, se indica cómo toosecure Hola comunican Hola varios nodos de un clúster de Windows independiente, así como el modo clientes tooauthenticate que se conectan clúster toothis, mediante certificados X.509. Esto garantiza que sólo los usuarios autorizados pueden tener acceso a los clúster hello, hello las aplicaciones implementadas y realizar tareas de administración. Seguridad de certificado debe estar habilitado en clúster de hello cuando se crea un clúster Hola.

### <a name="x509-certificates-and-service-fabric"></a>Certificados X.509 y Service Fabric
Los certificados digitales X.509 son servidores y clientes de tooauthenticate utilizadas y tooencrypt y firmar digitalmente los mensajes.

Hello tabla siguiente enumeran los certificados de Hola que necesita la configuración de clúster:

|Configuración de la información de certificado |Descripción|
|-------------------------------|-----------|
|ClusterCertificate|    Este certificado es necesario toosecure Hola comunicación entre los nodos de hello en un clúster. Puede utilizar dos certificados diferentes, uno principal y otro secundario para la actualización.|
|ServerCertificate| Este certificado se presenta a toohello cliente cuando intente tooconnect toothis clúster. Puede utilizar dos certificados de servidor diferentes, uno principal y otro secundario para la actualización.|
|ClientCertificateThumbprints|  Se trata de un conjunto de certificados que desea tooinstall en los clientes de hello autenticado.|
|ClientCertificateCommonNames|  Establecer nombre común Hola Hola primera del certificado de cliente para hello CertificateCommonName. Hola CertificateIssuerThumbprint es huella de hello certificado de emisor de Hola de este certificado.|
|ReverseProxyCertificate|   Se trata de un certificado opcional que se puede especificar si desea que toosecure su [un Proxy inverso](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).|

Para más información sobre cómo proteger los certificados, [haga clic aquí](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security).

## <a name="role-based-access-control-rbac"></a>Control de acceso basado en roles (RBAC)
Control de acceso permite Hola clúster administrador toolimit acceso toocertain las operaciones del clúster para los diferentes grupos de usuarios, mejorar la seguridad de clúster de Hola. Se admiten dos tipos de control de acceso diferente para clientes que se conectan tooa clúster: rol de administrador y el rol de usuario.

Los administradores tienen capacidades de toomanagement de acceso completa (incluidas las capacidades de lectura/escritura). Los usuarios, de forma predeterminada, tienen sólo capacidades de toomanagement de acceso de lectura (por ejemplo, capacidades de consulta) y las aplicaciones de tooresolve de capacidad de Hola y servicios.

Especificado los roles de cliente de administrador y usuario de hello en el tiempo de Hola de creación del clúster proporcionando identidades diferentes (certificados, etc. AAD) para cada uno. Para obtener más información sobre la configuración predeterminada de control de acceso de Hola y cómo toochange Hola valores predeterminados, consulte [el control de acceso basado en roles para los clientes de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

## <a name="secure-standalone-cluster-using-windows-security"></a>Protección de un clúster independiente mediante la seguridad de Windows
clúster de Service Fabric tooa de acceso no autorizado el tooprevent, debe proteger el clúster de Hola. Seguridad es especialmente importante al clúster Hola ejecuta cargas de trabajo de producción. Describe cómo tooconfigure seguridad de nodo a nodo a y nodo de cliente utilizando la seguridad de Windows en Hola archivo ClusterConfig.JSON.

**Configuración de la seguridad de Windows mediante gMSA**

Seguridad de toonode de nodo se configura al establecer [ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security) cuando el tejido de servicio tiene toorun en gMSA. En orden toobuild las relaciones de confianza entre los nodos, deben realizar relacionados entre sí.

Seguridad de toonode de cliente se configura mediante ClientIdentities. En orden tooestablish confianza entre un clúster de hello y cliente, debe configurar Hola clúster tooknow qué identidades de cliente que puede confiar.

**Configuración de la seguridad de Windows mediante un grupo de máquinas**

Seguridad de toonode de nodo se configura estableciendo con ClusterIdentity si desea que toouse un grupo de equipo dentro de un dominio de Active Directory. Para más información, consulte el artículo [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347) (Creación de un grupo de máquinas en Active Directory).

La seguridad de cliente a nodo se configura mediante ClientIdentities. tooestablish confianza entre un clúster de hello y cliente, debe configurar Hola clúster tooknow Hola cliente pueden confiar en las identidades que Hola clúster. Puede establecer la confianza de dos maneras diferentes:

-   Especificar usuarios Hola de grupo del dominio que se pueden conectar.
-   Especificar usuarios Hola de nodo del dominio que se pueden conectar.

## <a name="configure-application-security-in-service-fabric"></a>Configuración de la seguridad de la aplicación en Service Fabric
### <a name="managing-secrets-in-service-fabric-applications"></a>Administración de secretos en aplicaciones de Service Fabric
Este método ayuda a administrar secretos en una aplicación de Service Fabric. Los secretos pueden ser cualquier información confidencial, como cadenas de conexión de almacenamiento, contraseñas u otros valores que no se deben administrar en texto sin formato.

Este enfoque utiliza [el almacén de claves de Azure](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) toomanage claves y secretos. Sin embargo, con secretos en una aplicación está en la nube independiente de la plataforma tooallow aplicaciones toobe implementa tooa clúster hospedado en cualquier lugar. Hay cuatro pasos principales en este flujo:

-   Obtener un certificado de cifrado de datos.
-   Instalar certificado de hello en el clúster.
-   Cifrar valores secretos al implementar una aplicación con el certificado de Hola y se insertan en el archivo de configuración de un servicio Settings.xml.
-   Valores de lectura cifrado fuera Settings.xml mediante el descifrado con Hola mismo certificado de cifrado.

>[!Note]
>Más información sobre cómo [administrar secretos en aplicaciones de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="configure-security-policies-for-your-application"></a>Configuración de directivas de seguridad para la aplicación
Mediante la seguridad de tejido de servicio de Azure, puede ayudar a aplicaciones seguras que se ejecutan en el clúster de hello en distintas cuentas de usuario. Seguridad del servicio de Fabric también ayuda a certificados, archivos, directorios y recursos de hello segura que se usan las aplicaciones en tiempo de Hola de implementación con cuentas de usuario de hello, por ejemplo. Esto aumenta la seguridad entre aplicaciones en ejecución, incluso en un entorno hospedado compartido.
Hola pasos incluyen:

-   Configurar la directiva de Hola para un punto de entrada del programa de instalación de servicio.
-   Inicio de comandos de PowerShell desde un punto de entrada de configuración.
-   Uso de la redirección de la consola para la depuración local.
-   Configuración de una directiva para los paquetes de código del servicio.
-   Asignación de una directiva de acceso de seguridad a los puntos de conexión HTTP y HTTPS.

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>Protección de la comunicación de los servicios en la seguridad de Azure Service Fabric
La seguridad es uno de los aspectos más importantes de Hola de comunicación. marco de aplicación de servicios de confianza de Hello proporciona unos pilas de la comunicación creada previamente y herramientas que pueden ser tooimprove usa seguridad.

-   [Ayuda para proteger un servicio cuando usa la comunicación remota para los servicios](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication).
-   [Ayuda para proteger un servicio cuando se utiliza una pila de comunicación basada en WCF](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack).

## <a name="next-steps"></a>Pasos siguientes
- Para obtener información conceptual acerca de la seguridad de los clústeres, consulte [Creación de un clúster de Service Fabric con Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) y [Azure Portal](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal).
- Para más información, consulte [Escenarios de seguridad de los clústeres de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security).
