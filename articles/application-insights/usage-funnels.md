---
title: Embudos de Azure Application Insights
description: "Obtenga información sobre cómo usar Funnels para descubrir la forma en que los clientes interactúan con la aplicación."
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: mbullwin
ms.openlocfilehash: bbb25af888f34737f6a61cf43890ff248c4cc4de
ms.sourcegitcommit: cf42a5fc01e19c46d24b3206c09ba3b01348966f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/29/2017
---
# <a name="discover-how-customers-are-using-your-application-with-application-insights-funnels"></a>Descubra cómo los clientes usan la aplicación con los embudos de Application Insights.

Conocer la experiencia de los clientes es de suma importancia para su negocio. Si la aplicación implica varias fases, debe saber si la mayoría de los clientes avanzan a través de todo el proceso, o si finalizan el proceso en algún momento. La progresión a través de una serie de pasos en una aplicación web se conoce como *embudo*. Puede usar los embudos de Azure Application Insights para obtener información sobre los usuarios y supervisar las tasas de conversión detalladas. 

## <a name="create-your-funnel"></a>Creación de un embudo
Antes de crear el embudo, decida la pregunta a la que quiere obtener respuesta. Por ejemplo, es posible que desee saber cuántos usuarios están visualizando la página principal, viendo un perfil de cliente y creando un vale. En este ejemplo, los propietarios de la compañía Fabrikam Fiber desean conocer el porcentaje de clientes que han creado correctamente un vale de cliente.

Estos son los pasos que deben seguir para crear un embudo.

1. En la herramienta Embudos de Application Insights, seleccione **Nuevo**.
1. En el menú desplegable **Intervalo de tiempo**, seleccione **Últimos 90 días**. Seleccione **Mis embudos** o **Embudos compartidos**.
1. En la lista desplegable **Paso 1**, seleccione **Índice**. 
1. En la lista **Paso 2**, seleccione **Cliente**.
1. En la lista **Paso 3**, seleccione **Crear**.
1. Agregue un nombre para el embudo y seleccione **Guardar**.

En la siguiente captura de pantalla se muestra un ejemplo de tipo de datos que la herramienta Embudos genera. Los propietarios de Fabrikam pueden ver que, durante los últimos 90 días, el 54,3 % de sus clientes que visitó la página principal crearon un vale de cliente. También pueden ver que 2700 clientes consultaron el índice desde la página principal. Esto podría indicar un problema de actualización.


![Captura de pantalla de la herramienta Embudos con datos](./media/app-insights-understand-usage-patterns/funnel1.png)

### <a name="funnels-features"></a>Características de Embudos
La captura de pantalla anterior incluye cinco áreas resaltadas. Se trata de características de Embudos. En la lista siguiente se ofrecen más detalles sobre cada área correspondiente de la captura de pantalla:
1. Si la aplicación está muestreada, se mostrará un banner de muestreo. Al seleccionar el banner, se abre un panel contextual, en el que se explica cómo desactivar el muestreo. 
2. Puede exportar el embudo a [Power BI](app-insights-export-power-bi.md).
3. Seleccione un paso para ver más detalles a la derecha. 
4. En el gráfico del historial de conversiones se muestran tasas de conversión de los últimos 90 días. 
5. Acceda a la herramienta de los usuarios para comprenderlos mejor. Puede usar filtros en cada paso. 

## <a name="next-steps"></a>Pasos siguientes
  * [Información general del uso](app-insights-usage-overview.md)
  * [Usuarios, sesiones y eventos](app-insights-usage-segmentation.md)
  * [Retención](app-insights-usage-retention.md)
  * [Libros](app-insights-usage-workbooks.md)
  * [Adición de contexto de usuario](app-insights-usage-send-user-context.md)
  * [Exportación a Power BI](app-insights-export-power-bi.md)

