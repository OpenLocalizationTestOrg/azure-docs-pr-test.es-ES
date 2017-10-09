---
title: aaaIntegrate una cuenta de almacenamiento de Azure con red CDN de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse contenido de hello red de entrega de contenido (CDN) de Azure toodeliver gran ancho de banda almacenando en memoria caché los blobs del almacenamiento de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a>Integración de una cuenta de una instancia de Azure Storage con la red CDN de Azure
CDN puede ser habilitado toocache contenido desde el almacenamiento de Azure. Ofrece a los desarrolladores una solución global para entregar contenido con alto ancho de banda almacenando en memoria caché los blobs y el contenido estático de instancias de proceso en nodos físicos emplazados en Estados Unidos de hello, Europa, Asia, Australia y Sudamérica.

## <a name="step-1-create-a-storage-account"></a>Paso 1: Creación de una cuenta de almacenamiento
Usar hello siguiendo el procedimiento toocreate una nueva cuenta de almacenamiento para una suscripción de Azure. Una cuenta de almacenamiento proporciona acceso a los servicios de almacenamiento de Azure. cuenta de almacenamiento de Hello representa el nivel más alto de hello del espacio de nombres de hello para tener acceso a cada uno de los componentes del servicio de almacenamiento de Azure de hello: servicios, servicios de cola y tabla servicios de blobs. Para obtener más información, consulte toohello [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md).

toocreate una cuenta de almacenamiento, debe ser administrador de servicios de Hola o Coadministrador de hello asociado suscripción.

> [!NOTE]
> Hay varios métodos que puede usar una cuenta de almacenamiento, incluidos Hola Portal de Azure y Powershell toocreate.  Para este tutorial, usaremos Hola Portal de Azure.  
> 
> 

**toocreate una cuenta de almacenamiento para una suscripción de Azure**

1. Inicie sesión en toohello [Portal de Azure](https://portal.azure.com).
2. En hello esquina superior izquierda, seleccione **nuevo**. Hola **New** cuadro de diálogo, seleccione **datos + almacenamiento**, a continuación, haga clic en **cuenta de almacenamiento**.
    
    Hola **crear cuenta de almacenamiento** aparece hoja.   

    ![Crear cuenta de almacenamiento][create-new-storage-account]  

3. Hola **nombre** , escriba un nombre de subdominio. Esta entrada puede contener de 3 a 24 letras minúsculas y números.
   
    Este valor se convierte en el nombre de host de hello en hello URI que se utiliza para redirigir recursos de Blob, cola o tabla para la suscripción de Hola. Para resolver un recurso de contenedor en hello servicio Blob, usaría un URI en hello siguiendo el formato, donde  *&lt;StorageAccountLabel&gt;*  se refiere toohello un valor que escribió en **escriba una dirección URL**:
   
    http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*
   
    **Importante:** Hola subdominio de dirección URL etiqueta forms Hola de cuenta de almacenamiento de hello URI y debe ser único entre todos los servicios hospedados en Azure.
   
    Este valor también se utiliza como nombre de Hola de esta cuenta de almacenamiento en el portal de hello, o al tener acceso mediante programación a esta cuenta.
4. Deje los valores predeterminados de Hola para **modelo de implementación**, **cuenta kind**, **rendimiento**, y **replicación**. 
5. Seleccione hello **suscripción** que se utilizará la cuenta de almacenamiento de hello con.
6. Seleccione o cree un **grupo de recursos**.  Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Seleccione la ubicación para la cuenta de almacenamiento.
8. Haga clic en **Crear**. proceso de Hola de creación de cuenta de almacenamiento de hello puede tardar varios toocomplete minutos.

## <a name="step-2-enable-cdn-for-hello-storage-account"></a>Paso 2: Habilitar la red CDN Hola cuenta de almacenamiento

Con la integración más reciente de hello, ahora puede habilitar CDN para la cuenta de almacenamiento sin salir de la extensión de portal de almacenamiento. 

1. Seleccione la cuenta de almacenamiento de hello, buscar "red CDN" o desplácese hacia abajo del menú de navegación izquierdo de hello, haga clic en "CDN de Azure".
    
    Hola **CDN de Azure** aparece hoja.

    ![cdn enable navigation][cdn-enable-navigation]
    
2. Crear un nuevo extremo especificando información Hola necesario
    - **Perfil de CDN**: puede crear un perfil o usar uno existente.
    - **Nivel de precios**: solo necesita tooselect un precio de nivel si crea un nuevo perfil CDN.
    - **Nombre del punto de conexión de CDN**: escriba un nombre de punto de conexión de su elección.

    > [!TIP]
    > extremo de red CDN Hola creado utiliza Hola nombre de host de la cuenta de almacenamiento como origen de forma predeterminada.

    ![cdn new endpoint creation][cdn-new-endpoint-creation]

3. Después de su creación, nuevo punto de conexión de Hola se mostrará en la lista de extremos de hello anterior.

    ![cdn storage new endpoint][cdn-storage-new-endpoint]

> [!NOTE]
> También puede ir tooAzure CDN extensión tooenable CDN. [Tutorial](#Tutorial-cdn-create-profile).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a>Paso 3: Habilitación de características adicionales de CDN

En la hoja de "Red CDN de Azure" de la cuenta de almacenamiento, haga clic en extremo de red CDN Hola de hoja de configuración de red CDN de hello lista tooopen. Puede habilitar características adicionales de CDN para la entrega como, por ejemplo, la compresión, la cadena de consulta o el filtrado geográfico. También puede agregar el extremo de red CDN de tooyour de asignación de dominio personalizado y habilitar HTTPS de dominio personalizado.
    
![cdn storage cdn configuration][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a>Paso 4: Acceso a su contenido de la red CDN
tooaccess almacenado en caché contenido en la red CDN Hola, use Hola dirección URL de CDN proporcionado en el portal de Hola. dirección de Hola para un blob almacenado en caché será similar siguiente toohello:

http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\>

> [!NOTE]
> Una vez que habilite la cuenta de almacenamiento de tooa de acceso de red CDN, todos los objetos disponibles públicamente son aptos para su almacenamiento en caché de perimetral de red CDN. Si modifica un objeto que está almacenado actualmente en la red CDN Hola, contenido nuevo de hello no estará disponible a través de la red CDN Hola hasta que la red CDN Hola actualiza su contenido cuando expire el período de tiempo de vida de Hola almacenado en memoria caché contenido.
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a>Paso 5: Quitar contenido de CDN Hola
Si ya no desea toocache un objeto en hello red de entrega de contenido (CDN) de Azure, puede realizar una de hello pasos:

* Puede hacer Hola privados de contenedor en lugar de público. Vea [administrar toocontainers de acceso de lectura anónimo y los blobs](../storage/blobs/storage-manage-access-to-resources.md) para obtener más información.
* Puede deshabilitar o eliminar el extremo de red CDN Hola mediante Hola Portal de administración.
* Puede modificar su toorequests servicio hospedado responden más de toono para el objeto de Hola.

Un objeto que ya está almacenado en la red CDN Hola permanecerá en caché hasta que expire el período de período de vida de hello para el objeto de Hola o hasta que el punto de conexión de Hola se purga. Cuando expire el período de tiempo de vida de hello, CDN Hola comprobará toosee si el extremo de red CDN Hola sigue siendo válido y el objeto de hello todavía accesible de forma anónima. Si no es así, a continuación, objeto de Hola se ya no se almacenarán en caché.

## <a name="additional-resources"></a>Recursos adicionales
* [¿Cómo tooMap CDN contenido tooa dominio personalizado](cdn-map-content-to-custom-domain.md)
* [Habilitar HTTPS para el dominio personalizado](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
