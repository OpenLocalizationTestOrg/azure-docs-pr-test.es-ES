---
title: aaaCreate y administrar la base de datos PostgreSQL las reglas de firewall mediante Hola portal de Azure | Documentos de Microsoft
description: Crear y administrar la base de datos PostgreSQL las reglas de firewall mediante Hola portal de Azure
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a>Crear y administrar la base de datos PostgreSQL las reglas de firewall mediante Hola portal de Azure
Las reglas de firewall de nivel de servidor habilitar administradores tooaccess una base de datos de Azure para PostgreSQL Server desde una dirección IP o intervalo de direcciones IP. 

## <a name="prerequisites"></a>Requisitos previos
toostep a través de este tooguide cómo, necesita:
- Un servidor [Creación de una instancia de Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Crear una regla de firewall de nivel de servidor en hello portal de Azure
1. En hoja de servidor PostgreSQL hello, en configuración del encabezado, haga clic en **seguridad de conexión** tooopen hoja de seguridad de conexión de Hola para hello base de datos de Azure para PostgreSQL.

  ![Azure Portal: haga clic en Seguridad de conexión](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Haga clic en **Agregar mis IP** en la barra de herramientas de Hola. Esto creará una regla automáticamente con la dirección IP de hello del equipo, como percibido por hello sistema Azure.

  ![Azure Portal: haga clic en Agregar mi dirección IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Comprobar la dirección IP antes de guardar la configuración de Hola. En algunas situaciones, dirección IP de hello observada mediante el portal de Azure difiere de dirección IP de hello utilizada cuando obtiene acceso a Hola internet y servidores de Azure. Por lo tanto, puede que tenga toochange Hola IP inicial y final IP toomake Hola regla funcione según lo esperado.
Utilice un motor de búsqueda y otra toocheck herramienta en línea su propia dirección IP (por ejemplo, la búsqueda de Bing "¿Cuál es mi IP").

  ![Búsqueda en Bing "cuál es mi ip"](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Agregue intervalos de direcciones adicionales. En reglas de Hola para hello base de datos de Azure para PostgreSQL firewall, puede especificar una única dirección IP o un intervalo de direcciones. Si desea que toolimit Hola regla tooone dirección IP única, Hola tipo misma dirección en el campo de Hola para IP inicial y final IP. Abrir firewall de Hola permite a los administradores y usuarios toologin tooany base de datos Hola PostgreSQL server toowhich tienen credenciales válidas.

  ![Azure Portal: reglas de firewall ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. Haga clic en **guardar** en Hola toosave de barra de herramientas, esta regla de firewall de nivel de servidor. Espere la confirmación de Hola que Hola reglas de firewall de actualización toohello fue correcta.

  ![Azure Portal: haga clic en Guardar](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Administrar reglas de firewall de nivel de servidor existente a través de hello portal de Azure
Repita las reglas de firewall de hello pasos toomanage Hola.
* equipo de tooadd Hola actual, haga clic en el botón de hello demasiado + **Agregar mis IP**. Haga clic en **guardar** cambios de hello toosave.
* las direcciones IP adicionales tooadd, escriba Hola nombre de la regla, la dirección IP inicial y la dirección IP final. Haga clic en **guardar** cambios de hello toosave.
* toomodify una regla existente, haga clic en cualquiera de los campos de Hola de regla de Hola y modificar. Haga clic en **guardar** cambios de hello toosave.
* toodelete una regla existente, haga clic en los puntos suspensivos de hello […] y haga clic en eliminar quitar regla de Hola. Haga clic en **guardar** cambios de hello toosave.

## <a name="next-steps"></a>Pasos siguientes
- De forma similar, puede crear scripts demasiado[crear y administrar la base de datos PostgreSQL las reglas de firewall mediante la CLI de Azure](howto-manage-firewall-using-cli.md)
- Para obtener ayuda sobre conexión tooan base de datos de Azure para PostgreSQL server, vea [bibliotecas de conexiones de base de datos de PostgreSQL](concepts-connection-libraries.md)
