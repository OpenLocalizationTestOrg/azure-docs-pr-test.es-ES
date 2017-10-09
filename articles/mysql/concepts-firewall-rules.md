---
title: aaaAzure base de datos de reglas de firewall del servidor MySQL | Documentos de Microsoft
description: Describe las reglas de firewall para el servidor de Azure Database for MySQL.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1f85310385da947b6c492aa6aa21c1b885c2a97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-server-firewall-rules"></a>Reglas de firewall del servidor de Azure Database para MySQL
Firewalls impedir que todos los servidores de base de datos de access tooyour hasta que especifique qué equipos tienen permiso. firewall de Hello otorga servidor de toohello de acceso basado en hello procedentes de la dirección IP de cada solicitud.

tooconfigure del firewall, crear reglas de firewall que especifican los intervalos de direcciones IP aceptables. Puede crear reglas de firewall en el nivel de servidor de Hola.

**Las reglas de Firewall:** estas reglas permiten a los clientes tooaccess la base de datos de Azure completo de MySQL server, es decir, todas las bases de datos de Hola de Hola mismo servidor lógico. Las reglas de firewall de nivel de servidor pueden configurarse mediante Hola portal de Azure o mediante comandos de CLI de Azure. reglas de firewall de nivel de servidor de toocreate, debe ser propietario de la suscripción de Hola o un colaborador de suscripción.

## <a name="firewall-overview"></a>Información general de firewalls
Todos los tooyour de acceso de base de datos base de datos de MySQL server está bloqueado por firewall de Hola de forma predeterminada. toobegin con el servidor desde otro equipo, deberá toospecify uno o servidor de nivel de servidor más firewall reglas tooenable acceso tooyour. Utilice toospecify de reglas de firewall de hello dirección IP que va de hello tooallow de Internet. Acceso toohello sitio Web del portal Azure sí no se ve afectado por las reglas de firewall de Hola.

Hola de intentos de conexión desde Internet y Azure debe atravesar primero firewall Hola antes de poder alcanzar la base de datos de Azure para la base de datos MySQL, como se muestra en hello siguiente diagrama:

![Ejemplo de flujo de cómo funciona firewall Hola](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>La conexión desde Internet Hola
Las reglas de firewall de nivel de servidor aplican las bases de datos de tooall en hello base de datos de MySQL server.

Si dirección IP de saludo de solicitud de hello es dentro de uno de los intervalos de hello especificados en las reglas de firewall de nivel de servidor de hello, se concede la conexión Hola.

Si dirección IP de saludo de solicitud de hello no está dentro de intervalos de hello especifican en cualquiera de hello nivel de base de datos o reglas de firewall de nivel de servidor, se produce un error en la solicitud de conexión de Hola.

## <a name="programmatically-managing-firewall-rules"></a>Administración mediante programación de reglas de firewall
Además toohello portal de Azure, firewall de reglas se pueden administra mediante programación usando CLI de Azure. Consulte también la información sobre la [creación y administración de reglas de firewall de Azure Database for MySQL mediante la CLI de Azure](./howto-manage-firewall-using-cli.md).

## <a name="troubleshooting-hello-database-firewall"></a>Solucionar problemas de firewall de base de datos de Hola
Considere la posibilidad de hello siguientes puntos cuando toohello de acceso base de datos de Microsoft Azure para el servicio del servidor de MySQL no se comporta tal y como esperaba:

* **Lista de admisión de toohello de cambios no han surtido efecto todavía:** puede haber tanto como un retraso de cinco minutos para cambia toohello base de datos de Azure para el efecto de tootake de configuración de firewall de servidor MySQL.

* **inicio de sesión de Hello no está autorizado o se usó una contraseña incorrecta:** si un inicio de sesión no tiene permisos en hello base de datos de Azure para contraseña de servidor o hello MySQL utilizada es incorrecta, Hola toohello base de datos de conexión para el servidor MySQL se deniega. Crear una configuración de firewall sólo proporciona a los clientes un tooattempt oportunidad conectar el servidor de tooyour; cada cliente debe proporcionar credenciales de seguridad necesarias Hola.

* **Dirección IP dinámica:** si tiene una conexión a Internet con una dirección IP dinámica y tiene problemas para superar el firewall de hello, intente una de hello siguientes soluciones:

* Pregunte a su proveedor de servicios de Internet (ISP) para el intervalo de direcciones IP de hello asignado tooyour los equipos cliente que Hola de acceso base de datos de MySQL server y, a continuación, agregue el intervalo de direcciones IP de hello como una regla de firewall.

* Obtener una dirección IP estática en su lugar para los equipos cliente y, a continuación, agregue las direcciones IP hello como reglas de firewall.

## <a name="next-steps"></a>Pasos siguientes

[Crear y administrar la base de datos MySQL las reglas de firewall mediante el portal de Azure de hello](./howto-manage-firewall-using-portal.md)
[crear y administrar la base de datos de Azure con las reglas de firewall de MySQL con CLI de Azure](./howto-manage-firewall-using-cli.md)
