---
title: "aplicaciones de Proxy de aplicación de Azure AD en los equipos de aaaAccess | Documentos de Microsoft"
description: "Utilice el Proxy de aplicación de Azure AD tooaccess la aplicación local a través de Microsoft Teams."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="d6ee7-103">Acceso a aplicaciones locales a través de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d6ee7-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="d6ee7-104">Azure Proxy de aplicación de Active Directory proporciona un único inicio de sesión tooon aplicaciones locales con independencia de dónde se encuentre y Microsoft Teams optimiza sus esfuerzos de colaboración en un solo lugar.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-104">Azure Active Directory Application Proxy gives you single sign-on tooon-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="d6ee7-105">Integración de hello dos juntos significa que los usuarios puedan ser más productivos con sus compañeros de equipo en cualquier situación.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-105">Integrating hello two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="d6ee7-106">Los usuarios pueden agregar canales de los equipos de nube aplicaciones tootheir [con pestañas](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), pero ¿qué ocurre si ese sitio de SharePoint o la herramienta de planeación todas utilizan está hospedado en local?</span><span class="sxs-lookup"><span data-stu-id="d6ee7-106">Your users can add cloud apps tootheir Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="d6ee7-107">Proxy de aplicación es la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-107">Application Proxy is hello solution.</span></span> <span data-ttu-id="d6ee7-108">Puede agregar las aplicaciones publicadas a través de Proxy de aplicación tootheir canales con Hola mismo direcciones URL externas siempre usan tooaccess sus aplicaciones de forma remota.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-108">They can add apps published through Application Proxy tootheir channels using hello same external URLs they always use tooaccess their apps remotely.</span></span> <span data-ttu-id="d6ee7-109">Y como Proxy de aplicación autentica a través de Azure Active Directory, Hola misma experiencia de inicio de sesión único lleva a través de.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-109">And because Application Proxy authenticates through Azure Active Directory, hello same single sign-on experience carries through.</span></span>


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="d6ee7-110">Instalar el conector del Proxy de aplicación de Hola y publicar la aplicación</span><span class="sxs-lookup"><span data-stu-id="d6ee7-110">Install hello Application Proxy connector and publish your app</span></span>

<span data-ttu-id="d6ee7-111">Si no lo ha hecho ya, [configurar el Proxy de aplicación para el inquilino e instalar el conector de hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="d6ee7-111">If you haven't already, [configure Application Proxy for your tenant and install hello connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="d6ee7-112">A continuación, [publique la aplicación local](application-proxy-publish-azure-portal.md) para acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="d6ee7-113">Cuando publica la aplicación hello, tome nota de la dirección URL externa de hello porque los usuarios finales necesitan esa información cuando se agregan tooTeams de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-113">When you're publishing hello app, make note of hello external URL because your end users need that information when they add hello app tooTeams.</span></span>

<span data-ttu-id="d6ee7-114">Si ya tiene sus aplicaciones publicadas pero no recuerda sus direcciones URL externas, buscarlos en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6ee7-114">If you already have your apps published but don't remember their external URLs, look them up in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d6ee7-115">Inicie sesión en, a continuación, desplácese demasiado**Azure Active Directory** > **aplicaciones empresariales** > **todas las aplicaciones** > Seleccionar la aplicación > **Proxy de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-115">Sign in, then navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-tooteams"></a><span data-ttu-id="d6ee7-116">Agregar la aplicación tooTeams</span><span class="sxs-lookup"><span data-stu-id="d6ee7-116">Add your app tooTeams</span></span>

<span data-ttu-id="d6ee7-117">Una vez que publica la aplicación hello a través de Proxy de aplicación, que los usuarios sepan que puede agregar como una pestaña directamente en sus canales de los equipos.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-117">Once you publish hello app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="d6ee7-118">Haga que sigan estos tres pasos:</span><span class="sxs-lookup"><span data-stu-id="d6ee7-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="d6ee7-119">Navegue toohello los equipos de canal en el que desea tooadd esta aplicación y seleccionen  **+**  tooadd una pestaña.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-119">Navigate toohello Teams channel where you want tooadd this app and select **+** tooadd a tab.</span></span>

   ![Seleccione Agregar una pestaña](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="d6ee7-121">Seleccione **sitio Web** de opciones de la pestaña de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-121">Select **Website** from hello tab options.</span></span>

   ![Incorporación de un sitio web](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="d6ee7-123">Asigne un nombre de pestaña de Hola y establecer la dirección externa del Proxy de aplicación Hola URL toohello.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-123">Give hello tab a name and set hello URL toohello Application Proxy external URL.</span></span> 

   ![Configuración de la dirección URL y el nombre de la pestaña](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="d6ee7-125">Una vez que un miembro de un equipo agrega pestaña hello, muestra para todos los usuarios en el canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-125">Once one member of a team adds hello tab, it shows up for everyone in hello channel.</span></span> <span data-ttu-id="d6ee7-126">Los usuarios que dispongan de acceso toohello aplicación obtendrán acceso de inicio de sesión único con credenciales de Hola que usan para Teams de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-126">Any users who have access toohello app get single sign-on access with hello credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="d6ee7-127">Los usuarios que no dispongan de acceso toohello aplicación verán la pestaña de hello en los equipos, pero se bloquean hasta que otorgarles permisos toohello local aplicación y hello Azure versión publicada del portal de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-127">Any users who don't have access toohello app will see hello tab in Teams, but are blocked until you give them permissions toohello on-premises app and hello Azure portal published version of hello app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d6ee7-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6ee7-128">Next steps</span></span>

- <span data-ttu-id="d6ee7-129">Obtenga información acerca de cómo demasiado[publicar sitios de SharePoint locales](application-proxy-enable-remote-access-sharepoint.md) con Proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-129">Learn how too[publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="d6ee7-130">Configurar la toouse aplicaciones [dominios personalizados](active-directory-application-proxy-custom-domains.md) para su dirección URL externa.</span><span class="sxs-lookup"><span data-stu-id="d6ee7-130">Configure your apps toouse [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
