---
title: "aaaUse HDInsight varios clústeres con una cuenta de almacén de Azure Data Lake - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse más de HDInsight de un clúster con una sola cuenta de almacén de Data Lake"
keywords: almacenamiento para hdinsight,hdfs,datos estructurados,datos no estructurados, data lake store
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: nitinme
ms.openlocfilehash: 3a125b91fcc1e436270a1bd349f7a2d8f27e06fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-multiple-hdinsight-clusters-with-an-azure-data-lake-store-account"></a>Uso de varios clústeres de HDInsight con una cuenta de Azure Data Lake Store

A partir de HDInsight versión 3.5, puede crear clústeres de HDInsight con las cuentas de almacén de Azure Data Lake como Hola predeterminado filesystem.
Data Lake Store admite almacenamiento ilimitado, lo cual es idóneo no solo para hospedar grandes cantidades de datos, sino también para hospedar varios clústeres de HDInsight que compartan una única cuenta de Data Lake Store. Para instructionson cómo toocreate una HDInsight de clúster con el almacén de Data Lake como almacenamiento de hello, consulte [HDInsight crear clústeres con el almacén de Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Este artículo proporciona administrador de almacén de Data Lake toohello de recomendaciones para configurar un único y compartido datos Lake almacenar una cuenta que se puede usar en varias **active** clústeres de HDInsight. Estas recomendaciones aplican toohosting Hadoop segura, así como no seguras varios clústeres en una cuenta de almacén de Data Lake compartida.


## <a name="data-lake-store-file-and-folder-level-acls"></a>ACL de nivel de archivo y carpeta de Data Lake Store

Hello resto de este artículo se da por supuesto que tiene un conocimiento profundo de las ACL de nivel de archivo y carpeta en el almacén de Azure Data Lake, que se describe en detalle en [control de acceso en el almacén de Azure Data Lake](../data-lake-store/data-lake-store-access-control.md).

## <a name="data-lake-store-setup-for-multiple-hdinsight-clusters"></a>Configuración de Data Lake Store para varios clústeres de HDInsight
Empecemos por una jerarquía de carpetas de dos niveles tooexplain recomendaciones de hello para el uso de clústeres de HDInsight de mutilple con una cuenta de almacén de Data Lake. Considere la posibilidad de tener una cuenta de almacén de Data Lake con estructura de carpetas de hello **/clústeres/finance**. Con esta estructura, todos los clústeres de hello requeridos Hola Finanzas organización pueden usar /clusters/finance como ubicación de almacenamiento de Hola. Hola futuras, si otra organización, por ejemplo Marketing, desea que los clústeres de HDInsight de toocreate con Hola misma cuenta de almacén de Data Lake, podría crear /clusters/marketing. De momento, usaremos simplemente **/clusters/finance**.

tooenable esta toobe de la estructura de carpeta usa eficazmente los clústeres de HDInsight, Administrador de almacén de Data Lake Hola debe asignar los permisos adecuados, tal como se describe en la tabla de Hola. permisos de Hola que se muestra en la tabla de hello corresponden tooAccess ACL y no las ACL de forma predeterminada. 


|Carpeta  |Permisos  |usuario propietario  |grupo propietario  | Usuario con nombre | Permisos de usuario con nombre | Grupo con nombre | Permisos de grupo con nombre |
|---------|---------|---------|---------|---------|---------|---------|---------|
|/ | rwxr-x--x  |admin |admin  |Entidad de servicio |--x  |FINGRP   |r-x         |
|/clusters | rwxr-x--x |admin |admin |Entidad de servicio |--x  |FINGRP |r-x         |
|/clusters/finance | rwxr-x--t |admin |FINGRP  |Entidad de servicio |rwx  |-  |-     |

En la tabla de hello,

- **administración** es el creador de Hola y Administrador de cuenta de almacén de Data Lake Hola.
- **Entidad de servicio** es hello Azure Active Directory (AAD) entidad de servicio asociado a la cuenta de hello.
- **FINGRP** es un grupo de usuario creado en AAD que contenga los usuarios de hello organización de finanzas.

Para obtener instrucciones sobre cómo ver una aplicación de AAD (que también se crea una entidad de servicio), toocreate [crear una aplicación AAD](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application). Para obtener instrucciones sobre cómo toocreate un grupo de usuarios en AAD, consulte [administrar grupos en Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

Algunos tooconsider puntos clave.

- estructura de carpetas de nivel de Hello dos (**/clústeres/finance/**) deben crearse y aprovisionado con los permisos adecuados Hola, Administrador de almacén de Data Lake **antes de** con la cuenta de almacenamiento de Hola para los clústeres. Esta estructura no se crea automáticamente durante la creación de clústeres.
- ejemplo de Hola anterior recomienda establecer Hola grupo del propietario **/clústeres/finance** como **FINGRP** y permitir **r-x** tener acceso a la jerarquía de carpeta completa de tooFINGRP toohello a partir de la raíz de Hola. Esto garantiza que los miembros de Hola de FINGRP pueden explorar la estructura de carpeta de Hola a partir de la raíz.
- En caso de hello cuando diferentes entidades de servicio de AAD puede crear clústeres en **/clústeres/finance**, Hola rápidas bits (cuando se establece en hello **finance** carpeta) garantiza que las carpetas se crean por un servicio No se puede eliminar la entidad de seguridad por hello otro.
- Una vez que la estructura de carpetas de Hola y permisos están en su lugar, el proceso de creación de clústeres de HDInsight crea un loaction de almacenamiento de clúster específicos en **/clústeres/finance/**. Por ejemplo, podría ser almacenamiento de Hola para un clúster con hello nombre fincluster01 **/clusters/finance/fincluster01**. Hello propiedad y los permisos para carpetas de hello creados por clúster de HDInsight se muestra en la tabla de hello aquí.

    |Carpeta  |Permisos  |usuario propietario  |grupo propietario  | Usuario con nombre | Permisos de usuario con nombre | Grupo con nombre | Permisos de grupo con nombre |
    |---------|---------|---------|---------|---------|---------|---------|---------|
    |/clusters/finance/ fincluster01 | rwxr-x---  |Entidad de servicio |FINGRP  |- |-  |-   |-  | 
   


## <a name="recommendations-for-job-input-and-output-data"></a>Recomendaciones para los datos de entrada y salida de trabajos

Le recomendamos que el trabajo de tooa de datos de entrada y Hola salidas de un trabajo se almacenan en una carpeta fuera **/clústeres**. Esto garantiza que incluso si carpeta específica del clúster de hello es eliminado tooreclaim algún espacio de almacenamiento, las entradas de trabajo de Hola y salidas siguen estando disponibles para un uso futuro. En tal caso, asegúrese de que jerarquía de carpetas de Hola para almacenar Hola trabajo entradas y salidas de permite el nivel adecuado de acceso para hello entidad de servicio.

## <a name="limit-on-clusters-sharing-a-single-storage-account"></a>Límite de clústeres que comparten una única cuenta de almacenamiento

Hola Hola número límite de clústeres que se puede compartir una sola cuenta de almacén de Data Lake depende de la carga de trabajo de Hola que se ejecutan en esos clústeres. Tener demasiados clústeres o muy altas cargas de trabajo en clústeres de Hola que comparten una cuenta de almacenamiento puede provocar Hola almacenamiento cuenta entrada/salida tooget limitada.

## <a name="support-for-default-acls"></a>Soporte para ACL predeterminadas

Al crear una entidad de servicio con acceso de un usuario con el nombre (como se muestra en la tabla de hello anterior), se recomienda **no** agregar Hola con el nombre de usuario con una ACL de manera predeterminada. Aprovisionamiento de acceso de un usuario con el nombre con resultados de la ACL predeterminada asignación Hola de 770 permisos de usuario propietario, grupo propietario y otros usuarios. Mientras que el valor predeterminado de 770 no retira permisos al usuario propietario (7) o grupo propietario (7), retira todos los permisos del resto (0). Esto da como resultado un problema conocido con un determinado caso de uso que se describe en detalle en hello [problemas conocidos y soluciones alternativas](#known-issues-and-workarounds) sección.

## <a name="known-issues-and-workarounds"></a>Problemas conocidos y soluciones alternativas

Esta sección enumeran Hola problemas para el uso de HDInsight con el almacén de Data Lake y sus soluciones alternativas conocidos.

### <a name="publicly-visible-localized-yarn-resources"></a>Recursos YARN localizados visibles públicamente

Cuando se crea una nueva cuenta de almacenamiento de Azure Data Lake, el directorio raíz de Hola se aprovisiona automáticamente con too770 de conjunto de bits de permiso de acceso ACL. carpeta raíz de Hello propietaria de usuario es conjunto toohello que creó la cuenta de hello (almacén de Data Lake Hola, administrador) y grupo propietario Hola se establece toohello grupo principal de usuario de Hola que creó la cuenta de hello. No se proporciona acceso para otros usuarios.

Esta configuración se conoce tooaffect uno específico HDInsight casos de uso capturados en [YARN 247](https://hwxmonarch.atlassian.net/browse/YARN-247). Envíos de los trabajos pudieron generar un error con un toothis similar del mensaje de error:

    Resource XXXX is not publicly accessible and as such cannot be part of hello public cache.

Como se indica en hello que YARN JIRA anteriormente, vinculado al localizar recursos públicos, hello localizador valida que todos Hola recursos solicitados son realmente públicos activando sus permisos en el sistema de archivos remoto Hola. Se rechaza la localización de cualquier recurso local que no se ajuste a esa condición. Hola comprobación de permisos, incluye el archivo toohello de acceso de lectura para "otros". Este escenario no funciona de fábrica cuando se hospedan los clústeres de HDInsight de Azure Data Lake, ya que Azure Data Lake deniega el acceso demasiado "otros" en el nivel de la carpeta raíz.

#### <a name="workaround"></a>Solución alternativa
Ejecutar de lectura de conjunto de permisos para **otros** a través de la jerarquía de hello, por ejemplo, en  **/** , **/clústeres** y   **/clústeres/Finanzas**  tal y como se muestra en la tabla de hello anterior.

## <a name="see-also"></a>Otras referencias

* [Creación de un clúster de HDInsight con Almacén de Data Lake como almacenamiento](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)


