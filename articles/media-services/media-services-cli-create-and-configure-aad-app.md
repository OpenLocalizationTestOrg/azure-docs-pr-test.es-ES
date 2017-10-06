---
title: "toocreate aaaUse 2.0 CLI una aplicación de Azure AD y configúrelo tooaccess API de servicios multimedia de Azure | Documentos de Microsoft"
description: "Este tema se muestra cómo toouse CLI 2.0 toocreate una aplicación de Azure AD y configúrelo tooaccess API de servicios multimedia de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a><span data-ttu-id="1146d-103">Utilice CLI 2.0 toocreate una aplicación AAD y configúrelo tooaccess API de servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="1146d-103">Use CLI 2.0 toocreate an AAD app and configure it tooaccess Azure Media Services API</span></span>

<span data-ttu-id="1146d-104">Este tema muestra cómo toouse CLI 2.0 toocreate una aplicación de Azure Active Directory (Azure AD) y servicio principal tooaccess servicios multimedia de Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="1146d-104">This topic shows you how toouse CLI 2.0 toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1146d-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1146d-105">Prerequisites</span></span>

- <span data-ttu-id="1146d-106">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="1146d-106">An Azure account.</span></span> <span data-ttu-id="1146d-107">Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1146d-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="1146d-108">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="1146d-108">A Media Services account.</span></span> <span data-ttu-id="1146d-109">Para obtener más información, consulte [crear una cuenta de servicios multimedia de Azure mediante el portal de Azure de hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="1146d-109">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-hello-azure-cloud-shell"></a><span data-ttu-id="1146d-110">Usar hello Shell en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="1146d-110">Use hello Azure Cloud Shell</span></span>

1. <span data-ttu-id="1146d-111">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1146d-111">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1146d-112">Inicie Hola Shell en la nube desde el panel de navegación superior de hello del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="1146d-112">Launch hello Cloud Shell from hello upper navigation pane of hello portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="1146d-114">Para más información, vea [Introducción a Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="1146d-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a><span data-ttu-id="1146d-115">Crear una aplicación de Azure AD y configurar la cuenta de acceso de medios toohello con CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1146d-115">Create an Azure AD app and configure access toohello media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="1146d-116">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1146d-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="1146d-117">En este ejemplo, Hola **ámbito** es ruta de acceso de recurso completo de Hola para medios de hello cuenta de servicios.</span><span class="sxs-lookup"><span data-stu-id="1146d-117">In this example, hello **scope** is hello full resource path for hello media services account.</span></span> <span data-ttu-id="1146d-118">Sin embargo, Hola **ámbito** puede estar en cualquier nivel.</span><span class="sxs-lookup"><span data-stu-id="1146d-118">However, hello **scope** can be at any level.</span></span>

<span data-ttu-id="1146d-119">Por ejemplo, podría ser uno de hello siguientes niveles:</span><span class="sxs-lookup"><span data-stu-id="1146d-119">For example, it could be one of hello following levels:</span></span>
 
* <span data-ttu-id="1146d-120">Hola **suscripción** nivel.</span><span class="sxs-lookup"><span data-stu-id="1146d-120">hello **subscription** level.</span></span>
* <span data-ttu-id="1146d-121">Hola **grupo de recursos** nivel.</span><span class="sxs-lookup"><span data-stu-id="1146d-121">hello **resource group** level.</span></span>
* <span data-ttu-id="1146d-122">Hola **recursos** (por ejemplo, una cuenta de medios).</span><span class="sxs-lookup"><span data-stu-id="1146d-122">hello **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="1146d-123">Para más información, vea [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="1146d-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="1146d-124">Consulte también [Manage Role-Based el Control de acceso con hello Azure interfaz de línea de comandos](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1146d-124">Also see [Manage Role-Based Access Control with hello Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1146d-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1146d-125">Next steps</span></span>

<span data-ttu-id="1146d-126">Empezar a trabajar con [cargar archivos tooyour cuenta](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="1146d-126">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
