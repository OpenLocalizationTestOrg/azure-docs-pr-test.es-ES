---
title: 'aaa "CLI de Azure Script: crear una base de datos de Azure para MySQL | Documentos de Microsoft"'
description: Este script de la CLI de ejemplo crea un servidor de Azure Database for MySQL (Base de datos de Azure para MySQL) y configura una regla de firewall de nivel de servidor.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="29f8b-103">Crear un servidor MySQL y configurar una regla de firewall mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="29f8b-103">Create a MySQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="29f8b-104">Este script de la CLI de ejemplo crea un servidor de Azure Database for MySQL (Base de datos de Azure para MySQL) y configura una regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="29f8b-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="29f8b-105">Una vez que el script de Hola se ejecuta correctamente, Hola MySQL es accesible por todos los servicios de Azure y Hola configurado direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="29f8b-105">Once hello script runs successfully, hello MySQL server is accessible by all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="29f8b-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="29f8b-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="29f8b-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="29f8b-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="29f8b-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="29f8b-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="29f8b-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="29f8b-109">Sample script</span></span>
<span data-ttu-id="29f8b-110">En este script de ejemplo, editar Hola resaltada las líneas toocustomize Hola administrador username y password.</span><span class="sxs-lookup"><span data-stu-id="29f8b-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="29f8b-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="29f8b-111">Clean up deployment</span></span>
<span data-ttu-id="29f8b-112">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="29f8b-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="29f8b-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="29f8b-113">Script explanation</span></span>
<span data-ttu-id="29f8b-114">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="29f8b-114">This script uses hello following commands.</span></span> <span data-ttu-id="29f8b-115">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="29f8b-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="29f8b-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="29f8b-116">**Command**</span></span> | <span data-ttu-id="29f8b-117">**Notas**</span><span class="sxs-lookup"><span data-stu-id="29f8b-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="29f8b-118">az group create</span><span class="sxs-lookup"><span data-stu-id="29f8b-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="29f8b-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="29f8b-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="29f8b-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="29f8b-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="29f8b-121">Crea un servidor de MySQL que hospeda las bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="29f8b-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="29f8b-122">az mysql server firewall create</span><span class="sxs-lookup"><span data-stu-id="29f8b-122">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="29f8b-123">Crea un servidor de toohello de acceso de firewall regla tooallow y bases de datos en él desde el intervalo de direcciones IP de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="29f8b-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="29f8b-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="29f8b-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="29f8b-125">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="29f8b-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="29f8b-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29f8b-126">Next steps</span></span>
- <span data-ttu-id="29f8b-127">Obtener información detallada sobre Hola CLI de Azure: [documentación de Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="29f8b-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="29f8b-128">Pruebe scripts adicionales en: [Ejemplos de la CLI de Azure para Azure Database for MySQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="29f8b-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
