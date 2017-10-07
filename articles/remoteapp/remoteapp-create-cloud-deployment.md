---
title: "aaaHow toocreate una colección en la nube de RemoteApp de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una implementación de RemoteApp de Azure que guarda los datos en Hola nube de Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a072ad19d8293016382831d48d0af8e0f5e0d458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-cloud-collection-of-azure-remoteapp"></a>¿Cómo toocreate una colección en la nube de Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Hay dos tipos de [colecciones de Azure RemoteApp](remoteapp-collections.md): 

* Nube: reside completamente en Azure. Puede elegir toosave todos los datos en la nube de hello (para una colección de solo nube) o tooconnect su red virtual de colección tooa y guardar datos en él.   
* Híbrido: incluye una red virtual para acceso local: Esto requiere usar Hola de Azure AD y un entorno de Active Directory local.

Este tutorial le guía a través del proceso de Hola de creación de una colección en la nube. Hay cuatro pasos: 

1. Crear una colección de Azure RemoteApp.
2. Opcionalmente, puede configurar sincronización de directorios. Si utilizas Azure AD + Active Directory, tiene toosynchronize a los usuarios, contactos y contraseñas desde el inquilino de Azure AD tooyour de Active Directory local.
3. Publicar aplicaciones.
4. Configurar el acceso del usuario.

**Antes de empezar**

Necesita toodo Hola siguiente antes de crear la colección de hello:

* [Suscribirse](https://azure.microsoft.com/services/remoteapp/) a Azure RemoteApp. 
* Recopilar información acerca de los usuarios de Hola que desee tener acceso toogrant a. Esta información puede ser información de cuentas de Microsoft o información de cuentas de trabajo de Active Directory de usuarios.
* Este procedimiento se supone que es cualquier toouse continuo uno Hola de imágenes de plantilla proporcionados como parte de su suscripción o que ya ha cargado imagen de plantilla de Hola que desea toouse. Si necesita tooupload una imagen de plantilla diferente, puede hacerlo desde la página de hello imágenes de plantilla. Simplemente haga clic en **cargar una imagen de plantilla** y siga los pasos de hello en el Asistente de Hola. 
* Imagen de Office 365 ProPlus de hello toouse ¿desea? Consulte la información [aquí](remoteapp-officesubscription.md).
* ¿Desea tooprovide de aplicaciones personalizadas o programas de línea de negocio? Cree una nueva [imagen](remoteapp-imageoptions.md) y úsela en su colección en la nube.
* Averiguar si es necesario tooconnect tooa red virtual. Si elige tooconnect tooa red virtual, asegúrese de que cumple hello [directrices de ajuste de tamaño](remoteapp-vnetsizing.md) y que TI [puede conectarse tooRemoteApp](remoteapp-vnet.md). Extraer del repositorio hello [artículo de planificación de red virtual ](remoteapp-planvnet.md)para obtener más información.
* Si usa una red virtual, decide si quieres que toojoin lo tooyour dominio de Active Directory local.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>Paso 1: Creación de una colección en la nube (con o sin red virtual)
Use Hola siguientes pasos le indican demasiado**crear una colección de solo nube**:

1. En el portal de administración de hello, ir a página de RemoteApp toohello.
2. Haga clic en **Nuevo > Creación rápida**.
3. Escriba un nombre para la colección y seleccione su región.
4. Elija plan Hola que desea toouse - estándar o básica.
5. Elija hello toouse de plantilla para esta colección. 
   
    **Sugerencia:** incluye su suscripción de RemoteApp [imágenes de plantilla](remoteapp-images.md) que contienen Office 365 o programas Office 2013 (en modo de prueba), algunas publicada (por ejemplo, Word) y otros listo toopublish. También puede crear una [imagen](remoteapp-imageoptions.md) y usarla en su colección en la nube.
6. Haga clic en **Crear colección de RemoteApp**.
   
    **Importante:** puede tardar hasta too30 minutos tooprovision la colección.

Una vez creada la colección RemoteApp de Azure, haga doble clic en el nombre de Hola de colección de Hola. Se abrirá hello **inicio rápido** (página): Esto es donde termine de configurar la recopilación de Hola.

Use Hola siguientes pasos le indican toocreate una **cloud + colección de red virtual**:

1. En el portal de administración de hello, ir a página de Azure RemoteApp toohello.
2. Haga clic en **Nuevo** > **Crear con VNET**.
3. Escriba un nombre para la colección.
4. Elija plan Hola que desea toouse - estándar o básica.
5. Elija Hola red virtual que ya haya creado. ¿No sabe cómo toodo que? Por ahora, los pasos de Hola se encuentran en hello [híbrida](remoteapp-create-hybrid-deployment.md) tema.
6. Decide si quieres que toojoin su dominio de tooyour de la colección. Si es así, necesitará toouse AD Connect toointegrate Azure AD y el entorno de Active Directory. Esto es lo que se trata más adelante en el **paso 2**.
7. Haga clic en **Crear colección de RemoteApp**.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>Paso 2: Configuración de la sincronización de directorios de Active Directory (opcional)
Si desea toouse Active Directory, Azure RemoteApp requiere sincronización de directorios entre Azure Active Directory y los usuarios de toosynchronize de Active Directory local, contactos e inquilino de Azure Active Directory tooyour de contraseñas. Consulte [Configuración de Active Directory para RemoteApp de Azure](remoteapp-ad.md) para obtener información sobre planeación. También puede ir directamente demasiado[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) para obtener información.

## <a name="step-3-publish-apps"></a>Paso 3: Publicar aplicaciones
Una aplicación de Azure RemoteApp es aplicación hello o programa que proporcionan a los usuarios de tooyour. Se encuentra en la imagen de plantilla de Hola que cargó para la colección de Hola. Cuando un usuario tiene acceso a una aplicación, la aplicación hello aparece toorun en su entorno local, pero realmente se ejecuta en una máquina virtual en Azure. 

Antes de que los usuarios pueden tener acceso a aplicaciones, necesita toopublish ellos: permite las aplicaciones que los usuarios acceden a aplicaciones de Hola a través de la publicación Hola cliente de escritorio remoto.

Puede publicar varios tooyour de aplicaciones de la colección de RemoteApp de Azure. En la página de publicación de hello, haga clic en **publicar** tooadd un programa. Puede publicar de hello **iniciar** menú de imagen de plantilla de Hola o mediante la especificación de ruta de acceso de hello en imagen de plantilla de hello para la aplicación hello. Si elige tooadd de hello **iniciar** menú, elija toopublish de aplicación Hola. Si elige tooprovide Hola ruta de acceso toohello aplicación, proporcione un nombre para la aplicación hello y hello toowhere de ruta de acceso que está instalado en la imagen de la plantilla de Hola.

## <a name="step-4-configure-user-access"></a>Paso 4: Configuración del acceso de usuarios
Ahora que ha creado la colección, debe tooadd los usuarios de Hola que desea toobe puede toouse los recursos remotos. Si está utilizando Active Directory, los usuarios de Hola que proporcione acceso tooneed tooexist en el inquilino de Active Directory de hello asociados con suscripción de hello utilizan toocreate esta colección.

1. En la página de inicio rápido de hello, haga clic en **configurar el acceso de usuario**. 
2. Escriba Hola cuenta profesional (Active Directory) o la cuenta de Microsoft que desee tener acceso toogrant para.
   
   **Notas:** 
   
   Asegúrese de que usa hello  *user@domain.com*  formato.
   
   Si utilizas Office 365 ProPlus en la colección, debe usar las identidades de Active Directory de Hola para los usuarios. Esto ayuda a validar las licencias. 
3. Después de validan usuarios hello, haga clic en **guardar**.

## <a name="next-steps"></a>Pasos siguientes
Eso es todo, creó e implementó correctamente su colección en la nube de Azure RemoteApp. Hola siguiente paso es toohave a los usuarios descargar e instalación el cliente de escritorio remoto de Hola. Puede buscar dirección URL de hello para el cliente de hello en la página de inicio rápido de Azure RemoteApp de Hola. A continuación, tienen los usuarios inicien sesión en el cliente de Hola y acceder a las aplicaciones de hello publicó.

### <a name="help-us-help-you"></a>Permítanos ayudarle
¿Sabía que en suma toorating este artículo y realizar comentarios hacia abajo, a continuación, puede realizar cambios toohello artículo? ¿Falta algo? ¿Algo no es correcto? ¿Algo de lo que he escrito es simplemente confuso? Desplazarse hacia arriba y haga clic en **editar en GitHub** toomake cambios - los procederán toous para su revisión y, a continuación, una vez que se aprueban en ellos, podrá ver los cambios y mejoras aquí.

