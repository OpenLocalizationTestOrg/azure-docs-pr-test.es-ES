---
title: Hola aaaUsing CLI de Azure en Windows | Documentos de Microsoft
description: Uso de hello CLI de Azure en Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>Uso de hello CLI de Azure en Windows

Hola interfaz de línea de comandos (CLI) de Azure proporciona un entorno de scripting para crear y administrar recursos de Azure y la línea de comandos. Hola CLI de Azure está disponible para sistemas operativos Windows, Linux y macOS. En estos sistemas operativos, los comandos de CLI de hello son idénticos, sin embargo, puede diferir la sintaxis de scripting de sistema operativo específico.

Formas de detalles Hola este documento que Hola CLI de Azure se pueden instalar y ejecutar en Windows y detalles de las consideraciones de sintáctico para cada uno. Para documentación más detallada sobre la CLI de Azure, consulte la [documentación de la CLI de Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="windows-subsystem-for-linux"></a>Subsistema de Windows para Linux

Hola subsistema de Windows para Linux (WSL) proporciona un entorno de Ubuntu Linux en aniversario de Windows 10 y versiones posteriores. Cuando está habilitado, WSL proporciona una experiencia de Bash nativa que se puede usar para crear y ejecutar scripts de la CLI de Azure. Como WSL proporciona una experiencia de Bash nativa, los scripts de la CLI de Azure pueden compartirse entre macOS, Linux y Windows sin ninguna modificación.

Hola toouse CLI de Azure en WSL, complete siguiente de Hola.

|Tarea | Instrucciones |
|---|---|
| Habilitación de WSL | [Instalación de la documentación de WSL](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Instalar Hola CLI de Azure |[Instalar Hola CLI en WSL/Ubuntu 14.04](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

Hola CLI de Azure se puede ejecutar de forma nativa en Windows. En esta configuración, paquete de CLI de Azure de hello está instalado en el sistema operativo de Windows de Hola y se pueden ejecutar comandos de PowerShell. En esta configuración, los scripts y comandos de la CLI de Azure se pueden ejecutar en cualquier versión admitida de Windows; sin embargo, se requiere la sintaxis de scripts específica de cada plataforma. Por este motivo, los scripts no se comparten necesariamente entre macOS, Linux y Windows sin ninguna modificación.

Hola toouse CLI de Azure en Windows, instalar el paquete de hello usando estas instrucciones, [Install Hola CLI en Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).

## <a name="docker-image"></a>Imagen de Docker

Al usar Docker para Windows, se puede iniciar una imagen de Docker que incluye Hola CLI de Azure. Esta imagen se basa en Linux e incluye una experiencia de Bash nativa.  Cuando se usa Docker para Windows e imagen de CLI de Azure de hello, toobe de secuencias de comandos que se comparten entre macOS, Linux y Windows. 

Hola toouse CLI de Azure en Docker para Windows, asegúrese de que Docker para Windows se está ejecutando y ejecute el siguiente comando de Hola.

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

Una vez completado, una intensiva de sesión se iniciará decir precargados con herramientas de Azure CLI Hola.

## <a name="next-steps"></a>Pasos siguientes

[Ejemplo de la CLI para máquinas virtuales de Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Ejemplos de la CLI para Azure Web Apps](../../app-service-web/app-service-cli-samples.md)

[Ejemplos de la CLI para SQL de Azure](../../sql-database/sql-database-cli-samples.md)
