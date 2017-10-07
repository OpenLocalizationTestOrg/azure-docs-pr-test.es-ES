---
title: conceptos de aaaServer en la base de datos de Azure para PostgreSQL | Documentos de Microsoft
description: En este tema se incluyen consideraciones e instrucciones para trabajar con servidores de Azure Database for PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 9cc7816992f2ddedd76fdf906075a723b97720a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-servers"></a>Servidores de Azure Database for PostgreSQL
En este tema se incluyen consideraciones e instrucciones para trabajar con servidores de Azure Database for PostgreSQL.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>¿Qué es un servidor de Azure Database for PostgreSQL?
Un servidor de Azure Database for PostgreSQL es un punto central de administración de varias bases de datos. Es Hola misma construcción de servidor PostgreSQL que esté familiarizado con de Hola a todos en local. En concreto, Hola servicio PostgreSQL se administra, proporciona rendimiento garantizado, expone el acceso y las características en el nivel de servidor.

Un servidor de Azure Database for PostgreSQL:

- Se crea dentro de una suscripción de Azure.
- Es el recurso primario de Hola para bases de datos.
- Proporciona un espacio de nombres para las bases de datos.
- Es un contenedor con semántica de duración seguro - elimina un servidor y elimina las bases de datos de contenidos de Hola.
- Coloca recursos en una región.
- Proporciona un punto de conexión para el acceso a la base de datos y al servidor (.postgresql.database.azure.com).
- Proporciona el ámbito de Hola para las directivas de administración que se aplican a las bases de datos de tooits: inicio de sesión, firewall, los usuarios, roles, configuraciones, etcetera.
- Está disponible en varias versiones. Para más información, vea la información sobre [versiones de base de datos admitidas de PostgreSQL](concepts-supported-versions.md).
- Es ampliable por los usuarios. Para más información, consulte la información sobre [extensiones de PostgreSQL](concepts-extensions.md).

Dentro del servidor de Azure Database for PostgreSQL, puede crear una o varias bases de datos. Puede participar una base de datos por servidor tooutilize toocreate todos los recursos de Hola o crear tooshare de bases de datos de varios recursos de Hola. Hola precios están estructurados por servidor, en función de la configuración de Hola de nivel de precios, unidades de almacenamiento (GB) de proceso. Para más información, consulte [Planes de tarifa](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-postgresql-server"></a>¿Cómo conectarse y autenticarse tooan base de datos de Azure para PostgreSQL servidor?
Hello siguientes elementos ayudan a asegurarse de la base de datos de access segura tooyour.

|||
| :-- | :-- |
| **Autenticación y autorización** | El servidor de Azure Database for PostgreSQL admite la autenticación nativa de PostgreSQL. Puede conectarse y autenticarse tooserver con inicio de sesión de administrador del servidor de Hola. |
| **Protocolo** | servicio de Hello es compatible con un protocolo basado en mensajes utilizado PostgreSQL. |
| **TCP/IP** | se admite el protocolo de Hello sobre TCP/IP y a través de sockets de dominio de Unix. |
| **Firewall** | toohelp proteger los datos, una regla de firewall impide que todos los servidores de base de datos de access tooyour o bases de datos de tooits, hasta que especifique qué equipos tienen permiso. Vea la información sobre las [reglas de firewall del servidor de Azure Database for PostgreSQL](concepts-firewall-rules.md). |
|||

## <a name="how-do-i-manage-a-server"></a>¿Cómo se administra un servidor?
Puede administrar la base de datos de Azure para Hola de PostgreSQL servidores mediante el portal de Azure o hello [CLI de Azure](/cli/azure/postgres).

## <a name="next-steps"></a>Pasos siguientes
- Para obtener información general del servicio de hello, consulte [base de datos de Azure para información general de PostgreSQL](overview.md)
- Para obtener información sobre las cuotas y limitaciones aplicables a recursos específicos en función de su **nivel de servicio**, consulte [Niveles de servicio](concepts-service-tiers.md).
- Para obtener información sobre la conexión de toohello de servicio, consulte [bibliotecas de conexiones de base de datos de Azure para PostgreSQL](concepts-connection-libraries.md).
