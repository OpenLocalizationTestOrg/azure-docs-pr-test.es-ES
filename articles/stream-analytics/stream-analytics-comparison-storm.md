---
title: "Plataformas de análisis: Apache Storm comparación tooStream análisis | Documentos de Microsoft"
description: "Obtenga información orientativa elegir una plataforma de análisis en la nube mediante el uso de un tooStream de comparación de Apache Storm análisis. Comprenda las características y diferencias."
keywords: "plataforma de análisis, plataformas de análisis, plataforma de análisis de la nube, comparación de storm"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a>Elección de una plataforma de Stream Analytics: comparación de Apache Storm con Azure Stream Analytics
Azure ofrece varias soluciones para analizar datos de streaming: [Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/) y [Apache Storm en HDInsight de Azure](https://azure.microsoft.com/services/hdinsight/apache-storm/). Ambas plataformas de análisis ofrecen ventajas de Hola de una solución de PaaS. Pero Hola plataformas cuentan con algunas diferencias significativas en sus capacidades, así como en cómo configurar y administrarlos. 

Este artículo proporciona una comparación en paralelo de toohelp características que elija entre Apache Storm y análisis de transmisiones de Azure como una plataforma de análisis en la nube. 

## <a name="general-features"></a>Características generales

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong></strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm en HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>¿Código abierto?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
No. Azure Stream Analytics es una oferta propiedad de Microsoft.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Sí. Apache Storm es una tecnología con licencia de Apache.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>¿Soporte técnico de Microsoft?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Sí </p>
            </td>
            <td width="246" valign="top">
                <p>
Sí </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Requisitos de hardware</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Ninguno. Análisis de transmisiones de Azure es un servicio de Azure.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Ninguno. Apache Storm es un servicio de Azure.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Unidad de nivel superior</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Los usuarios implementan y supervisan trabajos de streaming.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Los usuarios implementan y supervisan todo un clúster, que puede hospedar varios trabajos de Storm y otras cargas de trabajo (de Batch incluidas).
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Precios</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Precio por volumen de datos procesados y Hola número de unidades de streaming necesario por hora que Hola trabajo se está ejecutando. 
                </p>
                    <p>Para más información, vea los <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">precios de Stream Analytics</a>.</p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
unidad de Hola de compra está basado en el clúster y se cobra puntualmente Hola Hola clúster se está ejecutando, independientemente de los trabajos que se implementa.
                </p>
                <p>
Para más información, vea los <a href="http://azure.microsoft.com/pricing/details/hdinsight/">precios de HDInsight</a>.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a>Creación

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong></strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm en HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>¿Funcionalidades: SQL DSL?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Sí. Stream Analytics ofrece un lenguaje de tipo SQL para crear las transformaciones.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
No. Los usuarios escriben el código en Java o C# o usan las API de Trident.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>¿Funcionalidades: operadores temporales?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Compatible de manera predeterminada con agregados de ventana y uniones temporales.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Deben implementarse operadores temporales por usuario de Hola.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Experiencia de desarrollo</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Los usuarios pueden crear, depurar y supervisar trabajos a través del portal de Azure, hello mediante datos de ejemplo que se deriva de una secuencia en directo.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Los usuarios que utilizan .NET pueden desarrollar, depurar y supervisar a través de Visual Studio. Los usuarios con Java u otros lenguajes pueden usar Hola IDE de su elección.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Compatibilidad con la depuración</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Registros de estado y las operaciones básicas de trabajo son depuración toohelp disponible. Análisis de transmisiones actualmente no permiten a los usuarios especificar el contenido o la cantidad de contenido se incluye en los registros de hello (es decir, el modo detallado).
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Hay registros detallados disponibles. Los usuarios pueden obtener acceso a registros en Visual Studio o iniciando sesión en el clúster toohello y tener acceso directamente a los registros de Hola.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>¿Extensibilidad con código personalizado?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Se admite parcialmente con UDF de JavaScript. Para más información, vea <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">Integración de UDF de JavaScript</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Sí. Los usuarios pueden escribir código personalizado en C#, Java o en cualquier otro lenguaje compatible con Storm.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a>Orígenes de datos (entradas) y salidas ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong></strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm en HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                 <strong>Orígenes de datos de entrada</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>Azure Event Hubs y Azure Blob Storage.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Hay conectores disponibles para Azure Event Hubs, Azure Service Bus, Kafka y otros más. Los usuarios pueden crear conectores adicionales con código personalizado.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Formatos de datos de entrada</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Avro, JSON y CSV </p>
            </td>
            <td width="246" valign="top">
                <p>
Los usuarios pueden implementar cualquier formato mediante código personalizado.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Salidas</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Un trabajo de streaming puede tener varias salidas. Las salidas compatibles son Azure Event Hubs, Azure Blob Storage, Azure Table Storage, Azure SQL DB y Power BI.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Storm admite muchas salidas en una topología y cada una puede tener una lógica personalizada para el procesamiento de bajada. Storm incluye conectores para Power BI, Azure Event Hubs, Azure Blob Storage, Azure Cosmos DB, SQL y HBase. Los usuarios pueden crear conectores adicionales con código personalizado.    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Formatos de codificación de datos</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Los datos deben tener formato UTF-8.
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
Los usuarios pueden implementar cualquier formato de codificación de datos mediante código personalizado.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a>Administración y operaciones ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong></strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm en HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Modelo de implementación del trabajo</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Azure Portal, PowerShell y las API de REST.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Azure Portal, PowerShell, Visual Studio y las API de REST.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Supervisión (estadísticas, contadores, etc.)</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
La supervisión se implementa mediante Azure Portal y las API de REST. Los usuarios también pueden configurar alertas de Azure.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Supervisión se implementa mediante hello aluvión de interfaz de usuario y las API de REST.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Escalabilidad</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Escalabilidad viene determinada por el número de Hola de Streaming Units (SUs) para cada trabajo. Cada unidad de transmisión por secuencias se procesa la too1 MB/segundo, con un máximo de 50 unidades. Para obtener más información, consulte <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">rendimiento tooincrease de escala</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Escalabilidad se determina mediante el número de nodos de clúster de HDInsight Storm Hola Hola. límite superior de Hello en número de Hola de nodos se define por la cuota de Azure del usuario de Hola.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Límites de procesamiento de datos</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Los usuarios pueden aumentar el procesamiento de datos u optimizar los costos aumentando o reduciendo el número de Hola de unidades de Streaming, con un límite de 1 GB/segundo.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Los usuarios pueden escalar o reducir verticalmente el tamaño del clúster.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Detener o reanudar</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Puede detenerlo y reanudarlo en el punto donde lo detuvo.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Se puede detener y reanudar en el punto donde se detuvo en función de la marca de agua.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Actualización de servicio y marco</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Revisión automática sin tiempo de inactividad.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Revisión automática sin tiempo de inactividad.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Continuidad empresarial mediante un servicio de alta disponibilidad con acuerdos de nivel de servicio garantizados</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li>Contrato de nivel de servicio con un tiempo de actividad del 99,9%</li>
                <li>Recuperación automática de errores</li>
                <li>Recuperación integrada de los operadores temporales con estado.</li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
SLA de tiempo de actividad del 99,9% de clúster de Storm Hola. 
                </p>
                <p>
Apache Storm es una plataforma de streaming con tolerancia a errores. Sin embargo, resulta tooensure de responsabilidad del usuario de Hola que streaming ejecutan los trabajos sin interrupciones.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a>Características avanzadas ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong></strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm en HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Control de eventos desordenados y llegada tardía</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Directivas configurables integradas pueden reordenar los eventos, quitar eventos o ajustar la hora del evento.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Los usuarios deben implementar lógica toohandle este escenario.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Datos de referencia</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Hay datos de referencia disponibles de Azure Blob Storage con un máximo de 100 MB de caché en memoria. Datos de referencia se actualizan por servicio Hola.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Sin límites en el tamaño de los datos. Hay conectores disponibles para HBase, Azure Cosmos DB, SQL Server y Azure. Los usuarios pueden crear conectores adicionales con código personalizado. Los datos de referencia deben actualizarse con código personalizado.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Integración con Machine Learning</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Los modelos de Azure Machine Learning publicados se pueden configurar a modo de funciones durante la creación del trabajo. Para más información, vea <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Escalado con funciones de Machine Learning</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Disponible a través de Storm Bolts.
                </p>
            </td>
        </tr>
    </tbody>
</table>
