---
title: Requisitos de Azure AD + Active Directory para Azure RemoteApp | Microsoft Docs
description: Aprenda a configurar Active Directory para trabajar con RemoteApp de Azure.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="0bcff-103">Requisitos de Azure AD + Active Directory para Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0bcff-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0bcff-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="0bcff-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0bcff-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="0bcff-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0bcff-106">En el caso de la colección de híbrida de Azure RemoteApp o de una colección en la nube que desee federar mediante AD Connect, deberá hacer lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="0bcff-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="0bcff-107">Conexión de Azure AD y Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bcff-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="0bcff-108">Si desea conectar el inquilino de Azure AD y los entornos de Active Directory locales, utilice AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0bcff-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="0bcff-109">En tan solo [4 clics](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) habrá conectado los dos directorios.</span><span class="sxs-lookup"><span data-stu-id="0bcff-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span></span>

<span data-ttu-id="0bcff-110">Nota: la sincronización de directorios se requiere para las colecciones híbridas.</span><span class="sxs-lookup"><span data-stu-id="0bcff-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="0bcff-111">Asegúrese de que "@domain.com" coincide.</span><span class="sxs-lookup"><span data-stu-id="0bcff-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="0bcff-112">Antes de empezar, asegúrese de que el UPN del bosque local coincide con el sufijo de su dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bcff-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="0bcff-113">Una vez configurado el sufijo del dominio UPN en Azure AD, todos los usuarios que inicien sesión en Azure RemoteApp lo harán como "usuario@<the suffix you set up>".</span><span class="sxs-lookup"><span data-stu-id="0bcff-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span></span> <span data-ttu-id="0bcff-114">Asegúrese de que los usuarios también pueden iniciar con el mismo user@suffix en el dominio local.</span><span class="sxs-lookup"><span data-stu-id="0bcff-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span></span> <span data-ttu-id="0bcff-115">En ciertos casos, puede configurar un nombre de dominio en Azure AD al especificar un sufijo de dominio diferente para el usuario local.</span><span class="sxs-lookup"><span data-stu-id="0bcff-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span></span> <span data-ttu-id="0bcff-116">En este caso, los usuarios no podrán conectarse a los equipos o recursos unidos mediante dominio a través de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0bcff-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="0bcff-117">Por ejemplo, si configura el sufijo de dominio UPN en AAD como contoso.com, pero algunos usuarios locales y de Active Directory están configurados para iniciar sesión con @contoso.uk, esos usuarios no podrán iniciar sesión correctamente en la colección ARA.</span><span class="sxs-lookup"><span data-stu-id="0bcff-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span></span> <span data-ttu-id="0bcff-118">El UPN de los usuarios en AAD y AD deben ser el mismo para que el inicio de sesión sea posible.</span><span class="sxs-lookup"><span data-stu-id="0bcff-118">Users UPN in AAD and AD must be the same for the login to be possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="0bcff-119">Creación de objetos para Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0bcff-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="0bcff-120">También debe crear los siguientes objetos de Active Directory locales:</span><span class="sxs-lookup"><span data-stu-id="0bcff-120">You also need to create the following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="0bcff-121">Una cuenta de servicio para proporcionar acceso a los recursos del dominio para los programas de RemoteApp mediante la combinación de extremos RDSH al dominio local.</span><span class="sxs-lookup"><span data-stu-id="0bcff-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span></span>
* <span data-ttu-id="0bcff-122">Una unidad organizativa (OU) que contenga objetos de equipo de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0bcff-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span></span> <span data-ttu-id="0bcff-123">Se recomienda usar la unidad organizativa (aunque no es necesario) para aislar las cuentas y las directivas que se van a utilizar con RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0bcff-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="0bcff-124">Se necesitan estos dos objetos cuando se crea la colección de RemoteApp, por lo que debe asegurarse de realizar estos pasos en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="0bcff-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span></span>

