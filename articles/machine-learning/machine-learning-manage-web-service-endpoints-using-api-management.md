---
title: "aaaLearn cómo utiliza la API de administración de servicios de toomanage web de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Una guía que muestra cómo utiliza la API de administración de servicios de toomanage web de aprendizaje automático de Azure."
keywords: "aprendizaje automático, administración de api"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a>Obtenga información acerca de cómo utiliza la API de administración de servicios de toomanage web de aprendizaje automático de Azure
## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooquickly Introducción al uso de administración de API toomanage los servicios web de aprendizaje automático de Azure.

## <a name="what-is-azure-api-management"></a>¿Qué es la Administración de API de Azure?
Administración de API de Azure es un servicio de Azure que le permite administrar los extremos de la API de REST al definir el acceso del usuario, el límite de uso y la supervisión de panel. Haga clic [aquí](https://azure.microsoft.com/services/api-management/) para obtener más información sobre Administración de API de Azure. Haga clic en [aquí](../api-management/api-management-get-started.md) para obtener una guía sobre cómo tooget comenzar con la administración de API de Azure. Esta otra guía, en la que está basada esta guía, aborda más temas, incluidos las configuraciones de notificación, el nivel de precios, el control de respuestas, la autenticación de los usuarios, la creación de productos, las suscripciones de desarrollador y los paneles de uso.

## <a name="what-is-azureml"></a>¿Qué es AzureML?
Aprendizaje automático de Azure es un servicio de Azure para el aprendizaje automático que permite la compilación tooeasily, implementar y compartir las soluciones de análisis avanzado. Haga clic en [aquí](https://azure.microsoft.com/services/machine-learning/) para obtener información detallada sobre AzureML.

## <a name="prerequisites"></a>Requisitos previos
toocomplete esta guía, debe:

* Una cuenta de Azure. Si no tienes una cuenta de Azure, haga clic en [aquí](https://azure.microsoft.com/pricing/free-trial/) para obtener más información acerca de cómo toocreate una cuenta de prueba gratuita.
* Una cuenta de AzureML. Si no tiene una cuenta de aprendizaje automático de Azure, haga clic en [aquí](https://studio.azureml.net/) para obtener más información acerca de cómo toocreate una cuenta de prueba gratuita.
* área de trabajo de Hello, el servicio y api_key para un experimento de aprendizaje automático de Azure que se implementa como un servicio web. Haga clic en [aquí](machine-learning-create-experiment.md) para obtener más información sobre cómo probar toocreate un aprendizaje automático de Azure. Haga clic en [aquí](machine-learning-publish-a-machine-learning-web-service.md) para obtener más información sobre cómo probar toodeploy un aprendizaje automático de Azure como un servicio web. Como alternativa, el apéndice A contiene instrucciones para toocreate y probar un aprendizaje automático de Azure simple experimentación e implementación como un servicio web.

## <a name="create-an-api-management-instance"></a>Creación de una instancia de Administración de API
A continuación se muestran los pasos de hello para el uso de administración de API toomanage el servicio web de aprendizaje automático de Azure. En primer lugar, cree una instancia del servicio. Inicie sesión en toohello [Portal clásico](https://manage.windowsazure.com/) y haga clic en **New** > **servicios de aplicaciones** > **administración de API**  >  **Crear**.

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

Especifique una **dirección URL**única. Esta guía se usan **demoazureml** – debe toochoose algo diferente. Elija Hola deseado **suscripción** y **región** para la instancia de servicio. Después de realizar las selecciones, haga clic en el botón siguiente Hola.

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

Especifique un valor para hello **nombreDeOrganización**. Esta guía se usan **demoazureml** – debe toochoose algo diferente. Escriba su dirección de correo electrónico en hello **correo electrónico del administrador** campo. Esta dirección de correo electrónico se usa para recibir notificaciones del sistema de administración de API de Hola.

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

Haga clic en hello casilla toocreate su instancia de servicio. *Ocupe toothirty minutos para una nueva toobe de servicio creado*.

## <a name="create-hello-api"></a>Crear API Hola
Una vez creada la instancia de servicio de hello, Hola siguiente paso es toocreate Hola API. Una API consta de un conjunto de operaciones que se pueden invocar desde una aplicación cliente. Las operaciones de API son servicios de tooexisting procesadas por el proxy web. Esta guía crea las API que toohello proxy AzureML RRS y BES servicios web existentes.

Las API se crean y configuran desde el portal para desarrolladores de API hello, que se obtiene acceso a través de hello Portal clásico de Azure. tooreach Hola seleccione portal, publicador de la instancia del servicio.

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

Haga clic en **administrar** Hola Portal clásico de Azure para el servicio de administración de API.

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

Haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **agregar API**.

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

Tipo de **API de demostración de aprendizaje automático de Azure** como hello **nombre de la API de Web**. Tipo de **https://ussouthcentral.services.azureml.net** como hello **dirección URL del servicio Web**. Tipo de **azureml-demo** como hello **sufijo de URL de la API de Web**. Comprobar **HTTPS** como hello **URL de la API de Web** esquema. Seleccione **Starter** en **Productos**. Cuando termine, haga clic en **guardar** toocreate Hola API.

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a>Las operaciones de Hola para agregar
Haga clic en **Agregar operación** tooadd operations toothis API.

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

Hola **nueva operación** ventana se mostrarán y Hola **firma** ficha se seleccionará de forma predeterminada.

## <a name="add-rrs-operation"></a>Adición de una operación de registro de recursos
Cree primero una operación de servicio de AzureML RRS Hola. Seleccione **POST** como hello **verbo HTTP**. Tipo de **/workspaces/ {área de} trabajo {servicio} / ejecutar? api-version = {valor apiversion} & detalles = {detalles}** como hello **plantilla de dirección URL**. Tipo de **ejecutar RR** como hello **nombre para mostrar**.

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

Haga clic en **respuestas** > **agregar** en hello izquierdo y seleccione **200 Aceptar**. Haga clic en **guardar** toosave esta operación.

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>Adición de operaciones BES
No se incluyen con fines capturas de pantalla Hola operaciones BES tal como están toothose muy similar para agregar la operación de Hola RR.

### <a name="submit-but-not-start-a-batch-execution-job"></a>Envío (pero no inicio) de un trabajo de ejecución por lotes
Haga clic en **Agregar operación** tooadd Hola BES de aprendizaje automático de Azure operación toohello API. Seleccione **POST** para hello **verbo HTTP**. Tipo de **/workspaces/ {área de} trabajo {servicio} / trabajos? api-version = {valor apiversion}** para hello **plantilla de dirección URL**. Tipo de **BES enviar** para hello **nombre para mostrar**. Haga clic en **respuestas** > **agregar** en hello izquierdo y seleccione **200 Aceptar**. Haga clic en **guardar** toosave esta operación.

### <a name="start-a-batch-execution-job"></a>Inicio de un trabajo de ejecución por lotes
Haga clic en **Agregar operación** tooadd Hola BES de aprendizaje automático de Azure operación toohello API. Seleccione **POST** para hello **verbo HTTP**. Tipo de **/workspaces/ {área de} trabajo {servicio} /jobs/ {jobid} / iniciar? api-version = {valor apiversion}** para hello **plantilla de dirección URL**. Tipo de **BES iniciar** para hello **nombre para mostrar**. Haga clic en **respuestas** > **agregar** en hello izquierdo y seleccione **200 Aceptar**. Haga clic en **guardar** toosave esta operación.

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a>Obtener estado de Hola o el resultado de un trabajo de ejecución por lotes
Haga clic en **Agregar operación** tooadd Hola BES de aprendizaje automático de Azure operación toohello API. Seleccione **obtener** para hello **verbo HTTP**. Tipo de **/workspaces/ {área de} trabajo {servicio} /jobs/ {jobid}? api-version = {valor apiversion}** para hello **plantilla de dirección URL**. Tipo de **estado BES** para hello **nombre para mostrar**. Haga clic en **respuestas** > **agregar** en hello izquierdo y seleccione **200 Aceptar**. Haga clic en **guardar** toosave esta operación.

### <a name="delete-a-batch-execution-job"></a>Eliminación de un trabajo de ejecución por lotes
Haga clic en **Agregar operación** tooadd Hola BES de aprendizaje automático de Azure operación toohello API. Seleccione **eliminar** para hello **verbo HTTP**. Tipo de **/workspaces/ {área de} trabajo {servicio} /jobs/ {jobid}? api-version = {valor apiversion}** para hello **plantilla de dirección URL**. Tipo de **BES eliminar** para hello **nombre para mostrar**. Haga clic en **respuestas** > **agregar** en hello izquierdo y seleccione **200 Aceptar**. Haga clic en **guardar** toosave esta operación.

## <a name="call-an-operation-from-hello-developer-portal"></a>Llamar a una operación de hello Portal para desarrolladores
Las operaciones pueden llamarse directamente desde el portal para desarrolladores de hello, que proporciona una manera cómoda de tooview y pruebe las operaciones de Hola de una API. En este paso de la guía llamará Hola **ejecutar RR** método que se agregó toohello **API de aprendizaje automático de Azure demostración**. Haga clic en **portal para desarrolladores de** desde el menú de Hola Hola parte superior derecha de hello Portal clásico.

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

Haga clic en **API** desde el menú superior de hello y, a continuación, haga clic en **API de demostración de aprendizaje automático de Azure** operaciones de hello toosee disponibles.

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

Seleccione **RR ejecutar** para la operación de Hola. Haga clic en **Pruébelo**.

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

Para los parámetros de solicitud, escriba su **área de trabajo**, **servicio**, **2.0** para hello **el elemento apiversion**, y **true**para hello **detalles**. Puede encontrar el **área de trabajo** y **servicio** en panel de servicio de web de aprendizaje automático de Azure de hello (vea **probar hello web servicio** en el apéndice A).

Para los encabezados de solicitud, haga clic en **Agregar encabezado** y escriba **Content-Type** y **application/json**, después haga clic en **Agregar encabezado** y escriba **Autorización** y **Portador <YOUR AZUREML SERVICE API-KEY>**. Puede encontrar el **clave de api** en panel de servicio de web de aprendizaje automático de Azure de hello (vea **probar hello web servicio** en el apéndice A).

Tipo de **{"Entradas": {"Entrada1": {"ColumnNames": "Valores" ["Col2"]: [["Esto es un buen día"]]}}, "GlobalParameters": {}}** Hola cuerpo de solicitud.

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

Haga clic en **Enviar**.

![Enviar](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

Después de invoca una operación, el portal para desarrolladores de hello muestra hello **dirección URL solicitada** de servicio de back-end de hello, Hola **estado de respuesta**, hello **encabezados de respuesta**, y cualquier **contenido de la respuesta**.

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>Apéndice A: Creación y prueba de un servicio web sencillo de AzureML
### <a name="creating-hello-experiment"></a>Crear experimento Hola
A continuación se muestran los pasos de Hola para crear un experimento de aprendizaje automático de Azure sencillo e implementar como un servicio web. Hola web servicio toma como entrada una columna de texto arbitrario y devuelve un conjunto de características representadas como enteros. Por ejemplo:

| Texto | Texto con hash |
| --- | --- |
| Este es un buen día |1 1 2 2 0 2 0 1 |

En primer lugar, mediante un explorador de su elección, navegue hasta: [https://studio.azureml.net/](https://studio.azureml.net/) y escriba su toolog de credenciales en. Después, cree un nuevo experimento en blanco.

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

Cambiar el nombre demasiado**SimpleFeatureHashingExperiment**. Expanda **Conjuntos de datos guardados** y arrastre **Reseñas de libros de Amazon** al experimento.

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

Expanda **Transformación de datos** y **Manipulación** y arrastre **Seleccionar columnas de conjunto de datos** al experimento. Conectar **reseñas de libros de Amazon** demasiado**seleccionar columnas de conjunto de datos**.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

Haga clic en **Seleccionar columnas de conjunto de datos** y después haga clic en **Iniciar el selector de columnas** y seleccione **Col2**. Haga clic en tooapply de marca de verificación de hello estos cambios.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

Expanda **análisis de texto** y arrastre **hash de características** en el experimento de Hola. Conectar **seleccionar columnas de conjunto de datos** demasiado**hash de características**.

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

Tipo de **3** para hello **hash de tamaño de bits**. Se crearán 8 (23) columnas.

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

En este momento, puede que desee tooclick **ejecutar** experimento de hello tootest.

![Ejecutar](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>Creación de un servicio web
Ahora va a crear un servicio web. Expanda **Servicio web** y arrastre **Entrada** al experimento. Conectar **entrada** demasiado**hash de características**. Arrastre también **Resultado** al experimento. Conectar **salida** demasiado**hash de características**.

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

Haga clic en **Publicar servicio web**.

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

Haga clic en **Sí** experimento de hello toopublish.

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a>Servicio web de Hola de prueba
Un servicio web de AzureML consta de los extremos RRS (servicio de solicitud/respuesta) y BES (servicio de ejecución por lotes). RRS sirve para la ejecución sincrónica. BES sirve para la ejecución por lotes asincrónica. tootest su sitio web de servicio con el origen de Python de ejemplo de Hola a continuación, quizás necesite toodownload y Hola instalar Azure SDK para Python (Véase: [cómo tooinstall Python](../python-how-to-install.md)).

También necesitará hello **área de trabajo**, **servicio**, y **api_key** de su experimento para el origen de ejemplo de Hola a continuación. Puede encontrar el área de trabajo de Hola y el servicio haciendo clic en **solicitud/respuesta** o **ejecución por lotes** para el experimento en el panel del servicio web Hola.

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

Puede encontrar Hola **api_key** haciendo clic en el experimento en el panel del servicio web Hola.

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>Prueba del extremo RRS
##### <a name="test-button"></a>Botón Probar
Un punto de conexión de manera sencilla tootest Hola RR es tooclick **prueba** en el panel del servicio web Hola.

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

Escriba **Este es un buen día** para **col2**. Haga clic en la marca de verificación de Hola.

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

Verá algo parecido a lo siguiente:

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>Código de ejemplo
Tootest de otra manera el RR es desde el código de cliente. Si hace clic en **solicitud/respuesta** en hello panel y desplácese toohello parte inferior, verá el código de ejemplo para C#, Python y R. También verá sintaxis Hola de Hola RR solicitud, incluidos los URI de solicitud de hello, encabezados y cuerpo.

Esta guía muestra un ejemplo de Python en funcionamiento. Deberá toomodify con hello **área de trabajo**, **servicio**, y **api_key** de su experimento.

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>Prueba de extremo BES
Haga clic en **ejecución por lotes** en hello panel y desplazamiento toohello inferior. Verá el código de ejemplo de C#, Python y R. También verá sintaxis Hola de Hola BES solicitudes toosubmit un trabajo, iniciar un trabajo, obtener el estado de Hola o los resultados de un trabajo y eliminar un trabajo.

Esta guía muestra un ejemplo de Python en funcionamiento. Necesita toomodify con hello **área de trabajo**, **servicio**, y **api_key** de su experimento. Además, es necesario hello toomodify **nombre de la cuenta de almacenamiento**, **clave de la cuenta de almacenamiento**, y **el nombre del contenedor de almacenamiento**. Por último, necesitará la ubicación de hello toomodify de hello **archivo de entrada** y la ubicación de Hola de hello **archivo de salida**.

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
