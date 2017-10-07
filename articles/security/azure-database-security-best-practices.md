---
title: "prácticas recomendadas de seguridad de base de datos de aaaAzure | Documentos de Microsoft"
description: "En este artículo se proporciona un conjunto de prácticas recomendadas para la reforzar la seguridad de las bases de datos de Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: tomsh
ms.openlocfilehash: 78984291e8f74879c7f738e2ce3176c4be18d154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-best-practices"></a>Procedimientos recomendados para la seguridad de las bases de datos de Azure

La seguridad es un aspecto importante a la hora de administrar bases de datos y siempre ha sido una prioridad para Azure SQL Database. Las bases de datos pueden ser toohelp estrechamente protegido cumplen más legales o requisitos de seguridad, como HIPAA, ISO 27001/27002 y PCI DSS nivel 1, entre otros. Una lista actualizada de certificaciones de cumplimiento de normas de seguridad está disponible en hello [sitio Microsoft Trust Center](http://azure.microsoft.com/support/trust-center/services/). También puede elegir tooplace las bases de datos en centros de datos de Azure específica en función de los requisitos normativos.

En este artículo veremos un conjunto de procedimientos recomendados de seguridad de las bases de datos de Azure. Estas prácticas recomendadas se derivan de nuestra experiencia con la seguridad de base de datos de Azure y experiencias de Hola de clientes como usted mismo.

Para cada procedimiento recomendado, explicaremos:

-   ¿Qué recomienda Hola
-   ¿Por qué desea tooenable este procedimiento recomendado
-   ¿Qué podría ser resultado de hello si no se recomienda tooenable Hola
-   ¿Cómo puede obtener información práctica recomendada de hello tooenable

En este artículo de prácticas recomendadas de seguridad de base de datos de Azure se basa en una opinión de consenso y capacidades de la plataforma Windows Azure y conjuntos de características tal como aparecen en tiempo de Hola que se escribió este artículo. Las opiniones y las tecnologías que cambian con el tiempo y este artículo será esos cambios se actualizaron en un tooreflect de forma periódica.

Los procedimientos recomendados de seguridad para las bases de datos de Azure descritos en este artículo incluyen:

-   Usar acceso de base de datos de toorestrict de reglas de firewall
-   Habilitación de la autenticación de bases de datos
-   Protección de los datos con cifrado
-   Protección de los datos en tránsito
-   Habilitación de la auditoría de bases de datos
-   Habilitación de la detección de amenazas para las bases de datos


## <a name="use-firewall-rules-toorestrict-database-access"></a>Usar acceso de base de datos de toorestrict de reglas de firewall

Microsoft Azure SQL Database ofrece un servicio de base de datos relacional para Azure y otras aplicaciones basadas en Internet. seguridad de acceso de tooprovide, base de datos SQL controla el acceso con reglas de firewall limitar conectividad por dirección IP, los mecanismos de autenticación que requieren los usuarios tooprove su identidad, mecanismos de autorización y limitar las acciones de toospecific de los usuarios y los datos. Firewalls impedir que todos los servidores de base de datos de access tooyour hasta que especifique qué equipos tienen permiso. firewall de Hello otorga toodatabases de acceso basado en hello procedentes de la dirección IP de cada solicitud.

![Reglas de firewall](./media/azure-database-security-best-practices/azure-database-security-best-practices-Fig1.png)

Hola servicio de base de datos de SQL Azure solo está disponible a través del puerto TCP 1433. tooaccess una base de datos de SQL desde el equipo, asegúrese de que el firewall del equipo cliente permite la comunicación de TCP de salida en el puerto TCP 1433. Si no es necesario para otras aplicaciones, bloquee las conexiones entrantes en el puerto TCP 1433 mediante reglas de firewall.

Como parte del proceso de conexión de hello, conexiones de máquinas virtuales de Azure son tooa redirigida otra dirección IP y el puerto, único para cada rol de trabajador. número de puerto de Hello es en el intervalo de hello entre too11999 11000. Para obtener más información sobre los puertos TCP, consulte [Puertos más allá del 1433 para ADO.NET 4.5 y SQL Database2](https://docs.microsoft.com/azure/sql-database/sql-database-develop-direct-route-ports-adonet-v12).

> [!Note]
> Para más información general acerca de las reglas de firewall de SQL Database, consulte [Introducción a las reglas de firewall de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

## <a name="enable-database-authentication"></a>Habilitación de la autenticación de bases de datos
SQL Database admite dos tipos de autenticación: la de SQL y la de Azure Active Directory.

La **autenticación de SQL** se recomienda en los casos siguientes:

-   Permite a los entornos de SQL Azure toosupport con sistemas operativos mixtos, donde todos los usuarios no son autenticados por un dominio de Windows.
-   Permite que aplicaciones más antiguas de SQL Azure toosupport y aplicaciones proporcionadas por terceros que requieren autenticación de SQL Server.
-   Permite a los usuarios tooconnect desde dominios desconocidos o que no se confía. Por ejemplo, una aplicación que los clientes establecidos se conectan con asigna tooreceive Hola estado de sus pedidos a los inicios de sesión de SQL Server.
-   Permite toosupport de SQL Azure en aplicaciones basadas en Web donde los usuarios crear sus propias identidades.
-   Permite que el software toodistribute a los desarrolladores según sus aplicaciones mediante el uso de una jerarquía de permisos compleja conocido, preestablecido inicios de sesión de SQL Server.

> [!Note]
> Sin embargo, la autenticación de SQL Server no puede usar el protocolo de seguridad Kerberos.

Si usa la **autenticación de SQL**, debe:

-   Administrar credenciales seguras Hola.
-   Proteger las credenciales de hello en la cadena de conexión de Hola.
-   (Potencialmente) proteger las credenciales de Hola Hola Web server toohello base de datos se transmiten por red Hola. Para obtener más información, consulte [Cómo: conectar tooSQL Server mediante la autenticación de SQL en ASP.NET 2.0](https://msdn.microsoft.com/library/ms998300.aspx).

**Autenticación de Azure Active Directory** es un mecanismo de conexión tooMicrosoft base de datos de SQL Azure y [almacenamiento de datos SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) mediante el uso de identidades en Azure Active Directory (Azure AD). Con la autenticación de Azure AD, puede administrar de forma centralizada las identidades de Hola de usuarios de base de datos y otros servicios de Microsoft en una ubicación central. Administración del identificador central proporciona un único lugar a los usuarios de base de datos de toomanage y simplifica la administración de permisos. Ventajas Hola siguientes:

-   Proporciona una autenticación de servidor alternativo tooSQL.
-   Ayuda a detener la proliferación de Hola de identidades de usuario entre los servidores de base de datos.
-   Permite la rotación de contraseñas en un solo lugar.
-   Los clientes pueden administrar los permisos de la base de datos con grupos externos (AAD).
-   Puede eliminar el almacenamiento de contraseñas mediante la habilitación de la autenticación integrada de Windows y otras formas de autenticación compatibles con Azure Active Directory.
-   Autenticación de Azure AD utiliza las identidades de tooauthenticate de usuarios de base de datos independiente en el nivel de base de datos de Hola.
-   Azure AD admite autenticación basada en el símbolo (token) para aplicaciones que se conectan tooSQL base de datos.
-   La autenticación de Azure AD es compatible con ADFS (federación de dominio) o la autenticación nativa de usuario y contraseña para una instancia de Azure Active Directory local sin sincronización de dominios.
-   Azure AD admite conexiones de SQL Server Management Studio que usan la autenticación universal de Active Directory, lo cual incluye Multi-Factor Authentication (MFA). MFA incluye una sólida autenticación con una gama de sencillas opciones de comprobación: llamada de teléfono, mensaje de texto, tarjetas inteligentes con PIN o notificación de aplicación móvil. Para obtener más información, consulte [Compatibilidad de SSMS con Azure AD MFA con Base de datos SQL y Almacenamiento de datos SQL](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).

pasos de configuración de Hello incluyen hello siguiendo los procedimientos tooconfigure y utilice autenticación de Azure Active Directory.

-   Cree y rellene una instancia de Azure AD.
-   Opcional: Asociar o cambiar Hola active directory que está asociada actualmente con la suscripción de Azure.
-   Cree un administrador de Azure Active Directory para Azure SQL Server o para [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
- Configure los equipos cliente.
-   Crear usuarios de base de datos independiente en la base de datos asignado tooAzure identidades de AD.
-   Conectar la base de datos de tooyour mediante el uso de identidades de Azure AD.

Puede encontrar más detalles [aquí](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

## <a name="protect-your-data-using-encryption"></a>Protección de los datos con cifrado

[Cifrado de datos transparente de base de datos de SQL Azure (TDE)](https://msdn.microsoft.com/library/dn948096.aspx) ayuda a protegerse contra amenazas de Hola de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de base de datos de hello, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin requiere la aplicación de toohello de cambios. TDE cifra almacenamiento Hola de toda una base de datos mediante el uso de una clave de cifrado de base de datos de hello llamado de clave simétrica.

Incluso cuando se cifra el almacenamiento en su totalidad hello, es muy importante tooalso cifrar la base de datos. Se trata de una implementación de defensa de hello en el enfoque de profundidad para la protección de datos. Si está usando la base de datos de SQL Azure y desea tooprotect datos confidenciales, como la tarjeta de crédito o números de seguridad social, puede cifrar las bases de datos con cifrado de AES de 256 bits de 140-2 validado de FIPS que cumpla los requisitos de Hola de muchos estándares del sector (por ejemplo, HIPAA, PCI).

Es importante toounderstand archivos relacionados con demasiado[extensión (BPE) del grupo de búferes](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension) no se cifran cuando una base de datos se cifra con TDE. Debe usar herramientas de cifrado de nivel de sistema de archivos como [BitLocker](https://technet.microsoft.com/library/cc732774) o hello [sistema de archivos cifrados (EFS)](https://technet.microsoft.com/library/cc700811.aspx) para BPE archivos relacionados.

Desde un usuario autorizado, como un administrador de seguridad o una base de datos puede tener acceso a datos de hello incluso si la base de datos de Hola se cifra con TDE, también debe seguir las recomendaciones de Hola a continuación:

-   Habilitar la autenticación de SQL en el nivel de base de datos de Hola.
-   Use la autenticación de Azure AD mediante [roles RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).
-   Los usuarios y las aplicaciones deben usar tooauthenticate cuentas independientes. De esta forma, puede limitar los permisos de hello concedidas toousers y las aplicaciones y reducir los riesgos de Hola de actividad malintencionada.
-   Implemente seguridad de nivel de base de datos mediante el uso de roles de base de datos fija (por ejemplo, db_datareader o db_datawriter), o bien puede crear roles personalizados para su aplicación toogrant objetos de base de datos de tooselected permisos explícitos.

Para otro tooencrypt formas los datos, tenga en cuenta:

-   [Cifrado de nivel de celda](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt columnas específicas o incluso las celdas de datos con distintas claves de cifrado.
-   Cifrado en uso con tecnología Always Encrypted: [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) permite que los clientes tooencrypt los datos confidenciales en aplicaciones de cliente y nunca revelan toohello de claves de cifrado de hello motor de base de datos (base de datos SQL o SQL Server). Como resultado, Always Encrypted proporciona una separación entre aquellos que poseen los datos de hello (y pueden verlos) y aquellos usuarios que administran datos de hello (pero no deberían tener acceso).
-   Mediante la seguridad de nivel de fila: seguridad de nivel de fila permite a los clientes toocontrol acceso toorows en una tabla de base de datos basada en características de Hola de usuario de Hola que se ejecuta una consulta (por ejemplo, grupo pertenencia o contexto de ejecución). Para más información, consulte [Seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131).

## <a name="protect-data-in-transit"></a>Protección de los datos en tránsito
Proteger los datos en tránsito debe ser una parte esencial de su estrategia de protección de datos. Puesto que los datos se va a mover y hacia atrás desde varias ubicaciones, recomendación general hello es que siempre que usan los datos de tooexchange de protocolos SSL/TLS en diferentes ubicaciones. En algunas circunstancias, puede que desee canal de tooisolate Hola toda comunicación entre el local y la nube infraestructura mediante el uso de una red privada virtual (VPN).

Para los datos que se desplazan entre la infraestructura local y Azure, debe plantearse usar medidas de seguridad apropiadas, como HTTPS o VPN.

Las organizaciones que necesitan tener acceso toosecure desde varias estaciones de trabajo locales encuentra tooAzure, usar [Azure VPN de sitio a sitio](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Para las organizaciones que necesitan toosecure acceso desde estaciones de trabajo individuales encuentra local o remoto tooAzure, considere el uso de [Point-to-Site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Los conjuntos de datos más grandes se pueden mover por medio de un vínculo WAN dedicado de alta velocidad como [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Si elige toouse ExpressRoute, también puede cifrar los datos de hello en el uso de nivel de aplicación de hello [SSL/TLS](https://support.microsoft.com/kb/257591) u otros protocolos para conseguir una protección adicional.

Si interactúa con el almacenamiento de Azure a través de hello Portal de Azure, todas las transacciones se producen a través de HTTPS. [API de REST de almacenamiento](https://msdn.microsoft.com/library/azure/dd179355.aspx) a través de HTTPS, también puede ser usado toointeract con [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) y [base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/).

Las organizaciones que no cumplan tooprotect datos en tránsito sean más susceptibles de [man-in-the-middle ataques](https://technet.microsoft.com/library/gg195821.aspx), [interceptaciones](https://technet.microsoft.com/library/gg195641.aspx) y secuestro de sesión. Estos ataques pueden ser el primer paso de Hola para obtener acceso a los datos tooconfidential.

más información acerca de la opción de VPN de Azure, lea el artículo de hello toolearn [planificación y diseño para la puerta de enlace VPN](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-plan-design).

## <a name="enable-database-auditing"></a>Habilitación de la auditoría de bases de datos
Auditoría de una instancia de hello motor de base de datos de SQL Server o una base de datos individual implica el seguimiento y registro de eventos que se producen en hello motor de base de datos. La auditoría de SQL Server le permite crear auditorías de servidor, que pueden contener especificaciones de auditoría de servidor para los eventos del nivel de servidor así como especificaciones de auditoría de base de datos para los eventos del nivel de base de datos. Eventos auditados se pueden escribir registros de eventos de toohello o tooaudit archivos.

Hay varios niveles de auditoría de SQL Server, según los requisitos legales o de estándares para la instalación. Auditoría de SQL Server proporciona herramientas de Hola y procesos necesarios tooenable, la tienda y ver auditorías en varios objetos de servidor y base de datos.

[Auditoría de base de datos de SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-auditing) realiza un seguimiento de eventos de base de datos y escribe el registro de auditoría tooan en su cuenta de almacenamiento de Azure.

La auditoría puede ayudarle a mantener el cumplimiento de normativas, comprender la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o infracciones de seguridad sospechosas.

Auditoría permite y facilita estándares de cumplimiento toocompliance pero no garantiza el cumplimiento de normas.

toolearn más acerca de la auditoría de base de datos y cómo tooenable, lea el artículo de hello [habilitar la detección de auditoría y de las amenazas en los servidores de SQL Server en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="enable-database-threat-detection"></a>Habilitación de la detección de amenazas para las bases de datos
Detección de amenazas de SQL le permite toodetect y responder a amenazas de toopotential cuando se producen al proporcionar alertas de seguridad en actividades anómalas. Se recibirá una alerta sobre las actividades sospechosas en las bases de datos, posibles vulnerabilidades y ataques de inyección de SQL, así como en patrones anómalos de acceso a bases de datos. Alertas de detección de amenazas de SQL se proporcionan detalles de actividad sospechosa y recomendarán la acción sobre cómo tooinvestigate y mitigar la amenaza de Hola.

Por ejemplo, inyección de código SQL es uno de hello Web aplicación problemas de seguridad comunes en hello Internet, aplicaciones usadas tooattack controladas por datos. Los atacantes aprovechar aplicación vulnerabilidades tooinject instrucciones SQL malintencionadas en campos de entrada de la aplicación, infracción o modificar datos en la base de datos de Hola.

toolearn acerca de cómo tooset la detección de amenazas para la base de datos en hello Azure, vea portal [detección de amenazas de base de datos de SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).

Además, la detección de amenazas de SQL integra las alertas con [Azure Security Center](https://azure.microsoft.com/services/security-center/). Le invitamos tootry márquelo durante 60 días para liberar.

toolearn más información acerca de la detección de amenazas de base de datos y cómo tooenable, lea el artículo de hello [habilitar la detección de auditoría y de las amenazas en los servidores de SQL Server en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="conclusion"></a>Conclusión
Azure Database es una sólida plataforma de base de datos, con una amplia gama de características de seguridad que satisfacen muchos de los requisitos de cumplimiento tanto normativos como organizativos. Puede ayudar a proteger los datos al controlar datos de tooyour de acceso físico de Hola y con una variedad de opciones de seguridad de los datos en el archivo - Hola, columna o nivel de fila con el cifrado de datos transparente, cifrado de nivel de celda o seguridad de nivel de fila. Siempre Encrypted también permite las operaciones en los datos cifrados, simplificando el proceso de Hola de actualizaciones de la aplicación. A su vez, acceso tooauditing registros de actividad de la base de datos SQL proporciona información de Hola que necesita, lo que le tooknow cómo y cuándo se tiene acceso a datos.

## <a name="next-steps"></a>Pasos siguientes
- toolearn más información acerca de las reglas de firewall, consulte [las reglas de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).
- toolearn acerca de los usuarios e inicios de sesión, vea [administrar inicios de sesión](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).
- Para ver un tutorial, consulte [Protección de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
