---
title: "aaaHow tooincrease simultaneidad de un servicio web de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooincrease simultaneidad de un aprendizaje automático de Azure de servicio web mediante la adición de puntos de conexión adicionales."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "aprendizaje automático de azure, servicios web, operacionalización, escalado, punto de conexión, simultaneidad"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>Escalado de un servicio web de Azure Machine Learning mediante la incorporación de puntos de conexión adicionales
> [!NOTE]
> En este tema se describe técnicas aplicables tooa **clásico** servicio Web de aprendizaje de máquina. 
> 
> 

De forma predeterminada, cada servicio Web publicado es 20 solicitudes simultáneas de toosupport configurado y puede ser tan alto como 200 solicitudes simultáneas. Aunque Hola portal de Azure clásico proporciona una manera tooset este valor, aprendizaje automático de Azure optimiza automáticamente Hola configuración tooprovide Hola obtener el mejor rendimiento para el servicio web y se omite el valor de portal de Hola. 

Si tiene previsto toocall Hola API con una carga más elevada de será compatible con un valor de número máximo de llamadas simultáneas de 200, debe crear varios puntos de conexión en hello mismo servicio Web. Acto seguido, podrá distribuir aleatoriamente la carga entre todos ellos.

Hola ajuste de escala de un servicio Web es una tarea común. Algunas razones tooscale son toosupport más de 200 solicitudes simultáneas, aumentar la disponibilidad a través de varios puntos de conexión o proporcionar puntos de conexión independientes para el servicio web de Hola. Puede aumentar escala Hola agregando extremos adicionales en hello mismo servicio Web a través de [portal de Azure clásico](https://manage.windowsazure.com/) o hello [servicio Web de Azure Machine Learning](https://services.azureml.net/) portal.

Para obtener más información sobre la incorporación de puntos de conexión nuevos, consulte [Creación de puntos de conexión](machine-learning-create-endpoint.md).

Tenga en cuenta que con un recuento de alta simultaneidad puede ser perjudicial si no se está llamando a Hola API con una tasa alta según corresponda. Podría ver los tiempos de espera esporádicas o picos de latencia de hello si coloca una carga relativamente baja en una API configurada para una carga elevada.

Hola que API sincrónicas se utilizan habitualmente en situaciones donde se desea una baja latencia. Latencia aquí implica tiempo Hola toma para una solicitud de API de hello toocomplete y no en cuenta los retrasos de red. Supongamos que tiene una API con una latencia de 50 ms. toofully consumir capacidad disponible de hello con nivel de limitación de alto y el número máximo de llamadas simultáneas = 20, necesita toocall esta API 20 * 1000 / 400 = 50 veces por segundo. Extender aún más, un número máximo de llamadas simultáneas de 200 permite toocall Hola API 4000 veces por segundo, suponiendo un 50-ms de latencia.

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
