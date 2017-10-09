---
title: "información general de API de exportación de interacción de aaaMobile"
description: "Obtenga información acerca de conceptos básicos de hello acerca de cómo exportar los datos sin procesar generan por tooleverage de dispositivos de sus usuarios, en sus propias herramientas"
services: mobile-engagement
documentationcenter: mobile
author: kpiteira
manager: erikre
editor: 
ms.assetid: 9380d47b-d7fa-4d4c-888f-97e6482196bb
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 04/26/2016
ms.author: kapiteir
ms.openlocfilehash: f55be29a29878e74f6a33419f08a5574a07a7478
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mobile-engagement-export-api-overview"></a>Información general de API de exportación de Mobile Engagement
## <a name="introduction"></a>Introducción
En este documento, obtendrá información sobre conceptos básicos de hello acerca de cómo exportar los datos sin procesar generan por tooleverage de dispositivos de sus usuarios, en sus propias herramientas.

## <a name="pre-requisites"></a>Requisitos previos
Exportación de datos sin procesar de Hola de Mobile Engagement requiere:

* Toobe toouse capaz de hello las API de API autenticación el programa de instalación (consulte [el programa de instalación manual de autenticación](mobile-engagement-api-authentication-manual.md)),
* Usar las API de REST de Hola o hello [.net SDK](mobile-engagement-dotnet-sdk-service-api.md),
* Una cuenta de almacenamiento de Azure.

> [!NOTE]
> También se recomienda Hola excelente [Microsoft Azure Storage Explorer](http://storageexplorer.com/), al menos durante la fase de desarrollo de hello tal como se proporciona una interfaz de usuario de toouse fácil para interactuar con el almacenamiento de Azure.
> 
> 

## <a name="what-can-be-exported"></a>¿Qué se puede exportar?
Mobile Engagement permite que sus usuarios toocollect muchos tipos de datos y, por tanto, con varios tipos de exportación adecuadas toothese distintos tipos de datos.
Hay 2 tipos esenciales de exportación:

* Instantánea: se suelen usar tooexport datos que representa un estado y para el que no tiene un historial de Mobile Engagement. Esto incluye, por ejemplo, etiquetas (información de la aplicación), tokens o comentarios de campañas de inserción. Como consecuencia estos tipos de exportación no están relacionados con la fecha de tooa.
* Históricos: este tipo de exportación se usa para datos que se acumulan a lo largo del tiempo, como eventos o actividades, por ejemplo.

Hola tabla siguiente describen exhaustivamente, todas las exportaciones posibles de hello:

| Tipo de exportación | Tipo de datos | Descripción |
| --- | --- | --- |
| Instantánea |Insertar |Genera una exportación de comentarios de campañas de inserción por identificador de dispositivo o identificador de usuario |
| Instantánea |Etiqueta |Genera una exportación de hello etiquetas (app-info) asociadas tooeach dispositivos |
| Instantánea |Dispositivo |Genera una exportación de la mayoría de los datos de hello acerca de los dispositivos, como technicals de hello (modelo, la configuración regional, zona horaria,...), etiquetas de Hola la primera vez encontrada... |
| Instantánea |SWT |Genera una exportación de todos los tokens de hello válido |
| Históricos |Actividad |Genera una exportación de todas las actividades de Hola para cada dispositivo en un período de tiempo determinado |
| Históricos |Evento |Genera una exportación de todas las actividades de Hola para cada dispositivo en un período de tiempo determinado |
| Históricos |Trabajo |Genera una exportación de todos los trabajos de Hola para cada dispositivo en un período de tiempo determinado |
| Históricos |Error |Genera una exportación de todos los errores de Hola para cada dispositivo en un período de tiempo determinado |

## <a name="how-does-it-work"></a>¿Cómo funciona?
Las exportaciones son tareas de larga ejecución que puede producir archivos de datos grandes. Por esta razón, no pueden ser invocado tooreturn inmediatamente una toodownload de archivo.
Datos de pedidos tooexport de Mobile Engagement, tendrá que toocreate una **trabajo de exportación de** a través de API donde debe especificar por lo general:

* tipo de Hola de exportación (instantánea o histórico)
* tipo de datos de Hello,
* Hola **contenedor de almacenamiento de Azure** (incluida una SAS válida con acceso de escritura) donde se escribirá el resultado de hello de exportación de Hola.
* Por ejemplo, el parámetro de la dirección URL del contenedor podría ser https://[StorageAccountName].blob.core.windows.net/[ContainerName]?[SASWritePermissionsToken]  

Aquí le mostramos un ejemplo real. https://testazmeexport.blob.core.windows.net/test1234azme?sv=2015-12-11&ss=b&srt=sco&sp=rwdlac&se=2016-12-17T04:59:26Z&st=2016-12-16T20:59:26Z&spr=https&sig=KRF3aVWjp2NEJDzjlmoplmu0M9HHlLdkBWRPAFmw90Q%3D

Tenga en cuenta que puede tardar unos minutos para su toobe trabajo iniciado y, a continuación, se puede ejecutar desde unos segundos para las horas de tooseveral minúsculo aplicaciones para las aplicaciones con una gran cantidad de usuarios o actividad.

Una vez que se crea el trabajo de hello, es posible toocheck su toosee estado si está aún en ejecución o si se ha completado.

Una vez que se ha realizado correctamente el trabajo de hello, archivo de datos resultante de hello está disponible en hello proporcionada el contenedor de almacenamiento.

