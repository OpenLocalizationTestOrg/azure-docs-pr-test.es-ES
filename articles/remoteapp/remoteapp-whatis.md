---
title: "¿aaaWhat es Azure RemoteApp? | Microsoft Docs"
description: "Obtenga información acerca de cómo dispositivo de tooany de tooshare aplicaciones y los recursos a través de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e13909f3a5698f58c7e4348f3ce53f43560f9b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-remoteapp"></a>¿Qué es Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

RemoteApp de Azure ofrece funcionalidad de Hola de programa de RemoteApp de Microsoft local hello, respaldado por servicios de escritorio remoto, tooAzure. Azure RemoteApp le ayuda a proporcionar acceso remoto seguro tooapplications desde diferentes dispositivos de usuario. Azure RemoteApp básicamente hospeda las sesiones de Terminal Server no son persistentes en la nube de Hola y obtener toouse ellos y compartirlos con los usuarios.

Con Azure RemoteApp puede compartir aplicaciones y recursos con usuarios en prácticamente cualquier dispositivo. Le permite hospedar las aplicaciones en nube de hello, es decir, que nosotros nos encargamos de hardware de Hola y ajuste de escala toomeet peticiones de usuario. Lo único que toodo es cargar Hola aplicaciones que desee tooshare y, a continuación, obtener su toouse a los usuarios de esas aplicaciones. [Los usuarios obtienen tookeep sus propios dispositivos](remoteapp-clients.md), mientras que administrar todo el contenido a través de hello portal de Azure. Incluso tendrá posibilidad de Hola de con sus credenciales corporativas, lo que le permite garantizar la seguridad de Hola de aplicaciones y datos.

Siga leyendo para obtener más información sobre Azure RemoteApp o, si ya está convencido, [pruébela ahora](https://azure.microsoft.com/services/remoteapp/).

¿Tiene preguntas acerca de Azure RemoteApp? Consulte nuestras [preguntas más frecuentes](remoteapp-faq.md).

RemoteApp de Azure es parte del programa Hola a [infraestructura de Escritorio Virtual de Microsoft](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx).

**¡Nuevo!** ¿Desea toolearn más información acerca de Azure RemoteApp? ¿O bien, está listo toovalidate RemoteApp de Azure a escala? Únase a nuestra semanal [solicite a los expertos de hello seminario Web](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website).

## <a name="azure-remoteapp-collections"></a>Colecciones de Azure RemoteApp
Hay dos tipos de [colecciones de Azure RemoteApp](remoteapp-collections.md):

* A **colección en la nube** se hospeda en y almacena los datos para los programas en la nube de Hola. Los usuarios pueden acceder a las aplicaciones mediante el inicio de sesión con sus cuentas de Microsoft o credenciales corporativas sincronizadas o federadas con Azure Active Directory.
  
    Elija una colección en la nube cuando la aplicación hello desea tooshare no requiere un recurso de conexión tooany red privada de su empresa (por ejemplo, a través de un dispositivo VPN). Si la aplicación hello utiliza recursos de hello Internet, OneDrive, o a Azure, una colección en la nube funcionará para usted. También es más rápida toocreate de Hola.
* A **colección híbrida** se hospeda en y almacena los datos en la nube de Azure Hola pero también permite a los usuarios obtener acceso a datos y recursos almacenados en la red local. Los usuarios pueden acceder a las aplicaciones mediante el inicio de sesión con sus credenciales corporativas sincronizadas o federadas con Azure Active Directory.
  
    Elija una colección híbrida si necesitas una tooresources de conexión de red privada de su empresa. Por ejemplo, si hello aplicación necesita tener acceso a tooone de siguientes hello:
  
  * Servidores de archivos ubicados en la intranet
  * Quicken
  * Bases de datos detrás de un firewall
    
    Normalmente es más útil para grandes organizaciones con una gran cantidad de recursos en sus redes privadas que no se pueden mover toohello en la nube.

tiene opciones diferentes, incluidas las redes Hello colecciones diferentes, por lo que se pueda determinar [qué colección](remoteapp-collections.md) funciona mejor para usted. 

### <a name="updating-your-collection"></a>Actualización de la colección
Uno de hello las principales diferencias entre colecciones de híbrida y nube hello es cómo se administran las actualizaciones de software. Con una colección en la nube que utiliza la imagen preinstalada de Office 365 ProPlus u Office 2013 hello, no es necesario tooworry sobre las actualizaciones. servicio de Hello mantiene propio e implementa las actualizaciones de forma continuada, tooboth aplicaciones y sistema operativo de Hola.

Para colecciones híbrida, así como las colecciones de nube que usen una imagen de plantilla personalizada, se va a encargar de mantenimiento de aplicaciones y la imagen de Hola. Para imágenes unidas a dominio, puede controlar las actualizaciones mediante herramientas como Windows Update, directiva de grupo o System Center.

Después de actualizar la imagen de plantilla personalizada, cargue Hola nueva imagen toohello nube de Azure y, a continuación, actualizar la nueva imagen de hello colección toouse Hola. (Puede hacerlo desde hello Azure RemoteApp **inicio rápido** página o panel de Hola.)

Vea [Actualización de la colección](remoteapp-update.md) para obtener más información.

## <a name="supported-remoteapp-clients"></a>Clientes compatibles con RemoteApp
RemoteApp de Azure es compatible con las aplicaciones de cliente de Windows y Windows RT Hola RemoteApp, así como las aplicaciones de escritorio remoto de Microsoft de Hola para Mac, iOS y Android. Los usuarios pueden usar estas aplicaciones para su móvil o proceso dispositivos tooaccess Hola nuevos programas de RemoteApp de Azure.

Vea [obtiene acceso a las aplicaciones de Azure RemoteApp](remoteapp-clients.md) para obtener más información acerca de los clientes de Hola.

## <a name="next-steps"></a>Pasos siguientes
Venga, pruébelo. Estos artículos le ayudarán a comenzar a usar Azure RemoteApp:

* [¿Qué tipo de colección necesita para Azure RemoteApp?](remoteapp-collections.md)
* [Creación de una imagen de Azure RemoteApp](remoteapp-imageoptions.md)
* [¿Cómo toocreate una colección en la nube de Azure RemoteApp](remoteapp-create-cloud-deployment.md)
* [¿Cómo toocreate una colección híbrida de RemoteApp de Azure](remoteapp-create-hybrid-deployment.md)
* [¿Cómo funciona la concesión de licencias de RemoteApp de Azure?](remoteapp-licensing.md)
* [Prácticas recomendadas para usar RemoteApp de Azure](remoteapp-bestpractices.md)
* [Preguntas más frecuentes sobre RemoteApp de Azure](remoteapp-faq.md)

### <a name="help-us-help-you"></a>Permítanos ayudarle
¿Sabía que en suma toorating este artículo y realizar comentarios hacia abajo, a continuación, puede realizar cambios toohello artículo? ¿Falta algo? ¿Algo no es correcto? ¿Algo de lo que he escrito es simplemente confuso? Desplazarse hacia arriba y haga clic en **editar en GitHub** o **editar** toomake cambios - los procederán toous para su revisión y, a continuación, una vez que se aprueban en ellos, podrá ver los cambios y mejoras aquí.

