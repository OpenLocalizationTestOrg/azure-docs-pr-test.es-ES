---
title: "extremos de servicios Web de aaaCreating en el aprendizaje automático | Documentos de Microsoft"
description: "Creación de puntos de conexión de servicio web en Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>Creación de extremos
> [!NOTE]
>  En este tema se describe técnicas aplicables tooa **clásico** servicio Web de aprendizaje de máquina.
> 
> 

Al crear servicios Web que venden a los clientes tooyour hacia delante, deberá a tooprovide modelos entrenados tooeach cliente experimento toohello todavía vinculado desde qué hello Web se creó el servicio. Además, las actualizaciones debe toohello experimento aplican selectivamente tooan extremo sin sobrescribir las personalizaciones de Hola.

tooaccomplish, aprendizaje automático de Azure permite toocreate varios puntos de conexión de un servicio Web implementado. Cada extremo de servicio Web de hello independientemente está dirigido, limitada y administra. Cada punto de conexión es una clave única de autorización y la dirección URL que puede distribuir a los clientes de tooyour.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>Agregar servicio Web de los puntos de conexión tooa
Hay tres tooadd formas un tooa punto de conexión del servicio Web.

* De manera programática
* A través del portal de servicios Web de Azure Machine Learning Hola
* Aunque Hola portal de Azure clásico

Una vez que se crea el extremo de hello, puede consumir a través de la API sincrónicas, lote API y las hojas de cálculo de excel. Además tooadding los puntos de conexión a través de esta interfaz de usuario, también puede usar hello las API de administración de punto de conexión tooprogrammatically agregar puntos de conexión.

> [!NOTE]
> Si ha agregado los puntos de conexión adicionales toohello servicio Web, no se puede eliminar el punto de conexión de hello predeterminado.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>Incorporación de un punto de conexión mediante programación
Puede agregar un servicio de punto de conexión tooyour Web mediante programación con hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de ejemplo.

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>Agregar un punto de conexión mediante el portal de servicios Web de Azure Machine Learning Hola
1. En estudio de aprendizaje automático, en la columna de navegación izquierdo de hello, haga clic en servicios Web.
2. En hello parte inferior del panel de servicio de hello Web, haga clic en **administrar puntos de conexión**. portal de servicios Web de Azure Machine Learning Hola abrirá la página de los puntos de conexión de toohello de hello servicio Web.
3. Haga clic en **Nuevo**.
4. Escriba un nombre y una descripción para el nuevo punto de conexión de Hola. Los nombres de los puntos de conexión deben tener 24 caracteres o menos y deben estar formados por letras en minúsculas o números. Seleccione el nivel de registro de hello y si los datos de ejemplo está habilitado. Para obtener más información sobre el registro, consulte [Habilitación del registro para los servicios web Machine Learning](machine-learning-web-services-logging.md).

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>Agregar un punto de conexión mediante Hola portal de Azure clásico
1. Inicie sesión en toohello [portal de Azure clásico](http://manage.windowsazure.com), haga clic en **aprendizaje automático** en la columna izquierda de Hola. Haga clic en el área de trabajo de Hola que contiene el servicio Web de hello en el que esté interesado.
   
    ![Navegue tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. Haga clic en **Servicios web**.
   
    ![Explorar los servicios de tooWeb](./media/machine-learning-create-endpoint/figure-2.png)
3. Haga clic en el servicio Web de hello está interesado en la lista de hello toosee de puntos de conexión disponibles.
   
    ![Navegue tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. En la parte inferior de Hola de página de hello, haga clic en **Agregar extremo**. Escriba un nombre y una descripción, asegúrese de que no hay ningún otros puntos de conexión con el mismo nombre en este servicio Web de Hola. Deje el nivel de limitación de hello con su valor predeterminado a menos que tenga requisitos especiales. toolearn más acerca de la limitación, consulte [ajuste de escala en los extremos de API](machine-learning-scaling-webservice.md).
   
    ![Crear extremo](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>Pasos siguientes
[¿Cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).

