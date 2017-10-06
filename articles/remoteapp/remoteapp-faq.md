---
title: "Preguntas más frecuentes de RemoteApp aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de respuestas toohello preguntas más frecuentes sobre Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: swadhwa
editor: 
ms.assetid: bad66603-91f9-437f-8a70-236405d2a27f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: da981fea9e38b4e74694aeaba5f97c8ed897ccd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-faq"></a>Preguntas más frecuentes sobre Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Hemos sabido Hola después preguntas acerca de RemoteApp de Azure. ¿Tiene alguna otra? Visite hello [RemoteApp foros](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureRemoteApp) y háganos saber lo que necesita tooknow, o un comentario de lista desplegable a continuación.

## <a name="cant-find-what-youre-looking-for-have-a-question-we-didnt-answer"></a>¿No encuentra lo que busca? ¿Tiene alguna pregunta que no hayamos respondido?
Si no se puede encontrar información de hello necesita, o tiene una pregunta adicional que no nos estamos cubriendo aquí, consulte toohello [foro de Azure RemoteApp](http://aka.ms/araforum) y formule su pregunta no existe. Siempre es posible agregar más respuestas aquí.

## <a name="what-is-azure-remoteapp"></a>¿Qué es Azure RemoteApp?
* **¿Qué es Azure RemoteApp?** RemoteApp es un servicio de Azure le ayuda a proporcionar acceso remoto seguro tooapplications desde diferentes dispositivos de usuario. Obtenga más información sobre [Azure RemoteApp](remoteapp-whatis.md).
* **¿Qué opciones de implementación de hello?** Hay dos tipos de colecciones de RemoteApp: híbridas y nube. La que necesite dependerá de varios factores, como si es necesaria la unión de dominios. Hablamos acerca de todas esas decisiones [aquí](remoteapp-collections.md).

## <a name="quick-tips-on-using-azure-remoteapp"></a>Sugerencias rápidas para usar Azure RemoteApp
* **¿Cuánto tiempo pasa hasta que me desconecto? ¿Cuánto puedo estar inactivo antes de que permite el arranque de hello?** 4 horas. Si usted o uno de los usuarios está inactivo durante 4 horas, se cerrará automáticamente la sesión de Azure RemoteApp. Desprotección Hola otras configuraciones predeterminadas en [suscripción de Azure y límites de servicio, cuotas y restricciones](../azure-subscription-service-limits.md).
* **¿Puedo probar este servicio de forma gratuita?** Sí. Hay una versión de prueba gratuita durante 30 días. Una vez finalizada la prueba de hello, puede realizar la transición tooa cuenta (que puede usar en producción) o dejar de usar el servicio de Hola de pago. Iniciar la prueba gratuita, vaya demasiado[portal.azure.com](http://portal.azure.com) -crear una nueva instancia de RemoteApp. Con la versión de prueba gratuita de hello, puede compilar 2 instancias de RemoteApp de 10 usuarios por cada instancia. Recuerde que esta versión de prueba solo tiene una duración de 30 días.
  
  ## <a name="azure-remoteapp-subscription-details"></a>Detalles de la suscripción de Azure RemoteApp
* **¿Cuáles son los límites de servicio de hello?** Se puede obtener información sobre la configuración predeterminada de Hola y servicios como límites de Azure RemoteApp en [suscripción de Azure y límites de servicio, cuotas y restricciones](../azure-subscription-service-limits.md). Indíquenos si tiene otras preguntas.
* **¿El número de usuarios realice tengo toohave?** Hay un mínimo de 20 usuarios. Que es lo mismo que toobe muy clara: Hola mínimo es 20. Se le facturarán 20. 
* **¿Cuánto cuesta RemoteApp?** Consulte [Detalles de precios de RemoteApp de Azure ](https://azure.microsoft.com/pricing/details/remoteapp/).
* **¿Un tipo de colección cuesta más que otro?** Sí, puede que sí, según los requisitos de la colección. Una colección híbrida requiere una conexión de red de Azure RemoteApp tooyour local. Si utiliza una ruta de red virtual (VNET) o una ExpressRoute existente, no se genera ningún costo adicional. Pero si usa una nueva red virtual de Azure y una puerta de enlace o Express Route, se le cobrará para hello [puerta de enlace VPN](https://azure.microsoft.com/pricing/details/vpn-gateway) o [Express Route](https://azure.microsoft.com/pricing/details/expressroute/). Este costo (lo que se detallan en vínculos de hello) es encima de su Azure RemoteApp mensual de costes.

## <a name="collections---whats-supported-which-should-you-use-and-others"></a>Colecciones: cuáles son compatibles, cuáles debe usar, etc.
* **¿Son compatibles las aplicaciones personalizadas de línea de negocio (LOB)?** Sí. crear una aplicación personalizada en Azure RemoteApp, toouse una [imagen de plantilla personalizada](remoteapp-create-custom-image.md)y, a continuación, cargarlo toohello colección de RemoteApp.
* **¿Funcionará mi aplicación de LOB personalizado en Azure RemoteApp?**  Hola mejor toofigure de manera que out es tootest lo. Extraer del repositorio hello [centro de compatibilidad de escritorio remoto](http://www.rdcompatibility.com/compatibility/default.aspx).
* **¿Qué método de implementación (nube o híbrida) es mejor para mi organización?** Las colecciones de híbrida proporcionan experiencia más completa de hello si desea una integración completa con el inicio de sesión único (SSO) y conectividad de red local protegido. Colecciones en la nube proporcionan una manera fácil y ágil tooisolate la implementación mediante el uso de varios métodos de autenticación. Obtener más información acerca de hello [opciones de implementación](remoteapp-whatis.md).
* **Tenemos SQL u otra base de datos en implementación local o en Azure. ¿Qué tipo de implementación debemos usar?** Depende de dónde esté la base de datos SQL o back-end. Si la base de datos de hello está en una red privada, utilice colección híbrida de Hola. Si base de datos de hello toohello expuesto Internet y permite tooit tooconnect de conexiones de cliente, puede usar la colección de hello en la nube.
* **¿Qué sucede con las características de asignación de unidad, puerto serie y USB, uso compartido del Portapapeles y redirección de impresora?** Todas estas características se admiten en RemoteApp de Azure. El uso compartido del Portapapeles y la redirección de impresora se habilitan de forma predeterminada. Puede obtener más información sobre la redirección [aquí](remoteapp-redirection.md). 

## <a name="template-images"></a>Imágenes de plantillas
* **¿Puedo usar una nube o una máquina virtual existente como plantilla de Hola para Mi colección de RemoteApp?** Sí. Puede crear una imagen basada en una máquina virtual de Azure, use uno de imágenes de hello incluidas con su suscripción o crear una imagen personalizada. Extraer del repositorio hello [opciones de imagen de RemoteApp](remoteapp-imageoptions.md).

## <a name="network-options"></a>Opciones de red
* **colección de Hello híbrida requiere una red virtual. ¿Podemos usar nuestra red virtual existente?** Puede hacerlo si hello red virtual existente es una red virtual de Azure. Consulte "paso 1: configurar la red virtual" Hola [instrucciones de colección híbrida](remoteapp-create-hybrid-deployment.md) para obtener más información.
* **¿Puedo usar una red virtual con una colección de nube?** Sí, claro. Consulte [Creación de una colección en la nube](remoteapp-create-cloud-deployment.md), especialmente el paso 1, para obtener más información.

## <a name="authentication-options"></a>Opciones de autenticación
* **¿Qué ocurre con la autenticación? ¿Los métodos que son compatibles?**  colección de hello en la nube es compatible con cuentas de Microsoft y cuentas de Azure Active Directory, que son también cuentas de Office 365. colección de Hello híbrida admite solo las cuentas de Azure Active Directory que se han sincronizado (mediante una herramienta como [sincronización de Azure Active Directory](http://blogs.technet.com/b/ad/archive/2014/09/16/azure-active-directory-sync-is-now-ga.aspx)) de una implementación de Windows Server Active Directory; en concreto, ya sea sincronizado con hello Opción de sincronización de contraseña o sincronizados con la federación de servicios de federación de Active Directory (AD FS) configurada. También puede configurar [Multi-Factor Authentication (MFA)](https://azure.microsoft.com/services/multi-factor-authentication/).

> [!NOTE]
> los usuarios de Azure Active Directory de Hello deben ser de inquilino de Hola que esté asociada con su suscripción. (Puede ver y modificar su suscripción en hello **configuración** portal Hola de. Vea [inquilino de Azure Active Directory de cambio hello usa RemoteApp](remoteapp-changetenant.md) para obtener más información.)
> 
> 

* **¿Por qué no puedo dar mi acceso a la cuenta de Azure Active Directory?**  los usuarios de Azure Active Directory de hello deben ser del directorio de Hola que esté asociada con su suscripción. Puede ver o modificar ese directorio en la ficha de configuración de hello en el portal de Hola. Vea [inquilino de Azure Active Directory de cambio hello usa RemoteApp](remoteapp-changetenant.md) para obtener más información.

## <a name="clients---what-device-can-i-use-tooaccess-azure-remoteapp"></a>¿Los clientes - cuál es el dispositivo puede usar tooaccess Azure RemoteApp?
Puede encontrar información de cliente buena, incluidos los pasos para instalar clientes diferentes de hello en [obtiene acceso a las aplicaciones de Azure RemoteApp](remoteapp-clients.md).

* **¿Qué dispositivos y sistemas operativos son aplicaciones de cliente de hello compatibles con?**
  Primero, los equipos de Hola y tabletas: 
  
  * Windows 10 (vista previa del cliente)
  * Windows 8.1 y Windows 8
  * Windows 7 Service Pack 1
  * Mac OS X
  * Windows RT
  * Tabletas Android
  * iPads

    Y los teléfonos de hello:
  * iPhone
  * Teléfono Android
  * Windows Phone
    
    [Descargar](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) ahora un cliente de RemoteApp.
* **¿Admite RemoteApp de Azure clientes ligeros?** Sí, hello clientes ligeros de Windows Embedded siguientes se admiten:
  
  * Windows Embedded Standard 7
  * Windows Embedded 8 Standard
  * Windows Embedded 8.1 Industry Pro
  * Windows 10 IoT Enterprise
* **¿Qué versión de Windows Server es compatible con hello Host de sesión de escritorio remoto (RDSH)?** Windows Server 2012 R2.

## <a name="support-and-feedback"></a>Soporte y comentarios
* **¿Cuál es el plan de soporte técnico de Hola para RemoteApp?** Se ofrecen de forma gratuita los servicios de asistencia para facturación y administración de suscripciones. El soporte técnico está disponible a través de hello [planes de servicio de Azure](https://azure.microsoft.com/support/plans/). También puede obtener soporte técnico gratuito de la comunidad a través de nuestro [foro de discusión de Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp). 
* **¿Cómo puedo enviar comentarios?** Visite hello [foro de comentarios](https://feedback.azure.com/forums/247748-azure-remoteapp/).
* **¿Que puedo hablar la toolearn más información acerca de Azure RemoteApp?** En suma tooour [foro de discusión](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp), que es idóneo toopost preguntas, puede combinar Hola semanalmente [pida seminario Web de expertos de hello](https://azureinfo.microsoft.com/US-Azure-WBNR-FY15-11Nov-AzureRemoteAppAskTheExperts-Registration-Page.html), donde se van a describir todos los aspectos de RemoteApp.
* **¿Existe documentación sobre RemoteApp?** Nos encanta que lo haya preguntado. ¿Además el contenido de Ayuda de portal de hello de la Ayuda de toohello (simplemente haga clic en hello **?** en cualquier página de portal de hello), Hola siguientes artículos está disponible tooteach todo acerca de RemoteApp:
  
  * **Introducción:**
    * [¿Qué es RemoteApp?](remoteapp-whatis.md)
    * [¿Qué es imágenes de plantilla de RemoteApp Hola?](remoteapp-images.md)
    * [¿Cómo funciona la concesión de licencias?](remoteapp-licensing.md)
    * [¿Cómo funcionan conjuntamente RemoteApp y Office?](remoteapp-o365.md)
    * [¿Cómo funciona la redirección en RemoteApp](remoteapp-redirection.md)?
  * **Implementación:**
    * [Creación de una imagen de plantilla personalizada](remoteapp-create-custom-image.md)
    * [Creación de una colección híbrida](remoteapp-create-hybrid-deployment.md)
    * [Creación de una colección en la nube](remoteapp-create-cloud-deployment.md)
    * [Configuración de Active Directory para RemoteApp](remoteapp-ad.md)
    * [Publicación de una aplicación en RemoteApp](remoteapp-publish.md)
  * **Administración:**
    
    * [Incorporación de usuarios](remoteapp-user.md)
    * [Prácticas recomendadas para configurar y usar RemoteApp](remoteapp-bestpractices.md)    
    
    Vídeos También tenemos una serie de vídeos acerca de RemoteApp. Algunos proporcionan Introducción ([tooAzure Introducción RemoteApp](https://azure.microsoft.com/documentation/videos/cloud-cover-ep-150-azure-remote-app-with-thomas-willingham-and-nihar-namjoshi/)) mientras que otros le guían a través de la implementación ([implementación de nube](https://www.youtube.com/watch?v=3NAv2iwZtGc&feature=youtu.be) y [implementación híbrida](https://www.youtube.com/watch?v=GCIMxPUvg0c&feature=youtu.be)). Écheles un vistazo.

### <a name="help-us-help-you"></a>Permítanos ayudarle
¿Sabía que en suma toorating este artículo y realizar comentarios hacia abajo, a continuación, puede realizar cambios toohello artículo? ¿Falta algo? ¿Algo no es correcto? ¿Algo de lo que he escrito es simplemente confuso? Desplazarse hacia arriba y haga clic en **editar en GitHub** toomake cambios - los procederán toous para su revisión y, a continuación, una vez que se aprueban en ellos, podrá ver los cambios y mejoras aquí.

