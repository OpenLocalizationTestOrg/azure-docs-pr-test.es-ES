---
title: "aaaHow toocreate una colección híbrida de RemoteApp de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una implementación de RemoteApp que se conecta la red interna tooyour."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 08ea0ce3-3a2c-4ddf-9394-6d75c8030cb1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fba29acc676e0af48e995da406f889c532c44c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-hybrid-collection-for-azure-remoteapp"></a>¿Cómo toocreate una colección híbrida de RemoteApp de Azure
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Hay dos tipos de colecciones de Azure RemoteApp:

* Nube: reside completamente en Azure. Puede elegir toosave todos los datos en la nube de hello (para una colección de solo nube) o tooconnect su red virtual de colección tooa y guardar datos en él.   
* Híbrido: incluye una red virtual para acceso local: Esto requiere usar Hola de Azure AD y un entorno de Active Directory local.

¿No sabe qué necesita? Revise [¿Qué tipo de colección necesita para Azure RemoteApp?](remoteapp-collections.md)

Este tutorial le guía a través del proceso de Hola de creación de una colección híbrida. Existen ocho pasos:

1. Decidir qué [imagen](remoteapp-imageoptions.md) toouse de la colección. Puede crear una imagen personalizada o usar uno de imágenes de Microsoft de hello incluidas con su suscripción.
2. Configurar la red virtual. Extraer del repositorio hello [planeación de la red virtual](remoteapp-planvnet.md) y [sizing](remoteapp-vnetsizing.md) información.
3. Crear una colección.
4. Unir el dominio local de tooyour de colección.
5. Agregar una colección de tooyour de imagen de plantilla.
6. Configurar la sincronización de directorios. RemoteApp de Azure requiere que integran con Azure Active Directory por cualquier 1) Configurar sincronización Azure Active Directory con la opción de sincronización de contraseñas de Hola o (2) Configurar sincronización Azure Active Directory sin opción de sincronización de contraseñas de hello pero usa un dominio que sea tooAD federada FS. Extraer del repositorio hello [información de configuración de Active Directory con RemoteApp](remoteapp-ad.md).
7. Publicar aplicaciones de RemoteApp.
8. Configurar el acceso del usuario.

**Antes de empezar**

Necesita toodo Hola siguiente antes de crear la colección de hello:

* [Suscribirse](https://azure.microsoft.com/services/remoteapp/) a Azure RemoteApp.
* Crear una cuenta de usuario en Active Directory toouse como Hola cuenta de servicio de Azure RemoteApp. Restrinja los permisos de Hola para esta cuenta para que sólo puede unirse a dominio de toohello máquinas.
* Recopile información sobre la red local: dirección IP de información y detalles de dispositivos VPN.
* Instalar hello [Azure PowerShell](/powershell/azure/overview) módulo.
* Recopilar información acerca de los usuarios de Hola que desee tener acceso toogrant a. Se necesita Hola nombre principal de usuario de Azure Active Directory (por ejemplo, name@contoso.com) para cada usuario. Asegúrese de que ese Hola UPN coincida entre Azure AD y Active Directory.
* Elija su imagen de plantilla. Una imagen de plantilla de RemoteApp de Azure contiene Hola aplicaciones y programas que desea toopublish para los usuarios. Consulte [Opciones de imagen de Azure RemoteApp](remoteapp-imageoptions.md) para obtener más información.
* Imagen de Office 365 ProPlus de hello toouse ¿desea? Consulte la información [aquí](remoteapp-officesubscription.md).
* [Configuración de Active Directory para RemoteApp de Azure](remoteapp-ad.md)

## <a name="step-1-set-up-your-virtual-network"></a>Paso 1: Configuración de la red virtual
Puede implementar una colección híbrida que use una red virtual de Azure existente, o bien puede crear una nueva red virtual. Una red virtual permite a los usuarios acceder a los datos de la red local a través de recursos remotos de RemoteApp. Usar una red virtual de Azure proporciona su tooother de acceso de red directa de colección servicios de Azure y máquinas virtuales implementadas toothat de red virtual.

Asegúrese de revisar hello [planeación de la red virtual](remoteapp-planvnet.md) y [tamaño de la red virtual](remoteapp-vnetsizing.md) información antes de crear la red virtual.

### <a name="create-an-azure-vnet-and-join-it-tooyour-active-directory-deployment"></a>Crear una red virtual de Azure y unirla tooyour implementación de Active Directory
Empiece por crear una [red virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Esto se hace en hello **red** ficha Hola portal de Azure. Deberá tooconnect la implementación de Active Directory que es el inquilino de Azure Active Directory sincronizados tooyour toohello de red virtual.

Vea [crear una red virtual con el portal de Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) para obtener más información.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Asegúrese de que la red virtual está lista para Azure RemoteApp
Antes de crear la colección, debemos asegurarnos de que la nueva red virtual está lista. Puede comprobarlo haciendo Hola siguiente:

1. Crear una máquina virtual dentro de hello subred de red virtual de Hola que acaba de crear para RemoteApp.
2. Use la máquina virtual de escritorio remoto tooconnect toohello. (Haga clic en **Conectar**).
3. Unir toohello misma implementación de Active Directory que quiere toouse de RemoteApp.

¿Funcionó este procedimiento? Entonces la red virtual y la subred están preparadas para Azure RemoteApp.

Puede encontrar más información sobre cómo crear máquinas virtuales de Azure y conectar toothem con Escritorio remoto [aquí](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>Paso 2: Crear una colección de Azure RemoteApp
1. Hola [portal de Azure](http://manage.windowsazure.com), vaya toohello página de RemoteApp de Azure.
2. Haga clic en **Nuevo > Crear con VNET**.
3. Escriba un nombre para la colección.
4. Elija plan Hola que desea toouse - estándar o básica.
5. Elija la red virtual de hello desplegable lista y, a continuación, en la subred.
6. Elija toojoin se tooyour dominio.
7. Haga clic en **Crear colección de RemoteApp**.

Una vez creada la colección RemoteApp de Azure, haga doble clic en el nombre de Hola de colección de Hola. Se abrirá hello **inicio rápido** (página): Esto es donde termine de configurar la recopilación de Hola.

¿Algo salió mal? Extraer del repositorio hello [colección híbrida información sobre la solución](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-toohello-local-domain"></a>Paso 3: Vincular el dominio local de toohello de colección
1. En hello **inicio rápido** página, haga clic en **unirse a un dominio local**.
2. Agregar hello Azure RemoteApp servicio cuenta tooyour local dominio de Active Directory. Necesitará el nombre del dominio de hello, unidad organizativa, nombre de usuario de cuenta de servicio y la contraseña.
   
    Se trata de información de Hola que recopiló si ha seguido los pasos de hello en [configurar Active Directory de Azure RemoteApp](remoteapp-ad.md).

## <a name="step-4-link-tooan-azure-remoteapp-image"></a>Paso 4: Imagen vínculo tooan Azure RemoteApp
Una imagen de plantilla de RemoteApp de Azure contiene programas de Hola que desee tooshare con los usuarios. Puede crear un nuevo [imagen de plantilla](remoteapp-imageoptions.md) o imagen existente de vínculo tooan (uno importado o cargado tooAzure RemoteApp). También puede vincular tooone de hello Azure RemoteApp [imágenes de plantilla](remoteapp-images.md) que incluyen Office 365 o programas de Office 2013 (en modo de prueba).

Si va a cargar la nueva imagen de hello, necesita tooenter Hola nombre y elegir ubicación de hello para la imagen de Hola. En hello siguiente página del Asistente de hello, verá un conjunto de cmdlets de PowerShell: copiar y ejecutar estos cmdlets desde una imagen especificada de Windows PowerShell tooupload prompt Hola con privilegios elevados.

Si está vinculando tooan imagen de plantilla existente, simplemente especificar nombre de la imagen de hello, la ubicación y la suscripción de Azure asociada.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>Paso 5: Configuración de la sincronización de directorios de Active Directory
RemoteApp de Azure requiere que integran con Azure Active Directory por cualquier 1) Configurar sincronización Azure Active Directory con la opción de sincronización de contraseñas de Hola o (2) Configurar sincronización Azure Active Directory sin opción de sincronización de contraseñas de hello pero usa un dominio que sea tooAD federada FS.

Consulte [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) : este artículo le ayuda a configurar la integración de directorios en cuatro pasos.

Consulte [Guía de sincronización de directorios](http://msdn.microsoft.com//library/azure/hh967642.aspx) para obtener información sobre planeación y pasos detallados.

## <a name="step-6-publish-apps"></a>Paso 6: Publicar aplicaciones
Una aplicación de Azure RemoteApp es aplicación hello o programa que proporcionan a los usuarios de tooyour. Se encuentra en la imagen de plantilla de Hola que cargó para la colección de Hola. Cuando un usuario tiene acceso a una aplicación, aparece toorun en su entorno local, pero realmente se ejecuta en Azure.

Antes de que los usuarios pueden tener acceso a aplicaciones, necesita toopublish les: Esto permite que las aplicaciones de Hola de acceso de los usuarios a través del cliente de escritorio remoto de Hola.

Puede publicar la colección de tooyour de varias aplicaciones. En la página de publicación de hello, haga clic en **publicar** tooadd una aplicación. Puede publicar de hello **iniciar** menú de imagen de plantilla de Hola o mediante la especificación de ruta de acceso de hello en imagen de plantilla de hello para la aplicación hello. Si elige tooadd de hello **iniciar** menú, elija tooadd de programa Hola. Si elige tooprovide Hola ruta de acceso toohello aplicación, proporcione un nombre para la aplicación hello y hello toowhere de ruta de acceso que está instalado en la imagen de la plantilla de Hola.

## <a name="step-7-configure-user-access"></a>Paso 7: Configuración del acceso de usuarios
Ahora que ha creado la colección, debe tooadd los usuarios de Hola que desea toobe puede toouse los recursos remotos. los usuarios de Hola que proporcione acceso tooneed tooexist en el inquilino de Active Directory de hello asociados con suscripción de hello usan toocreate esta colección de RemoteApp de Azure.

1. En la página de inicio rápido de hello, haga clic en **configurar el acceso de usuario**.
2. Escriba Hola cuenta profesional (Active Directory) o la cuenta de Microsoft que desee tener acceso toogrant para.
   
   **Notas:**
   
   Asegúrese de que usa hello  *user@domain.com*  formato.
   
   Si utilizas Office 365 ProPlus en la colección, debe usar las identidades de Active Directory de Hola para los usuarios. Esto ayuda a validar las licencias.
3. Una vez que se validan los usuarios de hello, haga clic en **guardar**.

## <a name="next-steps"></a>Pasos siguientes
Eso es todo, creó e implementó correctamente su colección híbrida de Azure RemoteApp. Hola siguiente paso es toohave a los usuarios descargar e instalación el cliente de escritorio remoto de Hola. Puede buscar dirección URL de hello para el cliente de hello en la página de inicio rápido de Azure RemoteApp de Hola. A continuación, tienen los usuarios inicien sesión en el cliente de Hola y acceder a las aplicaciones de hello publicó.

### <a name="help-us-help-you"></a>Permítanos ayudarle
¿Sabía que en suma toorating este artículo y realizar comentarios hacia abajo, a continuación, puede realizar cambios toohello artículo? ¿Falta algo? ¿Algo no es correcto? ¿Algo de lo que he escrito es simplemente confuso? Desplazarse hacia arriba y haga clic en **editar en GitHub** toomake cambios - los procederán toous para su revisión y, a continuación, una vez que se aprueban en ellos, podrá ver los cambios y mejoras aquí.

