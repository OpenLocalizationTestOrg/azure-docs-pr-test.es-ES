---
title: aaaCreate y administrar la base de datos de Azure con las reglas de firewall de MySQL con hello portal de Azure | Documentos de Microsoft
description: Crear y administrar la base de datos de Azure para las reglas de firewall de MySQL con hello portal de Azure
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>Crear y administrar la base de datos de Azure para las reglas de firewall de MySQL con hello portal de Azure
Las reglas de firewall de nivel de servidor habilitar administradores tooaccess una base de datos de Azure para MySQL Server desde una dirección IP o intervalo de direcciones IP. 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Crear una regla de firewall de nivel de servidor en hello portal de Azure

1. En la hoja de servidor MySQL hello, bajo Configuración de encabezado, haga clic en **seguridad de conexión** tooopen hoja de seguridad de conexión de hello para la base de datos de Azure para MySQL Hola.

   ![Azure Portal: haga clic en Seguridad de conexión](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Haga clic en **Agregar mis IP** en toocreate de barra de herramientas de hello una regla con la dirección IP de hello del equipo, según lo percibido por hello sistema Azure.

   ![Azure Portal: haga clic en Agregar mi dirección IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Comprobar la dirección IP antes de guardar la configuración de Hola. En algunas situaciones, dirección IP de hello observada mediante el portal de Azure difiere de dirección IP de hello utilizada cuando obtiene acceso a Hola internet y servidores de Azure. Por lo tanto, puede que tenga toochange Hola IP inicial y final IP toomake Hola regla funcione según lo esperado.

   Usar un motor de búsqueda y otra toocheck herramienta en línea su propia dirección IP (por ejemplo, buscar "¿Cuál es mi dirección IP").

   ![Resultados en Bing para "cuál es mi ip"](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Agregue intervalos de direcciones adicionales. En reglas de Hola para hello base de datos de Azure para firewall de MySQL, puede especificar una única dirección IP o un intervalo de direcciones. Si desea que toolimit Hola regla tooone dirección IP única, Hola tipo misma dirección en el campo de Hola para IP inicial y final IP. Abrir firewall de Hola permite tooaccess administradores y usuarios de cualquier base de datos MySQL server toowhich tienen credenciales válidas de Hola.

   ![Azure Portal: reglas de firewall ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Haga clic en **guardar** en Hola toosave de barra de herramientas, esta regla de firewall de nivel de servidor. Espere la confirmación de Hola que Hola reglas de firewall de actualización toohello fue correcta.

   ![Azure Portal: haga clic en Guardar](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Administrar reglas de firewall de nivel de servidor existente a través de hello portal de Azure
Repita las reglas de firewall de hello pasos toomanage Hola.
* equipo de tooadd Hola actual, haga clic en **+ Agregar mis IP**.
* Escriba las direcciones IP adicionales tooadd, Hola **nombre de la regla**, **IP inicial**, y **IP final**.
* toomodify una regla existente, haga clic en cualquiera de los campos de Hola de regla de Hola y modificar.
* regla de toodelete existente, haga clic en los puntos suspensivos de hello […] y haga clic en **eliminar**.
* Haga clic en **guardar** cambios de hello toosave.

## <a name="next-steps"></a>Pasos siguientes
- Para obtener ayuda en la conexión tooan base de datos de MySQL server, consulte [bibliotecas de conexiones de base de datos de Azure para MySQL](./concepts-connection-libraries.md)
