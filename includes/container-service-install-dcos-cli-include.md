---
title: Hola aaaInstall DC/OS CLI | Documentos de Microsoft
description: Instalar Hola DC/OS CLI.
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
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> <span data-ttu-id="cdee5-104">Este procedimiento se usa para trabajar con clústeres ACS basados en DC/OS.</span><span class="sxs-lookup"><span data-stu-id="cdee5-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="cdee5-105">No hay ninguna necesidad de toodo esto para los clústeres de ACS basado en el conjunto de.</span><span class="sxs-lookup"><span data-stu-id="cdee5-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="cdee5-106">En primer lugar, [conectar tooyour basadas en DC/OS ACS clúster](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="cdee5-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="cdee5-107">Cuando lo haya hecho esto, puede instalar Hola DC/OS CLI en el equipo cliente con comandos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="cdee5-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="cdee5-108">Si usa una versión antigua de Python, puede que observe algunos mensajes "InsecurePlatformWarnings".</span><span class="sxs-lookup"><span data-stu-id="cdee5-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="cdee5-109">Puede omitir estos errores con seguridad.</span><span class="sxs-lookup"><span data-stu-id="cdee5-109">You can safely ignore these.</span></span>

<span data-ttu-id="cdee5-110">En orden tooget iniciado sin necesidad de reiniciar el shell, ejecute:</span><span class="sxs-lookup"><span data-stu-id="cdee5-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="cdee5-111">Este paso no será necesario si inicia shells nuevos.</span><span class="sxs-lookup"><span data-stu-id="cdee5-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="cdee5-112">Ahora puede confirmar que Hola que CLI está instalado:</span><span class="sxs-lookup"><span data-stu-id="cdee5-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```