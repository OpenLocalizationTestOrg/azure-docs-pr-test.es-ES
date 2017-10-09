---
title: "documentación de Ayuda de aaaMulti geográfica | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un área de trabajo y publicar un servicio web en una región de Azure diferente de hello sur Central Estados Unidos (SCUS) región de Azure."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a>Documentación de ayuda multigeográfica
En este artículo se describe cómo crear un área de trabajo y publicar un servicio web en diferentes regiones de Azure.  Hola [productos de Azure por página región](https://azure.microsoft.com/en-us/regions/services/) enumera las áreas donde el aprendizaje automático de Azure está disponible.

## <a name="create-a-workspace"></a>Crear un área de trabajo
1. Inicie sesión en toohello Portal clásico de Azure.
2. Haga clic en **+ NUEVO** > **DATA SERVICES** > **MACHINE LEARNING** > **CREACIÓN RÁPIDA**.  En **UBICACIÓN**, seleccione otra región, como **Sudeste Asiático**.
   ![Imagen de ayuda multigeográfica 1][1]
3. Seleccione el área de trabajo de hello y, a continuación, haga clic en **inicio de sesión tooML Studio**.
   ![Imagen de ayuda multigeográfica 2][2]
4. Ahora dispone de un área de trabajo en otra región que se puede usar como cualquier otra área de trabajo. tooswitch entre las áreas de trabajo, busque toohello superior derecha de la pantalla. Haga clic en la lista desplegable de hello, región de hello seleccione y área de trabajo de hello, a continuación, seleccione. Todo lo que es la región del área de trabajo local toohello.  Por ejemplo, todos los servicios web creados a partir de un área de trabajo será Hola misma área de trabajo de Hola de región se encuentra en.
   ![Imagen de ayuda multigeográfica 3][3]

## <a name="open-an-experiment-from-gallery"></a>Abrir un experimento de Galería
Si abre un experimento desde la galería, también puede seleccionar qué región que desee toocopy Hola experimento en.

![Imagen de ayuda multigeográfica 4][4a]

## <a name="web-service-management"></a>Administración de servicios web
tooprogrammatically administrar servicios web, como de reciclaje, usar una dirección específica de la región hello:

* https://asiasoutheast.management.azureml.net
* https://europewest.management.azureml.net

### <a name="things-toonote"></a>Cosas toonote
1. Solo puede copiar experimentos entre áreas de trabajo que pertenecen toohello misma región de esta manera. Si necesita toocopy experimento en áreas de trabajo en distintas regiones, puede usar hello [PowerShell](http://aka.ms/amlps) commandlet [ *copia AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish que. Otra solución alternativa es toopublish Hola experimento en la Galería de modo que no figuran en, y vuelva a abrirla en el área de trabajo de Hola de hello otra región.
2. selector de región de Hello, solo se mostrarán las áreas de una región de trabajo a la vez.  
3. Se creará un área de trabajo libre o un área de trabajo (anónima) de acceso a invitados y se alojará en la zona central del sur de EE. UU.  
4. Los servicios web implementados desde un área de trabajo del sudeste asiático también se hospedarán en el sudeste asiático.  

## <a name="more-information"></a>Más información
Formule una pregunta en hello [foro de aprendizaje automático de Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
