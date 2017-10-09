---
title: aaaAzure AD + requisitos de Active Directory de Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset una toowork de Active Directory con Azure RemoteApp."
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
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="3b3c0-103">Requisitos de Azure AD + Active Directory para Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3b3c0-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3b3c0-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3b3c0-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3b3c0-106">Para la colección de híbrida de RemoteApp de Azure o para una colección en la nube que desea que toofederate mediante AD Connect, necesita toodo Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want toofederate using AD Connect, you need toodo hello following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="3b3c0-107">Conexión de Azure AD y Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b3c0-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="3b3c0-108">Si desea tooconnect inquilino de Azure AD y los entornos de Active Directory local, use AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-108">If you want tooconnect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="3b3c0-109">Éste lo guiará solo [4 clics](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect Hola dos directorios.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello two directories.</span></span>

<span data-ttu-id="3b3c0-110">Nota: la sincronización de directorios se requiere para las colecciones híbridas.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="3b3c0-111">Asegúrese de que "@domain.com" coincide.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="3b3c0-112">Antes de comenzar, asegúrese de que ese hello UPN para el sufijo de Hola de coincidencias de bosque local de su dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-112">Before you get started, make sure that hello UPN for your on-premises forest matches hello suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="3b3c0-113">Después de configurar el sufijo de dominio UPN de hello en Azure AD, todos los usuarios iniciar sesión en Azure RemoteApp iniciará la sesión como "usuario @<hello suffix you set up>."</span><span class="sxs-lookup"><span data-stu-id="3b3c0-113">After you set up hello UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<hello suffix you set up>."</span></span> <span data-ttu-id="3b3c0-114">Asegúrese de que los usuarios también pueden registrar con hello mismo user@suffix en el dominio local de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-114">Make sure that users can also log in with hello same user@suffix into hello on-premises domain.</span></span> <span data-ttu-id="3b3c0-115">En ciertos casos, puede configurar el nombre de un dominio en Azure AD al especificar un sufijo de dominio diferente para hello usuario localmente.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for hello user on-prem.</span></span> <span data-ttu-id="3b3c0-116">En este caso, los usuarios no ser capaz de tooconnect tooany Unidos al dominio equipos o los recursos a través de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-116">In this case, your users won't be able tooconnect tooany domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="3b3c0-117">Por ejemplo, si configura el sufijo de dominio UPN en AAD como contoso.com, pero algunos usuarios locales y Active Directory son toolog configurado con @contoso.uk, los usuarios no será capaz de toocorrectly registro en hello colección ARA.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured toolog in with @contoso.uk, then those users will not be able toocorrectly log into hello ARA collection.</span></span> <span data-ttu-id="3b3c0-118">Los usuarios que debe ser UPN en AAD y AD Hola mismo posibles de toobe de inicio de sesión de hello"</span><span class="sxs-lookup"><span data-stu-id="3b3c0-118">Users UPN in AAD and AD must be hello same for hello login toobe possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="3b3c0-119">Creación de objetos para Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3b3c0-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="3b3c0-120">También necesita hello toocreate siguientes objetos de Active Directory local:</span><span class="sxs-lookup"><span data-stu-id="3b3c0-120">You also need toocreate hello following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="3b3c0-121">Una cuenta de servicio tooprovide acceso toodomain recursos para los programas de RemoteApp al unirse a dominio RDSH puntos finales toohello local.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-121">A service account tooprovide access toodomain resources for RemoteApp programs by joining RDSH end points toohello on-premises domain.</span></span>
* <span data-ttu-id="3b3c0-122">Una unidad organizativa (UO) toocontain RemoteApp máquina los objetos.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-122">An Organizational Unit (OU) toocontain RemoteApp machine objects.</span></span> <span data-ttu-id="3b3c0-123">Uso de hello OU es cuentas de hello tooisolate recomendada (aunque no necesario) y las directivas que se va a utilizar con RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-123">Use of hello OU is recommended (but not required) tooisolate hello accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="3b3c0-124">Necesita ambos de estos objetos cuando se crea la colección de RemoteApp, por lo que debe toodo seguro de estos pasos en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="3b3c0-124">You need both of these objects when you create your RemoteApp collection, so be sure toodo these steps first.</span></span>

