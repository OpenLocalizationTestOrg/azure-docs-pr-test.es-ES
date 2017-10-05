---
title: "Tutorial: Integración de Azure Active Directory con Benefitsolver | Microsoft Docs"
description: "Aprenda cómo usar Benefitsolver con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="a72f0-103">Tutorial: Integración de Azure Active Directory con Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="a72f0-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="a72f0-104">El objetivo de este tutorial es mostrar la integración de Azure y Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="a72f0-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="a72f0-105">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a72f0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="a72f0-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="a72f0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a72f0-107">Una suscripción habilitada para el inicio de sesión único (SSO) en Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="a72f0-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="a72f0-108">Después de completar este tutorial, los usuarios de Azure AD que haya asignado a Benefitsolver podrán realizar inicios de sesión únicos en la aplicación utilizando [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a72f0-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a72f0-109">La situación descrita en este tutorial consta de los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a72f0-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="a72f0-110">Habilitación de la integración de aplicaciones para Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="a72f0-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="a72f0-111">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="a72f0-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="a72f0-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="a72f0-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="a72f0-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="a72f0-113">Assigning users</span></span>

<span data-ttu-id="a72f0-114">![Escenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="a72f0-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="a72f0-115">Habilitación de la integración de aplicaciones para Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="a72f0-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="a72f0-116">El objetivo de esta sección es describir cómo habilitar la integración de las aplicaciones para Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="a72f0-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="a72f0-117">Siga estos pasos para habilitar la integración de aplicaciones en Benefitsolver:</span><span class="sxs-lookup"><span data-stu-id="a72f0-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="a72f0-118">En el panel de navegación izquierdo del Portal de Azure clásico, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="a72f0-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a72f0-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a72f0-120">En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="a72f0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a72f0-121">Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="a72f0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="a72f0-122">![Aplicaciones](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="a72f0-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a72f0-123">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="a72f0-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="a72f0-124">![Agregar aplicaciones](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="a72f0-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a72f0-125">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="a72f0-126">![Agregar una aplicación de la galería](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="a72f0-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="a72f0-127">En el **cuadro de búsqueda**, escriba **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="a72f0-128">![Galería de aplicaciones](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="a72f0-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="a72f0-129">En el panel de resultados, seleccione **Benefitsolver** y, luego, haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a72f0-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="a72f0-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="a72f0-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="a72f0-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="a72f0-131">Configure single sign-on</span></span>

<span data-ttu-id="a72f0-132">El objetivo de esta sección es describir cómo se habilita la autenticación de los usuarios en Benefitsolver con su cuenta de Azure AD mediante la federación basada en el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="a72f0-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="a72f0-133">La aplicación Benefitsolver espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los **atributos del token de SAML** .</span><span class="sxs-lookup"><span data-stu-id="a72f0-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="a72f0-134">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="a72f0-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="a72f0-135">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="a72f0-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="a72f0-136">**Siga estos pasos para configurar el inicio de sesión único:**</span><span class="sxs-lookup"><span data-stu-id="a72f0-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="a72f0-137">En el Portal de Azure clásico, en la página de integración de aplicaciones de **Benefitsolver**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a72f0-138">![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="a72f0-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="a72f0-139">En la página **¿Cómo desea que los usuarios inicien sesión en Benefitsolver?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y, luego , haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="a72f0-140">![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="a72f0-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="a72f0-141">En la página **Configurar las opciones de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a72f0-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="a72f0-142">![Configurar las opciones de la aplicación](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configurar las opciones de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="a72f0-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="a72f0-143">En el cuadro de texto **URL de inicio de sesión**, escriba **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="a72f0-144">En el cuadro de texto **URL de respuesta**, escriba **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="a72f0-145">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-145">Click **Next**.</span></span>
4. <span data-ttu-id="a72f0-146">En la página **Configuración de inicio de sesión único en Benefitsolver**, para descargar los metadatos, haga clic en **Descargar metadatos** y, luego, guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a72f0-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="a72f0-147">![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="a72f0-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="a72f0-148">Envíe el archivo de metadatos descargado al equipo de soporte técnico de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="a72f0-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="a72f0-149">El equipo de soporte técnico de Benefitsolver es el que tiene que realizar la configuración real de SSO.</span><span class="sxs-lookup"><span data-stu-id="a72f0-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="a72f0-150">Cuando SSO se haya habilitado en su suscripción recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="a72f0-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="a72f0-151">En el Portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar** para cerrar el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a72f0-152">![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="a72f0-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="a72f0-153">En el menú de la parte superior, haga clic en **Atributos** to open the **SAML Token Atributos** .</span><span class="sxs-lookup"><span data-stu-id="a72f0-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="a72f0-154">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="a72f0-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="a72f0-155">Para agregar las asignaciones de los atributos necesarios, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a72f0-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="a72f0-156">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="a72f0-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="a72f0-157">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="a72f0-157">Attribute Name</span></span> | <span data-ttu-id="a72f0-158">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="a72f0-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="a72f0-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="a72f0-159">ClientID</span></span> |<span data-ttu-id="a72f0-160">Para obtener este valor tiene que acudir al equipo de soporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="a72f0-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="a72f0-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="a72f0-161">ClientKey</span></span> |<span data-ttu-id="a72f0-162">Para obtener este valor tiene que acudir al equipo de soporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="a72f0-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="a72f0-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="a72f0-163">LogoutURL</span></span> |<span data-ttu-id="a72f0-164">Para obtener este valor tiene que acudir al equipo de soporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="a72f0-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="a72f0-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="a72f0-165">EmployeeID</span></span> |<span data-ttu-id="a72f0-166">Para obtener este valor tiene que acudir al equipo de soporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="a72f0-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="a72f0-167">En cada fila de datos de la tabla anterior, haga clic en **agregar atributo de usuario**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="a72f0-168">En el cuadro de texto **Nombre de atributo** , escriba el nombre de atributo que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="a72f0-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="a72f0-169">En el cuadro de texto **Valor de atributo** , seleccione el valor de atributo que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="a72f0-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="a72f0-170">Haga clic en **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-170">Click **Complete**.</span></span>
9. <span data-ttu-id="a72f0-171">Haga clic en **Aplicar cambios**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="a72f0-172">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="a72f0-172">Configure user provisioning</span></span>
<span data-ttu-id="a72f0-173">Para permitir que los usuarios de Azure AD inicien sesión en Benefitsolver, deben aprovisionarse a Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="a72f0-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="a72f0-174">En el caso de Benefitsolver, los datos de empleados en la aplicación se rellenan a través de un archivo Census de su sistema HRIS (normalmente por la noche).</span><span class="sxs-lookup"><span data-stu-id="a72f0-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="a72f0-175">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Benefitsolver para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="a72f0-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="a72f0-176">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="a72f0-176">Assigning users</span></span>
<span data-ttu-id="a72f0-177">Para probar la configuración, debe asignar los usuarios de Azure AD que quiera que usen su aplicación para concederles acceso a ella.</span><span class="sxs-lookup"><span data-stu-id="a72f0-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="a72f0-178">Para asignar usuarios a Benefitsolver, lleve a cabo los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="a72f0-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="a72f0-179">En el Portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="a72f0-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a72f0-180">En el ** Benefitsolver ** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a72f0-180">On the **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="a72f0-181">![Asignar usuarios](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="a72f0-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="a72f0-182">Seleccione su usuario de prueba, haga clic en **Asignar** y en **Sí** para confirmar la asignación.</span><span class="sxs-lookup"><span data-stu-id="a72f0-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="a72f0-183">![Sí](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="a72f0-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a72f0-184">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a72f0-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a72f0-185">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a72f0-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

