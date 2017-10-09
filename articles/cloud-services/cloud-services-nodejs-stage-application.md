---
title: "una implementación de servicio de nube (Node.js) aaaStage | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy su tooa de aplicación de Azure ensayo entorno, a continuación, implemente el entorno de producción de tooa con intercambio de IP Virtual (VIP)."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d65d26a6-b424-49cd-a88c-7ef46bb112a8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 0656c84ac444a10f152f441265f85141347bf1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="staging-an-application-in-azure"></a>Ensayo de una aplicación en Azure
Una aplicación empaquetada puede ser implementado toohello entorno de Azure toobe probado antes de moverla producción toohello de ensayo en qué Hola aplicación esté disponible en Internet Hola de entorno. El entorno de ensayo es exactamente como entorno de producción de hello, salvo que puede solo Hola acceso provisionalmente la aplicación con una dirección URL ofuscada generadas por Azure. Después de comprobar que la aplicación funciona correctamente, puede ser implementado toohello entorno de producción mediante la realización de un intercambio de IP Virtual (VIP).

> [!NOTE]
> Hello pasos de este artículo solo aplican las aplicaciones de toonode hospedadas como un servicio de nube de Azure.
> 
> 

## <a name="step-1-stage-an-application"></a>Paso 1: realizar el ensayo de una aplicación
Esta tarea cubre cómo toostage una aplicación mediante el uso de Hola **Microsoft Azure PowerShell**.

1. Al publicar un servicio, basta con pasar hello **-ranura** parámetro hello **AzureServiceProject publicar** cmdlet.
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. Inicie sesión en toohello [portal de Azure clásico] y seleccione **servicios en la nube**. Se crea después de servicio de nube de Hola y Hola **ensayo** estado de la columna se ha actualizado demasiado**ejecuta**, haga clic en el nombre del servicio de Hola.
   
   ![portal que muestra un servicio en ejecución][cloud-service]
3. Seleccione hello **panel**y, a continuación, seleccione **ensayo**.
   
   ![panel de servicio en la nube][cloud-service-dashboard]
4. Tenga en cuenta valor Hola Hola **dirección URL del sitio** derecha toohello de entrada. nombre DNS de Hello es un identificador interno confuso que genera Azure.
   
    ![Dirección URL del sitio][cloud-service-staging-url]

Ahora puede comprobar que aplicación hello funciona correctamente en hello entorno de ensayo mediante el uso de hello dirección URL del sitio de ensayo.

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>Paso 2: Actualizar una aplicación en producción mediante el intercambio de VIP
Después de haber comprobado Hola versión actualizada de una aplicación en el entorno de ensayo, se puede rápidamente, habilítela en producción intercambiando Hola direcciones IP virtuales (VIP) de los entornos de ensayo y producción de hello.

> [!NOTE]
> Este paso se asume que ya ha implementado una aplicación tooproduction y provisionalmente Hola versión actualizada de la aplicación.
> 
> 

1. Inicie sesión en hello [portal de Azure clásico], haga clic en **servicios en la nube** y, a continuación, seleccione el nombre del servicio de Hola.
2. De hello **panel**, seleccione **ensayo**y, a continuación, haga clic en **intercambiar** final Hola de página Hola. Se abrirá Hola cuadro de diálogo de intercambio de VIP.
   
   ![cuadro de diálogo Intercambio de VIP][vip-swap-dialog]
3. Revisar la información de hello y, a continuación, haga clic en **Aceptar**. las dos implementaciones de Hello inician la actualización como Hola implementación conmutadores hello y tooproduction producción implementación conmutadores toostaging de almacenamiento provisional.

Ha almacenado provisionalmente una implementación y actualizar una implementación de producción intercambiando las VIP a la implementación de hello en almacenamiento provisional.

## <a name="additional-resources"></a>Recursos adicionales
* [¿Cómo tooDeploy un tooProduction el servicio de actualización mediante el intercambio de VIP en Azure]

[portal de Azure clásico]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[¿Cómo tooDeploy un tooProduction el servicio de actualización mediante el intercambio de VIP en Azure]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
