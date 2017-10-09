---
title: aaaHadoop componentes y las versiones - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de componentes de Hadoop de Hola y versiones de hello y HDInsight niveles de servicio disponibles en esta distribución de nube de Hortonworks Data Platform."
keywords: "versiones de hadoop, componentes del ecosistema de hadoop, componentes de hadoop, la versión de hadoop de toocheck"
services: hdinsight
editor: cgronlun
manager: asadk
author: bprakash
tags: azure-portal
documentationcenter: 
ms.assetid: 367b3f4a-f7d3-4e59-abd0-5dc59576f1ff
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: bprakash
ms.openlocfilehash: b661d901b0113458c3501ec06454fc8841189672
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-hadoop-components-and-versions-available-with-hdinsight"></a>¿Cuáles son los componentes de Hadoop de Hola y de versiones disponibles con HDInsight?

Obtenga información acerca de los componentes de hello Apache Hadoop ecosistema y versiones de Microsoft Azure HDInsight, así como Hola niveles de servicio estándar y Premium. Además, obtenga información acerca de cómo toocheck versiones de componentes de Hadoop en HDInsight. 

Cada versión de HDInsight es una distribución de nube de una versión de Hortonworks Data Platform (HDP).

## <a name="hadoop-components-available-with-different-hdinsight-versions"></a>Componentes de Hadoop disponibles con las distintas versiones de HDInsight
HDInsight de Azure es compatible con varias versiones de clústeres de Hadoop que se pueden implementar en cualquier momento. Cada opción de versión crea una versión específica de la distribución de HDP hello y un conjunto de componentes que están dentro de la distribución. A partir de 17 de febrero de 2017, versión de clúster de hello predeterminada utilizada por HDInsight de Azure es 3.5 y se basa en HDP 2.5.

en hello en la tabla siguiente se enumeran las versiones del componente Hola asociadas con las versiones del clúster de HDInsight. 

> [!NOTE]
> versión predeterminada de Hola para hello servicio HDInsight puede cambiar sin previo aviso. Si tiene una dependencia de la versión, especificar versión de HDInsight de hello al crear los clústeres con hello SDK para .NET con Azure PowerShell y la CLI de Azure.

| Componente | HDInsight 3.6 (predeterminado) | HDInsight 3.5 | HDInsight 3.4 | HDInsight 3.3 | HDInsight 3.2 | HDInsight 3.1 | HDInsight 3.0 |
| --- | --- | --- | --- | --- | --- | --- |--- |
| Hortonworks Data Platform |2.6 |2.5 |2.4 |2.3 |2.2 |2.1.7 |2.0 |
| Apache Hadoop y YARN |2.7.3 |2.7.3 |2.7.1 |2.7.1 |2.6.0 |2.4.0 |2.2.0 |
| Apache Tez |0.7.0 |0.7.0 |0.7.0 |0.7.0 |0.5.2 |0.4.0 |-|
| Apache Pig |0.16.0 |0.16.0 |0.15.0 |0.15.0 |0.14.0 |0.12.1 |0.12.0 |
| Apache Hive y HCatalog |1.2.1 |1.2.1 |1.2.1 |1.2.1 |0.14.0 |0.13.1 |0.12.0 |
| Apache Hive2 | 2.1.0 |-|-|-|-|-|-|
| Apache Tez Hive2 | 0.8.4 |-|-|-|-|-|-|
| Apache Ranger | 0.7.0 |0.6.0 |-|-|-|-|-|
| HBase Apache |1.1.2 |1.1.2 |1.1.2 |1.1.1 |0.98.4 |0.98.0 |-|
| Apache Sqoop |1.4.6 |1.4.6 |1.4.6 |1.4.6 |1.4.5 |1.4.4 |1.4.4 |
| Apache Oozie |4.2.0 |4.2.0 |4.2.0 |4.2.0 |4.1.0 |4.0.0 |4.0.0 |
| Apache Zookeeper |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.5 |3.4.5 |
| Apache Storm |1.1.0 |1.0.1 |0.10.0 |0.10.0 |0.9.3 |0.9.1 |-|
| Apache Mahout |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0 |0.9.0 |-|
| Apache Phoenix |4.7.0 |4.7.0 |4.4.0 |4.4.0 |4.2.0 |4.0.0.2.1.7.0-2162 |-|
| Spark de Apache |2.1.0 (solo Linux) |1.6.2 y 2.0 (solo Linux) |1.6.0 (solo Linux) |1.5.2 (solo la compilación experimental de Linux) |1.3.1 (solo Windows) |-|-|
| Apache Kafka | 0.10.0 | 0.10.0 | 0.9.0 |-|-|-|-|
| Apache Ambari | 2.5.0 | 2.4.0 | 2.2.1 | 2.1.0 |-|-|-|
| Apache Zeppelin | 0.7.0 |-|-|-|-|-|-|
| Mono |4.2.1 |4.2.1 |3.2.8 |-|-|-|

## <a name="check-for-current-hadoop-component-version-information"></a>Comprobación de la información de la versión de los componentes actuales de Hadoop

versiones de componentes del ecosistema de Hadoop de Hello asociadas con las versiones del clúster de HDInsight pueden cambiar con actualizaciones tooHDInsight. componentes de Hadoop de toocheck hello y tooverify qué versiones se utilizan para un clúster, use Hola API de REST de Ambari. Hola **GetComponentInformation** comando recupera información acerca de los componentes de servicio. Para obtener más información, vea hello [Ambari documentación][ambari-docs].

Para los clústeres de Windows, versión del componente de Hola de toocheck de otra manera es toolog tooa clúster mediante Escritorio remoto y examinar hello del directorio de hello C:\apps\dist\.

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o una versión posterior. Para más información, vea [Windows retirement on HDInsight](#hdinsight-windows-retirement) (Retirada de Windows en HDInsight).

### <a name="release-notes"></a>Notas de la versión

Vea [notas de la versión de HDInsight](hdinsight-release-notes.md) de notas de la versión adicionales en las versiones más recientes de Hola de HDInsight.

## <a name="supported-hdinsight-versions"></a>Versiones compatibles de HDInsight
Hello siguiente tabla enumera las versiones de Hola de HDInsight que están actualmente disponibles en hello portal de Azure. versiones HDP Hola correspondientes de la versión de HDInsight de tooeach se muestran junto con las fechas de lanzamiento de producto de Hola. También se proporcionan fechas de expiración y la retirada de soporte técnico de Hello, al que se conocen.

> [!NOTE]
> Después de soporte técnico para una versión ha caducado, no estén disponible a través del portal clásico de hello Microsoft Azure. Sin embargo, las versiones de clúster siguen toobe disponible con hello `Version` parámetro en Windows PowerShell hello [AzureRmHDInsightCluster New](https://msdn.microsoft.com/library/mt619331.aspx) comando y Hola .NET SDK hasta que la versión de Hola fecha de retirada.
> 
> Los clústeres de alta disponibilidad con dos nodos principales se implementan de forma predeterminada para los clústeres de HDInsight 2.1 y versiones posteriores. No están disponibles para los clústeres de HDInsight 1.6.

| Versión de HDInsight | Versión de HDP | SISTEMA OPERATIVO DE LA MÁQUINA VIRTUAL | Alta disponibilidad | Fecha de lanzamiento | Disponibilidad en hello portal de Azure | Fecha de expiración del soporte técnico | Fecha de retirada |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HDInsight 3.6 |HDP 2.6 |Ubuntu 16 |Sí |4 de abril de 2017 |Sí | | |
| HDInsight 3.5 |HDP 2.5 |Ubuntu 16 |Sí |30 de septiembre de 2016 |Sí |5 de septiembre de 2017 |31 de mayo de 2018 |
| HDInsight 3.4 |HDP 2.4 |Ubuntu 14.0.4 LTS |Sí |29 de marzo de 2016 |Sí |29 de diciembre de 2016 |9 de enero de 2018 |
| HDInsight 3.3 |HDP 2.3 |Windows Server 2012 R2 |Sí |2 de diciembre de 2015 |Sí |27 de junio de 2016 |31 de julio de 2018 |
| HDInsight 3.3 |HDP 2.3 |Ubuntu 14.0.4 LTS |Sí |2 de diciembre de 2015 |Sí |27 de junio de 2016 |31 de julio de 2017 |
| HDInsight 3.2 |HDP 2.2 |Ubuntu 12.04 LTS o Windows Server 2012 R2 |Sí |18 de febrero de 2015 |No |1 de marzo de 2016 |1 de abril de 2017 |
| HDInsight 3.1 |HDP 2,1 |Windows Server 2012 R2 |Sí |24 de junio de 2014 |No |18 de mayo de 2015 |30 de junio de 2016 |
| HDInsight 3.0 |HDP 2,0 |Windows Server 2012 R2 |Sí |11 de febrero de 2014 |No |17 de septiembre de 2014 |30 de junio de 2015 |
| HDInsight 2.1 |HDP 1,3 |Windows Server 2012 R2 |Sí |28 de octubre de 2013 |No |12 de mayo de 2014 |31 de mayo de 2015 |
| HDInsight 1.6 |HDP 1.1 | |No |28 de octubre de 2013 |No |26 de abril de 2014 |31 de mayo de 2015 |

## <a name="hdinsight-windows-retirement"></a>Retirada de Windows de HDInsight
Microsoft Azure HDInsight versión 3.3 fue Hola última versión de HDInsight en Windows. Hola fecha de retirada de HDInsight en Windows es el 31 de julio de 2018. Si dispone de los clústeres de HDInsight en 3.3 de Windows o una versión anterior, debe migrar tooHDInsight en Linux (HDInsight versión 3.5 o posterior) antes del 31 de julio de 2018. Migración de toohello sistema operativo Linux permite tooretain Hola capacidad toocreate o cambiar el tamaño de los clústeres de HDInsight. La compatibilidad con HDInsight 3.3 en Windows expiró el 27 de junio de 2016.

A partir de HDInsight versiones 3.4, Microsoft ha lanzado HDInsight solo en hello sistema operativo Linux. Como resultado, algunos de los componentes de hello dentro de HDInsight sólo están disponibles para Linux. Estos incluyen Apache Cazador, Kafka, Hive interactivo, Spark, las aplicaciones de HDInsight y el almacén de Azure Data Lake como sistema de archivos principal de Hola. Las versiones futuras de HDInsight sólo están disponibles en hello sistema operativo Linux. No habrá ninguna versión futura de HDInsight en Windows. 

## <a name="faqs"></a>Preguntas más frecuentes

### <a name="what-is-hello-timeline-for-retiring-hdinsight-on-windows"></a>¿Cuál es la escala de tiempo de Hola para retirar HDInsight en Windows?
31 de julio de 2018 es hello fecha de retirada de HDInsight en Windows. Si ha planeado Hola fecha de retirada es diferente de su región, se le notificará por separado. 

### <a name="what-is-hello-impact-of-retiring-hdinsight-on-windows-for-existing-customers"></a>¿Cuál es el impacto de Hola de retirada de HDInsight en Windows para los clientes existentes?
Después de retirar HDInsight en Windows, no puede crear ningún clúster de HDInsight en Windows ni cambiar el tamaño de un clúster existente de este tipo. La compatibilidad con HDInsight 3.3 expiró el 27 de junio de 2016. Por lo tanto, no hay soporte técnico ni correcciones de errores para HDInsight 3.3 o versiones anteriores. Las versiones futuras de HDInsight sólo están disponibles en hello sistema operativo Linux. No habrá ninguna versión futura de HDInsight en Windows.
 
### <a name="which-versions-of-hdinsight-on-windows-are-affected"></a>¿Qué versiones de HDInsight en Windows se ven afectadas?
HDInsight de Azure versión 3.3 es Hola última versión de HDInsight para Windows. Antes de que se ha retirado HDInsight en Windows, todas las ventanas de HDInsight clústeres 3.3 o versiones anteriores deben ser migrado tooHDInsight en Linux versión 3.5 o posterior. Migrar su tooHDInsight de clústeres en Linux permite nuevos clústeres de tooretain Hola capacidad toocreate o cambiar el tamaño de los clústeres existentes. 

### <a name="what-do-i-need-toodo"></a>¿Qué necesito toodo?
Migrar un clúster de HDInsight Linux de tooa compatible de clústeres de HDInsight Windows antes del 31 de julio de 2018. Obtenga más información en hello [documento de migración de HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Para obtener más información acerca de las versiones de HDInsight de Azure, consulte la lista Hola de [versiones compatibles](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-component-versioning#supported-hdinsight-versions). 

### <a name="where-do-i-find-hello-cluster-os-type"></a>¿Dónde se encuentra Hola clúster SO tipo?
Hola portal de Azure, vaya toohello página de información general del clúster de HDInsight y busque **clúster tipo** en **Essentials**. tipos de sistema operativo de Hello clúster se enumeran en la página. 

### <a name="i-cant-migrate-tooan-hdinsight-linux-cluster-by-july-31-2018-what-is-hello-impact-toomy-hdinsight-windows-cluster"></a>No se puede migrar tooan clúster de HDInsight Linux por el 31 de julio de 2018. ¿Qué es hello toomy de impacto en el clúster de HDInsight Windows?
Hello clúster de HDInsight Windows se ejecuta como-es, pero no puede crear un nuevo clúster de HDInsight Windows, o cambiar el tamaño de un clúster de HDInsight Windows existente. 

### <a name="my-cluster-has-a-net-dependency-how-do-i-resolve-this-dependency-on-linux"></a>El clúster tiene una dependencia de .NET. ¿Cómo se resuelve esta dependencia en Linux?
Puede resolver la dependencia de clústeres de Linux mediante hello [proyecto Mono](http://www.mono-project.com/). Esta implementación de código abierto de .NET está disponible para los clústeres de HDInsight en Linux. Obtenga más información en hello [documento de migración de HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). 

### <a name="im-a-new-customer-for-hdinsight-on-windows-how-can-i-create-an-hdinsight-windows-cluster"></a>Soy un nuevo cliente de HDInsight en Windows. ¿Cómo se puede crear un clúster de HDInsight en Windows?
A partir del 3 de julio de 2017, solo los clientes existentes de HDInsight en Windows pueden crear clústeres de HDInsight en Windows. Nuevos clientes no pueden crear un clúster de HDInsight Windows Hola portal de Azure con PowerShell u Hola SDK. Se recomienda que los nuevos clientes creen un clúster de HDInsight en Linux. Los clientes existentes pueden crear nuevas ventanas de HDInsight clústeres hasta hello HDInsight en Windows fecha de retirada. 

### <a name="is-there-a-pricing-impact-associated-with-moving-from-hdinsight-on-windows-toohdinsight-on-linux"></a>¿Hay afectará al precio asociada con el traslado de HDInsight en Windows tooHDInsight en Linux?
No, precios hello es Hola mismo para HDInsight en cualquier sistema operativo. 

### <a name="what-are-hello-customer-advantages-associated-with-hello-move-tooonly-using-hdinsight-on-linux"></a>¿Qué ventajas para el cliente hello asociadas Hola mover tooonly con HDInsight en Linux?
* Tiempo de comercialización más rápido para las tecnologías de grandes cantidades de datos de código abierto a través de hello servicio HDInsight
* Una gran comunidad y ecosistema de soporte técnico
* Comunidad de código abierto de desarrollo activo de capacidad tooexercise por hello Hadoop y otras tecnologías de grandes cantidades de datos

### <a name="does-hdinsight-on-linux-provide-additional-functionality-beyond-what-is-available-in-hdinsight-on-windows"></a>¿HDInsight en Linux proporciona funcionalidad adicional más allá de la disponible en HDInsight en Windows?
A partir de HDInsight versiones 3.4, Microsoft ha lanzado HDInsight solo en hello sistema operativo Linux. Como resultado, algunos de los componentes de hello dentro de HDInsight sólo están disponibles para Linux. Estos incluyen Apache Cazador, Kafka, Hive interactivo, Spark, las aplicaciones de HDInsight y el almacén de Azure Data Lake como sistema de archivos principal de Hola. 

## <a name="service-level-agreement-for-hdinsight-cluster-versions"></a>Contrato de nivel de servicio para las versiones de clúster de HDInsight
contrato de nivel de servicio (SLA) de Hola se define en términos de un _ventana de soporte técnico_. ventana de soporte técnico de Hello es Hola periodo de tiempo que una versión de clúster de HDInsight es compatible con el soporte técnico y el servicio de cliente de Microsoft. Si tiene la versión de Hola un _compatible con fecha de expiración_ que ha pasado, clúster de HDInsight de hello está fuera de la ventana de soporte técnico de hello. Para obtener más información sobre las versiones compatibles, consulte la lista Hola de [admite versiones del clúster de HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). fecha de expiración de soporte técnico de Hola para una versión X (después de que hay disponible una nueva versión de X + 1) de HDInsight especificado se calcula como Hola posterior de:  

* La fórmula 1: Agregar fecha toohello de 180 días cuando se publicó la versión de clúster de HDInsight de hello X.
* Fórmula 2: Agregar fecha toohello de 90 días cuando X + 1 de la versión de clúster de HDInsight de Hola se publica en el portal de Azure.

Hola _fecha de retirada_ es fecha Hola después del cual no se puede crear la versión de clúster hello en HDInsight. A partir del 31 de julio de 2017, no se puede cambiar el tamaño de un clúster de HDInsight después de su fecha de retirada. 

> [!NOTE]
> Clústeres de HDInsight Windows (incluidas versiones 2.1, 3.0, 3.1, 3.2 y 3.3) se ejecutan en la familia de SO invitado de Azure versión 4, que usa la versión de 64 bits de Hola de Windows Server 2012 R2. Familia del SO invitado Azure versión 4 es compatible con las versiones de .NET Framework de hello 4.0, 4.5, 4.5.1 y 4.5.2.

## <a name="hortonworks-release-notes-associated-with-hdinsight-versions"></a>Notas de la versión de HortonWorks asociadas con las versiones de HDInsight

sección de Hello proporciona vínculos toorelease notas para los componentes de Apache que se usan con HDInsight y distribuciones de Hortonworks Data Platform Hola.
* La versión 3.6 del clúster de HDInsight utiliza una distribución de Hadoop basada en [Hortonworks Data Platform 2.6](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html).
* La versión 3.5 del clúster de HDInsight utiliza una distribución de Hadoop basada en [Hortonworks Data Platform 2.5](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.5.0/bk_release-notes/content/ch_relnotes_v250.html). Versión de clúster de HDInsight 3.5 es hello _predeterminado_ clúster de Hadoop que se crea en Hola portal de Azure.
* La versión 3.4 del clúster de HDInsight utiliza una distribución de Hadoop basada en [Hortonworks Data Platform 2.4](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html).
* La versión 3.3 del clúster de HDInsight utiliza una distribución de Hadoop basada en [Hortonworks Data Platform 2.3](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html).

  * [Notas de la versión de Apache Storm](https://storm.apache.org/2015/11/05/storm0100-released.html) están disponibles en el sitio Web de Apache Hola.
  * [Notas de la versión de Apache Hive](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12332384&styleName=Text&projectId=12310843) están disponibles en el sitio Web de Apache Hola.
* La versión 3.2 del clúster de HDInsight utiliza una distribución de Hadoop basada en [Hortonworks Data Platform 2.2][hdp-2-2].

  * Las notas de la versión de los componentes específicos de Apache se encuentran disponibles como sigue: [Hive 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310843&version=12326450), [Pig 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310730&version=12326954), [HBase 0.98.4](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310753&version=12326810), [Phoenix 4.2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12315120&version=12327581), [M/R 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310941&version=12327180), [HDFS 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310942&version=12327181), [YARN 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12313722&version=12327197), [Common](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310240&version=12327179), [Tez 0.5.2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314426&version=12328742), [Ambari 2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12312020&version=12327486), [Storm 0.9.3](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314820&version=12327112) y [Oozie 4.1.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12324960&projectId=12311620).
* El clúster de HDInsight 3.1 utiliza una distribución de Hadoop basada en [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Los clústeres de HDInsight 3.1 creados antes 7 de noviembre de 2014 se basaban en [Hortonworks Data Platform 2.1.1][hdp-2-1-1].
* La versión 3.0 del clúster de HDInsight utiliza una distribución de Hadoop basada en [Hortonworks Data Platform 2.0][hdp-2-0-8].
* La versión 2.1 del clúster de HDInsight utiliza una distribución de Hadoop basada en [Hortonworks Data Platform 1.3][hdp-1-3-0].
* La versión 1.6 del clúster de HDInsight utiliza una distribución de Hadoop basada en [Hortonworks Data Platform 1.1][hdp-1-1-0].

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard y HDInsight Premium

HDInsight de Azure proporciona las ofertas de nube de hello grandes cantidades de datos en dos categorías: _estándar_ y _Premium_. Hello tabla siguiente enumeran las características que están disponibles _sólo_ de HDInsight Premium. Características que no se describen explícitamente en la tabla de hello están disponibles en HDInsight Standard y Premium.

> [!NOTE]
> Hello HDInsight Premium oferta está actualmente en versión preliminar y está disponible sólo para los clústeres de Linux.

| Característica de HDInsight Premium | Description |
| --- | --- |
| Usuarios de clústeres de HDInsight unidos a dominio |Unirse a dominios de Active Directory (Azure AD) de tooAzure de clústeres de HDInsight para la seguridad de nivel de empresa. En HDInsight Premium, puede configurar una lista de empleados de la empresa que se pueda autenticar a través de Azure AD toolog en clúster de HDInsight tooan. Hola, Administrador de empresa puede configurar el control de acceso basado en roles de seguridad de subárbol mediante [Apache Cazador](http://hortonworks.com/apache/ranger/) y restringir toouse de acceso de datos solo lo necesita. Por último, Hola, administrador puede auditar el acceso a los empleados de datos y cambios tooaccess controlar las directivas, y, por tanto, para lograr un alto grado de regulación de los recursos corporativos. Para obtener más información, consulte [Configure domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configuración de clústeres de HDInsight unidos a dominio). |

### <a name="cluster-types-supported-in-hdinsight-premium"></a>Tipos de clúster compatibles con HDInsight Premium
Hello tabla siguiente enumera los tipos de clúster de Hola que son compatibles con HDInsight Premium.

| Tipo de clúster | Estándar | Premium (vista previa) |
| --- | --- | --- |
| Hadoop |Sí |Sí (solo HDInsight 3.6) |
| Spark |Sí |No |
| HBase |Sí |No |
| Storm |Sí |No |
| R Server |Sí |No |
| Interactive Hive (versión preliminar) |Sí |No |
| Kafka (Versión preliminar) |Sí |No | 

### <a name="support-for-azure-data-lake-store-in-hdinsight-premium"></a>Compatibilidad con Azure Data Lake Store en HDInsight Premium

Los clústeres de HDInsight Premium no admiten el uso de Azure Data Lake Store como almacenamiento principal. Sin embargo, puede usar Azure Data Lake Store como almacenamiento complementario con clústeres de HDInsight Premium.

### <a name="pricing-and-sla"></a>Precios y contrato de nivel de servicio
Para obtener información sobre los precios y el contrato de nivel de servicio de HDInsight Premium, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="default-node-configuration-and-virtual-machine-sizes-for-clusters"></a>Configuración de nodo predeterminada y tamaños de máquina virtual para clústeres
Hola siguientes tamaños de máquina virtual (VM) de tablas lista Hola predeterminados para los clústeres de HDInsight.

> [!IMPORTANT]
> Si necesita más de 32 nodos de trabajo en un clúster, tiene que seleccionar un tamaño de nodo principal con al menos 8 núcleos y 14 GB de RAM.
> 
> 

* Todas las regiones, excepto Sur de Brasil y Japón Occidental:

  | Tipo de clúster | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | Principal: tamaño de máquina virtual predeterminado |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | Principal: tamaños de máquina virtual recomendados |D3 v2, D4 v2 y D12 v2 |D3 v2, D4 v2 y D12 v2 |A3, A4, A5 |D12 v2, v2 D13 y D14 v2 |D12 v2, v2 D13 y D14 v2 |
  | Trabajo: tamaño de máquina virtual predeterminado |D3 v2 |D3 v2 |D3 v2 |Windows: D12 v2; Linux: D4 v2 |Windows: D12 v2; Linux: D4 v2 |
  | Trabajo: tamaños de máquina virtual recomendados |D3 v2, D4 v2 y D12 v2 |D3 v2, D4 v2 y D12 v2 |D3 v2, D4 v2 y D12 v2 |Windows: D12 v2, v2 D13 y D14 v2; Linux: D4 v2, D12 v2, v2 D13 y D14 v2 |Windows: D12 v2, v2 D13 y D14 v2; Linux: D4 v2, D12 v2, v2 D13 y D14 v2 |
  | Zookeeper: tamaño de máquina virtual predeterminado | |A3 |A2 | | |
  | Zookeeper: tamaños de máquina virtual recomendados | |A3, A4, A5 |A2, A3, A4 | | |
  | Perimetral: tamaño de máquina virtual predeterminado | | | | |Windows: D12 v2; Linux: D4 v2 |
  | Perimetral: tamaño de máquina virtual recomendado | | | | |Windows: D12 v2, v2 D13 y D14 v2; Linux: D4 v2, D12 v2, v2 D13 y D14 v2 |
* Solo Sur de Brasil y Japón Occidental (ningún tamaño v2):

  | Tipo de clúster | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | Principal: tamaño de máquina virtual predeterminado |D3 |D3 |A3 |D12 |D12 |
  | Principal: tamaños de máquina virtual recomendados |D3, D4, D12 |D3, D4, D12 |A3, A4, A5 |D12, D13, D14 |D12, D13, D14 |
  | Trabajo: tamaño de máquina virtual predeterminado |D3 |D3 |D3 |Windows: D12; Linux: D4 |Windows: D12; Linux: D4 |
  | Trabajo: tamaños de máquina virtual recomendados |D3, D4, D12 |D3, D4, D12 |D3, D4, D12 |Windows: D12, D13 y D14; Linux: D4, D12, D13 y D14 |Windows: D12, D13 y D14; Linux: D4, D12, D13 y D14 |
  | Zookeeper: tamaño de máquina virtual predeterminado | |A2 |A2 | | |
  | Zookeeper: tamaños de máquina virtual recomendados | |A2, A3, A4 |A2, A3, A4 | | |
  | Perimetral: tamaños de máquina virtual predeterminados | | | | |Windows: D12; Linux: D4 |
  | Perimetral: tamaños de máquina virtual recomendados | | | | |Windows: D12, D13 y D14; Linux: D4, D12, D13 y D14 |

> [!NOTE]
> - Head se conoce como *Nimbus* para hello aluvión de tipo de clúster.
> - Se denomina trabajo *Supervisor* para hello aluvión de tipo de clúster.
> - Se denomina trabajo *región* para hello HBase ipo de clúster.

## <a name="next-steps"></a>Pasos siguientes
- [Configuración de clúster para Hadoop, Spark, etc. en HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Trabajo en Hadoop en HDInsight desde un equipo Windows](hdinsight-hadoop-windows-tools.md)

[Supported HDInsight versions]:(#supported-hdinsight-versions)

[image-hdi-versioning-versionscreen]: ./media/hdinsight-component-versioning/hdi-versioning-version-screen.png

[wa-forums]: http://azure.microsoft.com/support/forums/

[connect-excel-with-hive-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md

[hdp-2-2]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[ambari-docs]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[zookeeper]: http://zookeeper.apache.org/
