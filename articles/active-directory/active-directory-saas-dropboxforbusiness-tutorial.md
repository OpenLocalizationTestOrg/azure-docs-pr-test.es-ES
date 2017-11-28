---
title: "Tutorial: Integración de Azure Active Directory con Dropbox for Business | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: a56a5af171eaca259db29f25fee4331a77313420
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="573eb-103">Tutorial: Integración de Azure Active Directory con Dropbox para Empresas</span><span class="sxs-lookup"><span data-stu-id="573eb-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="573eb-104">En este tutorial, aprenderá a integrar Dropbox for Business con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="573eb-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="573eb-105">La integración de Dropbox for Business con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="573eb-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="573eb-106">En Azure AD se puede controlar quién tiene acceso a Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="573eb-106">You can control in Azure AD who has access to Dropbox for Business</span></span>
- <span data-ttu-id="573eb-107">Es posible habilitar que los usuarios inicien sesión automáticamente en Dropbox for Business (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="573eb-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="573eb-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="573eb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="573eb-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="573eb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="573eb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="573eb-110">Prerequisites</span></span>

<span data-ttu-id="573eb-111">Para configurar la integración de Azure AD con Dropbox for Business, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="573eb-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span></span>

- <span data-ttu-id="573eb-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="573eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="573eb-113">Una suscripción a Dropbox for Business con inicio de sesión único habilitado.</span><span class="sxs-lookup"><span data-stu-id="573eb-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="573eb-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="573eb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="573eb-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="573eb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="573eb-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="573eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="573eb-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="573eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="573eb-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="573eb-118">Scenario description</span></span>
<span data-ttu-id="573eb-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="573eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="573eb-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="573eb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="573eb-121">Adición de Dropbox for Business desde la galería</span><span class="sxs-lookup"><span data-stu-id="573eb-121">Adding Dropbox for Business from the gallery</span></span>
2. <span data-ttu-id="573eb-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="573eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-the-gallery"></a><span data-ttu-id="573eb-123">Adición de Dropbox for Business desde la galería</span><span class="sxs-lookup"><span data-stu-id="573eb-123">Adding Dropbox for Business from the gallery</span></span>
<span data-ttu-id="573eb-124">Para configurar la integración de Dropbox for Business en Azure AD, es preciso agregar Dropbox for Business desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="573eb-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="573eb-125">**Para agregar Dropbox for Business desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="573eb-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="573eb-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="573eb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="573eb-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="573eb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="573eb-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="573eb-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="573eb-131">Haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="573eb-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="573eb-133">En el cuadro de búsqueda, escriba **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="573eb-133">In the search box, type **Dropbox for Business**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="573eb-135">En el panel de resultados, seleccione **Dropbox for Business** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="573eb-135">In the results panel, select **Dropbox for Business**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="573eb-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="573eb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="573eb-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con Dropbox for Business con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="573eb-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="573eb-139">Para que el inicio de sesión único funcione, es preciso que Azure AD sepa cuál es el usuario homólogo de Dropbox for Business para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="573eb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span></span> <span data-ttu-id="573eb-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="573eb-140">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span></span>

<span data-ttu-id="573eb-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="573eb-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="573eb-142">Para configurar y probar el inicio de sesión único de Azure AD con Dropbox for Business, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="573eb-142">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="573eb-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="573eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="573eb-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="573eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="573eb-145">**[Crear un usuario de prueba en Dropbox for Business](#creating-a-dropbox-for-business-test-user)**: para tener un homólogo de Britta Simon en Dropbox for Business que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="573eb-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="573eb-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="573eb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="573eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="573eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="573eb-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="573eb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="573eb-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="573eb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="573eb-150">**Para configurar el inicio de sesión único de Azure AD con Dropbox for Business, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="573eb-150">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="573eb-151">En la página de integración de la aplicación **Dropbox for Business** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="573eb-151">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="573eb-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="573eb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="573eb-155">En la sección de **dominio y direcciones URL de Dropbox for Business**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="573eb-155">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span></span>

    <span data-ttu-id="573eb-156">a.</span><span class="sxs-lookup"><span data-stu-id="573eb-156">a.</span></span> <span data-ttu-id="573eb-157">Inicie sesión en el inquilino de Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="573eb-157">Sign on to your Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="573eb-158">![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="573eb-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="573eb-159">b.</span><span class="sxs-lookup"><span data-stu-id="573eb-159">b.</span></span> <span data-ttu-id="573eb-160">En el panel de navegación de la izquierda, haga clic en **Admin Console**(Consola de administración).</span><span class="sxs-lookup"><span data-stu-id="573eb-160">In the navigation pane on the left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="573eb-161">![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="573eb-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="573eb-162">c.</span><span class="sxs-lookup"><span data-stu-id="573eb-162">c.</span></span> <span data-ttu-id="573eb-163">En la **Admin Console** (Consola de administración), haga clic en la opción **Authentication** (Autenticación) del panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="573eb-163">On the **Admin Console**, click **Authentication** in the left navigation pane.</span></span> 
   
    <span data-ttu-id="573eb-164">![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="573eb-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="573eb-165">d.</span><span class="sxs-lookup"><span data-stu-id="573eb-165">d.</span></span> <span data-ttu-id="573eb-166">En la sección **Single sign-on** (Inicio de sesión único), seleccione **Enable single sign-on** (Habilitar inicio de sesión único) y haga clic en **More** (Más) para expandir esta sección.</span><span class="sxs-lookup"><span data-stu-id="573eb-166">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span></span>  
   
    <span data-ttu-id="573eb-167">![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="573eb-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="573eb-168">e.</span><span class="sxs-lookup"><span data-stu-id="573eb-168">e.</span></span> <span data-ttu-id="573eb-169">Copie la dirección URL que aparece al lado de **Users can sign in by entering their email address or they can go directly to**(Los usuarios pueden iniciar sesión especificando su dirección de correo electrónico o pueden ir directamente a).</span><span class="sxs-lookup"><span data-stu-id="573eb-169">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="573eb-171">f.</span><span class="sxs-lookup"><span data-stu-id="573eb-171">f.</span></span> <span data-ttu-id="573eb-172">En Azure Portal, en el cuadro de texto **Dirección URL de inicio de sesión**, pegue la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="573eb-172">On the Azure portal, in the **Sign-on URL** textbox, paste the URL.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="573eb-174">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://www.dropbox.com/sso/<id>`.</span><span class="sxs-lookup"><span data-stu-id="573eb-174">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="573eb-175">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="573eb-175">This value is not real value.</span></span> <span data-ttu-id="573eb-176">Actualice el valor con la dirección URL de inicio de sesión real que obtiene de la sección Inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="573eb-176">Update the value with the actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="573eb-177">Póngase en contacto con el [equipo de atención al cliente de Dropbox for Business](https://www.dropbox.com/business/contact) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="573eb-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="573eb-178">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="573eb-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="573eb-180">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="573eb-180">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="573eb-182">En la sección **Configuración de Dropbox for Business**, haga clic en **Configure Dropbox for Business** (Configurar Dropbox for Business) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="573eb-182">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span></span> <span data-ttu-id="573eb-183">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="573eb-183">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="573eb-185">Para configurar el inicio de sesión único en **Dropbox for Business**, vaya al inquilino de Dropbox for Business, en la sección **Inicio de sesión único** de la página **Autenticación**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="573eb-185">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span></span> 
   
    <span data-ttu-id="573eb-186">![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="573eb-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="573eb-187">a.</span><span class="sxs-lookup"><span data-stu-id="573eb-187">a.</span></span> <span data-ttu-id="573eb-188">Haga clic en **Required**(Obligatorio).</span><span class="sxs-lookup"><span data-stu-id="573eb-188">Click **Required**.</span></span>
   
    <span data-ttu-id="573eb-189">b.</span><span class="sxs-lookup"><span data-stu-id="573eb-189">b.</span></span> <span data-ttu-id="573eb-190">En la ventana **Configurar inicio de sesión único** de Azure Portal, copie el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) y péguelo en el cuadro de texto **Dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="573eb-190">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="573eb-191">c.</span><span class="sxs-lookup"><span data-stu-id="573eb-191">c.</span></span> <span data-ttu-id="573eb-192">Haga clic en **Elegir certificado** y vaya a su **archivo de certificado codificado en Base 64**.</span><span class="sxs-lookup"><span data-stu-id="573eb-192">Click **Choose certificate**, and then browse to your **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="573eb-193">d.</span><span class="sxs-lookup"><span data-stu-id="573eb-193">d.</span></span> <span data-ttu-id="573eb-194">Haga clic en **Guardar cambios** para completar la configuración en el inquilino de DropBox for Business.</span><span class="sxs-lookup"><span data-stu-id="573eb-194">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="573eb-195">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="573eb-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="573eb-196">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="573eb-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="573eb-197">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="573eb-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="573eb-198">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="573eb-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="573eb-199">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="573eb-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="573eb-201">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="573eb-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="573eb-202">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="573eb-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="573eb-204">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="573eb-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="573eb-206">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="573eb-206">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="573eb-208">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="573eb-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="573eb-210">a.</span><span class="sxs-lookup"><span data-stu-id="573eb-210">a.</span></span> <span data-ttu-id="573eb-211">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="573eb-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="573eb-212">b.</span><span class="sxs-lookup"><span data-stu-id="573eb-212">b.</span></span> <span data-ttu-id="573eb-213">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="573eb-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="573eb-214">c.</span><span class="sxs-lookup"><span data-stu-id="573eb-214">c.</span></span> <span data-ttu-id="573eb-215">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="573eb-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="573eb-216">d.</span><span class="sxs-lookup"><span data-stu-id="573eb-216">d.</span></span> <span data-ttu-id="573eb-217">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="573eb-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="573eb-218">Creación de un usuario de prueba de Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="573eb-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="573eb-219">En esta sección, creará un usuario llamado a Britta Simon en Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="573eb-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="573eb-220">Dropbox for Business admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="573eb-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="573eb-221">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="573eb-221">There is no action item for you in this section.</span></span> <span data-ttu-id="573eb-222">Si un usuario ya no existe en Dropbox for Business, se crea uno nuevo cuando se intenta acceder a esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="573eb-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="573eb-223">Si necesita crear un usuario de forma manual, póngase en contacto con el [equipo de soporte de cliente de Dropbox for Business](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="573eb-223">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="573eb-224">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="573eb-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="573eb-225">En esta sección, concederá acceso a Britta Simon a Dropbox for Business para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="573eb-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="573eb-227">**Siga estos pasos para asignar Britta Simon a Dropbox for Business:**</span><span class="sxs-lookup"><span data-stu-id="573eb-227">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="573eb-228">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="573eb-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="573eb-230">En la lista de aplicaciones, seleccione **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="573eb-230">In the applications list, select **Dropbox for Business**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="573eb-232">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="573eb-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="573eb-234">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="573eb-234">Click **Add** button.</span></span> <span data-ttu-id="573eb-235">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="573eb-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="573eb-237">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="573eb-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="573eb-238">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="573eb-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="573eb-239">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="573eb-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="573eb-240">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="573eb-240">Testing single sign-on</span></span>

<span data-ttu-id="573eb-241">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="573eb-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="573eb-242">Al hacer clic en el icono Dropbox for Business en el Panel de acceso, debe ir a la página de inicio de sesión de la aplicación Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="573eb-242">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="573eb-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="573eb-243">Additional resources</span></span>

* [<span data-ttu-id="573eb-244">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="573eb-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="573eb-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="573eb-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="573eb-246">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="573eb-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

