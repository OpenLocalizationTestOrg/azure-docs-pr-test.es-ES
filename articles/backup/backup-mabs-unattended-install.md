---
title: "instalación de aaaSilent del servidor de copia de seguridad de Azure v2 | Documentos de Microsoft"
description: "Usar un toosilently de secuencia de comandos de PowerShell de instalación v2 del servidor de copia de seguridad de Azure. Este tipo de instalación también se denomina instalación desatendida."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="3e468-104">Ejecutar una instalación desatendida de Azure Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="3e468-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="3e468-105">Obtenga información acerca de cómo toorun una instalación desatendida de v2 del servidor de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e468-105">Learn how toorun an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="3e468-106">Estos pasos no se aplican si va a instalar Azure Backup Server v1.</span><span class="sxs-lookup"><span data-stu-id="3e468-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="3e468-107">Instalar Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="3e468-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="3e468-108">En el servidor de Hola que hospeda el servidor de copia de seguridad de Azure v2, cree un archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="3e468-108">On hello server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="3e468-109">(Puede crear archivo hello en el Bloc de notas o en otro texto editor.) Guarde el archivo hello como MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="3e468-109">(You can create hello file in Notepad or in another text editor.) Save hello file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="3e468-110">Pegue Hola después el código en un archivo MABSSetup.ini Hola.</span><span class="sxs-lookup"><span data-stu-id="3e468-110">Paste hello following code in hello MABSSetup.ini file.</span></span> <span data-ttu-id="3e468-111">Reemplazar texto hello entre corchetes hello (\< \>) con valores de su entorno.</span><span class="sxs-lookup"><span data-stu-id="3e468-111">Replace hello text inside hello brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="3e468-112">Hola después de texto es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3e468-112">hello following text is an example:</span></span>

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. <span data-ttu-id="3e468-113">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="3e468-113">Save hello file.</span></span> <span data-ttu-id="3e468-114">A continuación, en un símbolo con privilegios elevados en el servidor de instalación de hello, escriba este comando:</span><span class="sxs-lookup"><span data-stu-id="3e468-114">Then, at an elevated command prompt on hello installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="3e468-115">Puede usar estas marcas para la instalación de hello:</span><span class="sxs-lookup"><span data-stu-id="3e468-115">You can use these flags for hello installation:</span></span></br><span data-ttu-id="3e468-116">
**/f**: ruta de acceso del archivo .ini</span><span class="sxs-lookup"><span data-stu-id="3e468-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="3e468-117">
**/l**: ruta de acceso del registro</span><span class="sxs-lookup"><span data-stu-id="3e468-117">
**/l**: Log path</span></span></br><span data-ttu-id="3e468-118">
**/i**: ruta de acceso de instalación</span><span class="sxs-lookup"><span data-stu-id="3e468-118">
**/i**: Installation path</span></span></br><span data-ttu-id="3e468-119">
**/x**: ruta de acceso de desinstalación</span><span class="sxs-lookup"><span data-stu-id="3e468-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="3e468-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e468-120">Next steps</span></span>
<span data-ttu-id="3e468-121">Después de instalar el servidor de copia de seguridad, obtenga información acerca de cómo tooprepare el servidor, o empezar a proteger una carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3e468-121">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="3e468-122">Preparar cargas de trabajo de Backup Server</span><span class="sxs-lookup"><span data-stu-id="3e468-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="3e468-123">Usar tooback del servidor de copia de seguridad de un servidor de VMware</span><span class="sxs-lookup"><span data-stu-id="3e468-123">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="3e468-124">Usar tooback del servidor de copia de seguridad de SQL Server</span><span class="sxs-lookup"><span data-stu-id="3e468-124">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="3e468-125">Agregar almacenamiento de copia de seguridad moderna tooBackup Server</span><span class="sxs-lookup"><span data-stu-id="3e468-125">Add Modern Backup Storage tooBackup Server</span></span>](backup-mabs-add-storage.md)
