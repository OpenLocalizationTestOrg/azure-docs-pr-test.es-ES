---
title: "aaaAccess conjuntos de datos con la biblioteca de cliente de Python de aprendizaje automático | Documentos de Microsoft"
description: "Instalar y usar hello tooaccess de biblioteca de cliente de Python y administrar datos de aprendizaje automático de Azure de forma segura un entorno local de Python."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a>Conjuntos de datos de Access con Python utilizando la biblioteca de cliente de Python de aprendizaje automático de Azure Hola
vista previa de Hola de biblioteca de cliente de Python de aprendizaje automático de Microsoft Azure puede habilitar un acceso seguro tooyour conjuntos de datos de aprendizaje automático de Azure desde un entorno local de Python y permite la creación de hello y administración de conjuntos de datos en un área de trabajo.

Este tema proporciona instrucciones sobre cómo realizar las siguientes acciones:

* instalar biblioteca de cliente de Python de aprendizaje automático de Hola 
* obtener acceso y cargar conjuntos de datos, incluidas las instrucciones sobre cómo tooget autorización tooaccess conjuntos de datos de aprendizaje automático de Azure de su entorno local de Python
* obtener acceso a los conjuntos de datos intermedios de experimentos;
* usar conjuntos de datos de hello Python cliente biblioteca tooenumerate, tener acceso a metadatos, lectura Hola del contenido de un conjunto de datos, crear nuevos conjuntos de datos y actualizar conjuntos de datos existentes

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a>Requisitos previos
biblioteca de cliente de Python Hola se ha probado en hello siguientes entornos:

* Windows, Mac y Linux
* Python 2.7, 3.3 y 3.4

Tiene una dependencia en hello siguientes paquetes:

* Solicitudes
* Python-dateutil
* Pandas

Se recomienda utilizar una distribución de Python como [Anaconda](http://continuum.io/downloads#all) o [Canopy](https://store.enthought.com/downloads/), que vienen con Python, IPython e instalar los paquetes de saludo tres mencionados anteriormente. Aunque IPython no es estrictamente necesario, es un excelente entorno para manipular y visualizar datos de forma interactiva.

### <a name="installation"></a>¿Cómo tooinstall Hola biblioteca de cliente de Python de aprendizaje automático de Azure
biblioteca de cliente de Python de aprendizaje automático de Azure de Hello también debe estar instalado toocomplete tareas de hello descritas en este tema. Está disponible de hello [índice del paquete Python](https://pypi.python.org/pypi/azureml). tooinstall en su entorno de Python, ejecute Hola siguiente comando desde el entorno de Python local:

    pip install azureml

Como alternativa, puede descargar e instalar desde orígenes de hello en [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).

    python setup.py install

Si tiene instalado en su equipo de git, puede usar pip tooinstall directamente desde el repositorio de git de hello:

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a>Usar conjuntos de datos de tooaccess de fragmentos de código de Studio
biblioteca de cliente de Python Hola proporciona conjuntos de datos existentes de acceso mediante programación tooyour de experimentos que se han ejecutado.

Desde la interfaz web de hello Studio, puede generar fragmentos de código que incluyen todos los toodownload de la información necesaria de Hola y deserializar los conjuntos de datos como objetos de trama de datos de Pandas en su equipo de ubicación.

### <a name="security"></a>Seguridad de acceso a datos
Hola Studio proporcionados para usarlo con la biblioteca de cliente de Python de hello incluye el identificador de área de trabajo y la autorización de fragmentos de código de token. Estos proporcionan el área de trabajo de acceso completo tooyour y deben estar protegidos, como una contraseña.

Por motivos de seguridad, funcionalidad de fragmento de código de hello solo está disponible toousers que tienen su rol establecer como **propietario** para el área de trabajo de Hola. El rol se muestra en el estudio de aprendizaje automático de Azure en hello **usuarios** página en **configuración**.

![Seguridad][security]

Si su rol no está establecido como **propietario**, puede solicitar toobe Invitado como un propietario o pida Hola propietario de hello tooprovide de área de trabajo, con el fragmento de código de hello.

token de autorización de hello tooobtain, puede hacer uno de hello siguientes:

* Solicite un token a un propietario. Los propietarios pueden acceder a sus tokens de autorización de la página de configuración de Hola de su área de trabajo de Studio. Seleccione **configuración** de hello dejado panel y haga clic en **TOKENS de autorización** toosee Hola tokens principales y secundarios.  Aunque Hola principal o tokens de autorización secundaria de hello pueden utilizarse en el fragmento de código de hello, se recomienda que los propietarios solo compartan tokens de autorización secundaria de Hola.

![Tokens de autorización](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* Pida toorole toobe promocionada del propietario.  toodo esto, un propietario actual del toofirst de necesidades del área de trabajo de hello quitarle de su área de trabajo de hello, a continuación, vuelva a invitar a tooit como propietario.

Una vez que han obtenido los desarrolladores de Id. de área de trabajo de Hola y autorización token, son tooaccess capaz de área de trabajo de hello mediante el fragmento de código de hello, independientemente de su rol.

Tokens de autorización se administran en hello **TOKENS de autorización** página en **configuración**. Puede volver a generar ellos, pero este procedimiento revoca el token de acceso toohello anterior.

### <a name="accessingDatasets"></a>Obtener acceso a los conjuntos de datos desde una aplicación local de Python
1. En estudio de aprendizaje automático, haga clic en **conjuntos de datos** en barra de navegación de Hola Hola izquierda.
2. Seleccione el conjunto de datos de hello le gustaría tooaccess. Puede seleccionar cualquiera de los conjuntos de datos de Hola de hello **Mis conjuntos de datos** lista o de hello **ejemplos** lista.
3. En la barra de herramientas de hello inferior, haga clic en **generar código de acceso a datos**. Si los datos de hello en un formato incompatible con la biblioteca de cliente de Python hello, este botón está deshabilitado.
   
    ![CONJUNTOS DE DATOS][datasets]
4. Seleccione el fragmento de código de hello en ventana hello que aparece y se copia tooyour Portapapeles.
   
    ![Código de acceso][dataset-access-code]
5. Pegue el código de hello en Bloc de notas de saludo de la aplicación local de Python.
   
    ![Bloc de notas][ipython-dataset]

## <a name="accessingIntermediateDatasets"></a>Obtener acceso a los conjuntos de datos intermedios de experimentos de Aprendizaje automático
Después de ejecuta un experimento en hello estudio de aprendizaje automático, es posible tooaccess Hola intermedio los conjuntos de datos de nodos de salida de hello de módulos. Los conjuntos de datos intermedios son datos que se han creado y utilizado para pasos intermedios cuando se ha ejecutado una herramienta de modelo.

Pueden tener acceso a conjuntos de datos intermedio como formato de datos de hello es compatible con la biblioteca de cliente de Python Hola.

Hola se admiten los formatos siguientes (constantes para estos están en hello `azureml.DataTypeIds` clase):

* PlainText
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

Puede determinar el formato de hello desplazando el puntero sobre un nodo de salida del módulo. Se muestra junto con el nombre de nodo de hello, información sobre herramientas.

Algunos de los módulos de hello, como hello [división] [ split] módulo, formato de salida tooa denominado `Dataset`, que no es compatible con la biblioteca de cliente de Python Hola.

![Formato de conjunto de datos][dataset-format]

Necesita toouse un módulo de conversión, como [convertir tooCSV][convert-to-csv], tooget una salida a un formato compatible.

![Formato GenericCSV][csv-format]

Hello pasos siguientes muestran un ejemplo que crea un experimento, lo ejecuta y tiene acceso a conjunto de datos intermedio Hola.

1. Cree un experimento nuevo.
2. Inserte un módulo **Conjunto de datos de clasificación binaria de ingresos en el censo de adultos** .
3. Insertar un [división] [ split] módulo y conecte la salida del módulo de conjunto de datos de entrada toohello.
4. Insertar un [convertir tooCSV] [ convert-to-csv] módulo y conectar su entrada tooone de hello [división] [ split] módulo genera.
5. Guardar experimento hello, ejecútelo y esperar a que toofinish ejecutando.
6. Haga clic en el nodo de salida de hello en hello [convertir tooCSV] [ convert-to-csv] módulo.
7. Cuando aparezca el menú contextual de hello, seleccione **generar código de acceso a datos**.
   
    ![Menú contextual][experiment]
8. Seleccione el fragmento de código de hello y cópielo tooyour Portapapeles desde la ventana de Hola que aparece.
   
    ![Código de acceso][intermediate-dataset-access-code]
9. Pegue el código de hello en el Bloc de notas.
   
    ![Bloc de notas][ipython-intermediate-dataset]
10. Puede visualizar datos Hola con matplotlib. Esto se muestra en un histograma para la columna de edad de hello:
    
    ![Histograma][ipython-histogram]

## <a name="clientApis"></a>Usar tooaccess de biblioteca de cliente de Python de aprendizaje automático de hello, leer, crear y administrar conjuntos de datos
### <a name="workspace"></a>Área de trabajo
área de trabajo de Hello es el punto de entrada de hello para la biblioteca de cliente de Python Hola. Proporcionar hello `Workspace` una instancia de clase con la toocreate de token de identificador y la autorización de área de trabajo:

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a>Enumerar los conjuntos de datos
tooenumerate todos los conjuntos de datos en un área de trabajo determinado:

    for ds in ws.datasets:
        print(ds.name)

tooenumerate Hola simplemente creados por el usuario los conjuntos de datos:

    for ds in ws.user_datasets:
        print(ds.name)

conjuntos de datos de ejemplo de Hola simplemente tooenumerate:

    for ds in ws.example_datasets:
        print(ds.name)

Puede tener acceso a un conjunto de datos por nombre (que distingue mayúsculas de minúsculas):

    ds = ws.datasets['my dataset name']

O bien, puede tener acceso a él por su índice:

    ds = ws.datasets[0]


### <a name="metadata"></a>Metadatos
Conjuntos de datos tienen metadatos, en toocontent de adición. (Los conjuntos de datos intermedios son una regla de excepción de toothis y no tiene ningún metadato.)

Algunos valores de metadatos son asignados por el usuario de hello en tiempo de creación:

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

Los demás son valores asignados por el Aprendizaje automático de Azure:

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

Vea hello `SourceDataset` clase para más de metadatos Hola disponibles.

### <a name="read-contents"></a>Leer contenido
fragmentos de código de Hello proporcionados por estudio de aprendizaje automático automáticamente descargarán y deserializar el objeto de hello dataset tooa Pandas trama de datos. Esto se hace con hello `to_dataframe` método:

    frame = ds.to_dataframe()

Si prefiere datos sin procesar de toodownload hello y realizar la deserialización de hello usted mismo, es una opción. En el momento de hello, esto es Hola única opción de formatos, como 'ARFF', no se puede deserializar la biblioteca de cliente de Python que Hola.

contenido de hello tooread como texto:

    text_data = ds.read_as_text()

contenido de hello tooread como binario:

    binary_data = ds.read_as_binary()

También puede abrir un contenido de toohello la secuencia:

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a>Crear un conjunto de datos nuevo
biblioteca de cliente de Python de Hello permite tooupload conjuntos de datos desde el programa de Python. Estos conjuntos de datos estarán disponibles para utilizarse en el área de trabajo.

Si tiene datos en una trama de datos de Pandas, use Hola siguiente código:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Si sus datos ya están serializados, puede utilizar:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

biblioteca de cliente de Python Hello es capaz de tooserialize da formato a una trama de datos de Pandas toohello a continuación (constantes para estos están en hello `azureml.DataTypeIds` clase):

* PlainText
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

### <a name="update-an-existing-dataset"></a>Actualizar un registro existente
Si intentas tooupload un nuevo conjunto de datos con un nombre que coincida con un conjunto de datos existente, debe obtener un error de conflicto.

tooupdate un conjunto de datos existente, primero debe tooget un conjunto de datos de referencia toohello existente:

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

A continuación, utilice `update_from_dataframe` tooserialize y reemplazar contenido Hola del conjunto de datos de hello en Azure:

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Si desea que el formato diferente del tooa tooserialize Hola datos, especifique un valor para hello opcional `data_type_id` parámetro.

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Opcionalmente, puede establecer una nueva descripción especificando un valor para hello `description` parámetro.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

Opcionalmente, puede establecer un nuevo nombre especificando un valor para hello `name` parámetro. De ahora en adelante, recuperará Hola conjunto de datos con nombre nuevo de Hola. Hola siguiente código actualiza la descripción, nombre y los datos de Hola.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

Hola `data_type_id`, `name` y `description` parámetros son opcionales y el valor anterior de tootheir predeterminado. Hola `dataframe` parámetro siempre es necesario.

Si sus datos ya están serializados, puede utilizar`update_from_raw_data` en lugar de `update_from_dataframe`. Funcionará de una forma similar si pasa `raw_data` en lugar de `dataframe`.

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

