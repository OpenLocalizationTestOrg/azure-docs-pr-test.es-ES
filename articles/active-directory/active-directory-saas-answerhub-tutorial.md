---
title: "Tutorial: Integración de Azure Active Directory con AnswerHub | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a1c9cc5d7a2ebe28e9fb7e0e6ed8e3d393873ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="e9990-103">Tutorial: Integración de Azure Active Directory con AnswerHub</span><span class="sxs-lookup"><span data-stu-id="e9990-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="e9990-104">En este tutorial, obtendrá información sobre cómo integrar AnswerHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9990-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9990-105">La integración de AnswerHub con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e9990-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e9990-106">En Azure AD puede controlar quién tiene acceso a AnswerHub</span><span class="sxs-lookup"><span data-stu-id="e9990-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="e9990-107">Puede permitir que los usuarios inicien sesión automáticamente en AnswerHub (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9990-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9990-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e9990-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e9990-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9990-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9990-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e9990-110">Prerequisites</span></span>

<span data-ttu-id="e9990-111">Para configurar la integración de Azure AD con AnswerHub, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e9990-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="e9990-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9990-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9990-113">Una suscripción habilitada para el inicio de sesión único en AnswerHub</span><span class="sxs-lookup"><span data-stu-id="e9990-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9990-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e9990-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9990-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e9990-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9990-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e9990-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9990-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9990-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9990-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e9990-118">Scenario description</span></span>
<span data-ttu-id="e9990-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e9990-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9990-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e9990-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9990-121">Incorporación de AnswerHub desde la galería</span><span class="sxs-lookup"><span data-stu-id="e9990-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="e9990-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9990-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="e9990-123">Incorporación de AnswerHub desde la galería</span><span class="sxs-lookup"><span data-stu-id="e9990-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="e9990-124">Para configurar la integración de AnswerHub en Azure AD, será preciso que agregue AnswerHub desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e9990-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9990-125">**Para agregar AnswerHub desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e9990-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9990-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9990-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e9990-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e9990-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e9990-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e9990-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e9990-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9990-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e9990-133">En el cuadro de búsqueda, escriba **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="e9990-133">In the search box, type **AnswerHub**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="e9990-135">En el panel de resultados, seleccione **AnswerHub** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9990-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9990-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9990-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9990-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con AnswerHub con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e9990-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9990-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de AnswerHub para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9990-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="e9990-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="e9990-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="e9990-141">Para establecer la relación de vínculo, en AnswerHub, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e9990-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e9990-142">Para configurar y probar el inicio de sesión único de Azure AD con AnswerHub, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e9990-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9990-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e9990-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9990-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9990-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9990-145">**[Creación de un usuario de prueba de AnswerHub](#creating-an-answerhub-test-user)**: para tener un homólogo de Britta Simon en AnswerHub que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9990-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9990-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9990-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9990-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e9990-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9990-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9990-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9990-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="e9990-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="e9990-150">**Para configurar el inicio de sesión único de Azure AD con AnswerHub, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e9990-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="e9990-151">En Azure Portal, en la página de integración de la aplicación **AnswerHub**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e9990-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e9990-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e9990-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="e9990-155">En la sección de **dominio y direcciones URL de AnswerHub**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e9990-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="e9990-157">a.</span><span class="sxs-lookup"><span data-stu-id="e9990-157">a.</span></span> <span data-ttu-id="e9990-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company>.answerhub.com`.</span><span class="sxs-lookup"><span data-stu-id="e9990-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="e9990-159">b.</span><span class="sxs-lookup"><span data-stu-id="e9990-159">b.</span></span> <span data-ttu-id="e9990-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="e9990-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e9990-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e9990-161">These values are not real.</span></span> <span data-ttu-id="e9990-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e9990-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e9990-163">Póngase en contacto con el [equipo de soporte de cliente de AnswerHub](mailto:success@answerhub.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="e9990-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="e9990-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e9990-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="e9990-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e9990-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e9990-168">En la sección **Configuración de AnswerHub**, haga clic en **Configurar AnswerHub** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e9990-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e9990-169">Copie la **dirección URL de cierre de sesión y la dirección URL del servicio de inicio de sesión único de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="e9990-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="e9990-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de AnswerHub como administrador.</span><span class="sxs-lookup"><span data-stu-id="e9990-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="e9990-172">Si necesita ayuda para configurar AnswerHub, póngase en contacto con el [equipo de soporte técnico de AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="e9990-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="e9990-173">Vaya a **Administración**.</span><span class="sxs-lookup"><span data-stu-id="e9990-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="e9990-174">Haga clic en la pestaña **Usuario y grupo** .</span><span class="sxs-lookup"><span data-stu-id="e9990-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="e9990-175">En el panel de navegación izquierdo, en la sección **Social Settings** (Configuración social), haga clic en **SAML Setup** (Configuración de SAML).</span><span class="sxs-lookup"><span data-stu-id="e9990-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="e9990-176">Haga clic en la pestaña **Configuración de IDP** .</span><span class="sxs-lookup"><span data-stu-id="e9990-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="e9990-177">En la pestaña **Configuración de IDP** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e9990-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="e9990-178">![Configuración de SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="e9990-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="e9990-179">a.</span><span class="sxs-lookup"><span data-stu-id="e9990-179">a.</span></span> <span data-ttu-id="e9990-180">En el cuadro de texto **IDP Login URL** (Dirección URL de inicio de sesión de IDP), pegue la **dirección URL del servicio de inicio de sesión único de SAML** que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e9990-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="e9990-181">b.</span><span class="sxs-lookup"><span data-stu-id="e9990-181">b.</span></span> <span data-ttu-id="e9990-182">En el cuadro de texto **IDP Logout URL** (Dirección URL de cierre de sesión de IDP), pegue la **dirección URL de cierre de sesión** que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e9990-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="e9990-183">c.</span><span class="sxs-lookup"><span data-stu-id="e9990-183">c.</span></span> <span data-ttu-id="e9990-184">En el cuadro de texto **IDP Name Identifier Format** (Formato del identificador de nombre de IDP), escriba el valor de identificador de usuario igual que el que se seleccionó en Azure Portal en la sección **Atributos de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e9990-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="e9990-185">d.</span><span class="sxs-lookup"><span data-stu-id="e9990-185">d.</span></span> <span data-ttu-id="e9990-186">Haga clic en **Claves y certificados**.</span><span class="sxs-lookup"><span data-stu-id="e9990-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="e9990-187">En la pestaña Claves y certificados, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e9990-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="e9990-188">![Claves y certificados](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Claves y certificados")</span><span class="sxs-lookup"><span data-stu-id="e9990-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="e9990-189">a.</span><span class="sxs-lookup"><span data-stu-id="e9990-189">a.</span></span> <span data-ttu-id="e9990-190">Abra el certificado codificado en Base 64 que descargó de Azure Portal en el Bloc de notas, copie el contenido en el Portapapeles y, luego, péguelo en el cuadro de texto **IDP Public Key (x509 Format)** (Clave pública de IDP [formato x509]).</span><span class="sxs-lookup"><span data-stu-id="e9990-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="e9990-191">b.</span><span class="sxs-lookup"><span data-stu-id="e9990-191">b.</span></span> <span data-ttu-id="e9990-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e9990-192">Click **Save**.</span></span>

14. <span data-ttu-id="e9990-193">En la pestaña **IDP Config** (Configuración de IDP), haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="e9990-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e9990-194">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9990-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e9990-195">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e9990-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e9990-196">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9990-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9990-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9990-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9990-198">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e9990-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e9990-200">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e9990-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9990-201">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9990-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9990-203">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e9990-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9990-205">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9990-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9990-207">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e9990-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9990-209">a.</span><span class="sxs-lookup"><span data-stu-id="e9990-209">a.</span></span> <span data-ttu-id="e9990-210">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9990-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9990-211">b.</span><span class="sxs-lookup"><span data-stu-id="e9990-211">b.</span></span> <span data-ttu-id="e9990-212">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9990-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9990-213">c.</span><span class="sxs-lookup"><span data-stu-id="e9990-213">c.</span></span> <span data-ttu-id="e9990-214">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e9990-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e9990-215">d.</span><span class="sxs-lookup"><span data-stu-id="e9990-215">d.</span></span> <span data-ttu-id="e9990-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e9990-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="e9990-217">Creación de un usuario de prueba de AnswerHub</span><span class="sxs-lookup"><span data-stu-id="e9990-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="e9990-218">Para permitir que los usuarios de Azure AD inicien sesión en AnswerHub, tienen que aprovisionarse en AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="e9990-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="e9990-219">En el caso de AnswerHub, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="e9990-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="e9990-220">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="e9990-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e9990-221">Inicie sesión en el sitio de la compañía de **AnswerHub** como administrador.</span><span class="sxs-lookup"><span data-stu-id="e9990-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="e9990-222">Vaya a **Administración**.</span><span class="sxs-lookup"><span data-stu-id="e9990-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="e9990-223">Haga clic en la pestaña **Users & Groups** (Usuarios y grupos).</span><span class="sxs-lookup"><span data-stu-id="e9990-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="e9990-224">En el panel de navegación izquierdo, en la sección **Manage Users** (Administrar usuarios), haga clic en **Create or import users** (Crear o importar usuarios).</span><span class="sxs-lookup"><span data-stu-id="e9990-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="e9990-225">![Usuarios y grupos](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Usuarios y grupos")</span><span class="sxs-lookup"><span data-stu-id="e9990-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="e9990-226">Escriba la **dirección de correo electrónico**, el **nombre de usuario** y la **contraseña** de una cuenta de Azure Active Directory válida que desee aprovisionar en los cuadros de texto relacionados y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="e9990-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="e9990-227">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de AnswerHub ofrecida por AnswerHub para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="e9990-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e9990-228">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9990-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e9990-229">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="e9990-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e9990-231">**Para asignar Britta Simon a AnswerHub, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e9990-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="e9990-232">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e9990-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e9990-234">En la lista de aplicaciones, seleccione **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="e9990-234">In the applications list, select **AnswerHub**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="e9990-236">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e9990-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e9990-238">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e9990-238">Click **Add** button.</span></span> <span data-ttu-id="e9990-239">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e9990-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e9990-241">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e9990-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e9990-242">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e9990-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9990-243">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e9990-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e9990-244">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e9990-244">Testing single sign-on</span></span>

<span data-ttu-id="e9990-245">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e9990-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e9990-246">Al hacer clic en el icono de AnswerHub en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="e9990-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="e9990-247">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e9990-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e9990-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e9990-248">Additional resources</span></span>

* [<span data-ttu-id="e9990-249">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9990-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9990-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9990-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

