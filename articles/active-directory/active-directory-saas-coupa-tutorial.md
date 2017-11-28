---
title: "Tutorial: Integración de Azure Active Directory con Coupa | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Coupa con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="34230-103">Tutorial: Integración de Azure Active Directory con Coupa</span><span class="sxs-lookup"><span data-stu-id="34230-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="34230-104">objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Coupa.</span><span class="sxs-lookup"><span data-stu-id="34230-104">hello objective of this tutorial is tooshow hello integration of Azure and Coupa.</span></span>  
<span data-ttu-id="34230-105">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="34230-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="34230-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="34230-106">A valid Azure subscription</span></span>
* <span data-ttu-id="34230-107">Una suscripción habilitada para el inicio de sesión único (SSO) en Coupa</span><span class="sxs-lookup"><span data-stu-id="34230-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="34230-108">Después de completar este tutorial, los usuarios de hello Azure AD que haya asignado tooCoupa será capaz de toosingle inicio de sesión en la aplicación hello mediante hello [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="34230-108">After completing this tutorial, hello Azure AD users you have assigned tooCoupa will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="34230-109">escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="34230-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="34230-110">Habilitar la integración de aplicación Hola para Coupa</span><span class="sxs-lookup"><span data-stu-id="34230-110">Enabling hello application integration for Coupa</span></span>
* <span data-ttu-id="34230-111">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="34230-111">Configuring single sign-on</span></span>
* <span data-ttu-id="34230-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="34230-112">Configuring user provisioning</span></span>
* <span data-ttu-id="34230-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="34230-113">Assigning users</span></span>

<span data-ttu-id="34230-114">![Escenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="34230-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-coupa"></a><span data-ttu-id="34230-115">Habilitar la integración de aplicación Hola para Coupa</span><span class="sxs-lookup"><span data-stu-id="34230-115">Enable hello application integration for Coupa</span></span>
<span data-ttu-id="34230-116">objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Coupa.</span><span class="sxs-lookup"><span data-stu-id="34230-116">hello objective of this section is toooutline how tooenable hello application integration for Coupa.</span></span>

<span data-ttu-id="34230-117">**integración de aplicaciones de hello tooenable para Coupa, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34230-117">**tooenable hello application integration for Coupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="34230-118">Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="34230-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="34230-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="34230-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="34230-120">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="34230-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="34230-121">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="34230-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="34230-122">![Aplicaciones](./media/active-directory-saas-coupa-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="34230-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="34230-123">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="34230-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="34230-124">![Agregar aplicaciones](./media/active-directory-saas-coupa-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="34230-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="34230-125">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="34230-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="34230-126">![Agregar una aplicación de la galería](./media/active-directory-saas-coupa-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="34230-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="34230-127">Hola **cuadro de búsqueda**, tipo **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="34230-127">In hello **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="34230-128">![Galería de aplicaciones](./media/active-directory-saas-coupa-tutorial/IC791898.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="34230-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="34230-129">En el panel de resultados de hello, seleccione **Coupa**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="34230-129">In hello results pane, select **Coupa**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="34230-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="34230-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="34230-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="34230-131">Configure single sign-on</span></span>

<span data-ttu-id="34230-132">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooCoupa con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="34230-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCoupa with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="34230-133">Configurar el inicio de sesión único para Coupa necesario tooretrieve un valor de huella digital de un certificado.</span><span class="sxs-lookup"><span data-stu-id="34230-133">Configuring single sign-on for Coupa requires you tooretrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="34230-134">Si no está familiarizado con este procedimiento, consulte [cómo tooretrieve valor de huella digital del certificado](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="34230-134">If you are not familiar with this procedure, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="34230-135">**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34230-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="34230-136">Inicie sesión en tooyour sitio de Coupa como administrador.</span><span class="sxs-lookup"><span data-stu-id="34230-136">Sign on tooyour Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="34230-137">Vaya demasiado**el programa de instalación \> Control de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="34230-137">Go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="34230-138">![Controles de seguridad](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de seguridad")</span><span class="sxs-lookup"><span data-stu-id="34230-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="34230-139">toodownload hello Coupa metadatos archivo tooyour equipo, haga clic en **descargar e importar metadatos de SP**.</span><span class="sxs-lookup"><span data-stu-id="34230-139">toodownload hello Coupa metadata file tooyour computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="34230-140">![Metadatos SP de Coupa](./media/active-directory-saas-coupa-tutorial/IC791901.png "Metadatos SP de Coupa")</span><span class="sxs-lookup"><span data-stu-id="34230-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="34230-141">En otra ventana del explorador, inicie sesión en toohello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="34230-141">In a different browser window, sign on toohello Azure classic portal.</span></span>
5. <span data-ttu-id="34230-142">En hello **Coupa** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34230-142">On hello **Coupa** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="34230-143">![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="34230-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="34230-144">En hello **¿cómo desea que los usuarios toosign en tooCoupa** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="34230-144">On hello **How would you like users toosign on tooCoupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="34230-145">![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="34230-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="34230-146">En hello **configurar URL de aplicación** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="34230-146">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="34230-147">![Configurar dirección URL de la aplicación](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="34230-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="34230-148">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL utilizada por su toosign a los usuarios en la aplicación de Coupa tooyour (p. ej.: "*http://company.Coupa.com*").</span><span class="sxs-lookup"><span data-stu-id="34230-148">In hello **Sign On URL** textbox, type URL used by your users toosign on tooyour Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="34230-149">Abra el archivo de metadatos de Coupa descargado y, a continuación, copie hello **AssertionConsumerService índice/URL**.</span><span class="sxs-lookup"><span data-stu-id="34230-149">Open your downloaded Coupa metadata file, and then copy hello **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="34230-150">Hola **Coupa Reply URL** cuadro de texto, pegue hello **AssertionConsumerService índice/URL** valor.</span><span class="sxs-lookup"><span data-stu-id="34230-150">In hello **Coupa Reply URL** textbox, paste hello **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="34230-151">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="34230-151">Click **Next**.</span></span>
8. <span data-ttu-id="34230-152">En hello **configurar inicio de sesión único en Coupa** page, toodownload el archivo de metadatos, haga clic en **descargar metadatos**y, a continuación, guardar archivo hello localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="34230-152">On hello **Configure single sign-on at Coupa** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
   
   <span data-ttu-id="34230-153">![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="34230-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="34230-154">En el sitio de Coupa hello, vaya demasiado**el programa de instalación \> Control de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="34230-154">On hello Coupa company site, go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="34230-155">![Controles de seguridad](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de seguridad")</span><span class="sxs-lookup"><span data-stu-id="34230-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="34230-156">Hola **inicie sesión con credenciales de Coupa** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="34230-156">In hello **Log in using Coupa credentials** section, perform hello following steps:</span></span>  

   <span data-ttu-id="34230-157">![Inicio de sesión con credenciales de Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Inicio de sesión con credenciales de Coupa")</span><span class="sxs-lookup"><span data-stu-id="34230-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="34230-158">Seleccione **Iniciar sesión con SAML**.</span><span class="sxs-lookup"><span data-stu-id="34230-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="34230-159">Haga clic en **examinar** tooupload el archivo de metadatos de Azure Active descargado.</span><span class="sxs-lookup"><span data-stu-id="34230-159">Click **Browse** tooupload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="34230-160">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="34230-160">Click **Save**.</span></span>
11. <span data-ttu-id="34230-161">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34230-161">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="34230-162">![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="34230-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="34230-163">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="34230-163">Configure user provisioning</span></span>

<span data-ttu-id="34230-164">En orden tooenable toolog de los usuarios de Azure AD en Coupa, se les deben aprovisionar en Coupa.</span><span class="sxs-lookup"><span data-stu-id="34230-164">In order tooenable Azure AD users toolog into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="34230-165">En caso de hello de Coupa, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="34230-165">In hello case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="34230-166">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34230-166">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="34230-167">Inicie sesión en tooyour **Coupa** como administrador.</span><span class="sxs-lookup"><span data-stu-id="34230-167">Log in tooyour **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="34230-168">En el menú de hello en la parte superior de hello, haga clic en **el programa de instalación**y, a continuación, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="34230-168">In hello menu on hello top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="34230-169">![Usuarios](./media/active-directory-saas-coupa-tutorial/IC791908.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="34230-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="34230-170">Haga clic en **Create**(Crear).</span><span class="sxs-lookup"><span data-stu-id="34230-170">Click **Create**.</span></span>
   
   <span data-ttu-id="34230-171">![Creación de usuarios](./media/active-directory-saas-coupa-tutorial/IC791909.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="34230-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="34230-172">Hola **crear usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="34230-172">In hello **User Create** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="34230-173">![Detalles del usuario](./media/active-directory-saas-coupa-tutorial/IC791910.png "Detalles del usuario")</span><span class="sxs-lookup"><span data-stu-id="34230-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="34230-174">Hola de tipo **inicio de sesión**, **nombre**, **Last Name**, **Id. de inicio de sesión único**, **correo electrónico** atributos de un cuenta válida de Azure Active Directory que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="34230-174">Type hello **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="34230-175">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="34230-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="34230-176">titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="34230-176">hello Azure Active Directory account holder will get an email with a link tooconfirm hello account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="34230-177">Puede usar cualquier otra Coupa usuario cuenta herramienta de creación o las API proporcionadas por Coupa tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="34230-177">You can use any other Coupa user account creation tools or APIs provided by Coupa tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="34230-178">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="34230-178">Assign users</span></span>
<span data-ttu-id="34230-179">tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.</span><span class="sxs-lookup"><span data-stu-id="34230-179">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="34230-180">**tooassign tooCoupa de los usuarios, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34230-180">**tooassign users tooCoupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="34230-181">Hola portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="34230-181">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="34230-182">En Hola ** Coupa ** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="34230-182">On hello **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="34230-183">![Asignar usuarios](./media/active-directory-saas-coupa-tutorial/IC791911.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="34230-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="34230-184">Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.</span><span class="sxs-lookup"><span data-stu-id="34230-184">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="34230-185">![Sí](./media/active-directory-saas-coupa-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="34230-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="34230-186">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="34230-186">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="34230-187">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="34230-187">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

