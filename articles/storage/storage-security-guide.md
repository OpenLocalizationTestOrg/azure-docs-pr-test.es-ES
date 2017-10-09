---
title: "Guía de seguridad de almacenamiento de aaaAzure | Documentos de Microsoft"
description: "Detalles de Hola muchos métodos de seguridad del almacenamiento de Azure, incluyendo pero sin limitarse tooRBAC, cifrado del servicio de almacenamiento, cifrado en el cliente, SMB 3.0 y cifrado del disco de Azure."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 6f931d94-ef5a-44c6-b1d9-8a3c9c327fb2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: d406ff0d6b45c6107d0276ad9e65c331078ce792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-guide"></a>Guía de seguridad de Azure Storage
## <a name="overview"></a>Información general
Almacenamiento de Azure proporciona un conjunto completo de capacidades de seguridad que juntos permiten a los desarrolladores de aplicaciones seguras toobuild. propia cuenta de almacenamiento Hola se puede proteger mediante el Control de acceso basado en roles y Azure Active Directory. Los datos se pueden proteger en tránsito entre una aplicación y Azure usando [cifrado de cliente](storage-client-side-encryption.md), HTTPS o SMB 3.0. Se pueden establecer toobe cifrada automáticamente cuando escribe datos tooAzure almacenamiento con [cifrado de servicio de almacenamiento (SSE)](storage-service-encryption.md). Discos de sistema operativo y los datos utilizados por máquinas virtuales se pueden establecer toobe cifrado con [cifrado del disco de Azure](../security/azure-security-disk-encryption.md). Se pueden conceder acceso delegado toohello objetos de datos en el almacenamiento de Azure mediante [firmas de acceso compartido](storage-dotnet-shared-access-signature-part-1.md).

Este artículo ofrece una visión general de cada una de estas características de seguridad que se pueden usar con Azure Storage. Se proporcionan vínculos tooarticles que proporcionan detalles de cada característica, por lo que puede hacer fácilmente una investigación más minuciosa en cada tema.

A continuación, incluimos hello toobe de temas tratado en este artículo:

* [Seguridad en el plano de la administración](#management-plane-security) : protección de la cuenta de almacenamiento

  plano de administración de Hello consta de hello toomanage de recursos que usa la cuenta de almacenamiento. En esta sección, hablaremos sobre el modelo de implementación de Azure Resource Manager hello y cómo toouse toocontrol de Control de acceso basado en roles (RBAC) tener acceso a las cuentas de almacenamiento de tooyour. También hablaremos acerca de cómo administrar las claves de cuenta de almacenamiento y cómo tooregenerate ellos.
* [Seguridad de datos plano](#data-plane-security) – tooYour de proteger el acceso a datos

  En esta sección, trataremos permitir acceso toohello objetos de datos reales en la cuenta de almacenamiento como blobs, archivos, las colas y tablas, con firmas de acceso compartido y almacena las directivas de acceso. Nos fijaremos en las Firmas de acceso compartido tanto a nivel de servicio como a nivel de cuenta. También veremos cómo toolimit tener acceso a dirección IP específica de tooa (o intervalo de direcciones IP), cómo usar el protocolo de Hola de toolimit tooHTTPS y cómo toorevoke una firma de acceso compartido sin esperar a tooexpire.
* [Cifrado en tránsito](#encryption-in-transit)

  Esta sección se describe cómo toosecure datos al transferirlos entre o salga de almacenamiento de Azure. Hablaremos acerca de hello recomendada el uso del cifrado de hello y HTTPS usado SMB 3.0 para recursos compartidos de archivos de Azure. También echaremos un vistazo a cifrado en el cliente, lo que permite tooencrypt Hola datos antes de transferirlos al almacenamiento en una aplicación cliente y toodecrypt Hola después de que se transfiere fuera de almacenamiento.
* [Cifrado en reposo](#encryption-at-rest)

  Hablaremos sobre el cifrado de servicio de almacenamiento (SSE) y cómo puede habilitar para una cuenta de almacenamiento, lo que los blobs en bloques, blobs de página y anexar blobs que se cifran automáticamente cuando escribe tooAzure almacenamiento. También veremos cómo puede usar el cifrado de disco de Azure y explorar diferencias básicas de Hola y casos de cifrado del disco frente a SSE frente a cifrado en el cliente. Asimismo, estudiaremos brevemente el cumplimiento de la norma FIPS para equipos del Gobierno de EE. UU.
* Usar [el análisis de almacenamiento](#storage-analytics) tooaudit acceso de almacenamiento de Azure

  En esta sección se describe cómo toofind información en análisis de almacenamiento de Hola se registra para una solicitud. Comenzaremos Eche un vistazo a análisis de almacenamiento real de los datos de registro y vea cómo toodiscern si se realiza una solicitud con Hola almacenamiento clave, con una firma de acceso compartido, la cuenta o de forma anónima y si se realizó correctamente o no se pudo.
* [Habilitación de clientes basados en explorador mediante el uso compartido de recursos entre orígenes](#Cross-Origin-Resource-Sharing-CORS)

  En esta sección habla de cómo tooallow de recursos entre orígenes (CORS) de uso compartido. Hablaremos sobre el acceso entre dominios, y cómo toohandle con capacidades de hello CORS integrada en el almacenamiento de Azure.

## <a name="management-plane-security"></a>Seguridad en el plano de la administración
plano de administración de Hello consta de las operaciones que afectan a la propia cuenta de almacenamiento Hola. Por ejemplo, puede crear o eliminar una cuenta de almacenamiento, obtener una lista de cuentas de almacenamiento en una suscripción, recuperar claves de cuenta de almacenamiento de Hola o volver a generar claves de cuenta de almacenamiento de Hola.

Cuando se crea una nueva cuenta de almacenamiento, se selecciona un modelo de implementación clásico o de Resource Manager. modelo clásico de Hola de creación de recursos en Azure solo permite suscripciones de toohello de acceso de todo o nada y Hola a su vez, la cuenta de almacenamiento.

Esta guía se centra en el modelo de administrador de recursos de Hola que es hello recomendada medios para crear cuentas de almacenamiento. Con las cuentas de almacenamiento del Administrador de recursos de hello, en lugar de la suscripción a toohello completa acceso determinado, puede controlar el acceso en un plano de administración de nivel toohello más finito con Control de acceso basado en roles (RBAC).

### <a name="how-toosecure-your-storage-account-with-role-based-access-control-rbac"></a>Cómo toosecure su cuenta de almacenamiento, con Control de acceso basado en roles (RBAC)
Vamos a ver qué es el control de acceso basado en roles y cómo se utiliza. Cada una de las suscripciones de Azure está asociada a una instancia de Azure Active Directory. Los usuarios, grupos y aplicaciones desde ese directorio pueden tener acceso a los recursos del toomanage Hola suscripción de Azure que usan el modelo de implementación del Administrador de recursos de Hola. Esto es lo que se conoce tooas Control de acceso basado en roles (RBAC). toomanage este acceso, puede usar hello [portal de Azure](https://portal.azure.com/), hello [herramientas de Azure CLI](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), o hello [API de REST de proveedor de recursos de almacenamiento de Azure ](https://msdn.microsoft.com/library/azure/mt163683.aspx).

Con el modelo del Administrador de recursos de hello, coloca cuenta de almacenamiento de hello en un recurso grupo y control de acceso toohello administración plano de esa cuenta de almacenamiento específico con Azure Active Directory. Por ejemplo, se pueden proporcionar a usuarios específicos Hola capacidad tooaccess Hola almacenamiento cuenta las claves, mientras que otros usuarios pueden ver información acerca de la cuenta de almacenamiento de hello, pero no pueden tener acceso a claves de cuenta de almacenamiento de Hola.

#### <a name="granting-access"></a>Concesión de acceso
Se concede acceso mediante la asignación de hello adecuado RBAC rol toousers, grupos y aplicaciones, en el ámbito adecuado de Hola. toogrant acceso toohello suscripción a completa, se asigna un rol en el nivel de suscripción de Hola. Puede conceder acceso tooall de recursos de hello en un grupo de recursos concediendo permisos toohello fam. propio. También puede asignar a roles específicos toospecific recursos, como cuentas de almacenamiento.

Estos son los puntos principales de Hola que necesita tooknow sobre el uso de operaciones de administración de RBAC tooaccess Hola de una cuenta de almacenamiento de Azure:

* Al asignar el acceso, básicamente asignar una cuenta de toohello de rol que desea que toohave acceso. Puede controlar el acceso toohello operaciones utilizadas toomanage esa cuenta de almacenamiento, pero no los datos de toohello objetos de cuenta de hello. Por ejemplo, puede conceder permiso tooretrieve propiedades de Hola de cuenta de almacenamiento de hello (por ejemplo, redundancia), pero no tooa contenedor o datos dentro de un contenedor dentro del almacenamiento de blobs.
* Para un usuario toohave permiso tooaccess Hola objetos de datos en la cuenta de almacenamiento de hello, puede proporcionar claves de cuenta de almacenamiento de permiso tooread hello y ese usuario, a continuación, puede usar esas claves tooaccess Hola blobs, colas, tablas y archivos.
* Cuenta de usuario específica de tooa, un grupo de usuarios o aplicaciones específicas de tooa se puedan asignar roles.
* Cada rol tiene una lista de acciones y no acciones. Por ejemplo, el rol de colaborador de la máquina Virtual de hello tiene una acción de "listKeys" que permite lee toobe de claves de cuenta de almacenamiento de Hola. Hola colaborador tiene "No acciones", como la actualización de acceso de Hola para los usuarios de Active Directory de Hola.
* Roles para el almacenamiento incluyen (pero no se limitan a) siguiente hello:

  * Propietario: puede administrar todo, incluido el acceso.
  * Colaborador: puede hacer cualquier cosa propietario Hola puede excepto asignar acceso. Un usuario con este rol puede ver y regenerar claves de cuenta de almacenamiento de Hola. Con claves de cuenta de almacenamiento de hello, pueden tener acceso a objetos de datos de Hola.
  * Lector: pueden ver información acerca de la cuenta de almacenamiento de hello, excepto los secretos. Por ejemplo, si asigna un rol con permisos de lectura en toosomeone de cuenta de almacenamiento de hello, pueden ver las propiedades de Hola de cuenta de almacenamiento de hello, pero no pueden realizar cambios de propiedades de toohello ni ver claves de cuenta de almacenamiento de Hola.
  * Colaborador de la cuenta de almacenamiento, puede administrar cuenta de almacenamiento de hello: pueden leer Hola grupos de recursos y los recursos, la suscripción y crear y administrar implementaciones de grupos de recursos de suscripción. También puede tener acceso a claves de cuenta de almacenamiento de hello, que a su vez significa que pueden tener acceso a plano de datos de Hola.
  * Administrador de acceso de usuario: puede administrar la cuenta de almacenamiento de toohello de acceso de usuario. Por ejemplo, puede conceder el usuario específico de tooa de acceso de lectura.
  * Colaborador de la máquina virtual: pueden administrar máquinas virtuales pero no Hola almacenamiento cuenta toowhich que están conectados. Esta función puede enumerar las claves de cuenta de almacenamiento hello, lo que significa que Hola toowhom usuario asignar este rol puede actualizar el plano de datos de Hola.

    En orden para un toocreate de usuario una máquina virtual, tienen toobe toocreate capaz de hello correspondiente archivo VHD en una cuenta de almacenamiento. toodo, que necesitan almacenamiento Hola de toobe tooretrieve capaz de clave de cuenta y pasarlo API toohello crear Hola máquina virtual. Por lo tanto, deben tener este permiso por lo que pueden enumerar claves de cuenta de almacenamiento de Hola.
* roles personalizados de Hello capacidad toodefine es una característica que le permite toocompose un conjunto de acciones de una lista de las acciones disponibles que se pueden realizar en recursos de Azure.
* usuario de Hello tiene toobe configurado en Azure Active Directory antes de asignar un rol toothem.
* Puede crear un informe de que conceder o revocar qué tipo de acceso a/desde los que y en qué ámbito usar PowerShell u Hola CLI de Azure.

#### <a name="resources"></a>Recursos
* [Control de acceso basado en roles de Azure Active Directory](../active-directory/role-based-access-control-configure.md)

  Este artículo explica Hola basada en roles de Azure Active Directory Access Control y cómo funciona.
* [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md)

  En este artículo se detalla todas Hola funciones integradas disponibles en RBAC.
* [Descripción de la implementación de Resource Manager y la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md)

  Este artículo explica la implementación del Administrador de recursos de Hola y modelos de implementación clásica y explica las ventajas de Hola de uso de grupos de administrador de recursos y recursos de Hola. Se explica cómo funcionan los proveedores de almacenamiento, red y Hola cálculo de Azure bajo el modelo del Administrador de recursos de Hola.
* [Administración del Control de acceso basado en roles con hello API de REST](../active-directory/role-based-access-control-manage-access-rest.md)

  Este artículo muestra cómo toouse Hola toomanage RBAC de API de REST.
* [Referencia de API de REST de proveedor de recursos de Azure Storage](https://msdn.microsoft.com/library/azure/mt163683.aspx)

  Se trata de referencia de Hola para hello las API que se puede utilizar toomanage la cuenta de almacenamiento mediante programación.
* [Tooauth de guía del desarrollador con la API del Administrador de recursos de Azure](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)

  Este artículo muestra cómo usar tooauthenticate Hola API del Administrador de recursos.
* [Role-Based Access Control for Microsoft Azure from Ignite (Control de acceso basado en rol para Microsoft Azure de Ignite)](https://channel9.msdn.com/events/Ignite/2015/BRK2707)

  Se trata de un vídeo de Channel 9 de la conferencia de Ignite de 2015 MS hello tooa de vínculo. En esta sesión, hablan sobre acceso a capacidades de administración y generación de informes en Azure y explorar las prácticas recomendadas en protección del acceso suscripciones tooAzure con Azure Active Directory.

### <a name="managing-your-storage-account-keys"></a>Administración de las claves de cuenta de almacenamiento
Cuenta de almacenamiento de las claves son cadenas de 512 bits creadas por Azure que, junto con el almacenamiento de hello, el nombre de cuenta pueden ser objetos de datos de hello tooaccess usado almacenados en la cuenta de almacenamiento de hello, p. ej., blobs, las entidades dentro de una tabla, cola de mensajes y archivos en un recurso compartido de archivos de Azure. Controla teclas de acceso toohello almacenamiento cuenta controles acceso toohello plano de datos para esa cuenta de almacenamiento.

Cada cuenta de almacenamiento tiene dos claves conoce tooas "Clave 1" y "Clave de 2" en hello [portal de Azure](http://portal.azure.com/) y Hola cmdlets de PowerShell. Se puede regenerar manualmente mediante uno de varios métodos, incluyendo, pero sin limitarse toousing Hola [portal de Azure](https://portal.azure.com/), PowerShell, Hola CLI de Azure o mediante programación con Hola biblioteca de cliente de almacenamiento o hello Azure API de REST de servicios de almacenamiento.

Hay cualquier serie de motivos tooregenerate las claves de cuenta de almacenamiento.

* Puede cambiarlas de nuevo de manera periódica por motivos de seguridad.
* Debería volver a generar las claves de cuenta de almacenamiento si alguien administra toohack en una aplicación y recuperar la clave de Hola que fue codificado o se guarda en un archivo de configuración, darles cuenta de almacenamiento de tooyour de acceso completo.
* Otro caso de regeneración de claves es si el equipo está usando una aplicación de explorador de almacenamiento que conserva la clave de cuenta de almacenamiento de Hola y uno de los miembros del equipo de hello deja. aplicación Hello continuaría toowork, concederles acceso tooyour almacenamiento cuenta después de que se vendan. Se trata realmente Hola motivo principal que crean firmas de acceso compartido de nivel de cuenta: puede usar un SAS de nivel de cuenta en lugar de almacenar las claves de acceso de hello en un archivo de configuración.

#### <a name="key-regeneration-plan"></a>Plan de regeneración de claves
No desea clave de hello regenerar toojust que se utiliza sin una planeación. Si lo hace, podría cortar todas las cuentas de almacenamiento toothat de acceso, que pueden provocar interrupciones importantes. Este es el motivo por el cual hay dos claves. Puede volver a generar una de ellas y luego la otra en vez de hacerlo de manera simultánea.

Antes de volver a generar las claves, asegúrese de que dispone de una lista de todas las aplicaciones que dependen de la cuenta de almacenamiento de hello, así como cualquier otro servicio que usa en Azure. Por ejemplo, si está utilizando servicios de multimedia de Azure que dependen de la cuenta de almacenamiento, deben volver a sincronizar las claves de acceso de hello con su servicio multimedia después de regenerar clave de Hola. Si usas todas las aplicaciones, como un explorador de almacenamiento, deberá tooprovide Hola nuevas claves toothose aplicaciones también. Tenga en cuenta que si tiene máquinas virtuales cuyos archivos de disco duro virtual se almacenan en la cuenta de almacenamiento de hello, no se verá afectado por la regeneración de claves de cuenta de almacenamiento de Hola.

Puede volver a generar las claves en hello portal de Azure. Una vez que se vuelven a generar las claves pueden ocupar too10 toobe minutos se sincroniza en los servicios de almacenamiento.

Cuando esté listo, aquí es donde se detalla cómo se debe cambiar la clave de proceso general de Hola. En este caso, suposición de hello es que actualmente está utilizando la clave 1 y va toochange todo toouse clave 2 en su lugar.

1. Volver a generar tooensure 2 de clave que es segura. Puede hacerlo en hello portal de Azure.
2. En todos las aplicaciones de Hola donde se almacena la clave de almacenamiento de hello, cambiar valor nuevo del 2 de clave de hello almacenamiento toouse clave. Probar y publicar la aplicación hello.
3. Después de que todos del programa Hola a aplicaciones y servicios están funcionando y ejecutarse correctamente, volver a generar clave 1. Esto garantiza que cualquier usuario toowhom no han proporcionado expresamente nueva clave de hello dejará de tener acceso a la cuenta de almacenamiento de toohello.

Si actualmente utilizas clave 2, puede usar Hola mismo proceso, pero los nombres de clave de hello inversa.

Puede migrar a través de un par de días, cambiar cada nueva clave de aplicación toouse hello y publicarlo. Una vez terminados todas ellas, a continuación, debe volver atrás y regenerar la clave antigua de Hola por lo que deja de funcionar.

Otra opción es la clave de cuenta de almacenamiento tooput hello en un [el almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/) como un secreto y tienen su clave de Hola de recuperación de las aplicaciones desde allí. A continuación, al regenerar la clave de Hola y actualizar Hola almacén de claves de Azure, las aplicaciones de hello no deberán toobe volver a implementar porque se recogen automáticamente la nueva clave de Hola de hello almacén de claves de Azure. Tenga en cuenta que puede hacer que la aplicación hello leer la clave de hello cada vez que lo necesite, o puede almacenarla en la caché en memoria y si se produce un error cuando se usa, recuperar clave Hola nuevo de hello almacén de claves de Azure.

El uso de Azure Key Vault también agrega otro nivel de seguridad a las claves de almacenamiento. Si utiliza este método, nunca tendrá Hola almacenamiento clave codificados en un archivo de configuración, lo que elimina ese caminos de alguien obtener acceso a las claves de toohello sin permiso específico.

Otra ventaja de utilizar el almacén de claves de Azure es que también puede controlar el acceso a las claves de tooyour con Azure Active Directory. Esto significa que puede conceder puñado de toohello de acceso de las aplicaciones que necesitan las claves de hello tooretrieve desde el almacén de claves de Azure y sabe que otras aplicaciones no será capaz de tooaccess claves de hello sin concederles permisos específicamente.

Nota: se recomienda toouse solo uno de hello las claves de todas las aplicaciones en hello mismo tiempo. Si usas en algunos lugares de claves 1 y 2 de la clave en otras, no podrá ser capaz de toorotate las claves sin alguna aplicación perder el acceso.

#### <a name="resources"></a>Recursos
* [Acerca de las cuentas de Azure Storage](storage-create-storage-account.md#regenerate-storage-access-keys)

  En este artículo se ofrece una visión general de las cuentas de almacenamiento y se trata la visualización, la copia y la regeneración de las claves de acceso de almacenamiento.
* [Referencia de API de REST de proveedor de recursos de Azure Storage](https://msdn.microsoft.com/library/mt163683.aspx)

  Este artículo contiene artículos de toospecific vínculos acerca de cómo recuperar claves de cuenta de almacenamiento de Hola y claves de la cuenta de almacenamiento de hello regenerando para una cuenta de Azure utilizando Hola API de REST. Nota: Se trata de cuentas de almacenamiento de Resource Manager.
* [Operaciones en cuentas de almacenamiento](https://msdn.microsoft.com/library/ee460790.aspx)

  En este artículo en hello almacenamiento Service Manager REST API Reference contiene artículos de toospecific de vínculos en la recuperación y regeneración de claves de la cuenta de almacenamiento hello mediante Hola API de REST. Nota: Esto es Hola clásico las cuentas de almacenamiento.
* [Diga administración de tookey goodbye: administrar los datos de almacenamiento de tooAzure de acceso mediante Azure AD](http://www.dushyantgill.com/blog/2015/04/26/say-goodbye-to-key-management-manage-access-to-azure-storage-data-using-azure-ad/)

  Este artículo muestra cómo toouse Active Directory toocontrol tener acceso a las claves de almacenamiento de Azure tooyour en el almacén de claves de Azure. También muestra cómo toouse una automatización de Azure trabajo claves de hello tooregenerate cada hora.

## <a name="data-plane-security"></a>Seguridad en el plano de los datos
Seguridad de plano de los datos hace referencia a los métodos toohello almacenan los objetos de datos de uso toosecure hello en almacenamiento de Azure: archivos, colas, tablas y blobs de Hola. Hemos visto métodos tooencrypt Hola datos y la seguridad durante el tránsito de datos de hello, pero cómo va acerca de cómo permitir el acceso a objetos de toohello?

Básicamente, hay dos métodos para controlar acceso toohello datos propios objetos. Hola primero es controlar claves de cuenta de almacenamiento de toohello de acceso, y hello en segundo lugar utiliza objetos de datos de firmas de acceso compartido toogrant acceso toospecific durante un período de tiempo específico.

Toonote de una excepción es que puede permitir el acceso público tooyour blobs estableciendo el nivel de acceso de Hola para hello contenedor de blobs de hello en consecuencia. Si configura el acceso para un contenedor tooBlob o contenedor, permitirá el acceso de lectura público para los blobs de hello en ese contenedor. Esto significa que cualquier persona con una dirección URL que apunte tooa blob del contenedor puede abrir en un explorador sin usar una firma de acceso compartido ni tener claves de cuenta de almacenamiento de Hola.

### <a name="storage-account-keys"></a>Claves de cuenta de almacenamiento
Claves de la cuenta de almacenamiento son cadenas de 512 bits creadas por Azure que, junto con el nombre de la cuenta de almacenamiento hello, puede ser objetos de datos de Hola de tooaccess usado almacenados en la cuenta de almacenamiento de Hola.

Por ejemplo, puede leer los blobs, escribir tooqueues, crear tablas y modificar los archivos. Muchas de estas acciones se pueden realizar mediante hello Azure portal, o mediante una de las muchas aplicaciones de explorador de almacenamiento. También puede escribir Hola de toouse código API de REST o uno de hello bibliotecas de cliente de almacenamiento tooperform estas operaciones.

Como se describe en la sección de hello en hello [administración plano seguridad](#management-plane-security), tener acceso a las claves de almacenamiento de toohello puede tener una cuenta de almacenamiento clásico proporcionando acceso completo toohello suscripción de Azure. Claves de almacenamiento de toohello de acceso de una cuenta de almacenamiento mediante el modelo de hello Azure Resource Manager se pueden controlar a través del Control de acceso basado en roles (RBAC).

### <a name="how-toodelegate-access-tooobjects-in-your-account-using-shared-access-signatures-and-stored-access-policies"></a>Cómo toodelegate tener acceso a tooobjects en su cuenta a través de firmas de acceso compartido y almacena las directivas de acceso
Una firma de acceso compartido es una cadena que contiene un token de seguridad que puede ser adjunta tooa URI que le permite obtener acceso a toostorage objetos de toodelegate y especificar restricciones como permisos de Hola y el intervalo de fecha y hora de Hola de acceso.

Puede conceder acceso tooblobs, contenedores, cola de mensajes, archivos y tablas. Con las tablas, puede realmente conceder permiso tooaccess un rango de entidades de tabla de Hola especificando Hola partición y fila intervalos de claves toowhich desea Hola usuario toohave acceso. Por ejemplo, si tiene datos almacenados con una clave de partición de estado geográfica, se pudieron proporcionar a alguien acceso toojust Hola datos de California.

En otro ejemplo, podría proporcionar un token SAS que le permite tooa cola de toowrite entradas a una aplicación web y proporcionar a un trabajador aplicación de rol un mensajes de tooget token de SAS de Hola de cola y procesan. O bien, se podría proporcionar a un cliente un token SAS puede usar contenedor tooa de tooupload imágenes en almacenamiento de blobs y proporcionan un tooread de permiso de aplicación web esas imágenes. En ambos casos, hay una separación de intereses: cada aplicación se les puede dar acceso de solo Hola que necesiten en orden tooperform su tarea. Esto es posible mediante el uso de Hola de firmas de acceso compartido.

#### <a name="why-you-want-toouse-shared-access-signatures"></a>¿Por qué desea toouse firmas de acceso compartido
¿Por qué desearía toouse una SAS en lugar de simplemente dar su clave de cuenta de almacenamiento, que es mucho más fácil? Dar su clave de cuenta de almacenamiento es como el uso compartido de las claves de Hola del Reino de almacenamiento. Con ella, es posible acceder a todo el contenido. Alguien podría usar las claves y cargar su cuenta de almacenamiento de tooyour de biblioteca de música todo. También podría reemplazar sus archivos por versiones infectadas o robar sus datos. Dar cuenta de almacenamiento de acceso ilimitado tooyour es algo que no debe tomarse ligeramente.

Con firmas de acceso compartido, puede permitir a un cliente solo los permisos de hello necesarios durante un período limitado de tiempo. Por ejemplo, si alguien está cargando una cuenta de tooyour de blob, puede concederles acceso de escritura para suficiente blob de hello tooupload de tiempo (según tamaño Hola de blob de hello, por supuesto). Y si cambia de opinión, puede revocar el acceso.

Además, puede especificar que las solicitudes realizadas mediante una SAS están restringido tooa ciertos tooAzure externo de intervalo de direcciones de dirección IP o una dirección IP. También puede requerir que las solicitudes se realicen mediante un protocolo específico (HTTPS o HTTP/HTTPS). Esto significa que si sólo desea tooallow tráfico HTTPS, puede establecer Hola requerido protocolo solo tooHTTPS y se bloqueará el tráfico HTTP.

#### <a name="definition-of-a-shared-access-signature"></a>Definición de una Firma de acceso compartido
Una firma de acceso compartido es que un conjunto de parámetros de consulta anexa la dirección URL de toohello que apunte al recurso de Hola

que proporciona información acerca del acceso de hello permitido y Hola período de tiempo para qué Hola se permite el acceso. Este es un ejemplo; Este URI proporciona acceso de lectura tooa blob durante cinco minutos. Tenga en cuenta que los parámetros de consulta de la Firma de acceso compartido deben presentar codificación URL; por ejemplo %3A para los dos puntos (:) o %20 para un espacio.

```
http://mystorage.blob.core.windows.net/mycontainer/myblob.txt (URL toohello blob)
?sv=2015-04-05 (storage service version)
&st=2015-12-10T22%3A18%3A26Z (start time, in UTC time and URL encoded)
&se=2015-12-10T22%3A23%3A26Z (end time, in UTC time and URL encoded)
&sr=b (resource is a blob)
&sp=r (read access)
&sip=168.1.5.60-168.1.5.70 (requests can only come from this range of IP addresses)
&spr=https (only allow HTTPS requests)
&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D (signature used for hello authentication of hello SAS)
```

#### <a name="how-hello-shared-access-signature-is-authenticated-by-hello-azure-storage-service"></a>Cómo Hola firma de acceso compartido se autentica mediante Hola servicio de almacenamiento de Azure
Al servicio de almacenamiento de hello recibe la solicitud de hello, que toma parámetros de consulta de entrada de Hola y crea una firma utilizando Hola mismo método como Hola programa que realiza la llamada. A continuación, compara dos firmas de Hola. Si se acepta y Hola servicio de almacenamiento puede comprobar toomake de versión de servicio de almacenamiento de hello seguro es válido, compruebe que hello fecha y hora actual están dentro de la ventana especificada de hello, asegúrese de que access Hola solicitado corresponde solicitud toohello realizada, etcetera.

Por ejemplo, con la dirección URL anterior, si Hola URL señalaba tooa archivo en lugar de un blob, esta solicitud produciría un error porque especifica ese Hola que firma de acceso compartido es para un blob. Si Hola comando REST que se llama es tooupdate un blob, produciría un error porque hello firma de acceso compartido especifica que se permita el acceso de solo lectura.

#### <a name="types-of-shared-access-signatures"></a>Tipos de Firmas de acceso compartido
* Una SAS de nivel de servicio pueden ser recursos específicos de tooaccess usado en una cuenta de almacenamiento. Algunos ejemplos de este se recuperar una lista de blobs en un contenedor, descarga un blob, actualizar una entidad en una tabla, agregar la cola de mensajes tooa o cargar un recurso compartido de archivo tooa.
* Una SAS de nivel de cuenta puede ser usado tooaccess todo lo que una SAS de nivel de servicio puede utilizarse para. Además, puede dar a tooresources de opciones que no se permiten con una SAS de nivel de servicio, como contenedores de toocreate de capacidad de hello, tablas, colas y recursos compartidos de archivos. También puede especificar los servicios de toomultiple de acceso a la vez. Por ejemplo, puede dar a alguien acceso tooboth blobs y los archivos en su cuenta de almacenamiento.

#### <a name="creating-an-sas-uri"></a>Creación de un URI de Firma de acceso compartido
1. Puede crear un URI ad hoc a petición, todos los parámetros de consulta de Hola de definir cada vez.

   Esta opción es realmente flexible, pero si tiene un conjunto lógico de parámetros que se parecen cada vez, es mejor utilizar una Directiva de acceso almacenada.
2. Puede crear una Directiva de acceso almacenada para todo un contenedor, el recurso compartido de archivos, la tabla o la cola. A continuación, puede usar esto como base de Hola para hello URI de SAS se crea. Los permisos basados en Directivas de acceso almacenadas se pueden revocar fácilmente. Puede hacer una copia de seguridad directivas too5 definidas en cada contenedor, cola, tabla o recurso compartido de archivos.

   Por ejemplo, si se va toohave muchas personas leen los blobs de hello en un contenedor específico, podría crear una directiva de acceso almacenada que dice "conceder acceso de lectura" y cualquier otro valor que será Hola mismo cada vez. A continuación, puede crear un URI de SAS con valores de hello de hello almacenado la directiva de acceso y especificar la fecha y hora de expiración de Hola. Hello ventaja de esto es que no tiene toospecify todos Hola parámetros de consulta cada vez.

#### <a name="revocation"></a>Revocación
Supongamos que se ha puesto en peligro su SAS, o quiere toochange, debido a la seguridad de la empresa o requisitos de cumplimiento de normas. ¿Cómo revocar el acceso a recursos de tooa con ese SAS? Depende de cómo haya creado Hola URI de SAS.

Si utiliza URI ad hoc, tiene tres opciones. Puede emitir tokens SAS con directivas de expiración corto y simplemente espere Hola SAS tooexpire. Puede cambiar el nombre o eliminar el recurso de hello (suponiendo que el token de Hola de tooa ámbito único objeto). Puede cambiar las claves de cuenta de almacenamiento de Hola. Esta última opción puede tener un gran impacto, dependiendo de cuántos services usa esa cuenta de almacenamiento y probablemente no es algo que desea toodo sin una planeación.

Si utilizas una SAS que se deriva de una directiva de acceso almacenada, puede quitar el acceso Revocando Hola almacenado la directiva de acceso: solo puede cambiar por lo que ya ha expirado o se puede quitar por completo. Esto surte efecto inmediatamente e invalida todas las Firmas de acceso compartido creadas utilizando esa Directiva de acceso almacenada. Actualizar o eliminar Hola directiva de acceso almacenada puede afectar a los usuarios obtener acceso a ese contenedor específico, el recurso compartido de archivos, la tabla o la cola a través de SAS, pero si hello se escriben los clientes para que solicitan una nueva SAS cuando Hola antigua deja de ser válido, esto funcionará sin problemas.

Ya mediante una SAS que se deriva de una directiva de acceso almacenada ofrece toorevoke de capacidad de Hola que SAS inmediatamente, resulta Hola recomienda tooalways de práctica recomendada usar almacena las directivas de acceso siempre que sea posible.

#### <a name="resources"></a>Recursos
Para obtener más información sobre el uso de firmas de acceso compartido y almacena las directivas de acceso, junto con ejemplos, consulte toohello siguientes artículos:

* Se trata de artículos de referencia de Hola.

  * [Ejemplos SAS del servicio.](https://msdn.microsoft.com/library/dn140256.aspx)

    Este artículo proporciona ejemplos de cómo utilizar una SAS de nivel de servicio con blobs, mensajes de cola, intervalos de tabla y archivos.
  * [Creación de una SAS de servicio](https://msdn.microsoft.com/library/dn140255.aspx)
  * [Creación de una SAS de cuenta](https://msdn.microsoft.com/library/mt584140.aspx)
* Se trata de tutoriales para usar toocreate de biblioteca de cliente de .NET de hello las firmas de acceso compartido y almacena las directivas de acceso.

  * [Uso de Firmas de acceso compartido (SAS)](storage-dotnet-shared-access-signature-part-1.md)
  * [Comparten las firmas de acceso, parte 2: Crear y utilizar una SAS con hello servicio Blob](storage-dotnet-shared-access-signature-part-2.md)

    Este artículo incluye una explicación del modelo SAS de hello, ejemplos de firmas de acceso compartido, y recomendaciones para la práctica recomendada de hello el uso de SAS. También trata de revocación de Hola de permiso de Hola.
* Limitación del acceso por dirección IP (ACL de IP)

  * [¿Qué es una lista de control de acceso (ACL) de extremo?](../virtual-network/virtual-networks-acl.md)
  * [Creación de una SAS de servicio](https://msdn.microsoft.com/library/azure/dn140255.aspx)

    Se trata de artículo de referencia de Hola para asociaciones de seguridad de nivel de servicio; incluye un ejemplo de ACLing de IP.
  * [Creación de una SAS de cuenta](https://msdn.microsoft.com/library/azure/mt584140.aspx)

    Se trata de artículo de referencia de Hola para asociaciones de seguridad de nivel de cuenta; incluye un ejemplo de ACLing de IP.
* Autenticación

  * [Autenticación de hello servicios de almacenamiento de Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* Tutorial de introducción a las Firmas de acceso compartido

  * [Getting Started with Shared Access Signatures (SAS) (Introducción a las Firmas de acceso compartido)](https://github.com/Azure-Samples/storage-dotnet-sas-getting-started)

## <a name="encryption-in-transit"></a>Cifrado en tránsito
### <a name="transport-level-encryption--using-https"></a>Cifrado de nivel de transporte – Uso de HTTPS
Otro paso que debe seguir la seguridad de hello tooensure de los datos de almacenamiento de Azure es datos de hello tooencrypt entre el cliente de Hola y el almacenamiento de Azure. primera recomendación de Hello es tooalways usar hello [HTTPS](https://en.wikipedia.org/wiki/HTTPS) Hola de protocolo, que garantiza una comunicación segura a través de Internet pública.

toohave un canal de comunicación segura, se debe utilizar siempre HTTPS al llamar a las API de REST de Hola o tiene acceso a objetos en el almacenamiento. Además, **firmas de acceso compartido**, que puede ser usado toodelegate tener acceso a objetos de almacenamiento de tooAzure, incluya una opción toospecify ese Hola solo puede usar el protocolo HTTPS al utilizar firmas de acceso compartido, lo que asegura que todo el personal Enviar vínculos con tokens SAS usará el protocolo adecuado de Hola.

Puede exigir el uso Hola de HTTPS al llamar a objetos de tooaccess de las API de REST de hello en cuentas de almacenamiento habilitando [proteger la transferencia se necesitan](storage-require-secure-transfer.md) Hola cuenta de almacenamiento. Una vez que esta opción esté habilitada, se rechazarán las conexiones que usan HTTP.

### <a name="using-encryption-during-transit-with-azure-file-shares"></a>Uso del cifrado durante el tránsito con recursos compartidos de archivos de Azure
Almacenamiento de archivos de Azure admite HTTPS cuando se utiliza la API de REST de hello, pero es más comúnmente usado como un recurso compartido de archivos SMB adjunta tooa máquina virtual. SMB 2.1 no admite el cifrado, por lo que las conexiones se permiten únicamente en hello mismo región de Azure. Sin embargo, SMB 3.0 admite el cifrado y está disponible en Windows Server 2012 R2, Windows 8, Windows 8.1 y Windows 10, lo que permite entre regiones accedan e incluso acceso en el escritorio de Hola.

Tenga en cuenta que aunque recursos compartidos de archivos de Azure se pueden utilizar con Unix, Hola cliente Linux SMB aún no admite el cifrado, por lo que solo se permite el acceso dentro de una región de Azure. Compatibilidad con el cifrado para Linux está en la guía básica de Hola de desarrolladores de Linux responsables de la funcionalidad SMB. Cuando agrega el cifrado, tendrá Hola misma capacidad para tener acceso a un recurso compartido de archivos de Azure en Linux tal como hace para Windows.

Se puede exigir el uso de Hola del cifrado con el servicio de archivos de Azure hello habilitando [proteger la transferencia se necesitan](storage-require-secure-transfer.md) Hola cuenta de almacenamiento. Si utiliza hello las API de REST, se necesita HTTPs. Para SMB, solo las conexiones SMB que admiten cifrado se conectarán correctamente.

#### <a name="resources"></a>Recursos
* [¿Cómo toouse almacenamiento de archivos de Azure con Linux](storage-how-to-use-files-linux.md)

  Este artículo muestra cómo compartir toomount un archivo de Azure en un sistema y cargar/descargar archivos de Linux.
* [Introducción a Almacenamiento de archivos de Azure en Windows](storage-dotnet-how-to-use-files.md)

  Este artículo proporciona información general sobre recursos compartidos de archivos de Azure y cómo toomount y usarlos con PowerShell y. NET.
* [En el interior de Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)

  Este artículo anuncia la disponibilidad general de Hola de almacenamiento de archivos de Azure y proporciona detalles técnicos acerca del cifrado de hello SMB 3.0.

### <a name="using-client-side-encryption-toosecure-data-that-you-send-toostorage"></a>Utilizando los datos de toosecure de cifrado de cliente que envíe toostorage
Otra opción que le ayuda a garantizar que sus datos están protegidos mientras se transfieren entre una aplicación cliente y el servicio Almacenamiento es el Cifrado de cliente. Hola datos se cifran antes de que se transfieren al almacenamiento de Azure. Cuando se recuperan datos de Hola desde el almacenamiento de Azure, se descifran los datos de hello tras su recepción en el lado del cliente de Hola. Aunque cifrar los datos de hello va a través de conexión de hello, se recomienda usar HTTPS, porque tiene comprobaciones de integridad de datos integradas que ayudan a mitigar los errores de red están afectando Hola la integridad de datos de Hola.

Cifrado en el cliente también es un método para cifrar los datos en reposo, como datos de Hola se almacenan en su forma cifrada. Hablaremos sobre esto con más detalle en la sección de hello en [cifrado en reposo](#encryption-at-rest).

## <a name="encryption-at-rest"></a>Cifrado en reposo
Hay tres características de Azure que proporcionan cifrado en reposo. Cifrado de disco de Azure es tooencrypt usado hello OS y discos de datos en máquinas virtuales de IaaS. Hola otros dos: cifrado en el cliente y SSE – son ambos datos tooencrypt usado en el almacenamiento de Azure. Vamos a analizarlos por separado y luego los vamos a comparar para determinar cuándo se puede utilizar cada uno de ellos.

Aunque pueden usar datos de cifrado en el cliente tooencrypt hello en tránsito (que también se almacena en su formato cifrado en el almacenamiento), puede preferir toosimply use HTTPS durante la transferencia de Hola y tener alguna manera de hello datos toobe cifra automáticamente cuando sea almacena. Hay dos toodo formas esto: cifrado del disco de Azure y SSE. Se utiliza una toodirectly cifrar los datos de hello en discos de sistema operativo y los datos usados por las máquinas virtuales y Hola otro datos utilizados tooencrypt escritos tooAzure almacenamiento de blobs.

### <a name="storage-service-encryption-sse"></a>cifrado del servicio de almacenamiento (SSE)
SSE permite toorequest que el servicio de almacenamiento de hello cifrar automáticamente los datos de hello al escribir tooAzure almacenamiento. Cuando se leen datos saludo del almacenamiento de Azure, se descifrará por servicio de almacenamiento de hello antes de devolverse. Esto le permite toosecure los datos sin necesidad de toomodify de código o agreguen código tooany aplicaciones.

Se trata de una configuración que se aplica la cuenta de almacenamiento completo toohello. Puede habilitar y deshabilitar esta característica cambiando el valor de Hola de saludo. toodo esto, puede usar Hola Hola de portal de Azure, PowerShell, CLI de Azure, Hola API de REST de proveedor de recursos de almacenamiento u Hola biblioteca de cliente de almacenamiento. De forma predeterminada, SSE está desactivado.

En este momento, Microsoft administra las claves de hello usadas para el cifrado de Hola. Se generan claves de Hola originalmente y administra un almacenamiento seguro de claves de hello, así como la rotación normal de Hola Hola tal como se define por la directiva interno de Microsoft. Hola futuras, se obtendrá Hola capacidad toomanage sus propias claves de cifrado y proporcionar una ruta de acceso de migración de claves administrada por Microsoft claves administradas toocustomer.

Esta característica está disponible para las cuentas de Standard y Premium almacenamiento creadas mediante el modelo de implementación del Administrador de recursos de Hola. SSE se aplica solo tooblock blobs, blobs de página y blobs en anexos. Hello otros tipos de datos, incluidas las tablas, colas y archivos, no se cifrarán.

Sólo se cifran los datos cuando se habilita SSE y se escriben los datos de hello tooBlob almacenamiento. El hecho de habilitar o deshabilitar el SSE no afecta a los datos existentes. En otras palabras, cuando se habilita el cifrado, le no volver atrás y cifrar los datos que ya existe; ni descifrará los datos de Hola que ya existen cuando se deshabilita SSE.

Si desea toouse esta característica con una cuenta de almacenamiento estándar, puede crear una nueva cuenta de almacenamiento de administrador de recursos y use AzCopy toocopy Hola datos toohello nueva cuenta.

### <a name="client-side-encryption"></a>cifrado de cliente
Hemos mencionado cifrado en el cliente al hablar de cifrado de Hola de datos de hello en tránsito. Esta característica permite tooprogrammatically cifrar los datos en una aplicación de cliente antes de enviarlo a través de hello conexión toobe escrito tooAzure almacenamiento y tooprogrammatically descifrar los datos después de recuperarlos desde el almacenamiento de Azure.

Esto proporciona cifrado en tránsito, pero también proporciona características de Hola de cifrado en reposo. Tenga en cuenta que aunque se cifran datos hello en tránsito, todavía sigue siendo recomendable usar HTTPS tootake aprovechar las comprobaciones de integridad de datos integrados de Hola que ayudan a mitigar los errores de red están afectando Hola la integridad de datos de Hola.

Un ejemplo de dónde se debería usar esta opción es si tiene una aplicación web que almacena los blobs y recupera los blobs y desea aplicación hello y toobe de datos lo más seguras posible. En ese caso, utilizaría el cifrado de cliente. Hola el tráfico entre el cliente de Hola y Hola servicio Blob de Azure contiene recursos cifrado de Hola y nadie puede interpretar los datos de hello en tránsito y reconstituir en los blobs privados.

Cifrado en el cliente está organizado en Java de Hola y Hola .NET almacenamiento bibliotecas de cliente, que a su vez utilizan las API de almacén de clave de Azure, lo bastante fácil para tooimplement Hola. proceso de Hola de cifrar y descifrar datos Hola utiliza la técnica de sobres de Hola y almacena los metadatos usados por el cifrado de hello en cada objeto de almacenamiento. Por ejemplo, para los blobs, lo almacena en los metadatos de blob de hello, mientras que para las colas, agrega tooeach la cola de mensajes.

Para el cifrado de hello propio, puede generar y administrar sus propias claves de cifrado. También puede usar las claves generadas por la biblioteca de cliente de almacenamiento de Azure hello, o puede tener hello Azure Key Vault generar claves de Hola. Puede almacenar las claves de cifrado en el almacenamiento de claves local o en Azure Key Vault. Almacén de claves de Azure permite secretos de toohello de toogrant acceso de usuarios de toospecific de almacén de claves de Azure con Azure Active Directory. Esto significa que no solo cualquiera puede leer Hola almacén de claves de Azure y recuperar claves hello que usa para el cifrado de cliente.

#### <a name="resources"></a>Recursos
* [Cifrado y descifrado de blobs en Almacenamiento de Microsoft Azure con Almacén de claves de Azure](storage-encrypt-decrypt-blobs-key-vault.md)

  Este artículo se muestra cómo toouse el cifrado de cliente con el almacén de claves de Azure, incluido cómo toocreate Hola KEK y almacenarlo en el almacén de hello mediante PowerShell.
* [Cifrado del lado de cliente y Almacén de claves de Azure para el Almacenamiento de Microsoft Azure](storage-client-side-encryption.md)

  Este artículo ofrece una explicación del cifrado en el cliente y proporciona ejemplos de uso de hello almacenamiento cliente tooencrypt y descifrar recursos de biblioteca de servicios de almacenamiento de cuatro Hola. También trata Azure Key Vault.

### <a name="using-azure-disk-encryption-tooencrypt-disks-used-by-your-virtual-machines"></a>Mediante el cifrado de disco de Azure usan discos tooencrypt las máquinas virtuales
Azure Disk Encryption es una característica nueva. Esta característica permite tooencrypt discos de sistemas operativos de Hola y discos de datos usados por una máquina Virtual de IaaS. Para Windows, las unidades de Hola se cifran mediante tecnología de cifrado de BitLocker de estándar del sector. Para Linux, discos de Hola se cifran mediante la tecnología de hello DM Crypt. Esto está integrado con el almacén de claves de Azure tooallow se toocontrol y administrar claves de cifrado de disco de Hola.

solución de Hello admite Hola los escenarios siguientes para las máquinas virtuales IaaS cuando están habilitadas en Microsoft Azure:

* Integración con el Almacén de claves de Azure
* Máquinas virtuales de nivel estándar: [máquinas virtuales IaaS de las series A, D, DS, G, GS, etc.](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Habilitación del cifrado en máquinas virtuales IaaS Linux y Windows
* Deshabilitación del cifrado en las unidades de datos y del sistema operativo en máquinas virtuales IaaS Windows
* Deshabilitación del cifrado en unidades de datos en máquinas virtuales IaaS Linux
* Habilitación del cifrado en máquinas virtuales IaaS que ejecutan el sistema operativo cliente de Windows
* Habilitación del cifrado en volúmenes con rutas de montaje
* Habilitación del cifrado en máquinas virtuales Linux configuradas con seccionamiento de disco (RAID) mediante mdadm
* Habilitación del cifrado en máquinas virtuales con Linux mediante LVM para discos de datos
* Habilitación del cifrado en máquinas virtuales con Windows configuradas mediante Espacios de almacenamiento
* Se admiten todas las regiones públicas de Azure.

solución de Hello no admite Hola siguientes escenarios, características y tecnologías de la versión de Hola:

* Máquinas virtuales IaaS de nivel básico
* Deshabilitación del cifrado en una unidad del sistema operativo para máquinas virtuales IaaS Linux
* Máquinas virtuales de IaaS que se crean mediante el método de creación de VM clásica de Hola
* Integración con el Servicio de administración de claves local
* Azure File Storage (sistema de archivos compartido), Network File System (NFS), volúmenes dinámicos y máquinas virtuales con Windows configuradas con sistemas RAID basados en software


> [!NOTE]
> Cifrado del disco de sistema operativo Linux es actualmente compatible en hello siguiendo las distribuciones de Linux: RHEL 7.2, CentOS 7.2n y 16.04 Ubuntu.
>
>

Esta característica garantiza que todos los datos de los discos de máquinas virtuales se cifran en reposo en Azure Storage.

#### <a name="resources"></a>Recursos
* [Azure Disk Encryption para máquinas virtuales IaaS Linux y Windows](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="comparison-of-azure-disk-encryption-sse-and-client-side-encryption"></a>Comparación entre Azure Disk Encryption, SSE y cifrado del lado cliente
#### <a name="iaas-vms-and-their-vhd-files"></a>Máquinas virtuales de IaaS y sus archivos VHD
Para los discos usados por las máquinas virtuales de IaaS, se recomienda utilizar Azure Disk Encryption. Puede activar SSE tooencrypt Hola archivos VHD utilizado tooback esos discos en el almacenamiento de Azure, pero solo cifra los datos recién escritos. Esto significa que si crear una máquina virtual y, a continuación, habilitar SSE Hola cuenta de almacenamiento que contiene el archivo de disco duro virtual de hello, se cifrarán sólo los cambios de hello, no Hola archivo de disco duro virtual original.

Si crea una máquina virtual mediante una imagen de hello Azure Marketplace, Azure realiza un [shallow copia](https://en.wikipedia.org/wiki/Object_copying) de hello imagen tooyour cuenta de almacenamiento en el almacenamiento de Azure y no se cifra incluso si tiene SSE habilitado. Después de crea Hola VM y comienza a actualizar la imagen de hello, SSE empezará a cifrar los datos de Hola. Por esta razón, es mejor toouse que cifrado del disco de Azure en máquinas virtuales creado a partir de imágenes en hello Azure Marketplace si quiere que estén totalmente cifrada.

Si se coloca una máquina virtual cifrada previamente en Azure desde el entorno local, ser capaz de tooupload Hola cifrado claves tooAzure el almacén de claves y seguir usando cifrado Hola para esa máquina virtual que se estaba utilizando en local. Cifrado de disco de Azure es toohandle habilitado en este escenario.

Si dispone de VHD no cifrados desde el entorno local, puede cargarlo en la Galería de hello como una imagen personalizada y aprovisionar una máquina virtual del mismo. Si lo hace mediante plantillas de administrador de recursos de hello, puede pedir lo tooturn en cifrado del disco de Azure cuando se arranca Hola máquina virtual.

Al agregar un disco de datos y montar en hello VM, puede activar el cifrado de disco de Azure en ese disco de datos. Cifrará primero ese disco de datos localmente, y, a continuación, capa de administración de servicio de hello va a hacer frente al almacenamiento de una operación de escritura diferida por lo que se cifra el contenido del almacenamiento de Hola.

#### <a name="client-side-encryption"></a>cifrado de cliente
Cifrado en el cliente es método más seguro de Hola de cifrar los datos, porque se cifra antes de tránsito y cifra los datos de hello en reposo. Sin embargo, requieren que agregue mediante almacenamiento, que puede que no desee las aplicaciones de código tooyour toodo. En esos casos, puede usar HTTPs para los datos en tránsito y datos de SSE tooencrypt hello en reposo.

Con el cifrado de cliente, puede cifrar las entidades de tabla, los mensajes de colas y los blobs. Con SSE, solo se pueden cifrar los blobs. Si necesita toobe de datos de tabla y cola cifrada, debe utilizar el cifrado de cliente.

Cifrado en el cliente se administra completamente con la aplicación hello. Esto es un enfoque más seguro hello, pero requieren la aplicación de tooyour de toomake cambios mediante programación y reúne los procesos de administración de claves en lugar. Utilice esto cuando desee Hola seguridad adicional durante el tránsito y desea que su toobe de los datos almacenados cifrado.

Cifrado en el cliente es más carga en el cliente de Hola y tiene tooaccount para esto en los planes de escalabilidad, especialmente si va a cifrar y transferir una gran cantidad de datos.

#### <a name="storage-service-encryption-sse"></a>cifrado del servicio de almacenamiento (SSE)
SSE se administra mediante Azure Storage. Uso de SSE no proporcione para la seguridad de Hola de datos de hello en tránsito, pero cifra datos Hola tal y como se escribe tooAzure almacenamiento. No hay ningún impacto en el rendimiento de hello cuando utilice esta característica.

Solo puede cifrar blobs en bloques, blobs en anexos y blobs en páginas mediante SSE. Si necesita datos de la tabla de tooencrypt o datos de la cola, considere la posibilidad de usar el cifrado de cliente.

Si tiene un archivo o una biblioteca de archivos de disco duro virtual que usar como punto de partida para crear nuevas máquinas virtuales, puede crear una nueva cuenta de almacenamiento, habilitar SSE y, a continuación, cargar la cuenta de toothat de archivos de disco duro virtual de Hola. Esos archivos VHD se cifrarán con el Azure Storage.

Si dispone de cifrado del disco de Azure habilitada para los discos de hello en una máquina virtual y SSE habilitado en la cuenta de almacenamiento de hello manteniendo los archivos de disco duro virtual de hello, funcionará bien; se producirá en los datos recién escritos que se cifraron dos veces.

## <a name="storage-analytics"></a>Storage Analytics
### <a name="using-storage-analytics-toomonitor-authorization-type"></a>Uso de tipo de análisis de almacenamiento de autorización toomonitor
Para cada cuenta de almacenamiento, puede habilitar el registro de tooperform de análisis de almacenamiento de Azure y almacenar datos de métricas. Esto es una herramienta excelente toouse cuando se desea métricas de rendimiento de hello toocheck de una cuenta de almacenamiento, o bien debe tootroubleshoot una cuenta de almacenamiento porque tiene problemas de rendimiento.

Otra parte de los datos que se puede ver en los registros de análisis de almacenamiento de hello es método de autenticación de hello usado por alguien cuando tienen acceso a almacenamiento de información. Por ejemplo, con el almacenamiento de blobs, puede ver si utilizan una firma de acceso compartido o claves de cuenta de almacenamiento de hello, o si tiene acceso de blob de Hola es público.

Esto puede ser muy útil si está protegiendo estrechamente toostorage de acceso. Por ejemplo, en almacenamiento de blobs puede establecer todos Hola contenedores tooprivate y la implementación de un uso Hola de un servicio SAS a lo largo de las aplicaciones. A continuación, puede comprobar Hola con regularidad registra toosee si los blobs son accesibles mediante claves de cuenta de almacenamiento de hello, lo que pueden indicar una infracción de seguridad, o blobs de hello son públicos pero no debe ser.

#### <a name="what-do-hello-logs-look-like"></a>¿Hello registros aspecto?
Después de habilitar las métricas de cuenta de almacenamiento de Hola y el registro a través del portal de Azure de hello, datos de análisis se iniciará tooaccumulate rápidamente. registro de Hello y métricas para cada servicio es independiente; sólo se escribe el registro de Hello cuando hay actividad en esa cuenta de almacenamiento, mientras que las métricas de Hola se registrará cada minuto, cada hora o cada día, dependiendo de cómo configure.

Hola registros se almacenan en blobs en bloques en un contenedor denominado $logs en la cuenta de almacenamiento de Hola. Este contenedor se crea automáticamente cuando se habilita Storage Analytics. Una vez creado este contenedor, no se puede eliminar, aunque sí puede eliminar su contenido.

En el contenedor $logs hello, hay una carpeta para cada servicio y, a continuación, se dan las subcarpetas Hola año/mes/día/hora. En la hora, simplemente se numeran Hola registros. Esto es qué hello estructura de directorios será similar:

![Vista de archivos de registro](./media/storage-security-guide/image1.png)

Se registra cada tooAzure solicitud almacenamiento. Ésta es una instantánea de un archivo de registro, que muestra hello primera algunos campos.

![Instantánea de un archivo de registro](./media/storage-security-guide/image2.png)

Puede ver que puede usar Hola registros tootrack cualquier tipo de cuenta de almacenamiento de tooa de llamadas.

#### <a name="what-are-all-of-those-fields-for"></a>¿Para qué sirven todos estos campos?
Hay un artículo aparecen en recursos de hello siguientes que proporciona la lista Hola de hello muchos campos de registros de Hola y lo que se usan para. Esta es Hola lista de campos en orden:

![Instantánea de los campos de un archivo de registro](./media/storage-security-guide/image3.png)

Estamos interesados en entradas de Hola para GetBlob y cómo se autentica, por lo que se necesita toolook para las entradas con el tipo de operación "Get" Blob y comprobar el estado de solicitud de hello (4<sup>th</sup> columna) y tipo de autorización de hello (8<sup>th</sup> columna).

Por ejemplo, en Hola primero algunas filas en lista de hello anterior, hello-estado de la solicitud es "Correcto" y Hola autorización-type es "autenticado". Esto significa solicitud Hola se validó con clave de cuenta de almacenamiento de Hola.

#### <a name="how-are-my-blobs-being-authenticated"></a>¿Cómo se autentican mis blobs?
Son tres los casos que nos interesan.

1. Hola blob es público y se tiene acceso mediante una dirección URL sin una firma de acceso compartido. En este caso, estado de solicitud de hello es "AnonymousSuccess" y "anónimo" hello autorización-tipo.

   1.0;2015-11-17T02:01:29.0488963Z;GetBlob;**AnonymousSuccess**;200;124;37;**anonymous**;;mystorage…
2. blob de Hello es privado y se utiliza con una firma de acceso compartido. En este caso, hello-estado de la solicitud es "SASSuccess" y tipo de autorización de hello es "sa".

   1.0;2015-11-16T18:30:05.6556115Z;GetBlob;**SASSuccess**;200;416;64;**sas**;;mystorage…
3. blob de Hello es privado y clave de almacenamiento de hello era tooaccess usado se. En este caso, es el estado de solicitud de Hola "**correcto**"y es de tipo de autorización de Hola"**autenticado**".

   1.0;2015-11-16T18:32:24.3174537Z;GetBlob;**Success**;206;59;22;**authenticated**;mystorage…

Puede usar tooview de analizador de mensajes de Microsoft de Hola y analizar estos registros. Incluye funcionalidades de búsqueda y filtrado. Por ejemplo, puede querer toosearch para instancias de GetBlob toosee si el uso de hello es lo esperado, es decir, toomake seguro de que alguien no se tiene acceso a su cuenta de almacenamiento incorrectamente.

#### <a name="resources"></a>Recursos
* [Análisis de almacenamiento](storage-analytics.md)

  Este artículo contiene información general de análisis de almacenamiento y cómo tooenable ellos.
* [Formato del registro del análisis de almacenamiento](https://msdn.microsoft.com/library/azure/hh343259.aspx)

  Este artículo explica Hola formato de registro de análisis de almacenamiento y detalles Hola campos disponibles en él, incluido el tipo de autenticación, que indica el tipo de saludo de autenticación utilizado para la solicitud de Hola.
* [Supervisar una cuenta de almacenamiento en hello portal de Azure](storage-monitor-storage-account.md)

  Este artículo se muestra cómo tooconfigure de métricas de supervisión y el registro de una cuenta de almacenamiento.
* [Solución integral de problemas con los registros y métricas de Almacenamiento de Azure, AzCopy y el analizador de mensajes](storage-e2e-troubleshooting.md)

  En este artículo se habla de solución de problemas mediante el análisis de almacenamiento de Hola y muestra cómo toouse Hola analizador de mensajes de Microsoft.
* [Guía de funcionamiento del analizador de mensajes de Microsoft](https://technet.microsoft.com/library/jj649776.aspx)

  En este artículo es referencia Hola para hello analizador de mensajes de Microsoft e incluye tutorial tooa de vínculos, inicio rápido y resumen de las características.

## <a name="cross-origin-resource-sharing-cors"></a>Uso compartido de recursos entre orígenes
### <a name="cross-domain-access-of-resources"></a>Acceso entre dominios de recursos
Cuando un explorador web que se ejecuta en un dominio realiza una solicitud HTTP para un recurso desde un dominio diferente, el proceso se denomina solicitud HTTP entre orígenes. Por ejemplo, una página HTML atendida desde contoso.com realiza una solicitud para un jpeg hospedado en fabrikam.blob.core.windows.net. Por motivos de seguridad, los exploradores restringen las solicitudes HTTP entre orígenes iniciadas desde scripts, como JavaScript. Esto significa que cuando algún código JavaScript en una página web en contoso.com solicita ese jpeg en fabrikam.blob.core.windows.net, Explorador de hello no permitirá solicitud Hola.

¿Lo que hace esto tiene toodo con el almacenamiento de Azure? Bueno, si va a almacenar activos estáticos como archivos de datos JSON o XML en el almacenamiento de blobs con una cuenta de almacenamiento llamado Fabrikam, dominio Hola para activos de hello será fabrikam.blob.core.windows.net y aplicación web de hello contoso.com no será capaz de tooaccess ellos con JavaScript porque Hola dominios son diferentes. Esto también es cierto si está probando toocall uno de los servicios de almacenamiento de Azure: por ejemplo, el almacenamiento de tablas: Hola que devuelven JSON datos toobe procesado por el cliente de JavaScript de Hola.

#### <a name="possible-solutions"></a>Posibles soluciones
Una manera de tooresolve se trata de un dominio personalizado como "storage.contoso.com" toofabrikam.blob.core.windows.net tooassign. problema de Hello es que solo se puede asignar esa cuenta de almacenamiento de tooone de dominio personalizado. ¿Qué ocurre si se almacenan recursos de hello en varias cuentas de almacenamiento?

Tooresolve de otra manera se trata de act, toohave hello web application como un proxy para las llamadas de almacenamiento de Hola. Esto significa que si va a cargar un almacenamiento de archivo tooBlob, aplicación web de hello podría escribir de forma local y se, a continuación, copia tooBlob almacenamiento o se leen completamente en la memoria y, a continuación, escribirlo tooBlob almacenamiento. Como alternativa, podría escribir una aplicación web dedicado (por ejemplo, una API Web) que carga los archivos de hello localmente y los escribe tooBlob almacenamiento. En cualquier caso, deberá tooaccount para esa función cuando es necesario determinar escalabilidad Hola.

#### <a name="how-can-cors-help"></a>¿En qué sentido puede resultar útil el uso compartido de recursos entre orígenes?
Almacenamiento de Azure permite tooenable CORS: Cross uso compartido de recursos de origen. Para cada cuenta de almacenamiento, puede especificar los dominios que pueden tener acceso a recursos de hello en esa cuenta de almacenamiento. Por ejemplo, en nuestro caso que se ha descrito anteriormente, podemos habilitar CORS hello fabrikam.blob.core.windows.net cuenta de almacenamiento y configurar tooallow acceso toocontoso.com. A continuación, hello web aplicación contoso.com puede acceder directamente a los recursos de hello en fabrikam.blob.core.windows.net.

Una toonote lo es que CORS permite el acceso, pero no proporciona autenticación, que es necesaria para todos los acceso no público de recursos de almacenamiento. Esto significa que solo se puede acceder a blobs si son públicos o si incluyó una firma de acceso compartido, lo que le otorga Hola permiso adecuado. Las tablas, las colas y los archivos no tienen acceso público y requieren una Firma de acceso compartido.

De forma predeterminada, el uso compartido de recursos entre orígenes está deshabilitado en todos los servicios. Puede habilitar CORS mediante Hola API de REST o hello almacenamiento cliente biblioteca toocall uno Hola métodos tooset Hola de autoservicio. Cuando lo haga, debe incluir una regla de uso compartido de recursos entre orígenes, que está en formato XML. Este es un ejemplo de una regla CORS que se ha establecido mediante la operación Set Service Properties de Hola para hello servicio Blob para una cuenta de almacenamiento. Puede realizar dicha operación mediante la biblioteca de cliente de almacenamiento de Hola o las API de REST de hello para el almacenamiento de Azure.

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Esto es lo que significa cada fila:

* **AllowedOrigins** esto indica qué dominios no coincidente pueden solicitar y recibir datos del servicio de almacenamiento de Hola. En este caso, indica que contoso.com y fabrikam.com pueden solicitar datos desde Blob Storage para una cuenta de almacenamiento específica. También puede establecer este carácter comodín tooa (\*) tooallow tooaccess de dominios todas las solicitudes.
* **AllowedMethods** trata Hola lista de métodos (verbos de solicitud HTTP) que puede usarse al realizar la solicitud de saludo. En este ejemplo, se permiten solo GET y PUT. Puede establecer este carácter comodín tooa (\*) tooallow utiliza toobe de todos los métodos.
* **AllowedHeaders** se trata de solicitud de hello pueden especificar encabezados que Hola dominio de origen al realizar la solicitud de Hola. En el ejemplo anterior, se permiten todos los encabezados de metadatos que comienzan por x-ms-meta-data, x-ms-meta-target y x-ms-meta-abc. Hola carácter comodín (\*) indica que cualquier encabezado que empiece con hello especificado se permite el prefijo.
* **ExposedHeaders** esto indica a qué encabezados de respuesta deben exponerse mediante emisor de solicitud de hello explorador toohello. En este ejemplo, se expondrán los encabezados que empiecen por "x-ms-meta-".
* **MaxAgeInSeconds** es Hola cantidad máxima de tiempo que un explorador almacenará en memoria caché solicitud de hello preparatoria OPTIONS. (Para obtener más información acerca de la solicitud preparatoria de hello, compruebe siguiente artículo primera hello).

#### <a name="resources"></a>Recursos
Para obtener más información acerca de CORS y cómo tooenable, consulte estos recursos.

* [Compatibilidad de uso compartido de recursos entre orígenes (CORS) para servicios de almacenamiento de Azure en Azure.com Hola](storage-cors-support.md)

  Este artículo proporciona información general de CORS y cómo las reglas de tooset Hola Hola diferentes servicios de almacenamiento.
* [Compatibilidad de uso compartido de recursos entre orígenes (CORS) para hello servicios de almacenamiento de Azure en MSDN](https://msdn.microsoft.com/library/azure/dn535601.aspx)

  Se trata de documentación de referencia de hello para la compatibilidad con CORS para servicios de almacenamiento de Azure Hola. Esta aplicación de servicio de almacenamiento de tooeach de tooarticles de vínculos y muestra un ejemplo y explica cada elemento de archivo CORS de hello.
* [Microsoft Azure Storage: Introducing CORS (Almacenamiento de Microsoft Azure: Introducción a uso compartido de recursos entre orígenes)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/02/03/windows-azure-storage-introducing-cors.aspx)

  Este artículo es un vínculo toohello blog inicial anuncio de CORS y que muestra cómo toouse lo.

## <a name="frequently-asked-questions-about-azure-storage-security"></a>Preguntas más frecuentes acerca de la seguridad de Azure Storage
1. **¿Cómo se puede comprobar la integridad de Hola de blobs de hello que estoy transferir entre o salga de almacenamiento de Azure si no puedo usar protocolo HTTPS de hello?**

   Si por algún motivo necesita toouse HTTP en lugar de HTTPS y está trabajando con los blobs en bloques, puede usar la comprobación de MD5 toohelp comprobar integridad de Hola de blobs de Hola que se transfieren. Esto le ayudará con la protección frente a errores de red o de la capa de transporte, pero no necesariamente con ataques de intermediarios.

   Si puede usar HTTPS, que proporciona seguridad de nivel de transporte, el uso de la comprobación de MD5 es redundante e innecesario.

   Para obtener más información, consulte la hello [Introducción a Azure Blob MD5](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/02/18/windows-azure-blob-md5-overview.aspx).
2. **¿Qué hay de cumplimiento de FIPS para hello EE. UU. para el Gobierno de EE. UU.?**

   Hola Estados Unidos información procesamiento estándar Federal (FIPS) define los algoritmos criptográficos aprobados para su uso por EE. UU. Equipos para la protección de Hola de confidencial para el gobierno federal. Habilitar FIPS modo en un servidor de Windows o el escritorio indica Hola SO que se deben usar los algoritmos criptográficos validados por FIPS únicamente. Si una aplicación utiliza algoritmos no compatibles, las aplicaciones de Hola se interrumpirán. Las versiones de.NET Framework 4.5.2 o versiones posteriores, aplicación hello automáticamente pasa algoritmos de toouse conformes a FIPS de algoritmos de criptografía de hello al equipo de Hola se encuentra en el modo FIPS.

   Microsoft deja una tooeach cliente toodecide si tooenable el modo FIPS. Creemos que no hay ninguna razón para los clientes que no son sujeto toogovernment normativa tooenable el modo FIPS de forma predeterminada.

   **Recursos**

* [Why We're Not Recommending “FIPS Mode” Anymore](http://blogs.technet.com/b/secguide/archive/2014/04/07/why-we-re-not-recommending-fips-mode-anymore.aspx) (Por qué ya no recomendamos el "modo FIPS")

  En este artículo de blog se proporciona información general de FIPS y se explica por qué no se habilita el modo FIPS de forma predeterminada.
* [FIPS 140 Validation (Validación FIPS 140)](https://technet.microsoft.com/library/cc750357.aspx)

  Este artículo proporciona información sobre cómo los productos de Microsoft y módulos criptográficos cumplan Hola FIPS estándar para hello EE. UU. de EE. UU.
* ["Criptografía de sistema: usar FIPS algoritmos compatibles con para cifrado, firma y operaciones hash" efectos de la configuración de seguridad en Windows XP y en versiones posteriores de Windows](https://support.microsoft.com/kb/811833)

  En este artículo se habla acerca del uso de Hola de modo FIPS en equipos de Windows más antiguos.
