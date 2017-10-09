---
title: archivos de aaaUpload en una cuenta de servicios multimedia de Azure con Aspera | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de carga de archivos en una cuenta de almacenamiento que está asociada con una cuenta de servicios multimedia mediante Hola ** Aspera Server en petición ** el servicio en Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a>Cargar archivos en una cuenta de servicios multimedia mediante Hola servicio Aspera Server On Demand en Azure

## <a name="overview"></a>Información general

**Aspera** es un software de transferencia de archivos de alta velocidad. **Aspera Server On Demand** para Azure permite la carga y descarga a alta velocidad de archivos de gran tamaño directamente en Azure Blob Storage. Para obtener información acerca de **Aspera On Demand**, vea hello [Aspera nube](http://cloud.asperasoft.com/) sitio. 
  
**Aspera Server On Demand** de Azure está disponible para su compra de hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/). En Ordenar toocomplete una compra de **Aspera Server On Demand** de Azure, inicie sesión en Azure Marketplace con su Windows Live ID.

Este tutorial le guiará por los pasos de Hola de carga de archivos en una cuenta de almacenamiento que está asociada con una cuenta de servicios multimedia mediante hello **Aspera Server On Demand** servicio en Azure. 

Puede encontrar un ejemplo que muestra cómo las funciones de Azure toouse a Aspera y servicios multimedia [aquí](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).

>[!NOTE]
>Hay un límite toohello tamaño máximo admitido para el procesamiento con servicios multimedia de Azure procesadores multimedia (MP). Vea [esto](media-services-quotas-and-limitations.md) tema para obtener más información acerca de la limitación de tamaño de archivo de Hola.
>

## <a name="prerequisites"></a>Requisitos previos 

toocomplete este tutorial, necesita:

* Un Windows Live ID
* Una [cuenta de Azure](https://azure.microsoft.com). Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Una [cuenta de Azure Media Services](media-services-portal-create-account.md).

## <a name="purchase-aspera-on-demand-for-azure"></a>Compra de Aspera On Demand para Azure

Una vez que han iniciado sesión en Azure Marketplace, siga estos pasos básicos toocomplete la compra de Aspera On Demand para Azure.

1. Busque Aspera y seleccione "Server On Demand".

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. Revise los planes de suscripción de Hola y haga clic en "Inicio de sesión de seguridad"

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. Rellene los detalles de hello para el servidor en la suscripción a petición.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. Haga clic en hello **tarifa** y seleccione el volumen mensual deseado en el panel de sub Hola. Hola **planear detalles** el panel, seleccione **Aceptar**. A continuación, en hello **elija el nivel de precios** del panel, haga clic en **seleccione**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. Haga clic en **condiciones legales** tooview y acepte los términos legales de hello en el panel de sub Hola. Una vez que haya revisado condiciones legales de hello, haga clic en **compra**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. Complete la compra de hello haciendo clic en **crear**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. Hola panel Azure anunciará que está aprovisionando servicio Hola.  Una vez que se completó con el aprovisionamiento, puede encontrar nueva suscripción de hello mediante la búsqueda en los recursos de nombre de hello del servicio de Hola. Una vez haya encontrado el servicio de hello, haga doble clic en él portal de administración de servicios de toolaunch Hola.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. Inicie el portal de administración de Aspera Hola. Una vez haya encontrado el nuevo servicio de Aspera, puede obtener el portal de administración de acceso toohello, haciendo clic en el servicio de Hola.  Se abrirá un nuevo panel. Desde dentro de dicho panel nuevo, deberá tooclick en hello **nombre de recurso** de su nuevo servicio.  En la siguiente captura de pantalla de hello, nombre de recurso de hello es 'AsperaTransferDemo'. Cuando hace clic en el nombre del recurso de hello, se inicia otro panel. En ese panel recién abierto, verá un vínculo "Manage" (Administrar). Haga clic en hello portal de administración de "Administrar" vínculo toolaunch hello Aspera.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. Haciendo clic en hello vínculo Administrar, aparecerá la página de registro de toohello, que es necesario tooaccess Hola servicio.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. En este punto, debe tener acceso toohello Aspera service portal de administración, donde puede crear teclas de acceso, descargar licencias y los clientes de Aspera, ver el uso y obtener información acerca de las API de Hola.

    Hello captura de pantalla siguiente muestra hello acceso creación. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    Hello captura de pantalla siguiente muestra uso Hola reporting interfaces en el portal de Hola. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>Carga de archivos con Aspera

1. Descargue e instale el software de cliente de Hola Aspera:
    
    * [Complemento del explorador](http://downloads.asperasoft.com/connect2/)
    * [Cliente enriquecido](http://downloads.asperasoft.com/en/downloads/2)

2. Realice su primera transferencia. En orden toouse hello Aspera cliente tootransfer con hello Aspera el servicio de transferencia, necesita toocomplete Hola siguiente: 

    1. Cree una clave de acceso, mediante el portal de Aspera Hola.  
    2. Descarga, instalación y cliente de licencia hello Aspera (software puede encontrarse en el portal de hello Aspera).  

    >[!NOTE]
    >Sírvase leer esta guía de cliente hello Aspera para obtener información de configuración.
    
    3. Recuperar información de la cuenta de almacenamiento que está asociada a la cuenta de multimedia de Azure con hello [portal de Azure](https://portal.azure.com/). En concreto, del nombre y la clave y el nombre del contenedor de blob de almacenamiento de hello en toowhich desea tooplace su contenido. 

        * información de almacenamiento de hello tooget desde el portal de hello: buscar la cuenta de almacenamiento, haga clic en las teclas de acceso de Hola y clave de hello y nombre de Hola de copia de la cuenta.
        * nombre del contenedor de hello tooget: buscar la cuenta de almacenamiento, seleccione **Blobs**, seleccione nombre de hello del contenedor de hello desea tooupload Hola contenido en. 

    A continuación se muestra hello captura de pantalla de cliente de hello Aspera **Connection Manager** donde debe especificar el tipo de almacenamiento 'Azure' hello y credenciales, así como contenedor de blobs de Hola.

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>Recursos

Hola recursos siguientes se menciona en este artículo. 

* [Complemento del explorador de Connect](http://downloads.asperasoft.com/connect2/)
* [Guía de Connect](http://downloads.asperasoft.com/en/documentation/8)
* [Cliente Aspera](http://downloads.asperasoft.com/en/downloads/2)
* [Guía de cliente](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a>Pasos siguientes

Ahora puede [copiar blobs de una cuenta de almacenamiento a una cuenta de AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

