---
title: "Preguntas más frecuentes sobre administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de hello responde toocommon preguntas, los patrones y prácticas recomendadas en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>P+F de Azure API Management
Obtener Hola respuestas toocommon preguntas, los patrones y prácticas recomendadas para la administración de API de Azure.

## <a name="contact-us"></a>Ponerse en contacto con nosotros
* [¿Cómo puedo formular equipo de administración de API de Microsoft Azure Hola una pregunta?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>Preguntas más frecuentes
* [¿Qué significa que una característica se encuentra en su versión preliminar?](#what-does-it-mean-when-a-feature-is-in-preview)
* [¿Cómo puedo proteger conexión Hola entre la puerta de enlace de administración de API de Hola y Mis servicios back-end?](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [¿Cómo copio mi instancia nueva de administración de API servicio instancia tooa?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [¿Es posible administrar mi instancia de Administración de API mediante programación?](#can-i-manage-my-api-management-instance-programmatically)
* [¿Cómo se agrega un grupo de administradores de toohello de usuario?](#how-do-i-add-a-user-to-the-administrators-group)
* [¿Por qué es Directiva de Hola que deseo tooadd disponible en el editor de directiva de hello?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [¿Cómo se pueden utilizar las versiones de API en API Management?](#how-do-i-use-api-versioning-in-api-management)
* [¿Cómo se configuran varios entornos en una sola API?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [¿Se puede usar SOAP con API Management?](#can-i-use-soap-with-api-management)
* [¿Es la constante de dirección IP de hello administración de API puerta de enlace? ¿Puedo usarla en las reglas de firewall?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [¿Se puede configurar un servidor de autorización de OAuth 2.0 con seguridad AD FS?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [¿Qué método de enrutamiento usa administración de API en ubicaciones geográficas de implementaciones toomultiple?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [¿Puedo usar un toocreate de plantilla de Azure Resource Manager una instancia de servicio de administración de API?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [¿Se puede usar un certificado SSL autofirmado para un back-end?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [¿Por qué obtengo un error de autenticación cuando intento tooclone un repositorio GIT?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [¿Funciona API Management con Azure ExpressRoute?](#does-api-management-work-with-azure-expressroute)
* [¿Por qué es necesaria una subred dedicada en las redes virtuales de estilo Resource Manager cuando API Management está implementado en ellas?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [¿Cuál es el tamaño de subred mínima de hello necesario al implementar la administración de API en una red virtual?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [¿Se puede mover un servicio de administración de API de tooanother de una suscripción?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [¿Existen restricciones de la importación de mi API o problemas conocidos con ella?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>¿Cómo puedo formular equipo de administración de API de Microsoft Azure Hola una pregunta?
Puede ponerse en contacto con nosotros mediante una de estas opciones:

* Publicar sus preguntas en nuestro [foro de MSDN de API Management](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt).
* Enviar un correo electrónico demasiado<mailto:apimgmt@microsoft.com>.
* Enviar una solicitud de característica en hello [foro de comentarios Azure](https://feedback.azure.com/forums/248703-api-management).

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>¿Qué significa que una característica se encuentra en su versión preliminar?
Cuando una característica está en versión preliminar, significa que se estamos buscando activamente comentarios acerca de cómo funciona la característica de Hola para usted. Una característica de vista previa es funcionalmente completa, pero es posible que nos aseguraremos de hacer un importante cambio en comentarios de toocustomer de respuesta. Se recomienda no depender de una característica que está en su versión preliminar en el entorno de producción. Si dispone de ningún tipo de información sobre las características de vista previa, háganoslo saber a través de una de las opciones de contacto de hello en [¿cómo puedo formular equipo de administración de API de Microsoft Azure Hola una pregunta?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question).

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>¿Cómo puedo proteger conexión Hola entre la puerta de enlace de administración de API de Hola y Mis servicios back-end?
Tiene varias opciones toosecure Hola conexión entre la puerta de enlace de administración de API de Hola y los servicios back-end. Puede:

* Use la autenticación básica HTTP. Para más información, consulte [Definición de la configuración de la API](api-management-howto-create-apis.md#configure-api-settings).
* Usar la autenticación mutua de SSL como se describe en [cómo services toosecure back-end mediante la autenticación de certificado de cliente en la administración de API de Azure](api-management-howto-mutual-certificates.md).
* Utilice la lista blanca IP en su servicio back-end. Si tiene una instancia de administración de API de nivel Standard o Premium, la dirección IP de Hola de puerta de enlace de hello permanece constante. Puede establecer la lista blanca de direcciones tooallow esta dirección IP. Puede obtener la dirección IP de hello de la instancia de la administración de API en el panel de Hola Hola portal de Azure.
* Conectar su tooan de instancia de la administración de API red Virtual de Azure.

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>¿Cómo copio mi instancia nueva de administración de API servicio instancia tooa?
Tiene varias opciones si desea que una instancia nueva de administración de API instancia tooa toocopy. Puede:

* Usar copia de seguridad de Hola y restaurar la función de administración de API. Para obtener más información, consulte [cómo tooimplement de recuperación de desastres mediante el uso de servicio de copia de seguridad y restauración en la administración de API de Azure](api-management-howto-disaster-recovery-backup-restore.md).
* Crear su propia copia de seguridad y restaurar la característica mediante hello [API de REST de administración](https://msdn.microsoft.com/library/azure/dn776326.aspx). Utilice toosave de API de REST de Hola y restauración entidades Hola de instancia de servicio de Hola que desee.
* Descargar configuración de servicio de hello mediante Git y, a continuación, cargarla tooa nueva instancia. Para obtener más información, consulte [cómo toosave y configurar la configuración del servicio de administración de API mediante Git](api-management-configuration-repository-git.md).

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>¿Es posible administrar mi instancia de Administración de API mediante programación?
Sí, puede administrar API Management mediante programación utilizando:

* Hola [API de REST de administración](https://msdn.microsoft.com/library/azure/dn776326.aspx).
* Hola [SDK del servicio Administración de biblioteca de Microsoft Azure ApiManagement](http://aka.ms/apimsdk).
* Hola [implementación del servicio](https://msdn.microsoft.com/library/mt619282.aspx) y [administración de servicios](https://msdn.microsoft.com/library/mt613507.aspx) cmdlets de PowerShell.

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>¿Cómo se agrega un grupo de administradores de toohello de usuario?
Aquí es cómo puede agregar un grupo de administradores de toohello de usuario:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Vaya toohello grupo de recursos que tiene una instancia de la administración de API de hello desea tooupdate.
3. Administración de API, asignar Hola **Api administración colaborador** usuario toohello de rol.

Ahora Hola recién agregado colaborador puede usar PowerShell de Azure [cmdlets](https://msdn.microsoft.com/library/mt613507.aspx). Le mostramos cómo toosign en como administrador:

1. Hola de uso `Login-AzureRmAccount` toosign de cmdlet en.
2. Establecer Hola contexto toohello suscripción que tiene servicio hello mediante `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`.
3. Obtenga la dirección URL de inicio de sesión único mediante `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`.
4. Usar portal de administración de hello URL tooaccess Hola.

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>¿Por qué es Directiva de Hola que deseo tooadd disponible en el editor de directiva de hello?
Si la directiva de Hola que desea tooadd aparece atenuado o sombreados en el editor de directivas de hello, asegúrese de que está en el ámbito correcto de Hola de directiva de Hola. Cada instrucción de directiva está diseñada para toouse en ámbitos específicos y secciones de la directiva. secciones de la directiva de tooreview hello y ámbitos para una directiva, consulte uso de la directiva de hello sección [las directivas de administración de API](https://msdn.microsoft.com/library/azure/dn894080.aspx).

### <a name="how-do-i-use-api-versioning-in-api-management"></a>¿Cómo se pueden utilizar las versiones de API en API Management?
Tiene el control de versiones algunas opciones toouse API Administración de API:

* Administración de API, puede configurar distintas versiones de API toorepresent. Por ejemplo, podría tener dos API distintas, MyAPIv1 y MyAPIv2. Un desarrollador puede elegir la versión de Hola Hola desarrollador desea toouse.
* También puede configurar su API con una dirección URL del servicio que no incluya un segmento de versión; por ejemplo: https://my.api. A continuación, configure un segmento de la versión de la plantilla [URL de reescritura](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) de cada operación. Por ejemplo, puede tener una operación con una [plantilla URL](api-management-howto-add-operations.md#url-template) llamada /resource y una plantilla [URL de reescritura](api-management-howto-add-operations.md#rewrite-url-template) denominada /v1/Resource. Puede cambiar el valor del segmento de versión de Hola por separado para cada operación.
* Si desea que tookeep un segmento de versión "predeterminada" hello de la API de dirección URL del servicio, en operaciones seleccionadas, Establece una directiva que usa hello [establecer el servicio back-end](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) ruta de acceso de solicitud de back-end de directiva toochange Hola.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>¿Cómo se configuran varios entornos en una sola API?
tooset varios entornos, por ejemplo, un entorno de prueba y un entorno de producción, en una única API, tiene dos opciones. Puede:

* Host distintas API en Hola mismo inquilino.
* Host hello las mismas API en varios inquilinos.

### <a name="can-i-use-soap-with-api-management"></a>¿Se puede usar SOAP con API Management?
Ahora se admite el [paso a través de SOAP](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/). Los administradores pueden importar Hola WSDL de su servicio de SOAP y administración de API de Azure, se creará un front-end SOAP. Ahora hay documentación del portal para desarrolladores, la consola de prueba, las directivas y el análisis disponible para los servicios SOAP.

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>¿Es la constante de dirección IP de hello administración de API puerta de enlace? ¿Puedo usarla en las reglas de firewall?
En niveles Standard y Premium de hello, dirección IP pública de hello (VIP) del inquilino de administración de API de hello es estático para duración de hello del inquilino de hello, con algunas excepciones. cambios de dirección IP de Hello en estas circunstancias:

* servicio de Hola se elimina y se vuelve a crear.
* suscripción al servicio Hello es [suspendido](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) o [advierte](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (por ejemplo, para nonpayment) y, a continuación, se restablecen.
* Agregar o quitar la red Virtual de Azure (puede usar red Virtual solo en hello desarrollador y nivel Premium).

Para las implementaciones de varias regiones, Hola cambios de dirección regional si región hello es vacantes y, a continuación, se restablecen (puede usar varias regiones implementación solo al nivel Premium de hello).

A los inquilinos de nivel Premium configurados para la implementación en varias regiones se les asigna una dirección IP pública por región.

Puede obtener la dirección (o direcciones IP, en una implementación de varias regiones) en página de inquilino de Hola Hola portal de Azure.

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>¿Se puede configurar un servidor de autorización de OAUth 2.0 con seguridad AD FS?
toolearn tooconfigure un servidor de autorización de OAuth 2.0 con la seguridad de los servicios de federación de Active Directory (AD FS), vea [utilizando ADFS en administración de API](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/).

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>¿Qué método de enrutamiento usa administración de API en ubicaciones geográficas de implementaciones toomultiple?
Administración de API usa hello [método de enrutamiento de tráfico de rendimiento](../traffic-manager/traffic-manager-routing-methods.md#priority) en ubicaciones geográficas de implementaciones toomultiple. El tráfico entrante es toohello enrutado de puerta de enlace API más cercano. Si una región se queda sin conexión, el tráfico entrante es enrutado automáticamente toohello siguiente más cercano puerta de enlace. Aprenda más acerca de los métodos de enrutamiento en [Métodos de enrutamiento de tráfico de Traffic Manager](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>¿Puedo usar un toocreate de plantilla de Azure Resource Manager una instancia de servicio de administración de API?
Sí. Vea hello [servicio de administración de API de Azure](http://aka.ms/apimtemplate) plantillas de inicio rápido.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>¿Se puede usar un certificado SSL autofirmado para un back-end?
Sí. Le mostramos cómo toouse certificado de una firma automática Secure Sockets Layer (SSL) para un back-end:

1. Cree una entidad de [back-end](https://msdn.microsoft.com/library/azure/dn935030.aspx) mediante API Management.
2. Conjunto hello **skipCertificateChainValidation** propiedad demasiado**true**.
3. Si ya no desea tooallow los certificados autofirmados, eliminar la entidad de back-end de Hola o establecer hello **skipCertificateChainValidation** propiedad demasiado**false**.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>¿Por qué obtengo un error de autenticación cuando intento tooclone un repositorio Git?
Si utiliza el Administrador de credenciales de Git, o si está tratando de tooclone un repositorio Git con Visual Studio, puede ejecutar en un problema conocido con el cuadro de diálogo de credenciales de Windows hello. cuadro de diálogo de Hello limita too127 caracteres de la longitud de contraseña, y lo trunca contraseña generada de Microsoft de Hola. Estamos trabajando en acortar contraseña Hola. Por ahora, use Git Bash tooclone su repositorio de Git.

### <a name="does-api-management-work-with-azure-expressroute"></a>¿Funciona API Management con Azure ExpressRoute?
Sí. API Management funciona con Azure ExpressRoute.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>¿Por qué es necesaria una subred dedicada en las redes virtuales de estilo Resource Manager cuando API Management está implementado en ellas?
requisito de subred dedicada de Hello para la administración de API procede del hecho de hello, que se basa en el modelo de implementación estándar (capa de PAAS V1). Aunque se puede implementar a una VNET de administrador de recursos (capa de V2), hay consecuencias toothat. Hello modelo de implementación clásico de Azure no está asociado estrechamente con el modelo del Administrador de recursos de hello de modo que si se crea un recurso en la capa de V2, capa de hello V1 no saberlo y pueden ocurrir problemas, como la administración de API intentar toouse una dirección IP que ya está asignada tooa NIC (compilada en V2).
toolearn más información acerca de la diferencia de los modelos clásico y el Administrador de recursos de Azure, consulte demasiado[diferencia en los modelos de implementación](../azure-resource-manager/resource-manager-deployment-model.md).

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>¿Cuál es el tamaño de subred mínima de hello necesario al implementar la administración de API en una red virtual?
tamaño de la subred mínima de Hello necesarios toodeploy administración de API es [/29](../virtual-network/virtual-networks-faq.md#configuration), que es el tamaño de la subred mínima de Hola que admite Azure.

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>¿Se puede mover un servicio de administración de API de tooanother de una suscripción?
Sí. cómo hacerlo, consulte toolearn [mover tooa de recursos nuevo grupo de recursos o suscripción](../azure-resource-manager/resource-group-move-resources.md).

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>¿Existen restricciones de la importación de mi API o problemas conocidos con ella?
[Problemas conocidos y restricciones](api-management-api-import-restrictions.md) para formatos Open API(Swagger), WSDL y WADL.
