---
title: Hola aaaInstall 1.0 de CLI de Azure | Documentos de Microsoft
description: Instalar hello 1.0 de CLI de Azure para Mac, Linux y Windows toostart mediante los servicios de Azure
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a>Instalar Hola 1.0 de CLI de Azure
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [CLI de Azure 1.0](cli-install-nodejs.md)
> * [CLI de Azure 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> Este tema describe cómo se llama tooinstall hello Azure CLI 1.0, que se integra en nodeJs y es compatible con todas las API de implementación clásica, así como un gran número de actividades de implementación del Administrador de recursos. Debe usar hello [CLI de Azure 2.0](/cli/azure/overview) para las implementaciones de CLI de nuevo o prevención y administración.

Instalar rápidamente hello toouse de interfaz de línea de comandos de Azure (Azure CLI 1.0) un conjunto de código abierto basado en el shell de comandos para crear y administrar recursos de Microsoft Azure. En el equipo tiene varias tooinstall opciones estas herramientas multiplataforma:

* **paquete de NPM** : ejecución npm (Administrador de paquetes de saludo de JavaScript) tooinstall Hola paquete más reciente de Azure CLI 1.0 en su sistema operativo o distribución de Linux. Se requiere que node.js y npm estén instalados en su equipo.
* **Instalador** : descargue un instalador para facilitar la instalación en Mac o Windows.
* **Contenedor de docker** : comenzar a usar Hola CLI más reciente en un contenedor de Docker listos para ejecutarse. Se requiere el host de Docker en su equipo.

Para obtener más opciones y segundo plano, consulte repositorio del proyecto de hello en [GitHub](https://github.com/azure/azure-xplat-cli).

Una vez instalado hello Azure CLI 1.0, [conectarse con su suscripción de Azure](xplat-cli-connect.md) ejecución hello y **azure** comandos desde la interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema y así sucesivamente) toowork con los recursos de Azure.

## <a name="option-1-install-an-npm-package"></a>Opción 1: Instalación de un paquete de NPM
Hola tooinstall CLI desde un paquete npm, asegúrese de que ha descargado e instalado hello [más recientes Node.js y npm](https://nodejs.org/en/download/package-manager/). A continuación, ejecute **instalar npm** paquete de tooinstall Hola cli de azure:

```bash
npm install -g azure-cli
```

En las distribuciones de Linux, podría necesitar toouse **sudo** toosuccessfully ejecutar hello **npm** comando, como se indica a continuación:

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> Si necesita tooinstall o actualizar Node.js y npm en su sistema operativo o distribución de Linux, se recomienda que instale la versión más reciente de Node.js LTS de hello (4.x). Si utiliza una versión anterior, podrían producirse errores de instalación.

Si lo prefiere, descargue Hola Linux más reciente [archivo tar] [ linux-installer] para hello npm paquete localmente. A continuación, instale el paquete descargado npm de Hola de como se indica a continuación (en las distribuciones de Linux podría necesitar toouse **sudo**):

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>Opción 2: Uso de un instalador
Si usa un equipo Mac o Windows, está disponible para su descarga Hola siguiente a instaladores CLI:

* [Instalador de Mac OS X][mac-installer]
* [MSI de Windows][windows-installer]

> [!TIP]
> En Windows, también puede descargar hello [instalador de plataforma Web](https://go.microsoft.com/?linkid=9828653) tooinstall Hola CLI. Esto deja de instalador Hola tooinstall opción adicional de Azure SDK y herramientas de línea de comandos después de instalar Hola CLI.

## <a name="option-3-use-a-docker-container"></a>Opción 3: Uso de un contenedor Docker
Si ha configurado el equipo como un [Docker](https://docs.docker.com/engine/understanding-docker/) host, puede ejecutar Hola 1.0 más reciente de CLI de Azure en un contenedor de Docker. Ejecución hello después del comando (en las distribuciones de Linux podría necesitar toouse **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Ejecución de los comandos de la CLI de Azure 1.0
Después de instala Hola 1.0 de CLI de Azure, ejecute hello **azure** comando desde la interfaz de usuario de línea de comandos (intensiva de errores, Terminal, símbolo del sistema y así sucesivamente). Por ejemplo, comandos de la Ayuda de toorun hello, escriba Hola siguiente:

```azurecli
azure help
```

> [!NOTE]
> En algunas distribuciones de Linux, puede recibir un mensaje de error similar demasiado`/usr/bin/env: ‘node’: No such file or directory`. Este error procede de las instalaciones recientes de Node.js que se instala en /usr/bin/nodejs. toofix, cree un vínculo simbólico demasiado/usr/bin/nodo mediante la ejecución de este comando:

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

versión de hello toosee de hello Azure CLI 1.0 instalado, Hola de tipo siguientes:

```azurecli
azure --version
```

De este modo, ya está listo. todos los tooaccess Hola toowork de comandos CLI con sus propios recursos, [conectarse tooyour suscripción de Azure desde hello Azure CLI](xplat-cli-connect.md).

> [!NOTE]
> Cuando utiliza CLI de Azure por primera vez, verá un mensaje que pregunta si desea que la información de uso de Microsoft toocollect tooallow. La participación es voluntaria. Si elige tooparticipate, puede detener en cualquier momento mediante la ejecución de `azure telemetry --disable`. participación de tooenable en cualquier momento, ejecute `azure telemetry --enable`.

## <a name="update-hello-cli"></a>Actualizar Hola CLI
Microsoft publica con frecuencia versiones actualizadas de hello CLI de Azure. Vuelva a instalar Hola CLI mediante el instalador de Hola para su sistema operativo, o ejecutar el contenedor Docker más reciente de Hola. O bien, si ha hello Node.js y npm instalado más recientes, actualice escribiendo Hola siguiente (en las distribuciones de Linux podría necesitar toouse **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>Habilitación de la función de autocompletar
La función de autocompletar de los comandos de la CLI es compatible con Mac y Linux.

tooenable en zsh, ejecute:

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable en intensiva de errores, ejecute:

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>Pasos siguientes
* [Conectarse desde Hola CLI tooyour suscripción de Azure](xplat-cli-connect.md) toocreate y administrar recursos de Azure.
* toolearn más información acerca de hello CLI de Azure, descargar código fuente, informar de problemas, o contribuir proyecto toohello, visite hello [repositorio de GitHub para hello Azure CLI](https://github.com/azure/azure-xplat-cli).
* Si tiene alguna pregunta sobre el uso de Hola CLI de Azure o Azure, visite hello [foros de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
