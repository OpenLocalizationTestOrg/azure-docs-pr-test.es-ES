---
title: "Servicio Web de aprendizaje de máquina del aaaConnect tooa | Documentos de Microsoft"
description: "Con C# o Python, conectar tooan servicio Web de aprendizaje de máquina de Azure con una clave de autorización."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a>Conectar el servicio Web de Azure Machine Learning tooan
Hola experiencia del desarrollador de aprendizaje automático de Azure es un predicciones de toomake de API de servicio Web de datos de entrada en tiempo real o en modo por lotes. Utilice las predicciones de toocreate de estudio de aprendizaje automático de Azure e implementar un servicio Web de aprendizaje de máquina de Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

toolearn acerca de cómo toocreate e implementar un servicio Web de aprendizaje de máquina mediante el estudio de aprendizaje automático:

* Para obtener un tutorial sobre cómo toocreate un experimento en estudio de aprendizaje automático, consulte [crear su primer experimento](machine-learning-create-experiment.md).
* Para obtener más información acerca de cómo toodeploy un servicio Web, consulte [implementar un servicio Web de aprendizaje de máquina](machine-learning-publish-a-machine-learning-web-service.md).
* Para obtener más información acerca de aprendizaje automático, por lo general, visite hello [centro de documentación de aprendizaje de máquina](https://azure.microsoft.com/documentation/services/machine-learning/).

## <a name="azure-machine-learning-web-service"></a>Servicio web Azure Machine Learning
Con hello servicio Web de aprendizaje de máquina de Azure, una aplicación externa se comunica con un modelo de puntuación de flujo de trabajo de aprendizaje automático en tiempo real. Una llamada de servicio Web de aprendizaje de máquina devuelve resultados de predicción tooan de aplicación externa. toomake una llamada de servicio Web de aprendizaje de máquina, se pasa una clave de API que se crea al implementar una predicción. Hola servicio Web de aprendizaje de máquina está basado en REST, una opción de arquitectura populares para proyectos de programación web.

Aprendizaje automático de Azure tiene dos tipos de servicios:

* Servicio de respuesta de solicitud (RR): una latencia baja, el servicio altamente escalable que ofrece una interfaz toohello sin estado modelos creado e implementado de hello estudio de aprendizaje automático.
* Servicio de ejecución por lotes (BES): servicio asincrónico que puntúa un lote de registros de datos.

Para más información sobre los servicios web Machine Learning, consulte [Implementación de un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Obtener una clave de autorización de Aprendizaje automático de Azure
Cuando se implementa el experimento, se generan claves de API para hello servicio Web. Puede recuperar las claves de Hola desde varias ubicaciones.

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a>Desde el portal de servicios Web de Microsoft Azure Machine Learning Hola
Inicie sesión en toohello [servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net) portal.

clave de API hello tooretrieve para un servicio Web de aprendizaje de máquina nueva:

1. En el portal de servicios Web de Azure Machine Learning hello, haga clic en **servicios Web** menú superior Hola.
2. Haga clic en el servicio Web de hello para el que desea que clave de hello tooretrieve.
3. En el menú superior de hello, haga clic en **usar**.
4. Copie y guarde hello **Primary Key**.

clave de API de hello tooretrieve para un servicio Web de aprendizaje de máquina clásico:

1. En el portal de servicios Web de Azure Machine Learning hello, haga clic en **servicios Web clásico** menú superior Hola.
2. Haga clic en el servicio Web de hello con el que está trabajando.
3. Haga clic en el punto de conexión de hello para el que desea que clave de hello tooretrieve.
4. En el menú superior de hello, haga clic en **usar**.
5. Copie y guarde hello **Primary Key**.

### <a name="classic-web-service"></a>Servicio web clásico
 También puede recuperar una clave para un servicio Web clásico de estudio de aprendizaje automático o hello portal de Azure clásico.

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. En estudio de aprendizaje automático, haga clic en **servicios WEB** de hello izquierda.
2. Haga clic en un servicio web. Hola **clave de API** en hello **panel** ficha.

#### <a name="azure-classic-portal"></a>Portal de Azure clásico
1. Haga clic en **aprendizaje automático** de hello izquierda.
2. Haga clic en el área de trabajo de hello en el que se encuentra el servicio Web.
3. Haga clic en **SERVICIOS WEB**.
4. Haga clic en un servicio web.
5. Haga clic en un extremo. Hola "Clave de API" está inactivo en hello inferior derecha.

## <a id="connect"></a>Conectar el servicio Web de aprendizaje de máquina tooa
Puede conectarse tooa servicio Web de aprendizaje de máquina mediante cualquier lenguaje de programación que admita la respuesta y solicitud HTTP. Puede ver ejemplos en C#, Python y R desde una página de ayuda de servicio web Machine Learning.

**Ayuda de la API de Machine Learning** Se crea una página de ayuda de API de Machine Learning al implementar un servicio web. Vea [Tutorial de Aprendizaje automático de Azure: Implementación de un servicio web](machine-learning-walkthrough-5-publish-web-service.md).
Hola ayuda de API de aprendizaje de máquina contiene detalles acerca de una servicio Web de predicción.

1. Haga clic en el servicio Web de hello con el que está trabajando.
2. Haga clic en el punto de conexión de hello para el que desea tooview Hola página de Ayuda de API.
3. En el menú superior de hello, haga clic en **usar**.
4. Haga clic en **página de Ayuda de API** en hello solicitud-respuesta o puntos de conexión de la ejecución por lotes.

**Ayuda de API de aprendizaje de máquina de tooview para un servicio Web nuevo**

Hola Portal de servicios de Web de aprendizaje de máquina de Azure:

1. Haga clic en **servicios WEB** en el menú superior Hola.
2. Haga clic en el servicio Web de hello para el que desea que clave de hello tooretrieve.

Haga clic en **Consume** tooget Hola URI hello Reposonse de solicitud y servicios de ejecución por lotes y código de ejemplo en C#, R y Python.

Haga clic en **Swagger API** tooget Swagger documentación en función de hello las API que se llama desde Hola proporcionado URI.

### <a name="c-sample"></a>Ejemplo de C#
tooconnect tooa servicio Web de aprendizaje de máquina, utilice un **HttpClient** pasar ScoreData. ScoreData contiene un FeatureVector, un vector de n dimensiones de características numéricos que representa hello ScoreData. Servicio de aprendizaje automático de toohello, autenticarse con una clave de API.

Hola tooconnect tooa servicio Web de aprendizaje de máquina, **Microsoft.AspNet.WebApi.Client** debe estar instalado el paquete de NuGet.

**Instalar Microsoft.AspNet.WebApi.Client NuGet en Visual Studio**

1. Publicar el conjunto de datos de descarga de Hola de UCI: conjunto de datos de clase de 2 para adultos servicio Web.
2. Haga clic en **Herramientas** > **Administrador de paquetes NuGet** > **Consola del administrador de paquetes**.
3. Elija **Install-Package Microsoft.AspNet.WebApi.Client**.

**ejemplo de código de hello toorun**

1. Publicar "ejemplo 1: descargar el conjunto de datos de UCI: conjunto de datos de contenido para adultos 2 clase" experimento, parte de la colección de aprendizaje automático de ejemplo de Hola.
2. Asignar apiKey con clave de Hola desde un servicio Web. Consulte el apartado anterior **Obtener una clave de autorización de Aprendizaje automático de Azure** .
3. Asignar serviceUri con hello URI de la solicitud.

### <a name="python-sample"></a>Ejemplo de Python
tooconnect tooa servicio Web de aprendizaje de máquina, utilice hello **urllib2** biblioteca pasar ScoreData. ScoreData contiene un FeatureVector, un vector de n dimensiones de características numéricos que representa hello ScoreData. Servicio de aprendizaje automático de toohello, autenticarse con una clave de API.

**ejemplo de código de hello toorun**

1. Implementar "ejemplo 1: descargar el conjunto de datos de UCI: conjunto de datos de contenido para adultos 2 clase" experimento, parte de la colección de aprendizaje automático de ejemplo de Hola.
2. Asignar apiKey con clave de Hola desde un servicio Web. Vea hello **obtener una clave de autorización de aprendizaje automático de Azure** sección principio Hola de este artículo.
3. Asignar serviceUri con hello URI de la solicitud.

