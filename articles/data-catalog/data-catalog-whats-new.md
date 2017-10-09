---
title: "aaaWhat de nuevo en el catálogo de datos de Azure | Documentos de Microsoft"
description: "Este artículo proporciona que información general de las nuevas capacidades agrega tooAzure el catálogo de datos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 1201f8d4-6f26-4182-af3f-91e758a12303
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/22/2017
ms.author: maroche
ms.openlocfilehash: f60130487ece39e110446b68544945089d2ab37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-data-catalog"></a>Novedades en el Catálogo de datos de Azure
Actualiza demasiado**el catálogo de datos** periódicamente se lanzan. No todas las versiones incluyen nuevas características de cara al usuario, ya que algunas se centran en las funcionalidades del servicio back-end. Esta página destaca nuevo servicio de catálogo de datos de Azure de toohello agregado capacidades orientadas al usuario.

## <a name="whats-new-for-august-2017"></a>Novedades de agosto de 2017 
A partir de agosto de 2017 Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

*   Un ejemplo de desarrollador nuevo está disponible para crear y administrar los metadatos de la relación mediante el uso de hello API de REST de catálogo de datos. Hola *importar información de relación en el catálogo de datos* ejemplo está disponible en hello [página de ejemplos de código de catálogo de datos](https://azure.microsoft.com/resources/samples/?service=data-catalog&sort=0). 
* Soporte técnico para extraer unir metadatos de la relación de los orígenes de datos de Teradata al registrar las tablas relacionadas con la herramienta de registro de origen de datos de Hola.
* Soporte para la función con valores de tabla de SQL Server objetos (TVF) al registrar orígenes de datos de SQL Server mediante la herramienta de registro de origen de datos de Hola.
* Varias actualizaciones y mejoras tooincrease Hola utilidad y el rendimiento del portal del catálogo de datos de Hola.

## <a name="whats-new-for-july-2017"></a>Novedades de julio de 2017 
A partir de julio de 2017 Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:
*   Compatibilidad para un control más pormenorizado sobre las operaciones permitidas de metadatos, entre las que se incluyen:
    - Los administradores del catálogo pueden restringir las etiquetas de toocontribute de capacidad de los usuarios y metadatos relacionados toohello catálogo, habilitar el catálogo de toohello de acceso de solo lectura.
    - Los administradores del catálogo pueden restringir capacidad tooregister nuevos orígenes de datos los usuarios en el catálogo de Hola.
    - Los administradores del catálogo pueden restringir la propiedad de tootake de capacidad de los usuarios de metadatos del activo de datos en el catálogo de Hola.
    - Permisos pueden concederse tooAzure grupos de seguridad de Active Directory y los usuarios para facilitar la administración de permisos.
* Compatibilidad con las relaciones entre los activos de datos registrada y detección activos de datos relacionados en el portal del catálogo de datos de hello, incluidos:
    - Extracción de metadatos de la relación de MySQL, Oracle y SQL Server (incluida la base de datos de SQL Azure), orígenes de datos cuando se usa Hola herramienta de registro de origen de datos de catálogo de datos.
    - Detección de activos de datos relacionados cuando se consultan los metadatos del activo en el portal del catálogo de datos de Hola.
    - Las operaciones toodefine, detectar y administrar las relaciones entre los activos de datos mediante el uso de hello API de REST de catálogo de datos.

Para obtener más detalles sobre la administración de permisos en el catálogo de datos, vea [cómo toosecure tener acceso a los activos de datos y el catálogo de toodata](data-catalog-how-to-secure-catalog.md).
Para obtener más detalles sobre las relaciones en el catálogo de datos, vea [cómo se relacionan los activos de datos en el catálogo de datos en tooview](data-catalog-how-to-view-related-data-assets.md).

## <a name="whats-new-for-june-2017"></a>Novedades de junio de 2017 
A partir de junio de 2017 Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:
*   Compatibilidad con los orígenes de datos de Sybase, Apache Cassandra y MongoDB. Ahora los usuarios pueden registrar y detectar tablas y bases de datos de Cassandra y MongoDB, así como bases de datos, tablas y vistas de Sybase.

> [!NOTE]
> Al registrar MongoDB y Casandra tablas que contengan columnas con tipos de datos complejos, como registros y matrices, estas columnas no se incluirá en los metadatos de hello agregado tooData catálogo.

## <a name="whats-new-for-may-2017"></a>Novedades de mayo de 2017 
A partir de mayo de 2017 Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:
*   Un ejemplo de desarrollador nuevo está disponible para la importación masiva de Hola de términos del glosario empresarial. ejemplo de Hola a la importación masiva glosario está disponible en hello [página de ejemplos de desarrollador de catálogo de datos](https://docs.microsoft.com/azure/data-catalog/data-catalog-samples). 
*   Compatibilidad con la edición de información de conexión de ODBC en el portal del catálogo de datos de Azure de Hola. Los propietarios de activos de datos y los administradores del catálogo de datos ahora pueden editar información de conexión de Hola para orígenes de datos ODBC registrados sin necesidad de orígenes de datos de registro toore Hola.
*   Compatibilidad con las direcciones URL interactivas en las definiciones y las descripciones del glosario empresarial. Cuando las direcciones URL se incluyen en las propiedades de descripción y la definición de Hola para términos del glosario empresarial, se mostrará como hipervínculos en el portal del catálogo de datos de Hola Hola las direcciones URL.
*   Compatibilidad para mostrar nombres expertos además tooexpert direcciones de correo electrónico. Cuando se visualizan a expertos en Propiedades de Hola para un recurso de datos en el portal del catálogo de datos de hello, nombre completo del experto en Hola de Azure Active Directory se mostrará en hello información sobre herramientas.

## <a name="whats-new-for-april-2017"></a>Novedades de abril de 2017 
A partir de abril de 2017 Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:
*   Compatibilidad con los orígenes de datos ODBC. Los usuarios ahora pueden registrar y detectar las bases de datos ODBC, tablas y vistas, usando la herramienta de registro de origen de datos de catálogo de datos de Hola.

## <a name="whats-new-for-march-2017"></a>Novedades de marzo de 2017 
A partir de marzo de 2017 Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:
*   Compatibilidad con el uso de grupos de seguridad de AAD para los administradores de Data Catalog.
*   Azure Data Catalog ahora está disponible en una nueva región de Azure. Los clientes pueden aprovisionar Hola catálogo de datos de Azure en hello oeste región Ee.uu. Central, en suma tooEast EE. UU., oeste de Estados Unidos, Europa occidental y Australia Oriental, Europa del Norte y sudeste de Asia. Para más información, consulte [Regiones de Azure](https://azure.microsoft.com/regions/).

## <a name="whats-new-for-february-2017"></a>Novedades de febrero de 2017 
A partir de febrero de 2017 Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:
*   Compatibilidad con la configuración avanzada de la herramienta de registro de origen de datos de catálogo de datos de Hola. Los usuarios pueden especificar valores de tiempo de espera de comando al registrar orígenes de datos de gran tamaño.
*   Compatibilidad con los orígenes de datos de FTP y PostgreSQL. Los usuarios ahora pueden registrar y detectar archivos y directorios de FTP, así como bases de datos, tablas y vistas de PostgreSQL.

## <a name="whats-new-for-january-2017"></a>Novedades de enero de 2017 
A partir de enero de 2017 Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:
*   Azure Data Catalog ahora es compatible con [CSA STAR](https://www.microsoft.com/trustcenter/compliance/csa-star-certification).
*   Integración con [Obtener y transformar en Excel 2016 y Power Query para Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605). Los usuarios de Excel pueden compartir y detectar consultas mediante Azure Data Catalog desde Excel. Esta funcionalidad está disponible toousers con licencias de Power BI Pro.

## <a name="whats-new-for-december-2016"></a>Novedades de diciembre de 2016
A partir de 2016 de diciembre, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:
*   Azure Data Catalog ahora es compatible con [HIPAA](https://www.microsoft.com/trustcenter/Compliance/HIPAA) y con las [cláusulas según el modelo de la UE](https://www.microsoft.com/TrustCenter/Compliance/EU-Model-Clauses).
*   Compatibilidad con la edición de la información de conexión de los orígenes de datos. Los propietarios de activos de datos y los administradores del catálogo de datos ahora pueden editar información de conexión de Hola para orígenes de datos registrados sin necesidad de orígenes de datos de registro toore Hola.
*   Compatibilidad con los orígenes de datos de Salesforce.com. Los usuarios ahora pueden registrar y detectar objetos de Salesforce.


## <a name="whats-new-for-november-2016"></a>Novedades de noviembre de 2016
A partir de noviembre de 2016, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:
*   Azure Data Catalog ahora es compatible con [ISO/IEC 27001](https://www.microsoft.com/trustcenter/compliance/iso-iec-27001) y con [ISO/IEC 27018](https://www.microsoft.com/TrustCenter/Compliance/iso-iec-27018).
*   Compatibilidad con el registro manual de Hola de orígenes de datos ODBC mediante el portal del catálogo de datos de Hola y API de REST.

## <a name="whats-new-for-september-2016"></a>Novedades de septiembre de 2016
A partir de septiembre de 2016, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Compatibilidad con orígenes de datos de IBM DB2. Ahora los usuarios pueden registrar y detectar tablas y vistas de IBM DB2.
* Compatibilidad con orígenes de datos de Azure Cosmos DB. Los usuarios ahora pueden registrar y detectar colecciones y bases de datos de Cosmos DB.
* Soporte técnico para personalizar el nombre del catálogo de hello en el portal del catálogo de datos de Hola. Los administradores del catálogo ahora pueden proporcionar el texto que se muestra en el título del portal hello, como nombre de la organización de Hola.

## <a name="whats-new-for-august-2016"></a>Novedades de agosto de 2016
A partir de agosto de 2016, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Mejoras para el registro de orígenes de datos de SQL Server Master Data Services (MDS). Los usuarios ahora pueden incluir perfiles de datos y las vistas previas al registrar las entidades MDS con la herramienta de registro de origen de datos de catálogo de datos de Hola.
* Compatibilidad con las búsquedas guardadas de la organización definidas por el administrador. Al guardar una búsqueda en el portal del catálogo de datos de hello, los administradores del catálogo de datos ahora pueden elegir toosave búsquedas para su uso personal o para todos los usuarios del catálogo. Las búsquedas guardadas de la organización se comparten con todos los usuarios del catálogo y pueden proporcionar puntos de partida estandarizados para la detección de orígenes de datos.
* Actualiza la vista de propiedades de toohello en el portal del catálogo de datos de Hola. Todas las propiedades de recurso de datos se muestran ahora y administran en un panel único, puede cambiar el tamaño de tooprovide una experiencia más coherente y reconocible.

## <a name="whats-new-for-july-2016"></a>Novedades de julio de 2016
A partir de julio de 2016, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Compatibilidad con orígenes de datos de SQL Server Master Data Services (MDS). Los usuarios ahora pueden registrar y detectar entidades y modelos MDS.
* Compatibilidad con los procedimientos almacenados de SQL Server. Los usuarios ahora pueden registrar y descubrir objetos de procedimientos almacenados en orígenes de datos de SQL Server.
* Compatibilidad con idiomas adicionales en el portal del catálogo de datos de Azure de Hola y herramienta de registro en origen de datos de hello, para un total de 18 idiomas admitidos. Hola experiencia de usuario del catálogo de datos de Azure se localiza en función de las preferencias de idioma de hello establecer en Windows o en el Explorador de web Hola.
* Las actualizaciones y perfeccionamiento de hello catálogo de datos página principal del portal, incluidas las mejoras de rendimiento y una experiencia de usuario mejorada.

## <a name="whats-new-for-june-2016"></a>Novedades de junio de 2016
En junio de 2016, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Compatibilidad con el tamaño de columnas en la vista de lista de Hola durante la detección de activos de datos en el portal del catálogo de datos de Hola. Los usuarios ahora pueden redimensionar toomore columnas individuales puedan leerse con facilidad metadatos del activo largos como descripciones y etiquetas.
* Power Query para Excel se ha agregado toohello "Abrir en" menú en el portal del catálogo de datos de Hola. Los usuarios ahora pueden abrir orígenes de datos admitidos en Excel 2016 o en Excel 2010 y Excel 2013 con hello [Power Query para Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605) complemento instalado.
* Compatibilidad con orígenes de datos de Azure Table Storage. Los usuarios ahora pueden registrar y detectar objetos de tabla en los orígenes de datos de Azure Storage.

## <a name="whats-new-for-may-2016"></a>Novedades de mayo de 2016
A partir de mayo de 2016, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Glosario empresarial que permite a los administradores del catálogo toodefine business términos y las jerarquías toocreate un vocabulario empresarial común. Los usuarios pueden etiquetar activos de datos registrados con toomake de términos de glosario sea más fácil toodiscover y comprender el contenido de hello del catálogo de Hola. Para obtener más información, vea [cómo tooset seguridad Hola glosarios empresariales para etiquetar los rige](data-catalog-how-to-business-glossary.md)  
* Mejoras toohello Glosario de negocio de catálogo de datos que permite a los usuarios tooupdate varios términos de glosario en una sola operación. Los usuarios pueden seleccionar varios Hola de tooedit términos siguientes campos:
  * Término primario: usuario Hola puede seleccionar un nuevo término primario y todos los términos seleccionados son elementos secundarios de toobe actualizada del término primario de hello seleccionado. Si Hola seleccionado términos tienen hello mismo elemento primario y, a continuación, ese elemento primario se muestra en el cuadro de texto de hello, en caso contrario Hola primario término campo tooblank del conjunto.   
  * Las etiquetas y las partes interesadas: los usuarios pueden agregar y quitar etiquetas y las partes interesadas para varios términos de glosario mediante Hola misma experiencia como etiquetado varios activos de datos.

> [!NOTE]
> Glosario de Hello empresarial solo está disponible en hello edición estándar de catálogo de datos de Azure. Hello edición gratuita no proporciona capacidades de etiquetado controlados o glosarios empresariales.

## <a name="whats-new-for-march-2016"></a>Novedades de marzo de 2016
A partir de marzo de 2016, Hola siguiendo las capacidades se han agregado tooAzure datos catálogo: g:

* Un extremo de API de REST consolidado para tener acceso mediante programación a las capacidades de búsqueda de Hola y capacidades de administración de activos de catálogo de hello servicio catálogo de datos de Azure. El punto de conexión de API de búsqueda y el punto de conexión de API de catálogo están en desuso y dejarán de estar operativos el 21 de marzo de 2016. Semántica de toohello de hello API no hay ningún cambio. Solo el punto de conexión de hello URI cambiado. Para obtener más información, vea hello [referencia de API de REST de catálogo de datos de Azure](https://msdn.microsoft.com/library/azure/mt267595.aspx). Para obtener ejemplos de la API, consulte [Muestras para desarrolladores de Azure Data Catalog](data-catalog-samples.md).

## <a name="whats-new-for-february-2016"></a>Novedades de febrero de 2016
A partir de febrero de 2016, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Seleccionar un origen de datos recién rediseñado experiencia en la herramienta de registro de origen de datos de catálogo de datos de Azure de Hola. Hello herramienta de registro de origen de datos ha sido actualizada toomake TI sea más fácil toolocate y seleccione Hola orígenes de datos admitidos por el catálogo de datos.
* Compatibilidad con 10 idiomas adicionales en el portal del catálogo de datos de Azure de Hola y herramienta de registro de origen de datos de Hola. Además tooEnglish, Hola experiencia del catálogo de datos de Azure está ahora disponible en alemán, español, francés, italiano, japonés, coreano, portugués (Brasil), ruso, chino simplificado y chino tradicional. Hola experiencia del usuario se localiza el catálogo de datos de Azure se basa en las preferencias de idioma de hello establecer en Windows o en el explorador web del usuario de Hola.
* Compatibilidad con la replicación geográfica de datos de Catálogo de datos de Azure para continuidad empresarial y recuperación ante desastres. Todo el contenido el catálogo de datos, incluidas las anotaciones de metadatos y crowdsourced de origen de datos, ahora se replica entre dos regiones de Azure en ningún toocustomers costo adicional alguno. están emparejadas previamente, como mínimo 500 millas de distancia, Hello regiones de Azure y siga asignación Hola tal y como se describe en [negocio continuidad y recuperación ante desastres (BCDR): las regiones emparejadas de Azure](../best-practices-availability-paired-regions.md).
* Compatibilidad con cambiar Hola utilizado por el catálogo de datos de suscripción de Azure. Los administradores del catálogo de datos Azure pueden utilizar la página de configuración de hello en hello catálogo de datos de Azure portal tooselect una suscripción de Azure diferentes para la facturación.

## <a name="whats-new-for-january-2016"></a>Novedades de enero de 2016
A partir de enero de 2016, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Compatibilidad con el registro manual de orígenes de datos adicionales. Ahora puede usar "Crear entrada Manual" en el portal del catálogo de datos de Azure de hello, o usar Hola API de REST de catálogo de datos de Azure tooregister hello siguientes orígenes de datos:
  * OData: función, conjunto de entidades y contenedor de entidades
  * HTTP: archivo, punto de conexión, informe y sitio
  * Sistema de archivos: archivo
  * SharePoint: lista
  * FTP: archivo y directorio
  * Salesforce.com: objeto
  * DB2: tabla, vista y base de datos
  * PostgreSQL: tabla, vista y base de datos
* Compatibilidad con orígenes de datos de "Abrir en SQL Server Data Tools" para SQL Server (incluyendo Azure SQL DB y Almacenamiento de datos SQL de Azure).  
* Compatibilidad con el registro y la detección de vistas y paquetes de SAP HANA. Puede registrar SAP HANA orígenes de datos con datos del catálogo de datos de Azure Hola del origen de la herramienta de registro y pueden anotar y detectar los orígenes de datos de SAP HANA registrados mediante el portal del catálogo de datos de Azure de Hola.
* Hola toopin de capacidad y liberar recursos de datos en el portal del catálogo de datos de Azure de Hola. Puede elegir toopin datos activos toomake les sea más fácil toorediscover y volver a utilizar.
* Una página principal recién rediseñada en el portal del catálogo de datos de Azure de Hola. Hola nueva página de inicio incluye una visión general de hello usuarios actividad actual - incluidas publicados recientemente activos, anclado activos y búsquedas guardadas - y una visión general de la actividad de Hola Hola catálogo como un todo.
* Compatibilidad con la configuración de usuario persistentes en el portal del catálogo de datos de Azure de Hola. Configuración de la experiencia de usuario - vista de cuadrícula o icono incluida, Hola número de resultados por página y resaltado o desactivar - se conserva entre sesiones de usuario.
* Catálogo de datos de Azure está ahora disponible en dos nuevas regiones de Azure. Los clientes pueden aprovisionar Hola el catálogo de datos en las regiones de Europa del Norte y sudeste de Asia hello, en suma tooEast EE. UU., oeste de Estados Unidos, Europa occidental y Australia Oriental. Para más información, consulte [Regiones de Azure](https://azure.microsoft.com/regions/).

> [!NOTE]
> "Abrir en SQL Server Data Tools" requiere Visual Studio 2013 con Update 4 y las herramientas de SQL Server toobe instalado. versión más reciente de hello tooinstall de SQL Server Data Tools, visite [descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).


## <a name="whats-new-for-december-2015"></a>Novedades de diciembre de 2015
A partir de diciembre de 2015, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Compatibilidad con perfiles de datos para orígenes de datos de Almacenamiento de datos SQL de Azure. Al registrar las vistas y tablas de almacenamiento de datos de SQL Azure, los usuarios pueden elegir las métricas de perfil de datos de tooinclude con metadatos de hello extraídos de origen de datos de Hola.
* Compatibilidad para el registro y la detección de objetos de MySQL y bases de datos. Los usuarios pueden registrar MySQL orígenes de datos con datos del catálogo de datos de Azure Hola del origen de la herramienta de registro y pueden anotar y detectar registrados orígenes de datos de MySQL mediante el portal del catálogo de datos de Azure de Hola.
* Compatibilidad con SPNEGO y la autenticación de Windows para orígenes de datos de Teradata. Al registrar Teradata tablas y vistas, los usuarios pueden elegir tooTeradata tooconnect usa la autenticación SPNEGO y Windows y LDAP y TD2.
* Compatibilidad con orígenes de datos de Almacén de Azure Data Lake. Los usuarios ahora pueden registrar y detectar los orígenes de datos de Almacén de Azure Data Lake mediante el Catálogo de datos de Azure.
* Soporte técnico para especificar manualmente la configuración de proxy de red en la herramienta de registro de origen de datos de catálogo de datos de Azure de Hola. Los usuarios pueden seleccionar "Modificar configuración de proxy" desde la página de bienvenida de la herramienta de Hola y pueden especificar toobe de dirección y el puerto de la proxy de hello utilizado por la herramienta de Hola.

## <a name="whats-new-for-november-2015"></a>Novedades de noviembre de 2015
A partir de noviembre de 2015, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Hola tooview de capacidad y copie las cadenas de conexión desde portal del catálogo de datos de Azure de Hola para SQL Server (incluida la base de datos de SQL Azure) y orígenes de datos de Oracle. Los usuarios puedan seleccionar el vínculo "Ver las cadenas de conexión" en la información de conexión de Hola para un servidor SQL Server o tabla, vista o base de datos, toosee Hola cadenas de conexión Oracle utilizan el origen de datos de tooconnect toohello. Se ofrecen cadenas de conexión de ADO.NET, ODBC, OLEDB y JDBC para los orígenes de datos de SQL Server. Se ofrecen cadenas de conexión de OLEDB y ODBC para los orígenes de datos de Oracle.
* Compatibilidad para incluir perfiles de datos al registrar tablas y vistas de Teradata.
* Compatibilidad con "Abrir en Power BI Desktop" para orígenes de SQL Server (incluida Base de datos SQL de Azure y Almacenamiento de datos SQL de Azure), SQL Server Analysis Services, Almacenamiento de Azure y HDFS.  
* Compatibilidad con la autenticación LDAP para orígenes de datos de Teradata. Al registrar Teradata tablas y vistas, los usuarios pueden elegir tooTeradata tooconnect mediante LDAP y la autenticación de TD2.
* Compatibilidad con "Abrir en Excel" para orígenes de datos de Teradata.
* Compatibilidad con los términos de búsqueda recientes en el portal del catálogo de datos de Azure de Hola. Al realizar búsquedas en el portal de hello, los usuarios pueden seleccionar de la experiencia de detección de Hola de tooaccelerate de términos de búsqueda usados recientemente.
* Compatibilidad con la vista preliminar de orígenes de datos de Teradata. Al registrar Teradata tablas y vistas, los usuarios pueden elegir registros de instantánea tooinclude con metadatos de hello extraídos de origen de datos de Hola.
* Compatibilidad con "Abrir en Excel" para orígenes de datos de Almacenamiento de datos SQL de Azure.
* Compatibilidad con definir y modificar esquemas de nivel de columna para los activos de datos registrados manualmente. Después de crear manualmente un recurso de datos mediante el portal del catálogo de datos de Azure de hello, los usuarios pueden agregar definiciones de columna en las propiedades de hello datos activos.
* Compatibilidad con las consultas de "tiene" al buscar el catálogo de datos, detección de hello tooenable de activos de datos registrada poseer metadatos específicos. La sintaxis de consulta de Catálogo de datos de Azure ahora incluye:

| Sintaxis de consulta | Propósito |
| --- | --- |
| `has:previews` |Busca los activos de datos que incluyen una vista previa. |
| `has:documentation` |Busca los activos de datos para los que se ha proporcionado documentación. |
| `has:tableDataProfiles` |Busca activos de datos con información de perfil de datos de nivel de tabla. |
| `has:columnsDataProfiles` |Busca activos de datos con información de perfil de datos de nivel de columna. |


> [!NOTE]
> "Abrir en Power BI Desktop" requiere una versión actual de toobe de aplicación de Power BI Desktop Hola instalado. Si encuentra problemas o errores con esta característica, asegúrese de que tiene la versión más reciente de Hola de Power BI Desktop desde [PowerBI.com](https://powerbi.com).


## <a name="whats-new-for-october-2015"></a>Novedades de octubre de 2015
A partir de octubre de 2015, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Compatibilidad con cifrado en reposo de vistas previas de datos y perfiles de datos para orígenes de datos registrados. Catálogo de datos de Azure cifra de forma transparente los registros de vista previa y orígenes de datos registrados con el servicio de hello, sin necesidad de administración de claves por los administradores del catálogo de perfiles de datos.
* Compatibilidad con orígenes de datos de Teradata. Ahora los usuarios pueden registrar y detectar tablas y vistas de Teradata.
* Compatibilidad con orígenes de datos de Hive locales. Los usuarios ahora pueden registrarse y detectar tablas de Hive de Apache Hive en orígenes de datos locales de Hadoop.
* Compatibilidad con las búsquedas guardadas en el portal del catálogo de datos de Azure de Hola. Los usuarios pueden guardar los términos de búsqueda y tooeasily de selecciones de filtro se repiten las búsquedas anteriores y definir vistas útiles del contenido del catálogo de Hola. El usuario puede marcar una búsqueda guardada como su búsqueda predeterminada. Cuando un usuario hace clic en icono de búsqueda de Hola "lupa" desde la página de principal del portal de catálogo de datos de Azure de Hola o de página de "Introducción" Hola, Hola usuario se le conducirá directamente toohello marcado como valor predeterminado de búsqueda guardada.
* Compatibilidad para la documentación de texto enriquecido para los activos de datos registrada y contenedores en el portal del catálogo de datos de Azure de Hola. Los usuarios ahora pueden proporcionar documentación para los activos de datos como tablas, vistas e informes y para contenedores, como bases de datos y modelos, para escenarios donde las etiquetas y descripciones no sean suficientes.
* Compatibilidad con el registro manual de tipos de orígenes de datos conocidos. Los usuarios pueden escribir manualmente la información de origen de datos mediante el portal del catálogo de datos de Azure de Hola para todos los tipos de orígenes de datos compatibles con el catálogo de datos.
* Compatibilidad con la autorización de grupos de seguridad de Azure Active Directory. Los administradores del catálogo pueden habilitar a acceso toosecurity grupos de catálogos, cuentas de usuario, lo que sea más fácil toomanage acceso tooAzure el catálogo de datos.
* Soporte técnico para abrir orígenes de datos de Hive en Excel desde el portal del catálogo de datos de Azure de Hola.

> [!NOTE]
> Para la versión actual de hello, solo Teradata TD2 se admite la autenticación. En futuras versiones se admitirán también otros mecanismos de autenticación.

> [!NOTE]
> característica de "Abrir en Excel" de hello toouse para orígenes de datos de Hive, los usuarios deben haber instalado al controlador ODBC de Hola para Hive.

## <a name="whats-new-for-september-2015"></a>Novedades de septiembre de 2015
A partir de septiembre de 2015, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Compatibilidad para incluir perfiles de datos al registrar orígenes de datos de Hive.
* Compatibilidad para detectar mediante programación Hola API de catálogo, lo que facilita toointegrate de aplicaciones con el catálogo de datos de Azure.
* Un nuevo "Introducción" origen de datos experiencia de detección en el portal del catálogo de datos de Azure de Hola. Cuando los usuarios escriben la página de "detectar" hello del portal del catálogo de datos de Azure Hola sin escribir un término de búsqueda, se muestra una visión general del contenido de catálogo de hello como etiquetas de Hola que se usan con mayor frecuencia, expertos, tipos de orígenes de datos y tipos de objeto.
* Compatibilidad para el registro y la detección de objetos y bases de datos de Almacenamiento de datos SQL de Azure. Para obtener información adicional sobre el Almacenamiento de datos SQL de Azure, consulte [Almacenamiento de datos SQL](https://azure.microsoft.com/services/sql-data-warehouse/).
* Compatibilidad para el registro y la detección de modelos de SQL Server Analysis Services y servidores de SQL Server Reporting Services como contenedores. Al registrar los objetos SSAS y SSRS, el catálogo de datos crea una entrada para el modelo SSAS de Hola y el servidor SSRS y para los informes de Hola y otros objetos. contenedores de Hola se pueden detectar y anotan utilizando el portal del catálogo de datos de Azure de Hola. Los usuarios también pueden buscar y filtrar contenido Hola de un modelo o un servidor en toosearching de suma y el filtrado de contenido de hello del catálogo de Hola.
* Compatibilidad con el registro y la detección de objetos de SQL Server Analysis Services mediante HTTP o HTTPS. Los usuarios ahora pueden conectarse a servidores de tooSSAS mediante una dirección URL (por ejemplo, https://servername/olap/msmdpump.dll) en lugar de un nombre de servidor y pueden usar la autenticación básica y anónima en la autenticación de tooWindows de adición. Para obtener más información sobre tooSSAS de conexiones HTTP/HTTPS, vea [servicios de configuración del acceso HTTP tooAnalysis](https://msdn.microsoft.com/library/gg492140.aspx).
* Compatibilidad con orígenes de datos de Hive en HDInsight. Los usuarios ahora pueden registrarse y detectar tablas de Hive de Apache Hive de Hadoop en orígenes de datos de HDInsight. Para obtener información adicional sobre Hive en HDInsight, vea hello [centro de documentación de HDInsight](../hdinsight/hdinsight-use-hive.md).
* Compatibilidad para el registro y la detección de bases de datos de SQL Server y clústeres de HDFS como contenedores. Al registrar las tablas de Oracle y vistas o HDFS, el catálogo de datos crea una entrada de base de datos de hello, tablas y vistas. base de datos de Hola se puede detectar y anota utilizando el portal del catálogo de datos de Azure de Hola. Los usuarios también pueden buscar y filtrar Hola contenido de una base de datos o clúster además toosearching y filtrar el contenido de hello del catálogo de Hola.
* Compatibilidad para el registro manual de tipos de orígenes de datos desconocidos. Los usuarios pueden especificar manualmente información de origen de datos mediante el portal del catálogo de datos de Azure hello, para que los orígenes de datos no admiten explícitamente por hello herramienta de registro de origen de datos se pueden anotar y detectado.
* Compatibilidad para el registro y la detección de bases de datos de SQL Server como contenedores. Al registrar las vistas y tablas de SQL Server, el catálogo de datos crea una entrada de base de datos de hello, tablas y vistas. base de datos de Hola se puede detectar y anota utilizando el portal del catálogo de datos de Azure de Hola. Los usuarios también pueden buscar y filtrar contenido Hola de una base de datos en toosearching de suma y el filtrado de contenido de hello del catálogo de Hola.

> [!NOTE]
> Objetos SSAS y de SSRS que se han registrado toohello anterior versión 18 de septiembre se deben registrar volver a con la herramienta de registro de origen de datos de hello antes hello modelo o servidor que se agrega entrada toohello catálogo. Vuelva a registrar un origen de datos no afecta a las anotaciones que se han agregado los usuarios en el portal del catálogo de datos de Azure de Hola.

> [!NOTE]
> Las tablas de Oracle y vistas y archivos HDFS y directorios que se han registrado toohello anterior versión 11 de septiembre se deben volver a registrar con la herramienta de registro de origen de datos de hello antes hello entrada de base de datos o un clúster se agrega toohello catálogo. Vuelva a registrar un origen de datos no afecta a las anotaciones que se han agregado los usuarios en el portal del catálogo de datos de Azure de Hola.

> [!NOTE]
> Tablas de SQL Server y las vistas que se han registrado toohello anterior versión 4 de septiembre deben volver a registrarse mediante la herramienta de registro de origen de datos de hello antes de entrada de la base de datos de Hola se agrega toohello catálogo. Vuelva a registrar un origen de datos no afecta a las anotaciones que se han agregado los usuarios en el portal del catálogo de datos de Azure de Hola.

## <a name="whats-new-for-august-2015"></a>Novedades de agosto de 2015
A partir de agosto de 2015, Hola siguiendo las capacidades se han agregado tooAzure el catálogo de datos:

* Compatibilidad con la generación de perfiles de datos de orígenes de datos de SQL Server y Oracle. Al registrar las vistas y tablas de SQL Server y Oracle, los usuarios pueden elegir tooinclude información de perfil de datos para los objetos de Hola que se va a registrar. perfil de datos de Hello incluye las estadísticas de nivel de objeto y el nivel de columna.
* Compatibilidad con orígenes de datos de Hadoop HDFS. Los usuarios pueden registrarse ahora y detectar directorios y archivos HDFS.
* Soporte técnico para proporcionar información de solicitud de acceso a orígenes de datos registrados. Para cualquier recurso de datos registrados, los usuarios ahora pueden proporcionar instrucciones para que solicitan acceso, incluidos los vínculos de correo electrónico o las direcciones URL, tooeasily integrar con los procesos y las herramientas existentes.
* Información sobre herramientas para las etiquetas y expertos, toomake sea más fácil toodiscover lo que los usuarios han proporcionado los metadatos de activos de datos registrada.
* Hemos agregado un nuevo "User" botón y menú tooour barra de navegación superior. Este menú permite usuario Hola ver hello toolog de cuenta usada en el catálogo de datos de tooAzure y toosign out si lo desea. Este menú también muestra el nombre del catálogo de hello, que es útil toodevelopers utilizando Hola API de REST de catálogo de datos de Azure.
* Standard Edition solo: Al agregar propietarios toodata activos, el catálogo de datos ahora admite cuentas de usuario y grupos de seguridad como propietarios. tooadd un grupo de seguridad como propietario de los activos de datos seleccionado, puede especificar nombre para mostrar de los grupos de Hola o dirección de correo electrónico UPN del grupo de hello, si lo tiene.
* Compatibilidad con orígenes de datos de almacenamiento de blobs de Azure. Los usuarios pueden registrarse ahora y detectar el almacenamiento de blobs de Azure y los directorios.

