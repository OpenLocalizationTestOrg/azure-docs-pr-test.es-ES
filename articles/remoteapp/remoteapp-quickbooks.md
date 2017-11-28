---
title: "Implementación de QuickBooks en Azure RemoteApp | Microsoft Docs"
description: "Obtenga información acerca de cómo compartir QuickBooks con Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: bbfac45220f6ef36c9951daae0ced1974e8ddabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="36348-103">¿Cómo se implementa QuickBooks en Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="36348-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="36348-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="36348-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="36348-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="36348-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="36348-106">Use la siguiente información para compartir QuickBooks como aplicación en Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="36348-106">Use the following information to share QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="36348-107">Puede compartir QuickBooks 2015 Enterprise con Azure RemoteApp en una colección híbrida o en la nube.</span><span class="sxs-lookup"><span data-stu-id="36348-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="36348-108">El archivo de empresa debe residir en una máquina virtual que está ejecutando el servidor de base de datos de QuickBooks que es independiente de los servidores de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="36348-108">The company file must reside on a VM that is running QuickBooks database server that is separate from the Azure RemoteApp servers.</span></span> <span data-ttu-id="36348-109">No almacene nunca el archivo en la imagen de Azure RemoteApp: se espera una pérdida de datos si lo hace.</span><span class="sxs-lookup"><span data-stu-id="36348-109">Never store the company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="36348-110">Solo QuickBooks Enterprise admite el hospedaje del archivo de QuickBooks en un recurso compartido externo con el servidor de base de datos de QuickBooks accesible a través de redes Windows estándar.</span><span class="sxs-lookup"><span data-stu-id="36348-110">Only QuickBooks Enterprise supports hosting the QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="36348-111">El servidor de base de datos de QuickBooks que hospeda el archivo de empresa debe residir en una máquina virtual independiente dentro de la misma red virtual que la colección de Azure RemoteApp .</span><span class="sxs-lookup"><span data-stu-id="36348-111">The QuickBooks database server that is hosting the company file must reside on a separate VM within the same VNET as the Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a><span data-ttu-id="36348-112">Pasos para implementar QuickBooks</span><span class="sxs-lookup"><span data-stu-id="36348-112">Steps to deploy QuickBooks</span></span>
1. <span data-ttu-id="36348-113">Cree una máquina virtual de Azure e instale QuickBooks, el servidor de base de datos de QuickBooks y coloque el archivo de empresa en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="36348-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place the company file on a Azure VM.</span></span>  <span data-ttu-id="36348-114">Asegúrese de configurar correctamente las reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="36348-114">Make sure to properly configure firewall rules.</span></span>
2. <span data-ttu-id="36348-115">Instale QuickBooks en una[ imagen personalizada](remoteapp-imageoptions.md) y cree una colección de [Azure RemoteApp](remoteapp-collections.md), en la nube o híbrida, dentro de la misma red virtual donde reside la máquina virtual que hospeda el servidor de base de datos de QuickBooks con archivos de empresa.</span><span class="sxs-lookup"><span data-stu-id="36348-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within the exact same VNET where the VM hosting the QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="36348-116">[Publique](remoteapp-publish.md) la aplicación QuickBooks para los usuarios</span><span class="sxs-lookup"><span data-stu-id="36348-116">[Publish](remoteapp-publish.md) QuickBooks app to users</span></span>
4. <span data-ttu-id="36348-117">Inicie el cliente QuickBooks hospedado en Azure RemoteApp, vaya mediante redes estándar Windows a la máquina virtual que hospeda el servidor de base de datos de QuickBooks y abra el archivo de empresa.</span><span class="sxs-lookup"><span data-stu-id="36348-117">Launch the Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking to the VM hosting the QuickBooks database server and open the company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="36348-118">Referencias de documentación</span><span class="sxs-lookup"><span data-stu-id="36348-118">Documentation references</span></span>
* <span data-ttu-id="36348-119">[Configuraciones admitidas](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="36348-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="36348-120">[Opciones de implementación](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="36348-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="36348-121">También puede consultar la presentación de Ignite [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) (Fundamentos de administración y gestión de Microsoft Azure RemoteApp), con un avance rápido hasta 1:02:45 para llegar a la parte de QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="36348-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward to 1:02:45 to get to the QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="36348-122">Arquitectura de implementación</span><span class="sxs-lookup"><span data-stu-id="36348-122">Deployment architecture</span></span>
![Implementación de QuickBooks y RemoteApp de Azure](./media/remoteapp-quickbooks/ra-quickbooks.png)

