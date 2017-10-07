---
title: aplicaciones de HDInsight aaaPublish - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate y publicar aplicaciones de HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a>Publicar aplicaciones de HDInsight en hello Azure Marketplace
Una aplicación de HDInsight es una aplicación que los usuarios pueden instalar en un clúster de HDInsight basado en Linux. Estas aplicaciones puede desarrollarlas Microsoft, fabricantes de software independientes (ISV) o el propio usuario. En este artículo, aprenderá cómo toopublish una aplicación de HDInsight en hello Azure Marketplace.  Para obtener información general acerca de la publicación en hello Azure Marketplace, vea [publicar un toohello de oferta de Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).

Aplicaciones de HDInsight usan hello *aportar su propia licencia (BYOL)* modelo, donde proveedor de la aplicación es responsable de licencias hello tooend-usuarios de la aplicación y los usuarios finales solo se le cobrará por Azure para los recursos de Hola crear, como clúster de HDInsight de Hola y sus nodos de máquinas virtuales. Actualmente, la facturación de la propia aplicación hello no se realiza a través de Azure.

Otro artículo relacionado con la aplicación de HDInsight:

* [Instalar aplicaciones de HDInsight](hdinsight-apps-install-applications.md): Obtenga información acerca de cómo los clústeres tooinstall una tooyour de aplicación de HDInsight.
* [Instalar aplicaciones personalizadas de HDInsight](hdinsight-apps-install-custom-applications.md): Obtenga información acerca de cómo tooinstall y probar aplicaciones personalizadas de HDInsight.

## <a name="prerequisites"></a>Requisitos previos
toosubmit el marketplace de toohello aplicación personalizada, debe crear y probar su aplicación personalizada. Vea Hola siguientes artículos:

* [Instalar aplicaciones personalizadas de HDInsight](hdinsight-apps-install-custom-applications.md): Obtenga información acerca de cómo tooinstall y probar aplicaciones personalizadas de HDInsight.

También es preciso haber registrado una cuenta de desarrollador. Vea [publicar un toohello de oferta de Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) y [crear una cuenta de Microsoft Developer](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).

## <a name="define-application"></a>Definición de la aplicación
Hay dos pasos implicados para publicar aplicaciones toohello Azure Marketplace.  En primer lugar defina un **createUiDef.json** tooindicate de archivo que los clústeres de la aplicación es compatible con; y, a continuación, publicar la plantilla de Hola de hello portal de Azure. Hola pasos de la sección es un archivo de createUiDef.json de ejemplo.

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| Campo | Description | Valores posibles |
| --- | --- | --- |
| types |tipos de clústeres de Hello es compatible con la aplicación hello. |Hadoop, HBase, Storm y Spark (o cualquier combinación de éstos) |
| tiers |niveles de clúster de Hello es compatible con la aplicación hello. |Standard, Premium (o ambos) |
| versions |Hola tipos de clúster de HDInsight que es compatible con la aplicación hello. |3.4 |

## <a name="application-install-script"></a>Script de instalación de aplicación
Siempre que una aplicación está instalada en un clúster (uno ya existente o uno nuevo), se crea un nodo del borde y script de instalación de aplicación Hola se ejecuta en él.
  > [!IMPORTANT]
  > nombre de Hola Hola instalar secuencia de comandos de nombres de aplicaciones debe ser único para un clúster determinado con hello siguiendo el formato.
  > 
  > name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"
  > 
  > Tenga en cuenta que hay nombre de secuencia de comandos de toohello de tres partes:
  > 
  > 1. Un prefijo de nombre de la secuencia de comandos, que incluirá el nombre de la aplicación de Hola o una aplicación de toohello relevantes de nombre.
  > 2. Un signo "-", para mejorar la legibilidad.
  > 3. Una función de cadena única con nombre de la aplicación hello como parámetro de Hola.
  > 
  > Un ejemplo es Hola anterior finaliza cada vez: matiz-install-v0-4wkahss55hlas Hola conserva la lista de acciones de script. Para ver una carga de JSON de ejemplo, diríjase a [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).
  > 
script de instalación de Hello debe tener Hola siguientes características:
1. Asegúrese de que el script de Hola es idempotente. Varias llamadas debe generar script de toohello Hola mismo resultado.
2. script de Hola debe ser correctamente con control de versiones. Utilizar una ubicación diferente para el script de Hola al actualizar o probar los cambios para que no afecten a los clientes que están tratando de aplicación de hello tooinstall. 
3. Agregar secuencias de comandos de registro suficiente toohello en cada momento. Hola normalmente los registros de la secuencia de comandos es hello toodebug de forma única los problemas de instalación de aplicación.
4. Asegúrese de que las llamadas tooexternal servicios o recursos tienen reintentos adecuados para que la instalación de hello no se ve afectado por problemas de red transitorios.
5. Si el script está iniciando servicios en los nodos de hello, asegúrese de que Servicios de Hola se supervisan y configurado toostart automáticamente en el caso de los reinicios de nodo.

## <a name="package-application"></a>Empaquetado de aplicación
Cree un archivo zip que contenga todos los archivos requeridos para instalar aplicaciones de HDInsight. Necesita Hola archivo zip en [publicar aplicación](#publish-application).

* [createUiDefinition.json](#define-application).
* mainTemplate.json. En [Instalación de aplicaciones de HDInsight personalizadas](hdinsight-apps-install-custom-applications.md), puede encontrar un ejemplo.
* Todos los scripts requeridos.

> [!NOTE]
> Hola archivos de la aplicación (incluidos los archivos de aplicación web si hay alguno) se pueden ubicar en cualquier extremo accesible públicamente.
> 

## <a name="publish-application"></a>Publicación de la aplicación
Siga Hola siguiendo los pasos toopublish una aplicación de HDInsight:

1. Inicio de sesión toohello [portal de Azure publicación](https://publish.windowsazure.com/).
2. Haga clic en **plantillas de solución** de hello izquierdo toocreate una nueva plantilla de solución.
3. Escriba un título y haga clic en **Create a new solution template** (Crear una plantilla de solución).
4. Haga clic en **cuenta del centro de desarrollo de crear y combinación Hola programa Azure** tooregister su compañía si no lo ha hecho.  Consulte [Crear una cuenta de desarrollador de Microsoft](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).
5. Haga clic en **definir algunas tooget topologías iniciado**. Una plantilla de solución es un tooall "primario" sus topologías. Puede definir varias topologías en una oferta o plantilla de solución. Cuando una oferta se inserta toostaging, se inserta con todos sus topologías. 
6. Escriba un nombre de la topología y, a continuación, haga clic en hello además de inicio de sesión.
7. Escriba una nueva versión y, a continuación, haga clic en hello signo.
8. Archivo de carga Hola zip preparado en [empaquetar aplicación](#package-application).  
9. Haga clic en **Request Certification**(Solicitar certificado). equipo de certificación de Microsoft de Hello revisará archivos hello y certificar topología Hola.

## <a name="next-steps"></a>Pasos siguientes
* [Instalar aplicaciones de HDInsight](hdinsight-apps-install-applications.md): Obtenga información acerca de cómo los clústeres tooinstall una tooyour de aplicación de HDInsight.
* [Instalar aplicaciones personalizadas de HDInsight](hdinsight-apps-install-custom-applications.md): Obtenga información acerca de cómo toodeploy una tooHDInsight de aplicación de HDInsight no publicado.
* [Personalizar los clústeres de HDInsight basados en Linux con acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md): Obtenga información acerca de cómo las aplicaciones adicionales de toouse acción de secuencia de comandos tooinstall.
* [Crear clústeres de Linux-based Hadoop en HDInsight con plantillas de Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Obtenga información acerca de cómo los clústeres toocreate de plantillas de administrador de recursos de toocall HDInsight.
* [Usar los nodos de borde vacío en HDInsight](hdinsight-apps-use-edge-node.md): Obtenga información acerca de cómo toouse vacío arista nodo para obtener acceso a clúster de HDInsight, probar aplicaciones de HDInsight y hospedaje de aplicaciones de HDInsight.

