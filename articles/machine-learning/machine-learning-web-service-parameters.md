---
title: "aaaUse parámetros de servicio de Web de aprendizaje de máquina de Azure | Documentos de Microsoft"
description: "¿Cómo toouse parámetros de servicio Web de Azure Machine Learning toomodify Hola comportamiento del modelo cuando se accede al servicio web de Hola."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a>Usar parámetros de servicio web de Aprendizaje automático de Azure
Se crea un servicio web de Aprendizaje automático de Azure mediante la publicación de un experimento que contiene módulos con parámetros configurables. En algunos casos, puede que desee el comportamiento del módulo de toochange Hola mientras se ejecuta el servicio web de Hola. *Parámetros de servicio Web* le permiten toodo esta tarea. 

Un ejemplo común es la configuración hello [importar datos] [ reader] módulo para ese usuario Hola de hello servicio web publicado puede especificar un origen de datos diferente cuando se accede al servicio web de Hola. O configurar hello [exportar datos] [ writer] módulo para que se puede especificar un destino diferente. Algunos otros ejemplos incluyen el cambio de número de Hola de bits para hello [hash de características] [ feature-hashing] módulo o hello número de características deseadas para hello [selección de características basada en filtros] [ filter-based-feature-selection] módulo. 

Puede definir parámetros de servicio web y asociarlos con uno o más parámetros de módulo en el experimento, y puede especificar si son obligatorios u opcionales. usuario de Hello del servicio web de hello, a continuación, puede proporcionar valores para estos parámetros cuando llama al servicio web de Hola. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a>¿Cómo tooset y usar parámetros de servicio Web
Para definir un parámetro del servicio Web, al hacer clic en el parámetro toohello hello icono siguiente para un módulo y seleccionando "Establecer como parámetro del servicio web". Esto crea un nuevo parámetro del servicio Web y conecta el parámetro module de toothat. A continuación, cuando se accede al servicio web de hello, usuario Hola puede especificar un valor para el parámetro del servicio Web de Hola y es toohello aplicado módulo parámetro.

Una vez que defina un parámetro del servicio Web, está disponible tooany otro parámetro de módulo en el experimento de Hola. Si define un parámetro del servicio Web asociado a un parámetro para un módulo, puede usar ese mismo parámetro de servicio Web para cualquier otro módulo, como parámetro hello espera Hola al mismo tipo de valor. Por ejemplo, si el parámetro del servicio Web de hello es un valor numérico, a continuación, solo se puede utilizar para los parámetros del módulo que espera un valor numérico. Cuando el usuario Hola establece un valor de parámetro del servicio Web de hello, será parámetros del módulo tooall aplicados asociado.

Puede decidir si valor tooprovide un valor predeterminado para hello parámetro del servicio Web. Si, a continuación,, Hola parámetro es opcional para el usuario de hello del servicio web de Hola. Si no proporciona un valor predeterminado, el usuario de hello es tooenter requiere un valor cuando se accede al servicio web de Hola.

documentación de API de servicio web de Hola Hola incluye información de usuario del servicio web hello en cómo toospecify Hola parámetro del servicio Web mediante programación al tener acceso a servicios web de Hola.

> [!NOTE]
> Hola documentación de la API para un servicio web clásico se proporciona a través de hello **página de Ayuda de API** vínculo en el servicio web de hello **panel** en estudio de aprendizaje automático. Hola documentación de la API para un nuevo servicio web se proporciona a través de hello [servicios Web de Azure Machine Learning](https://services.azureml.net/Quickstart) portal en hello **Consume** y **Swagger API** páginas para su servicio Web.
> 
> 

## <a name="example"></a>Ejemplo
Por ejemplo, supongamos que tenemos un experimento con un [exportar datos] [ writer] módulo que envía el almacenamiento de blobs de tooAzure de información. Se definirá un parámetro del servicio Web denominado "Ruta de acceso de Blob" que permite hello web usuario toochange Hola ruta de acceso toohello blob del almacenamiento del servicio cuando se tiene acceso al servicio de Hola.

1. En estudio de aprendizaje automático, haga clic en hello [exportar datos] [ writer] tooselect de módulo se. Sus propiedades se muestran en toohello de panel de propiedades de hello derecha del lienzo del experimento de Hola.
2. Especifique el tipo de almacenamiento de hello:
   
   * En **Especifique el destino de los datos**, seleccione Almacenamiento de blobs de Azure.
   * En **Especifique el tipo de autenticación**, seleccione "Cuenta".
   * Especifique la información de cuenta de hello para hello almacenamiento de blobs de Azure. 
     <p />
3.Haga clic en hello icono toohello derecha de hello **ruta tooblob comienza con el parámetro container**. Su aspecto es similar a este:
   
   ![Icono de parámetro del servicio web][icon]
   
   Seleccione "Establecer como parámetro del servicio web".
   
   Se agrega una entrada en **parámetros de servicio Web** final Hola del panel de propiedades de hello con hello nombre "ruta de acceso tooblob empezando con el contenedor". Esto es hello parámetro del servicio Web que ya está asociado a este [exportar datos] [ writer] parámetro module.
4. toorename Hola parámetro del servicio Web, haga clic en el nombre de hello, escriba "Ruta de acceso de Blob" y presione hello **ENTRAR** clave. 
5. tooprovide un valor predeterminado para hello parámetro del servicio Web, haga clic en hello icono toohello derecha del nombre de hello, seleccione "Proporcionar el valor predeterminado", escriba un valor (por ejemplo, "container1/output1.csv") y presione hello **ENTRAR** clave.
   
   ![Parámetro del servicio web][parameter]
6. Haga clic en **Ejecutar**. 
7. Haga clic en **implementar el servicio de Web** y seleccione **implementar servicio Web [estándar]** o **implementar [New] servicio Web** servicio web de toodeploy Hola.

> [!NOTE] 
> toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola. Para obtener más información, vea [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

usuario de Hello del servicio web de hello ahora puede especificar un nuevo destino para hello [exportar datos] [ writer] módulo al obtener acceso a servicios web de Hola.

## <a name="more-information"></a>Más información
Para obtener un ejemplo más detallado, vea hello [parámetros de servicio Web](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entrada Hola [Blog de aprendizaje automático](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).

Para obtener más información sobre cómo acceder a un servicio web de aprendizaje automático, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

