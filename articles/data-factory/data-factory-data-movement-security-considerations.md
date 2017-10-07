---
title: Consideraciones de aaaSecurity para el movimiento de datos en Data Factory de Azure | Documentos de Microsoft
description: "Información acerca de cómo proteger el movimiento de datos en Azure Data Factory."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 4bfce8884df14ad5b94e28ad3dfcf7025e2130a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---security-considerations-for-data-movement"></a>Azure Data Factory: consideraciones de seguridad para el movimiento de datos
## <a name="introduction"></a>Introducción
Este artículo describe la infraestructura de seguridad básica que los servicios de movimiento de datos de Data Factory de Azure usan toosecure los datos. Los recursos de administración de Azure Data Factory están integrados en la infraestructura de seguridad de Azure y aplican todas las medidas de seguridad que ofrece Azure.

En una solución de Data Factory, se crean una o varias [canalizaciones](data-factory-create-pipelines.md)de datos. Una canalización es una agrupación lógica de actividades que realizan una tarea. Estas canalizaciones residen en la región de Hola donde se creó la factoría de datos de Hola. 

Aunque factoría de datos solo está disponible en **oeste de EE.**, **UU**, y **Europa del Norte** regiones, el servicio de movimiento de datos de hello está disponible [globalmente en varias regiones](data-factory-data-movement-activities.md#global). Factoría de datos de servicio garantiza que datos no dejan un área geográfica / región a menos que se indique explícitamente al Hola servicio toouse una región alternativa si servicio de movimiento de datos de hello no se ha implementado todavía toothat región. 

Azure Data Factory en sí no almacena datos, excepto las credenciales de servicio vinculadas de los almacenes de datos en la nube, que se cifran mediante certificados. Le permite crear flujos de trabajo de datos tooorchestrate movimiento de datos entre [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) y el procesamiento de datos mediante [servicios de proceso](data-factory-compute-linked-services.md) en otras regiones o en local entorno. También permite demasiado[supervisar y administrar flujos de trabajo](data-factory-monitor-manage-pipelines.md) mediante programación y mecanismos de interfaz de usuario.

El movimiento de datos mediante Azure Data Factory tiene la **certificación**:
-   [HIPAA/HITECH](https://www.microsoft.com/en-us/trustcenter/Compliance/HIPAA)  
-   [ISO/IEC 27001](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27001)  
-   [ISO/IEC 27018](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27018) 
-   [CSA STAR](https://www.microsoft.com/en-us/trustcenter/Compliance/CSA-STAR-Certification)
     
Si está interesado en cumplimiento de Azure y cómo Azure protege su propia infraestructura, visite hello [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx). 

En este artículo, revisamos consideraciones de seguridad en hello dos escenarios de movimiento de datos siguientes: 

- **Escenario de nube**: en este escenario, el origen y el destino son públicamente accesibles a través de Internet. Por ejemplo, los servicios de almacenamiento administrado en la nube, como Azure Storage, Azure SQL Data Warehouse, Azure SQL Database, Azure Data Lake Store, Amazon S3, Amazon Redshift, los servicios de SaaS como Salesforce y los protocolos de web, como FTP y OData. [Aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) encontrará una lista integral de los orígenes de datos admitidos.
- **Escenario híbrido**: en este escenario, el origen o destino está detrás de un firewall o dentro de un datos locales de red o hello corporativas almacén está en una red privada / virtual (con mayor frecuencia origen hello) de red y no es accesible públicamente . Los servidores de base de datos hospedados en máquinas virtuales también se incluyen en este escenario.

## <a name="cloud-scenarios"></a>Escenarios de nube
###<a name="securing-data-store-credentials"></a>Protección de las credenciales del almacén de datos
Azure Data Factory protege las credenciales del almacén de datos al **cifrarlos** con **certificados administrados por Microsoft**. Estos certificados se alternan cada **dos años** (lo cual incluye la renovación del certificado y la migración de las credenciales). Estas credenciales cifradas se almacenan de forma segura en una instancia de **Azure Storage administrada por los servicios de administración de Azure Data Factory**. Para más información acerca de la seguridad de Azure Storage, consulte [Introducción a la seguridad de Azure Storage](../security/security-storage-overview.md).

### <a name="data-encryption-in-transit"></a>Cifrado de datos en tránsito
Si el almacén de datos de nube de hello admite HTTPS o TLS, todos los datos que se transfiere entre los servicios de movimiento de datos en la factoría de datos y un almacén de datos en la nube son a través de un canal seguro HTTPS ni TLS.

> [!NOTE]
> Todas las conexiones demasiado**base de datos de SQL Azure** y **almacenamiento de datos de SQL Azure** siempre requieren cifrado (SSL/TLS) mientras están en tránsito tooand de base de datos de Hola. Mientras se crea una canalización con un editor de JSON, agregar hello **cifrado** propiedad y establecerla demasiado**true** en hello **cadena de conexión**. Cuando usas hello [Asistente para copiar](data-factory-azure-copy-wizard.md), Asistente Hola establece esta propiedad de forma predeterminada. Para **el almacenamiento de Azure**, puede usar **HTTPS** en la cadena de conexión de Hola.

### <a name="data-encryption-at-rest"></a>Cifrado de datos en reposo
Algunos almacenes de datos admiten el cifrado de datos en reposo. Se recomienda habilitar el mecanismo de cifrado de datos para estos almacenes. 

#### <a name="azure-sql-data-warehouse"></a>Almacenamiento de datos SQL de Azure
Cifrado de datos transparente (TDE) en el almacén de datos de SQL Azure ayuda a protegerse contra amenazas de Hola de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de los datos en reposo. Este comportamiento es transparente toohello cliente. Para más información, consulte [Proteger una base de datos en SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md).

#### <a name="azure-sql-database"></a>Azure SQL Database
La base de datos de SQL Azure también admite el cifrado de datos transparente (TDE), que ayuda a protegerse contra amenazas de Hola de actividad malintencionada realizando en tiempo real cifrado y descifrado de datos de hello sin necesidad de cambios toohello aplicación. Este comportamiento es transparente toohello cliente. Para más información, consulte [Transparent Data Encryption with Azure SQL Database](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) (Cifrado de datos transparente con Azure SQL Database). 

#### <a name="azure-data-lake-store"></a>Almacén de Azure Data Lake
Almacén de Azure Data Lake también permite cifrar los datos almacenados en la cuenta de hello. Cuando se habilita, almacén de Data Lake cifra los datos antes de guardar automáticamente y se descifra antes de la recuperación, lo que el cliente toohello transparente obtener acceso a datos de Hola. Para más información, consulte [Seguridad en Azure Data Lake Store](../data-lake-store/data-lake-store-security-overview.md). 

#### <a name="azure-blob-storage-and-azure-table-storage"></a>Azure Blob Storage y Azure Table Storage
Almacenamiento de Azure, almacenamiento de blobs y tablas de Azure admite el cifrado de servicio de almacenamiento (SSE), que cifra automáticamente los datos antes de guardar toostorage y descifra antes de la recuperación. Para más información, consulte [Cifrado del servicio Azure Storage para datos en reposo](../storage/common/storage-service-encryption.md).

#### <a name="amazon-s3"></a>Amazon S3
Amazon S3 admite el cifrado de cliente y servidor para datos en reposo. Para más información, consulte [Protección de datos del cliente mediante cifrado](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html). Actualmente, Data Factory no admite Amazon S3 en Virtual Private Cloud (VPC).

#### <a name="amazon-redshift"></a>Amazon Redshift
Amazon Redshift admite cifrado de clúster para datos en reposo. Para más información, consulte [Amazon Redshift Database Encryption](http://docs.aws.amazon.com/redshift/latest/mgmt/working-with-db-encryption.html) (Cifrado de base de datos de Amazon Redshift). Actualmente, Data Factory no admite Amazon Redshift en VPC. 

#### <a name="salesforce"></a>Salesforce
Salesforce admite Shield Platform Encryption, que permite el cifrado de todos los archivos, datos adjuntos y campos personalizados. Para obtener más información, consulte [Hola descripción flujo de autenticación de OAuth de servidor de Web](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_web_server_oauth_flow.htm).  

## <a name="hybrid-scenarios-using-data-management-gateway"></a>Escenarios híbridos (con Data Management Gateway)
Escenarios híbridos requieren toobe Data Management Gateway instalado en una red local o en una red virtual (Azure) o una nube privada virtual (Amazon). puerta de enlace de Hello debe ser capaz de tooaccess almacenes de datos locales de Hola. Para obtener más información acerca de la puerta de enlace de hello, consulte [Data Management Gateway](data-factory-data-management-gateway.md). 

![Canales de Data Management Gateway](media/data-factory-data-movement-security-considerations/data-management-gateway-channels.png)

Hola **canal del comando** permite la comunicación entre los servicios de movimiento de datos en la factoría de datos y Data Management Gateway. comunicación de Hello contiene información relacionada con la actividad de toohello. canal de datos de Hola se usa para transferir datos entre almacenes de datos local y almacenes de datos en la nube.    

### <a name="on-premises-data-store-credentials"></a>Credenciales de los almacenes de datos locales
credenciales de Hola para los almacenes de datos local se almacenan localmente (no en la nube hello). Pueden establecerse de tres maneras distintas. 

- Con **texto sin formato** (menos seguro) a través de HTTPS desde Azure Portal o el Asistente para copia. Hola credenciales se pasan en la puerta de enlace de texto sin formato toohello local.
- Con la **biblioteca de criptografía de JavaScript del Asistente para copia**.
- Con la **aplicación de administración de credenciales con un clic**. Haga clic en de Hello-una vez que la aplicación se ejecuta en la máquina local de Hola que tiene la puerta de enlace de acceso toohello y establece las credenciales de almacén de datos de Hola. Esta opción y Hola siguiente son Hola opciones más seguras. aplicación de administrador de credenciales de Hello, de forma predeterminada, utiliza el puerto de hello 8050 en la máquina de hello con puerta de enlace para una comunicación segura.  
- Use [AzureRmDataFactoryEncryptValue nuevo](/powershell/module/azurerm.datafactories/New-AzureRmDataFactoryEncryptValue) las credenciales de tooencrypt de cmdlet de PowerShell. Hola cmdlet utiliza esa puerta de enlace está configurado toouse tooencrypt Hola credenciales de certificado de Hola. Puede usar las credenciales de hello cifrado, este cmdlet devueltas y agregarlo demasiado**EncryptedCredential** elemento de hello **connectionString** en archivo JSON de Hola que se utiliza con hello [ Nueva AzureRmDataFactoryLinkedService](/powershell/module/azurerm.datafactories/new-azurermdatafactorylinkedservice) cmdlet o en el fragmento de JSON Hola Hola Editor de generador de datos en el portal de Hola. Esta opción y hello, haga clic-una vez que la aplicación son opciones más seguras de Hola. 

#### <a name="javascript-cryptography-library-based-encryption"></a>Cifrado basado en la biblioteca de criptografía de JavaScript
Puede cifrar las credenciales del almacén de datos mediante [biblioteca JavaScript criptografía](https://www.microsoft.com/download/details.aspx?id=52439) de hello [Asistente para copiar](data-factory-copy-wizard.md). Cuando se selecciona esta opción, Hola Asistente para copiar recupera la clave pública de Hola de puerta de enlace y usa las credenciales del almacén de datos de tooencrypt Hola. las credenciales de Hola se descifran por máquina de puerta de enlace de Hola y protegidas por Windows [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx).

**Exploradores admitidos:** IE8, IE9, IE10, IE11, Microsoft Edge y las versiones más recientes de los exploradores Firefox, Chrome, Opera y Safari. 

#### <a name="click-once-credentials-manager-app"></a>Aplicación de administración de credenciales con un clic
Puede iniciar Hola click-una vez según la aplicación del Administrador de credenciales desde el portal de Azure o copiar asistente al crear las canalizaciones. Esta aplicación garantiza que las credenciales no se transfieren en texto sin formato a través de la conexión de Hola. De forma predeterminada, usa el puerto de hello **8050** en la máquina de hello con puerta de enlace para una comunicación segura. Si es necesario, se puede cambiar este puerto.  
  
![Puerto HTTPS para la puerta de enlace de Hola](media/data-factory-data-movement-security-considerations/https-port-for-gateway.png)

Actualmente, Data Management Gateway utiliza un solo **certificado**. Este certificado se crea durante la instalación de puerta de enlace de hello (se aplica tooData crear puerta de enlace de administración después de noviembre de 2016 y versión 2.4.xxxx.x o posterior). Puede reemplazar este certificado por su propio certificado SSL/TLS. Este certificado se usa con un clic de hello-una vez que toosecurely de aplicación de administrador de credenciales conectar toohello máquina de puerta de enlace para establecer las credenciales del almacén de datos. Almacena los datos las credenciales del almacén seguro local mediante el uso de Windows hello [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx) en la máquina de hello con puerta de enlace. 

> [!NOTE]
> Las puertas de enlace más antiguos que se instalaron antes de noviembre de 2016 o de versión 2.3.xxxx.x continuar toouse credenciales cifran y almacenan en la nube. Incluso si actualiza la versión más reciente de toohello de puerta de enlace de Hola, credenciales de hello no están máquina local de tooan migrados    
  
| Versión de la puerta de enlace (durante la creación) | Credenciales almacenadas | Cifrado/seguridad de las credenciales | 
| --------------------------------- | ------------------ | --------- |  
| < = 2.3.xxxx.x | En la nube | Cifrado mediante certificado (distinto de hello utilizado por la aplicación del Administrador de credenciales) | 
| > = 2.4.xxxx.x | Local | Protección con la DPAPI | 
  

### <a name="encryption-in-transit"></a>Cifrado en tránsito
Son todas las transferencias de datos a través de canal seguro **HTTPS** y **TLS sobre TCP** ataques de man-in-the-middle tooprevent durante la comunicación con servicios de Azure.
 
También puede usar [IPSec VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md) o [Express Route](../expressroute/expressroute-introduction.md) toofurther canal de comunicación de hello segura entre su red local y Azure.

Red virtual es una representación lógica de la red en la nube de Hola. Puede conectarse un tooyour de red local red virtual de Azure (VNet) mediante la configuración de VPN con IPSec (sitio a sitio) o Express Route (intercambio de tráfico privado)       

Hello siguiente tabla resume Hola de red y puerta de enlace de las recomendaciones de configuración basadas en diferentes combinaciones de ubicaciones de origen y destino para el movimiento de datos híbridos.

| Origen | Destino | Network configuration (Configuración de red) | Instalación de la puerta de enlace |
| ------ | ----------- | --------------------- | ------------- | 
| Local | Máquinas virtuales y servicios en la nube implementados en redes virtuales | VPN de IPSec (de punto a sitio o de sitio a sitio) | La puerta de enlace se puede instalare una máquina local o virtual de Azure (VM) en una red virtual | 
| Local | Máquinas virtuales y servicios en la nube implementados en redes virtuales | ExpressRoute (Emparejamiento privado) | La puerta de enlace se puede instalare una máquina local o virtual de Azure en una red virtual | 
| Local | Servicios basados en Azure que tienen un punto de conexión público | ExpressRoute (Emparejamiento público) | La puerta de enlace debe estar instalada en la máquina local | 

Hello siguientes imágenes muestran el uso de Hola de Data Management Gateway para mover datos entre una base de datos local y servicios de Azure mediante expressroute y VPN con IPSec (con red Virtual):

**ExpressRoute:**
 
![Uso de ExpressRoute con la puerta de enlace](media/data-factory-data-movement-security-considerations/express-route-for-gateway.png) 

**Conexión VPN de IPSec:**

![Conexión VPN de IPSec con la puerta de enlace](media/data-factory-data-movement-security-considerations/ipsec-vpn-for-gateway.png)

### <a name="firewall-configurations-and-whitelisting-ip-address-of-gateway"></a>Configuraciones de firewall y lista de direcciones IP que admite la puerta de enlace

#### <a name="firewall-requirements-for-on-premisesprivate-network"></a>Requisitos de firewall para redes locales o privadas  
En una empresa, un **firewall corporativo** se ejecuta en el enrutador central de Hola de organización de Hola. Y, **firewall de Windows** se ejecuta como un demonio en equipo local hello en qué Hola está instalada la puerta de enlace. 

Hello tabla siguiente proporciona **el puerto de salida** y requisitos de dominio para hello **firewall corporativo**.

| Nombres de dominio | Puertos de salida | Descripción |
| ------------ | -------------- | ----------- | 
| `*.servicebus.windows.net` | 443, 80 | Requiere servicios de movimiento de hello puerta de enlace tooconnect toodata de factoría de datos |
| `*.core.windows.net` | 443 | Usa Hola puerta de enlace tooconnect tooAzure cuenta de almacenamiento cuando use hello [provisionalmente copia](data-factory-copy-activity-performance.md#staged-copy) característica. | 
| `*.frontend.clouddatahub.net` | 443 | Requiere Hola puerta de enlace tooconnect toohello servicio Data Factory de Azure. | 
| `*.database.windows.net` | 1433   | (OPCIONAL) Necesario cuando el destino es Azure SQL Database o Azure SQL Data Warehouse. Hola de uso almacenados provisionalmente copia característica toocopy datos tooAzure almacenamiento de datos de SQL Azure/base de datos SQL sin tener que abrir el puerto 1433 de Hola. | 
| `*.azuredatalakestore.net` | 443 | (OPCIONAL) Necesario cuando el destino es Azure Data Lake Store. | 

> [!NOTE] 
> Es posible que tenga toomanage puertos / dominios de creación de listas blancas en Hola nivel firewall corporativo según sea necesario, orígenes de datos respectivos. En esta tabla, Azure SQL Database, Azure SQL Data Warehouse y Azure Data Lake Store solo se usan a modo de ejemplo.   

Hello tabla siguiente proporciona **puerto entrante** requisitos para hello **firewall de windows**.

| Puertos de entrada | Descripción | 
| ------------- | ----------- | 
| 8050 (TCP) | Requiere Hola credencial manager aplicación toosecurely establecer credenciales para almacenes de datos local en la puerta de enlace de Hola. | 

![Requisitos de puerto de la puerta de enlace](media\data-factory-data-movement-security-considerations/gateway-port-requirements.png) 

#### <a name="ip-configurations-whitelisting-in-data-store"></a>Configuraciones IP/lista de admitidos en el almacén de datos
Algunos almacenes de datos en la nube de hello también requieren blancas de dirección IP del equipo de hello obtener acceso a ellos. Asegúrese de que dirección IP de Hola de máquina de puerta de enlace de hello en la lista blanca configurada correctamente en el firewall.

Hello siguientes almacenes de datos de nube requieren blancas de dirección IP del equipo de puerta de enlace de Hola. Algunos de estos almacenes de datos, de forma predeterminada, no necesita crear listas blancas de dirección IP de Hola. 

- [Azure SQL Database](../sql-database/sql-database-firewall-configure.md) 
- [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal)
- [Almacén de Azure Data Lake](../data-lake-store/data-lake-store-secure-data.md#set-ip-address-range-for-data-access)
- [Azure Cosmos DB](../documentdb/documentdb-firewall-support.md)
- [Amazon Redshift](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**Pregunta:** Hola puerta de enlace se puede compartir entre factorías de datos diferentes?
**Respuesta:** Aún no se admite esta característica. Estamos trabajando en ello.

**Pregunta:** ¿cuáles son los requisitos de puerto de Hola para hello toowork de puerta de enlace?
**Respuesta:** puerta de enlace realiza las conexiones basadas en HTTP tooopen internet. Hola **puertos salientes 80 y 443** debe estar abierto para la puerta de enlace toomake esta conexión. Abra **8050 de puerto de entrada** solo en nivel de equipo de hello (no en el nivel de firewall corporativo) para la aplicación de administrador de credenciales. Si se utiliza la base de datos de SQL Azure o almacenamiento de datos de SQL Azure como origen y destino, tendrá que tooopen **1433** puerto así. Para más información, consulte la sección [Configuraciones del firewall y lista de direcciones IP admitidas](#firewall-configurations-and-whitelisting-ip-address-of gateway). 

**Pregunta:** ¿Cuáles son los certificados necesarios para la puerta de enlace?
**Respuesta:** puerta de enlace actual requiere un certificado que se utiliza la aplicación de administrador de credenciales de Hola para establecer las credenciales del almacén de datos de forma segura. Este certificado es un certificado autofirmado creado y configurado el programa de instalación de puerta de enlace de Hola. En su lugar, puede usar su propio certificado TLS / SSL. Para más información, consulte la sección sobre la [aplicación de administración de credenciales con un solo clic](#click-once-credentials-manager-app). 

## <a name="next-steps"></a>Pasos siguientes
Para información sobre el rendimiento de la actividad de copia, consulte la [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md).

 
