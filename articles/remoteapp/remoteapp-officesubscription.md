---
title: "aaaHow toouse la suscripción a Office 365 con Azure RemoteApp | Documentos de Microsoft"
description: "Obtenga información acerca de cómo puede utilizar la suscripción a Office 365 en Azure RemoteApp tooshare las aplicaciones de Office."
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: f82b6e23-2b71-47be-846d-fd93f2652f3c
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2648868dd28cbcd93e38461ae6dce25eaa5d5e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-your-office-365-subscription-with-azure-remoteapp"></a>¿Cómo toouse la suscripción a Office 365 con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

¿Sabía que puede usar su suscripción de Office 365 existente en las aplicaciones de Office de Azure RemoteApp tooshare de nube de hello? Siga leyendo para obtener información sobre el Office 365 + opciones de RemoteApp de Azure, incluidos tooarticles vínculos acerca de Office 365 que le ayudarán a realizar Hola más de su suscripción.

## <a name="how-do-i-use-office-365-accounts-for-azure-remoteapp"></a>¿Cómo uso cuentas de Office 365 para Azure RemoteApp?
Extraer del repositorio nuevo artículo de Peter para todos Hola información: [cómo toouse Azure RemoteApp con cuentas de usuario de Office 365](remoteapp-o365user.md)

## <a name="can-i-use-my-office-365-subscription-toorun-office-applications-in-azure-remoteapp"></a>¿Puedo usar mis aplicaciones de Office de toorun de suscripción de Office 365 en Azure RemoteApp?
Sí. De hecho, use su suscripción de Office 365 es Hola solo forma toobring su tooAzure de las aplicaciones de Office RemoteApp.

(Nota: si la implementación de Azure RemoteApp se envía por un socio de hospedaje, pueden ser capaz de tooprovide con licencias de Office en función de un [el contrato de licencia de proveedor de servicio](http://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx))

Hello gran ventaja de la suscripción a Office 365 es que permite usar Hola mismo licencias de usuario en muchos entornos, incluidos Hola nube de Azure y distintas plataformas. Cuando se usan las aplicaciones de Office en Azure RemoteApp no necesita toopurchase más licencias o configurar sus licencias existentes de ninguna manera especial. Todo lo que necesita es una suscripción de Office 365 que incluya [Office 365 ProPlus](https://technet.microsoft.com/library/Gg702619.aspx).

Office 365 ProPlus permite la [activación en equipos compartidos](https://technet.microsoft.com/library/Dn782860.aspx) ; esta característica permite la activación temporal de usuarios en Office en entornos virtuales y en la nube, como Azure RemoteApp (y Servicios de Escritorio remoto).

¿Qué planes de Office 365 incluyen Office 365 ProPlus? Extraer del repositorio hello [disponibilidad dentro de cada plan de servicio](https://technet.microsoft.com/library/office-365-plan-options.aspx) tabla. Tenga en cuenta que no todos los planes incluyen Office 365 ProPlus (por ejemplo, el plan de Office 365 empresa hello). Si el plan no lo hace, considere la posibilidad de actualizar el plan de tooa que realiza (por ejemplo, Office 365 educación E3).

## <a name="ok-so-how-are-my-office-365-proplus-licenses-used-with-azure-remoteapp"></a>De acuerdo, así que ¿cómo se usan mis licencias de Office 365 ProPlus con Azure RemoteApp?
Cada licencia de usuario para Office 365 ProPlus permite a un único usuario activar las aplicaciones de Office en los equipos de too5 más tabletas y teléfonos. Cada activación está registrado con el usuario de hello hasta que desactive Office en el dispositivo de Hola. (Los usuarios pueden administrar sus dispositivos en hello [portal de Office 365](https://portal.office365.com/).)

Con Azure RemoteApp un único usuario podría iniciar sesión en varios equipos en hello mismo día sin que se dé cuenta. Eso es porque servicio Hola automáticamente administra y escala recursos en nube de hello, mientras Hola usuario solo ve Hola aplicaciones y programas que ha compartido. Para este escenario de Office 365 ProPlus ofrece un modo de activación de equipo compartido: Esto significa que el usuario no necesita toodo cualquier tooaccess de administración de licencias esos recursos y que los equipos individuales hello no cuentan para el límite de activaciones de hello 5 equipo.

Siempre y cuando (Hola, administrador) asigna licencias de Office 365 ProPlus tooyour a los usuarios, puede utilizar Office en sus dispositivos personales, así como a través de la colección de RemoteApp de Azure.

## <a name="which-office-applications-can-i-use-with-office-365-and-azure-remoteapp"></a>¿Qué aplicaciones de Office se pueden usar con Office 365 y Azure RemoteApp?
Puede usar el tooactivate de suscripción de Office 365 y compartir Office 2013 en las implementaciones de Azure RemoteApp. Actualmente no admitimos hello uso de otras versiones de Office con Azure RemoteApp. Esto incluye Office 2003, Office 2007, Office 2010 y Office 2016.

## <a name="what-about-visio-pro-or-project-pro"></a>¿Qué sucede con Visio Pro o Project Pro?
imagen de Office 365 ProPlus Hola incluido en su suscripción de RemoteApp incluye Visio Pro y Project Pro. Pero no puede usar su tooactivate de suscripción de Office 365 ProPlus esos programas; cada uno de ellos tiene su propia licencia. Puede activarlas en hello [portal de Office 365](https://portal.office365.com/). 

No tienes toolicense estos programas si no desea toouse ellos. Simplemente activar programas de Hola que desee toouse - y omite Hola a otros usuarios. Podrá verlas en la imagen de hello, pero no se pueden usar. 

## <a name="how-do-i-get-started-with-office-365-and-azure-remoteapp"></a>¿Cómo puedo comenzar con Office 365 y Azure RemoteApp?
Ahora que conoce los detalles de Hola de licencia de Office 365, vamos a ayudarle a comenzar a usar en Azure RemoteApp: es muy fácil:

Cuando se crea la colección de RemoteApp de Azure, use hello **Office 365 ProPlus (suscripción requerido)** imagen.

![Imagen de Azure RemoteApp con Office 365 Pro Plus](./media/remoteapp-officesubscription/remoteapp-officeimage.png)

Esta imagen contiene la versión más reciente de Hola de Windows Server y Office 365 ProPlus. Después de configurar la colección (incluidas las aplicaciones publicación), los usuarios simplemente inician sesión en Azure RemoteApp (mediante su cliente de RemoteApp) y proporcionan sus credenciales de Office 365 para las aplicaciones de Office. Las licencias se entregan automáticamente sin necesidad de ninguna configuración o administración.

## <a name="can-i-create-a-custom-image-with-office-365-proplus"></a>¿Puedo crear una imagen personalizada con Office 365 ProPlus?
Puede crear una imagen personalizada de la colección que incluye Office 365 ProPlus. Hay 2 opciones: usar la imagen de galería de Azure de hello que proporcionamos o bien puede crear su propia imagen personalizada e instalar Office 365 ProPlus no existe.

### <a name="use-hello-azure-gallery-image"></a>Usar la imagen de la Galería de Azure de Hola
toodeploy de manera más fácil de Hello Office 365 ProPlus colección tooa es demasiado[empezar con uno de imágenes de la Galería de Azure de hello](remoteapp-image-on-azurevm.md) incluido en su suscripción de Azure RemoteApp. Asegúrese de que elige hello **Host de sesión de escritorio remoto de Windows de servidor con Office 365 ProPlus preinstalado** imagen. A continuación, instalar ninguna otra aplicación que desee en esa imagen y está listo toogo.

### <a name="use-a-custom-image"></a>Uso de una imagen personalizada
Siempre puede crear una imagen personalizada, puede crear un [Azure VM](remoteapp-image-on-azurevm.md) o [crear localmente la imagen de hello](remoteapp-create-custom-image.md) y cargarlo tooAzure. En cualquier caso, asegúrese de que instalar Office 365 ProPlus con nodo de activación de hello equipo compartido. Hola de uso [herramienta de implementación de Office](http://blogs.technet.com/b/odsupport/archive/2014/07/11/using-the-office-deployment-tool.aspx) y siga hello [instrucciones](https://technet.microsoft.com/library/Dn782858.aspx) para la instalación.  

### <a name="disable-automatic-updates-for-office-365-proplus-in-your-custom-image---important"></a>Deshabilite las actualizaciones automáticas para Office 365 ProPlus en la imagen personalizada. IMPORTANTE:
La imagen personalizada se usa RemoteApp de Azure como una plantilla para agregar recursos adicionales como demanda Hola desde los aumentos de los usuarios. tooprevent retrasos y problemas de conexión, debe deshabilitar las actualizaciones automáticas para Office en imagen Hola. Si no lo hace, todos los recursos creados con dicha plantilla se actualizarán automáticamente cuando se inicie. Utilice en su lugar, proceso de Azure RemoteApp estándar de Hola para actualizar la imagen personalizada. Este modo actualizar las aplicaciones de Office de hello una vez en la imagen de plantilla de hello y, a continuación, dejar que Azure RemoteApp tenga cuidado de obtener actualizaciones de hello tooyour a los usuarios.

las actualizaciones automáticas de toodisable, agregue Hola siguiente toohello el archivo de configuración de la herramienta de implementación de Office:

        <Updates Enabled="FALSE" />

Ahora, el archivo de configuración debe contener estas líneas:

        <Display Level="NONE" AcceptEULA="TRUE" />
        <Property Name="SharedComputerLicensing" Value="1" />
        <Updates Enabled="FALSE" />

## <a name="so-how-can-i-update-an-image-with-office-365-proplus"></a>Entonces, ¿cómo puedo actualizar una imagen con Office 365 ProPlus?
Hay muchas imágenes de hello tooupdate de razones en la colección. Estas son algunas:

* Obtener las últimas actualizaciones de Windows hello 
* Obtener actualizaciones de aplicaciones de Office 365 ProPlus más recientes de Hola
* Actualizar la aplicación personalizada
* Cambiar otras opciones de configuración para la propia imagen de Hola

Para obtener pasos hello-to-end para actualizar la imagen de hello toouse de colección actualiza, vaya [aquí](remoteapp-update.md). Pero para obtener información sobre cómo tooupdate Hola imagen y Office 365 ProPlus, desproteger Hola siguiente información.

Tiene dos opciones para actualizar la imagen: reemplazar la imagen por una completamente nueva o actualizar manualmente la imagen existente.

### <a name="replace-your-image-with-hello-latest-azure-gallery-image--add-customizations"></a>Reemplace la imagen con la última imagen de la Galería de Azure de hello + agregar personalizaciones
Con esta opción, dejar que Microsoft ocuparse de las actualizaciones de Windows Server y Office 365 ProPlus Hola. En lugar de actualizar la imagen existente, podrá crear una imagen completamente nueva basada en la última imagen de la Galería de Hola. A continuación, repita los pasos que hizo antes de la imagen de hello toocustomize - instalar aplicaciones personalizadas, modificar configuración de la imagen de hello etcetera.

imágenes de la Galería de Hola se actualizan periódicamente, por lo que puede colocar la forma más fácil, saber que las aplicaciones de Windows Server y Office 365 ProPlus están toodate. Por supuesto, ventajas y desventajas de hello son que tenga tooapply sus personalizaciones cada vez que reciba una nueva imagen. Puede crear tooautomate scripts establecer sus personalizaciones.

### <a name="manually-update-your-existing-image"></a>Actualización manual de la imagen existente
Con esta opción, se usa la imagen de toohello de actualizaciones tooapply de herramientas de Windows estándar. Para Office 365 ProPlus, utilice toodownload de herramienta de implementación de Office de hello e instale las actualizaciones más recientes de Hola o versiones de Office 365 ProPlus.

> [!IMPORTANT]
> Recuerde: deshabilitar las actualizaciones automáticas Office 365 ProPlus Hola.
> 
> 

¿Necesita más información sobre el uso de hello herramienta de implementación de Office para las actualizaciones?

* [Implantar hacer clic en ejecutar para productos de Office 365 con hello herramienta de implementación de Office](https://technet.microsoft.com/library/JJ219423.aspx)
* [Implementación y actualización de Office 365 ProPlus mediante la herramienta de implementación de Office de Hola](https://channel9.msdn.com/Events/Ignite/2015/BRK3168) (vídeo)
* [Configuración de las opciones de actualización de Office 365 ProPlus](https://technet.microsoft.com/library/dn761708.aspx)

