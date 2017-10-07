---
title: "aaaTroubleshoot crear colecciones de RemoteApp híbrida | Documentos de Microsoft"
description: "Obtenga información acerca de cómo errores de creación de colección de tootroubleshoot RemoteApp híbrida"
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
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="67fa2-103">Solución de problemas de creación de colecciones híbridas de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="67fa2-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="67fa2-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="67fa2-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="67fa2-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="67fa2-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="67fa2-106">Una colección híbrida se hospeda en y almacena los datos en la nube de Azure Hola pero también permite a los usuarios obtener acceso a datos y recursos almacenados en la red local.</span><span class="sxs-lookup"><span data-stu-id="67fa2-106">A hybrid collection is hosted in and stores data in hello Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="67fa2-107">Los usuarios pueden acceder a las aplicaciones mediante el inicio de sesión con sus credenciales corporativas sincronizadas o federadas con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="67fa2-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="67fa2-108">Puede implementar una colección híbrida que use una red virtual de Azure existente o bien puede crear una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="67fa2-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="67fa2-109">Se recomienda crear o utilizar una subred de red virtual con un rango de CIDR lo suficientemente grande como para cubrir el crecimiento futuro esperado para Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="67fa2-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="67fa2-110">¿Todavía no ha creado la colección?</span><span class="sxs-lookup"><span data-stu-id="67fa2-110">Haven't created your collection yet?</span></span> <span data-ttu-id="67fa2-111">Vea [crear una colección híbrida](remoteapp-create-hybrid-deployment.md) para conocer los pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="67fa2-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for hello steps.</span></span>

<span data-ttu-id="67fa2-112">Si tiene problemas para crear la colección, o si no funciona la colección de hello forma Hola piensa que debería, desproteger Hola siguiente información.</span><span class="sxs-lookup"><span data-stu-id="67fa2-112">If you are having trouble creating your collection, or if hello collection isn't working hello way you think it should, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="67fa2-113">La imagen no es válida</span><span class="sxs-lookup"><span data-stu-id="67fa2-113">Your image is invalid</span></span>
<span data-ttu-id="67fa2-114">Si ve un mensaje como "GoldImageInvalid" cuando se está esperando tooprovision Azure la colección, significa que la imagen de plantilla no cumple con hello [define los requisitos de la imagen](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="67fa2-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="67fa2-115">Por lo tanto, vaya a leerlos [requisitos](remoteapp-imagereqs.md), corrija la imagen e inténtelo de toocreate volver a la colección.</span><span class="sxs-lookup"><span data-stu-id="67fa2-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="67fa2-116">¿La red virtual tiene grupos de seguridad de red definidos?</span><span class="sxs-lookup"><span data-stu-id="67fa2-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="67fa2-117">Si tiene definidos en la subred de Hola se usan para la colección de grupos de seguridad de red, asegúrese de que estos [puertos y direcciones URL](remoteapp-ports.md) son accesibles desde dentro de la subred.</span><span class="sxs-lookup"><span data-stu-id="67fa2-117">If you have network security groups defined on hello subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="67fa2-118">Puede agregar otra red seguridad grupos toohello máquinas virtuales implementadas por el usuario en la subred de Hola para un control más estricto.</span><span class="sxs-lookup"><span data-stu-id="67fa2-118">You can add additional network security groups toohello VMs deployed by you in hello subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="67fa2-119">¿Utiliza sus propios servidores DNS?</span><span class="sxs-lookup"><span data-stu-id="67fa2-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="67fa2-120">¿Son accesibles desde la subred de red virtual?</span><span class="sxs-lookup"><span data-stu-id="67fa2-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="67fa2-121">Tiene toomake Hola seguro de los servidores DNS en la red virtual siempre están funcionando y máquinas virtuales siempre pueda tooresolve Hola que hospedados en hello red virtual.</span><span class="sxs-lookup"><span data-stu-id="67fa2-121">You have toomake sure hello DNS servers in your VNET are always up and always able tooresolve hello virtual machines hosted in hello VNET.</span></span> <span data-ttu-id="67fa2-122">No utilice Google DNS para ello.</span><span class="sxs-lookup"><span data-stu-id="67fa2-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="67fa2-123">En las colecciones híbridas utiliza sus propios servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="67fa2-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="67fa2-124">Especifica estos recursos en el esquema de configuración de red o a través del portal de administración de hello cuando se crea la red virtual.</span><span class="sxs-lookup"><span data-stu-id="67fa2-124">You specify them in your network configuration schema or through hello management portal when you create your virtual network.</span></span> <span data-ttu-id="67fa2-125">Se usan servidores DNS en orden de Hola que se especifican en forma de conmutación por error (como tooround opuestos Round robin).</span><span class="sxs-lookup"><span data-stu-id="67fa2-125">DNS servers are used in hello order that they are specified in a failover manner (as opposed tooround robin).</span></span>  
<span data-ttu-id="67fa2-126">Consulte demasiado[resolución de nombres para las máquinas virtuales e instancias de rol](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake que los servidores DNS estén configurado correcly.</span><span class="sxs-lookup"><span data-stu-id="67fa2-126">Please refer too[Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="67fa2-127">Asegúrese de que los servidores DNS de hello de la colección están accesibles y está disponible en la subred de red virtual de hello especificado para esta colección.</span><span class="sxs-lookup"><span data-stu-id="67fa2-127">Make sure hello DNS servers for your collection are accessible and available from hello VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="67fa2-128">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="67fa2-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Definir el DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="67fa2-130">¿Utiliza un controlador de dominio de Active Directory en la colección?</span><span class="sxs-lookup"><span data-stu-id="67fa2-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="67fa2-131">Actualmente solo se puede asociar un dominio de Active Directory con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="67fa2-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="67fa2-132">colección de Hello híbrida admite solo las cuentas de Azure Active Directory que se han sincronizado con la herramienta de sincronización de directorios de una implementación de Windows Server Active Directory; en concreto, o bien se sincronizan con la opción de sincronización de contraseña de Hola o sincronizados con la federación de servicios de federación de Active Directory (AD FS) configurada.</span><span class="sxs-lookup"><span data-stu-id="67fa2-132">hello hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with hello Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="67fa2-133">Es necesario toocreate un dominio personalizado que coincide con el sufijo de dominio UPN de hello para el dominio local y configurar la integración de directorio.</span><span class="sxs-lookup"><span data-stu-id="67fa2-133">You need toocreate a custom domain that matches hello UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="67fa2-134">Consulte [Configuración de Active Directory para Azure RemoteApp](remoteapp-ad.md) para obtener información.</span><span class="sxs-lookup"><span data-stu-id="67fa2-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="67fa2-135">Asegúrese de que detalles del dominio Hola proporcionadas son válidas y controlador de dominio de hello sea accesible desde Hola que VM creada en la subred de hello usada para la aplicación de Azure remota.</span><span class="sxs-lookup"><span data-stu-id="67fa2-135">Make sure hello domain details provided are valid and hello domain controller is reachable from hello VM created in hello subnet used for Azure Remote App.</span></span> <span data-ttu-id="67fa2-136">Compruebe también que la cuenta de servicio de hello las credenciales proporcionadas tienen permisos tooadd equipos toohello proporcionado por el dominio y que Hola nombre AD siempre se puede resolver de hello DNS proporcionado en hello red virtual.</span><span class="sxs-lookup"><span data-stu-id="67fa2-136">Also make sure hello service account credentials supplied have permissions tooadd computers toohello provided domain and that hello AD name provided can be resolved from hello DNS provided in hello VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="67fa2-137">¿Qué nombre de dominio especificó al crear la colección?</span><span class="sxs-lookup"><span data-stu-id="67fa2-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="67fa2-138">nombre de dominio de Hello creen o agreguen debe ser un nombre de dominio interno (no el nombre de dominio de Azure AD) y debe estar en un formato DNS (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="67fa2-138">hello domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="67fa2-139">Por ejemplo, tiene un nombre interno de Active Directory (contoso.local) y un UPN de Active Directory (contoso.com) - tiene el nombre interno de hello toouse cuando se crea la colección.</span><span class="sxs-lookup"><span data-stu-id="67fa2-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have toouse hello internal name when you create your collection.</span></span>

