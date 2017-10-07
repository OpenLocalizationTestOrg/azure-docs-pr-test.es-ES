---
title: "información general sobre la seguridad de base de datos aaaAzure | Documentos de Microsoft"
description: "Este artículo proporciona información general sobre las características de seguridad de base de datos Azure Hola."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: TomSh
ms.openlocfilehash: 13f14b99d15800e85e9906a9d167eb0adf2135de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-overview"></a>Introducción a la seguridad de base de datos de Azure

La seguridad es un aspecto importante a la hora de administrar bases de datos y siempre ha sido una prioridad para Azure SQL Database. Azure SQL Database admite la seguridad de conexión con las reglas de firewall y el cifrado de conexión. Es compatible con la autenticación mediante nombre de usuario y contraseña y con la autenticación de Azure Active Directory, que usa las identidades administradas por Azure Active Directory. La autorización usa el control de acceso basado en roles.

La base de datos de SQL Azure admite el cifrado mediante la realización de cifrado en tiempo real y el descifrado de las bases de datos, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin necesidad de cambios toohello aplicación.

Microsoft proporciona otras formas de datos de empresa de tooencrypt:

-   Nivel de celda columnas específicas de cifrado tooencrypt o incluso las celdas de datos con distintas claves de cifrado.
-   Si necesita un módulo de seguridad de hardware o la administración central de la jerarquía de claves de cifrado, considere la posibilidad de usar Azure Key Vault con SQL Server en una máquina virtual de Azure.
-   Always Encrypted (actualmente en versión preliminar) realiza cifrado transparente tooapplications y permite a los clientes tooencrypt datos confidenciales en aplicaciones de cliente sin compartir claves de cifrado de hello con base de datos de SQL.

Auditoría de base de datos de SQL Azure permite que las empresas toorecord eventos tooan auditoría de inicio de sesión de almacenamiento de Azure. Auditoría de base de datos de SQL Server también se integra con análisis e informes de obtención de detalles de toofacilitate de Microsoft Power BI.

 Las bases de datos de SQL Azure pueden ser toosatisfy estrechamente protegida más legales o requisitos de seguridad, como HIPAA, ISO 27001/27002 y PCI DSS nivel 1, entre otros. Una lista actualizada de certificaciones de cumplimiento de normas de seguridad está disponible en hello [sitio de Microsoft Azure Trust Center](http://azure.microsoft.com/support/trust-center/services/).

Este artículo le guía a través de conceptos básicos de Hola de proteger las bases de datos SQL de Microsoft Azure para estructurado, Tabular y los datos relacionales. En concreto, este artículo le ayudará a empezar a trabajar con los recursos necesarios para proteger los datos, controlar el acceso y realizar una supervisión proactiva.

En este artículo de información general de seguridad de base de datos de Azure se centra en hello siguientes áreas:

-   Protección de datos
-   Control de acceso
-   Supervisión proactiva
-   Administración de seguridad centralizada
-   Azure Marketplace

## <a name="protect-data"></a>Protección de datos

SQL Database protege los datos mediante el cifrado de los datos en movimiento a través de [Seguridad de la capa de transporte](https://support.microsoft.com/kb/3135244), de los datos en reposo a través de [Cifrado de datos transparente](http://go.microsoft.com/fwlink/?LinkId=526242) y de los datos de uso a través de [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx).

En esta sección hablaremos de:

-   Cifrado en movimiento
-   Cifrado en reposo
-   Cifrado en uso (cliente)

Para otro tooencrypt formas los datos, tenga en cuenta:

-   [Cifrado de nivel de celda](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt columnas específicas o incluso las celdas de datos con distintas claves de cifrado.
-   Si necesita un módulo de seguridad de hardware o la administración central de la jerarquía de claves de cifrado, considere la posibilidad de usar [Azure Key Vault con SQL Server en una máquina virtual de Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

### <a name="encryption-in-motion"></a>Cifrado en movimiento

Un problema común para todas las aplicaciones cliente/servidor es la necesidad de Hola para proteger la privacidad cuando mueve los datos a través de redes públicas y privadas. Si no se cifran los datos que se transfieren a través de una red, no hay posibilidad de Hola que se pueden capturar y robo por los usuarios no autorizados. Cuando se trabaja con los servicios de base de datos, deberá toomake seguro de que los datos se cifran entre Hola base de datos cliente y servidor, así como entre servidores de base de datos que se comunican entre sí y con las aplicaciones de nivel intermedio.

Uno de los problemas existentes a la hora de administrar una red es el de proteger los datos que se envían entre las aplicaciones a través de una red que no es de confianza. Puede usar [TLS/SSL](https://docs.microsoft.com/windows-server/security/tls/transport-layer-security-protocol) tooauthenticate servidores y clientes y, a continuación, usarla tooencrypt mensajes entre las partes de hello autenticado.

En el proceso de autenticación de hello, un cliente TLS/SSL envía un servidor TLS/SSL de tooa de mensaje y servidor hello responde con información de hello ese servidor hello necesita tooauthenticate propio. Hola cliente y servidor realizan un intercambio adicional de claves de sesión y Hola extremos del cuadro de diálogo de autenticación. Cuando se completa la autenticación, puede empezar comunicación segura SSL entre el servidor de Hola y cliente de hello mediante claves de cifrado simétrico de Hola que se establecen durante el proceso de autenticación de Hola.

Todas las conexiones tooAzure base de datos SQL requiere el cifrado (SSL/TLS) en todo momento mientras los datos están "en tránsito" tooand de base de datos de Hola. SQL Azure usa clientes y servidores de tooauthenticate TLS/SSL y, a continuación, utilizarlo tooencrypt mensajes entre las partes de hello autenticado. En la cadena de conexión de la aplicación, debe especificar parámetros tooencrypt Hola conexión y no tootrust Hola servidor certificado (Esto se realiza automáticamente si copia la cadena de conexión de hello Portal clásico de Azure), en caso contrario Hola will de conexión No comprobar la identidad de saludo del servidor de Hola y serán susceptibles de sufrir ataques de demasiado "man-in-the-middle". Para el controlador ADO.NET, por ejemplo, estos parámetros de cadena de conexión hello son Encrypt = True y TrustServerCertificate = False.

### <a name="encryption-at-rest"></a>Cifrado en reposo
Puede tomar varias bases de datos de hello segura de toohelp de precauciones, como diseñar un sistema seguro, cifrar los activos confidenciales e instalar un firewall alrededor de los servidores de base de datos de Hola. Sin embargo, en un escenario donde se diera el caso de medios físicos de hello (por ejemplo, unidades de disco o cintas de copia de seguridad), un tercero malintencionado puede simplemente restaurar o adjuntar la base de datos de Hola y examinar los datos de Hola.

Una solución tooencrypt Hola datos confidenciales en la base de datos de Hola y protege las claves de hello tooencrypt usado Hola datos con un certificado. Esto evita que cualquiera que carezca de las claves de hello del uso de datos de hello, pero este tipo de protección debe planearse.

toosolve este problema, SQL Server y SQL Azure admite [cifrado de datos transparente (TDE)](https://docs.microsoft.com/sql/relational-databases/securityrecryption/transparent-data-encryption-tde). El TDE cifra los archivos de datos de SQL Server y Azure SQL Database, conocidos como datos de cifrado en reposo.

Cifrado de datos transparente de bases de datos de SQL Azure le ayuda a protegerse contra amenazas de Hola de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de la base de datos de hello, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin necesidad de realizar cambios aplicación de toohello.  

TDE cifra almacenamiento Hola de toda una base de datos mediante el uso de una clave de cifrado de base de datos de hello llamado de clave simétrica. En la base de datos de SQL, clave de cifrado de base de datos de hello está protegido por un certificado de servidor integrado. certificado de servidor integrado de Hello es único para cada servidor de base de datos SQL.

Si una base de datos está en una relación de GeoDR, está protegida por una clave diferente en cada servidor. Si hay dos bases de datos conectado toohello mismo servidor, comparten Hola mismo certificado integrado. Microsoft alterna automáticamente estos certificados al menos cada 90 días. Para obtener una descripción general de TDE, vea [Cifrado de datos transparente (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde).

### <a name="encryption-in-use-client"></a>Cifrado en uso (cliente)

La mayoría de las infracciones de datos implican robo de Hola de datos críticos, como números de tarjeta de crédito o información de identificación personal. Las bases de datos pueden representar tesoros repletos de información confidencial. Pueden contener datos personales de los clientes, información confidencial sobre la competencia y propiedad intelectual. Los datos perdidos o robados (sobre todo los datos de los clientes) pueden comportar daños de marca, desventajas competitivas e importantes sanciones, incluso demandas.

![Always Encrypted](./media/azure-databse-security-overview/azure-database-fig1.png)

[Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) es un característica diseñada tooprotect datos confidenciales, como números de tarjeta de crédito o números de identificación nacional (por ejemplo, Estados Unidos números de seguridad social), almacenados en las bases de datos de la base de datos de SQL Azure o SQL Server. Always Encrypted permite a los clientes tooencrypt datos confidenciales en aplicaciones de cliente y nunca revela toohello de claves de cifrado de hello motor de base de datos (base de datos SQL o SQL Server).

Always Encrypted proporciona una separación entre aquellos que poseen los datos de hello (y pueden verlos) y aquellos usuarios que administran datos de hello (pero no deberían tener acceso). Al asegurar que los administradores de base de datos local, los operadores de base de datos de nube y otros con privilegios elevados, pero los usuarios no autorizados, no pueden tener acceso a datos de hello cifrado,

Además, Always Encrypted realiza cifrado transparente tooapplications. Un controlador habilitado para Always Encrypted instalado en el equipo cliente de Hola para que puede cifrar y descifrar datos confidenciales de la aplicación de cliente de hello automáticamente. Hola controlador cifra los datos de hello en columnas confidenciales antes de pasar datos de hello toohello motor de base de datos y vuelve a escribir las consultas automáticamente para que se conserve la aplicación de hello semántica toohello. De forma similar, driver Hola descifra de forma transparente datos almacenados en columnas de la base de datos cifrada, contenidas en los resultados de consulta.

## <a name="access-control"></a>Control de acceso
seguridad tooprovide, base de datos SQL controla el acceso con reglas de firewall limitar conectividad por dirección IP, los mecanismos de autenticación que requieren los usuarios tooprove su identidad, mecanismos de autorización y limitar las acciones de toospecific de los usuarios y los datos.

### <a name="database-access"></a>Acceso a la base de datos

Protección de datos comienza con el control de acceso a los datos tooyour. Centro de datos de Hello hospedar sus datos administra el acceso físico, aunque puede configurar un seguridad toomanage del firewall en la capa de red Hola. También puede controlar el acceso configurando inicios de sesión para la autenticación y definiendo permisos para los roles de servidor y de base de datos.

En esta sección hablaremos de:

-   Firewall y reglas de firewall
-   Autenticación
-   Autorización

#### <a name="firewall-and-firewall-rules"></a>Firewall y reglas de firewall

Microsoft Azure SQL Database ofrece un servicio de base de datos relacional para Azure y otras aplicaciones basadas en Internet. toohelp proteger los datos, firewalls impedir que todos los servidores de base de datos de access tooyour hasta que especifique qué equipos tienen permiso. firewall de Hello otorga toodatabases de acceso basado en hello procedentes de la dirección IP de cada solicitud. Para más información, consulte [Introducción a las reglas de firewall de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

Hola [base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/) servicio solamente está disponible a través del puerto TCP 1433. tooaccess una base de datos de SQL desde el equipo, asegúrese de que el firewall del equipo cliente permite la comunicación de TCP de salida en el puerto TCP 1433. Si no es necesario para otras aplicaciones, bloquee las conexiones entrantes en el puerto TCP 1433.

#### <a name="authentication"></a>Autenticación

Autenticación de base de datos SQL refiere toohow demostrar su identidad cuando se conecta la base de datos de toohello. SQL Database admite dos tipos de autenticación:

-   **Autenticación de SQL:** se crea una cuenta de inicio de sesión único cuando se crea una instancia SQL lógica, llamado hello cuenta del suscriptor de base de datos de SQL. Esta cuenta se conecta mediante la [autenticación de SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview) (nombre de usuario y contraseña). Esta cuenta es que un administrador en la instancia de servidor lógico de Hola y en todas las bases de datos de usuario adjunta toothat instancia. permisos de Hola de hello cuenta del suscriptor no pueden estar restringidos. Solo puede existir una de estas cuentas.
-   **Autenticación de Active Directory Azure:** [autenticación de Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication) es un mecanismo de conexión tooMicrosoft base de datos de SQL Azure y almacenamiento de datos de SQL mediante el uso de identidades en Azure Active Directory ( Azure AD). Esto permite toocentrally administrar identidades de los usuarios de base de datos.

![Autenticación](./media/azure-databse-security-overview/azure-database-fig2.png)

 Ventajas de la autenticación de Azure Active Directory:
  - Proporciona una autenticación de servidor alternativo tooSQL.
  - También ayuda a detener la proliferación de Hola de identidades de usuario entre los servidores de base de datos y permite la rotación de contraseña en un único lugar.
  - Puede administrar los permisos de la base de datos usando grupos externos (Azure Active Directory).
  - Puede eliminar el almacenamiento de contraseñas mediante la habilitación de la autenticación integrada de Windows y otras formas de autenticación compatibles con Azure Active Directory.

#### <a name="authorization"></a>Autorización
[Autorización](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins) hace referencia toowhat puede hacer un usuario dentro de una base de datos de SQL Azure, y esto se controla mediante la base de datos de su cuenta de usuario [las pertenencias a roles](https://msdn.microsoft.com/library/ms189121) y [permisos de nivel de objeto](https://msdn.microsoft.com/library/ms191291.aspx). La autorización es el proceso Hola para determinar qué recursos susceptibles de protegerse puede tener acceso una entidad de seguridad y qué operaciones se permiten a esos recursos.

### <a name="application-access"></a>Acceso a las aplicaciones

En esta sección hablaremos de:

-   Enmascaramiento de datos dinámicos
-   Seguridad de nivel de fila

#### <a name="dynamic-data-masking"></a>Enmascaramiento de datos dinámicos
Un representante del servicio en un centro de llamadas puede identificar a los llamadores mediante varios dígitos de su número del seguro social o un número de tarjeta de crédito, pero esos elementos no deben estar completamente los datos expuestos a toohello representante del servicio.

Puede definir una regla de enmascaramiento que enmascare todos excepto Hola los últimos cuatro dígitos de cualquier número del seguro social o un número de tarjeta de crédito en el conjunto de resultados de Hola de cualquier consulta.

![Enmascaramiento de datos dinámicos](./media/azure-databse-security-overview/azure-database-fig3.png)

Como otro ejemplo, una máscara de datos apropiados puede ser datos de información personal identificable (PII) de tooprotect definido, por lo que un desarrollador puede realizar consultas en entornos de producción para resolver problemas sin infringir las normativas de cumplimiento.

[Base de datos de enmascaramiento dinámico SQL](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started) limita la exposición de información confidencial ocultándolos toonon privilegios a los usuarios. Enmascaramiento dinámico de datos es compatible con la versión de Hola V12 de base de datos de SQL Azure.

[Enmascaramiento dinámico de datos](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking) ayuda a evitar que los datos de toosensitive de acceso no autorizado, permitiéndole toodesignate cuánto Hola confidencial tooreveal con un impacto mínimo en el nivel de aplicación Hola. Es una característica de seguridad basada en directivas que oculta los datos confidenciales Hola Hola conjunto de resultados de una consulta de campos de la base de datos designada, Hola datos en la base de datos de hello no cambian.


> [!Note]
> Enmascaramiento dinámico de datos puede configurarse Hola, Administrador de base de datos de Azure, el Administrador de servidor o roles de seguridad responsable de seguridad.

#### <a name="row-level-security"></a>Seguridad de nivel de fila
Otro requisito de seguridad habitual de las bases de datos multiinquilino es la [seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131.aspx). Esta característica permite toocontrol toorows de acceso en una tabla de base de datos basada en características de Hola de usuario de Hola que se ejecuta una consulta (por ejemplo, grupo pertenencia o contexto de ejecución).

![Seguridad de nivel de fila](./media/azure-databse-security-overview/azure-database-fig4.png)

lógica de la restricción de Hello acceso está ubicada en el nivel de base de datos de hello en lugar de estar alejado de los datos de hello en otro nivel de aplicación. sistema de bases de datos de Hello aplica restricciones de acceso de hello cada vez que se intenta que acceder a los datos desde cualquier nivel. Esto hace el sistema de seguridad más sólido y confiable que reduce la superficie Hola de su sistema de seguridad.

La seguridad de nivel de fila introduce el control de acceso basado en predicados. Ofrece una evaluación flexible, centralizada y basada en predicados que puede tener en cuenta metadatos o cualquier otro criterio Hola administrador determine como apropiada. predicado de Hola se usa como un criterio toodetermine si el usuario de hello tiene datos de toohello de saludo acceso adecuado en función de atributos de usuario o no. El control de acceso basado en etiquetas se puede implementar mediante el control de acceso basado en predicados.

## <a name="proactive-monitoring"></a>Supervisión proactiva
SQL Database protege los datos proporcionando capacidades de **auditoría** y **detección de amenazas**.

### <a name="auditing"></a>Auditoría
Auditoría de base de datos de SQL Server aumenta la capacidad toogain una visión general eventos y los cambios que se producen dentro de la base de datos de hello, incluidas las actualizaciones y las consultas en datos Hola.

[Auditoría de base de datos de SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-auditing-get-started) realiza un seguimiento de eventos de base de datos y escribe el registro de auditoría tooan en su cuenta de almacenamiento de Azure. La auditoría puede ayudarle a mantener el cumplimiento de normativas, comprender la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o infracciones de seguridad sospechosas. Auditoría permite y facilita estándares de cumplimiento toocompliance pero no garantiza el cumplimiento de normas.

La auditoría de SQL Database le permite:

-   **Conservar** una traza de auditoría de eventos seleccionados. Puede definir categorías de base de datos acciones toobe auditado.
-   **Informar** sobre la actividad de la base de datos. Puede usar los informes preconfigurados y un tooget de panel a trabajar rápidamente con actividad y los informes de eventos.
-   **Analizar** informes. Puede buscar eventos sospechosos, actividades inusuales y tendencias.

Existen dos métodos de auditoría:

-   **Auditoría de blobs** -se escriben los registros tooAzure almacenamiento de blobs. Es el método de auditoría más reciente, que proporciona mayor rendimiento, admite auditoría de nivel de objeto de mayor granularidad y es más rentable.
-   **Auditoría de tabla** -tooAzure el almacenamiento de tablas se escriben los registros.

### <a name="threat-detection"></a>Detección de amenazas
La [detección de amenazas de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection) detecta actividades sospechosas que indican posibles amenazas de seguridad. La detección de amenazas permite toorespond toosuspicious eventos de base de datos de hello, como las inserciones de SQL, cuando se producen. Proporciona alertas y permite el uso de Hola de auditoría de base de datos de SQL Azure tooexplore eventos sospechosos Hola.

![Detección de amenazas](./media/azure-databse-security-overview/azure-database-fig5.jpg)

Por ejemplo, inyección de código SQL es uno de hello Web aplicación problemas de seguridad comunes en hello Internet, aplicaciones usadas tooattack controladas por datos. Los atacantes aprovechar aplicación vulnerabilidades tooinject instrucciones SQL malintencionadas en campos de entrada de la aplicación, infracción o modificar datos en la base de datos de Hola.

Los responsables de seguridad u otros administradores designados pueden recibir una notificación inmediata sobre las actividades sospechosas en las bases de datos cuando se producen. Cada notificación proporciona detalles de actividad sospechosa de Hola y recomienda cómo toofurther investigar y mitigar la amenaza de Hola.        

## <a name="centralized-security-management"></a>Administración de seguridad centralizada

[Centro de seguridad de Azure](https://azure.microsoft.com/documentation/services/security-center/) le ayuda a evitar, detectar y responder toothreats. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

[Centro de seguridad](https://docs.microsoft.com/azure/security-center/security-center-sql-database) ayuda a proteger los datos en la base de datos SQL proporcionando visibilidad sobre seguridad Hola de todos los servidores y bases de datos. Con Security Center puede realizar estas tareas:

-   Definir las directivas de auditoría y cifrado de SQL Database
-   Supervisión de seguridad de Hola de recursos de base de datos SQL en todas sus suscripciones.
-   Identificar y corregir problemas de seguridad rápidamente
-   Integrar las alertas de [detección de amenazas de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection)
-   El Centro de seguridad admite el acceso basado en rol.

## <a name="azure-marketplace"></a>Azure Marketplace

Hello Azure Marketplace es un marketplace de aplicaciones y servicios en línea que permite a las nuevas empresas y software independiente (ISV) toooffer sus clientes de tooAzure soluciones alrededor de Hola a todos.
Hello Azure Marketplace combina ecosistemas de partner de Microsoft Azure en una sola plataforma unificada toobetter servir nuestros clientes y socios. Haga clic en [aquí](https://azuremarketplace.microsoft.com/marketplace/apps?search=Database%20Security&page=1) tooglance productos de seguridad de base de datos disponibles en lugar de mercado de Azure.

## <a name="next-steps"></a>Pasos siguientes

- Obtenga más información sobre la [protección de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
- Obtenga más información sobre [los servicios Azure Security Center y Azure SQL Database](https://docs.microsoft.com/azure/security-center/security-center-sql-database).
- toolearn más información acerca de la detección de amenazas, consulte [detección de amenazas de base de datos de SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
- más información, consulte toolearn [rendimiento de base de datos de SQL mejorar](https://docs.microsoft.com/azure/sql-database/sql-database-performance-tutorial). 
