---
title: "herramienta de evaluación de soluciones de inteligencia de aaaCortana | Documentos de Microsoft"
description: "Como Partner de Microsoft, estos son todos los pasos de hello necesita toofollow toopublish su tooAppSource de solución de inteligencia de Cortana."
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 76cde4e2090c121683b7026f3d80f90f64566607
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-evaluation-tool"></a>Herramienta de evaluación de soluciones Cortana Intelligence
## <a name="overview"></a>Información general
Puede usar las soluciones de análisis avanzado de hello tooassess de herramienta de evaluación de soluciones de inteligencia de Cortana para el cumplimiento de las mejores prácticas recomendadas de Microsoft. Microsoft está toowork satisfechos con nuestros partners (ISV / SIs) tooprovide soluciones de alta calidad para los clientes, distribuidores y la implementación. Esta guía se recorra proceso Hola del uso de herramienta de evaluación de hello solución con la solución y se describen los procedimientos recomendados específicos de hello en busca.

## <a name="getting-started"></a>Introducción
Por favor, [descargar](https://aka.ms/aa-evaluation-tool-download) e instalar la herramienta de evaluación de soluciones de inteligencia de Cortana Hola.

Requisitos previos:
- Windows 10: [Sitio oficial de Windows 10](https://www.microsoft.com/en-us/windows)
- Azure PowerShell: [Instalación y configuración de Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).

## <a name="identifying-your-app"></a>Identificación de la aplicación
Una vez finalizada la instalación, abra la herramienta de Hola y comenzar la primera evaluación.

![Herramienta de evaluación abierta](./media/cortana-intelligence-appsource-evaluation-tool/1-open-evaluation-tool.png)

Especifique la información de identificación de la solución.

![Conexión a suscripción de Azure](./media/cortana-intelligence-appsource-evaluation-tool/2-connect-azure-subscription.png)

Conecte tooyour suscripción de Azure y proporcionar Hola grupo de recursos que contiene la aplicación.

![Selección de recursos](./media/cortana-intelligence-appsource-evaluation-tool/3-select-resources.png)

Una vez que se ha cargado el grupo de recursos de hello, seleccione los recursos de Hola que se incluyen en la solución e identifican la accesibilidad de Hola de cualquier recurso de datos como:
- Ingesta de datos
- Consumo
- Interno

Usamos esta información toobetter entender cómo la solución es utilizar varios componentes y tooensure orientadas al usuario componentes son coherentes con los procedimientos recomendados.

### <a name="ingestion"></a>Ingesta de datos
Ingesta en este caso significa que los orígenes de datos que son toopull utilizado en los datos de solución de hello exterior o que todos los servicios fuera de la solución de hello usar toopush datos en él.

### <a name="consumption"></a>Consumo
Consumo en este caso significa que los conjuntos de datos que son usuarios de tooend de datos de uso toopush, directa o indirectamente. Por ejemplo:
- Los conjuntos de datos usados en consultas directas de PowerBI.
- Los conjuntos de datos consultados en una aplicación web.

>[!NOTE]
Si se usa un recurso concreto para la ingesta y el consumo, elija **Consumo**.

### <a name="internal"></a>Interno
Use interno para los recursos de datos que solo se usan en el procesamiento interno de la aplicación.

A continuación, podrá tooprovide solicitadas unas credenciales válidas para cualquier base de datos especificada en el paso anterior de hello:

![Establecimiento de requisitos previos](./media/cortana-intelligence-appsource-evaluation-tool/4-set-test-prerequisites.png)

## <a name="solution-test-cases"></a>Casos de prueba de la solución
herramienta de solución de Hello realizará una colección de pruebas automatizadas en su solución.

![Establecimiento de ejecución de pruebas](./media/cortana-intelligence-appsource-evaluation-tool/5-set-test-execution.png)

Después de completan las pruebas de hello, estará más frecuentes tooprovide una explicación o justificación de por qué la solución no cumple el requisito de Hola.

![Justificación comercial](./media/cortana-intelligence-appsource-evaluation-tool/6-provide-business-justification.png)

Por ejemplo, si la solución publica tooAzure SQL DW, evaluación de hello pruebas requieren tooalso publicar tooAzure Analysis Services. 

La solución podría usar máquinas virtuales de IaaS con SQL Server Analysis Services en lugar de Azure Analysis Services. Esto sería una razón aceptable si hay errores de prueba de Hola.
## <a name="packaging-your-evaluation-results"></a>Empaquetado de los resultados de evaluación
Después de completar los casos de prueba de hello, el paquete de la evaluación será el archivo zip de tooa exportado y deberá tooprovide comentarios en la herramienta de evaluación de Hola. 

Necesita tooshare esta prueba da como resultado archivos zip con Microsoft para su toobe solución evalúa antes de obtener toobe aprobación agregado tooAppSource

![Puntuación de la herramienta de evaluación](./media/cortana-intelligence-appsource-evaluation-tool/7-grade-evaluation-tool.png)

Por encima de la sección de este artículo tratan diversas características de la herramienta de Hola, ahora háganoslo revise los tipos de procedimientos recomendados que da como resultado de esta herramienta.

## <a name="security-evaluation-considerations"></a>Consideraciones sobre la evaluación de seguridad
### <a name="databases-should-use-azure-active-directory-authentication"></a>Las bases de datos deberían usar la autenticación de Azure Active Directory
Los recursos de SQL Azure o Azure SQL DW de hello sloution deben habilitarse con la autenticación de Azure Active Directory (AAD). AAD proporciona un único lugar toomanage todos sus identidades y roles.

| Para más información sobre | Vea este artículo |
| --- | --- |
| AAD con SQL Database y SQL Data Warehouse | [Use Azure Active Directory Authentication for authentication with SQL Database or SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) (Usar la autenticación de Azure Active Directory con SQL Database o SQL Data Warehouse) |
| Configuración y administración de AAD | [Configuración y administración de la autenticación de Azure Active Directory con SQL Database o SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) |
| Autenticación de aplicaciones web de Azure | [Autenticación y autorización en el Servicio de aplicaciones de Azure](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview) |
| Configuración de aplicaciones web con AAD | [Cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Azure Active Directory](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)|

### <a name="datasets-accessible-tooend-users-should-support-role-based-access-control"></a>Conjuntos de datos accesible tooend: los usuarios deben deben admitir el control de acceso basado en roles
Al ejecutar la herramienta de evaluación de hello, estará más frecuentes toospecify cualquier informe o la publicación de recursos. Se supone que estos recursos están diseñados para el acceso de los usuarios finales, no de los desarrolladores. Estos recursos deben ser ofrecen control de acceso basado en roles (RBAC) en orden tooensure que los usuarios finales son sólo puede tooaccess autorizado datos.

En concreto, cualquiera de hello Azure recursos siguientes pueden configurarse con RBAC y se consideran aceptable:
- Proteger HDInsight, vea [una seguridad de tooHadoop Introducción a clústeres de HDInsight Unidos a un dominio](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)
- Azure SQL, vea [AAD authentication with Azure SQL]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) (Autenticación de SSD con Azure SQL)
- Azure Analysis Services, vea [Manage database roles and users for Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users) (Administrar usuarios y roles de base de datos de Azure Analysis Services)
- Azure SQL Data Warehouse (Tenga en cuenta que, dado que SQL DW admite RBAC, no se recomienda para el acceso directo de usuarios finales).

Si usa otro tipo de recurso que admite RBAC, especifique en justificación del caso de prueba de Hola.

### <a name="azure-data-lake-store-should-use-at-rest-encryption"></a>Azure Data Lake Store debería usar cifrado en reposo
Azure Data Lake Store (ADLS) admite el cifrado en reposo de forma predeterminada mediante claves de cifrado administradas por ADLS. También puede configurar el cifrado con Azure Key Vault.

Para más información sobre cómo especificar la configuración de cifrado de ADLS, vea [Creación de una cuenta de Almacén de Azure Data Lake](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account).

### <a name="azure-sql-and-azure-sql-data-warehouse-should-use-encryption"></a>Azure SQL y Azure SQL Data Warehouse deberían usar cifrado
Azure SQL y Azure SQL DW admiten el cifrado de datos transparente (TDE), que proporciona cifrado y descifrado en tiempo real de datos y archivos de registro.

| Para más información sobre | Vea este artículo |
| --- | --- |
| Cifrado de datos transparente (TDE)  | [Cifrado de datos transparente](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde) |
| Azure SQL Data Warehouse con TDE | [Introducción al cifrado de datos transparente (TDE)](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql) |
| Configuración de Azure SQL con TDE | [Cifrado de datos transparente con Base de datos SQL de Azure](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) |
| Configuración de Azure SQL con Always Encrypted | [Always Encrypted: protección de datos confidenciales en Base de datos SQL y almacenamiento de las claves de cifrado en Almacén de claves de Azure](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault)|

Además en tooTDE, SQL Azure también admite Always Encrypted, una nueva tecnología de cifrado de datos que garantice el cifrado de datos no solo en rest y durante el movimiento entre cliente y servidor, sino también al datos está en uso mientras se ejecutan comandos en el servidor de Hola.

### <a name="any-virtual-machines-must-be-deployed-from-hello-azure-marketplace"></a>Todas las máquinas virtuales deben implementarse de hello Azure Marketplace
En orden tooprovide un nivel coherente de seguridad en AppSource, es necesario que las máquinas virtuales implementadas como parte de una solución de inteligencia de Cortana estar certificadas y ser publicadas en hello Azure Marketplace.

Consulte la lista actual de hello toosearch de imágenes de Azure Marketplace, [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute).

Para obtener información sobre cómo toopublish imagen de una máquina virtual de Azure Marketplace, vea [guía toocreate una imagen de máquina virtual para hello Azure Marketplace](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation).

## <a name="scalability-evaluation-considerations"></a>Consideraciones sobre la evaluación de escalabilidad
### <a name="cortana-intelligence-solutions-should-include-a-scalable-big-data-platform"></a>Las soluciones de Cortana Intelligence deberían incluir una plataforma escalable de macrodatos
Soluciones de inteligencia de Cortana adaptarán toovery tamaños de datos de gran tamaño. En Azure, esto significa que deben incluir uno de dos plataformas de datos de escala de Petabyte hello:
- Almacén de Azure Data Lake
- Almacenamiento de datos SQL de Azure

Si la solución no requiere la admisión de estos tamaños de datos o si se usa una plataforma de datos alternativo, explicarme esto en justificación del caso de prueba de Hola.
### <a name="cortana-intelligence-solutions-should-include-dedicated-ingestion-data-environments"></a>Las soluciones de Cortana Intelligence deberían incluir entornos dedicados de datos de ingesta
Las soluciones de Cortana Intelligence en general deberían evitar la inserción directa de datos en orígenes de datos relacionales. En lugar de eso, los datos sin procesar deberían almacenarse en un entorno no estructurado, con inserciones o actualizaciones independientes en cualquier almacén relacional con Azure Data Factory.

Para más información sobre cómo copiar datos con Azure Data Factory, vea [Tutorial: Crear una canalización con la actividad de copia mediante Visual Studio](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio).

### <a name="azure-sql-data-warehouse-should-use-polybase-for-data-ingestion"></a>Azure SQL Data Warehouse debería usar PolyBase para la ingesta de datos
Azure SQL DW admite PolyBase para la ingesta de datos paralela altamente escalable. PolyBase permite consultas de tooissue de almacenamiento de datos de SQL Azure toouse en conjuntos de datos externos almacenados en almacenamiento de blobs de Azure o almacén de Azure Data Lake. Esto proporciona un rendimiento superior tooalternative métodos de las actualizaciones masivas.

Para obtener instrucciones sobre cómo empezar a usar PolyBase y Azure SQL DW, vea [Carga de datos con PolyBase en Almacenamiento de datos SQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase).

Para más información sobre los procedimientos recomendados con PolyBase y Azure SQL DW, vea [Guía para el uso de PolyBase en Almacenamiento de datos SQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide).

## <a name="availability-evaluation-considerations"></a>Consideraciones sobre la evaluación de disponibilidad

### <a name="datasets-accessible-tooend-users-should-support-a-large-volume-of-concurrent-users"></a>Los usuarios de tooend accesible de conjuntos de datos deben admitir un gran volumen de usuarios simultáneos
Al ejecutar la herramienta de evaluación de hello, estará más frecuentes toospecify cualquier informe o la publicación de recursos. Se supone que estos recursos están diseñados para el acceso de los usuarios finales, no de los desarrolladores. Estos recursos deberían admitir un número mediano o grande de usuarios simultáneos.

En concreto, almacenamiento de datos de SQL Azure no debe ser usuarios de tooend disponibles de origen de datos único Hola. Si el almacenamiento de datos de SQL Azure se proporciona como un recurso para usuarios avanzados, Azure Analysis Services deben realizarse tootypical disponibles a los usuarios.

Para más información sobre los límites de simultaneidad de Azure SQL DW, vea [Simultaneidad y administración de cargas de trabajo en Almacenamiento de datos SQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency).

Para más información sobre Azure Analysis Services, vea [Analysis Services Overview](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview) (Información general sobre Analysis Services).

### <a name="azure-sql-resources-should-have-a-read-only-replica-for-failover"></a>Los recursos de Azure SQL deberían tener una réplica de solo lectura para la conmutación por error
Bases de datos SQL Azure admiten instancia secundaria tooa de replicación geográfica. Esta instancia, a continuación, se puede usar como una aplicación de alta disponibilidad de conmutación por error instancia tooprovide.

Para más información sobre la replicación geográfica para bases de datos de Azure SQL, vea [SQL Database GEO Replication overview](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview) (Información general sobre la replicación geográfica de SQL Database).

Para obtener instrucciones sobre cómo tooconfigure replicación geográfica para SQL Azure, consulte [configurar la replicación geográfica activa para base de datos de SQL de Azure con Transact-SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql).

### <a name="azure-sql-data-warehouse-should-have-geo-redundant-backups-enabled"></a>Azure SQL Data Warehouse debería tener habilitadas las copias de seguridad con redundancia geográfica
Almacenamiento de datos de SQL Azure admite el almacenamiento de toogeo redundantes de las copias de seguridad diarias. Esta replicación geográfica garantiza que se puedan restaurar almacenamiento de datos de hello incluso en situaciones donde no se puede tener acceso a instantáneas almacenadas en su región primaria. Esta característica está activada de forma predeterminada y no se debe deshabilitar para las soluciones de Cortana Intelligence.

Para más información sobre las copias de seguridad y la restauración de Azure SQL DW, vea [Copias de seguridad de SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups).

### <a name="virtual-machines-should-be-configured-with-availability-sets"></a>Las máquinas virtuales deberían configurarse con conjuntos de disponibilidad
Máquinas virtuales de Azure debe estar configuradas en conjuntos de disponibilidad de impacto de hello toominimize de orden de eventos de mantenimiento planeadas y no planeadas.

Para obtener más información acerca de la disponibilidad de la máquina virtual de Azure, consulte [administrar Hola disponibilidad de máquinas virtuales de Windows en Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability).

## <a name="other-evaluation-considerations"></a>Otras consideraciones sobre la evaluación
### <a name="cortana-intelligence-apps-should-use-a-centralized-tool-for-data-orchestration"></a>Las aplicaciones de Cortana Intelligence deberían usar una herramienta centralizada de orquestación de datos
Con una única herramienta para administrar y programar la transformación y el movimiento de los datos se garantiza la coherencia de los datos críticos. Proporciona una lógica clara en torno a la lógica de reintento, la administración de dependencias, las alertas y los registros, etc. Se recomienda usar hello [Data Factory de Azure](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction) de orquestación de datos en Azure.

Si está usando una herramienta que no sea Azure Data Factory para la orquestación de datos, describa la herramienta o herramientas que use.
### <a name="azure-machine-learning-models-should-be-retrained-using-azure-data-factory"></a>Los modelos de Azure Machine Learning deberían volver a aprender con Azure Data Factory
Aprendizaje automático Azure (AzureML) proporciona herramientas de toouse fácil para la creación de Hola y de implementación de modelado de predicción y las canalizaciones de aprendizaje automático. Sin embargo, es importante que las implementaciones de producción de estos modelos de aprendizaje automático de Azure no se basa en un único conjunto de datos fijo, pero en su lugar se adapta toohello cambiante dinámica de fenómenos del mundo real.

Para más información sobre la creación de servicios web de reaprendizaje en AzureML, vea [Volver a entrenar modelos de aprendizaje automático mediante programación](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically).

Para obtener más información acerca de cómo automatizar el proceso de entrenamiento del modelo hello mediante Data Factory de Azure, consulte [modelos de aprendizaje automático de Azure actualizar mediante actividades de actualización de recursos](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity).

## <a name="existing-documentation"></a>Documentación existente
[Microsoft Azure Certified toogrow su negocio en la nube](https://azure.microsoft.com/en-us/marketplace/programs/certified/)

[Microsoft Azure Certified: Cortana Intelligence](https://azure.microsoft.com/en-us/marketplace/programs/certified/cortana/)

