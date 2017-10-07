---
title: aaaDiscover, identificar y clasificar los datos personales en Microsoft Azure | Documentos de Microsoft
description: "Obtenga información sobre cómo buscar, clasificar, detectar e identificar datos"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a>Detección, identificación y clasificación de datos personales en Microsoft Azure

Este artículo proporciona orientación sobre cómo toodiscover, identificar y clasificar los datos personales en varios servicios, incluido el uso de catálogo de datos de Azure, Azure Active Directory, base de datos SQL, Power Query para clústeres de Hadoop en HDInsight de Azure, Azure y Azure tools Consultas de Information Protection, búsqueda de Azure y SQL para la base de datos de Azure Cosmos.

## <a name="scenario-problem-statement-and-goal"></a>Escenario, declaración del problema y objetivo

Una empresa de deportes con sede en Estados Unidos recopila un conjunto de datos tanto personales como de otro tipo. Entre ellos, se incluyen datos de clientes y empleados. Hola empresa mantiene en varias bases de datos y lo almacena en varias ubicaciones diferentes en su entorno de Azure. Además tooselling material para deportes, también alojar y administrar el registro para eventos deportivo preferenciales alrededor de Hola a todos, incluido en hello Europa, y en algunos Hola de casos que recopilan los datos del cliente incluyen información médica.

Como empresa de hello hospeda muchos tours ciclistas internacionales cada año y tiene el personal contingente en ubicaciones en todo el mundo Hola, un par de conjuntos de datos de hello son bastante grandes. empresa Hello también tiene aplicaciones creadas por el desarrollador que usan los clientes y empleados.

compañía de Hello desea hello tooaddress los siguientes problemas:

- Datos personales de clientes y empleados deben ser clasificado/distinguen de hello otra empresa Hola de datos recopila en orden tooensure correcta acceso y seguridad.
- Administrador de datos Hello debe tooeasily detectar la ubicación de Hola de los datos personales del cliente a través de las diferentes áreas de hello entorno de Azure.
- Clientes y empleados datos personales que aparecen en documentos comparten y las comunicaciones de correo electrónico deben estar etiquetadas toohelp asegurarse de que se mantengan seguros.
- los desarrolladores de aplicaciones de la compañía de Hello necesitan una búsqueda de tooeasily de forma de datos personales de clientes y empleados en sus aplicaciones móviles y web.
- Los desarrolladores también necesitan tooquery su base de datos de documentos para los datos personales.

### <a name="company-goals"></a>Objetivos de la empresa

- Todos los datos personales de clientes y empleados deben etiquetarse o anotarse en Azure Data Catalog para que se puedan localizar fácilmente. Lo ideal es que los datos personales de clientes y empleados se etiqueten y anoten por separado.
- Los datos personales de perfiles de usuario de clientes y empleados y la información de trabajo que residen en Azure Active Directory deben encontrarse fácilmente.
- Los datos personales que residen en varias bases de datos SQL deben consultarse con facilidad. 
- Algunos de los grandes conjuntos de datos de la compañía de Hola se administran a través de HDInsight de Azure y almacenados en Hadoop. Se deben importar en Excel para que se puedan consultar los datos personales.
- Los datos personales compartidos en documentos y las comunicaciones de correo electrónico se deben clasificar, etiquetar y mantener seguros con Azure Information Protection.
- Hello los desarrolladores de aplicaciones de la compañía deben ser capaz de toodiscover datos personales clientes y empleados en aplicaciones de Hola que han compilado, lo pueden realizar con búsqueda de Azure.
- Los desarrolladores deben ser capaz de toofind datos personales en la base de datos del documento.

## <a name="azure-active-directory-data-discovery"></a>Azure Active Directory: detección de datos

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) es el directorio multiinquilino basado en la nube y el servicio de administración de identidades de Microsoft. Puede buscar los perfiles de usuario de clientes y empleados e información de trabajo de usuario que contienen datos personales en el [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) entorno (AAD) mediante el uso de hello [portal de Azure](https://portal.azure.com/).

Esto es especialmente útil si desea toofind o cambiar los datos personales de un usuario específico. También puede agregar o cambiar el perfil de usuario y la información del trabajo. Debe iniciar sesión con una cuenta que sea un administrador global para el directorio de Hola.

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a>¿Cómo busco o veo el perfil de usuario y la información del trabajo?

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.

2. Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.

   ![cómo busco el perfil de usuario y la información del trabajo](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. En hello **usuarios y grupos** hoja, seleccione **usuarios**.

  ![Apertura de Usuarios y grupos](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. En hello **a los usuarios y grupos: los usuarios** hoja, seleccione un usuario de la lista de hello y, a continuación, en la hoja de hello para el usuario seleccionado de hello, seleccione **perfil** información de perfil de usuario de tooview que podría contener datos personales .

  ![seleccionar usuario](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. Si necesita tooadd o cambiar la información de perfil de usuario, puede hacerlo y, a continuación, en la barra de comandos de hello, seleccione **guardar.**
6. En la hoja de hello para el usuario seleccionado de hello, seleccione **de trabajo información** información tooview de trabajo del usuario que puede contener datos personales.

 ![ver la información laboral](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. Si necesita tooadd o cambiar la información de trabajo de usuario, puede hacerlo y, a continuación, en la barra de comandos de hello, seleccione **guardar.**

## <a name="azure-sql-database-data-discovery"></a>Azure SQL Database: detección de datos

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) es una base de datos en la nube que ayuda a los desarrolladores a crear y mantener aplicaciones. Para buscar datos personales en [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50), se pueden usar consultas SQL estándares. Consulta elástico de SQL Azure (versión preliminar) permite que las consultas entre bases de datos de tooperform de los usuarios.

Una detallada [base de datos SQL](../sql-database/sql-database-technical-overview.md) tutorial explica muchos aspectos del uso de una base de datos SQL, incluida la forma toobuild uno y cómo toorun consultas de datos. Hola aquí te mostramos un resumen de información de hello disponible en el tutorial Hola con secciones de toospecific de vínculos.

### <a name="how-do-i-build-a-sql-database"></a>¿Cómo se compila una base de datos SQL?

Hay tres toodo de maneras:

- Se puede crear una base de datos de SQL Azure en hello [portal de Azure](https://portal.azure.com/). En el tutorial de hello, deberá usar un conjunto específico de recursos de proceso y almacenamiento dentro de un grupo de recursos y el servidor lógico. Usará datos de ejemplo de una empresa ficticia denominada AdventureWorks. También creará una regla de firewall de nivel de servidor. toolearn cómo toodo, Hola visita [crear una base de datos de SQL Azure en el portal de Azure hello](../sql-database/sql-database-get-started-portal.md) tutorial.

  ![Crear una instancia de Azure SQL Database](media/how-to-discover-classify-personal-data-azure/create-database.png)
- Una base de datos SQL también puede crearse en hello [Shell en la nube de Azure](https://azure.microsoft.com/features/cloud-shell/) CLI, una herramienta de línea de comandos basada en explorador. herramienta de Hello está disponible en el portal de Azure de Hola y se puede ejecutar directamente desde ahí. En este tutorial, inicie la herramienta de hello, definir variables de secuencia de comandos, crear un grupo de recursos y un servidor lógico y configurar una regla de firewall del servidor. Después, creará una base de datos con datos de ejemplo. toolearn cómo toocreate la base de datos de esta manera, visite hello [crear una base de datos de SQL Azure único con hello Azure CLI](../sql-database/sql-database-get-started-cli.md) tutorial.

  ![Tutorial de CLIT](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
La CLI de Azure la usan normalmente los desarrolladores y administradores de Linux. A algunos usuarios les resulta más fácil y más intuitiva que PowerShell, que es la tercera opción.

- Por último, puede crear una base de datos SQL con PowerShell, que es un toocreate de línea de comandos o script herramienta que se usa y administrar Azure y otros recursos. En este tutorial, inicie la herramienta de hello, definir variables de secuencia de comandos, crear un grupo de recursos y un servidor lógico y configurar una regla de firewall del servidor. Después, creará una base de datos con datos de ejemplo.

tutorial de Hello requiere hello Azure PowerShell versión 4.0 o posterior del módulo. Ejecute Get-Module - ListAvailable AzureRM toofind su versión. Si necesita tooinstall o una actualización, consulte el módulo de instalar Azure PowerShell.

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

toolearn cómo toocreate la base de datos de esta manera, visite hello [crear una sola base de datos de SQL Azure con Powershell](../sql-database/sql-database-get-started-powershell.md) tutorial.

>[!Note]
Administradores de Windows suelen toouse PowerShell, pero algunos de ellos prefieran CLI de Azure.

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a>¿Cómo busca datos personales en la base de datos SQL en hello portal de Azure? **

Puede usar la herramienta de editor de consultas integrada de hello dentro de hello toosearch portal Azure para datos personales. Podrá iniciar sesión en la herramienta toohello usando su inicio de sesión de administrador SQL server y la contraseña y, a continuación, escriba una consulta.

  ![Buscar sql mediante el portal de Hola](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

Paso 5 del tutorial de hello muestra una consulta de ejemplo en el panel del editor de consultas de hello, pero no se centran en información personal o confidencial (también combina los datos de dos tablas y crea un alias para la columna de origen de Hola Hola conjunto de datos que se devuelven). Hello captura de pantalla siguiente muestra hello consulta de paso 5, así como Hola panel de resultados que se devuelve:

  ![editor de consultas](media/how-to-discover-classify-personal-data-azure/query-editor.png)

Si la base de datos se ha denominado MyTable, una consulta de ejemplo para obtener información personal podría incluir el nombre, el número del seguro social y el número de identificación, y tendría este aspecto:

“SELECT Name, SSN, ID number FROM MyTable”

¿Ejecutar consulta de hello y, a continuación, ver los resultados de Hola Hola **resultados** panel.

Para obtener más información sobre cómo tooquery una instancia de SQL de base de datos en hello portal de Azure, visite hello [base de datos SQL de consulta hello](../sql-database/sql-database-get-started-portal.md) sección del tutorial Hola.

### <a name="how-do-i-search-for-data-across-multiple-databases"></a>¿Cómo se buscan datos entre varias bases de datos?

Consulta elástico de SQL (vista previa) permite tooperform entre bases de datos y varias consultas de base de datos y devolver un único resultado. Hola [tutorial Introducción](../sql-database/sql-database-elastic-query-overview.md) incluye una descripción detallada de los escenarios y explica Hola diferencia entre las particiones de base de datos horizontal y vertical. La creación de partición horizontal se denomina "particionamiento".

  ![Particiones verticales](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![creación de partición horizontal](media/how-to-discover-classify-personal-data-azure/horizontal.png)

tooget iniciado, visite hello [información general de consulta flexible de base de datos de SQL Azure (vista previa)](../sql-database/sql-database-elastic-query-overview.md) página.

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a>Power Query (para importar clústeres de Hadoop de Azure HDInsight): detección de datos para grandes conjuntos de datos

Hadoop es un servicio de almacenamiento y procesamiento de código abierto de Apache para grandes conjuntos de datos, que se analizan y almacenan en clústeres de Hadoop. [HDInsight de Azure](https://azure.microsoft.com/services/hdinsight/) permite a los usuarios toowork con Hadoop clústeres en Azure. Power Query es un complemento de Excel que, entre otras cosas, ayuda a los usuarios a detectar datos de orígenes diferentes.

Datos personales asociados con los clústeres de Hadoop en HDInsight de Azure pueden ser importado tooExcel con Power Query. Una vez Hola datos están en Excel puede usar una consulta tooidentify lo.

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a>¿Cómo se usan los clústeres de Excel Power Query tooimport Hadoop en HDInsight de Azure en Excel?

Un tutorial de HDInsight le guiará a través de este proceso. Que se explican los requisitos previos e incluye un vínculo tooa [empezar a trabajar con HDInsight de Azure](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) tutorial. Instrucciones explican Excel 2016, así como de 2013 y 2010 (pasos son ligeramente diferentes para las versiones anteriores de Excel hello). Si no tienes Hola Excel Power Query complemento, Hola tutorial muestra cómo tooget lo. Podrá empezar el tutorial de hello en Excel y deberá toohave una cuenta de almacenamiento de blobs de Azure asociada al clúster.

  ![Power Query en Excel](media/how-to-discover-classify-personal-data-azure/excel.png)

toolearn cómo toodo, Hola visita [tooHadoop Excel conectarse mediante Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) tutorial.

Origen: [tooHadoop conectar Excel mediante Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a>Azure Information Protection: clasificación de datos personales de documentos y correo electrónico

[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) puede ayudar a los clientes de Azure aplicar etiquetas tooclassify y proteger los documentos compartidos interna o externamente y comunicaciones por correo electrónico. Algunos de estos elementos pueden contener información personal de clientes o empleados. Las reglas y condiciones se pueden definir automática o manualmente, ya sea por parte de los administradores o de los usuarios. Por ejemplo, si un usuario guarda un documento que incluye información de tarjeta de crédito, debería ver una recomendación de etiqueta configurada por el Administrador de Hola.

### <a name="how-do-i-try-it"></a>¿Cómo puedo probarlo?

Si desea que toogive Azure Information Protection un toosee try si puede ser una elección para su organización, visite hello [tutorial rápido](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial). Le guía a través de cinco pasos básicos: de clasificación de tooseeing de directiva de instalación tooconfiguring, el etiquetado y uso compartido en acción y debe tener menos de una media hora.

### <a name="how-do-i-deploy-it"></a>¿Cómo lo implemento?

Si desea que toodeploy Azure Information Protection para su organización, visite hello [plan para la implementación para la clasificación, el etiquetado y la protección](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).

### <a name="is-there-anything-else-i-should-know"></a>¿Hay algo más que deba saber?

Para obtener información complementaria que le ayudará a considerar cómo tooset, configúrelo, visite Hola [listo, configurar, proteger!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
(Preparados, listos, ¡a proteger!). Y verificación hello más vínculos enumerados a continuación para obtener más información sobre Azure Information Protection.

## <a name="azure-search-data-discovery-for-developer-apps"></a>Azure Search: detección de datos para aplicaciones de desarrollador

[Azure Search](https://azure.microsoft.com/services/search/) es una solución de búsqueda en la nube para desarrolladores que proporciona una experiencia de búsqueda de datos completa para sus aplicaciones. Búsqueda de Azure permite toolocate datos a través de índices definidos por el usuario, como originados de la base de datos de Azure Cosmo, base de datos de SQL Azure, almacenamiento de blobs de Azure, almacenamiento de tabla de Azure o datos JSON de cliente personalizado. También puede estructurar las consultas de Lucene con toosearch de API de REST de búsqueda de Azure de Hola para tipos de datos personales o datos personales de Hola de usuarios específicos. Entre las características, se incluyen la búsqueda de texto completo, la sintaxis de consulta simple y la sintaxis de consulta de Lucene. 

## <a name="how-do-i-use-sql-tooquery-data"></a>¿Cómo se puede usar datos SQL tooquery?

toobegin con conceptos básicos de hello, visite hello [base de datos de Azure CosmosD: cómo tooquery mediante SQL](../cosmos-db/tutorial-query-documentdb.md) tutorial. tutorial de Hello proporciona un documento de muestra y dos consultas de SQL de ejemplo y los resultados.

Para obtener instrucciones más detalladas sobre cómo crear consultas SQL, visite [Consultas SQL para la API de DocumentDB de Azure Cosmos DB](../cosmos-db/documentdb-sql-query.md).

Si está tooAzure nueva base de datos de Cosmos y como toolearn cómo toocreate una base de datos, agregar una colección y agregar datos, visitarán hello [base de datos de Azure Cosmos: compilar una aplicación web de API de documentos](../cosmos-db/create-documentdb-dotnet.md) tutorial de inicio rápido. Si desea que toodo esto en un lenguaje distinto de. NET, como Java, Python, elija su idioma preferido cuando obtenga toohello sitio.

## <a name="next-steps"></a>Pasos siguientes

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)

[¿Qué es SQL Database?](../sql-database/sql-database-technical-overview.md)

[SQL Database Query Editor available in Azure portal (Editor de consultas de SQL Database disponible en Azure Portal)] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)

[¿Qué es Azure Information Protection?](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[¿Qué es Azure Rights Management?](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[Azure Information Protection: Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/) (Azure Information Protection: preparados, listos, ¡a proteger!)
