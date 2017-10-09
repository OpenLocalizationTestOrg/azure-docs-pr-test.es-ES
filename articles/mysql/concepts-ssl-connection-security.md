---
title: aaaSSL conectividad de base de datos de Azure para MySQL | Documentos de Microsoft
description: "Información para configurar la base de datos MySQL y tooproperly de aplicaciones asociadas de usar conexiones SSL"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>Conectividad SSL de Azure Database for MySQL
Base de datos de Azure para MySQL permite conectar las aplicaciones de tooclient de servidor de base de datos mediante capa de Sockets seguros (SSL). Aplicar las conexiones SSL entre el servidor de base de datos y las aplicaciones cliente ayuda a protege contra los ataques de "tipo man in intermedio Hola" mediante el cifrado de flujo de datos de hello entre servidor hello y la aplicación.

## <a name="default-settings"></a>Configuración predeterminada
De forma predeterminada, servicio de base de datos de hello debe estar configurado toorequire SSL conexiones al conectar tooMySQL.  Se recomienda evitar la desactivación de la opción de SSL de hello siempre que sea posible. 

Al aprovisionar una nueva base de datos de Azure de MySQL server a través de hello portal de Azure y la CLI, el cumplimiento de las conexiones SSL está habilitado de forma predeterminada. 

Del mismo modo, las cadenas de conexión que están predefinidas en la configuración de "Cadenas de conexión" hello en el servidor en hello portal de Azure incluyen parámetros de hello necesario para idiomas tooconnect tooyour base de datos servidor común mediante SSL. Hello parámetro SSL varía en función de conector de hello, por ejemplo "ssl = true" o "sslmode = requieren" o "sslmode = necesaria" y otras variaciones.

toolearn cómo tooenable o deshabilitar conexión de SSL al desarrollar la aplicación, consulte demasiado[cómo tooconfigure SSL](howto-configure-ssl.md).

## <a name="next-steps"></a>Pasos siguientes
[Bibliotecas de conexiones de Azure Database for MySQL](concepts-connection-libraries.md)
