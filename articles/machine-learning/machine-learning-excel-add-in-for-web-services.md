---
title: "complemento aaaExcel para servicios Web de aprendizaje de máquina | Documentos de Microsoft"
description: "Cómo toouse Azure Machine Learning Web services directamente en Excel sin escribir ningún código."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a>Complemento de Excel para servicios web de Aprendizaje automático de Azure
Excel resulta fácil toocall los servicios web directamente sin Hola necesita toowrite cualquier código.

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a>Pasos tooUse un servicio web de Existing en hello libro

1. Abra hello [archivo de Excel de ejemplo](http://aka.ms/amlexcel-sample-2), que contiene Hola Excel complemento y datos acerca de los pasajeros en Hola Titanic.
2. Elija el servicio web de hello haciendo clic en él: "Titanic Predictor de permanencia (complemento de Excel de ejemplo) [puntuación]" en este ejemplo.
   
    ![Seleccionar un servicio web][01]
3. Esto le llevará toohello **Predict** sección.  Este libro ya contiene datos de ejemplo, pero para un libro en blanco también puede seleccionar una celda en Excel y hacer clic en **Usar datos de ejemplo**.
4. Seleccione datos Hola con los encabezados y haga clic en el icono de rango de datos de entrada de Hola.  Asegúrese de que está activada la casilla de "Mis datos tienen encabezados" de Hola.
5. En **salida**, escriba el número de células Hola donde desea Hola toobe de salida, por ejemplo "H1" aquí.
6. Haga clic en **Predicción**.
   
    ![Sección Predicción][02]

Implemente un servicio web o use uno existente. Para obtener más información acerca de cómo implementar un servicio web, consulte [tutorial paso 5: implementar el servicio Web de aprendizaje de máquina de Azure de hello](machine-learning-walkthrough-5-publish-web-service.md).

Obtener clave de API de hello para el servicio web. Realizará esta acción en un sitio u otro en función de si publicó un servicio web Machine Learning clásico o uno nuevo.

**Uso de un servicio web clásico** 

1. En estudio de aprendizaje automático, haga clic en hello **servicios WEB** sección en el panel izquierdo de hello y, a continuación, seleccione el servicio web de Hola.
   
    ![Seleccionar un servicio web de Studio][04]
2. Copie la clave de API de hello para el servicio web de Hola.
   
    ![Clave de API de Studio][05]
3. En hello **panel** para el servicio web de hello, haga clic en hello **solicitud/respuesta** vínculo.
4. Busque hello **URI de solicitud** sección.  Copie y guarde la dirección URL de Hola.

> [!NOTE]
> Ahora es posible toosign en hello [servicios Web de Azure Machine Learning](https://services.azureml.net) clave de API de hello tooobtain portal para un servicio web de aprendizaje automático clásico.
> 
> 

**Uso de un servicio web nuevo**

1. Hola [servicios Web de Azure Machine Learning](https://services.azureml.net) portal, haga clic en **servicios Web**, a continuación, seleccione el servicio web. 
2. Haga clic en **Consume**(Consumo).
3. Busque hello **información básica de consumo** sección. Copie y guarde hello **Primary Key** hello y **solicitud-respuesta** dirección URL.

## <a name="steps-tooadd-a-new-web-service"></a>Pasos tooAdd un nuevo servicio web

1. Implemente un servicio web o use uno existente. Para obtener más información acerca de cómo implementar un servicio web, consulte [tutorial paso 5: implementar el servicio Web de aprendizaje de máquina de Azure de hello](machine-learning-walkthrough-5-publish-web-service.md).
2. Haga clic en **Consume**(Consumo).
3. Busque hello **información básica de consumo** sección. Copie y guarde hello **Primary Key** hello y **solicitud-respuesta** dirección URL.
4. En Excel, vaya toohello **servicios Web** sección (si se encuentra en hello **Predict** sección, haga clic en hello flecha atrás toogo toohello lista de servicios web).
   
    ![Vaya tooWeb selección de servicio][03]
5. Haga clic en **Agregar servicio web**.
6. Pegue la URL de hello en hello la etiqueta de cuadro de texto de complemento de Excel **URL**.
7. Clave de API/primario pegar hello en el cuadro de texto hello con la etiqueta **clave de API**.
8. Haga clic en **Agregar**.
   
    ![Dirección URL y clave de API y de un servicio web clásico.][06]
9. servicio web de toouse hello, siga Hola anterior direcciones, "Pasos tooUse un servicio web de existente."

## <a name="sharing-your-workbook"></a>Compartir el libro
Si guarda el libro, clave de API principal de Hola para servicios web de hello que ha agregado también se guarda. Esto significa que solo deben compartir el libro Hola con personas de que confianza.

Hacer preguntas en hello después de la sección de comentarios o en nuestros [foro](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
