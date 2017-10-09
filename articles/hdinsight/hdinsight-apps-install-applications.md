---
title: aplicaciones de aaaInstall terceros Hadoop en HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de tooinstall terceros Hadoop en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/16/2017
ms.author: jgao
ms.openlocfilehash: 00071517c81a17c01dccedf9e8dd5d0cabb38567
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>Instalación de aplicaciones de Hadoop de terceros en Azure HDInsight

En este artículo, aprenderá cómo tooinstall una aplicación de Hadoop de otro fabricante ya publicada en HDInsight de Azure. Para obtener instrucciones sobre cómo instalar su propia aplicación, consulte [Instalación de aplicaciones de HDInsight personalizadas](hdinsight-apps-install-custom-applications.md).

Una aplicación de HDInsight es una aplicación que los usuarios pueden instalar en un clúster de HDInsight basado en Linux. Estas aplicaciones puede desarrollarlas Microsoft, fabricantes de software independientes (ISV) o el propio usuario.  

En la actualidad hay cuatro aplicaciones publicadas:

* **DATAIKU DDS en HDInsight**: Dataiku DSS (Studio de ciencia de datos) es un software que permite que los datos tooprototype profesionales (científicos de datos, los analistas de negocios, los desarrolladores...), generar e implementar servicios muy concretos que transforman los datos sin procesar en predicciones de negocio beneficiosas.
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft) ofrece a los analistas un toodiscover de forma interactiva, analizar y visualizar los resultados de hello en grandes cantidades de datos. Incorporar los cambios de orígenes de datos adicionales fácilmente toodiscover nuevas relaciones y obtener respuestas de Hola que necesita rápidamente.
* **Recopilador de datos de Streamsets para HDnsight** proporciona un entorno completo de desarrollo integrado (IDE) que permite diseñar, probar, implementar y administrar y a cualquier introducción canalizaciones que los datos de secuencia y por lotes de la malla e incluye una serie de las transformaciones en la secuencia, sin tener toowrite de código personalizado. 
* **Jaulas CDAP para HDInsight** proporciona Hola unificado primero la plataforma de integración para grandes cantidades de datos que reduce el Hola tiempo tooproduction para aplicaciones de datos y lagos de datos en un 80%. Esta aplicación solo admite con clústeres Standard HBase 3.4.
* **La inteligencia Artificial H2O para HDInsight (Beta)** H2O agua mineral con gas admite Hola siguiendo los algoritmos distribuida: GLM, Naïve Bayes, bosque aleatorias de distribuidas, máquina impulso de gradiente, redes neurales profundo, profunda de aprendizaje, K-means, PCA, Modelos de clasificación bajos generalizados, la detección de anomalías y Autoencoders.
* **Plataforma de análisis de Kyligence** La plataforma de análisis de Kyligence (KAP) es un almacén de datos preparado para la empresa con tecnología Apache Kylin y Apache Hadoop; permite la latencia de consultas en fracciones de segundo en el conjunto de datos de gran escala y simplifica el análisis de datos para usuarios empresariales y analistas. 
* **SnapLogic Hadooplex** hello SnapLogic Hadooplex con HDInsight habilita visión de toobusiness de clientes tooget más rápido proporcionando preparación desde prácticamente cualquier toohello de origen en la nube Microsoft Azure y recopilación de datos de autoservicio plataforma.
* **Servidor de trabajo de Spark para KNIME Spark ejecutor** servidor de trabajo de Spark para KNIME Spark ejecutor es tooconnect usado Hola plataforma de análisis de KNIME tooHDInsight clústeres.

instrucciones de Hello proporcionadas en este artículo usan portal de Azure. También puede exportar plantilla de Azure Resource Manager Hola desde el portal de Hola u Obtenga una copia de la plantilla de administrador de recursos de Hola de proveedores y usar PowerShell de Azure y plantilla de hello toodeploy de CLI de Azure.  Consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight con plantillas de Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

## <a name="prerequisites"></a>Requisitos previos
Si desea que las aplicaciones de HDInsight de tooinstall en un clúster de HDInsight existente, debe tener un clúster de HDInsight. toocreate uno, vea [crear clústeres](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). También puede instalar aplicaciones de HDInsight al crear un clúster de HDInsight.

## <a name="install-applications-tooexisting-clusters"></a>Instalar clústeres de tooexisting de aplicaciones
Hello siguiente procedimiento muestra cómo clúster de HDInsight existente de tooinstall HDInsight aplicaciones tooan.

**tooinstall una aplicación de HDInsight**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **clústeres de HDInsight** en el menú de la izquierda Hola.  Si no lo ve, haga clic en **Más servicios** y, después, en **Clústeres de HDInsight**.
3. Haga clic en un clúster de HDInsight.  Si no tiene ninguno, debe crearlo primero.  Consulte [Crear clúster](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).
4. Haga clic en **aplicaciones** en hello **configuraciones** categoría. Verá una lista de aplicaciones instaladas. Si no puede encontrar las aplicaciones, que significa que no hay ninguna aplicación para esta versión de clúster de HDInsight Hola.
   
    ![Menú del portal de aplicaciones de HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. Haga clic en **agregar** desde el menú de la hoja de Hola. 
   
    ![Aplicaciones instaladas en aplicaciones de HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    Verá una lista de las aplicaciones de HDInsight existentes.
   
    ![Aplicaciones disponibles para aplicaciones de HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. Haga clic en una de las aplicaciones de hello, acepte los términos legales de hello y, a continuación, haga clic en **seleccione**.

Puede ver el estado de instalación de Hola de notificaciones de portal de hello (haga clic en el icono de campana de hello en la parte superior de hello del portal de hello). Después de hello aplicación está instalada, aplicación hello aparecerá en la hoja de aplicaciones instalado Hola.

## <a name="install-applications-during-cluster-creation"></a>Instalación de aplicaciones durante la creación del clúster
Tiene aplicaciones de HDInsight de hello opción tooinstall al crear un clúster. Durante el proceso de hello, HDInsight aplicaciones se instalan después de clúster de Hola se crea y se encuentra en estado de ejecución de Hola. Hello siguiente procedimiento muestra cómo las aplicaciones de HDInsight de tooinstall al crear un clúster.

**tooinstall una aplicación de HDInsight**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **NUEVO**, en **Datos y análisis** y, luego, en **HDInsight**.
3. Especifique el **nombre del clúster**: dicho nombre debe ser único globalmente.
4. Haga clic en **suscripción** tooselect Hola suscripción de Azure que se usa para el clúster de Hola.
5. Haga clic en **Seleccionar tipo de clúster**y luego seleccione:
   
   * **Tipo de clúster**: si no sabe qué toochoose, seleccione **Hadoop**. Es del tipo de clúster más popular de Hola.
   * **Sistema operativo**: seleccione **Linux**.
   * **Versión**: usar la versión predeterminada de hello si no sabe qué toochoose. Para obtener más información, consulte [Versiones de clústeres de HDInsight](hdinsight-component-versioning.md).
   * **Nivel de clúster**: HDInsight de Azure proporciona las ofertas de nube de hello grandes cantidades de datos en dos categorías: nivel estándar y nivel Premium. Para más información, consulte [Niveles de clúster](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).
6. Haga clic en **aplicaciones**, haga clic en uno de hello aplicaciones publicadas y, a continuación, haga clic en **seleccione**.
7. Haga clic en **credenciales** y, a continuación, escriba una contraseña de usuario de administrador de Hola. También deberá tooenter un **nombre de usuario SSH** y un **contraseña** o **clave pública**, que es usuario SSH de hello tooauthenticate usado. El uso de una clave pública es Hola enfoque recomendado. Haga clic en **seleccione** en la configuración de credenciales de hello inferior toosave Hola.
8. Haga clic en **origen de datos**, seleccione uno de hello cuentas de almacenamiento existentes o crear un nuevo toobe de cuenta de almacenamiento usado como cuenta de almacenamiento predeterminada de hello para el clúster de Hola.
9. Haga clic en **grupo de recursos** tooselect un recurso existente de grupo o haga clic en **New** toocreate un nuevo grupo de recursos
10. En hello **nuevo HDInsight clúster** hoja, asegúrese de que **Pin tooStartboard** está seleccionada y, a continuación, haga clic en **crear**. 

## <a name="list-installed-hdinsight-apps-and-properties"></a>Lista de las aplicaciones de HDInsight instaladas y sus propiedades
portal de Hello muestra que una lista de hello instalado aplicaciones de HDInsight para un clúster y las propiedades de Hola de cada aplicación instalada.

**propiedades de aplicación y la presentación de HDInsight toolist**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **clústeres de HDInsight** en el menú de la izquierda Hola.  Si no lo ve, haga clic en **Examinar** y en **Clústeres de HDInsight**.
3. Haga clic en un clúster de HDInsight.
4. De hello **configuración** hoja, haga clic en **aplicaciones** en hello **General** categoría. hoja de aplicaciones instalado Hola enumera todas las aplicaciones de hello instalado. 
   
    ![Aplicaciones instaladas en aplicaciones de HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. Haga clic en uno de hello instalado aplicaciones tooshow Hola propiedad. Hola listas de la hoja de propiedades:
   
   * Nombre de la aplicación: el nombre de la aplicación.
   * Estado: el estado de la aplicación. 
   * Página Web: Hola dirección URL de aplicación web de Hola que ha implementado el nodo del borde de toohello. credencial de Hello es hello igual que las credenciales de usuario de hello HTTP que se ha configurado para el clúster de Hola.
   * Extremo HTTP: credencial hello es hello igual que las credenciales de usuario de hello HTTP que se ha configurado para el clúster de Hola. 
   * Punto de conexión SSH: puede usar el nodo del borde SSH tooconnect toohello. las credenciales de SSH de Hello son Hola igual que las credenciales de usuario SSH de Hola que ha configurado para el clúster de Hola. Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
6. toodelete una aplicación, haga clic en aplicación hello y, a continuación, haga clic en **eliminar** desde el menú contextual de Hola.

## <a name="connect-toohello-edge-node"></a>Conectar el nodo del borde toohello
Puede conectar los nodos de borde de toohello mediante HTTP y SSH. puede encontrar información de punto de conexión de Hola de hello [portal](#list-installed-hdinsight-apps-and-properties). Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

credenciales del extremo HTTP Hola son credenciales de usuario HTTP de Hola que ha configurado para el clúster de HDInsight de hello; credenciales del extremo SSH Hola son credenciales SSH de Hola que ha configurado para el clúster de HDInsight Hola.

## <a name="troubleshoot"></a>Solución de problemas
Vea [solucionar problemas de instalación de hello](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation).

## <a name="next-steps"></a>Pasos siguientes
* [Instalar aplicaciones personalizadas de HDInsight](hdinsight-apps-install-custom-applications.md): Obtenga información acerca de cómo toodeploy una tooHDInsight de aplicación de HDInsight no publicado.
* [Publicar aplicaciones de HDInsight](hdinsight-apps-publish-applications.md): Obtenga información acerca de cómo toopublish su tooAzure de aplicaciones personalizada de HDInsight Marketplace.
* [MSDN: Instalar una aplicación de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Obtenga información acerca de cómo las aplicaciones de HDInsight de toodefine.
* [Personalizar los clústeres de HDInsight basados en Linux con acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md): Obtenga información acerca de cómo las aplicaciones adicionales de toouse acción de secuencia de comandos tooinstall.
* [Crear clústeres de Linux-based Hadoop en HDInsight con plantillas de administrador de recursos](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Obtenga información acerca de cómo los clústeres toocreate de plantillas de administrador de recursos de toocall HDInsight.
* [Usar los nodos de borde vacío en HDInsight](hdinsight-apps-use-edge-node.md): Obtenga información acerca de cómo toouse vacío arista nodo para obtener acceso a clúster de HDInsight, probar aplicaciones de HDInsight y hospedaje de aplicaciones de HDInsight.

