---
title: "Tutorial: Integración de Azure Active Directory con Coupa | Microsoft Docs"
description: "Aprenda a usar Coupa con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
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
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="28ac5-103">Tutorial: Integración de Azure Active Directory con Coupa</span><span class="sxs-lookup"><span data-stu-id="28ac5-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="28ac5-104">El objetivo de este tutorial es mostrar la integración de Azure y Coupa.</span><span class="sxs-lookup"><span data-stu-id="28ac5-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="28ac5-105">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="28ac5-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="28ac5-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="28ac5-106">A valid Azure subscription</span></span>
* <span data-ttu-id="28ac5-107">Una suscripción habilitada para el inicio de sesión único (SSO) en Coupa</span><span class="sxs-lookup"><span data-stu-id="28ac5-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="28ac5-108">Después de completar este tutorial, los usuarios de Azure AD que ha asignado a Coupa podrá realizar un inicio de sesión único en la aplicación con la [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="28ac5-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="28ac5-109">La situación descrita en este tutorial consta de los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="28ac5-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="28ac5-110">Habilitación de la integración de aplicaciones para Coupa</span><span class="sxs-lookup"><span data-stu-id="28ac5-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="28ac5-111">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="28ac5-111">Configuring single sign-on</span></span>
* <span data-ttu-id="28ac5-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="28ac5-112">Configuring user provisioning</span></span>
* <span data-ttu-id="28ac5-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="28ac5-113">Assigning users</span></span>

<span data-ttu-id="28ac5-114">![Escenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="28ac5-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="28ac5-115">Habilitación de la integración de aplicaciones para Coupa</span><span class="sxs-lookup"><span data-stu-id="28ac5-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="28ac5-116">El objetivo de esta sección es describir cómo se habilita la integración de las aplicaciones para Coupa.</span><span class="sxs-lookup"><span data-stu-id="28ac5-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="28ac5-117">**Siga estos pasos para habilitar la integración de aplicaciones para Coupa:**</span><span class="sxs-lookup"><span data-stu-id="28ac5-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="28ac5-118">En el panel de navegación izquierdo del Portal de Azure clásico, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="28ac5-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="28ac5-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="28ac5-120">En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="28ac5-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="28ac5-121">Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="28ac5-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="28ac5-122">![Aplicaciones](./media/active-directory-saas-coupa-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="28ac5-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="28ac5-123">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="28ac5-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="28ac5-124">![Agregar aplicaciones](./media/active-directory-saas-coupa-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="28ac5-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="28ac5-125">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="28ac5-126">![Agregar una aplicación de la galería](./media/active-directory-saas-coupa-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="28ac5-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="28ac5-127">En el **cuadro de búsqueda**, escriba **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="28ac5-128">![Galería de aplicaciones](./media/active-directory-saas-coupa-tutorial/IC791898.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="28ac5-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="28ac5-129">En el panel de resultados, seleccione **Coupa** y, después, haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28ac5-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="28ac5-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="28ac5-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="28ac5-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="28ac5-131">Configure single sign-on</span></span>

<span data-ttu-id="28ac5-132">El objetivo de esta sección es describir cómo se habilita la autenticación de usuarios en Coupa con su cuenta de Azure AD mediante la federación basada en el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="28ac5-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="28ac5-133">La configuración de un inicio de sesión único para Coupa requiere la recuperación de un valor de huella digital de un certificado.</span><span class="sxs-lookup"><span data-stu-id="28ac5-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="28ac5-134">Si no está familiarizado con este procedimiento, consulte [Recuperación del valor de huella digital de un certificado](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="28ac5-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="28ac5-135">**Siga estos pasos para configurar el inicio de sesión único:**</span><span class="sxs-lookup"><span data-stu-id="28ac5-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="28ac5-136">Inicie sesión en su sitio de la compañía de Coupa como administrador.</span><span class="sxs-lookup"><span data-stu-id="28ac5-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="28ac5-137">Vaya a **Configuración \> Control de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="28ac5-138">![Controles de seguridad](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de seguridad")</span><span class="sxs-lookup"><span data-stu-id="28ac5-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="28ac5-139">Para descargar el archivo de metadatos de Coupa en el equipo, haga clic en **Descargar e importar metadatos de SP**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="28ac5-140">![Metadatos SP de Coupa](./media/active-directory-saas-coupa-tutorial/IC791901.png "Metadatos SP de Coupa")</span><span class="sxs-lookup"><span data-stu-id="28ac5-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="28ac5-141">En otra ventana de explorador, inicie sesión en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="28ac5-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="28ac5-142">En la página de integración de aplicaciones de **Coupa**, haga clic en **Configurar inicio de sesión único** para abrir el diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="28ac5-143">![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="28ac5-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="28ac5-144">En la página **¿Cómo desea que los usuarios inicien sesión en Coupa?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="28ac5-145">![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="28ac5-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="28ac5-146">En la página **Configurar dirección URL de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="28ac5-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="28ac5-147">![Configurar dirección URL de la aplicación](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="28ac5-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="28ac5-148">En el cuadro de texto **Dirección URL de inicio de sesión**, escriba la dirección URL que los usuarios usan para iniciar sesión en la aplicación Coupa (por ejemplo, “*http://company.Coupa.com*”).</span><span class="sxs-lookup"><span data-stu-id="28ac5-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="28ac5-149">Abra el archivo de metadatos de Coupa descargado y después copie la **dirección URL/índice AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="28ac5-150">En el cuadro de texto **Dirección URL de respuesta de Coupa**, pegue el valor de la **dirección URL/índice AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="28ac5-151">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-151">Click **Next**.</span></span>
8. <span data-ttu-id="28ac5-152">En la página **Configurar inicio de sesión único en Coupa**, para descargar el archivo de metadatos, haga clic en **Descargar metadatos** y, después, guarde el archivo de forma local en el equipo.</span><span class="sxs-lookup"><span data-stu-id="28ac5-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="28ac5-153">![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="28ac5-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="28ac5-154">En el sitio de la compañía de Coupa, vaya a **Configuración \> Control de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="28ac5-155">![Controles de seguridad](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de seguridad")</span><span class="sxs-lookup"><span data-stu-id="28ac5-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="28ac5-156">En la sección **Iniciar sesión con credenciales de Coupa** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="28ac5-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="28ac5-157">![Inicio de sesión con credenciales de Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Inicio de sesión con credenciales de Coupa")</span><span class="sxs-lookup"><span data-stu-id="28ac5-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="28ac5-158">Seleccione **Iniciar sesión con SAML**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="28ac5-159">Haga clic en **Examinar** para cargar el archivo de metadatos de Azure Active descargado.</span><span class="sxs-lookup"><span data-stu-id="28ac5-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="28ac5-160">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-160">Click **Save**.</span></span>
11. <span data-ttu-id="28ac5-161">En el Portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar** para cerrar el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="28ac5-162">![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="28ac5-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="28ac5-163">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="28ac5-163">Configure user provisioning</span></span>

<span data-ttu-id="28ac5-164">Para permitir que los usuarios de Azure AD inicien sesión en Coupa, tienen que aprovisionarse en Coupa.</span><span class="sxs-lookup"><span data-stu-id="28ac5-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="28ac5-165">En el caso de Coupa, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="28ac5-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="28ac5-166">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="28ac5-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="28ac5-167">Inicie sesión como administrador en el sitio de la compañía de **Coupa** .</span><span class="sxs-lookup"><span data-stu-id="28ac5-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="28ac5-168">En el menú en la parte superior, haga clic en **Configurar** y, después, en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="28ac5-169">![Usuarios](./media/active-directory-saas-coupa-tutorial/IC791908.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="28ac5-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="28ac5-170">Haga clic en **Create**(Crear).</span><span class="sxs-lookup"><span data-stu-id="28ac5-170">Click **Create**.</span></span>
   
   <span data-ttu-id="28ac5-171">![Creación de usuarios](./media/active-directory-saas-coupa-tutorial/IC791909.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="28ac5-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="28ac5-172">En la sección **Creación de usuario** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="28ac5-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="28ac5-173">![Detalles del usuario](./media/active-directory-saas-coupa-tutorial/IC791910.png "Detalles del usuario")</span><span class="sxs-lookup"><span data-stu-id="28ac5-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="28ac5-174">En los cuadros de texto relacionados, escriba los atributos **Nombre de usuario**, **Nombre**, **Apellidos**, **Id. de inicio de sesión único**, **Correo electrónico** de una cuenta válida de Azure Active Directory que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="28ac5-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="28ac5-175">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="28ac5-176">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="28ac5-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="28ac5-177">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Canvas ofrecida por Coupa para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="28ac5-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="28ac5-178">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="28ac5-178">Assign users</span></span>
<span data-ttu-id="28ac5-179">Para probar la configuración, debe conceder acceso a los usuarios de Azure AD a los que quiere permitir el uso de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="28ac5-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="28ac5-180">**Para asignar usuarios a Coupa, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="28ac5-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="28ac5-181">En el Portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="28ac5-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="28ac5-182">En el ** Coupa ** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="28ac5-182">On the **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="28ac5-183">![Asignar usuarios](./media/active-directory-saas-coupa-tutorial/IC791911.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="28ac5-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="28ac5-184">Seleccione su usuario de prueba, haga clic en **Asignar** y en **Sí** para confirmar la asignación.</span><span class="sxs-lookup"><span data-stu-id="28ac5-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="28ac5-185">![Sí](./media/active-directory-saas-coupa-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="28ac5-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="28ac5-186">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="28ac5-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="28ac5-187">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="28ac5-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

