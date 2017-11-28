---
title: "Instalación de la CLI de DC/OS | Microsoft Docs"
description: Instale la CLI de DC/OS.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, microservicios, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: a8ea47f158c0d666340815d2e039995c7483257f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
> [!NOTE]
> <span data-ttu-id="48681-104">Este procedimiento se usa para trabajar con clústeres ACS basados en DC/OS.</span><span class="sxs-lookup"><span data-stu-id="48681-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="48681-105">No es necesario realizarlo en clústeres ACS basados en Swarm.</span><span class="sxs-lookup"><span data-stu-id="48681-105">There is no need to do this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="48681-106">En primer lugar, [conéctese a su clúster ACS basado en DC/OS](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="48681-106">First, [connect to your DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="48681-107">Una vez que haya hecho esto, puede instalar la CLI de DC/OS en el equipo cliente con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="48681-107">Once you have done this, you can install the DC/OS CLI on your client machine with the commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="48681-108">Si usa una versión antigua de Python, puede que observe algunos mensajes "InsecurePlatformWarnings".</span><span class="sxs-lookup"><span data-stu-id="48681-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="48681-109">Puede omitir estos errores con seguridad.</span><span class="sxs-lookup"><span data-stu-id="48681-109">You can safely ignore these.</span></span>

<span data-ttu-id="48681-110">Para empezar a trabajar sin necesidad de reiniciar el shell, ejecute:</span><span class="sxs-lookup"><span data-stu-id="48681-110">In order to get started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="48681-111">Este paso no será necesario si inicia shells nuevos.</span><span class="sxs-lookup"><span data-stu-id="48681-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="48681-112">Ahora puede confirmar que la CLI está instalada:</span><span class="sxs-lookup"><span data-stu-id="48681-112">Now you can confirm that the CLI is installed:</span></span>

```bash
dcos --help
```