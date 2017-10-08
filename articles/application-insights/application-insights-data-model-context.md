---
title: "aaaAzure modelos de datos de telemetría de visión de aplicación, contexto de telemetría | Documentos de Microsoft"
description: "Modelo de datos de contexto de telemetría de Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a>Contexto de telemetría: modelo de datos de Application Insights

Cada elemento de telemetría puede tener campos de contexto fuertemente tipados. Cada campo permite un escenario de supervisión específico. Utilice Hola propiedades personalizadas colección toostore personalizados o específicos de la aplicación información contextual.


##<a name="application-version"></a>Versión de la aplicación

La información en los campos de contexto de aplicación Hola está siempre acerca de la aplicación hello que está enviando la telemetría de Hola. Versión de la aplicación es usado tooanalyze tendencia cambios de comportamiento de la aplicación hello y sus implementaciones de toohello de correlación.

Longitud máxima: 1024


##<a name="client-ip-address"></a>Dirección IP de cliente

dirección IP de Hello hello de dispositivo de cliente. Se admiten IPv4 e IPv6. Cuando telemetría se envía desde un servicio, contexto de ubicación de hello es acerca del usuario de Hola que inició la operación de hello en el servicio de Hola. Application Insights extraen información de ubicación geográfica de Hola de dirección IP del cliente de hello y, a continuación, truncan. La IP del cliente no puede usarse por sí misma a modo de información de identificación del usuario final. 

Longitud máxima: 46


##<a name="device-type"></a>Tipo de dispositivo

Este campo se utilizaba originalmente tooindicate Hola tipo de dispositivo de usuario final Hola Hola de aplicación hello. Hoy en día utiliza principalmente toodistinguish JavaScript telemetría con hello tipo de dispositivo 'Browser' de telemetría de servidor con el tipo de dispositivo de hello 'Equipo'.

Longitud máxima: 64


##<a name="operation-id"></a>Identificador de operación

Un identificador único de la operación de raíz de Hola. Este identificador permite toogroup telemetría a través de varios componentes. Consulte [Correlación de telemetría](application-insights-correlation.md) para obtener más información. Id. de operación de Hola se crea mediante una solicitud o una vista de página. Todos los demás telemetría establece este valor de toohello de campo de Hola que contiene la vista de página o de solicitud. 

Longitud máxima: 128


##<a name="parent-operation-id"></a>Identificador de la operación principal

Identificador único del primario inmediato del elemento de hello telemetría de Hola. Consulte [Correlación de telemetría](application-insights-correlation.md) para obtener más información.

Longitud máxima: 128


##<a name="operation-name"></a>Nombre de la operación

nombre de Hello (grupo) de operación de Hola. nombre de la operación de Hola se crea mediante una solicitud o una vista de página. Todos los demás elementos de telemetría establecer este valor de toohello de campo para hello que contiene la vista de página o de solicitud. Nombre de la operación se utiliza para buscar todos los elementos de telemetría de Hola para un grupo de operaciones (por ejemplo ' GET Home/Index'). Esta propiedad de contexto es usado tooanswer preguntas como "¿Cuáles son Hola típico excepciones de esta página."

Longitud máxima: 1024


##<a name="synthetic-source-of-hello-operation"></a>Origen sintético de operación de Hola

Nombre del origen sintético. Algunos telemetría de aplicación hello puede representar tráfico sintético. Puede ser web rastreador (crawler) indización Hola de sitio web, pruebas de disponibilidad de sitio o seguimientos de bibliotecas de diagnóstico como Application Insights SDK propio.

Longitud máxima: 1024


##<a name="session-id"></a>Identificador de la sesión

Id. de sesión - instancia Hola Hola de interacción del usuario con la aplicación hello. Información de los campos de contexto de sesión de hello siempre es acerca del usuario final de Hola. Cuando telemetría se envía desde un servicio, contexto de la sesión de hello es acerca del usuario de Hola que inició la operación de hello en el servicio de Hola.

Longitud máxima: 64


##<a name="anonymous-user-id"></a>Identificador del usuario anónimo

Este es el identificador del usuario anónimo. Representa el usuario final de saludo de la aplicación hello. Cuando se envía la telemetría de un servicio, contexto de usuario de hello es acerca del usuario de Hola que inició la operación de hello en el servicio de Hola.

[Muestreo](app-insights-sampling.md) es una cantidad de hello técnicas toominimize Hola de telemetría recopilado. Tooeither de intentos de algoritmo de muestreo ejemplo o alejar Hola todos los ponen en correlación telemetría. El identificador del usuario anónimo se usa para muestrear la generación de puntuaciones. Por ello, el identificador del usuario anónimo debería ser un valor suficiente aleatorio. 

Con nombre de usuario de toostore de Id. de usuario anónimo es un uso inapropiado del campo de Hola. Use el identificador del usuario autenticado.

Longitud máxima: 128


##<a name="authenticated-user-id"></a>Identificador del usuario autenticado

Id. de usuario autenticado. Hola opuesto del identificador de usuario anónimo, este campo representa el usuario Hola con un nombre descriptivo. Puesto que se trata de información de identificación personal, la mayoría de SDK no la recopilan de forma predeterminada.

Longitud máxima: 1024


##<a name="account-id"></a>Identificador de la cuenta

En aplicaciones de varios inquilinos es Id. de cuenta de Hola o nombre, qué usuario Hola está actuando con. Algunos ejemplos son el identificador de la suscripción de Azure Portal o el nombre del blog de la plataforma de creación de blogs.

Longitud máxima: 1024


##<a name="cloud-role"></a>Rol en la nube

Nombre de aplicación Hola de hello rol es una parte de. Se asigna directamente toohello nombre del rol en azure. También puede ser usado toodistinguish micro servicios, que son parte de una sola aplicación.

Longitud máxima: 256


##<a name="cloud-role-instance"></a>Instancia de rol en la nube

Nombre de instancia de Hola donde se ejecuta la aplicación hello. El nombre de equipo del nombre de instancia local para Azure.

Longitud máxima: 256


##<a name="internal-sdk-version"></a>Interno: versión del SDK

Esta es la versión del SDK. Consulte https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification para obtener información.

Longitud máxima: 64


##<a name="internal-node-name"></a>Interno: nombre del nodo

Este campo representa el nombre de nodo Hola usado para la facturación. Usar detección estándar de hello toooverride de nodos.

Longitud máxima: 256


## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de cómo demasiado[ampliar y filtrar telemetría](app-insights-api-filtering-sampling.md).
- Consulte [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.
- Compruebe la [configuración](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) de la recopilación de propiedades estándar de contexto.
