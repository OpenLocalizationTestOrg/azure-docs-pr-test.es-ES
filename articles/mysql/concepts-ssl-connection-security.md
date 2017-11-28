---
title: Conectividad SSL de Azure Database for MySQL | Microsoft Docs
description: "Información para configurar Azure Database for MySQL y las aplicaciones asociadas, a fin de usar correctamente las conexiones SSL"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b03b3a2dbfad92cc0cfa84777b38ddff90452cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="4cf0c-103">Conectividad SSL de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="4cf0c-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="4cf0c-104">Azure Database for MySQL permite conectar el servidor de bases de datos a las aplicaciones cliente con la Capa de sockets seguros (SSL).</span><span class="sxs-lookup"><span data-stu-id="4cf0c-104">Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="4cf0c-105">El establecimiento de conexiones SSL entre el servidor de bases de datos y las aplicaciones cliente ofrece protección frente a ataques de tipo "Man in the middle" mediante el cifrado del flujo de datos entre el servidor y la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4cf0c-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="4cf0c-106">Configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="4cf0c-106">Default settings</span></span>
<span data-ttu-id="4cf0c-107">De forma predeterminada, el servicio de base de datos debe configurarse para requerir conexiones SSL al conectar con MySQL.</span><span class="sxs-lookup"><span data-stu-id="4cf0c-107">By default, the database service should be configured to require SSL connections when connecting to MySQL.</span></span>  <span data-ttu-id="4cf0c-108">Se recomienda evitar que se deshabilite la opción SSL siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="4cf0c-108">It is recommended avoid disabling the SSL option whenever possible.</span></span> 

<span data-ttu-id="4cf0c-109">Al aprovisionar un nuevo servidor de Azure Database for MySQL en Azure Portal o con la CLI de Azure, el establecimiento de conexiones SSL está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4cf0c-109">When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="4cf0c-110">Del mismo modo, las cadenas de conexión que están predefinidas en la configuración de "Cadenas de conexión" del servidor en Azure Portal incluyen los parámetros necesarios para que los lenguajes comunes se conecten al servidor de base de datos mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="4cf0c-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="4cf0c-111">El parámetro SSL varía según el conector; por ejemplo "ssl=true", "sslmode=require", "sslmode=required" y otras variaciones.</span><span class="sxs-lookup"><span data-stu-id="4cf0c-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="4cf0c-112">Para obtener información sobre cómo habilitar o deshabilitar la conexión SSL al desarrollar la aplicación, vea [Configuración de SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="4cf0c-112">To learn how to enable or disable SSL connection when developing application, please refer to [How to configure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cf0c-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4cf0c-113">Next steps</span></span>
[<span data-ttu-id="4cf0c-114">Bibliotecas de conexiones de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="4cf0c-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
