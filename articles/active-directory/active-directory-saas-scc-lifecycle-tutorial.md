---
title: "Tutorial: Integración de Azure Active Directory con SCC LifeCycle | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse SCC LifeCycle con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="941c9-103">Tutorial: Integración de Azure Active Directory con SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="941c9-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="941c9-104">objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="941c9-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="941c9-105">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="941c9-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="941c9-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="941c9-106">A valid Azure subscription</span></span>
* <span data-ttu-id="941c9-107">Una suscripción habilitada para el inicio de sesión único (SSO) en SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="941c9-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="941c9-108">Después de completar este tutorial, Hola usuarios de Azure AD que haya asignado será el ciclo de vida de tooSCC toosingle capaz de inicio de sesión en la aplicación hello en el sitio de SCC LifeCycle (servicio iniciado por el proveedor inicio de sesión), o mediante hello [Introducción Panel de acceso de toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="941c9-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="941c9-109">escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="941c9-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="941c9-110">Habilitar la integración de aplicación Hola para SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="941c9-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="941c9-111">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="941c9-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="941c9-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="941c9-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="941c9-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="941c9-113">Assigning users</span></span>

<span data-ttu-id="941c9-114">![Escenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="941c9-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="941c9-115">Habilitar la integración de aplicación Hola para SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="941c9-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="941c9-116">objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="941c9-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="941c9-117">**integración de aplicaciones de hello tooenable para SCC LifeCycle, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="941c9-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="941c9-118">Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="941c9-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="941c9-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="941c9-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="941c9-120">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="941c9-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="941c9-121">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="941c9-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="941c9-122">![Aplicaciones](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="941c9-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="941c9-123">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="941c9-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="941c9-124">![Agregar aplicaciones](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="941c9-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="941c9-125">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="941c9-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="941c9-126">![Agregar una aplicación de la galería](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="941c9-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="941c9-127">Hola **cuadro de búsqueda**, tipo **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="941c9-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="941c9-128">![Galería de aplicaciones](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="941c9-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="941c9-129">En el panel de resultados de hello, seleccione **SCC LifeCycle**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="941c9-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="941c9-130">![Ciclo de vida de SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "Ciclo de vida de SCC")</span><span class="sxs-lookup"><span data-stu-id="941c9-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="941c9-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="941c9-131">Configure single sign-on</span></span>

<span data-ttu-id="941c9-132">objetivo de Hola de esta sección es toooutline cómo tooauthenticate tooSCC del ciclo de vida de tooenable a los usuarios con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="941c9-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="941c9-133">**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="941c9-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="941c9-134">En el portal de Azure clásico en Hola Hola **SCC LifeCycle** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen Hola ** configurar inicio de sesión único ** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="941c9-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="941c9-135">![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="941c9-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="941c9-136">En hello **¿cómo desea que los usuarios toosign en tooSCC ciclo de vida de** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="941c9-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="941c9-137">![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="941c9-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="941c9-138">En hello **configurar URL de aplicación** página Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL Hola utilizado por su toosign a los usuarios en tooyour aplicación de SCC LifeCycle mediante Hola sigue el patrón "*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*"y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="941c9-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="941c9-139">![Configurar dirección URL de la aplicación](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="941c9-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="941c9-140">En hello **configurar inicio de sesión único en SCC LifeCycle** página, haga clic en **descargar metadatos**y, a continuación, guarde el archivo de metadatos localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="941c9-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="941c9-141">![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="941c9-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="941c9-142">Reenviar ese tooSCC del archivo de metadatos equipo de soporte técnico de ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="941c9-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="941c9-143">Inicio de sesión único tiene toobe habilitada por Hola, equipo de soporte técnico de SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="941c9-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="941c9-144">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="941c9-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="941c9-145">![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="941c9-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="941c9-146">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="941c9-146">Configure user provisioning</span></span>

<span data-ttu-id="941c9-147">En orden tooenable toolog de los usuarios de Azure AD en SCC LifeCycle, se les deben aprovisionar en SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="941c9-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="941c9-148">No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooSCC del ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="941c9-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="941c9-149">Cuando un toolog de intentos de usuario asignado en SCC LifeCycle, automáticamente se crea una cuenta de SCC LifeCycle si es necesario.</span><span class="sxs-lookup"><span data-stu-id="941c9-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="941c9-150">Puede usar cualquier otra SCC LifeCycle usuario cuenta herramienta de creación o las API proporcionadas por tooprovision de SCC LifeCycle cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="941c9-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="941c9-151">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="941c9-151">Assign users</span></span>
<span data-ttu-id="941c9-152">tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.</span><span class="sxs-lookup"><span data-stu-id="941c9-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="941c9-153">**tooassign usuarios tooSCC ciclo de vida, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="941c9-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="941c9-154">Hola portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="941c9-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="941c9-155">En Hola ** SCC LifeCycle ** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="941c9-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="941c9-156">![Asignar usuarios](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="941c9-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="941c9-157">Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.</span><span class="sxs-lookup"><span data-stu-id="941c9-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="941c9-158">![Sí](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="941c9-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="941c9-159">Si desea tootest la configuración de SSO, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="941c9-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="941c9-160">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="941c9-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

