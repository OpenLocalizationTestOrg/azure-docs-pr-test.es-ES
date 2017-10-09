---
title: aaaDeploy QuickBooks en Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooshare QuickBooks con Azure RemoteApp."
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
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="0f904-103">¿Cómo se implementa QuickBooks en Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="0f904-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0f904-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="0f904-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0f904-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0f904-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0f904-106">Usar hello después información tooshare QuickBooks como una aplicación en Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0f904-106">Use hello following information tooshare QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="0f904-107">Puede compartir QuickBooks 2015 Enterprise con Azure RemoteApp en una colección híbrida o en la nube.</span><span class="sxs-lookup"><span data-stu-id="0f904-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="0f904-108">archivo de empresa de Hello debe residir en una máquina virtual que está ejecutando el servidor de base de datos de QuickBooks que es independiente de los servidores de hello Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0f904-108">hello company file must reside on a VM that is running QuickBooks database server that is separate from hello Azure RemoteApp servers.</span></span> <span data-ttu-id="0f904-109">Archivo de empresa de hello en la imagen de Azure RemoteApp no almacene nunca: pérdida de datos se espera que si lo hace.</span><span class="sxs-lookup"><span data-stu-id="0f904-109">Never store hello company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="0f904-110">Sólo QuickBooks Enterprise es compatible con hospedaje archivo QuickBooks de hello en un recurso compartido externo con el servidor de base de datos de QuickBooks accesible a través de redes de Windows estándar.</span><span class="sxs-lookup"><span data-stu-id="0f904-110">Only QuickBooks Enterprise supports hosting hello QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="0f904-111">Hello servidor de base de datos de QuickBooks que hospeda el archivo de empresa de hello debe residir en una máquina virtual independiente dentro de hello misma red virtual como Hola colección RemoteApp de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f904-111">hello QuickBooks database server that is hosting hello company file must reside on a separate VM within hello same VNET as hello Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a><span data-ttu-id="0f904-112">Pasos toodeploy QuickBooks</span><span class="sxs-lookup"><span data-stu-id="0f904-112">Steps toodeploy QuickBooks</span></span>
1. <span data-ttu-id="0f904-113">Crear una máquina virtual de Azure, instale QuickBooks, servidor de base de datos de QuickBooks y coloque el archivo de empresa de hello en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f904-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place hello company file on a Azure VM.</span></span>  <span data-ttu-id="0f904-114">Asegúrese de que tooproperly configurar reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="0f904-114">Make sure tooproperly configure firewall rules.</span></span>
2. <span data-ttu-id="0f904-115">Instalar QuickBooks en un [imagen personalizada](remoteapp-imageoptions.md) y crear un [colección de Azure RemoteApp](remoteapp-collections.md), en la nube o híbridas, dentro de hello exactamente la misma red virtual donde hospedaje de máquinas virtuales de Hola Hola servidor de base de datos de QuickBooks con archivos de la compañía se encuentra.</span><span class="sxs-lookup"><span data-stu-id="0f904-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within hello exact same VNET where hello VM hosting hello QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="0f904-116">[Publicar](remoteapp-publish.md) toousers de aplicación de QuickBooks</span><span class="sxs-lookup"><span data-stu-id="0f904-116">[Publish](remoteapp-publish.md) QuickBooks app toousers</span></span>
4. <span data-ttu-id="0f904-117">Iniciar a cliente QuickBooks hospedados en Azure RemoteApp de hello, navegar con el servidor de base de datos de toohello VM hospedaje Hola QuickBooks de red de Windows estándar y abra el archivo de empresa de hello.</span><span class="sxs-lookup"><span data-stu-id="0f904-117">Launch hello Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking toohello VM hosting hello QuickBooks database server and open hello company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="0f904-118">Referencias de documentación</span><span class="sxs-lookup"><span data-stu-id="0f904-118">Documentation references</span></span>
* <span data-ttu-id="0f904-119">[Configuraciones admitidas](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="0f904-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="0f904-120">[Opciones de implementación](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="0f904-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="0f904-121">También puede desproteger la presentación de Ignite [conceptos básicos de Microsoft Azure RemoteApp administración y administración](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -avancemos too1:02:45 tooget toohello QuickBooks parte.</span><span class="sxs-lookup"><span data-stu-id="0f904-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward too1:02:45 tooget toohello QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="0f904-122">Arquitectura de implementación</span><span class="sxs-lookup"><span data-stu-id="0f904-122">Deployment architecture</span></span>
![Implementación de QuickBooks y RemoteApp de Azure](./media/remoteapp-quickbooks/ra-quickbooks.png)

