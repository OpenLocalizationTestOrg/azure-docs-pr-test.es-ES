---
title: aaaDeploy tooAzure Analysis Services mediante el uso de SSDT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy un tooan de modelo tabular Azure Analysis Services server mediante el uso de SSDT."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>Implementación de un modelo desde SSDT
Una vez que ha creado un servidor en su suscripción de Azure, está listo toodeploy un tooit de base de datos de modelo tabular. Puede usar SQL Server Data Tools (SSDT) toobuild e implementar un proyecto de modelo tabular que está trabajando. 

## <a name="prerequisites"></a>Requisitos previos
tooget iniciado, debe:

* **Servidor de Analysis Services** en Azure. más información, consulte toolearn [crear un servidor de Analysis Services de Azure](analysis-services-create-server.md).
* **Proyecto de modelos tabulares** en SSDT o un modelo tabular existente en Hola 1200 o nivel de compatibilidad superior. ¿Nunca ha creado ninguno? Intente hello [tutorial de modelado tabular ventas de Adventure Works Internet](https://msdn.microsoft.com/library/hh231691.aspx).
* **Puerta de enlace local** -si uno o varios orígenes de datos de forma local en la red de su organización, es necesario tooinstall una [puerta de enlace de datos local](analysis-services-gateway.md). puerta de enlace de Hello es necesario para la conexión de su servidor en la nube de hello tooyour datos orígenes tooprocess y la actualización de datos locales en el modelo de Hola.

> [!TIP]
> Antes de implementar, asegúrese de que puede procesar los datos de hello en las tablas. En SSDT, haga clic en **Modelo** > **Proceso** > **Procesar todo**. Si se produce un error de procesamiento, no se implementará correctamente.
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>toodeploy un modelo tabular desde SSDT

1. Antes de implementar, necesita el nombre del servidor de tooget Hola. En **portal de Azure** > servidor > **Introducción** > **nombre del servidor**, el nombre del servidor de copia Hola.
   
    ![Obtención del nombre del servidor en Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. En SSDT > **el Explorador de soluciones**, proyecto de hello contextual > **propiedades**. A continuación, en **implementación** > **Server** pegar el nombre del servidor de Hola.   
   
    ![Pegar el nombre del servidor en la propiedad del servidor de implementación](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. En el **Explorador de soluciones**, haga clic con el botón derecho en **Propiedades** y haga clic en **Implementar**. Es posible que toosign solicitada en tooAzure.
   
    ![Implementar tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    Estado de la implementación aparece en ventana de salida Hola y de implementar.
   
    ![Estado de implementación](./media/analysis-services-deploy/aas-deploy-status.png)

Eso es todo lo hay tooit!


## <a name="troubleshooting"></a>Solución de problemas
Si se produce un error en la implementación al implementar metadatos, es probable porque SSDT no pudo conectar a servidor tooyour. Asegúrese de que se puede conectar servidor tooyour con SSMS. A continuación, asegúrese de hello propiedad del servidor de implementación para el proyecto de hello es correcto.

Si se produce un error en la implementación en una tabla, es probable porque el servidor no pudo conectar el origen de datos de tooa. Si el origen de datos es local en la red de su organización, que seguro tooinstall una [puerta de enlace de datos local](analysis-services-gateway.md).

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene el servidor de modelo tabular implementado tooyour, está listo tooconnect tooit. También puede [conectar tooit con SSMS](analysis-services-manage.md) toomanage lo. Además, puede [conectar tooit mediante una herramienta cliente](analysis-services-connect.md) como Power BI, Power BI Desktop o Excel y empezar a crear informes.

