---
title: una imagen de Azure RemoteApp aaaCreate | Documentos de Microsoft
description: "Obtener información sobre opciones de hello disponibles para la creación de imágenes para Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="c30d3-103">Creación de una imagen de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="c30d3-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c30d3-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="c30d3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c30d3-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="c30d3-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c30d3-106">RemoteApp de Azure utiliza imágenes toohold Hola aplicaciones que se comparten con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c30d3-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="c30d3-107">(Tomamos la imagen y usar las máquinas virtuales de toocreate - que el acceso a los usuarios de hello cuando inician sesión en Azure RemoteApp.) toocreate una colección de RemoteApp de Azure con su elección de las aplicaciones, ya sea en la nube o híbridas, primero debe crear una imagen con esas aplicaciones instaladas.</span><span class="sxs-lookup"><span data-stu-id="c30d3-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="c30d3-108">A continuación, cree una recopilación que use esa imagen, asignar a usuarios colección toohello y publicar los usuarios toothose de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c30d3-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="c30d3-109">Tiene varias opciones para crear o utilizar imágenes.</span><span class="sxs-lookup"><span data-stu-id="c30d3-109">You have several options for creating or using images.</span></span> <span data-ttu-id="c30d3-110">Hola básica [requisito](remoteapp-imagereqs.md) para una imagen que ejecutan Windows Server 2012 R2 y tiene instalado el rol de Host de sesión de escritorio remoto (RDSH) de Hola.</span><span class="sxs-lookup"><span data-stu-id="c30d3-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="c30d3-111">La forma de conseguir esto es lo que resulta interesante.</span><span class="sxs-lookup"><span data-stu-id="c30d3-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="c30d3-112">Tiene las siguientes opciones cuando se trata de tooimages de Hola:</span><span class="sxs-lookup"><span data-stu-id="c30d3-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="c30d3-113">Puede importar y utilizar una [imagen basada en una máquina virtual de Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="c30d3-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="c30d3-114">Esto es una buena opción para aplicaciones de línea de negocio que requieren una configuración personalizada.</span><span class="sxs-lookup"><span data-stu-id="c30d3-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="c30d3-115">Puede personalizar hello toowork de imagen para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c30d3-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="c30d3-116">Puede [crear y cargar una imagen personalizada](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="c30d3-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="c30d3-117">Esto es apropiado si ya tiene una imagen que se utiliza para la implementación local de Servicios de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="c30d3-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="c30d3-118">Puede usar uno de hello [imágenes de plantilla](remoteapp-images.md) incluido en su suscripción de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c30d3-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="c30d3-119">Estas imágenes se crean y mantenido por el equipo de RemoteApp de Hola y contienen algunas aplicaciones estándares (por ejemplo, hello Office suite) que puede hacer que los usuarios de tooyour disponible.</span><span class="sxs-lookup"><span data-stu-id="c30d3-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="c30d3-120">Tenga en cuenta que esa imagen de Office 365 Pro Plus Hola sola puede usarse en un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c30d3-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="c30d3-121">Independientemente de dónde obtener la imagen o cómo crear, es conveniente que comprenden hello toomake [requisitos de la aplicación](remoteapp-appreqs.md) tooensure que la aplicación funciona bien en RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c30d3-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="c30d3-122">A continuación, el paso siguiente de hello es toocreate una [nube](remoteapp-create-cloud-deployment.md) o [híbrida](remoteapp-create-hybrid-deployment.md) colección.</span><span class="sxs-lookup"><span data-stu-id="c30d3-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

