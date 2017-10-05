---
title: "Creación de una imagen de Azure RemoteApp | Microsoft Docs"
description: "Obtenga información acerca de las opciones disponibles para la creación de imágenes para Azure RemoteApp."
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
ms.openlocfilehash: 4b8ba6f264f982e03930c5ad4ccdb2d80f2c8665
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="a8d18-103">Creación de una imagen de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="a8d18-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a8d18-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="a8d18-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a8d18-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="a8d18-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a8d18-106">Azure RemoteApp usa imágenes para mantener las aplicaciones que se comparten con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a8d18-106">Azure RemoteApp uses images to hold the apps that you share with your users.</span></span> <span data-ttu-id="a8d18-107">(Tomamos su imagen y la usamos para crear máquinas virtuales, que es a lo que acceden los usuarios cuando inician sesión en Azure RemoteApp). Para crear una colección de Azure RemoteApp con las aplicaciones de su elección, ya estén en la nube o sean híbridas, empiece por crear una imagen con esas aplicaciones instaladas.</span><span class="sxs-lookup"><span data-stu-id="a8d18-107">(We take your image and use it to create VMs - that's what the users access when they sign into Azure RemoteApp.) To create an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="a8d18-108">A continuación, cree una colección que utiliza esa imagen, asigne usuarios a la colección y publique aplicaciones para esos usuarios.</span><span class="sxs-lookup"><span data-stu-id="a8d18-108">Then, create a collection that uses that image, assign users to the collection, and publish apps to those users.</span></span>

<span data-ttu-id="a8d18-109">Tiene varias opciones para crear o utilizar imágenes.</span><span class="sxs-lookup"><span data-stu-id="a8d18-109">You have several options for creating or using images.</span></span> <span data-ttu-id="a8d18-110">El [requisito](remoteapp-imagereqs.md) básico para una imagen es que ejecute Windows Server 2012 R2 y tenga instalado el rol de host de sesión de Escritorio remoto (RDSH).</span><span class="sxs-lookup"><span data-stu-id="a8d18-110">The basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have the Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="a8d18-111">La forma de conseguir esto es lo que resulta interesante.</span><span class="sxs-lookup"><span data-stu-id="a8d18-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="a8d18-112">Tiene las siguientes opciones cuando se trata de imágenes:</span><span class="sxs-lookup"><span data-stu-id="a8d18-112">You have the following options when it comes to images:</span></span>

* <span data-ttu-id="a8d18-113">Puede importar y utilizar una [imagen basada en una máquina virtual de Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="a8d18-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="a8d18-114">Esto es una buena opción para aplicaciones de línea de negocio que requieren una configuración personalizada.</span><span class="sxs-lookup"><span data-stu-id="a8d18-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="a8d18-115">Puede personalizar la imagen para que funcione para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a8d18-115">You can customize the image to work for the app.</span></span>
* <span data-ttu-id="a8d18-116">Puede [crear y cargar una imagen personalizada](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="a8d18-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="a8d18-117">Esto es apropiado si ya tiene una imagen que se utiliza para la implementación local de Servicios de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="a8d18-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="a8d18-118">Puede utilizar una de las [imágenes de plantilla](remoteapp-images.md) incluidas en su suscripción de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a8d18-118">You can use one of the [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="a8d18-119">Estas imágenes se crean y mantienen por parte del equipo de RemoteApp y contienen algunas aplicaciones estándar (por ejemplo, el conjunto de programas de Office) que puede poner a disposición de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a8d18-119">These images are created and maintained by the RemoteApp team and contain some standard applications (like the Office suite) that you can make available to your users.</span></span> <span data-ttu-id="a8d18-120">Tenga en cuenta que la imagen Office 365 Pro Plus se puede utilizar en una configuración de producción.</span><span class="sxs-lookup"><span data-stu-id="a8d18-120">Note that only the Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="a8d18-121">Independientemente de dónde obtenga la imagen o de cómo la cree, es importante que entienda los [requisitos de la aplicación](remoteapp-appreqs.md) para garantizar que la aplicación funciona bien en RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a8d18-121">Regardless of where you get your image or how you create it, you'll want to make sure you understand the [app requirements](remoteapp-appreqs.md) to ensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="a8d18-122">A continuación, el siguiente paso es crear una colección en la [nube](remoteapp-create-cloud-deployment.md) o [híbrida](remoteapp-create-hybrid-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a8d18-122">Then, the next step is to create a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

