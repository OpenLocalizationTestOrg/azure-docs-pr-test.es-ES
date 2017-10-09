---
title: "un servicio web de aprendizaje automático de aaaDeploy | Documentos de Microsoft"
description: "Cómo tooconvert entrenamiento experimentar tooa predictivo experimento, preparar para la implementación, a continuación, implementarlo como un servicio web de aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a>Implementar un servicio web de Aprendizaje automático de Azure
Aprendizaje automático de Azure le permite toobuild, probar e implementar soluciones de análisis predictivas.

Desde una perspectiva general, esto se realiza en tres pasos:

* **[Crear un experimento de entrenamiento]**  -estudio de aprendizaje automático de Azure es un entorno de desarrollo visual de colaboración que use tootrain y pruebe un análisis predictivos de modelo utilizando los datos de entrenamiento que suministre.
* **[Convertir experimento predictivo tooa]**  : una vez que el modelo se ha entrenado con datos existentes y está listo toouse se tooscore nuevos datos, preparar y simplificar el experimento para las predicciones.
* **[Implementarlo como un servicio web]**: puede implementar el experimento predictivo como un servicio web de Azure [nuevo] o [clásico]. Los usuarios pueden enviar tooyour modelo de datos y predicciones de su modelo de recepción.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a>Crear un experimento de entrenamiento
tootrain un modelo de análisis predictivos, usas toocreate un experimento de entrenamiento donde incluir datos de entrenamiento de diversos módulos tooload, preparar los datos de hello según sea necesario, aplicar algoritmos de aprendizaje automático y evaluar los resultados de Hola de estudio de aprendizaje automático de Azure . Puede iterar en un experimento y probar diferentes toocompare algoritmos de aprendizaje de automático y evaluar los resultados de Hola.

se explica el proceso de Hola de crear y administrar los experimentos de aprendizaje más exhaustivamente en otro lugar. Para obtener más información, consulte estos artículos:

* [Creación de un experimento sencillo en el Estudio de aprendizaje automático de Azure](machine-learning-create-experiment.md)
* [Desarrollo de una solución predictiva con Aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)
* [Importar datos de entrenamiento en Estudio de aprendizaje automático de Azure](machine-learning-data-science-import-data.md)
* [Administrar iteraciones de experimentos en Estudio de aprendizaje automático de Azure](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Convertir el experimento de predicción de hello entrenamiento experimento tooa
Cuando haya entrenar el modelo, ya está listo tooconvert experimentar el entrenamiento en un experimento predictivo tooscore nuevos datos.

Mediante la conversión tooa predictivo experimentar, va a recibir el toobe listo entrenado implementado como un servicio web puntuación. Los usuarios del servicio web de hello pueden enviar datos de entrada tooyour modelo y su modelo enviará resultados de predicción de hello back. Cuando convierta tooa predictivo experimentar, tenga en cuenta cómo espera que su toobe modelo utilizado por otros usuarios.

tooconvert su tooa de experimento de entrenamiento predictivo experimentar, haga clic en **ejecutar** en hello parte inferior del lienzo del experimento de hello, haga clic en **configurar el servicio de Web**, a continuación, seleccione **predictivo servicio Web** .

![Convertir tooscoring experimento](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

Para obtener más información acerca de cómo tooperform esta conversión, consulte [cómo tooprepare el modelo para la implementación en estudio de aprendizaje automático de Azure](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Hello pasos siguientes describen la implementación de un experimento de predicción como un nuevo servicio web. También puede implementar Hola experimento como servicio web de clásico.

## <a name="deploy-it-as-a-web-service"></a>Implementación como un servicio web

Puede implementar experimento predictivo Hola como un servicio web nuevo o como un servicio de web estándar.

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a>Implementar experimento predictivo Hola como un servicio web nuevo
Ahora que se ha preparado el experimento de predicción de hello, puede implementarlo como un nuevo servicio web de Azure. Con el servicio web de hello, los usuarios pueden enviar tooyour modelo de datos y modelo de hello devolverá las predicciones.

toodeploy experimentar, haga clic en la predicción **ejecutar** final Hola de hello experimentar el lienzo. Una vez que el experimento de hello ha terminado de ejecutarse, haga clic en **implementar el servicio de Web** y seleccione **implementar el servicio de Web [New]**.  se abre la página de implementación de Hello del portal de servicio Web de aprendizaje de máquina de Hola.

> [!NOTE] 
> toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola. Para obtener más información, vea [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a>Página de implementación de experimentos del portal Servicios web Machine Learning
En página de experimento implementar hello, escriba un nombre para el servicio web de Hola.
Seleccione un plan de tarifa. En caso contrario, si tiene un plan de precios existente que seleccione la plantilla, debe crear un nuevo plan de precios para el servicio de Hola.

1. Hola **Plan de precios** de lista desplegable, seleccione un plan existente o hello **seleccione Nuevo plan** opción.
2. En **el nombre del Plan**, escriba un nombre que identificará el plan de hello en la factura.
3. Seleccione uno de hello **mensual niveles planear**. plan de Hello niveles predeterminados toohello planes para la región predeterminada y el servicio web está implementado toothat región.

Haga clic en **implementar** hello y **inicio rápido** se abre la página para el servicio web.

página de inicio rápido del servicio de Hello web proporciona acceso e instrucciones sobre las tareas más comunes de hello que llevará a cabo después de crear un servicio web. Desde aquí, se pueden acceder fácilmente a las páginas de prueba de Hola y usar.

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a>Prueba del servicios web nuevo
tootest su nuevo servicio web, haga clic en **probar el servicio web** en tareas comunes. En la página de prueba de hello, puede probar el servicio web como un servicio de solicitud-respuesta (RR) o un servicio de ejecución por lotes (BES).

página de prueba de Hola RR muestra hello entradas, salidas y los parámetros globales que haya definido para el experimento de Hola. servicio web de tootest hello, puede escribir manualmente los valores adecuados para entradas de Hola o suministre un archivo con formato de separados por comas (CSV) de valor que contiene valores de prueba de Hola.

tootest con registros de recursos, de modo de vista de lista de hello, escriba los valores adecuados para las entradas de Hola y haga clic en **prueba solicitud-respuesta**. Mostrar los resultados de predicción en toohello de columna de salida de hello izquierda.

![Implementar el servicio web de Hola](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

tootest BES, haga clic en ejecutar **por lotes**. En la página de prueba de Hola por lotes, haga clic en Examinar en la entrada y seleccione un archivo CSV que contiene los valores de ejemplo adecuado. Si no tiene un archivo CSV y creado el experimento de predicción usando estudio de aprendizaje automático, puede descargar el conjunto de datos de hello para el experimento de predicción y utilizarlo.

conjunto de datos de hello toodownload, abra estudio de aprendizaje automático. Abra el experimento de predicción y haga clic en la entrada de hello para el experimento. En el menú contextual de hello, seleccione **conjunto de datos** y, a continuación, seleccione **descargar**.

![Implementar el servicio web de Hola](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

Haga clic en **Probar**. estado de Hello de la tarea de ejecución por lotes muestra toohello justo debajo **trabajos por lotes de prueba**.

![Implementar el servicio web de Hola](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

En hello **configuración** página, Hola descripción del cambio, título, actualizar la clave de cuenta de almacenamiento de Hola y habilitar los datos de ejemplo para el servicio web.

![Configurar el servicio web de Hola](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

Una vez haya implementado el servicio web de hello, hacer lo siguiente:

* **Acceso** a través de la API del servicio web Hola.
* **Administrar** a través de aprendizaje automático de Azure portal de servicios web u Hola portal de Azure clásico.
* **Actualizarlo** si cambia el modelo

#### <a name="access-your-new-web-service"></a>Acceso al servicio web nuevo
Una vez que implementa el servicio web desde estudio de aprendizaje automático, puede enviar datos toohello servicio y recibir respuestas mediante programación.

Hola **Consume** página proporciona toda la información de hello necesita tooaccess el servicio web. Por ejemplo, clave Hola API se proporciona el servicio de toohello de tooallow autorizado acceso.

Para obtener más información acerca del acceso a un servicio web de aprendizaje automático, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).

#### <a name="manage-your-new-web-service"></a>Administración del servicio web nuevo
Puede administrar los nuevos servicios web mediante el portal de servicios web Machine Learning. De hello [página principal del portal](https://services.azureml-test.net/), haga clic en **servicios Web**. Desde la página de servicios web de hello, puede eliminar o copiar un servicio. toomonitor un servicio específico, haga clic en el servicio de hello y, a continuación, haga clic en **panel**. Haga clic en trabajos por lotes de toomonitor asociados con el servicio web de hello, **el registro de solicitudes por lotes**.

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a>Implementar experimento predictivo hello como servicio web clásico

Ahora que se ha preparado suficientemente experimento predictivo hello, puede implementarlo como un servicio web de Azure clásico. Con el servicio web de hello, los usuarios pueden enviar tooyour modelo de datos y modelo de hello devolverá las predicciones.

toodeploy experimentar, haga clic en la predicción **ejecutar** final Hola de hello experimentar el lienzo y, a continuación, haga clic en **implementar servicio Web**. Hola web servicio está configurado y se colocan en el panel del servicio web Hola.

![Implementar el servicio web de Hola](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a>Prueba del servicio web clásico

Puede probar el servicio web de hello en el portal de servicios Web de aprendizaje de máquina de Hola o estudio de aprendizaje automático.

Hola tootest servicio de respuesta de solicitud web, haga clic en hello **prueba** botón en el panel del servicio web Hola. Un cuadro de diálogo aparece tooask, de los datos de entrada de hello para el servicio de Hola. Se trata de columnas de hello esperadas por hello experimento de puntuación. Escriba un conjunto de datos y haga clic en **Aceptar**. resultados de Hello generados por el servicio web de Hola se muestran en parte inferior de Hola de panel de Hola.

Puede hacer clic en hello **prueba** vista previa de vínculo tootest su servicio en el portal de servicios Web de Azure Machine Learning Hola tal y como se mostró anteriormente en hello nueva sección de servicio web.

Hola tootest servicio de ejecución por lotes, haga clic en **prueba** vista previa de vínculo. En la página de prueba de Hola por lotes, haga clic en Examinar en la entrada y seleccione un archivo CSV que contiene los valores de ejemplo adecuado. Si no tiene un archivo CSV y creado el experimento de predicción usando estudio de aprendizaje automático, puede descargar el conjunto de datos de hello para el experimento de predicción y utilizarlo.

![Servicio web de Hola de prueba](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

En hello **configuración** página, puede cambiar el nombre para mostrar del servicio de Hola Hola y escriba una descripción. Hola nombre y la descripción se muestra en hello [portal de Azure clásico](http://manage.windowsazure.com/) donde se administran los servicios web.

Puede dar una descripción para los datos de entrada, los de salida y los parámetros del servicio web escribiendo una cadena para cada columna en **INPUT SCHEMA** (ESQUEMA DE ENTRADA), **OUTPUT SCHEMA** (ESQUEMA DE SALIDA) y **WEB SERVICE PARAMETER** (PARÁMETRO DE SERVICIO WEB). Estas descripciones se utilizan en la documentación de código de ejemplo de Hola proporcionada para el servicio web de Hola.

Puede habilitar el registro toodiagnose los errores que está viendo cuando se accede a su servicio web. Para más información, vea [Habilitar el registro para los servicios web de Aprendizaje automático](machine-learning-web-services-logging.md).

![Configurar el servicio web de Hola](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

También puede configurar extremos de hello para el servicio web de hello en hello Azure Machine Learning Web Services portal toohello procedimiento similar se mostró anteriormente en hello nueva sección de servicio web. Opciones de Hello son diferentes, puede agregar o cambiar la descripción del servicio de hello, habilite el registro y habilitar datos de ejemplo para las pruebas.

#### <a name="access-your-classic-web-service"></a>Acceso al servicio web clásico
Una vez que implementa el servicio web desde estudio de aprendizaje automático, puede enviar datos toohello servicio y recibir respuestas mediante programación.

panel de Hello proporciona toda la información de hello necesita tooaccess el servicio web. Por ejemplo, la clave de API de hello es siempre tooallow autorizados acceso toohello servicio y las páginas de Ayuda de API se proporcionan toohelp empezar a escribir el código.

Para obtener más información acerca del acceso a un servicio web de aprendizaje automático, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).

#### <a name="manage-your-classic-web-service"></a>Administración del servicio web clásico
Hay varias acciones que puede realizar toomonitor un servicio web. Puede actualizarlo y eliminarlo. También puede agregar servicio web de extremos adicionales tooa clásico en el extremo de suma toohello predeterminado que se crea al implementarla.

Para obtener más información, consulte [administrar un área de trabajo de aprendizaje automático de Azure](machine-learning-manage-workspace.md) y [administrar un servicio web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a>Actualizar el servicio web de Hola
Puede realizar cambios tooyour servicio de web, como actualizar modelo Hola con datos de entrenamiento adicional y vuelva a implementar sobrescribiendo el servicio web original de Hola.

servicio web de tooupdate hello, abra el experimento de predicción original hello usa el servicio web de toodeploy hello y realice una copia modificable haciendo clic en **SAVE AS**. Realice los cambios y haga clic en **Publicar servicio web**.

Dado que haya implementado este experimento antes, se le preguntará si desea toooverwrite (servicio Web clásico) o servicio existente de Hola de actualización (nuevo servicio web). Haga clic en **Sí** o **actualización** detiene el servicio web existente de hello e implementa experimento de predicción nueva Hola se implementa en su lugar.

> [!NOTE]
> Si ha realizado cambios en la configuración de servicio web original de hello, por ejemplo, escribir un nuevo nombre para mostrar o la descripción, debe tooenter esos valores de nuevo.
> 
> 

Una opción para actualizar el servicio web es el modelo de hello tooretrain mediante programación. Para obtener más información, consulte [Volver a entrenar modelos de aprendizaje automático mediante programación](machine-learning-retrain-models-programmatically.md).

<!-- internal links -->
[Crear un experimento de entrenamiento]: #create-a-training-experiment
[Convertir experimento predictivo tooa]: #convert-the-training-experiment-to-a-predictive-experiment
[Implementarlo como un servicio web]: #deploy-it-as-a-web-service
[nuevo]: #deploy-the-predictive-experiment-as-a-new-Web-service
[clásico]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
