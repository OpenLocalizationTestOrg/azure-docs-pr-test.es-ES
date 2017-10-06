---
title: aaaHow toodeploy un servicio Web regiones toomultiple | Documentos de Microsoft
description: Pasos toodeploy (copiar) un regiones de tooother nuevo servicio Web.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a>¿Cómo toodeploy un servicio Web toomultiple regiones
Hola nuevos servicios de Web de Azure le permiten tooeasily implementar un regiones de toomultiple del servicio web sin necesidad de varias suscripciones o áreas de trabajo. 

El precio es específica, por tanto, debe definir un plan de facturación para cada región en el que va a implementar el servicio web de hello de la región.

## <a name="toocreate-a-plan-in-another-region"></a>toocreate un plan en otra región
1. Inicie sesión en el [portal de servicios web de Aprendizaje automático de Microsoft Azure](https://services.azureml.net/).
2. Haga clic en hello **planes** opción de menú.
3. En los planes de Hola a través de la página de vista, haga clic en **nuevo**.
4. De hello **suscripción** lista desplegable, suscripción Hola seleccione en qué Hola va a residir nuevo plan.
5. De hello **región** lista desplegable, seleccione una región para el nuevo plan de Hola. Hola opciones del Plan para la región seleccionada Hola se mostrará en hello **opciones del Plan de** sección de página de Hola.
6. De hello **grupo de recursos** lista desplegable, seleccione un recurso de grupo para el plan de Hola. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
7. En **el nombre del Plan** nombre de plan de Hola Hola de tipo.
8. En **opciones del Plan de**, haga clic en el nivel de facturación de Hola de nuevo plan de Hola.
9. Haga clic en **Crear**.

## <a name="deploying-hello-web-service-tooanother-region"></a>Implementar hello web servicio tooanother área
1. Haga clic en hello **servicios Web** opción de menú.
2. Seleccione Hola servicio Web que se va a implementar tooa nueva región.
3. Haga clic en **Copiar**.
4. En **nombre del servicio Web**, escriba un nombre nuevo para el servicio web de Hola.
5. En **descripción de servicio Web**, escriba una descripción para el servicio web de Hola.
6. De hello **suscripción** lista desplegable, suscripción Hola seleccione en qué Hola va a residir nuevo servicio web.
7. De hello **grupo de recursos** lista desplegable, seleccione un recurso de grupo para el servicio web de Hola. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. De hello **región** lista desplegable región seleccione hello en el servicio web que toodeploy Hola.
9. De hello **cuenta de almacenamiento** lista desplegable, seleccione una cuenta de almacenamiento en qué hello toostore servicio web.
10. De hello **Plan de precios** lista desplegable, seleccione un plan en la región de Hola que seleccionó en el paso 8.
11. Haga clic en **Copiar**.

