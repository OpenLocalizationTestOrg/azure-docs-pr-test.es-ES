---
title: "aaaMicrosoft Dynamics CRM y visión de la aplicación de Azure | Documentos de Microsoft"
description: "Obtenga la telemetría de Microsoft Dynamics CRM Online con Application Insights. Tutorial sobre configuración, obtención de datos, visualización y exportación."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>Tutorial: Habilitar la telemetría para Microsoft Dynamics CRM Online con Application Insights
Este artículo muestra cómo los datos de telemetría tooget de [Microsoft Dynamics CRM Online](https://www.dynamics.com/) con [Azure Application Insights](https://azure.microsoft.com/services/application-insights/). Usaremos el proceso completo de Hola de agregar la aplicación de tooyour de secuencias de comandos de Application Insights, captura de datos y visualización de datos.

> [!NOTE]
> [Examinar la solución de ejemplo de Hola](https://dynamicsandappinsights.codeplex.com/).
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a>Agregar Application Insights toonew o instancia de CRM Online existente
toomonitor su aplicación, agregar una aplicación de tooyour Application Insights SDK. Hola SDK envía telemetría toohello [portal de Application Insights](https://portal.azure.com), donde puede usar nuestro análisis eficaces y herramientas de diagnóstico, o exportar hello toostorage de datos.

### <a name="create-an-application-insights-resource-in-azure"></a>Creación de un recurso de Application Insights en Azure
1. Obtenga una [cuenta en Microsoft Azure](http://azure.com/pricing). 
2. Inicio de sesión en hello [portal de Azure](https://portal.azure.com) y agregar un nuevo recurso de Application Insights. Aquí es donde se procesarán y mostrarán los datos.
   
    ![Haga clic en +, Servicios para desarrolladores, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    Elija ASP.NET como tipo de aplicación Hola.
3. Abra la página de introducción de Hola y abra "supervisar y diagnosticar el lado del cliente".
   
    ![Fragmento de código para inserción en la página web](./media/app-insights-sample-mscrm/03.png)

**Mantenga abierta la página de códigos de hello** mientras Hola siguiente paso en otra ventana del explorador. Código de hello, deberá pronto. 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>Creación de un recurso web de JavaScript en Microsoft Dynamics CRM
1. Abra la instancia de CRM Online e inicie sesión con privilegios de administrador.
2. Abra Microsoft Dynamics CRM configuración, las personalizaciones, personalizar Hola sistema
   
    ![Configuración de Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Configuración > Personalizaciones](./media/app-insights-sample-mscrm/05.png)

    ![Personalizar la opción de sistema de Hola](./media/app-insights-sample-mscrm/06.png)

1. Cree un recurso de JavaScript.
   
    ![Cuadro de diálogo de nuevo recurso web](./media/app-insights-sample-mscrm/07.png)
   
    Asígnele un nombre, seleccione **Script (JScript)** y Hola Abrir editor de texto.
   
    ![Editor de texto hello abierto](./media/app-insights-sample-mscrm/08.png)
2. Copie el código de hello de Application Insights. Mientras se copiaban que las etiquetas de script de tooignore seguro. Consulte la siguiente captura de pantalla:
   
    ![Establecer la clave de instrumentación](./media/app-insights-sample-mscrm/09.png)
   
    código de Hello incluye la clave de instrumentación de Hola que identifica el recurso de información de la aplicación.
3. Guarde y publique.
   
    ![Guardar y publicar](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>Formularios de instrumentos
1. En Microsoft CRM Online, abra el formulario de la cuenta de hello
   
    ![Formulario de la cuenta](./media/app-insights-sample-mscrm/11.png)
2. Abra el formulario de hello propiedades
   
    ![Propiedades del formulario](./media/app-insights-sample-mscrm/12.png)
3. Agregar Hola recurso web de JavaScript que ha creado
   
    ![Menú Agregar](./media/app-insights-sample-mscrm/13.png)
   
    ![Agregar recurso web de Hola](./media/app-insights-sample-mscrm/14.png)
4. Guarde y publique las personalizaciones de formulario.

## <a name="metrics-captured"></a>Métricas capturadas
Ha configurado una captura de telemetría del formulario de Hola. Cada vez que se utiliza, se enviará datos tooyour recursos de Application Insights.

Estos son ejemplos de datos de Hola que verá.

#### <a name="application-health"></a>Estado de la aplicación
![Ejemplo de tiempo de carga de página](./media/app-insights-sample-mscrm/15.png)

![Ejemplo de gráfico de vistas de página](./media/app-insights-sample-mscrm/16.png)

Excepciones de explorador:

![Gráfico de excepciones de explorador](./media/app-insights-sample-mscrm/17.png)

Haga clic en hello gráfico tooget más detalle:

![Lista de excepciones](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>Uso
![Sesiones, usuarios y vistas de página](./media/app-insights-sample-mscrm/19.png)

![Gráficos de sesión](./media/app-insights-sample-mscrm/20.png)

![Versiones de explorador](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>Exploradores
![Desglose de tiempo de carga de página](./media/app-insights-sample-mscrm/22.png)

![Recuento de sesiones por versión de explorador](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>Geolocalización
![Recuento de sesiones por país](./media/app-insights-sample-mscrm/24.png)

![Sesiones y usuarios por país](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>Solicitud de la vista de página interior
![Resumen de vistas de página](./media/app-insights-sample-mscrm/26.png)

![Buscar en eventos de vista de página](./media/app-insights-sample-mscrm/27.png)

![Vistas de página similares](./media/app-insights-sample-mscrm/28.png)

![Propiedades de la vista de página](./media/app-insights-sample-mscrm/29.png)

![Páginas por sesión](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>Código de ejemplo
[Examinar el código de ejemplo de Hola](https://dynamicsandappinsights.codeplex.com/).

## <a name="power-bi"></a>Power BI
Puede hacer un análisis más profundo incluso si se [exportar Hola datos tooMicrosoft Power BI](app-insights-export-power-bi.md).

## <a name="sample-microsoft-dynamics-crm-solution"></a>Solución de ejemplo de Microsoft Dynamics CRM
[Esta es la solución de ejemplo de Hola implementada en Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).

## <a name="learn-more"></a>Más información
* [¿Qué es Application Insights?](app-insights-overview.md)
* [Application Insights para páginas web](app-insights-javascript.md)
* [Más ejemplos y tutoriales](app-insights-code-samples.md)
