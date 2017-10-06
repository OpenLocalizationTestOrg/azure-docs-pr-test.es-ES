---
title: "características de Shell en la nube (versión preliminar) aaaAzure | Documentos de Microsoft"
description: "Introducción a las características de Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a>Características y herramientas para Azure Cloud Shell
Shell de nube de Azure es un toomanage de experiencia de shell basado en un explorador y desarrollar recursos de Azure.

Shell de nube ofrece un explorador accesible, preconfigurado y experiencia de shell de administración de recursos de Azure sin sobrecarga de Hola de instalar, control de versiones y el mantenimiento de una máquina usted mismo.

Cloud Shell aprovisiona máquinas a medida que se solicitan y, por tanto, el estado de la máquina no se conservará entre sesiones. Como Cloud Shell se ha creado para sesiones interactivas, los shells finalizan automáticamente después de 20 minutos de inactividad.

## <a name="bash-in-cloud-shell"></a>Bash en Cloud Shell
### <a name="tools"></a>Herramientas
|Categoría   |Nombre   |
|---|---|
|Intérprete de shell de Linux|Bash<br> sh               |
|Herramientas de Azure            |[CLI de Azure 2.0](https://github.com/Azure/azure-cli) y [1.0](https://github.com/Azure/azure-xplat-cli)<br> [AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Batch Shipyard](https://github.com/Azure/batch-shipyard)     |
|Editores de texto           |vim<br> nano<br> emacs       |
|Control de código fuente         |git                    |
|Herramientas de compilación            |make<br> maven<br> npm<br> pip         |
|Contenedores             |[CLI de Docker](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Draft](https://github.com/Azure/draft)<br> [CLI de DC/OS](https://github.com/dcos/dcos-cli)         |
|Bases de datos              |Cliente de MySQL<br> Cliente de PostgreSql<br> [Utilidad sqlcmd](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli) |
|Otros                  |Cliente de iPython<br> [CLI de Cloud Foundry](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a>Compatibilidad con idiomas
|language   |Versión   |
|---|---|
|.NET       |1.01       |
|Go         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|Python     |2.7 y 3.5 (predeterminadas)|

## <a name="secure-automatic-authentication"></a>Protección de la autenticación automática
En la nube Shell automáticamente y de forma segura autentica el acceso de cuenta de hello 2.0 de CLI de Azure.

## <a name="azure-files-persistence"></a>Persistencia de Azure Files
Dado que Cloud Shell se asigna para cada solicitud mediante una máquina temporal, los archivos fuera de $Home y el estado de la máquina no se conservan entre sesiones.
archivos de toopersist entre las sesiones, los recorridos de Shell en la nube a través de adjuntar un archivo de Azure comparten en el primer inicio.
Una vez finalizado, Cloud Shell conectará automáticamente su almacenamiento para todas las sesiones futuras.

[Más información acerca de cómo adjuntar tooCloud de recursos compartidos de archivos de Azure Shell.](persisting-shell-storage.md)

## <a name="next-steps"></a>Pasos siguientes
[Inicio rápido de Cloud Shell](quickstart.md) <br>
[Más información sobre la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/) <br>