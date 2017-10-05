---
title: 'Ejemplos de Azure PowerShell: App Service | Microsoft Docs'
description: 'Ejemplos de Azure PowerShell: App Service'
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 3254fdd57cfcd170f22374c1e3b058e6081d8e8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="4cd26-103">Ejemplos de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cd26-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="4cd26-104">En la tabla siguiente se incluyen vínculos a scripts de Bash creados con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4cd26-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="4cd26-105">**Creación de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="4cd26-105">**Create app**</span></span>||
| [<span data-ttu-id="4cd26-106">Creación de una aplicación web con implementación desde GitHub</span><span class="sxs-lookup"><span data-stu-id="4cd26-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="4cd26-107">Crea una aplicación web de Azure que extrae código de GitHub.</span><span class="sxs-lookup"><span data-stu-id="4cd26-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="4cd26-108">Creación de una aplicación web con implementación continua desde GitHub</span><span class="sxs-lookup"><span data-stu-id="4cd26-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="4cd26-109">Crea una aplicación web de Azure que implementa continuamente código desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="4cd26-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="4cd26-110">Creación de una aplicación web e implementación de código con FTP</span><span class="sxs-lookup"><span data-stu-id="4cd26-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="4cd26-111">Crea una aplicación web de Azure y cargue archivos de un directorio local con FTP.</span><span class="sxs-lookup"><span data-stu-id="4cd26-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="4cd26-112">Creación de una aplicación web e implementación de código desde un repositorio local de GitHub</span><span class="sxs-lookup"><span data-stu-id="4cd26-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="4cd26-113">Crea una aplicación web de Azure y configura la inserción de código desde un repositorio de Git local.</span><span class="sxs-lookup"><span data-stu-id="4cd26-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="4cd26-114">Creación de una aplicación web e implementación de código en un entorno de ensayo</span><span class="sxs-lookup"><span data-stu-id="4cd26-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="4cd26-115">Crea una aplicación web de Azure con una ranura de implementación para cambios en el código de ensayo.</span><span class="sxs-lookup"><span data-stu-id="4cd26-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="4cd26-116">**Configuración de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="4cd26-116">**Configure app**</span></span>||
| [<span data-ttu-id="4cd26-117">Asignación de un dominio personalizado a una aplicación web</span><span class="sxs-lookup"><span data-stu-id="4cd26-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="4cd26-118">Crea una aplicación web de Azure y le asigna un nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="4cd26-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="4cd26-119">Enlace de un certificado SSL personalizado a una aplicación web</span><span class="sxs-lookup"><span data-stu-id="4cd26-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="4cd26-120">Crea una aplicación web de Azure y enlaza a ella el certificado SSL de un nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="4cd26-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="4cd26-121">**Escalado de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="4cd26-121">**Scale app**</span></span>||
| [<span data-ttu-id="4cd26-122">Escalado manual de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="4cd26-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="4cd26-123">Crea una aplicación web de Azure y la escala a través de dos instancias.</span><span class="sxs-lookup"><span data-stu-id="4cd26-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="4cd26-124">Escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="4cd26-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="4cd26-125">Crea dos aplicaciones web de Azure en dos regiones geográficas diferentes y hace que estén disponibles a través de un punto de conexión único mediante Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="4cd26-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="4cd26-126">**Conexión de la aplicación a recursos**</span><span class="sxs-lookup"><span data-stu-id="4cd26-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="4cd26-127">Conexión de una aplicación web a una base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="4cd26-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="4cd26-128">Crea una aplicación web de Azure y una base de datos SQL y, a continuación, añade la cadena de conexión de base de datos a la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4cd26-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="4cd26-129">Conexión de una aplicación web a una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4cd26-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="4cd26-130">Crea una aplicación web de Azure y una cuenta de almacenamiento y, a continuación, añade la cadena de conexión de almacenamiento a la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4cd26-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="4cd26-131">**Supervisión de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="4cd26-131">**Monitor app**</span></span>||
| [<span data-ttu-id="4cd26-132">Supervisión de una aplicación web con registros de servidor web</span><span class="sxs-lookup"><span data-stu-id="4cd26-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="4cd26-133">Crea una aplicación web de Azure, habilita el registro para ella y descarga los registros en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="4cd26-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
