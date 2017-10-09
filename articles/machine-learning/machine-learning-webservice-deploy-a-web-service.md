---
title: "aaaDeploying un nuevo servicio web de aprendizaje automático de Azure | Documentos de Microsoft"
description: "flujo de trabajo de saludo de la implementación de un BRAZO en función de servicio web"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a>Implementación de servicios web nuevos
Microsoft Azure Machine learning ahora proporciona servicios web que se basan en [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permitiendo nuevas opciones del plan de facturación y la implementación de las áreas de toomultiple del servicio web.

flujo de trabajo general de Hello toodeploy un servicio web mediante servicios Web de Microsoft Azure Machine Learning es:

* Crear un experimento predictivo
* Implementarlo
* Configurar su nombre
* plan de facturación
* Probarlo
* Utilizarlo

Hola siguiente gráfico ilustra el flujo de trabajo de Hola.

![Flujo de trabajo de implementación de servicios web][1]

## <a name="deploy-web-service-from-studio"></a>Implementación de servicios web desde Studio
toodeploy un experimento como un nuevo servicio web. Inicie sesión en estudio de aprendizaje automático de Hola y crear un nuevo servicio web de predicción. 

**Nota**: Si ya ha implementado un experimento como servicio web clásico, no se podrá implementar como nuevo.

Haga clic en **ejecutar** final Hola de hello experimentar el lienzo y, a continuación, haga clic en **implementar el servicio de Web** y **implementar [New] servicio Web**. se abrirá la página de implementación de Hello del administrador del servicio Web de aprendizaje de máquina de Hola.

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a>Página de implementación de experimentos del administrador de servicios web de Aprendizaje automático
En página de experimento implementar hello, escriba un nombre para el servicio web de Hola.
Seleccione un plan de tarifa. En caso contrario, si tiene un plan de precios existente que seleccione la plantilla, debe crear un nuevo plan de precios para el servicio de Hola. 

1. Hola **Plan de precios** de lista desplegable, seleccione un plan existente o hello **seleccione Nuevo plan** opción.
2. En **el nombre del Plan**, escriba un nombre que identificará el plan de hello en la factura.
3. Seleccione uno de hello **mensual niveles planear**. Tenga en cuenta que los niveles de plan de hello predeterminado toohello planes para la región predeterminada y el servicio web es la región de toothat implementado.

Haga clic en **implementar** y se abre la página de inicio rápido de hello para el servicio web.

## <a name="quickstart-page"></a>Página Inicio rápido
página de inicio rápido del servicio de Hello web proporciona acceso e instrucciones sobre las tareas más comunes de hello que llevará a cabo después de crear un nuevo servicio web. Desde aquí puede acceder fácilmente ambos hello **prueba** página y **Consume** página.

## <a name="testing-your-web-service"></a>Pruebas del servicio web
Desde la página de inicio rápido de hello, haga clic en servicio web de prueba en las tareas comunes.   

servicio web de hello tootest como un servicio de solicitud-respuesta (RR):

* Haga clic en **prueba** en la barra de menús de Hola.
* Haga clic en **Request-Response**(Solicitud-respuesta).
* Escriba los valores adecuados para las columnas de entrada de su experimento Hola.
* Haga clic en **Test Request-Response**(Probar solicitud-respuesta).

Resultados se muestran en hello lado derecho de la página de Hola.

tootest un servicio web de servicio de ejecución de lotes (BES), se utilizará un archivo CSV:

* Haga clic en **prueba** en la barra de menús de Hola.
* Haga clic en **Lotes**.
* En la entrada, haga clic en Examinar y navegar por el archivo de datos de ejemplo de tooyour.
* Haga clic en **Probar**.

estado de saludo de la prueba se muestra bajo **probar los trabajos por lotes**.

## <a name="consuming-your-web-service"></a>Uso de servicios web
Cuando se implementa como servicio web, los experimentos de Aprendizaje automático de Azure proporcionan una API de REST que puede ser consumida por una amplia gama de dispositivos y plataformas. Esto es porque los mensajes con formato Hola simple API de REST acepta y responde con JSON. portal de aprendizaje automático de Azure Hello proporciona código que se puede usar toocall Hola servicio web en R, C# y Python.

En la página de hello Consuming encontrará:

* clave de API de Hola y el URI para consumir el servicio web en aplicaciones.
* Tookick de plantillas de aplicación web y Excel inicie el proceso de consumo.
* Código de ejemplo en C#, python y R tooget ha iniciado.

Para obtener más información sobre el consumo de servicios web, consulte [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre el consumo de servicios web, consulte:

[¿Cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md)

[Servicios web Azure Machine Learning: Implementación y consumo](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
