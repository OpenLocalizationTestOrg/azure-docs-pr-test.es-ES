---
title: "seguridad aaaHadoop: clústeres de HDInsight Unidos a un dominio - Azure | Documentos de Microsoft"
description: Aprenda a...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/31/2016
ms.author: saurinsh
ms.openlocfilehash: 5a9469402a61bcba4017e1ff4bd06dfba23ac963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toohadoop-security-with-domain-joined-hdinsight-clusters-preview"></a>Una seguridad de tooHadoop Introducción a clústeres de HDInsight Unidos a un dominio (versión preliminar)

Hasta hoy, Azure HDInsight solo admite un único usuario administrador local. Esto funcionaba muy bien para departamentos o equipos de aplicaciones menores. Como Hadoop basado en las cargas de trabajo ganadas más popularidad de sector empresarial de hello, hello necesitan para enterprise funcionalidades de grado como basada en active directory, la autenticación, la compatibilidad de varios usuario y control de acceso basado en roles se convirtió en cada vez más importantes. Usar clústeres de HDInsight Unidos a un dominio, puede crear un dominio de Active Directory de HDInsight clúster unido tooan, configurar una lista de empleados de empresa de Hola que puede autenticar a través de Azure Active Directory toolog en clúster tooHDInsight. Alguien fuera de hello enterprise no se puede iniciar sesión o tener acceso a clúster de HDInsight Hola. Hello administrador empresarial puede configurar control de acceso basado en roles para el uso de seguridad de subárbol [Apache Cazador](http://hortonworks.com/apache/ranger/), por lo tanto restringir el acceso a toodata tooonly tanto como sea necesario. Por último, Hola, administrador puede auditar el acceso de datos de Hola por los empleados, y cualquier tooaccess cambios realizados controlar las directivas, lo que se consigue un alto grado de regulación de los recursos corporativos.

> [!NOTE]
> nuevas características de Hola que se describe en esta vista previa están disponibles solo en clústeres de HDInsight basados en Linux para cargas de trabajo de Hive. Hola otras cargas de trabajo, como HBase, Spark, Storm y Kafka, se habilitarán en futuras versiones.

> [!IMPORTANT]
> Oozie no está habilitado en HDInsight unido a un dominio.

## <a name="benefits"></a>Ventajas
La seguridad de la empresa contiene cuatro grandes pilares; seguridad del perímetro, autenticación, autorización y cifrado.

![Pilares de las ventajas de los clústeres de HDInsight de dominio unido](./media/hdinsight-domain-joined-introduction/hdinsight-domain-joined-four-pillars.png).

### <a name="perimeter-security"></a>Seguridad del perímetro
La seguridad del perímetro en HDInsight se logra con redes virtuales y el servicio de puerta de enlace. En la actualidad, un administrador de organización puede crear un clúster de HDInsight dentro de una red virtual y usar grupos de seguridad de red (reglas de firewall de entrada o salida) toorestrict acceso toohello una red virtual. Solo entrada hello las direcciones IP definidas en hello las reglas de firewall será capaz de toocommunicate con clúster de HDInsight de hello, lo que proporciona seguridad en el perímetro. Otro nivel de seguridad del perímetro se realiza mediante el servicio de puerta de enlace. Hola puerta de enlace es servicio de Hola que actúa como primera línea de defensa para cualquier clúster de HDInsight de toohello de solicitud entrante. Acepta la solicitud de hello, lo valida y sólo entonces permite Hola solicitud toopass toohello otros nodos en clúster, lo que proporciona seguridad en el perímetro tooother los nodos de nombre y los datos en el clúster de Hola.

### <a name="authentication"></a>Autenticación
Con esta versión preliminar pública, un administrador de empresa puede aprovisionar un clúster de HDInsight unido a dominio en una [red virtual](https://azure.microsoft.com/services/virtual-network/). nodos de Hola Hola del clúster de HDInsight será dominio toohello combinadas administrado de la empresa Hola. Esto se logra mediante el uso de [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md). Todos los nodos Hola Hola clúster son tooa Unidos a un dominio que administra enterprise Hola. Con esta configuración, pueden registrar empleados de la empresa de hello en nodos del clúster toohello con sus credenciales de dominio. También pueden usar su tooauthenticate de credenciales de dominio con otros extremos aprobados como toointeract matiz, vistas de Ambari, ODBC, JDBC, PowerShell y las API de REST con clúster de Hola. Hola, administrador tiene control total sobre la limitación Hola número de usuarios interactuar con el clúster de Hola a través de estos extremos.

### <a name="authorization"></a>Autorización
Una práctica recomendada, seguida por la mayoría de las empresas es que no todos los empleados tiene acceso a recursos de empresa de tooall. Del mismo modo, con esta versión, Hola, administrador puede definir directivas de control de acceso basado en roles para los recursos de clúster de Hola. Por ejemplo, puede configurar Hola, administrador [Apache Cazador](http://hortonworks.com/apache/ranger/) tooset directivas de control de acceso de Hive. Esta funcionalidad garantiza que los empleados será capaz de tooaccess sólo tantos datos que necesitan toobe correcta en su trabajo. Clúster de SSH acceso toohello también es administrador de toohello solo restringido.

### <a name="auditing"></a>Auditoría
Junto con protección de hello HDInsight contra usuarios no autorizados los recursos de clúster y proteger los datos de hello, auditoría de todos los acceso a recursos de clúster toohello y Hola datos están necesario tootrack acceso no autorizado o accidental de los recursos de Hola. Con esta versión preliminar, Hola, administrador puede ver y todos los recursos de clúster de HDInsight de toohello de acceso y los datos de informes. Hola, administrador también puede ver e informe todos los cambios de las directivas de control de acceso toohello realiza en Apache Cazador admite puntos de conexión. Un clúster de HDInsight Unidos al dominio utiliza Hola familiar interfaz de usuario de Apache Cazador toosearch los registros de auditoría. En el back-end de hello, usa Cazador [Solr Apache](http://hortonworks.com/apache/solr/) para almacenar y buscar registros de Hola.

### <a name="encryption"></a>Cifrado
Protección de datos es importante para los requisitos de cumplimiento y seguridad de la organización reunión y, además de restringir el acceso toodata de empleados no autorizados, también es necesario proteger cifrándolos. Ambos Hola almacenes de datos para los clústeres de HDInsight, Blob de almacenamiento de Azure, y transparente de servidor compatible con el almacenamiento de Azure datos Lake [cifrado de datos](../storage/common/storage-service-encryption.md) en reposo. Los clústeres de HDInsight seguros funcionarán perfectamente con esta funcionalidad de cifrado de los datos en reposo en el lado servidor.

## <a name="next-steps"></a>Pasos siguientes
* Para configurar un clúster de HDInsight unido a dominio, consulte [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configuración de clústeres de HDInsight unidos a un dominio).
* Para administrar los clústeres de HDInsight unidos a dominio, consulte [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Administración de clústeres de HDInsight unidos a un dominio).
* Para configurar directivas de Hive y ejecución de consultas de Hive, consulte [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configuración de directivas de los clústeres de HDInsight unidos a dominio).
* Para ejecutar consultas de Hive mediante SSH en clústeres de HDInsight unidos a un dominio, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
