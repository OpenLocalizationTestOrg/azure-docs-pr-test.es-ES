---
title: 'aaaDatabase seguridad: base de datos de Azure Cosmos | Documentos de Microsoft'
description: "Obtenga información sobre cómo Azure Cosmos DB proporciona protección de bases de datos y seguridad para los datos."
keywords: "seguridad de bases de datos NoSQL, información de seguridad, seguridad de datos, el cifrado de bases de datos, protección de bases de datos, directivas de seguridad, pruebas de seguridad"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: a02a6a82-3baf-405c-9355-7a00aaa1a816
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: mimig
ms.openlocfilehash: 85ffa62f611bfad00bf3fc5dbe536f91f97f1113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-security"></a>Seguridad de base de datos de Azure Cosmos DB

En este artículo se describe prácticas recomendadas de seguridad de base de datos y características clave ofrecen por base de datos de Azure Cosmos toohelp evitar, detectar y responder toodatabase infracciones.
 
## <a name="whats-new-in-azure-cosmos-db-security"></a>Novedades en la seguridad de Azure Cosmos DB

El cifrado en reposo ahora está disponible para los documentos y copias de seguridad almacenados en Azure Cosmos DB en todas las regiones de Azure. El cifrado en reposo se aplica automáticamente a los clientes nuevos y existentes de estas regiones. No hay ninguna necesidad de tooconfigure nada; y obtendrá Hola mismo latencia grande, el rendimiento, disponibilidad y funcionalidad igual que antes con ventaja Hola de conocer los datos están seguro y protegido con cifrado en reposo.

## <a name="how-do-i-secure-my-database"></a>¿Cómo puedo proteger mi base de datos? 

Seguridad de los datos constituye una responsabilidad compartida entre clientes de Hola y el proveedor de base de datos. Función de proveedor de base de datos de Hola que elija, cantidad de Hola de responsabilidad que realice puede variar. Si elige una solución local, deberá tooprovide todo tipo de seguridad de toophysical de protección de extremo del hardware - que no es tarea fácil. Si elige un proveedor de bases de datos en la nube PaaS como Azure Cosmos DB, se reduce considerablemente el área de responsabilidad. Hola después de la imagen, tomada prestada de Microsoft [comparten las responsabilidades de la informática en nube](https://aka.ms/sharedresponsibility) notas del producto, se muestra cómo se reduce la responsabilidad con un proveedor de PaaS como base de datos de Azure Cosmos.

![Responsabilidades del cliente y del proveedor de bases de datos](./media/database-security/nosql-database-security-responsibilities.png)

Hola componentes de seguridad de alto nivel en la nube de muestra de diagrama anterior, pero qué elementos ¿necesita tooworry sobre específicamente para la solución de base de datos? ¿Y cómo se puede comparar soluciones tooeach otros? 

Se recomienda Hola siguiente lista de comprobación de requisitos de los sistemas de base de datos toocompare:

- Seguridad de red y la configuración de firewall
- Autenticación de usuarios y controles de usuario muy específicos
- Datos de capacidad tooreplicate globalmente para errores regionales
- Tooanother del centro de capacidad tooperform las conmutaciones por error de datos
- Replicación de datos local dentro de un centro de datos
- Copias de seguridad de datos automáticas
- Restauración de los datos eliminados de las copias de seguridad
- Protección y aislamiento de datos confidenciales
- Supervisión de ataques
- Responde tooattacks
- Restricciones de gobernanza de capacidad toogeo barrera datos tooadhere toodata
- Protección física de los servidores en centros de datos protegidos

Aunque puede parecer obvio, reciente [infracciones de la base de datos a gran escala](http://thehackernews.com/2017/01/mongodb-database-security.html) nos recuerdan de importancia de hello simple pero críticos de hello según los requisitos:
- Servidores revisados que se mantengan actualizados toodate
- Protocolo HTTPS de forma predeterminada/cifrado SSL
- Cuentas administrativas con contraseñas seguras

## <a name="how-does-azure-cosmos-db-secure-my-database"></a>¿Cómo puede proteger Azure Cosmos DB mi base de datos?

Echemos un vistazo volver a Hola precede a lista, ¿cuántos de esos requisitos de seguridad de base de datos de Azure Cosmos proporciona? Todos.

Analicemos cada uno de ellas en detalle.

|Requisito de seguridad|Enfoque de seguridad de Azure Cosmos DB|
|---|---|---|
|Seguridad de las redes|Uso de un servidor de seguridad IP se Hola primera capa de protección toosecure la base de datos. Azure Cosmos DB admite controles de acceso basado en IP orientado a directivas para agregar compatibilidad con el firewall de entrada. los controles de acceso basado en IP Hola son reglas de firewall toohello similares usadas por sistemas de base de datos tradicional, pero se expanden para que una cuenta de base de datos de la base de datos de Azure Cosmos solo es accesible desde un conjunto de aprobados de máquinas o servicios en la nube. <br><br>Base de datos de Azure Cosmos permite tooenable una dirección IP específica (168.61.48.0), un intervalo IP (168.61.48.0/8) y combinaciones de direcciones IP e intervalos. <br><br>Todas las solicitudes procedentes de máquinas que no pertenezcan a esta lista permitida las bloqueará Azure Cosmos DB. Las solicitudes de aprueban máquinas y servicios en la nube, a continuación, deben completar toobe de proceso de autenticación de hello proporcionado recursos de toohello de control de acceso.<br><br>Más información en [Compatibilidad con un firewall de Azure Cosmos DB](firewall-support.md).|
|Autorización|Azure Cosmos DB utiliza el código de autenticación de mensajes basado en hash (HMAC) para la autorización. <br><br>Cada solicitud está en hash con clave de cuenta secreta de Hola y Hola Base64 codificado valor hash subsiguiente se envía con cada base de datos de Cosmos tooAzure de llamada. solicitar toovalidate hello, usos de servicio de base de datos de Azure Cosmos Hola Hola clave secreta correcta y propiedades toogenerate un hash, a continuación, compara el valor de hello con hello en solicitud de saludo. Si coincide con dos valores de hello, operación Hola está autorizado correctamente y se procesa la solicitud de hello, en caso contrario, hay un error de autorización y se rechazó la solicitud de saludo.<br><br>Puede usar un [clave maestra](secure-access-to-data.md#master-keys), o un [token de recurso](secure-access-to-data.md#resource-tokens) permitir que los recursos de tooa de acceso específico, como un documento.<br><br>Obtenga más información en [proteger acceso a recursos de base de datos de Cosmos tooAzure](secure-access-to-data.md).|
|Usuarios y permisos|Con hello [clave maestra](#master-key) para cuenta de hello, puede crear recursos de usuario y permisos de los recursos por base de datos. A [token de recurso](#resource-token) está asociado con un permiso en una base de datos y determina si el usuario de hello tiene acceso (lectura y escritura, de sólo lectura, o ningún acceso) tooan recursos de aplicación de base de datos de Hola. Los recursos de aplicación incluyen colecciones, documentos, datos adjuntos, procedimientos almacenados, desencadenadores y UDF. token de recurso de Hello es, a continuación, usa durante la autenticación tooprovide o denegar el acceso a recursos de toohello.<br><br>Obtenga más información en [proteger acceso a recursos de base de datos de Cosmos tooAzure](secure-access-to-data.md).|
|Integración de Active Directory (RBAC)| También puede proporcionar acceso toohello base de datos cuenta con control de acceso (de índices IAM) Hola portal de Azure, como se muestra en la captura de pantalla de Hola que sigue a esta tabla. IAM proporciona una funcionalidad de control de acceso basado en roles y se integra con Active Directory. Puede usar roles integrados o personalizado para usuarios y grupos, como se muestra en hello después de la imagen.|
|Replicación global|Base de datos de Azure Cosmos ofrece llave en mano distribución global, lo que permite tooreplicate su tooany datos uno de los centros de datos en todo el mundo de Azure con hello haga clic en un botón. Replicación global le permite escalar globalmente y proporcionar acceso de baja latencia tooyour datos alrededor de Hola a todos.<br><br>En el contexto de Hola de seguridad, replicación global garantiza la protección de datos frente a errores regionales.<br><br>Obtenga más información en [Distribución de datos global con DocumentDB](distribute-data-globally.md).|
|Conmutaciones por error regionales|Si se han replicado los datos en más de un centro de datos, Azure Cosmos DB sustituirá automáticamente las operaciones en caso de que se desconecte un centro de datos regional. Puede crear una lista de prioridades de las regiones de conmutación por error con regiones de hello en el que se replican los datos. <br><br>Obtenga más información en [Conmutaciones por error regionales de Azure Cosmos DB](regional-failover.md).|
|Replicación local|Incluso dentro de un solo centro de datos, base de datos de Azure Cosmos replica automáticamente los datos para dar de alta disponibilidad Hola elección de [niveles de coherencia](consistency-levels.md). Esto asegura que haya un  [Acuerdo de Nivel de Servicio de disponibilidad del 99,99 % del tiempo de actividad](https://azure.microsoft.com/support/legal/sla/cosmos-db), que incluye una garantía financiera (algo que no puede proporcionar ningún otro servicio de bases de datos).|
|Copias de seguridad en línea automatizadas|Las copias de seguridad de las bases de datos de Azure Cosmos DB se realizan de manera periódica y se guardan en un almacén con redundancia geográfica. <br><br>Obtenga más información en [Copias de seguridad y restauración automáticas en línea con Azure Cosmos DB](online-backup-and-restore.md).|
|Restauración de los datos eliminados|Hello automatizadas de copias de seguridad en línea pueden ser utilizados toorecover datos que ha eliminado accidentalmente una demasiado ~ 30 días posteriores a eventos de Hola. <br><br>Obtenga más información en [Copias de seguridad y restauración automáticas en línea con Azure Cosmos DB](online-backup-and-restore.md).|
|Protección y aislamiento de datos confidenciales|Todos los datos en regiones de hello enumerados en [What's new?](#whats-new) ahora se cifran en reposo.<br><br>PII y otros datos confidenciales pueden ser colecciones toospecific aislado y lectura / escritura o acceso de solo lectura puede ser toospecific limitado a los usuarios.|
|Supervisión de los ataques|Mediante el uso de registros de actividad y de auditoría, puede supervisar su cuenta para detectar actividad normal y anómala. Puede ver qué operaciones se realizaron en los recursos, que inicia la operación de hello, cuando se ha producido la operación de hello, estado de Hola de operación de Hola y mucho más, como se muestra en la captura de pantalla de hello sigue a esta tabla.|
|Responder tooattacks|Una vez que se ha puesto en contacto con soporte técnico de Azure tooreport un ataque potencial, se inicia un proceso de respuesta a incidentes paso 5. objetivo de Hola de proceso del paso 5 de hello es toorestore seguridad de servicio normal y las operaciones tan pronto como sea posible después de que se detecta un problema y se inicia una investigación.<br><br>Obtenga más información en [respuestas de seguridad de Microsoft Azure en hello en la nube](https://aka.ms/securityresponsepaper).|
|Geovalla|Azure Cosmos DB garantiza el cumplimiento y la gobernanza de datos para regiones soberana (por ejemplo, Alemania y US Gov).|
|Instalaciones protegidas|Los datos de Azure Cosmos DB se almacenan en los SSD de los centros de datos protegidos de Azure.<br><br>Obtenga información sobre los [centros de datos globales de Microsoft](https://www.microsoft.com/en-us/cloud-platform/global-datacenters).|
|HTTPS, SSL y cifrado TLS|Todas las interacciones de Azure Cosmos DB de cliente a servicio exigen los protocolos SSL o TLS 1.2. Además, para todas las replicaciones dentro de centro de datos y entre ellos se exigen estos protocolos.|
|Cifrado en reposo|Todos los datos almacenados en Azure Cosmos DB se cifran en reposo. Más información en [Cifrado de Azure Cosmos DB en reposo](.\database-encryption-at-rest.md)|
|Servidores revisados|Como una base de datos administrado, base de datos de Azure Cosmos elimina los servidores de toomanage y revisión de necesidad de hello, que se hace automáticamente para usted.|
|Cuentas administrativas con contraseñas seguras|Su disco duro toobelieve se incluso necesario toomention este requisito, pero a diferencia de algunos de nuestros competidores, es imposible toohave una cuenta administrativa con ninguna contraseña en la base de datos de Azure Cosmos.<br><br> La seguridad a través de SSL y autenticación basada en secreto HMAC está incorporada de forma predeterminada.|
|Certificaciones de protección de datos y seguridad|Azure Cosmos DB tiene las certificaciones [ISO 27001](https://www.microsoft.com/en-us/TrustCenter/Compliance/ISO-IEC-27001), [las cláusulas modelo de la Comisión Europea (EUMC)](https://www.microsoft.com/en-us/TrustCenter/Compliance/EU-Model-Clauses) e [HIPAA](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA). Hay pendientes más certificaciones.|

Hello captura de pantalla siguiente muestra la integración de Active directory (RBAC) con control de acceso (de índices IAM) en Hola portal de Azure: ![(de índices IAM) de control de acceso en hello portal de Azure: demostrar la seguridad de base de datos](./media/database-security/nosql-database-security-identity-access-management-iam-rbac.png)

registros de actividad toomonitor su cuenta y Hello captura de pantalla siguiente muestra cómo puede utilizar el registro de auditoría: ![registros de actividad para la base de datos de Azure Cosmos](./media/database-security/nosql-database-security-application-logging.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de las claves maestras y tokens de recursos, consulte [tooAzure de acceso de proteger datos de la base de datos de Cosmos](secure-access-to-data.md).

Si quiere saber más sobre las certificaciones de Microsoft, visite el [Centro de confianza de Azure](https://azure.microsoft.com/support/trust-center/).
