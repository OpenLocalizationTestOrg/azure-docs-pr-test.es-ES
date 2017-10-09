---
title: "prácticas recomendadas de seguridad de Service Fabric de aaaAzure | Documentos de Microsoft"
description: "En este artículo se proporciona un conjunto de procedimientos recomendados para la reforzar la seguridad de Azure Service Fabric."
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
ms.openlocfilehash: 483a21240da17d56bb4641653093ddcbad379d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-best-practices"></a>Procedimientos recomendados de seguridad de Azure Service Fabric
La implementación de una aplicación en Azure es un proceso rápido, sencillo y rentable. Antes de implementar la aplicación en la nube en producción útil toohave una práctica recomendada tooassist en la evaluación de la aplicación en una lista de prácticas recomendadas esenciales y recomendadas.

Azure Service Fabric es una plataforma de sistemas distribuidos que resulta fácil toopackage, implementar y administrar microservicios escalables y confiables. Service Fabric también aborda retos significativos de hello en desarrollar y administrar aplicaciones en la nube. Los desarrolladores y administradores pueden evitar problemas complejos de infraestructura y centrarse en su lugar en las cargas de trabajo más exigentes y críticas que son escalables, confiables y fáciles de administrar. 

Para cada procedimiento recomendado, explicaremos:

-   ¿Qué recomienda Hola
-   ¿Por qué desea tooenable este procedimiento recomendado
-   ¿Qué podría ser resultado de hello si no se recomienda tooenable Hola
-   ¿Cómo puede obtener información práctica recomendada de hello tooenable

Actualmente tenemos Hola procedimientos recomendados de seguridad de Azure Service Fabric:

-   Utilizar una plantilla de Manager(ARM) de recursos de Azure y clúster de módulo de PowerShell de Azure Service Fabric toocreate segura
-   Uso de certificados X.509
-   Configuración de directivas de seguridad
-   Configuración de seguridad de Reliable Actors
-   Configuración de SSL para Azure Service Fabric
-   Aislamiento y seguridad de red con Azure Service Fabric
-   Configuración de un almacén de claves de seguridad
-   Asignar usuarios tooroles


## <a name="best-practices-for-securing-your-cluster"></a>Procedimientos recomendados para proteger el clúster

**Idea general**

Use siempre un clúster seguro
-   Seguridad del clúster: uso de certificados
-   Acceso de cliente (solo lectura y administración): uso de AAD

Use implementaciones automatizadas
-   Usar secuencias de comandos toogenerate, implementar y escribirse secretos
-   Mantener secretos de hello en KV, use AD para todos los otros accesos de cliente
-   Ningún usuario debe tener toothem acceso sin autenticación.

Además, tenga en cuenta los siguiente de hello:
-   Cree zonas desmilitarizadas con grupos de seguridad de red (NSG)
-   Utilizar tooRDP de servidores de salto en máquinas virtuales de clúster o toomanage su clúster

Clústeres deben ser segura tooprevent no autorizado a los usuarios conecten clúster tooyour, especialmente cuando tiene las cargas de trabajo de producción en ejecución. Aunque es posible toocreate un clúster no seguro, si lo hace, permite a los usuarios anónimos tooconnect tooit, si expone toohello de puntos de conexión de administración pública de Internet.

Usar tecnologías tooimplement esos escenarios. Hola [los escenarios de seguridad de clúster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) son:

-   Nodo a nodo seguridad: esta protege la comunicación entre equipos en clúster de Hola y Hola máquinas virtuales. Esto garantiza que sólo los equipos que son clústeres de hello toojoin autorizados pueden participar en hospedaje de aplicaciones y servicios en clúster de Hola.
Los clústeres que se ejecutan en Azure o los independientes que se ejecutan en Windows pueden utilizar una [seguridad basada en certificados](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security) o la [seguridad de Windows](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-windows-security) para las máquinas con Windows Server.
-   Nodo de cliente seguridad This protege la comunicación entre un cliente de Service Fabric y los nodos individuales en el clúster de Hola.
-   Control de acceso basado en roles (RBAC) - especificar los roles de cliente de administrador y usuario de hello en tiempo de Hola de creación del clúster proporcionando identidades diferentes (certificados, etc. AAD) para cada uno.
-   Recomendaciones de seguridad-clústeres de Azure, se recomienda usar los clientes tooauthenticate de seguridad AAD y certificados para la seguridad de nodo a nodo.

tooconfigure Hola independiente clúster de Windows, vea [configurar configuración de clúster de windows independiente](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest).

Usar plantillas del Administrador de recursos de Azure y clúster de módulo de PowerShell de Azure Service Fabric toocreate segura.
[Aquí](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) hay disponible una guía paso a paso que le dirige en la configuración de un clúster seguro de Azure Service Fabric en Azure con Azure Resource Manager.

Utilizar hello Azure Resource Manager plantilla toocustomize su clúster
-   Almacenamiento administrado por el programa de instalación de discos duros virtuales de máquinas virtuales

Usar hello Azure Resource Manager plantilla toodrive cambios tooyour grupo de recursos
-   Fácil administración de la configuración
-   Auditoría

Trate la configuración del clúster como código
-   Ser exhaustiva en la comprobación de las configuraciones de hello elija toodeploy
-   Evite el uso de comandos implícita tootweak los recursos directamente

Muchos aspectos de hello [ciclo de vida de aplicación de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-lifecycle) puede automatizarse. El [módulo Microsoft Azure Powershell de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications#upload-the-application-package) automatiza las tareas comunes para implementar, actualizar, quitar y probar aplicaciones de Azure Service Fabric. También cuenta con API HTTP y administradas para la administración de aplicaciones.

## <a name="use-x509-certificates"></a>Uso de certificados X.509
Los clústeres siempre deben protegerse mediante certificados X.509 o con la seguridad de Windows. Solo se configura con seguridad en el momento de creación de clúster y no es posible tooenable seguridad después de crear el clúster de Hola.

Si va a especificar una [certificado de clúster](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security), establecer valor de Hola de ClusterCredentialType tooX509. Si va a especificar el certificado de servidor para conexiones externas, establezca hello ServerCredentialType tooX509.

-   Los certificados usados en clústeres que ejecutan cargas de trabajo de producción deberán crearse mediante un servicio de certificados de Windows Server correctamente configurado u obtenerse de una entidad de certificación (CA) autorizada.
-   No use nunca certificados temporales o de pruebas en producción creados con herramientas como MakeCert.exe.
-   Puede usar un certificado autofirmado, pero solo para los clústeres de prueba y no para los que se encuentran en fase de producción.

Si el clúster de hello no es seguro. Cualquiera puede conectarse de forma anónima y realizar operaciones de administración, por lo que los clústeres de producción siempre deben protegerse mediante certificados X.509 o la seguridad de Windows.

toolearn más cómo ver certificados tooenable en clúster de service fabric, [agregar o quitar certificados para un clúster de service fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure).

## <a name="configure-security-policies"></a>Configuración de directivas de seguridad
Service Fabric también ayuda a certificados, archivos, directorios y recursos de hello segura que se usan las aplicaciones en tiempo de Hola de implementación con cuentas de usuario de hello, por ejemplo. Esto aumenta la seguridad entre aplicaciones en ejecución, incluso en un entorno hospedado compartido.

-   Usar un usuario o grupo de dominio de Active Directory: puede ejecutar el servicio de hello con credenciales de Hola para una cuenta de usuario o grupo de Active Directory. Esto se aplica a Active Directory local dentro del dominio y no a Azure Active Directory (AAD). Mediante el uso de un grupo o usuario de dominio, a continuación, puede tener acceso a otros recursos de dominio de hello (por ejemplo, recursos compartidos de archivos) que se han concedido permisos.

-   Asignar una directiva de acceso de seguridad para los extremos HTTP y HTTPS: si aplica un servicio de tooa de directiva de ejecución y el manifiesto del servicio de hello declara los recursos de punto de conexión con protocolo de hello HTTP, debe especificar un tooensure SecurityAccessPolicy que los puertos asignan toothese los extremos están correctamente con control de acceso aparecen para la cuenta de usuario de ejecución que se ejecuta el servicio de Hola Hola. En caso contrario, http.sys no tiene acceso toohello servicio y obtener errores con llamadas de cliente de Hola.
toolearn más habilitar directivas de seguridad de servicio, vea tejido [configurar directivas de seguridad para la aplicación](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-runas-security).

## <a name="reliable-actors-security-configuration"></a>Configuración de seguridad de Reliable Actors
Servicio Fabric Reliable Actors es una implementación del patrón de diseño de hello actor. Al igual que con cualquier modelo de diseño de software, decisión Hola si toouse un patrón específico estará en función de si un software diseñe problema encaja patrón Hola.

Como guía general, considere la posibilidad de hello actor patrón toomodel su problema o escenario si:
-   El espacio del problema implica un gran número (miles o más) de unidades pequeñas, independientes y aisladas de estado y lógica.
-   Desea toowork con objetos de un único subproceso que no requieren interacción importante de los componentes externos, incluidas las consultas de estado a través de un conjunto de actores.
-   Las instancias de actor no bloquearán a los autores de llamadas con retrasos imprevisibles emitiendo operaciones de E/S.

En Service Fabric, actores se implementan en el marco de trabajo de hello Reliable Actors: un marco de trabajo de aplicaciones basados en el patrón de actor construido sobre [servicios confiables de tejido de servicio](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction). Cada servicio de Reliable Actors que escribe es en realidad un servicio de confianza con estado particionado.
Cada actor se define como una instancia de un tipo de actor, toohello idéntica forma un objeto .NET es una instancia de un tipo. NET. Por ejemplo, puede haber un tipo de actor que implementa la funcionalidad de Hola de una calculadora y podría haber muchos actores de ese tipo que se distribuyen en varios nodos en un clúster. Cada uno de esos actores se identifica de forma única mediante un identificador de actor.

[Las configuraciones de seguridad de Replicador](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-kvsactorstateprovider-configuration) son el canal de comunicación de hello toosecure utilizado que se usa durante la replicación. Esto significa que los servicios no pueden ver sus respectivas tráfico de replicación, garantizar que los datos de Hola que ofrezca alta disponibilidad también están seguros. De forma predeterminada, una sección de configuración de seguridad vacía impide la seguridad de la replicación.
Las configuraciones de Replicador configurar Replicador de Hola que se encarga de hacer que el estado del proveedor de estado de Actor Hola gran confiabilidad.

## <a name="configure-ssl-for-azure-service-fabric"></a>Configuración de SSL para Azure Service Fabric

Autenticación de servidor: [autentica](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) Hola cliente de administración de tooa de puntos de conexión de la administración de clúster, por lo que hello administración cliente sabe está hablando clúster real toohello. Este certificado también proporciona un [SSL](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) para hello API de administración de HTTPS y para el Explorador de Service Fabric a través de HTTPS.
Debe adquirir un nombre de dominio personalizado para el clúster. Cuando solicite un certificado de una entidad de certificación, hello nombre de sujeto del certificado debe coincidir con nombre de dominio personalizado de Hola que usa para el clúster.

tooconfigure SSL para una aplicación, primero debe tooget un certificado SSL firmado por una entidad de certificación (CA), un tercero de confianza que emite certificados para este propósito. Si no ya tiene una, deberá tooobtain de una compañía que venda certificados SSL.

certificado de Hello debe cumplir Hola según los requisitos para los certificados SSL en Azure:
-   certificado de Hello debe contener una clave privada.
-   certificado de Hello debe crearse para el intercambio de claves, exportable tooa archivo de intercambio de información Personal (.pfx).
-   Hello nombre de sujeto del certificado debe coincidir con servicio de nube de hello dominio utilizado tooaccess Hola. No se puede obtener un certificado SSL de una entidad de certificación (CA) para el dominio de cloudapp.net Hola. Debe adquirir una toouse de nombre de dominio personalizado al tener acceso al servicio. Cuando solicite un certificado de una entidad de certificación, nombre de sujeto del certificado de hello debe coincidir con tooaccess de usa el nombre de dominio personalizado de Hola la aplicación. Por ejemplo, si su nombre de dominio personalizado es contoso.com, solicitaría un certificado a su entidad de certificación para **.contoso.com** o **www.contoso.com.**
-   certificado de Hello debe usar un mínimo de cifrado de 2048 bits.

HTTP es inseguro y está sujeto tooeavesdropping ataques porque hello datos que se transfieren desde el servidor web toohello de hello web explorador o entre otros puntos de conexión, se transmite como texto simple. Esto significa que los atacantes pueden interceptar y ver datos confidenciales, como los detalles de las tarjetas de crédito e inicios de sesión de cuenta. Cuando los datos se envían o se publican a través de un explorador mediante HTTPS, SSL garantiza que esa información se cifre y esté a salvo de la interceptación.

más información, vea toolearn, [configurar SSL para la aplicación de azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate).

## <a name="network-isolationsecurity-with-azure-service-fabric"></a>Aislamiento y seguridad de red con Azure Service Fabric
Use [plantilla de Azure Resource Manager (ARM)](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) como ejemplo para configurar un valor de nodetype tres clúster segura y toocontrol Hola tráfico de red entrante y saliente con grupos de seguridad de red.

plantilla de Hello tiene un grupo de seguridad de red para cada uno de hello escala set(VMSS) toocontrol Hola tráfico las máquinas virtuales dentro y fuera de hello VMSS. De forma predeterminada, las reglas de hello configuradas tooallow que todos Hola tráfico necesario Hola sistema hello y servicios de puertos de la aplicación especificados en la plantilla de Hola. Revisar estas reglas y realizar cambios toofit sus necesidades, incluidas agregar nuevos archivos para las aplicaciones.

Para más información, consulte [Azure Service Fabric: escenarios comunes de redes](https://docs.microsoft.com/azure/service-fabric/service-fabric-patterns-networking).

## <a name="set-up-a-key-vault-for-security"></a>Configuración de un almacén de claves de seguridad
Los certificados se utilizan en toosecure de autenticación y cifrado de Service Fabric tooprovide diversos aspectos de un clúster y sus aplicaciones.

Service Fabric utiliza certificados X.509 toosecure un clúster y proporcionar características de seguridad de la aplicación. Usar el almacén de claves demasiado[administrar certificados](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure) para clústeres de Service Fabric en Azure. Cuando se implementa un clúster de Azure, proveedor de recursos de Azure de Hola que es responsable de la creación de clústeres de Service Fabric extrae los certificados de almacén de claves y los instala en clúster de hello las máquinas virtuales.

Hola relación entre [el almacén de claves de Azure](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), un clúster de service fabric y el proveedor de recursos de Azure de Hola que utiliza certificados almacenados en un almacén de claves cuando crea un clúster.

**Crear un grupo de recursos** Hola primer paso es toocreate un grupo de recursos específicamente para el almacén de claves. Se recomienda que coloque el almacén de claves de hello en su propio grupo de recursos. Esta acción le permite quitar Hola cálculo y almacenamiento de grupos de recursos, incluido el grupo de recursos de Hola que contiene el clúster de Service Fabric, sin perder sus claves y secretos. grupo de recursos de Hola que contiene el almacén de claves debe estar en hello misma región que el clúster de Hola que lo está usando.

**Crear un almacén de claves en el nuevo grupo de recursos de hello** almacén de claves de hello debe estar habilitado para la implementación tooallow Hola proceso recursos proveedor tooget certificados de él y lo instala en instancias de máquina virtual.
toolearn más tooset el almacén de claves de Azure vea, [empezar a trabajar con el almacén de claves de Azure](https://docs.microsoft.com/azure/key-vault/key-vault-get-started).

## <a name="assign-users-roles"></a>Asignación de roles a usuarios
Después de haber creado Hola aplicaciones toorepresent el clúster, asignar los usuarios roles toohello compatibles con Service Fabric: solo lectura y administrador. Puede asignar roles de hello mediante Hola portal de Azure clásico.

>[!Note]
> Para más información sobre los roles de Service Fabric, consulte [Control de acceso basado en roles para clientes de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

Azure Service Fabric admite dos tipos de control de acceso diferente para los clientes que están conectado tooa [clúster de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm): administrador y usuario. Control de acceso permite Hola clúster administrador toolimit acceso toocertain las operaciones del clúster para los diferentes grupos de usuarios, mejorar la seguridad de clúster de Hola.

## <a name="next-steps"></a>Pasos siguientes
- Configuración del [entorno de desarrollo](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started) de Service Fabric.
- Más información sobre las [opciones de soporte técnico de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-support).

