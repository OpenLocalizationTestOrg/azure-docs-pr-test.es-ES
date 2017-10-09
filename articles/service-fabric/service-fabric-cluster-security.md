---
title: "un clúster de Service Fabric aaaSecure | Documentos de Microsoft"
description: "Estos escenarios se describen escenarios de seguridad de Hola para un tooimplement de diferentes tecnologías que se usan de hello y clúster de Service Fabric."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.openlocfilehash: 249a9e85b8fbe174e2accee85a94d95b2872a3af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>Escenarios de seguridad de los clústeres de Service Fabric
Un clúster de Service Fabric es un recurso que usted posee. Clústeres deben ser segura tooprevent no autorizado a los usuarios conecten clúster tooyour, especialmente cuando tiene las cargas de trabajo de producción en ejecución. Aunque es posible toocreate un clúster no seguro, si lo hace, permite a los usuarios anónimos tooconnect tooit, si expone toohello de puntos de conexión de administración pública de Internet. 

Este artículo proporciona información general del programa Hola a escenarios de seguridad para los clústeres que se ejecutan en Azure o independiente y Hola tooimplement de varias tecnologías que se usan esos escenarios. escenarios de seguridad de clúster de Hello son:

* Seguridad de nodo a nodo
* Seguridad de cliente a nodo
* Control de acceso basado en roles (RBAC)

## <a name="node-to-node-security"></a>Seguridad de nodo a nodo
Protege la comunicación entre máquinas virtuales de Hola o las máquinas de clúster de Hola. Esto garantiza que sólo los equipos que son clústeres de hello toojoin autorizados pueden participar en hospedaje de aplicaciones y servicios en clúster de Hola.

![Diagrama de comunicación de nodo a nodo][Node-to-Node]

Los clústeres que se ejecutan en Azure o los independientes que se ejecutan en Windows pueden utilizar una [seguridad basada en certificados](https://msdn.microsoft.com/library/ff649801.aspx) o la [seguridad de Windows](https://msdn.microsoft.com/library/ff649396.aspx) para las máquinas con Windows Server.

### <a name="node-to-node-certificate-security"></a>Seguridad basada en certificados de nodo a nodo
Service Fabric utiliza los certificados de servidor X.509 que especifique como parte de las configuraciones de tipo de nodo de hello cuando se crea un clúster. Se proporciona una introducción rápida de estos certificados son y cómo puede adquirir o crearlos final Hola de este artículo.

Seguridad de los certificados se configura al crear el clúster de hello ya sea a través del portal de Azure hello, plantillas del Administrador de recursos de Azure o una plantilla JSON independiente. Puede especificar un certificado principal y uno secundario opcional que se utiliza para la sustitución del certificado. Hello certificados principales y secundarios que especifique deben ser diferentes de cliente de administración de Hola y certificados de cliente de solo lectura que especifique para [seguridad del nodo de cliente](#client-to-node-security).

Para lee de Azure [configurar un clúster usando una plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) toolearn cómo tooconfigure certificado seguridad en un clúster.

Para Windows Server de modo independiente, lea [Protección de un clúster de Windows independiente mediante certificados ](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>Seguridad de Windows de nodo a nodo
Para Windows Server de modo independiente, lea [Protección de un clúster independiente en Windows mediante la seguridad de Windows](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>Seguridad de cliente a nodo
Autentica a los clientes y protege la comunicación entre un cliente y los nodos individuales en el clúster de Hola. Este tipo de seguridad se autentica y protege la comunicación de cliente, lo que garantiza que sólo los usuarios autorizados puedan acceder a clúster de Hola y aplicaciones de hello implementadas en clúster de Hola. Los clientes se identifican exclusivamente mediante sus credenciales de seguridad de Windows o las credenciales de seguridad del certificado.

![Diagrama de comunicación de cliente a nodo][Client-to-Node]

Los clústeres que se ejecutan en Azure o los independientes que se ejecutan en Windows pueden utilizar una [seguridad basada en certificados](https://msdn.microsoft.com/library/ff649801.aspx) o la [seguridad de Windows](https://msdn.microsoft.com/library/ff649396.aspx).

### <a name="client-to-node-certificate-security"></a>Seguridad basada en certificados de cliente a nodo
 Seguridad de los certificados de cliente para el nodo se configura al crear el clúster de hello ya sea a través del portal de Azure hello, plantillas de administrador de recursos o una plantilla JSON independiente mediante la especificación de un certificado de cliente de administración o un certificado de cliente.  Hello Administrador cliente y al usuario los certificados de cliente que especifique deben ser diferentes de hello principal y secundarios certificados que especifique para [seguridad de nodo a nodo](#node-to-node-security) como procedimiento recomendado. De forma predeterminada, los certificados de clúster de hello para la seguridad de nodo a nodo se agregan toohello permitida a cliente lista de certificados de administración.

Los clientes se conectan mediante Hola certificado de administración de clúster de toohello tienen capacidades de toomanagement de acceso completo.  Los clientes se conectan clúster toohello mediante certificado de cliente de usuario de solo lectura de hello tienen solo las capacidades de toomanagement de acceso de lectura. En otras palabras, estos certificados se usan para hello bases de datos de control de acceso roles (RBAC) se describe más adelante en este artículo.

Para lee de Azure [configurar un clúster usando una plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) toolearn cómo tooconfigure certificado seguridad en un clúster.

Para Windows Server de modo independiente, lea [Protección de un clúster de Windows independiente mediante certificados ](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Seguridad de Azure Active Directory (AAD) de cliente a nodo en Azure
Clústeres que se ejecutan en Azure también pueden proteger el acceso toohello extremos de administración con Azure Active Directory (AAD). Vea [configurar un clúster usando una plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) para obtener información sobre cómo toocreate Hola artefactos necesarios de AAD, cómo toopopulate ellas durante las operaciones de clúster creación y cómo tooconnect toothose clústeres posteriormente.

## <a name="security-recommendations"></a>Recomendaciones de seguridad
Para los clústeres de Azure, se recomienda usar los clientes tooauthenticate de seguridad AAD y certificados para la seguridad de nodo a nodo.

Para los clústeres Windows Server independientes, se recomienda que utilice la seguridad de Windows con las cuentas administradas de grupo (GMA) si tiene Windows Server 2012 R2 y Active Directory. De lo contrario, use la seguridad de Windows con cuentas de Windows.

## <a name="role-based-access-control-rbac"></a>Control de acceso basado en roles (RBAC)
Control de acceso permite Hola clúster administrador toolimit acceso toocertain las operaciones del clúster para los diferentes grupos de usuarios, mejorar la seguridad de clúster de Hola. Se admiten dos tipos de control de acceso diferente para clientes que se conectan tooa clúster: rol de administrador y el rol de usuario.

Los administradores tienen capacidades de toomanagement de acceso completa (incluidas las capacidades de lectura/escritura). Los usuarios, de forma predeterminada, tienen sólo capacidades de toomanagement de acceso de lectura (por ejemplo, capacidades de consulta) y las aplicaciones de tooresolve de capacidad de Hola y servicios.

Especificado los roles de cliente de administrador y usuario de hello en el tiempo de Hola de creación del clúster proporcionando identidades diferentes (certificados, etc. AAD) para cada uno. Para obtener más información sobre la configuración predeterminada de control de acceso de Hola y cómo toochange Hola valores predeterminados, consulte [el control de acceso basado en roles para los clientes de Service Fabric](service-fabric-cluster-security-roles.md).

## <a name="x509-certificates-and-service-fabric"></a>Certificados X.509 y Service Fabric
Los certificados digitales X.509 son servidores y clientes de tooauthenticate utilizadas y tooencrypt y firmar digitalmente los mensajes. Para obtener más detalles sobre estos certificados, vaya demasiado[trabajar con certificados](http://msdn.microsoft.com/library/ms731899.aspx).

Algunos tooconsider aspectos importantes:

* Los certificados usados en clústeres que ejecutan cargas de trabajo de producción deberán crearse mediante un servicio de certificados de Windows Server correctamente configurado u obtenerse de una [entidad de certificación (CA)](https://en.wikipedia.org/wiki/Certificate_authority)autorizada.
* No use nunca certificados temporales o de pruebas en producción creados con herramientas como MakeCert.exe.
* Puede usar un certificado autofirmado, pero solo para los clústeres de prueba y no para los que se encuentran en fase de producción.

### <a name="server-x509-certificates"></a>Certificados de servidor X.509
Certificados de servidor tienen la tarea principal de hello de autenticar un servidor (nodo) tooclients o autenticar un servidor de servidor (nodo) tooa (nodo). Una de las comprobaciones iniciales de hello cuando un nodo o un cliente se autentica un nodo es el valor de Hola de toocheck de nombre común de hello en el campo de asunto Hola. Este nombre común o uno de los nombres alternativos del firmante de los certificados Hola debe encontrarse en la lista de Hola de nombres comunes permitidos.

Hello siguiente artículo describe cómo toogenerate certificados con nombres alternativos del firmante (SAN): [cómo tooadd un tooa de nombre alternativo de sujeto proteger certificado LDAP](http://support.microsoft.com/kb/931351).

campo de asunto Hola puede contener varios valores, cada uno prefijado con un tipo de valor de inicialización tooindicate Hola. Normalmente, la inicialización de hello es "CN" nombre común; Por ejemplo, "CN = www.contoso.com". También es posible hello toobe de campo de asunto en blanco. Si se rellena el campo de nombre alternativo del sujeto opcional hello, debe contener nombre común de hello del certificado de hello y una entrada por cada nombre alternativo del sujeto. Estos se especifican como valores de nombre DNS.

valor de Hello del campo de propósitos planteados de hello del certificado de hello debe incluir un valor apropiado, como "Autenticación de servidor" o "Autenticación de cliente".

### <a name="client-x509-certificates"></a>Certificados de cliente X.509
Los certificados de cliente normalmente no los emite una entidad de certificación de terceros. En su lugar, hello almacén Personal de la ubicación del usuario actual Hola normalmente contiene certificados de cliente colocados ahí por una entidad emisora raíz, con un propósito planteado de "Autenticación de cliente". cliente de Hello puede utilizar este tipo de certificado cuando se requiere autenticación mutua.

> [!NOTE]
> Todas las operaciones de administración en el clúster de Service Fabric requieren certificados de servidor. No se pueden usar certificados de cliente para la administración.
> 
> 

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->


## <a name="next-steps"></a>Pasos siguientes
En este artículo se proporciona información conceptual sobre la seguridad de los clústeres. Después,


1.  [cree un clúster en Azure con una plantilla de Resource Manager](service-fabric-cluster-creation-via-arm.md) 
2.  [Azure Portal](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
