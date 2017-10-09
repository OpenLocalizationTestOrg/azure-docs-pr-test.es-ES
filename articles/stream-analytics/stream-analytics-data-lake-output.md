---
title: "aaaStream Lake almacén resultado del análisis de datos | Documentos de Microsoft"
description: "Configuración de la autenticación y la autorización de un Almacén de Azure Data Lake en un trabajo de Análisis de transmisiones"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a>Salida de los Análisis de transmisiones del Almacén de Data Lake
Los trabajos de Análisis de transmisiones admiten varios métodos de salida, y uno de ellos es el [Almacén de Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/). El Almacén de Azure Data Lake es un repositorio de gran escala en toda la empresa para cargas de trabajo de análisis de macrodatos. Almacén de Data Lake permite toostore datos de cualquier tamaño, el tipo y la ingesta de velocidad para análisis operativos y exploratorios.

## <a name="authorize-a-data-lake-store-account"></a>Autorización de una cuenta del Almacén de Data Lake
1. Cuando se selecciona el almacén de Data Lake como una salida en hello portal de Azure, se le pedirá tooauthorize uso del almacén de Data Lake existente o toorequest acceso toohello de almacén de Data Lake a través de hello Portal clásico.
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. Si ya tiene acceso tooData Lake almacén, haga clic en "Autorizar ahora" y de un breve período de tiempo una página mostrará que indica "Redirigir tooauthorization". página de Hola se cerrará automáticamente y aparecerá con la página de Hola que permitiría tooconfigure Hola almacén de Data Lake salida.

Si no se ha registrado para el almacén de Data Lake, puede seguir solicitud Hola de tooinitiate de "Sign up now" de vínculo de Hola o siga hello [obtener instrucciones iniciadas](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="configure-hello-data-lake-store-output-properties"></a>Configurar las propiedades de salida de almacén de Data Lake Hola
Una vez que tenga cuenta de almacén de Data Lake Hola autenticado, puede configurar propiedades de hello para la salida de almacén de Data Lake. Hola tabla es la lista de Hola de nombres de propiedad y su tooconfigure de descripción de la salida de su almacén de Data Lake.

<table>
<tbody>
<tr>
<td><B>NOMBRE DE LA PROPIEDAD</B></td>
<td><B>DESCRIPCIÓN</B></td>
</tr>
<tr>
<td>Alias de salida</td>
<td>Se trata de un nombre descriptivo que se usa en consultas toodirect Hola consulta salida toothis almacén de Data Lake.</td>
</tr>
<tr>
<td>Cuenta del Almacén de Data Lake</td>
<td>nombre de Hola de cuenta de almacenamiento de Hola donde va a enviar el resultado. Aparecerá una lista de cuentas de almacén de Data Lake Hola usuario registrado tenga acceso a.</td>
</tr>
<tr>
<td>Patrón de prefijo de la ruta [<I>opcional</I>]</td>
<td>Hola toowrite de ruta de archivo especifican de los archivos dentro de hello cuenta de almacén de Data Lake. <BR>{date}, {time}<BR>Ejemplo 1: carpeta1/registros/{date}/{time}<BR>Ejemplo 2: carpeta1/registros/{date}</td>
</tr>
<tr>
<td>Formato de fecha [<I>opcional</I>]</td>
<td>Si el token de fecha de Hola se usa en la ruta de acceso de prefijo de hello, puede seleccionar formato de fecha de hello en el que se organizan los archivos. Ejemplo: AAAA/MM/DD</td>
</tr>
<tr>
<td>Formato de hora [<I>opcional</I>]</td>
<td>Si el token de tiempo de Hola se usa en la ruta de acceso de prefijo de hello, especifique el formato de hora de hello en el que se organizan los archivos. Actualmente, el valor de hello solo admitido es HH.</td>
</tr>
<tr>
<td>Formato de serialización de eventos</td>
<td>Formato de serialización para los datos de salida. Se admiten JSON, CSV y Avro.</td>
</tr>
<tr>
<td>Codificación</td>
<td>Si el formato CSV o JSON, debe especificarse una codificación. UTF-8 es Hola solo admite el formato de codificación en este momento.</td>
</tr>
<tr>
<td>Delimitador</td>
<td>Solo se aplica para la serialización de CSV. Análisis de transmisiones admite un número de delimitadores comunes para la serialización de datos CSV. Los valores admitidos son la coma, punto y coma, espacio, tabulador y barra vertical.</td>
</tr>
<tr>
<td>Formato</td>
<td>Solo se aplica para la serialización de JSON. Separados por líneas Especifica que la salida de hello se formateará haciendo que cada objeto JSON separado por una nueva línea. Matriz especifica que la salida de hello se formateará como una matriz de objetos JSON.</td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a>Renovación de la autorización del Almacén de Data Lake
Actualmente, hay una limitación donde el token de autenticación de hello necesita toobe actualizar manualmente cada 90 días para todos los trabajos con salida de almacén de Data Lake. También necesitará toore-autenticar la cuenta de almacén de Data Lake si ha cambiado la contraseña ya que el trabajo se creó o autenticado por última vez. Un síntoma de este problema es ninguna salida de trabajo y un error en los registros de operaciones de Hola que indica la necesidad de autorización nuevo.

tooresolve este problema, detenga el trabajo en ejecución y vaya tooyour almacén de Data Lake de salida. Haga clic en el vínculo de "Autorización Renew" Hola y durante un breve tiempo una página mostrará que indica "Redirigir tooauthorization..". página de Hola se cerrará automáticamente y si se realiza correctamente, se indicará "Autorización renovada correctamente". A continuación, necesita tooclick "Guardar" final Hola de página de Hola y puede continuar, reinicie el trabajo de hello pérdida de datos de tooavoid de última hora de detención.

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

