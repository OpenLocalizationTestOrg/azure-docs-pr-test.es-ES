---
title: conceptos de aaaServer en la base de datos de Azure para MySQL | Documentos de Microsoft
description: En este tema se incluyen consideraciones e instrucciones para trabajar con servidores de Azure Database for MySQL.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a>Conceptos sobre servidores de Azure Database for MySQL
En este tema se incluyen consideraciones e instrucciones para trabajar con servidores de Azure Database for MySQL.

## <a name="what-is-an-azure-database-for-mysql-server"></a>¿Qué es un servidor de Azure Database for MySQL?

Un servidor de Azure Database for MySQL es un punto central de administración de varias bases de datos. Es Hola misma construcción de servidor de MySQL que esté familiarizado con de Hola a todos en local. En concreto, hello base de datos de Azure para el servicio MySQL se administra, proporciona rendimiento garantizado, expone el acceso y las características en el nivel de servidor.

Un servidor de Azure Database for MySQL:

- Se crea dentro de una suscripción de Azure.
- Es el recurso primario de Hola para bases de datos.
- Proporciona un espacio de nombres para las bases de datos.
- Es un contenedor con semántica de duración seguro - elimina un servidor y elimina las bases de datos de contenidos de Hola.
- Coloca recursos en una región.
- Proporciona un punto de conexión para el acceso a la base de datos y al servidor.
- Proporciona el ámbito de Hola para las directivas de administración que se aplican a las bases de datos de tooits: inicio de sesión, firewall, los usuarios, roles, configuraciones, etcetera.
- Está disponible en varias versiones. Para más información, vea [Supported Azure Database for MySQL database versions](./concepts-supported-versions.md) (Versiones de base de datos admitidas de Azure Database for MySQL).

En un servidor de Azure Database for MySQL, puede crear una o varias bases de datos. Puede participar una base de datos por servidor tooutilize toocreate todos los recursos de Hola o crear tooshare de bases de datos de varios recursos de Hola. Hola precios están estructurados por servidor, en función de la configuración de Hola de nivel de precios, unidades de almacenamiento (GB) de proceso. Para más información, consulte [Planes de tarifa](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a>¿Cómo conectarse y autenticarse tooan base de datos de MySQL server?

Hello siguientes elementos ayudan a asegurarse de la base de datos de access segura tooyour.

|||
| :-- | :-- |
| **Autenticación y autorización** | El servidor de Azure Database for MySQL admite la autenticación nativa de MySQL. Puede conectarse y autenticarse tooserver con inicio de sesión de administrador del servidor de Hola. |
| **Protocolo** | servicio de Hello es compatible con un protocolo basado en mensajes utilizado MySQL. |
| **TCP/IP** | se admite el protocolo de Hello sobre TCP/IP y a través de sockets de dominio de Unix. |
| **Firewall** | toohelp proteger los datos, una regla de firewall impide que todos los servidores de base de datos de access tooyour o bases de datos de tooits, hasta que especifique qué equipos tienen permiso. Vea [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md) (Reglas de firewall del servidor de Azure Database for MySQL). |
| **SSL** | servicio de Hello es compatible con la implantación conexiones SSL entre las aplicaciones y el servidor de base de datos.  Vea [tooAzure base de datos de conexión de conectividad de configurar SSL en su aplicación toosecurely para MySQL](./howto-configure-ssl.md). |
|||

## <a name="how-do-i-manage-a-server"></a>¿Cómo se administra un servidor?
Puede administrar la base de datos de Azure para los servidores de MySQL mediante Hola portal de Azure u Hola CLI de Azure.

## <a name="next-steps"></a>Pasos siguientes
- Para obtener información general del servicio de hello, consulte [base de datos de Azure para información general de MySQL](./overview.md)
- Para obtener información sobre las cuotas y limitaciones aplicables a recursos específicos en función de su **nivel de servicio**, consulte [Niveles de servicio](./concepts-service-tiers.md).
- Para obtener información acerca de la conexión de toohello de servicio, consulte [bibliotecas de conexiones de base de datos de Azure para MySQL](./concepts-connection-libraries.md).
