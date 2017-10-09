---
title: "Guía de aaaTroubleshooting para análisis de transmisiones de Azure | Documentos de Microsoft"
description: "Cómo tootroubleshoot su trabajo de análisis de transmisiones"
keywords: "guía de solución de problemas"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Guía de solución de problemas de Azure Stream Analytics

Solución de problemas de análisis de transmisiones Azure puede aparecer toobe muy trabajoso a primera vista. Después de trabajar con muchos usuarios, se ha creado este proceso de hello guía toohelp optimizada y eliminen Hola suposiciones acerca de las funciones, las consultas, salidas y entradas.

## <a name="troubleshoot-your-stream-analytics-job"></a>Solución de problemas de los trabajos de Stream Analytics

Para obtener mejores resultados en el trabajo de análisis de transmisiones de solución de problemas, use Hola siguientes instrucciones:

1.  Pruebe la conectividad:
    - Comprobar conectividad tooinputs y salidas mediante hello **Probar conexión** botón para cada entrada y salida.

2.  Examine los datos de entrada:
    - tooverify que los datos de entrada está fluyendo en Centro de eventos, use [Explorador de Service Bus](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure concentrador de eventos (si se usa la entrada de concentrador de eventos).  
    - Hola de uso [ **datos de ejemplo** ](stream-analytics-sample-data-input.md) botón para cada entrada y descargar datos de entrada de ejemplo de Hola.
    - Inspeccionar Hola ejemplo datos toounderstand Hola de forma de datos de hello: Hola hello y esquema [tipos de datos](https://msdn.microsoft.com/library/azure/dn835065.aspx).

3.  Pruebe la consulta:
    - En hello **consulta** , utilice hello **probar** botón consulta de hello tootest y utilizar datos de ejemplo de Hola descargado demasiado[prueba Hola consulta](stream-analytics-test-query.md). Examinar los errores e intente toocorrect ellos.
    - Si usa [ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), compruebe que los eventos de hello tienen marcas de tiempo mayor de hello [hora de inicio del trabajo](stream-analytics-out-of-order-and-late-events.md).

4.  Depure la consulta:
    - Vuelva a generar consultas Hola progresivamente de agregados de instrucción select simple toomore complejos mediante el uso de pasos. toobuild la lógica de la consulta de hello paso a paso, utilice [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) cláusulas.
    - Use [SELECT INTO](stream-analytics-select-into.md) toodebug pasos de consulta.

5.  Elimine los errores comunes, como:
    - A [ **donde** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) cláusula de consulta de hello filtra todos los eventos, impide que se genera ningún resultado.
    - Cuando se utilizan funciones de ventana, esperan toosee de duración de ventana en su totalidad Hola un resultado de consulta de Hola.
    - marca de tiempo de Hola para eventos precede a la hora de inicio del trabajo de hello y, por lo tanto, se quitan los eventos.

6.  Use la ordenación de eventos:
    - Si todos los hello pasos anteriores funcionados bien, vaya toohello **configuración** hoja y seleccione [ **orden de los eventos**](stream-analytics-out-of-order-and-late-events.md). Compruebe que esta directiva está configurada de acuerdo con su escenario. Hola directiva es *no* aplican cuando se utiliza hello **prueba** consulta de botón tootest Hola. El resultado es una diferencia entre pruebas en explorador frente a ejecutar trabajo de hello en producción.

7.  Depure mediante métricas:
    - Si no obtiene ningún resultado después de hello espera duración (basado en consulta hello), intente Hola siguiente:
        - Mire [ **métricas** ](stream-analytics-monitoring.md) en hello **Monitor** ficha. Dado que se agregan los valores de hello, las métricas de Hola se retrasan por unos minutos.
            - Si los eventos de entrada > 0, trabajo hello es capaz de tooread datos de entrada. Si Eventos de entrada no es > 0, entonces:
                - toosee si el origen de datos de hello tiene datos válidos, protegerlo mediante el uso de [Explorador de Service Bus](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a). Esta comprobación se aplica si el trabajo de hello usa concentrador de eventos como entrada.
                - Compruebe toosee si el formato de serialización de datos de Hola y codificación de datos son los esperados.
                - Si el trabajo de hello es mediante un concentrador de eventos, compruebe toosee si Hola cuerpo del mensaje de bienvenida es *Null*.
            - Si los errores de conversión de datos > 0 y aumente, podría darse siguiente hello:
                - trabajo de Hello podría no ser capaz de toode-serializar eventos Hola.
                - Hello esquema de eventos podría no coincidir con hello definido o esquema esperado de eventos de hello en consulta Hola.
                - Hola tipos de datos de algunos de los campos de hello en caso de hello podrían no coincidir con las expectativas.
            - Si los errores en tiempo de ejecución > 0, significa que el trabajo de hello puede recibir datos de hello pero genera errores durante el procesamiento de consultas de Hola.
                - errores de hello toofind, vaya toohello [los registros de auditoría](../azure-resource-manager/resource-group-audit.md) y filtrar por *error* estado.
            - Si InputEvents > 0 y OutputEvents = 0, significa que uno de hello siguientes es cierta:
                - El procesamiento de consultas no ha generado ningún evento de salida.
                - Los eventos o sus campos pueden tener un formato incorrecto, por lo que no se genera ninguna salida después de procesar la consulta.
                - trabajo de Hello era toohello de datos no se puede toopush [receptor de salida](stream-analytics-select-into.md) por motivos de conectividad o autenticación.
        - Hola todos los mencionados anteriormente casos de error, las operaciones de mensajes de registro explican detalles adicionales (incluidos lo que está sucediendo), excepto en casos donde la lógica de consulta Hola filtra todos los eventos. Si el procesamiento de Hola de varios eventos genera errores, registros de análisis de transmisiones registros Hola en primer lugar tres mensajes de error del programa Hola a mismo tipo dentro de 10 minutos tooOperations. Luego, suprime los errores idénticos adicionales con un mensaje que dice "Los errores se producen demasiado rápido y se están suprimiendo".

8. Depure mediante auditorías y registros de diagnóstico:
    - Use [los registros de auditoría](../azure-resource-manager/resource-group-audit.md)y errores del filtro de tooidentify y de depuración.
    - Use [registros de diagnóstico de trabajo](stream-analytics-job-diagnostic-logs.md) tooidentify y depuración de errores.

9. Examine Hola salidas:
    - Cuando el estado del trabajo de hello es *ejecuta*, en función de la duración de Hola que estipulada en consulta hello, puede ver la salida de hello en el origen de datos del receptor de Hola.
    - Si no ve resultados que se van tooa resultados específicos tipo, redirigirá tooan tipo de salida que es menos complejo, como un Blob de Azure. Mediante el Explorador de almacenamiento, compruebe toosee si se puede ver la salida de hello. Además, compruebe si los límites de limitación en la salida de hello impiden datos desde la que se reciben.

10. Use el análisis de flujo de datos con las métricas de diagrama de trabajo:
    - flujo de datos de tooanalyze e identifican los problemas, use hello [diagrama de trabajo con métricas](stream-analytics-job-diagram-with-metrics.md).

11. Abra un caso de soporte técnico:
    - Por último, si se produce un error en todo lo demás, abrir un caso de soporte técnico de Microsoft mediante Hola Id. de suscripción que contiene el trabajo.

## <a name="get-help"></a>Obtener ayuda

Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes

* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
