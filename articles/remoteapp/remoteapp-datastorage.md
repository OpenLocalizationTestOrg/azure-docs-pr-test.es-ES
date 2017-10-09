---
title: "aaaNever almacén de datos confidenciales en imágenes personalizadas para Azure RemoteApp | Documentos de Microsoft"
description: "Obtenga información acerca de las instrucciones de Hola para almacenar datos en imágenes personalizadas en Azure RemoteApp"
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
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="67737-103">Nunca almacene información confidencial en imágenes personalizadas</span><span class="sxs-lookup"><span data-stu-id="67737-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="67737-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="67737-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="67737-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="67737-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="67737-106">Si hospeda su propia aplicación en Azure RemoteApp, Hola primer paso es toocreate una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="67737-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="67737-107">Utilizamos ese instancias de máquina virtual de toocreate de imagen personalizada que atienden a sus aplicaciones, usuarios de tooyour.</span><span class="sxs-lookup"><span data-stu-id="67737-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="67737-108">imagen personalizada Hello debe contener sólo las aplicaciones y datos confidenciales nunca que se pueden perder, como bases de datos SQL, archivos de personal o archivos de datos especiales como los archivos de la empresa de QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="67737-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="67737-109">Todos los datos confidenciales deben residir externo tooAzure RemoteApp en un servidor de archivos, otra máquina virtual de Azure, o en SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="67737-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="67737-110">imagen de Hello debe solo host Hola la aplicación que se conecta el origen de datos de toohello y muestra los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="67737-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="67737-111">Consulte [Requisitos para las imágenes Azure RemoteApp](remoteapp-imagereqs.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="67737-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="67737-112">toounderstand ¿por qué no debería almacenar datos confidenciales, debe toounderstand cómo funciona RemoteApp de Azure.</span><span class="sxs-lookup"><span data-stu-id="67737-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="67737-113">Cuando se crea o actualiza una colección, entre bastidores de hello varios clones o copias de la imagen de Hola se crean.</span><span class="sxs-lookup"><span data-stu-id="67737-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="67737-114">Estas instancias de máquina virtual son réplicas exactas de imagen personalizada de hello; Cuando los usuarios inician aplicaciones son tooone conectado de estas instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="67737-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="67737-115">Pero no se garantiza hello misma instancia y no es importante porque son no persistentes.</span><span class="sxs-lookup"><span data-stu-id="67737-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="67737-116">Hola instancias de máquina virtual aplicaciones de hospedaje hello no son persistentes y pueden ser destruido o eliminado en función, por ejemplo, durante la actualización de la colección.</span><span class="sxs-lookup"><span data-stu-id="67737-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="67737-117">Una vez que se aprovisiona la colección de Hola y los usuarios inician toohello conectar máquinas virtuales, datos de usuario están persistentes y proteger porque se guarda en un almacenamiento independiente dentro de un disco duro virtual que llamamos una [disco de perfil de usuario (UPD)](remoteapp-upd.md), que es el perfil de usuario de Hola c:\Users\<userprofile >.</span><span class="sxs-lookup"><span data-stu-id="67737-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="67737-118">Cuando se inicia una aplicación, se monta y se tratan como un perfil de usuario local por sistema operativo de Hola Hola UPD.</span><span class="sxs-lookup"><span data-stu-id="67737-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="67737-119">Obtenga más información sobre cómo [Azure RemoteApp guarda la configuración y los datos de usuario](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="67737-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="67737-120">Datos de ejemplo que no deben residir en la imagen de hello:</span><span class="sxs-lookup"><span data-stu-id="67737-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="67737-121">Datos compartidos para los usuarios tooaccess</span><span class="sxs-lookup"><span data-stu-id="67737-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="67737-122">Base de datos SQL o Base de datos QuickBooks</span><span class="sxs-lookup"><span data-stu-id="67737-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="67737-123">Todos los datos en D:\\</span><span class="sxs-lookup"><span data-stu-id="67737-123">Any data in D:\\</span></span>

<span data-ttu-id="67737-124">Datos de ejemplo que pueden residir en hello predeterminado perfil toobe se copian en UPD de todos los usuarios:</span><span class="sxs-lookup"><span data-stu-id="67737-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="67737-125">Archivos de configuración por usuario</span><span class="sxs-lookup"><span data-stu-id="67737-125">Configuration files per user</span></span>
* <span data-ttu-id="67737-126">Scripts que los usuarios tendrían que conservar en el UPD</span><span class="sxs-lookup"><span data-stu-id="67737-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="67737-127">Puntos clave:</span><span class="sxs-lookup"><span data-stu-id="67737-127">Key points:</span></span>

* <span data-ttu-id="67737-128">No almacene nunca datos confidenciales que se pueden perder en la imagen de hello al crear una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="67737-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="67737-129">Los datos confidenciales siempre deben residir en un servidor de archivos independiente, separar de la máquina virtual de Azure, en nube hello y las instancias VM externo siempre toohello hospedar sus aplicaciones en Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="67737-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="67737-130">Datos de usuario se guardan y se conserva en el disco de perfil de usuario (UDP) de Hola</span><span class="sxs-lookup"><span data-stu-id="67737-130">User data is saved and persists in hello user profile disk (UPD)</span></span>

