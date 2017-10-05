---
title: "Solución de problemas de creación de colecciones híbridas de RemoteApp | Microsoft Docs"
description: "Obtenga información sobre cómo solucionar problemas con la creación de las colecciones híbridas de RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a486dcb3f994cd78311ee86521a6792a4d57438e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="83c2d-103">Solución de problemas de creación de colecciones híbridas de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="83c2d-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="83c2d-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="83c2d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="83c2d-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="83c2d-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="83c2d-106">Una colección híbrida se hospeda en y almacena los datos en la nube de Azure, pero también permite a los usuarios acceder a datos y recursos almacenados en la red local.</span><span class="sxs-lookup"><span data-stu-id="83c2d-106">A hybrid collection is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="83c2d-107">Los usuarios pueden acceder a las aplicaciones mediante el inicio de sesión con sus credenciales corporativas sincronizadas o federadas con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83c2d-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="83c2d-108">Puede implementar una colección híbrida que use una red virtual de Azure existente o bien puede crear una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="83c2d-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="83c2d-109">Se recomienda crear o utilizar una subred de red virtual con un rango de CIDR lo suficientemente grande como para cubrir el crecimiento futuro esperado para Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="83c2d-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="83c2d-110">¿Todavía no ha creado la colección?</span><span class="sxs-lookup"><span data-stu-id="83c2d-110">Haven't created your collection yet?</span></span> <span data-ttu-id="83c2d-111">Consulte los pasos en [Creación de una colección híbrida](remoteapp-create-hybrid-deployment.md) .</span><span class="sxs-lookup"><span data-stu-id="83c2d-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for the steps.</span></span>

<span data-ttu-id="83c2d-112">Si tiene problemas al crear la colección, o si la colección no funciona del modo esperado, consulte la siguiente información.</span><span class="sxs-lookup"><span data-stu-id="83c2d-112">If you are having trouble creating your collection, or if the collection isn't working the way you think it should, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="83c2d-113">La imagen no es válida</span><span class="sxs-lookup"><span data-stu-id="83c2d-113">Your image is invalid</span></span>
<span data-ttu-id="83c2d-114">Si ve un mensaje como "GoldImageInvalid" cuando esté esperando a que Azure aprovisione la colección, la imagen de plantilla no cumple [los requisitos definidos para la imagen](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="83c2d-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="83c2d-115">Por lo tanto, consulte los [requisitos](remoteapp-imagereqs.md), corrija la imagen y pruebe a crear la colección de nuevo.</span><span class="sxs-lookup"><span data-stu-id="83c2d-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="83c2d-116">¿La red virtual tiene grupos de seguridad de red definidos?</span><span class="sxs-lookup"><span data-stu-id="83c2d-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="83c2d-117">Si ha definido grupos de seguridad de red en la subred que utiliza para la colección, asegúrese de que se puede acceder a estas [direcciones URL y puertos](remoteapp-ports.md) desde la subred.</span><span class="sxs-lookup"><span data-stu-id="83c2d-117">If you have network security groups defined on the subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="83c2d-118">Puede agregar grupos de seguridad de red adicionales a las red virtuales que implemente en la subred para disponer de un control más estricto.</span><span class="sxs-lookup"><span data-stu-id="83c2d-118">You can add additional network security groups to the VMs deployed by you in the subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="83c2d-119">¿Utiliza sus propios servidores DNS?</span><span class="sxs-lookup"><span data-stu-id="83c2d-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="83c2d-120">¿Son accesibles desde la subred de red virtual?</span><span class="sxs-lookup"><span data-stu-id="83c2d-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="83c2d-121">Tendrá que asegurarse de que los servidores DNS de la red virtual estén siempre activos y puedan resolver en todo momento las máquinas virtuales hospedadas en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="83c2d-121">You have to make sure the DNS servers in your VNET are always up and always able to resolve the virtual machines hosted in the VNET.</span></span> <span data-ttu-id="83c2d-122">No utilice Google DNS para ello.</span><span class="sxs-lookup"><span data-stu-id="83c2d-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="83c2d-123">En las colecciones híbridas utiliza sus propios servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="83c2d-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="83c2d-124">Los especifica en el esquema de configuración de red o a través del Portal de administración al crear la red virtual.</span><span class="sxs-lookup"><span data-stu-id="83c2d-124">You specify them in your network configuration schema or through the management portal when you create your virtual network.</span></span> <span data-ttu-id="83c2d-125">Los servidores DNS se utilizan en el orden en que se especifican en forma de conmutación por error (como oposición a round robin).</span><span class="sxs-lookup"><span data-stu-id="83c2d-125">DNS servers are used in the order that they are specified in a failover manner (as opposed to round robin).</span></span>  
<span data-ttu-id="83c2d-126">Consulte [Resolución de nombres para las máquinas virtuales e instancias de rol](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) para asegurarse de que los servidores DNS se han configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="83c2d-126">Please refer to [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) to make sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="83c2d-127">Asegúrese de que los servidores DNS de la colección son accesibles y están disponibles en la subred de red virtual especificada para esta colección.</span><span class="sxs-lookup"><span data-stu-id="83c2d-127">Make sure the DNS servers for your collection are accessible and available from the VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="83c2d-128">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="83c2d-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Definir el DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="83c2d-130">¿Utiliza un controlador de dominio de Active Directory en la colección?</span><span class="sxs-lookup"><span data-stu-id="83c2d-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="83c2d-131">Actualmente solo se puede asociar un dominio de Active Directory con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="83c2d-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="83c2d-132">La colección híbrida solo admite cuentas de Azure Active Directory que se hayan sincronizado con la herramienta DirSync desde una implementación de Windows Server Active Directory; en concreto, sincronizadas con la opción Sincronización de contraseña o bien con la opción de federación de Servicios de federación de Active Directory (AD FS) configurada.</span><span class="sxs-lookup"><span data-stu-id="83c2d-132">The hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with the Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="83c2d-133">Deberá crear un dominio personalizado que coincida con el sufijo UPN del dominio del dominio local para, a continuación, configurar la integración de directorio.</span><span class="sxs-lookup"><span data-stu-id="83c2d-133">You need to create a custom domain that matches the UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="83c2d-134">Consulte [Configuración de Active Directory para Azure RemoteApp](remoteapp-ad.md) para obtener información.</span><span class="sxs-lookup"><span data-stu-id="83c2d-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="83c2d-135">Asegúrese de que los detalles de dominio proporcionados son válidos y de que se puede acceder al controlador de dominio desde la máquina virtual creada en la subred que se utiliza para Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="83c2d-135">Make sure the domain details provided are valid and the domain controller is reachable from the VM created in the subnet used for Azure Remote App.</span></span> <span data-ttu-id="83c2d-136">Asegúrese también de que las credenciales de cuenta de servicio suministradas tienen permisos para agregar equipos al dominio proporcionado y de que el nombre de AD indicado se puede resolver a partir del DNS proporcionado en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="83c2d-136">Also make sure the service account credentials supplied have permissions to add computers to the provided domain and that the AD name provided can be resolved from the DNS provided in the VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="83c2d-137">¿Qué nombre de dominio especificó al crear la colección?</span><span class="sxs-lookup"><span data-stu-id="83c2d-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="83c2d-138">El nombre de dominio que creó o agregó debe ser un nombre de dominio interno (no un nombre de dominio de Azure AD) y debe utilizar el formato DNS que se puede resolver (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="83c2d-138">The domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="83c2d-139">Por ejemplo, si tiene un nombre interno de Active Directory (contoso.local) y un UPN de Active Directory (contoso.com), debe utilizar el nombre interno al crear la colección.</span><span class="sxs-lookup"><span data-stu-id="83c2d-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have to use the internal name when you create your collection.</span></span>

