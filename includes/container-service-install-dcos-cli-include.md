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
> Este procedimiento se usa para trabajar con clústeres ACS basados en DC/OS. No hay ninguna necesidad de toodo esto para los clústeres de ACS basado en el conjunto de.
> 
> 

En primer lugar, [conectar tooyour basadas en DC/OS ACS clúster](../articles/container-service/container-service-connect.md). Cuando lo haya hecho esto, puede instalar Hola DC/OS CLI en el equipo cliente con comandos de hello siguientes:

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

Si usa una versión antigua de Python, puede que observe algunos mensajes "InsecurePlatformWarnings". Puede omitir estos errores con seguridad.

En orden tooget iniciado sin necesidad de reiniciar el shell, ejecute:

```bash
source ~/.bashrc
```

Este paso no será necesario si inicia shells nuevos.

Ahora puede confirmar que Hola que CLI está instalado:

```bash
dcos --help
```