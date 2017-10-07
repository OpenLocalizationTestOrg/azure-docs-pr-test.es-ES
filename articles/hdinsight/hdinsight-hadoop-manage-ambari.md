---
title: aaaMonitor y administrar mediante la interfaz de usuario de Ambari Web de HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Ambari toomonitor y administrar clústeres de HDInsight basados en Linux. En este documento, aprenderá cómo clústeres toouse hello Ambari de interfaz de usuario Web incluido con HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a>Administrar clústeres de HDInsight con Ambari Web UI Hola

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Apache Ambari simplifica la administración de Hola y supervisión de un clúster de Hadoop proporcionando fácil toouse web API de REST y de interfaz de usuario. Ambari se incluye en clústeres de HDInsight basados en Linux y es usado toomonitor Hola clúster y realizar cambios de configuración.

En este documento, aprenderá cómo toouse Hola Ambari Web UI con un clúster de HDInsight.

## <a id="whatis"></a> ¿Qué es Ambari?

[Apache Ambari](http://ambari.apache.org) simplifica la administración de Hadoop al proporcionar una interfaz de usuario de web fácil de usar. Puede usar Ambari para crear, administrar y supervisar clústeres de Hadoop. Los desarrolladores pueden integrar estas capacidades en sus aplicaciones mediante el uso de hello [API de REST de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Hola Ambari Web UI se proporciona de forma predeterminada con los clústeres de HDInsight que usan el sistema operativo de Linux de Hola.

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). 

## <a name="connectivity"></a>Conectividad

Hola interfaz de usuario de Ambari Web está disponible en el clúster de HDInsight en HTTPS://CLUSTERNAME.azurehdidnsight.net, donde **CLUSTERNAME** es Hola nombre del clúster.

> [!IMPORTANT]
> Conexión tooAmbari en HDInsight requiere HTTPS. Cuando se le solicite para la autenticación, utilice nombre de cuenta de administrador de Hola y la contraseña que proporcionó cuando se creó el clúster de Hola.

## <a name="ssh-tunnel-proxy"></a>Túnel SSH (proxy)

Mientras Ambari para el clúster es accesible directamente a través de Internet de hello, algunos vínculos de hello Ambari la interfaz de usuario de Web (por ejemplo, toohello JobTracker) no se exponen en Hola internet. tooaccess estos servicios, debe crear un túnel SSH. Para más información, consulte el documento [Uso de un túnel SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).

## <a name="ambari-web-ui"></a>Interfaz de usuario web de Ambari

Cuando se conecte toohello Ambari Web UI, son tooauthenticate solicitadas toohello página. Usar usuario de administrador de clúster de hello (el valor predeterminado es administrador) y la contraseña que usó durante la creación del clúster.

Cuando se abre la página de hello, tenga en cuenta barra hello en la parte superior de Hola. Esta barra contiene los siguientes Hola información y los controles:

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* **Logotipo de Ambari** -panel de Hola se abre, que puede ser usado toomonitor Hola clúster.

* **Operaciones de # nombre de clúster** -muestra el número de Hola de las operaciones en curso de Ambari. Seleccionar nombre de clúster de Hola o **ops #** muestra una lista de operaciones en segundo plano.

* **alertas de #** -muestra las advertencias o alertas críticas, si existe, de clúster de Hola.

* **Panel** -panel de Hola de muestra.

* **Servicios** -configuración de información y configuración de servicios de hello en clúster Hola.

* **Hosts** -información y opciones de configuración para los nodos de hello en clúster de Hola.

* **Alerts** : un registro de información, advertencias y alertas críticas.

* **Administración** -pila/servicios de Software que están instalados en el clúster de hello, información de la cuenta de servicio y la seguridad de Kerberos.

* **Botón Admin** : administración de Ambari, configuración del usuario y cierre de sesión.

## <a name="monitoring"></a>Supervisión

### <a name="alerts"></a>Alertas

Hello siguiente lista contiene Estados de alertas comunes hello usa Ambari:

* **OK (CORRECTO)**
* **Warning (ADVERTENCIA)**
* **CRITICAL (CRÍTICA)**
* **UNKNOWN (DESCONOCIDO)**

Las alertas excepto **Aceptar** provocar hello **alertas #** entrada en la parte superior de Hola Hola toodisplay Hola del número de página de alertas. Al seleccionar esta entrada, muestran las alertas de Hola y su estado.

Las alertas se organizan en varios grupos predeterminados, que pueden verse desde hello **alertas** página.

![página de alertas](./media/hdinsight-hadoop-manage-ambari/alerts.png)

Puede administrar los grupos de hello mediante el uso de hello **acciones** menú y seleccionando **administrar grupos de alerta**.

![administrar cuadro de diálogo de grupos de alertas](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

También puede administrar los métodos de alerta y crear notificaciones de alerta de hello **acciones** menú seleccionando __Administrar notificaciones de alerta__. Se muestran las notificaciones actuales. También puede crear notificaciones desde aquí. Se pueden enviar notificaciones a través de **CORREO ELECTRÓNICO** o **SNMP** cuando se producen combinaciones de alerta/gravedad específicas. Por ejemplo, puede enviar un mensaje de correo electrónico cuando se da alguna de las alertas de Hola Hola **YARN predeterminado** grupo se establece demasiado**crítico**.

![cuadro de diálogo Crear alerta](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

Por último, al seleccionar __Administrar configuración de la alerta__ de hello __acciones__ menú permite un número de hello tooset de veces que debe aparecer una alerta antes de enviar una notificación. Esta configuración puede ser notificaciones tooprevent usado para errores transitorios.

### <a name="cluster"></a>Clúster

Hola **métricas** ficha del panel de hello contiene una serie de widgets que hacen que sea fácil toomonitor estado de hello del clúster de un vistazo. Varios widgets, como **CPU Usage**(Uso de CPU), proporcionan información adicional al hacer clic en ellos.

![panel con métricas](./media/hdinsight-hadoop-manage-ambari/metrics.png)

Hola **Heatmaps** ficha muestra las métricas como color heatmaps, desde la toored verde.

![panel con mapas térmicos](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

Para obtener más información sobre los nodos de hello en clúster de hello, seleccione **Hosts**. A continuación, seleccione el nodo específico de Hola que le interesen.

![detalles del host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a>Services

Hola **servicios** sidebar en el panel de hello proporciona una perspectiva rápida de estado de hello de servicios de Hola que se ejecutan en el clúster de Hola. Varios iconos son utilizados tooindicate estado o las acciones que se deben realizar. Por ejemplo, se muestra un símbolo de reciclaje amarillo si un servicio necesita toobe recicla.

![barra lateral de servicios](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> Servicios de Hello muestra difieren entre las versiones y tipos de clúster de HDInsight. Servicios de Hello mostrados aquí pueden ser diferentes de servicios de Hola que se muestran para el clúster.

Al seleccionar un servicio muestra la información más detallada en el servicio de Hola.

![información de resumen de servicio](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a>Vínculos rápidos

Algunos servicios de mostrar una **vínculos rápidos** vínculo situado en la parte superior de Hola de página de Hola. Esto puede resultar web específicos del servicio de tooaccess usa interfaces de usuario, como:

* **Job History** : el historial de trabajos de MapReduce.
* **Resource Manager** : la interfaz de usuario del administrador de recursos de YARN.
* **NameNode** : la interfaz de usuario de NameNode del Sistema de archivos distribuido de Hadoop (HDFS).
* **Oozie Web UI** : interfaz de usuario de Oozie.

Si se selecciona cualquiera de estos vínculos, abre una nueva pestaña en el explorador, que muestra la página seleccionada Hola.

> [!NOTE]
> Seleccionar hello **vínculos rápidos** entrada para un servicio puede devolver un error "no se encontró el servidor". Si se produce este error, debe usar un túnel SSH al usar hello **vínculos rápidos** entrada para este servicio. Para más información, consulte [Uso de la tunelización SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).

## <a name="management"></a>Administración

### <a name="ambari-users-groups-and-permissions"></a>Usuarios, grupos y permisos de Ambari

Se puede trabajar con usuarios, grupos y permisos cuando se usa un clúster de HDInsight [unido a un dominio](hdinsight-domain-joined-introduction.md). Para obtener información sobre el uso de hello Ambari IU de administración en un clúster Unidos a un dominio, consulte [administrar clústeres de HDInsight Unidos al dominio](hdinsight-domain-joined-introduction.md).

> [!WARNING]
> No se cambie la contraseña de Hola de guardián de hello Ambari (hdinsightwatchdog) en el clúster de HDInsight basados en Linux. Cambiar los saltos de contraseña Hola Hola acciones de script de capacidad toouse o realizar operaciones de escala con el clúster.

### <a name="hosts"></a>Hosts

Hola **Hosts** página enumera todos los hosts en clúster de Hola. toomanage hosts, siga estos pasos.

![página de hosts](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> No se debe agregar, retirar o volver a programar un host con los clústeres de HDInsight.

1. Seleccione un host de Hola que desea toomanage.

2. Hola de uso **acciones** acción de hello tooselect de menú que desea tooperform:

   * **Iniciar todos los componentes** -iniciar todos los componentes en el host de Hola.

   * **Detener todos los componentes** -detener todos los componentes en el host de Hola.

   * **Reinicie todos los componentes** : detener e iniciar todos los componentes de host de Hola.

   * **Activar el modo de mantenimiento** -suprime las alertas para el host de Hola. Este modo se debería habilitar si va a realizar acciones que generan alertas. Por ejemplo, detener e iniciar un servicio.

   * **Desactiva el modo de mantenimiento** -devuelve Hola toonormal las alertas de host.

   * **Detener** -DataNode se detiene o NodeManagers en host Hola.

   * **Iniciar** -inicia DataNode o NodeManagers en host Hola.

   * **Reinicie** -detiene e inicia DataNode o NodeManagers en host Hola.

   * **Retirar** -quita un host de clúster de Hola.

     > [!NOTE]
     > No use esta acción en clústeres de HDInsight.

   * **Recommission** -agrega un clúster de toohello host previamente dado de baja.

     > [!NOTE]
     > No use esta acción en clústeres de HDInsight.

### <a id="service"></a>Servicios

De hello **panel** o **servicios** , utilice hello **acciones** situado en la parte inferior de Hola de lista de hello de servicios toostop e iniciar los servicios.

![Service Actions](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> Mientras **Agregar servicio** aparece en este menú, no debe ser clúster de HDInsight de toohello de servicios de tooadd usado. Se deben agregar nuevos servicios deben mediante una acción de script durante el aprovisionamiento del clúster. Para obtener más información sobre el uso de las acciones de script, consulte [Personalización de clústeres de HDInsight mediante la acción de script](hdinsight-hadoop-customize-cluster-linux.md).

Mientras hello **acciones** botón puede reiniciar todos los servicios, a menudo desea toostart, detener o reiniciar un servicio específico. Use Hola siguientes pasos se tooperform acciones en un servicio individual:

1. De hello **panel** o **Services** , seleccione un servicio.

2. De arriba Hola de hello **resumen** , utilice hello **acciones de servicio** botón y seleccione Hola acción tootake. Esto reinicia el servicio de hello en todos los nodos.

    ![acción de servicio](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > Reiniciar algunos servicios mientras se está ejecutando el clúster de hello puede generar alertas. tooavoid de alertas, puede usar hello **acciones de servicio** botón tooenable **modo de mantenimiento** para servicio de hello antes de realizar el reinicio de Hola.

3. Una vez que se ha seleccionado una acción, Hola **op #** entrada en la parte superior de Hola de hello página incrementos tooshow que está en curso una operación en segundo plano. Si configura toodisplay, se muestra la lista de Hola de operaciones en segundo plano.

   > [!NOTE]
   > Si habilitó **modo de mantenimiento** para el servicio de hello, recuerde toodisable mediante hello **acciones de servicio** botón una vez que haya finalizado la operación de Hola.

tooconfigure un servicio, utilice Hola pasos:

1. De hello **panel** o **Services** , seleccione un servicio.

2. Seleccione hello **configuraciones** muestra la configuración actual de Hola de ficha. También aparecerá una lista de las configuraciones anteriores.

    ![configuraciones](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. Usar configuración de hello toomodify de hello campos que se muestran y, a continuación, seleccione **guardar**. O seleccione una configuración anterior y, a continuación, seleccione **convertir en actual** tooroll realizar copia de toohello de configuración anterior.

## <a name="ambari-views"></a>Vistas de Ambari

Ambari vistas permiten a los desarrolladores tooplug elementos de interfaz de usuario en hello Ambari Web UI con hello [Ambari vistas Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views). HDInsight proporciona Hola siguientes vistas con tipos de clúster de Hadoop:

* Administrador de cola de hilo: Administrador de cola de hello proporciona una interfaz de usuario simple para ver y modificar las colas YARN.

* Vista de Hive: Hola Hive vista permite consultas de Hive toorun directamente desde el explorador web. Puede guardar consultas, ver los resultados, guardar los resultados de almacenamiento del clúster toohello o descargar el sistema local de tooyour de resultados. Para más información sobre el uso de vistas de Hive, consulte [Uso de vistas de Hive con HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).

* La vista Tez: Hola Tez vista permite toobetter entender y optimizar los trabajos. Puede ver información sobre cómo se ejecutan los trabajos de Tez y qué recursos se usan.
