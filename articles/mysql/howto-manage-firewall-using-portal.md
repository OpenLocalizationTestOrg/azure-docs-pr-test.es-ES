---
title: "Creación y administración de reglas de firewall de Azure Database for MySQL mediante Azure Portal | Microsoft Docs"
description: "Creación y administración de reglas de firewall de Azure Database for MySQL mediante Azure Portal"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a>Creación y administración de reglas de firewall de Azure Database for MySQL mediante Azure Portal
Las reglas de firewall de nivel de servidor permiten a los administradores tener acceso a un servidor de Azure Database for MySQL desde una dirección IP o desde un intervalo de direcciones IP especificado. 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a>Creación de una regla de firewall de nivel a servidor en Azure Portal

1. En la hoja del servidor de MySQL, en el encabezado Configuración, haga clic en **Seguridad de conexión** para abrir la hoja de seguridad de conexión para Azure Database for MySQL.

   ![Azure Portal: haga clic en Seguridad de conexión](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Haga clic en **Agregar mi dirección IP** en la barra de herramientas para crear una regla con la dirección IP del equipo, según lo percibido por el sistema de Azure.

   ![Azure Portal: haga clic en Agregar mi dirección IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Compruebe la dirección IP antes de guardar la configuración. En algunos casos, la dirección IP observada por Azure Portal difiere de la dirección IP utilizada para acceder a Internet y a los servidores de Azure. Por tanto, puede necesitar cambiar las direcciones IP inicial y final para que la regla funcione según lo previsto.

   Utilice un motor de búsqueda y otra herramienta en línea para comprobar su propia dirección IP (por ejemplo, busque "cuál es mi dirección ip").

   ![Resultados en Bing para "cuál es mi ip"](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Agregue intervalos de direcciones adicionales. En las reglas de firewall de Azure Database for MySQL, puede especificar una dirección IP o un intervalo de direcciones. Si desea limitar la regla a una única dirección IP, escriba la misma dirección en los campos de dirección IP inicial y dirección IP final. Abrir el firewall permite a los administradores y usuarios tener acceso a cualquier base de datos del servidor de MySQL para el que tengan unas credenciales válidas.

   ![Azure Portal: reglas de firewall ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Haga clic en **Guardar**, en la barra de herramientas, para guardar esta regla de firewall de nivel de servidor. Espere la confirmación de que la actualización de las reglas de firewall se realizó correctamente.

   ![Azure Portal: haga clic en Guardar](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a>Administración de reglas de firewall de nivel de servidor existentes a través del Portal de Azure
Repita los pasos para administrar las reglas de firewall.
* Para agregar el equipo actual, haga clic en **+ Agregar mi dirección IP**.
* Para agregar direcciones IP adicionales, escriba el **nombre de la regla**, la **dirección IP inicial** y la **dirección IP final**.
* Para modificar una regla existente, haga clic en cualquiera de los campos de la regla y realice la modificación.
* Para eliminar una regla existente, haga clic en los puntos suspensivos […] y haga clic en **Eliminar**.
* Haga clic en **Guardar** para guardar los cambios.

## <a name="next-steps"></a>Pasos siguientes
- Para obtener ayuda para la conexión a un servidor de Azure Database for MySQL, consulte [Bibliotecas de conexiones para Azure Database for MySQL](./concepts-connection-libraries.md).
