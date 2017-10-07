---
title: tooAzure de servicio de aplicaciones de Azure existente aaaConnect base de datos de MySQL | Documentos de Microsoft
description: "Instrucciones de cómo tooproperly conectarse un tooAzure de servicio de aplicaciones de Azure existente base de datos de MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a>Conectar un tooAzure de servicio de aplicaciones de Azure base de datos existente de MySQL server
Este documento se explica cómo tooconnect un tooyour de servicio de aplicaciones de Azure existente Azure la base de datos de MySQL server.

## <a name="before-you-begin"></a>Antes de empezar
Inicie sesión en toohello [portal de Azure](https://portal.azure.com). Cree de un servidor de Azure Database for MySQL. Para obtener más información, consulte demasiado[cómo toocreate Azure la base de datos de MySQL server del Portal de](quickstart-create-mysql-server-database-using-azure-portal.md) o [cómo toocreate Azure la base de datos para el servidor de MySQL usando CLI](quickstart-create-mysql-server-database-using-azure-cli.md).

Actualmente hay dos soluciones tooenable acceso una base de datos de servicio de aplicaciones de Azure tooan de MySQL. En ambas soluciones hay que configurar las reglas de firewall de nivel de servidor.

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a>Solución 1: crear un tooallow de regla de firewall todas las direcciones IP
Base de datos de Azure para MySQL proporciona seguridad de acceso mediante un firewall tooprotect los datos. Cuando se conecta desde un servicio de aplicaciones de Azure de tooAzure base de datos de MySQL server, tenga en cuenta que Hola saliente direcciones IP de servicio de aplicaciones son de naturaleza dinámica. 

disponibilidad de hello tooensure de su servicio de aplicación de Azure, se recomienda usar este tooallow solución todas las direcciones IP.

> [!NOTE]
> Microsoft está trabajando para una tooavoid solución a largo plazo que permite que todas las direcciones IP para los servicios de Azure tooconnect tooAzure base de datos MySQL.

1. En la hoja de servidor MySQL hello, bajo Configuración de encabezado, haga clic en **seguridad de conexión** tooopen hoja de seguridad de conexión de hello para la base de datos de Azure para MySQL Hola.

   ![Azure Portal: haga clic en Seguridad de conexión](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Escriba **NOMBRE DE LA REGLA**, **IP INICIAL** e **IP FINAL**. A continuación, haga clic en **Guardar**.
   - Nombre de la regla: Permitir-Todas-IP
   - IP inicial: 0.0.0.0
   - IP final: 255.255.255.255

   ![Azure Portal: agregar todas las IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a>Solución 2: crear un firewall tooexplicitly de regla permitir saliente direcciones IP
Puede agregar explícitamente que todos Hola saliente direcciones IP de su servicio de aplicaciones de Azure.

1. En la hoja de propiedades del servicio de aplicación Hola, ver su **dirección IP saliente**.

   ![Azure Portal: ver direcciones IP de salida](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. En el módulo de seguridad de conexión de MySQL de hello, agregue direcciones IP saliente uno por uno.

   ![Azure Portal: agregar direcciones IP explícitas](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. Recuerde demasiado**guardar** las reglas del firewall.

Aunque Hola servicio de aplicaciones de Azure intenta tookeep IP direcciones constante con el tiempo, hay casos donde pueden cambiar las direcciones IP de Hola. Por ejemplo, cuando Hola reciclajes de aplicación o se produce una operación de escala, o cuando se agregan nuevas máquinas en Azure datos regionales centros de capacidad de hello tooincrease. Cuando cambian de direcciones IP de hello, aplicación hello podría experimentar un tiempo de inactividad en caso de hello ya no puede conectarse toohello MySQL server. Tenga en cuenta esta posibilidad al elegir uno de hello anterior soluciones.

## <a name="ssl-configuration"></a>Configuración de SSL
Azure Database for MySQL tiene SSL habilitado de forma predeterminada. Si la aplicación no usa SSL tooconnect toohello database, necesita toodisable SSL en el servidor de MySQL. Para obtener más información acerca de cómo tooconfigure SSL, vea [uso de SSL con la base de datos de Azure para MySQL](howto-configure-ssl.md).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de las cadenas de conexión, consulte demasiado[las cadenas de conexión](howto-connection-string.md).
