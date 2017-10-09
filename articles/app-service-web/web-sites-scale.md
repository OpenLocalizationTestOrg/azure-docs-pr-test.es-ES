---
title: "aaaScale seguridad de una aplicación en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale seguridad de una aplicación en la capacidad de tooadd de servicio de aplicaciones de Azure y características."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a>Escalado vertical de aplicaciones en Azure
Este artículo muestra cómo tooscale la aplicación de servicio de aplicaciones de Azure. Hay dos flujos de trabajo para la escala de escala, seguridad y escalado horizontal y este artículo explica Hola de escalado vertical flujo de trabajo.

* [Escalado vertical](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): obtenga más CPU, memoria, espacio en disco y características adicionales como máquinas virtuales exclusivas, dominios y certificados personalizados, espacios de ensayo, autoescala y mucho más. Escalar verticalmente cambiando Hola tarifa del plan de servicio de aplicaciones al que pertenece la aplicación.
* [Escalar horizontalmente](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): aumentar Hola número de instancias de máquina virtual que ejecuta la aplicación.
  Puede escalar horizontalmente tooas muchas como 20 instancias, según el nivel de precios. [Entornos del servicio de aplicación](../app-service/app-service-app-service-environments-readme.md) en **Premium** capa aumentarán las instancias de too50 de recuento de escalabilidad horizontal. Para más información sobre el escalado horizontal, consulte [Escalado del número de instancias de forma manual o automática](../monitoring-and-diagnostics/insights-how-to-scale.md). Allí encontrará espera cómo toouse escalado automático, que es el número de instancias de tooscale automáticamente en función de reglas predefinidas y las programaciones.

Hola escala configuración toman sólo segundos tooapply y afecta a todas las aplicaciones en su [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
No se requieren toochange el código o volver a implementar la aplicación.

Para obtener información sobre precios de Hola y las características de los planes de servicio de aplicaciones individuales, consulte [detalles de precios de servicio de aplicación](https://azure.microsoft.com/pricing/details/web-sites/).  

> [!NOTE]
> Antes de cambiar un plan de servicio de aplicaciones de hello **libre** nivel, primero debe quitar hello [los límites de gastos](https://azure.microsoft.com/pricing/spending-limits/) en su lugar para la suscripción de Azure. tooview o cambiar opciones de la suscripción de servicio de aplicaciones de Microsoft Azure, vea [suscripciones de Microsoft Azure][azuresubscriptions].
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>Escalado vertical del plan de tarifa
1. En el explorador, abra hello [portal de Azure][portal].
2. En la hoja de la aplicación, haga clic en **Toda la configuración** y en **Escalar verticalmente**.
   
    ![Navegue tooscale seguridad de la aplicación de Azure.][ChooseWHP]
3. Elija el nivel y, después, haga clic en **Seleccionar**.
   
    Hola **notificaciones** ficha parpadeará en un color verde **correcto** una vez completada la operación de Hola.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>Recursos relacionados con el escalado
Si su aplicación depende de otros servicios, como Base de datos SQL o Almacenamiento de Azure, también puede escalar verticalmente estos recursos según sus necesidades. Estos recursos no se escalan con hello plan de servicio de aplicaciones y se deben escalar por separado.

1. En **Essentials**, haga clic en hello **grupo de recursos** vínculo.
   
    ![Escalado vertical de recursos relacionados con la aplicación de Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. Hola **resumen** forma parte de hello **grupo de recursos** hoja, haga clic en un recurso que desea tooscale. Hola siguiente captura de pantalla muestra un recurso de base de datos SQL y un recurso de almacenamiento de Azure.
   
    ![Navegue tooresource grupo hoja tooscale seguridad de la aplicación de Azure](./media/web-sites-scale/ResourceGroup.png)
3. Para un recurso de base de datos SQL, haga clic en **configuración** > **tarifa** hello tooscale nivel de precios.
   
    ![Escalar verticalmente el back-end de base de datos SQL de hello para la aplicación de Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    También puede activar la [replicación geográfica](../sql-database/sql-database-geo-replication-overview.md) de su instancia de Base de datos SQL.
   
    Para un recurso de almacenamiento de Azure, haga clic en **configuración** > **configuración** tooscale una de las opciones de almacenamiento.
   
    ![Escalar verticalmente la cuenta de almacenamiento de Azure de hello utilizado por la aplicación de Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>Más información sobre las características del desarrollador
Función Hola tarifa hello siguientes orientadas al desarrollador características están disponibles:

### <a name="bitness"></a>Valor de bits
* Hola **básica**, **estándar**, y **Premium** niveles admiten aplicaciones de 64 bits y 32 bits.
* Hola **libre** y **Shared** plan niveles admiten sólo las aplicaciones de 32 bits.

### <a name="debugger-support"></a>Compatibilidad con el depurador
* Compatibilidad del depurador está disponible para hello **libre**, **Shared**, y **básica** modos en una conexión por cada plan de servicio de aplicaciones.
* Compatibilidad del depurador está disponible para hello **estándar** y **Premium** modos en cinco conexiones simultáneas por plan de servicio de aplicaciones.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>Más información sobre otras características
* Para obtener información detallada acerca de todos los de hello restantes características Hola servicio de aplicaciones de planes, incluido el precio y características de interés tooall los usuarios (incluidos los desarrolladores), consulte [detalles de precios de servicio de aplicación](https://azure.microsoft.com/pricing/details/web-sites/).

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/) donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con Azure, consulte [evaluación gratuita de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).
* Para obtener información sobre los precios, soporte técnico y SLA, visitan Hola siguientes vínculos.
  
    [Detalles de precios de Transferencias de datos](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Planes de soporte técnico de Azure](https://azure.microsoft.com/support/plans/)
  
    [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/)
  
    [Detalles de precios de Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Tamaños de máquinas virtuales y servicios en la nube de Microsoft Azure][vmsizes]
  
    [Detalles de precios del Servicio de aplicaciones](https://azure.microsoft.com/pricing/details/app-service/)
  
    [Detalles de precios de Servicios de aplicaciones: las conexiones SSL](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* Para obtener información sobre las prácticas recomendadas de Servicios de aplicaciones de Azure, incluida la creación de una arquitectura resistente y escalable, consulte [Prácticas recomendadas: Aplicaciones web del Servicio de aplicaciones de Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).
* Para ver vídeos acerca de cómo escalar aplicaciones de servicio de aplicaciones, vea Hola recursos siguientes:
  
  * [Cuando tooScale sitios Web de Azure - con Stefan Schackow](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [Escalación automática de sitios web de Azure mediante CPU o programación: con Stefan Schackow](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [Escalación de sitios web de Azure: con Stefan Schackow](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
