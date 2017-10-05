---
title: "Permitir a la aplicación recuperar los secretos del almacén de claves de Azure Stack | Microsoft Docs"
description: "Usar una aplicación de ejemplo para trabajar con el almacén de claves de Azure Stack"
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
ms.openlocfilehash: 4b517526d89e7f6c2649e2f12810b4db705defa3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="run-the-sample-application-for-key-vault"></a><span data-ttu-id="49d25-103">Ejecutar la aplicación de ejemplo para el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="49d25-103">Run the sample application for Key Vault</span></span>

<span data-ttu-id="49d25-104">En esta guía, deberá usar una aplicación de ejemplo para recuperar los secretos y las contraseñas desde el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="49d25-104">In this guide, you'll use a sample application to retrieve secrets and passwords from Key Vault.</span></span>

## <a name="download-the-samples-and-prepare"></a><span data-ttu-id="49d25-105">Descargue las muestras y preparar</span><span class="sxs-lookup"><span data-stu-id="49d25-105">Download the samples and prepare</span></span>
<span data-ttu-id="49d25-106">Descargar los ejemplos de cliente del almacén de claves de Azure desde el [página de ejemplos de cliente de almacén de claves de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="49d25-106">Download the Azure Key Vault client samples from the [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span>

<span data-ttu-id="49d25-107">Extraiga el contenido del archivo .zip en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="49d25-107">Extract the contents of the .zip file to your local computer.</span></span>

<span data-ttu-id="49d25-108">Leer la **README.md** archivo (es decir, un archivo de texto) y, a continuación, siga las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="49d25-108">Read the **README.md** file (this is a text file), and then follow the instructions.</span></span>

## <a name="run-sample-1--hellokeyvault"></a><span data-ttu-id="49d25-109">Ejecutar el ejemplo #1: HelloKeyVault</span><span class="sxs-lookup"><span data-stu-id="49d25-109">Run Sample #1--HelloKeyVault</span></span>
<span data-ttu-id="49d25-110">HelloKeyVault es una aplicación de consola que le guía a través de los escenarios clave que son compatibles con el almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="49d25-110">HelloKeyVault is a console application that walks through the key scenarios that are supported by Key Vault:</span></span>

1. <span data-ttu-id="49d25-111">Crear o importar una clave (clave HSM o software)</span><span class="sxs-lookup"><span data-stu-id="49d25-111">Create/import a key (HSM or software key)</span></span>
2. <span data-ttu-id="49d25-112">Cifrar un secreto con una clave de contenido</span><span class="sxs-lookup"><span data-stu-id="49d25-112">Encrypt a secret using a content key</span></span>
3. <span data-ttu-id="49d25-113">Ajustar la clave de contenido utilizando una clave de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="49d25-113">Wrap the content key using a Key Vault key</span></span>
4. <span data-ttu-id="49d25-114">Desempaquetar la clave de contenido</span><span class="sxs-lookup"><span data-stu-id="49d25-114">Unwrap the content key</span></span>
5. <span data-ttu-id="49d25-115">Descifrar el secreto</span><span class="sxs-lookup"><span data-stu-id="49d25-115">Decrypt the secret</span></span>
6. <span data-ttu-id="49d25-116">Establecer un secreto</span><span class="sxs-lookup"><span data-stu-id="49d25-116">Set a secret</span></span>

<span data-ttu-id="49d25-117">Esa aplicación de consola debe ejecutar sin cambios, excepto en que los valores de configuración adecuado en el archivo App.Config se actualizarán según los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="49d25-117">That console application should run with no changes, except that the appropriate configuration settings in App.Config will be updated according to the following steps:</span></span>

1. <span data-ttu-id="49d25-118">Actualice los valores de configuración de aplicación en HelloKeyVault\App.config con su URL del almacén, el Id. de aplicación principal y el secreto.</span><span class="sxs-lookup"><span data-stu-id="49d25-118">Update the app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret.</span></span> <span data-ttu-id="49d25-119">Opcionalmente, se pueden generar la información mediante **scripts\GetAppConfigSettings.ps1**.</span><span class="sxs-lookup"><span data-stu-id="49d25-119">The information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.</span></span>
2. <span data-ttu-id="49d25-120">Actualice los valores de las variables en GetAppConfigSettings.ps1 obligatorios.</span><span class="sxs-lookup"><span data-stu-id="49d25-120">Update the values of the mandatory variables in GetAppConfigSettings.ps1.</span></span>
3. <span data-ttu-id="49d25-121">Inicie la ventana de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49d25-121">Launch the Windows PowerShell window.</span></span>
4. <span data-ttu-id="49d25-122">Ejecute el script GetAppConfigSettings.ps1 dentro de la ventana de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49d25-122">Run the GetAppConfigSettings.ps1 script within the PowerShell window.</span></span>
5. <span data-ttu-id="49d25-123">Copiar los resultados de la secuencia de comandos en el archivo HelloKeyVault\App.config.</span><span class="sxs-lookup"><span data-stu-id="49d25-123">Copy the results of the script to the HelloKeyVault\App.config file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49d25-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49d25-124">Next steps</span></span>
[<span data-ttu-id="49d25-125">Implementación de una máquina virtual con una contraseña de Key Vault</span><span class="sxs-lookup"><span data-stu-id="49d25-125">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="49d25-126">Implementación de una máquina virtual con un certificado de Key Vault</span><span class="sxs-lookup"><span data-stu-id="49d25-126">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

