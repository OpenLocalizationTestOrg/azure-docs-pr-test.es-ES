---
title: "secretos de almacén de claves de Azure pila de aaaAllow aplicación tooretrieve | Documentos de Microsoft"
description: "Usar un toowork de la aplicación de ejemplo con el almacén de claves de pila de Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/04/2017
ms.author: sngun
ms.openlocfilehash: 2ff3f0bab86d9d1934b463f72124863d29dbe696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-for-key-vault"></a><span data-ttu-id="a8c9f-103">Ejecutar la aplicación de ejemplo de Hola para el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="a8c9f-103">Run hello sample application for Key Vault</span></span>

<span data-ttu-id="a8c9f-104">En esta guía, usará un tooretrieve de la aplicación de ejemplo secretos y las contraseñas desde el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="a8c9f-104">In this guide, you'll use a sample application tooretrieve secrets and passwords from Key Vault.</span></span>

## <a name="download-hello-samples-and-prepare"></a><span data-ttu-id="a8c9f-105">Descargar ejemplos de hello y preparar</span><span class="sxs-lookup"><span data-stu-id="a8c9f-105">Download hello samples and prepare</span></span>
<span data-ttu-id="a8c9f-106">Descargar los ejemplos de cliente del almacén de claves de Azure de Hola de hello [página de ejemplos de cliente de almacén de claves de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="a8c9f-106">Download hello Azure Key Vault client samples from hello [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span>

<span data-ttu-id="a8c9f-107">Extraiga el contenido de hello del equipo local del tooyour de archivo .zip Hola.</span><span class="sxs-lookup"><span data-stu-id="a8c9f-107">Extract hello contents of hello .zip file tooyour local computer.</span></span>

<span data-ttu-id="a8c9f-108">Hola de lectura **README.md** archivo (es decir, un archivo de texto) y, a continuación, siga las instrucciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8c9f-108">Read hello **README.md** file (this is a text file), and then follow hello instructions.</span></span>

## <a name="run-sample-1--hellokeyvault"></a><span data-ttu-id="a8c9f-109">Ejecutar el ejemplo #1: HelloKeyVault</span><span class="sxs-lookup"><span data-stu-id="a8c9f-109">Run Sample #1--HelloKeyVault</span></span>
<span data-ttu-id="a8c9f-110">HelloKeyVault es una aplicación de consola que le guía a través de los escenarios clave de Hola que son compatibles con el almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="a8c9f-110">HelloKeyVault is a console application that walks through hello key scenarios that are supported by Key Vault:</span></span>

1. <span data-ttu-id="a8c9f-111">Crear o importar una clave (clave HSM o software)</span><span class="sxs-lookup"><span data-stu-id="a8c9f-111">Create/import a key (HSM or software key)</span></span>
2. <span data-ttu-id="a8c9f-112">Cifrar un secreto con una clave de contenido</span><span class="sxs-lookup"><span data-stu-id="a8c9f-112">Encrypt a secret using a content key</span></span>
3. <span data-ttu-id="a8c9f-113">Incluir clave de contenido de hello mediante una clave de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="a8c9f-113">Wrap hello content key using a Key Vault key</span></span>
4. <span data-ttu-id="a8c9f-114">Unwrap clave de contenido de Hola</span><span class="sxs-lookup"><span data-stu-id="a8c9f-114">Unwrap hello content key</span></span>
5. <span data-ttu-id="a8c9f-115">Descifrar el secreto de Hola</span><span class="sxs-lookup"><span data-stu-id="a8c9f-115">Decrypt hello secret</span></span>
6. <span data-ttu-id="a8c9f-116">Establecer un secreto</span><span class="sxs-lookup"><span data-stu-id="a8c9f-116">Set a secret</span></span>

<span data-ttu-id="a8c9f-117">Debe ejecutar esa aplicación de consola sin realizar ningún cambio, salvo que los valores de configuración adecuados de hello en el archivo App.Config se actualizará según toohello pasos:</span><span class="sxs-lookup"><span data-stu-id="a8c9f-117">That console application should run with no changes, except that hello appropriate configuration settings in App.Config will be updated according toohello following steps:</span></span>

1. <span data-ttu-id="a8c9f-118">Actualizar valores de configuración de aplicación hello en HelloKeyVault\App.config con su URL del almacén, el Id. de aplicación principal y el secreto.</span><span class="sxs-lookup"><span data-stu-id="a8c9f-118">Update hello app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret.</span></span> <span data-ttu-id="a8c9f-119">información de Hello, opcionalmente, se pueden generar mediante **scripts\GetAppConfigSettings.ps1**.</span><span class="sxs-lookup"><span data-stu-id="a8c9f-119">hello information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.</span></span>
2. <span data-ttu-id="a8c9f-120">Actualizar valores de hello de variables obligatoria de hello en GetAppConfigSettings.ps1.</span><span class="sxs-lookup"><span data-stu-id="a8c9f-120">Update hello values of hello mandatory variables in GetAppConfigSettings.ps1.</span></span>
3. <span data-ttu-id="a8c9f-121">Inicie la ventana de Windows PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8c9f-121">Launch hello Windows PowerShell window.</span></span>
4. <span data-ttu-id="a8c9f-122">Ejecutar script de Hola GetAppConfigSettings.ps1 dentro de la ventana de PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="a8c9f-122">Run hello GetAppConfigSettings.ps1 script within hello PowerShell window.</span></span>
5. <span data-ttu-id="a8c9f-123">Copiar resultados de Hola Hola toohello HelloKeyVault\App.config del archivo de script.</span><span class="sxs-lookup"><span data-stu-id="a8c9f-123">Copy hello results of hello script toohello HelloKeyVault\App.config file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8c9f-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8c9f-124">Next steps</span></span>
[<span data-ttu-id="a8c9f-125">Implementación de una máquina virtual con una contraseña de Key Vault</span><span class="sxs-lookup"><span data-stu-id="a8c9f-125">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="a8c9f-126">Implementación de una máquina virtual con un certificado de Key Vault</span><span class="sxs-lookup"><span data-stu-id="a8c9f-126">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

