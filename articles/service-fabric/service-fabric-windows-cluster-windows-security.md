---
title: "aaaSecure un clúster se ejecuta en Windows mediante la seguridad de Windows | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure seguridad de nodo a nodo a y nodo de cliente en una independiente de clúster que se ejecuta en Windows mediante la seguridad de Windows."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>Proteger un clúster independiente en Windows mediante la seguridad de Windows
clúster de Service Fabric tooa de acceso no autorizado el tooprevent, debe proteger el clúster de Hola. Seguridad es especialmente importante al clúster Hola ejecuta cargas de trabajo de producción. Este artículo se describe cómo tooconfigure seguridad de nodo a nodo a y nodo de cliente utilizando la seguridad de Windows en hello *ClusterConfig.JSON* archivo.  proceso de Hello corresponde toohello configurar paso de seguridad de [crear un clúster independiente que se ejecute en Windows](service-fabric-cluster-creation-for-windows-server.md). Para más información sobre cómo Service Fabric usa la seguridad de Windows, consulte [Escenarios de seguridad de los clústeres](service-fabric-cluster-security.md).

> [!NOTE]
> Debe considerar detenidamente selección Hola de nodo a nodo seguridad porque no hay ninguna actualización de clúster desde un tooanother de opción de seguridad. selección de seguridad de toochange hello, deberá toorebuild Hola completo del clúster.
>
>

## <a name="configure-windows-security-using-gmsa"></a>Configuración de la seguridad de Windows mediante gMSA  
ejemplo de Hola a *ClusterConfig.gMSA.Windows.MultiMachine.JSON* descargar el archivo de configuración con hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. zip](http://go.microsoft.com/fwlink/?LinkId=730690) paquete de clúster independiente contiene una plantilla para la configuración de seguridad de Windows mediante [cuenta de servicio administrada de grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| **Opciones de configuración.** | **Descripción** |  
| --- | --- |  
| WindowsIdentities |Contiene las identidades de cliente y el clúster de Hola. |  
| ClustergMSAIdentity |Permite configurar la seguridad de nodo a nodo. Una cuenta de servicio administrada de grupo. |  
| ClusterSPN |SPN completo de dominio para la cuenta gMSA|  
| ClientIdentities |Permite configurar la seguridad de cliente a nodo. Una matriz de cuentas de usuario de cliente. |  
| Identidad |identidad del cliente Hello, un usuario de dominio. |  
| IsAdmin |True especifica que ese usuario de dominio de hello tiene acceso de cliente de administrador, false para el acceso de cliente de usuario. |  
  
[Seguridad de nodo toonode](service-fabric-cluster-security.md#node-to-node-security) se configura al establecer **ClustergMSAIdentity** cuando el tejido de servicio tiene toorun en gMSA. En orden toobuild las relaciones de confianza entre los nodos, deben realizar relacionados entre sí. Esto puede realizarse de dos maneras diferentes: especificar Hola grupo cuenta de servicio administrada que incluye todos los nodos de clúster de Hola o grupo Hola de máquina del dominio que incluye todos los nodos de clúster de Hola. Se recomienda encarecidamente usar hello [cuenta de servicio administrada de grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) enfoque, especialmente para clústeres más grandes (más de 10 nodos) o para los clústeres que son probable toogrow o se reducción.  
Este enfoque no requiere Hola de creación de un grupo de dominio para el que ha concedido tooadd de derechos de acceso a los administradores de clústeres y quitarán a miembros. Estas cuentas también son útiles para la administración automática de contraseñas. Para más información, consulte [Introducción a las cuentas de servicio administradas de grupo](http://technet.microsoft.com/library/jj128431.aspx).  
 
[Seguridad de cliente toonode](service-fabric-cluster-security.md#client-to-node-security) se configura mediante **ClientIdentities**. En orden tooestablish confianza entre un clúster de hello y cliente, debe configurar Hola clúster tooknow qué identidades de cliente que puede confiar. Esto puede hacerse de dos maneras diferentes: especifique los usuarios del grupo de dominio Hola que pueden conectarse o especificar Hola a los usuarios de nodo del dominio que se pueden conectar. Service Fabric admite dos tipos de control de acceso diferente para los clientes que están conectados tooa clúster de Service Fabric: administrador y usuario. Control de acceso permite Hola para hello clúster administrador toolimit acceso toocertain tipos de operaciones de clúster para los diferentes grupos de usuarios, mejorar la seguridad de clúster de Hola.  Los administradores tienen capacidades de toomanagement de acceso completa (incluidas las capacidades de lectura/escritura). Los usuarios, de forma predeterminada, tienen sólo capacidades de toomanagement de acceso de lectura (por ejemplo, capacidades de consulta) y las aplicaciones de tooresolve de capacidad de Hola y servicios. Para más información sobre los controles de acceso, consulte [Control de acceso basado en roles para clientes de Service Fabric](service-fabric-cluster-security-roles.md).  
 
Hola después ejemplo **seguridad** sección configura la seguridad de Windows que usan gMSA y especifica ese Hola máquinas en *ServiceFabric.clusterA.contoso.com* gMSA forman parte del clúster de Hola y que *CONTOSO\usera* tiene acceso de cliente de administración:  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a>Configuración de la seguridad de Windows mediante un grupo de máquinas  
ejemplo de Hola a *ClusterConfig.Windows.MultiMachine.JSON* descargar el archivo de configuración con hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. zip](http://go.microsoft.com/fwlink/?LinkId=730690) paquete de clúster independiente contiene una plantilla para configurar la seguridad de Windows.  Seguridad de Windows está configurada en hello **propiedades** sección: 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| **Opciones de configuración** | **Descripción** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType** se establece demasiado*Windows* si ClusterIdentity especifica un nombre de grupo de equipo de Active Directory. |  
| ServerCredentialType |Establecer demasiado*Windows* tooenable la seguridad de Windows para los clientes.<br /><br />Esto indica que los clientes de Hola de clúster de Hola y el propio clúster Hola se ejecuta dentro de un dominio de Active Directory. |  
| WindowsIdentities |Contiene las identidades de cliente y el clúster de Hola. |  
| ClusterIdentity |Utilice un nombre de grupo del equipo, domain\machinegroup, seguridad de nodo a nodo tooconfigure. |  
| ClientIdentities |Permite configurar la seguridad de cliente a nodo. Una matriz de cuentas de usuario de cliente. |  
| Identidad |Agregar usuario de dominio de hello, dominio ombre de usuario para la identidad del cliente Hola. |  
| IsAdmin |Conjunto tootrue toospecify que Hola de usuario de dominio no tiene acceso de cliente de administrador o false para el acceso de cliente de usuario. |  

[Seguridad de nodo toonode](service-fabric-cluster-security.md#node-to-node-security) se configura mediante el uso de la configuración **ClusterIdentity** si desea que toouse un grupo de equipo dentro de un dominio de Active Directory. Para más información, consulte el artículo [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx) (Creación de un grupo de máquinas en Active Directory).

La [seguridad de cliente a nodo](service-fabric-cluster-security.md#client-to-node-security) se configura mediante **ClientIdentities**. tooestablish confianza entre un clúster de hello y cliente, debe configurar Hola clúster tooknow Hola cliente pueden confiar en las identidades que Hola clúster. Puede establecer la confianza de dos maneras diferentes:

- Especificar usuarios Hola de grupo del dominio que se pueden conectar.
- Especificar usuarios Hola de nodo del dominio que se pueden conectar.

Service Fabric admite dos tipos de control de acceso diferente para los clientes que están conectados tooa clúster de Service Fabric: administrador y usuario. Control de acceso permite a Hola clúster administrador toolimit acceso toocertain los tipos de operaciones de clúster para los diferentes grupos de usuarios, lo que hace que el clúster de hello más segura.  Los administradores tienen capacidades de toomanagement de acceso completa (incluidas las capacidades de lectura/escritura). Los usuarios, de forma predeterminada, tienen sólo capacidades de toomanagement de acceso de lectura (por ejemplo, capacidades de consulta) y las aplicaciones de tooresolve de capacidad de Hola y servicios.  

Hola después ejemplo **seguridad** sección configura la seguridad de Windows, especifica que Hola máquinas en *ServiceFabric/clusterA.contoso.com* forman parte del clúster de Hola y especifica que  *CONTOSO\usera* tiene acceso de cliente de administración:

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> Service Fabric no debe implementarse en un controlador de dominio. Asegúrese de que ClusterConfig.json no incluye la dirección IP de Hola Hola del controlador de dominio cuando se usa un grupo de equipos o grupo cuentas de servicio administradas (gMSA).
>
>

## <a name="next-steps"></a>Pasos siguientes
Después de configurar la seguridad de Windows en hello *ClusterConfig.JSON* de archivos, reanudar el proceso de creación de clúster de hello en [crear un clúster independiente que se ejecute en Windows](service-fabric-cluster-creation-for-windows-server.md).

Para más información sobre la seguridad de nodo a nodo, la seguridad de cliente a nodo y el control de acceso basado en roles, consulte [Escenarios de seguridad de clúster](service-fabric-cluster-security.md).

Vea [clúster segura de conectar tooa](service-fabric-connect-to-secure-cluster.md) para obtener ejemplos de conectarse con PowerShell o FabricClient.
