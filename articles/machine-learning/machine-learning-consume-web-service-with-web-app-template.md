---
title: "un servicio web de aprendizaje automático con una plantilla de aplicación web aaaConsume | Documentos de Microsoft"
description: "Usar una plantilla de aplicación web en Azure Marketplace tooconsume un servicio web de predicción en aprendizaje automático de Azure."
keywords: "servicio web,operacionalización,API de REST,aprendizaje automático"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a>Consumo de un servicio web de Aprendizaje automático de Azure con una plantilla de aplicación web

Una vez haya desarrollado el modelo de predicción e implementarla como un servicio web de Azure con estudio de aprendizaje automático, o mediante herramientas como R o Python, puede tener acceso mediante una API de REST de modelo operaciones Hola.

Hay varias maneras de tooconsume Hola API de REST de servicio y acceso hello web. Por ejemplo, puede escribir una aplicación en C#, R, o código generado automáticamente cuando implementa el servicio web de Hola de ejemplo de Python con hello (disponible en hello [Portal de servicios Web de aprendizaje de máquina](https://services.azureml.net/quickstart) o en el panel de servicio web de hello en Estudio de aprendizaje automático). O bien puede usar el libro de Microsoft Excel de ejemplo de Hola creado para usted en hello mismo tiempo.

Pero Hola tooaccess de forma más rápida y más fácil su servicio web es a través de plantillas de aplicación de hello Web disponibles en hello [Marketplace de aplicaciones Web de Azure](https://azure.microsoft.com/marketplace/web-applications/all/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a>Hola plantillas de aplicaciones de Web de aprendizaje de máquina de Azure
plantillas de aplicación de Hello web disponibles en hello Azure Marketplace pueden compilar una aplicación web personalizada que conoce los datos de entrada de su servicio web y los resultados esperados. Todo lo que necesita toodo es proporcionar datos y servicio web de tooyour de acceso de aplicación de hello web y plantilla de Hola Hola rest.

Existen dos plantillas:

* [Plantilla de aplicación web Request-Response Service de Aprendizaje automático de Azure](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [Plantilla de aplicación web Batch Execution Service de Aprendizaje automático de Azure](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

Cada plantilla crea una aplicación de ASP.NET de ejemplo, mediante Hola URI de API y la clave para el servicio web e implementa como un tooAzure de sitio web. plantilla de servicio de solicitud-respuesta (RR) de Hello crea una aplicación web que le permite toosend una sola fila de datos toohello web servicio tooget un único resultado. plantilla de servicio de ejecución de lotes (BES) de Hello crea una aplicación web que le permite toosend muchas filas de datos tooget varios resultados.

Ninguna codificación es necesario toouse estas plantillas. Basta con proporcionar Hola clave de API y el URI y plantilla Hola compila la aplicación hello automáticamente.

clave de API de hello tooget y URI de la solicitud para un servicio web:

1. Hola [Portal de servicios Web](https://services.azureml.net/quickstart), para un nuevo servicio web, haga clic en **servicios Web** en la parte superior de Hola. O bien, para un servicio web clásico, haga clic en **Servicios web clásicos**.
2. Haga clic en el servicio de web de Hola que desee tooaccess.
3. Para un servicio web clásico, haga clic en punto de conexión de hello desea tooaccess.
4. Haga clic en **Consume** en la parte superior de Hola.
5. Hola copia **principal** o **clave secundaria** y guárdelo.
6. Si está creando una plantilla de servicio de solicitud-respuesta (RR), copie hello **solicitud-respuesta** URI y guárdelo. Si está creando una plantilla de servicio de ejecución de lotes (BES), copie hello **solicitudes por lotes** URI y guárdelo.


## <a name="how-toouse-hello-request-response-service-rrs-template"></a>¿Cómo toouse Hola plantilla de servicio de solicitud-respuesta (RR)
Siga estos plantilla pasos toouse Hola RR web app, como se muestra en hello siguiente diagrama.

![Plantilla de proceso toouse RR web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. Vaya toohello [portal de Azure](https://portal.azure.com), **inicio de sesión**, haga clic en **New**, busque y seleccione **Azure ML solicitudes y respuestas Web del servicio de aplicaciones**, a continuación, haga clic en **Crear**. 
   
   * Asigne un nombre único a la aplicación web. dirección URL de Hola de aplicación web de hello será este nombre seguido de `.azurewebsites.net.` por ejemplo,`http://carprediction.azurewebsites.net.`
   * Seleccione Hola suscripción de Azure y servicios en la que se ejecuta el servicio web.
   * Haga clic en **Crear**.
     
     ![Crear una aplicación web][image5]

4. Cuando Azure ha terminado de implementar la aplicación web de hello, haga clic en hello **URL** Hola página de configuración de aplicación web en Azure, o escriba la dirección URL de hello en un explorador web. Por ejemplo: `http://carprediction.azurewebsites.net.`
5. Cuando Hola aplicación de web primero se ejecuta le pedirá hello **URL de entrada de la API** y **clave de API**.
   Escriba los valores de hello guardó anteriormente (**URI de solicitud** y **clave de API**, respectivamente).
     
     Haga clic en **Enviar**.
     
     ![Escriba el URI del mensaje y la clave de API][image6]

6. Hola de aplicación web se muestra su **configuración de la aplicación Web** página con la configuración del servicio web actual Hola. Aquí puede realizar cambios toohello configuración de aplicación web de hello.
   
   > [!NOTE]
   > Estas opciones de hello solo si se cambia su para esta aplicación web. Configuración predeterminada de Hola de su servicio web no cambia. Por ejemplo, si cambia hello **descripción** aquí no cambia la descripción de Hola se muestra en el panel de servicio web de hello en estudio de aprendizaje automático.
   > 
   > 
   
    Cuando haya terminado, haga clic en **guardar cambios**y, a continuación, haga clic en **vaya tooHome página**.

7. De hello página principal que puede escribir valores de servicio web de toosend tooyour. Haga clic en **enviar** cuando haya terminado, y se devolverá el resultado de hello.

Si desea que tooreturn toohello **configuración** página, vaya toohello `setting.aspx` página de aplicación web de hello. Por ejemplo: `http://carprediction.azurewebsites.net/setting.aspx.` podrá volver a clave de API de hello tooenter solicitadas: necesita que tooaccess Hola página y actualizar la configuración de Hola.

Puede detener, reiniciar o eliminar la aplicación web de Hola Hola portal de Azure como cualquier otra aplicación web. Mientras se está ejecutando puede buscar direcciones web principal de toohello y escribir nuevos valores.

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a>¿Cómo toouse Hola plantilla de servicio de ejecución de lotes (BES)
Puede usar hello BES plantilla de aplicación web en hello mismo excepto forma como plantilla de Hola RR, dicha aplicación Hola que se crea, podrá toosubmit varias filas de datos y recibir varios resultados.

los valores de entrada de Hola para un servicio web de ejecución de lotes pueden proceder de almacenamiento de Azure o un archivo local; Hola resultados se almacenan en un contenedor de almacenamiento de Azure.
Por lo tanto, será necesario un toohold del contenedor de almacenamiento de Azure Hola resultados devueltos por la aplicación web de hello, y deberá tooget los datos de entrada listo.

![Procesar toouse BES plantilla web][image2]

1. Seguimiento Hola mismo Hola de toocreate procedimiento BES web app para la plantilla de RR hello, excepto go demasiado[plantilla de aplicación Web de Azure ML lote ejecución servicio](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Hola plantilla BES en Azure Marketplace y haga clic en **crear aplicación Web** .

2. toospecify donde desea que los resultados de hello almacenados, escriba la información del contenedor de destino de Hola en la página de inicio de aplicación web de Hola. Especificar donde la aplicación web de hello puede obtener valores de entrada de hello, en un archivo local o en un contenedor de almacenamiento de Azure.
   Haga clic en **Enviar**.
   
    ![Información de almacenamiento][image7]

aplicación web de Hello mostrará una página con el estado del trabajo.
Cuando se haya completado el trabajo de Hola se le ofrecerán ubicación Hola de resultados de hello en el almacenamiento de blobs de Azure. También tiene opción de Hola de descarga de archivos local de hello resultados tooa.

## <a name="for-more-information"></a>Para obtener más información
más información acerca de toolearn...

* la creación de un experimento de aprendizaje automático con Estudio de aprendizaje automático, consulte [Creación del primer experimento en Estudio de aprendizaje automático de Azure](machine-learning-create-experiment.md)
* toodeploy experimentar el aprendizaje automático como un servicio web, vea [implementar un servicio web de aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md)
* otras maneras tooaccess el servicio web, vea [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md)

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
