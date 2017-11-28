---
title: "Nunca almacene datos confidenciales en imágenes personalizadas para Azure RemoteApp | Microsoft Docs"
description: "Obtenga información acerca de las directrices para almacenar datos en imágenes personalizadas en Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="cd6dd-103">Nunca almacene información confidencial en imágenes personalizadas</span><span class="sxs-lookup"><span data-stu-id="cd6dd-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cd6dd-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cd6dd-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="cd6dd-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cd6dd-106">Cuando hospede su propia aplicación en Azure RemoteApp, el primer paso es crear una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span></span> <span data-ttu-id="cd6dd-107">Usamos esa imagen personalizada para crear instancias de máquina virtual que sirvan las aplicaciones a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-107">We use that custom image to create VM instances that serve your apps to your users.</span></span> <span data-ttu-id="cd6dd-108">La imagen personalizada debe contener SOLO aplicaciones y nunca datos confidenciales que se puedan perder, como bases de datos SQL, archivos de personal o archivos de datos especiales como archivos de empresa de QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="cd6dd-109">Todos los datos confidenciales deben ser externos a Azure RemoteApp en un servidor de archivos, otra máquina virtual de Azure o SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="cd6dd-110">La imagen solo debe hospedar la aplicación que se conecta al origen de datos y presenta los datos.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-110">The image should just host the application that connects to the data source and presents the data.</span></span> <span data-ttu-id="cd6dd-111">Consulte [Requisitos para las imágenes Azure RemoteApp](remoteapp-imagereqs.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="cd6dd-112">Para entender por qué no debe almacenar datos confidenciales, debe entender cómo funciona Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span></span> <span data-ttu-id="cd6dd-113">Cuando se crea o actualiza una colección, se crean varios clones o copias de la imagen entre bambalinas.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span></span> <span data-ttu-id="cd6dd-114">Todas estas instancias de máquina virtual son réplicas exactas de la imagen personalizada. Cuando los usuarios inician aplicaciones, se conectan a una de estas instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span></span> <span data-ttu-id="cd6dd-115">Sin embargo, no se garantiza la misma instancia y no debe importar porque son no persistentes.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="cd6dd-116">Las instancias de máquina virtual que hospedan las aplicaciones no son persistentes y pueden destruirse o eliminarse, por ejemplo, durante la actualización de la colección.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="cd6dd-117">Una vez que se aprovisiona la colección y los usuarios empiecen a conectarse a las máquinas virtuales, los datos de usuario son persistentes y se protegen porque se guardan en un almacenamiento independiente dentro de un VHD que llamamos un [disco de perfil de usuario (UPD)](remoteapp-upd.md), que es el perfil de usuario en c:\users\<perfilusuario>.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="cd6dd-118">Cuando se inicia una aplicación, el UPD se monta y se tratan como un perfil de usuario local por el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span></span> <span data-ttu-id="cd6dd-119">Obtenga más información sobre cómo [Azure RemoteApp guarda la configuración y los datos de usuario](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="cd6dd-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="cd6dd-120">Datos de ejemplo que no deben residir en la imagen:</span><span class="sxs-lookup"><span data-stu-id="cd6dd-120">Example data that should not reside in the image:</span></span>

* <span data-ttu-id="cd6dd-121">Datos compartidos de los usuarios para obtener acceso a</span><span class="sxs-lookup"><span data-stu-id="cd6dd-121">Shared data for users to access</span></span>
* <span data-ttu-id="cd6dd-122">Base de datos SQL o Base de datos QuickBooks</span><span class="sxs-lookup"><span data-stu-id="cd6dd-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="cd6dd-123">Todos los datos en D:\\</span><span class="sxs-lookup"><span data-stu-id="cd6dd-123">Any data in D:\\</span></span>

<span data-ttu-id="cd6dd-124">Los datos de ejemplo que pueden residir en el perfil predeterminado que se copiará en cada UPD de todos los usuarios:</span><span class="sxs-lookup"><span data-stu-id="cd6dd-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span></span>

* <span data-ttu-id="cd6dd-125">Archivos de configuración por usuario</span><span class="sxs-lookup"><span data-stu-id="cd6dd-125">Configuration files per user</span></span>
* <span data-ttu-id="cd6dd-126">Scripts que los usuarios tendrían que conservar en el UPD</span><span class="sxs-lookup"><span data-stu-id="cd6dd-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="cd6dd-127">Puntos clave:</span><span class="sxs-lookup"><span data-stu-id="cd6dd-127">Key points:</span></span>

* <span data-ttu-id="cd6dd-128">Nunca almacene datos confidenciales que se pueden perder en la imagen cuando cree una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-128">Never store sensitive data that can be lost on the image when creating a custom image.</span></span>
* <span data-ttu-id="cd6dd-129">Los datos confidenciales siempre deben residir en un servidor de archivos independiente, una máquina virtual de Azure independiente, en la nube y siempre deben ser externos a las instancias de máquina virtual que hospedan las aplicaciones en Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cd6dd-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="cd6dd-130">Los datos de usuario se guardan y se conserva en el disco de perfil de usuario (UDP)</span><span class="sxs-lookup"><span data-stu-id="cd6dd-130">User data is saved and persists in the user profile disk (UPD)</span></span>

