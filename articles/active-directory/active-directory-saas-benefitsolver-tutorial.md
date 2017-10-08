---
title: "Tutorial: Integración de Azure Active Directory con Benefitsolver | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Benefitsolver con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
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
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="c4459-103">Tutorial: Integración de Azure Active Directory con Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="c4459-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="c4459-104">objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="c4459-104">hello objective of this tutorial is tooshow hello integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="c4459-105">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c4459-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="c4459-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="c4459-106">A valid Azure subscription</span></span>
* <span data-ttu-id="c4459-107">Una suscripción habilitada para el inicio de sesión único (SSO) en Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="c4459-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="c4459-108">Después de completar este tutorial, los usuarios de hello Azure AD que haya asignado tooBenefitsolver será capaz de toosingle inicio de sesión en la aplicación hello mediante hello [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4459-108">After completing this tutorial, hello Azure AD users you have assigned tooBenefitsolver will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="c4459-109">escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c4459-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="c4459-110">Habilitar la integración de aplicación Hola para Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="c4459-110">Enabling hello application integration for Benefitsolver</span></span>
2. <span data-ttu-id="c4459-111">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="c4459-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="c4459-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="c4459-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="c4459-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="c4459-113">Assigning users</span></span>

<span data-ttu-id="c4459-114">![Escenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="c4459-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-benefitsolver"></a><span data-ttu-id="c4459-115">Habilitar la integración de aplicación Hola para Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="c4459-115">Enabling hello application integration for Benefitsolver</span></span>
<span data-ttu-id="c4459-116">objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="c4459-116">hello objective of this section is toooutline how tooenable hello application integration for Benefitsolver.</span></span>

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a><span data-ttu-id="c4459-117">integración de aplicaciones de hello tooenable para Benefitsolver, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c4459-117">tooenable hello application integration for Benefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="c4459-118">Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4459-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="c4459-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c4459-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="c4459-120">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="c4459-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="c4459-121">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="c4459-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="c4459-122">![Aplicaciones](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="c4459-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="c4459-123">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="c4459-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="c4459-124">![Agregar aplicaciones](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="c4459-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="c4459-125">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="c4459-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="c4459-126">![Agregar una aplicación de la galería](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="c4459-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="c4459-127">Hola **cuadro de búsqueda**, tipo **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="c4459-127">In hello **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="c4459-128">![Galería de aplicaciones](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="c4459-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="c4459-129">En el panel de resultados de hello, seleccione **Benefitsolver**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c4459-129">In hello results pane, select **Benefitsolver**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="c4459-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="c4459-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="c4459-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="c4459-131">Configure single sign-on</span></span>

<span data-ttu-id="c4459-132">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooBenefitsolver con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4459-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooBenefitsolver with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="c4459-133">La aplicación de Benefitsolver espera las aserciones de SAML de hello en un formato específico, lo que requiere tooyour de asignaciones de atributo personalizado de tooadd **atributos de token saml** configuración.</span><span class="sxs-lookup"><span data-stu-id="c4459-133">Your Benefitsolver application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> 

<span data-ttu-id="c4459-134">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="c4459-134">hello following screenshot shows an example for this.</span></span>

<span data-ttu-id="c4459-135">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="c4459-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="c4459-136">**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c4459-136">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4459-137">En el portal de Azure clásico en Hola Hola **Benefitsolver** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4459-137">In hello Azure classic portal, on hello **Benefitsolver** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c4459-138">![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c4459-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="c4459-139">En hello **¿cómo desea que los usuarios toosign en tooBenefitsolver** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c4459-139">On hello **How would you like users toosign on tooBenefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="c4459-140">![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c4459-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="c4459-141">En hello **configurar opciones de aplicación** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c4459-141">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="c4459-142">![Configurar las opciones de la aplicación](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configurar las opciones de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="c4459-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="c4459-143">Hola **dirección URL de inicio de sesión** cuadro de texto, tipo **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="c4459-143">In hello **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="c4459-144">Hola **dirección URL de respuesta** cuadro de texto, tipo **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="c4459-144">In hello **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="c4459-145">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c4459-145">Click **Next**.</span></span>
4. <span data-ttu-id="c4459-146">En hello **configurar inicio de sesión único en Benefitsolver** page, toodownload sus metadatos, haga clic en **descargar metadatos**y, a continuación, guarde el archivo de metadatos de hello localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c4459-146">On hello **Configure single sign-on at Benefitsolver** page, toodownload your metadata, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="c4459-147">![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c4459-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="c4459-148">Enviar el equipo de soporte técnico de hello descargar metadatos archivo tooyour Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="c4459-148">Send hello downloaded metadata file tooyour Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="c4459-149">El equipo de soporte de Benefitsolver tiene la configuración real del SSO toodo Hola.</span><span class="sxs-lookup"><span data-stu-id="c4459-149">Your Benefitsolver support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="c4459-150">Cuando SSO se haya habilitado en su suscripción recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="c4459-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="c4459-151">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4459-151">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c4459-152">![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c4459-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="c4459-153">En el menú de hello en la parte superior de hello, haga clic en **atributos** tooopen hello **atributos de Token SAML** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4459-153">In hello menu on hello top, click **Attributes** tooopen hello **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="c4459-154">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="c4459-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="c4459-155">asignaciones de atributos de tooadd Hola necesario, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c4459-155">tooadd hello required attribute mappings, perform hello following steps:</span></span>
   
   <span data-ttu-id="c4459-156">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="c4459-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="c4459-157">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="c4459-157">Attribute Name</span></span> | <span data-ttu-id="c4459-158">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="c4459-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="c4459-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="c4459-159">ClientID</span></span> |<span data-ttu-id="c4459-160">Debe tooget este valor desde el equipo de soporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="c4459-160">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="c4459-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="c4459-161">ClientKey</span></span> |<span data-ttu-id="c4459-162">Debe tooget este valor desde el equipo de soporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="c4459-162">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="c4459-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="c4459-163">LogoutURL</span></span> |<span data-ttu-id="c4459-164">Debe tooget este valor desde el equipo de soporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="c4459-164">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="c4459-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="c4459-165">EmployeeID</span></span> |<span data-ttu-id="c4459-166">Debe tooget este valor desde el equipo de soporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="c4459-166">You need tooget this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="c4459-167">Para cada fila de datos de tabla de hello anterior, haga clic en **Agregar atributo de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c4459-167">For each data row in hello table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="c4459-168">Hola **nombre del atributo** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="c4459-168">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
   3. <span data-ttu-id="c4459-169">Hola **valor del atributo** cuadro de texto, valor de atributo seleccione Hola se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="c4459-169">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
   4. <span data-ttu-id="c4459-170">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="c4459-170">Click **Complete**.</span></span>
9. <span data-ttu-id="c4459-171">Haga clic en **Aplicar cambios**.</span><span class="sxs-lookup"><span data-stu-id="c4459-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="c4459-172">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="c4459-172">Configure user provisioning</span></span>
<span data-ttu-id="c4459-173">En orden tooenable toolog de los usuarios de Azure AD en Benefitsolver, se les deben aprovisionar en Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="c4459-173">In order tooenable Azure AD users toolog into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="c4459-174">En caso de hello de Benefitsolver, los datos del empleado están en la aplicación que se rellenan a través de un archivo del censo desde el sistema HRIS (normalmente por la noche).</span><span class="sxs-lookup"><span data-stu-id="c4459-174">In hello case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="c4459-175">Puede usar cualquier otra Benefitsolver usuario cuenta herramienta de creación o las API proporcionadas por Benefitsolver tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="c4459-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver tooprovision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="c4459-176">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="c4459-176">Assigning users</span></span>
<span data-ttu-id="c4459-177">tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.</span><span class="sxs-lookup"><span data-stu-id="c4459-177">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a><span data-ttu-id="c4459-178">tooassign tooBenefitsolver de los usuarios, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c4459-178">tooassign users tooBenefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="c4459-179">Hola portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="c4459-179">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="c4459-180">En Hola ** Benefitsolver ** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c4459-180">On hello **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="c4459-181">![Asignar usuarios](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="c4459-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="c4459-182">Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.</span><span class="sxs-lookup"><span data-stu-id="c4459-182">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="c4459-183">![Sí](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="c4459-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c4459-184">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c4459-184">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="c4459-185">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4459-185">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

