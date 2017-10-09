---
title: aaaCreate una cuenta de servicios multimedia de Azure con hello portal de Azure | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de creación de una cuenta de servicios multimedia de Azure con hello portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a>Crear una cuenta de servicios multimedia de Azure mediante Hola portal de Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Azure. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Hola portal de Azure proporciona una manera tooquickly crear una cuenta de servicios de multimedia de Azure (AMS). Puede usar los servicios de multimedia que permiten toostore, cifrar, codificar, administrar y transmitir por secuencias contenido multimedia en Azure tooaccess de cuenta. En el momento de hello crear una cuenta de servicios multimedia, también crear una cuenta de almacenamiento asociada (o use una existente) en hello misma región geográfica Hola cuenta de servicios multimedia.

En este artículo se explica algunos conceptos comunes y muestra cómo toocreate servicios multimedia de una cuenta con hello portal de Azure.

## <a name="concepts"></a>Conceptos
El acceso a Servicios multimedia requiere dos cuentas asociadas:

* Una cuenta de Media Services. El proporciona cuenta acceso tooa conjunto de servicios de multimedia en la nube que están disponibles en Azure. Una cuenta de Servicios multimedia no almacena el contenido multimedia real, sino En su lugar, almacena metadatos acerca de contenido multimedia de Hola y trabajos de procesamiento de medios en su cuenta. En el momento de hello que crear cuenta de hello, seleccione una región de servicios multimedia disponible. región de Hello que seleccionó es un centro de datos que almacena las entradas de metadatos de Hola para su cuenta.
  
* Una cuenta de almacenamiento de Azure. Las cuentas de almacenamiento deben encontrarse en hello misma región geográfica Hola cuenta de servicios multimedia. Cuando se crea una cuenta de servicios multimedia, puede elegir una cuenta de almacenamiento existente en hello misma región, o puede crear una nueva cuenta de almacenamiento en hello misma región. Si elimina una cuenta de servicios multimedia, no se eliminan los blobs de hello en su cuenta de almacenamiento de información relacionada.

> [!NOTE]
> Para obtener información acerca de la disponibilidad de las características de Azure Media Services en distintas regiones, consulte la sección [Availability of Media Services features across datacenters](scenarios-and-availability.md#availability) (Disponibilidad de las características de Media Services en los centros de datos).

## <a name="create-an-ams-account"></a>Creación de una cuenta de AMS
pasos de Hello en esta sección muestran cómo toocreate un AMS cuenta.

1. Inicie sesión en hello [portal de Azure](https://portal.azure.com/).
2. Haga clic en **+Nuevo** > **Web y móvil** > **Servicios multimedia**.
   
    ![Creación de Servicios multimedia](./media/media-services-create-account/media-services-new1.png)
3. En **CREAR CUENTA DE SERVICIOS MULTIMEDIA** especifique los valores obligatorios.
   
    ![Creación de Servicios multimedia](./media/media-services-create-account/media-services-new3.png)
   
   1. En **nombre de la cuenta**, escriba el nombre de Hola de nueva cuenta de AMS Hola. Un nombre de cuenta de servicios multimedia es todas las letras minúsculas o números sin espacios y es de 3 too24 caracteres de longitud.
   2. En la suscripción, seleccione entre las diferentes suscripciones de Azure Hola que tienen acceso a.
   3. En **grupo de recursos**, seleccione Hola recursos nuevos o existentes.  Un grupo de recursos es una colección de recursos que comparten ciclos de vida, permisos y directivas. Obtenga más información [aquí](../azure-resource-manager/resource-group-overview.md#resource-groups).
   4. En **ubicación**, seleccione Hola región geográfica que será los registros de medios y los metadatos de hello toostore usado para su cuenta de servicios multimedia. Esta región se tooprocess usado y transmitir los medios. Solo Hola servicios multimedia regiones disponibles aparecen en el cuadro de lista desplegable de Hola. 
   5. En **cuenta de almacenamiento**, seleccione un almacenamiento de blobs de tooprovide de cuenta de almacenamiento de contenido multimedia de Hola de su cuenta de servicios multimedia. Puede seleccionar una cuenta de almacenamiento existente en hello misma región geográfica como su cuenta de servicios multimedia, o puede crear una cuenta de almacenamiento. Se crea una nueva cuenta de almacenamiento en hello misma región. las reglas de Hello para la cuenta de almacenamiento son nombres Hola igual que para las cuentas de servicios multimedia.
      
       Puede obtener más información acerca del almacenamiento [aquí](../storage/common/storage-introduction.md).
   6. Seleccione **toodashboard Pin** progreso de hello toosee de implementación de la cuenta de hello.
4. Haga clic en **crear** final Hola del formulario de Hola.
   
    Una vez que se crea correctamente la cuenta de hello, carga la página información general. En hello streaming cuenta de hello de tabla de punto de conexión tendrá un valor predeterminado del origen de hello **detenido** estado. 

    >[!NOTE]
    >Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 
   
## <a name="toomanage-your-ams-account"></a>toomanage su cuenta AMS

toomanage su cuenta AMS (por ejemplo, conectar toohello AMS API mediante programación, cargar vídeos, codificar activos, configurar la protección de contenido, supervisar el progreso del trabajo) seleccione **configuración** en hello izquierda del portal de Hola. De hello **configuración**, navegue tooone de hojas disponibles hello (por ejemplo: **el acceso de API**, **activos**, **trabajos**, **Protección de contenido**).


## <a name="next-steps"></a>Pasos siguientes

Ya puede cargar archivos en su cuenta de AMS. Para más información, consulte [Upload files into a Media Services account using the Azure portal](media-services-portal-upload-files.md)(Carga de archivos en una cuenta de Servicios multimedia desde el Portal de Azure).

Si tiene previsto tooaccess AMS API mediante programación, vea [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

