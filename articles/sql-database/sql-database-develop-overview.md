---
title: "información general sobre el desarrollo de aplicaciones de base de datos aaaSQL | Documentos de Microsoft"
description: "Obtenga información acerca de las bibliotecas de conectividad disponible y procedimientos recomendados para las aplicaciones se conectan tooSQL base de datos."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a>Introducción al desarrollo de aplicaciones en SQL Database
Este artículo le guía a través de consideraciones básicas de Hola que un desarrollador debe tener en cuenta al escribir código tooconnect tooAzure base de datos SQL.

> [!TIP]
> Para un tutorial que se muestra cómo toocreate un servidor, se crea un firewall basado en servidor, ver propiedades del servidor, conectar con SQL Server Management Studio, base de datos maestra Hola de consulta, cree una base de datos de ejemplo y una base de datos en blanco, consultar propiedades de base de datos, conectarse uso de SQL Server Management Studio y la base de datos de ejemplo de Hola de consulta, vea [Tutorial de obtener](sql-database-get-started-portal.md).
>

## <a name="language-and-platform"></a>Plataforma y lenguaje
Existen ejemplos de código para diferentes lenguajes de programación y plataformas. Puede encontrar ejemplos de código de toohello vínculos desde: 

* Más información: [Bibliotecas de conexiones para Base de datos SQL y SQL Server](sql-database-libraries.md)

## <a name="tools"></a>Herramientas 
Puede aprovechar herramientas de código abierto como [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli) o [VS Code](https://code.visualstudio.com/). Además, Azure SQL Database funciona con herramientas de Microsoft como [Visual Studio](https://www.visualstudio.com/downloads/) y [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).  También puede usar Hola Portal de administración de Azure, PowerShell, y las API de REST le ayudarán a obtener productividad adicional.

## <a name="resource-limitations"></a>Limitaciones de recursos
La base de datos de SQL Azure administra Hola recursos disponibles tooa base de datos mediante dos mecanismos diferentes: regulación de recursos y el cumplimiento de límites.

* Más información: [Límites de recursos de Base de datos SQL](sql-database-resource-limits.md)

## <a name="security"></a>Seguridad
Base de datos SQL de Azure proporciona recursos para limitar el acceso, proteger los datos y supervisar las actividades en una base de datos SQL.

* Más información: [Protección de bases de datos SQL](sql-database-security-overview.md)

## <a name="authentication"></a>Autenticación
* Base de datos SQL de Azure admite inicios de sesión y usuarios de autenticación de SQL Server, así como de [autenticación de Azure Active Directory](sql-database-aad-authentication.md) .
* Necesita una base de datos determinado, en lugar de la aplicación de valores predeterminado toohello toospecify *maestro* base de datos.
* No se puede utilizar Transact-SQL hello **uso NombreBaseDatos;** ejecutada en la base de datos de base de datos SQL tooswitch tooanother.
* Más información: [Seguridad de la Base de datos SQL: administrar la seguridad del inicio de sesión y el acceso a la base de datos](sql-database-manage-logins.md)

## <a name="resiliency"></a>Resistencia
Cuando se produce un error transitorio al conectar tooSQL base de datos, el código debe reintentar la llamada de Hola.  Se recomienda que lógica de reintento utilizar lógica de retroceso, por lo que no sobrecargar Hola base de datos de SQL con varios clientes reintentando simultáneamente.

* Ejemplos de código: para los ejemplos de código que muestran la lógica de reintento, vea los ejemplos para el idioma de Hola de su elección en: [bibliotecas de conexiones de base de datos SQL y SQL Server](sql-database-libraries.md)
* Más información: [Códigos de error para las aplicaciones cliente de la Base de datos SQL: error de conexión de base de datos y otros problemas](sql-database-develop-error-messages.md)

## <a name="managing-connections"></a>Administración de conexiones
* En la lógica de conexión de cliente, invalide toobe de tiempo de espera predeterminado de hello 30 segundos.  valor predeterminado de Hola de 15 segundos es demasiado corto para las conexiones que dependen de Hola a internet.
* Si usas un [agrupación de conexiones](http://msdn.microsoft.com/library/8xx3tyca.aspx), ser seguro tooclose Hola Hola de conexión instantánea el programa no esté usando activamente y no está preparando tooreuse lo.

## <a name="network-considerations"></a>Consideraciones sobre la red
* En equipo de Hola que hospeda el programa cliente, asegúrese de que firewall de hello permite la comunicación de TCP de salida en el puerto 1433.  Más información: [Configuración del firewall en la Base de datos SQL de Azure mediante el Portal de Azure](sql-database-configure-firewall-settings.md)
* Si su programa cliente conecta tooSQL base de datos mientras el cliente se ejecuta en una máquina virtual (VM) de Azure, debe abrir determinados intervalos de puertos en hello máquina virtual. Más información: [Puertos más allá de 1433 para ADO.NET 4.5 y SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)
* Las conexiones de cliente tooAzure base de datos SQL a veces omitir el proxy de Hola e interactuar directamente con la base de datos de Hola. Los puertos que no sean 1433 se convierten en puertos importantes. Para más información, consulte [Arquitectura de conectividad de Azure SQL Database](sql-database-connectivity-architecture.md) y [Puertos más allá de 1433 para ADO.NET 4.5 y SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="data-sharding-with-elastic-scale"></a>Particionamiento de datos con la escala elástica
Escala elástica simplifica el proceso de Hola de escalado (y). 

* [Modelos de diseño para las aplicaciones SaaS multiinquilino con base de datos SQL de Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md)
* [Introducción a la vista previa de Escalado elástico de Base de datos SQL de Azure](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a>Pasos siguientes
Explorar todas las hello [funciones de base de datos SQL](sql-database-technical-overview.md)
