---
title: "Tutorial: integración de Azure Active Directory con Flatter Files | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Flatter Files."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: e02150cb27768d7b403bdca191bc1f189821def4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="42c91-103">Tutorial: integración de Azure Active Directory con Flatter Files</span><span class="sxs-lookup"><span data-stu-id="42c91-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="42c91-104">En este tutorial, aprenderá a integrar Flatter Files con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42c91-104">In this tutorial, you learn how to integrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42c91-105">Integrar Flatter Files con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="42c91-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42c91-106">Puede controlar en Azure AD quién tiene acceso a Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="42c91-106">You can control in Azure AD who has access to Flatter Files</span></span>
- <span data-ttu-id="42c91-107">Puede permitir que los usuarios inicien sesión automáticamente en Flatter Files (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42c91-107">You can enable your users to automatically get signed-on to Flatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42c91-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="42c91-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="42c91-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42c91-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42c91-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="42c91-110">Prerequisites</span></span>

<span data-ttu-id="42c91-111">Para configurar la integración de Azure AD con Flatter Files, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="42c91-111">To configure Azure AD integration with Flatter Files, you need the following items:</span></span>

- <span data-ttu-id="42c91-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42c91-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42c91-113">Una suscripción habilitada para el inicio de sesión único en Flatter Files</span><span class="sxs-lookup"><span data-stu-id="42c91-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42c91-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="42c91-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42c91-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="42c91-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42c91-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="42c91-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42c91-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42c91-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42c91-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="42c91-118">Scenario description</span></span>
<span data-ttu-id="42c91-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="42c91-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42c91-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="42c91-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42c91-121">Adición de Flatter Files desde la galería</span><span class="sxs-lookup"><span data-stu-id="42c91-121">Adding Flatter Files from the gallery</span></span>
2. <span data-ttu-id="42c91-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42c91-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-the-gallery"></a><span data-ttu-id="42c91-123">Adición de Flatter Files desde la galería</span><span class="sxs-lookup"><span data-stu-id="42c91-123">Adding Flatter Files from the gallery</span></span>
<span data-ttu-id="42c91-124">Para configurar la integración de Flatter Files en Azure AD, deberá agregar Flatter Files desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="42c91-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42c91-125">**Para agregar Flatter Files desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="42c91-125">**To add Flatter Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42c91-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42c91-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42c91-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="42c91-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42c91-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="42c91-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="42c91-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42c91-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="42c91-133">En el cuadro de búsqueda, escriba **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="42c91-133">In the search box, type **Flatter Files**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="42c91-135">En el panel de resultados, seleccione **Flatter Files** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="42c91-135">In the results panel, select **Flatter Files**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42c91-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42c91-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42c91-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Flatter Files con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="42c91-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42c91-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Flatter Files para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42c91-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Flatter Files is to a user in Azure AD.</span></span> <span data-ttu-id="42c91-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="42c91-140">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span></span>

<span data-ttu-id="42c91-141">Para establecer la relación de vínculo, en Flatter Files, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="42c91-141">In Flatter Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="42c91-142">Para configurar y probar el inicio de sesión único de Azure AD con Flatter Files, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="42c91-142">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42c91-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="42c91-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42c91-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42c91-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42c91-145">**[Creación de un usuario de prueba de Flatter Files](#creating-a-flatter-files-test-user)**: para tener un homólogo de Britta Simon en CS Stars que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42c91-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="42c91-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42c91-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42c91-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="42c91-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42c91-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42c91-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42c91-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="42c91-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="42c91-150">**Para configurar el inicio de sesión único de Azure AD con Flatter Files, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="42c91-150">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="42c91-151">En Azure Portal, en la página de integración de la aplicación **Flatter Files**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="42c91-151">In the Azure portal, on the **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="42c91-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="42c91-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="42c91-155">En la sección **Dominio y direcciones URL de Flatter Files**, el usuario no tiene que realizar ningún paso ya que la aplicación se ha integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="42c91-155">On the **Flatter Files Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="42c91-157">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="42c91-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="42c91-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="42c91-159">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42c91-161">En la sección **Configuración de Flatter Files**, haga clic en **Configurar Flatter Files** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="42c91-161">On the **Flatter Files Configuration** section, click **Configure Flatter Files** to open **Configure sign-on** window.</span></span> <span data-ttu-id="42c91-162">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="42c91-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="42c91-164">Inicie sesión en su aplicación de Flatter Files como administrador.</span><span class="sxs-lookup"><span data-stu-id="42c91-164">Sign-on to your Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="42c91-165">Haga clic en **PANEL**.</span><span class="sxs-lookup"><span data-stu-id="42c91-165">Click **DASHBOARD**.</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="42c91-167">Haga clic en **Settings** (Configuración) y, después, siga estos pasos siguientes en la pestaña **Company** (Compañía):</span><span class="sxs-lookup"><span data-stu-id="42c91-167">Click **Settings**, and then perform the following steps on the **Company** tab:</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="42c91-169">a.</span><span class="sxs-lookup"><span data-stu-id="42c91-169">a.</span></span> <span data-ttu-id="42c91-170">Seleccione **Usar SAML 2.0 para autenticación**.</span><span class="sxs-lookup"><span data-stu-id="42c91-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="42c91-171">b.</span><span class="sxs-lookup"><span data-stu-id="42c91-171">b.</span></span> <span data-ttu-id="42c91-172">Haga clic en **Configurar SAML**.</span><span class="sxs-lookup"><span data-stu-id="42c91-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="42c91-173">En el cuadro de diálogo **Configuración de SAML** , realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="42c91-173">On the **SAML Configuration** dialog, perform the following steps:</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="42c91-175">a.</span><span class="sxs-lookup"><span data-stu-id="42c91-175">a.</span></span> <span data-ttu-id="42c91-176">En el cuadro de texto **Dominio**, escriba el dominio registrado.</span><span class="sxs-lookup"><span data-stu-id="42c91-176">In the **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="42c91-177">Si no dispone de un dominio registrado, póngase en contacto con el equipo de soporte técnico de Flatter Files a través de [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="42c91-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="42c91-178">b.</span><span class="sxs-lookup"><span data-stu-id="42c91-178">b.</span></span> <span data-ttu-id="42c91-179">En el cuadro de texto **Identity Provider URL** (Dirección URL del proveedor de identidades), pegue el valor de **Dirección URL del servicio de inicio de sesión único de SAML** que ha copiado en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="42c91-179">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="42c91-180">c.</span><span class="sxs-lookup"><span data-stu-id="42c91-180">c.</span></span>  <span data-ttu-id="42c91-181">Abra el certificado codificado en base 64 en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado de proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="42c91-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="42c91-182">d.</span><span class="sxs-lookup"><span data-stu-id="42c91-182">d.</span></span> <span data-ttu-id="42c91-183">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="42c91-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="42c91-184">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="42c91-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42c91-185">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="42c91-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42c91-186">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42c91-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42c91-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42c91-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="42c91-188">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="42c91-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="42c91-190">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="42c91-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42c91-191">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42c91-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42c91-193">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="42c91-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42c91-195">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42c91-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42c91-197">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="42c91-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42c91-199">a.</span><span class="sxs-lookup"><span data-stu-id="42c91-199">a.</span></span> <span data-ttu-id="42c91-200">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42c91-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42c91-201">b.</span><span class="sxs-lookup"><span data-stu-id="42c91-201">b.</span></span> <span data-ttu-id="42c91-202">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42c91-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42c91-203">c.</span><span class="sxs-lookup"><span data-stu-id="42c91-203">c.</span></span> <span data-ttu-id="42c91-204">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="42c91-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="42c91-205">d.</span><span class="sxs-lookup"><span data-stu-id="42c91-205">d.</span></span> <span data-ttu-id="42c91-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="42c91-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="42c91-207">Creación de un usuario de prueba de Flatter Files</span><span class="sxs-lookup"><span data-stu-id="42c91-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="42c91-208">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="42c91-208">The objective of this section is to create a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="42c91-209">**Para crear una usuaria llamada Britta Simon en Flatter Files, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="42c91-209">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="42c91-210">Inicie sesión en su sitio de la compañía de **Flatter Files** como administrador.</span><span class="sxs-lookup"><span data-stu-id="42c91-210">Sign on to your **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="42c91-211">En el panel de navegación de la izquierda, haga clic en **Configuración** y, luego, en la pestaña **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="42c91-211">In the navigation pane on the left, click **Settings**, and then click the **Users** tab.</span></span>
   
    ![Creación de un usuario de Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="42c91-213">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="42c91-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="42c91-214">En el cuadro de diálogo **Agregar usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="42c91-214">On the **Add User** dialog, perform the following steps:</span></span>
   
    ![Creación de un usuario de Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="42c91-216">a.</span><span class="sxs-lookup"><span data-stu-id="42c91-216">a.</span></span> <span data-ttu-id="42c91-217">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="42c91-217">In the **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="42c91-218">b.</span><span class="sxs-lookup"><span data-stu-id="42c91-218">b.</span></span> <span data-ttu-id="42c91-219">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="42c91-219">In the **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="42c91-220">c.</span><span class="sxs-lookup"><span data-stu-id="42c91-220">c.</span></span> <span data-ttu-id="42c91-221">En el cuadro de texto **Dirección de correo electrónico**, escriba la dirección de correo electrónico de Britta en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="42c91-221">In the **Email Address** textbox, type Britta's email address in the Azure portal.</span></span>
   
    <span data-ttu-id="42c91-222">d.</span><span class="sxs-lookup"><span data-stu-id="42c91-222">d.</span></span> <span data-ttu-id="42c91-223">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="42c91-223">Click **Submit**.</span></span>   


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="42c91-224">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42c91-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="42c91-225">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="42c91-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flatter Files.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="42c91-227">**Para asignar a Britta Simon a Flatter Files, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="42c91-227">**To assign Britta Simon to Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="42c91-228">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="42c91-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="42c91-230">En la lista de aplicaciones, seleccione **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="42c91-230">In the applications list, select **Flatter Files**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="42c91-232">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="42c91-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="42c91-234">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="42c91-234">Click **Add** button.</span></span> <span data-ttu-id="42c91-235">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="42c91-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="42c91-237">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="42c91-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42c91-238">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="42c91-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42c91-239">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="42c91-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42c91-240">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="42c91-240">Testing single sign-on</span></span>

<span data-ttu-id="42c91-241">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="42c91-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="42c91-242">Al hacer clic en el icono de Flatter Files en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="42c91-242">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span></span>
<span data-ttu-id="42c91-243">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42c91-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="42c91-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="42c91-244">Additional resources</span></span>

* [<span data-ttu-id="42c91-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42c91-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42c91-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42c91-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

