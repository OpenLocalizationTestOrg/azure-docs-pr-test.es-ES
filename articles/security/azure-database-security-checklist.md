---
title: "lista de comprobación de seguridad de base de datos de aaaAzure | Documentos de Microsoft"
description: "En este artículo se proporciona un conjunto de comprobaciones de la seguridad de Azure Database."
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
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 5e3a69591df3c8508a8707a2d47068342863ce93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-checklist"></a>Lista de comprobación de la seguridad de Azure Database

toohelp mejorar la seguridad, base de datos de Azure incluye una serie de controles de seguridad integrados que puede usar toolimit y controlar el acceso.

Entre ellos se incluyen los siguientes:

-   Un firewall que permite toocreate [las reglas de firewall](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) limitar conectividad por su dirección IP
-   Firewall de nivel de servidor accesible desde Hola portal de Azure
-   Reglas de firewall de nivel de base de datos accesibles desde SSMS
-   Base de datos de una conexión segura tooyour con cadenas de conexión segura
-   Uso de la administración del acceso
-   Cifrado de datos
-   Auditoría de SQL Database
-   Detección de amenazas de SQL Database

## <a name="introduction"></a>Introducción
Informática en la nube requiere nuevos paradigmas de seguridad que son usuarios de la aplicación toomany familiarizado, los administradores de base de datos y los programadores. Como resultado, algunas organizaciones están tooimplement dudas acerca de si una infraestructura de nube para la administración de datos debido a los riesgos de seguridad de tooperceived. Sin embargo, se puede mitigar gran parte de este problema mediante una mejor comprensión de hello las características de seguridad integradas en Microsoft Azure y base de datos de SQL de Microsoft Azure.

## <a name="checklist"></a>Lista de comprobación
Le recomendamos que lea hello [prácticas recomendadas de seguridad de base de datos de Azure](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices) artículo anterior tooreviewing esta lista de comprobación. Una vez que comprenda los procedimientos recomendados de hello estará tooget capaz de hello máximo partido de esta lista de comprobación. A continuación, puede usar este toomake de lista de comprobación confirma que ha accedido por problemas importantes de hello en la seguridad de base de datos de Azure.


|Categoría de la lista de comprobación| Descripción|
| ------------ | -------- |
|**Protección de datos**||
| <br> Cifrado en movimiento o tránsito| <ul><li>[Seguridad de la capa de transporte](https://docs.microsoft.com/en-us/windows-server/security/tls/transport-layer-security-protocol), para el cifrado de datos cuando mueven datos toohello redes.</li><li>Base de datos requiere una comunicación segura desde los clientes basados en hello [TDS (flujo de datos tabulares)](https://msdn.microsoft.com/en-in/library/dd357628.aspx) protocolo a través de TLS (seguridad de la capa de transporte).</li></ul> |
|<br>Cifrado en reposo| <ul><li>[Cifrado de datos transparente](http://go.microsoft.com/fwlink/?LinkId=526242), cuando los datos inactivos se almacenan físicamente en cualquier formato digital.</li></ul>|
|**Control de acceso**||  
|<br> Acceso a la base de datos | <ul><li>[Autenticación](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) (Autenticación de Azure Active Directory). La autenticación de AD usa las identidades administradas por Azure Active Directory.</li><li>[Autorización](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) conceder a los usuarios Hola privilegios mínimos necesarios.</li></ul> |
|<br>Acceso a las aplicaciones| <ul><li>[Seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131) (uso de directiva de seguridad, en hello al mismo tiempo, restringir el acceso de nivel de fila basado en contexto de identidad, el rol o la ejecución de un usuario).</li><li>[Enmascaramiento de datos dinámicos](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dynamic-data-masking-get-started) (permiso de uso de & directiva, limita la exposición de información confidencial ocultándolos toonon privilegios a los usuarios)</li></ul>|
|**Supervisión proactiva**||  
| <br>Seguimiento y detección| <ul><li>[Auditoría](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing) realiza un seguimiento de eventos de base de datos y los escribe tooan registro de auditoría o en el registro de actividad su [cuenta de almacenamiento de Azure](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account).</li><li>Seguimiento del estado de Azure Database mediante [registros de actividad de Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</li><li>[Detección de amenazas](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-threat-detection) detecta actividades anómalas de la base de datos que indica la base de datos toohello amenazas de seguridad potenciales. </li></ul> |
|<br>Azure Security Center| <ul><li>[Supervisión de datos](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-auditing-on-sql-databases) Use Azure Security Center como solución de supervisión de seguridad centralizada para SQL y otros servicios de Azure.</li></ul>|     

## <a name="conclusion"></a>Conclusión
Azure Database es una sólida plataforma de base de datos, con una amplia gama de características de seguridad que satisfacen muchos de los requisitos de cumplimiento tanto normativos como organizativos. Puede proteger fácilmente los datos por controlar datos de tooyour de acceso físico de Hola y con una variedad de opciones de seguridad de los datos en el archivo - Hola, columna o nivel de fila con el cifrado de datos transparente, cifrado de nivel de celda o seguridad de nivel de fila. Siempre Encrypted también permite las operaciones en los datos cifrados, simplificando el proceso de Hola de actualizaciones de la aplicación. A su vez, acceso tooauditing registros de actividad de la base de datos SQL proporciona información de Hola que necesita, lo que le tooknow cómo y cuándo se tiene acceso a datos.

## <a name="next-steps"></a>Pasos siguientes
Puede mejorar la protección de hello de la base de datos frente a accesos no autorizados con unos pocos pasos sencillos o usuarios malintencionados. En este tutorial, aprenderá a:

- Configurar [reglas de firewall](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) para un servidor o una base de datos.
- Proteger los datos con [cifrado](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption).
- Habilitar la [auditoría de SQL Database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing).

