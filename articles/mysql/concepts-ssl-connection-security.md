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
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="9b846-103">Conectividad SSL de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="9b846-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="9b846-104">Base de datos de Azure para MySQL permite conectar las aplicaciones de tooclient de servidor de base de datos mediante capa de Sockets seguros (SSL).</span><span class="sxs-lookup"><span data-stu-id="9b846-104">Azure Database for MySQL supports connecting your database server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="9b846-105">Aplicar las conexiones SSL entre el servidor de base de datos y las aplicaciones cliente ayuda a protege contra los ataques de "tipo man in intermedio Hola" mediante el cifrado de flujo de datos de hello entre servidor hello y la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b846-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="9b846-106">Configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="9b846-106">Default settings</span></span>
<span data-ttu-id="9b846-107">De forma predeterminada, servicio de base de datos de hello debe estar configurado toorequire SSL conexiones al conectar tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="9b846-107">By default, hello database service should be configured toorequire SSL connections when connecting tooMySQL.</span></span>  <span data-ttu-id="9b846-108">Se recomienda evitar la desactivación de la opción de SSL de hello siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="9b846-108">It is recommended avoid disabling hello SSL option whenever possible.</span></span> 

<span data-ttu-id="9b846-109">Al aprovisionar una nueva base de datos de Azure de MySQL server a través de hello portal de Azure y la CLI, el cumplimiento de las conexiones SSL está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9b846-109">When provisioning a new Azure Database for MySQL server through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="9b846-110">Del mismo modo, las cadenas de conexión que están predefinidas en la configuración de "Cadenas de conexión" hello en el servidor en hello portal de Azure incluyen parámetros de hello necesario para idiomas tooconnect tooyour base de datos servidor común mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="9b846-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="9b846-111">Hello parámetro SSL varía en función de conector de hello, por ejemplo "ssl = true" o "sslmode = requieren" o "sslmode = necesaria" y otras variaciones.</span><span class="sxs-lookup"><span data-stu-id="9b846-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="9b846-112">toolearn cómo tooenable o deshabilitar conexión de SSL al desarrollar la aplicación, consulte demasiado[cómo tooconfigure SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="9b846-112">toolearn how tooenable or disable SSL connection when developing application, please refer too[How tooconfigure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b846-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b846-113">Next steps</span></span>
[<span data-ttu-id="9b846-114">Bibliotecas de conexiones de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="9b846-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
