---
title: eventos de aaaCorrelate con el tiempo con Storm y HBase en HDInsight
description: "Obtenga información acerca de cómo toocorrelate eventos que llegan en distintos momentos mediante Storm y HBase en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a>Correlación de eventos que llegan a diferentes horas con Storm y HBase

Si utiliza un almacén de datos persistente con Apache Storm, puede poner en correlación entradas de datos que llegan en distintos momentos. Por ejemplo, la vinculación de eventos de inicio de sesión y cierre de sesión de un toocalculate de sesión de usuario cómo sesión de hello tiempo duró.

En este documento, aprenderá cómo toocreate una topología básica de C# Storm que realiza el seguimiento de eventos de inicio y cierre de sesión para sesiones de usuario y calcula la duración de Hola de sesión de Hola. topología de Hello usa HBase como un almacén de datos persistente. HBase también le permite tooperform de consultas por lotes en la información adicional de hello datos históricos tooproduce. Por ejemplo, la cantidad de sesiones de usuario que se iniciaron o terminaron durante un período de tiempo específico.

## <a name="prerequisites"></a>Requisitos previos

* Visual Studio y hello HDInsight tools para Visual Studio. Para obtener más información, consulte [Introducción al uso de herramientas de HDInsight de Hola para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Apache Storm en clústeres de HDInsight (Windows)

  > [!WARNING]
  > Aunque se admiten topologías SCP.NET en clústeres basados en Linux aluvión creados después de 10/28/2016, hello HBase SDK para el paquete de .NET disponible a partir del 28/10/2016 no funciona correctamente en HDInsight basados en Linux

* Apache HBase en un clúster de HDInsight (basado en Linux o Windows).

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Java](https://java.com) 1.7 o superior en el entorno de desarrollo. Java es toopackage usado Hola topología cuando llega el clúster de HDInsight de toohello enviado.

  * Hola **JAVA_HOME** entorno debe variable punto toohello el directorio que contiene Java.
  * Hola **%JAVA_HOME%/bin** directorio debe estar en la ruta de acceso de Hola

## <a name="architecture"></a>Arquitectura

![Diagrama de flujo de datos de Hola a través de la topología de Hola](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

Correlacionar eventos requiere un identificador común para el origen del evento de Hola. Por ejemplo, un identificador de usuario, Id. de sesión u otro dispositivo de datos que sea un) único y b) incluidos en tooStorm de todos los datos enviados. Este ejemplo utiliza un toorepresent de valor GUID un identificador de sesión.

Este ejemplo consta de dos clústeres de HDInsight:

* HBase: almacén de datos persistente para los datos históricos
* Storm: utilizar los datos entrantes tooingest

Hello datos generados aleatoriamente por topología aluvión de Hola y consta de hello siguientes elementos:

* Id. de sesión: un GUID que identifica de forma única cada sesión
* Evento: evento de INICIO o FINALIZACIÓN. En este ejemplo, INICIO siempre tiene lugar antes de la FINALIZACIÓN
* : Hola: hora del evento Hola.

Estos datos se procesan y almacenan en HBase.

### <a name="storm-topology"></a>Topología de Storm

Cuando se inicia una sesión, un **iniciar** evento recibe topología hello y registra tooHBase. Cuando un **final** recibe el evento, la topología de hello recupera hello **iniciar** eventos y calcula el tiempo de hello entre eventos de hello dos. Esto **duración** valor, a continuación, se almacena en HBase junto con hello **final** información del evento.

> [!IMPORTANT]
> Mientras esta topología muestra el patrón básico de hello, una solución de producción necesitaría tootake diseño para hello los escenarios siguientes:
>
> * Eventos que llegan sin orden
> * Eventos duplicados
> * Eventos quitados

topología de ejemplo de Hola se compone de Hola de los componentes siguientes:

* Session.cs: simula una sesión de usuario mediante la creación de un identificador de sesión aleatorio, inicio Hola de tiempo y el tiempo de sesión dura.

* Spout.cs: crea 100 sesiones, emite un evento de inicio, espera el tiempo de espera aleatorio de Hola para cada sesión y, a continuación, emite un evento de fin. A continuación, recicla finalizó sesiones toogenerate nuevos.

* HBaseLookupBolt.cs: usa toolook de Id. de sesión de hello información de sesión de HBase. Cuando se procesa un evento de fin, busca los eventos de inicio correspondiente de Hola y calcula la duración de Hola de sesión de Hola.

* HBaseBolt.cs: almacena información en HBase.

* TypeHelper.cs: Ayuda con la conversión de tipos al leer / escribir tooHBase.

### <a name="hbase-schema"></a>Esquema de HBase

En HBase, datos de Hola se almacenan en una tabla con hello después de esquema y configuración:

* Clave de fila: Hola identificador de sesión es utilizado como clave de Hola para las filas de esta tabla.

* Familia de columna: nombre de familia de hello es 'cf'. Las columnas almacenadas en esta familia son:

  * evento: INICIO o FINALIZACIÓN.

  * tiempo: tiempo de hello en milisegundos que Hola evento se ha producido.

  * duración: Hola longitud entre eventos de inicio y finalización.

* Las versiones: familia de hello 'cf' se establece tooretain 5 versiones de cada fila.

  > [!NOTE]
  > Las versiones son un registro de los valores anteriores almacenados para una clave de fila específica. De forma predeterminada, HBase sólo devuelve valor hello para la versión más reciente de Hola de una fila. En este caso, hello misma fila se utiliza para todos los eventos (inicio, fin.) de que cada versión de una fila se identifica mediante el valor de marca de tiempo de Hola. Las versiones proporcionan una vista histórica de los eventos registrados para un identificador concreto.

## <a name="download-hello-project"></a>Descargar proyecto Hola

proyecto de ejemplo de Hola puede descargarse desde [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).

Esta descarga contiene Hola después de proyectos de C#:

* CorrelationTopology: topología de Storm de C# que emite aleatoriamente eventos de inicio y finalización para las sesiones de usuario. Cada sesión dura entre 1 y 5 minutos.

* SessionInfo: C# aplicación de consola que crea la tabla HBase de Hola y proporciona consultas de ejemplo tooreturn información acerca de los datos de sesión almacenada.

## <a name="create-hello-table"></a>Crear tabla de Hola

1. Abra hello **SessionInfo** proyecto en Visual Studio.

2. En **el Explorador de soluciones**, contextual hello **SessionInfo** de proyecto y seleccione **propiedades**.

    ![Captura de pantalla del menú con propiedades seleccionadas](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. Seleccione **configuración**, a continuación, después de hello de conjunto de valores:

   * HBaseClusterURL: clúster de HBase de tooyour de dirección URL Hola. Por ejemplo, https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: cuenta de usuario de administrador/HTTP hello para el clúster

   * HBaseClusterPassword: contraseña Hola de cuenta de usuario de administrador/HTTP Hola

   * HBaseTableName: nombre Hola de hello tabla toouse con este ejemplo

   * HBaseTableColumnFamily: nombre de familia de columna hello

     ![Imagen del cuadro de diálogo de configuración](./media/hdinsight-storm-correlation-topology/settings.png)

4. Ejecutar soluciones de Hola. Cuando se le pida, seleccione tabla de hello 'c' toocreate clave hello en el clúster de HBase.

## <a name="build-and-deploy-hello-storm-topology"></a>Compilar e implementar la topología de Storm Hola

1. Abra hello **CorrelationTopology** solución en Visual Studio.

2. En **el Explorador de soluciones**, contextual hello **CorrelationTopology** del proyecto y seleccione Propiedades.

3. En la ventana de propiedades de hello, seleccione **configuración** y escriba los valores de configuración de Hola para este proyecto. Hello 5 primeros son Hola mismos valores usan por hello **SessionInfo** proyecto:

   * HBaseClusterURL: clúster de HBase de tooyour de dirección URL Hola. Por ejemplo, https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: cuenta de usuario Hola admin/HTTP para el clúster.

   * HBaseClusterPassword: la contraseña de Hola de cuenta de usuario de administrador/HTTP Hola.

   * HBaseTableName: nombre de Hola de hello tabla toouse con este ejemplo. Este valor es Hola mismo nombre de la tabla como se utiliza en el proyecto de SessionInfo Hola.

   * HBaseTableColumnFamily: nombre de familia Hola columna. Este valor es Hola mismo nombre de familia de la columna tal y como se usan en hello SessionInfo proyecto.

   > [!IMPORTANT]
   > No cambie hello HBaseTableColumnNames, tal y como valores predeterminados de hello son nombres Hola utilizados por **SessionInfo** tooretrieve datos.

4. Guardar las propiedades de hello, a continuación, compile el proyecto de Hola.

5. En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **enviar tooStorm en HDInsight**. Si se le pide, escriba credenciales de hello para la suscripción de Azure.

   ![Imagen del programa Hola a enviar el elemento de menú toostorm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. Hola **topología enviar** cuadro de diálogo, clúster de Storm Hola seleccione desea toodeploy esta topología.

   > [!NOTE]
   > Hello primera vez que envíe una topología, puede tardar unos segundos nombre de hello tooretrieve los clústeres de HDInsight.

7. Una vez topología Hola clúster toohello cargados y enviados, Hola **aluvión de la vista de topología** se abre y muestra hello ejecutando topología. datos de hello toorefresh, seleccione hello **CorrelationTopology** y use el botón de actualización de hello en hello parte superior derecha de la página de Hola.

   ![Imagen de la vista de topología de Hola](./media/hdinsight-storm-correlation-topology/topologyview.png)

   Cuando la topología de hello comienza generar datos, Hola valor Hola **emitida** incrementos de columna.

   > [!NOTE]
   > Si hello **vista de topología de Storm** no se abre automáticamente, use Hola siguientes tooopen de pasos:
   >
   > 1. Desde el **Explorador de soluciones**, expanda **Azure** y **HDInsight**.
   > 2. Clúster de Storm Hola de menú contextual que Hola topología se ejecutan en y, a continuación, seleccione **vista aluvión de topologías**

## <a name="query-hello-data"></a>Consultar datos de Hola

Una vez que se ha emitido los datos, utilice Hola seguir los pasos tooquery Hola datos.

1. Devolver toohello **SessionInfo** proyecto. Si no está ejecutando, inicie una nueva instancia de este.

2. Cuando se le pida, seleccione **s** toosearch para eventos de inicio. Está tooenter solicitada un inicio y finalización tiempo toodefine un intervalo de tiempo - se devuelven sólo los eventos entre estos dos veces.

    Dar formato al escribir inicio Hola siguiente Hola de uso y de finalización: hh: mm y 'm' o 'CP'. Por ejemplo, 11:20 pm.

    tooreturn registran eventos, use una hora de inicio de antes de hello aluvión de topología implementó y una hora de finalización de ahora. datos de valor devuelto de Hello contienen entradas toohello similar siguiente texto:

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

Buscando Hola de final eventos funciona igual como eventos de inicio. Sin embargo, los eventos de fin se generan aleatoriamente entre 1 y 5 minutos después de evento de inicio de Hola. Puede que tenga tootry eventos de fin de hello toofind de intervalos de tiempo unos. Eventos de fin también contienen durante Hola Hola sesión - diferencia Hola entre la hora del evento de inicio de Hola y hora de finalización del evento. Este es un ejemplo de datos de eventos de FINALIZACIÓN:

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> Aunque son valores de tiempo de Hola que especifica en hora local, hora de hello procedente de la consulta de hello está en UTC.

## <a name="stop-hello-topology"></a>Detener la topología de Hola

Cuando esté listo toostop topología de hello, devolver toohello **CorrelationTopology** proyecto en Visual Studio. Hola **vista de topología de Storm**, seleccione la topología de hello y, a continuación, usar hello **Kill** situado en la parte superior de Hola de vista de topología de Hola.

## <a name="delete-your-cluster"></a>Eliminación del clúster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Pasos siguientes

Para obtener más ejemplos de Storm, vea [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).
