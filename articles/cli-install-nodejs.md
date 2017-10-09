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
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="c5b63-103">Instalar Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c5b63-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5b63-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5b63-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="c5b63-105">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="c5b63-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="c5b63-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c5b63-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="c5b63-107">Este tema describe cómo se llama tooinstall hello Azure CLI 1.0, que se integra en nodeJs y es compatible con todas las API de implementación clásica, así como un gran número de actividades de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c5b63-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="c5b63-108">Debe usar hello [CLI de Azure 2.0](/cli/azure/overview) para las implementaciones de CLI de nuevo o prevención y administración.</span><span class="sxs-lookup"><span data-stu-id="c5b63-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="c5b63-109">Instalar rápidamente hello toouse de interfaz de línea de comandos de Azure (Azure CLI 1.0) un conjunto de código abierto basado en el shell de comandos para crear y administrar recursos de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b63-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="c5b63-110">En el equipo tiene varias tooinstall opciones estas herramientas multiplataforma:</span><span class="sxs-lookup"><span data-stu-id="c5b63-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="c5b63-111">**paquete de NPM** : ejecución npm (Administrador de paquetes de saludo de JavaScript) tooinstall Hola paquete más reciente de Azure CLI 1.0 en su sistema operativo o distribución de Linux.</span><span class="sxs-lookup"><span data-stu-id="c5b63-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="c5b63-112">Se requiere que node.js y npm estén instalados en su equipo.</span><span class="sxs-lookup"><span data-stu-id="c5b63-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="c5b63-113">**Instalador** : descargue un instalador para facilitar la instalación en Mac o Windows.</span><span class="sxs-lookup"><span data-stu-id="c5b63-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="c5b63-114">**Contenedor de docker** : comenzar a usar Hola CLI más reciente en un contenedor de Docker listos para ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="c5b63-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="c5b63-115">Se requiere el host de Docker en su equipo.</span><span class="sxs-lookup"><span data-stu-id="c5b63-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="c5b63-116">Para obtener más opciones y segundo plano, consulte repositorio del proyecto de hello en [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="c5b63-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="c5b63-117">Una vez instalado hello Azure CLI 1.0, [conectarse con su suscripción de Azure](xplat-cli-connect.md) ejecución hello y **azure** comandos desde la interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema y así sucesivamente) toowork con los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b63-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="c5b63-118">Opción 1: Instalación de un paquete de NPM</span><span class="sxs-lookup"><span data-stu-id="c5b63-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="c5b63-119">Hola tooinstall CLI desde un paquete npm, asegúrese de que ha descargado e instalado hello [más recientes Node.js y npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="c5b63-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="c5b63-120">A continuación, ejecute **instalar npm** paquete de tooinstall Hola cli de azure:</span><span class="sxs-lookup"><span data-stu-id="c5b63-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="c5b63-121">En las distribuciones de Linux, podría necesitar toouse **sudo** toosuccessfully ejecutar hello **npm** comando, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c5b63-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="c5b63-122">Si necesita tooinstall o actualizar Node.js y npm en su sistema operativo o distribución de Linux, se recomienda que instale la versión más reciente de Node.js LTS de hello (4.x).</span><span class="sxs-lookup"><span data-stu-id="c5b63-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="c5b63-123">Si utiliza una versión anterior, podrían producirse errores de instalación.</span><span class="sxs-lookup"><span data-stu-id="c5b63-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="c5b63-124">Si lo prefiere, descargue Hola Linux más reciente [archivo tar] [ linux-installer] para hello npm paquete localmente.</span><span class="sxs-lookup"><span data-stu-id="c5b63-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="c5b63-125">A continuación, instale el paquete descargado npm de Hola de como se indica a continuación (en las distribuciones de Linux podría necesitar toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="c5b63-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="c5b63-126">Opción 2: Uso de un instalador</span><span class="sxs-lookup"><span data-stu-id="c5b63-126">Option 2: Use an installer</span></span>
<span data-ttu-id="c5b63-127">Si usa un equipo Mac o Windows, está disponible para su descarga Hola siguiente a instaladores CLI:</span><span class="sxs-lookup"><span data-stu-id="c5b63-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="c5b63-128">[Instalador de Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="c5b63-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="c5b63-129">[MSI de Windows][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="c5b63-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="c5b63-130">En Windows, también puede descargar hello [instalador de plataforma Web](https://go.microsoft.com/?linkid=9828653) tooinstall Hola CLI.</span><span class="sxs-lookup"><span data-stu-id="c5b63-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="c5b63-131">Esto deja de instalador Hola tooinstall opción adicional de Azure SDK y herramientas de línea de comandos después de instalar Hola CLI.</span><span class="sxs-lookup"><span data-stu-id="c5b63-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="c5b63-132">Opción 3: Uso de un contenedor Docker</span><span class="sxs-lookup"><span data-stu-id="c5b63-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="c5b63-133">Si ha configurado el equipo como un [Docker](https://docs.docker.com/engine/understanding-docker/) host, puede ejecutar Hola 1.0 más reciente de CLI de Azure en un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="c5b63-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="c5b63-134">Ejecución hello después del comando (en las distribuciones de Linux podría necesitar toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="c5b63-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="c5b63-135">Ejecución de los comandos de la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="c5b63-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="c5b63-136">Después de instala Hola 1.0 de CLI de Azure, ejecute hello **azure** comando desde la interfaz de usuario de línea de comandos (intensiva de errores, Terminal, símbolo del sistema y así sucesivamente).</span><span class="sxs-lookup"><span data-stu-id="c5b63-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="c5b63-137">Por ejemplo, comandos de la Ayuda de toorun hello, escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5b63-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="c5b63-138">En algunas distribuciones de Linux, puede recibir un mensaje de error similar demasiado`/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="c5b63-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="c5b63-139">Este error procede de las instalaciones recientes de Node.js que se instala en /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="c5b63-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="c5b63-140">toofix, cree un vínculo simbólico demasiado/usr/bin/nodo mediante la ejecución de este comando:</span><span class="sxs-lookup"><span data-stu-id="c5b63-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="c5b63-141">versión de hello toosee de hello Azure CLI 1.0 instalado, Hola de tipo siguientes:</span><span class="sxs-lookup"><span data-stu-id="c5b63-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="c5b63-142">De este modo, ya está listo.</span><span class="sxs-lookup"><span data-stu-id="c5b63-142">Now you are ready!</span></span> <span data-ttu-id="c5b63-143">todos los tooaccess Hola toowork de comandos CLI con sus propios recursos, [conectarse tooyour suscripción de Azure desde hello Azure CLI](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c5b63-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c5b63-144">Cuando utiliza CLI de Azure por primera vez, verá un mensaje que pregunta si desea que la información de uso de Microsoft toocollect tooallow.</span><span class="sxs-lookup"><span data-stu-id="c5b63-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="c5b63-145">La participación es voluntaria.</span><span class="sxs-lookup"><span data-stu-id="c5b63-145">Participation is voluntary.</span></span> <span data-ttu-id="c5b63-146">Si elige tooparticipate, puede detener en cualquier momento mediante la ejecución de `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="c5b63-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="c5b63-147">participación de tooenable en cualquier momento, ejecute `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="c5b63-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="c5b63-148">Actualizar Hola CLI</span><span class="sxs-lookup"><span data-stu-id="c5b63-148">Update hello CLI</span></span>
<span data-ttu-id="c5b63-149">Microsoft publica con frecuencia versiones actualizadas de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b63-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="c5b63-150">Vuelva a instalar Hola CLI mediante el instalador de Hola para su sistema operativo, o ejecutar el contenedor Docker más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5b63-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="c5b63-151">O bien, si ha hello Node.js y npm instalado más recientes, actualice escribiendo Hola siguiente (en las distribuciones de Linux podría necesitar toouse **sudo**).</span><span class="sxs-lookup"><span data-stu-id="c5b63-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="c5b63-152">Habilitación de la función de autocompletar</span><span class="sxs-lookup"><span data-stu-id="c5b63-152">Enable tab completion</span></span>
<span data-ttu-id="c5b63-153">La función de autocompletar de los comandos de la CLI es compatible con Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="c5b63-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="c5b63-154">tooenable en zsh, ejecute:</span><span class="sxs-lookup"><span data-stu-id="c5b63-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="c5b63-155">tooenable en intensiva de errores, ejecute:</span><span class="sxs-lookup"><span data-stu-id="c5b63-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="c5b63-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5b63-156">Next steps</span></span>
* <span data-ttu-id="c5b63-157">[Conectarse desde Hola CLI tooyour suscripción de Azure](xplat-cli-connect.md) toocreate y administrar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b63-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="c5b63-158">toolearn más información acerca de hello CLI de Azure, descargar código fuente, informar de problemas, o contribuir proyecto toohello, visite hello [repositorio de GitHub para hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="c5b63-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="c5b63-159">Si tiene alguna pregunta sobre el uso de Hola CLI de Azure o Azure, visite hello [foros de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="c5b63-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
