---
title: Reglas de firewall del servidor de Azure Database for PostgreSQL | Microsoft Docs
description: Describe las reglas de firewall para el servidor de Azure Database for PostgreSQL.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1d46a4434c483c3612a9a7b4cdef718d6dc3e765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Reglas de firewall del servidor de Azure Database for PostgreSQL
Firewalls impedir que todos los servidores de base de datos de access tooyour hasta que especifique qué equipos tienen permiso. firewall de Hello otorga servidor de toohello de acceso basado en hello procedentes de la dirección IP de cada solicitud.
tooconfigure del firewall, crear reglas de firewall que especifican los intervalos de direcciones IP aceptables. Puede crear reglas de firewall en el nivel de servidor de Hola.

**Las reglas de Firewall:** estas reglas permiten a clientes tooaccess la base de datos de Azure completo para servidor de PostgreSQL, es decir, todas las bases de datos de Hola de Hola mismo servidor lógico. Las reglas de firewall de nivel de servidor pueden configurarse mediante Hola portal de Azure o mediante comandos de CLI de Azure. reglas de firewall de nivel de servidor de toocreate, debe ser propietario de la suscripción de Hola o un colaborador de suscripción.

## <a name="firewall-overview"></a>Información general de firewalls
Todos los tooyour de acceso de base de datos base de datos de Azure para PostgreSQL servidor está bloqueado por firewall de Hola de forma predeterminada. toobegin con el servidor desde otro equipo, deberá toospecify uno o servidor de nivel de servidor más firewall reglas tooenable acceso tooyour. Utilice toospecify de reglas de firewall de hello dirección IP que va de hello tooallow de Internet. Acceso toohello sitio Web del portal Azure sí no se ve afectado por las reglas de firewall de Hola.
Hola de intentos de conexión desde Internet y Azure debe atravesar primero firewall Hola antes de poder alcanzar la base de datos PostgreSQL, como se muestra en hello siguiente diagrama:

![Ejemplo de flujo de cómo funciona firewall Hola](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>La conexión desde Internet Hola
Las reglas de firewall de nivel de servidor aplican tooall bases de datos en hello base de datos de Azure para servidor de PostgreSQL. Si dirección IP de saludo de solicitud de hello es dentro de uno de los intervalos de hello especificados en las reglas de firewall de nivel de servidor de hello, se concede la conexión Hola.
Si dirección IP de saludo de solicitud de hello no está dentro de intervalos de hello especifican en cualquiera de hello nivel de base de datos o reglas de firewall de nivel de servidor, se produce un error en la solicitud de conexión de Hola.
Por ejemplo, si la aplicación se conecta con un controlador JDBC de PostgreSQL, puede encontrar este error intentando tooconnect cuando firewall de hello está bloqueando la conexión de Hola.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: no pg\_hba.conf entry for host "123.45.67.890", user "adminuser", database "postgresql", SSL

## <a name="programmatically-managing-firewall-rules"></a>Administración mediante programación de reglas de firewall
Además toohello portal de Azure, firewall de reglas se pueden administra mediante programación usando CLI de Azure.
Vea también la información sobre la [creación y la administración de reglas de firewall de Azure Database for PostgreSQL mediante la CLI de Azure](howto-manage-firewall-using-cli.md).

## <a name="troubleshooting-hello-database-firewall"></a>Solucionar problemas de firewall de base de datos de Hola
Considere la posibilidad de hello siguientes puntos cuando toohello de acceso base de datos de Microsoft Azure para el servicio del servidor de PostgreSQL no se comporta tal y como esperaba:

* **Lista de admisión de toohello de cambios no han surtido efecto todavía:** puede haber tanto como un retraso de cinco minutos para cambia toohello base de datos de Azure para el efecto de tootake de configuración de firewall de servidor de PostgreSQL.

* **inicio de sesión de Hello no está autorizado o se usó una contraseña incorrecta:** si un inicio de sesión no tiene permisos en hello base de datos de Azure para contraseña de servidor o hello PostgreSQL utilizada es incorrecta, Hola conexión toohello base de datos de Azure para servidor de PostgreSQL denegado. Crear una configuración de firewall sólo proporciona a los clientes un tooattempt oportunidad conectar el servidor de tooyour; cada cliente debe proporcionar credenciales de seguridad necesarias Hola.

Por ejemplo, mediante un cliente JDBC, puede aparecer Hola siguiente error.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: password authentication failed for user "yourusername"

* **Dirección IP dinámica:** si tiene una conexión a Internet con una dirección IP dinámica y tiene problemas para superar el firewall de hello, intente una de hello siguientes soluciones:

* Pregunte a su proveedor de servicios de Internet (ISP) para el intervalo de direcciones IP de hello asignado tooyour los equipos cliente que Hola de acceso base de datos de Azure para PostgreSQL servidor y, a continuación, agregar el intervalo de direcciones IP de hello como una regla de firewall.

* Obtener una dirección IP estática en su lugar para los equipos cliente y, a continuación, agregue las direcciones IP hello como reglas de firewall.

## <a name="next-steps"></a>Pasos siguientes
Para leer artículos sobre cómo crear reglas de firewall de nivel de servidor y de base de datos, consulte:
* [Crear y administrar la base de datos PostgreSQL las reglas de firewall mediante Hola portal de Azure](howto-manage-firewall-using-portal.md)
* [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md) (Creación y administración de reglas de firewall de Azure Database for PostgreSQL mediante la CLI de Azure)