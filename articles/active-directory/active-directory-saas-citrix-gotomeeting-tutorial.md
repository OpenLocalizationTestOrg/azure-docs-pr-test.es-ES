---
title: "Tutorial: Integración de Azure Active Directory con Citrix GoToMeeting | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: c1ac144c4fa43312ec26fce03cd0ee1bfcf73d4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="576f8-103">Tutorial: Integración de Azure Active Directory con Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="576f8-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="576f8-104">En este tutorial, aprenderá a integrar Citrix GoToMeeting con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="576f8-104">In this tutorial, you learn how to integrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="576f8-105">La integración de Citrix GoToMeeting con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="576f8-105">Integrating Citrix GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="576f8-106">Puede controlar en Azure AD quién tiene acceso a Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="576f8-106">You can control in Azure AD who has access to Citrix GoToMeeting</span></span>
- <span data-ttu-id="576f8-107">Puede permitir que los usuarios inicien sesión automáticamente en Citrix GoToMeeting (Inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="576f8-107">You can enable your users to automatically get signed-on to Citrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="576f8-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="576f8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="576f8-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="576f8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="576f8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="576f8-110">Prerequisites</span></span>

<span data-ttu-id="576f8-111">Para configurar la integración de Azure AD con Citrix GoToMeeting, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="576f8-111">To configure Azure AD integration with Citrix GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="576f8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="576f8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="576f8-113">Una suscripción habilitada para el inicio de sesión único en Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="576f8-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="576f8-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="576f8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="576f8-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="576f8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="576f8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="576f8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="576f8-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="576f8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="576f8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="576f8-118">Scenario description</span></span>
<span data-ttu-id="576f8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="576f8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="576f8-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="576f8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="576f8-121">Adición de Citrix GoToMeeting desde la galería</span><span class="sxs-lookup"><span data-stu-id="576f8-121">Adding Citrix GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="576f8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="576f8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-the-gallery"></a><span data-ttu-id="576f8-123">Adición de Citrix GoToMeeting desde la galería</span><span class="sxs-lookup"><span data-stu-id="576f8-123">Adding Citrix GoToMeeting from the gallery</span></span>
<span data-ttu-id="576f8-124">Para configurar la integración de Citrix GoToMeeting en Azure AD, deberá agregar Citrix GoToMeeting desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="576f8-124">To configure the integration of Citrix GoToMeeting into Azure AD, you need to add Citrix GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="576f8-125">**Para agregar Citrix GoToMeeting desde la galería, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="576f8-125">**To add Citrix GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="576f8-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="576f8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="576f8-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="576f8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="576f8-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="576f8-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="576f8-131">Haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="576f8-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="576f8-133">En el cuadro de búsqueda, escriba **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="576f8-133">In the search box, type **Citrix GoToMeeting**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="576f8-135">En el panel de resultados, seleccione **Citrix GoToMeeting** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="576f8-135">In the results panel, select **Citrix GoToMeeting**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="576f8-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="576f8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="576f8-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Citrix GoToMeeting con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="576f8-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="576f8-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo en Citrix GoToMeeting de un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="576f8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="576f8-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="576f8-140">In other words, a link relationship between an Azure AD user and the related user in Citrix GoToMeeting needs to be established.</span></span>

<span data-ttu-id="576f8-141">Esta relación de vínculo se establece asignando el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="576f8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="576f8-142">Para configurar y probar el inicio de sesión único de Azure AD con Citrix GoToMeeting, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="576f8-142">To configure and test Azure AD single sign-on with Citrix GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="576f8-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="576f8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="576f8-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="576f8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="576f8-145">**[Creación de un usuario de prueba de Citrix GoToMeeting ](#creating-a-citrix-gotomeeting-test-user)**: para tener un homólogo de Britta Simon en Citrix GoToMeeting que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="576f8-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - to have a counterpart of Britta Simon in Citrix GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="576f8-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="576f8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="576f8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="576f8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="576f8-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="576f8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="576f8-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="576f8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="576f8-150">**Para configurar el inicio de sesión único de Azure AD con Citrix GoToMeeting, realice los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="576f8-150">**To configure Azure AD single sign-on with Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="576f8-151">En la página de integración de la aplicación **Citrix GoToMeeting** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="576f8-151">In the Azure portal, on the **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="576f8-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="576f8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="576f8-155">En la sección **Citrix GoToMeeting Domain and URLs** (Dominio y direcciones URL de Citrix GoToMeeting), no tienen que realizar ningún paso.</span><span class="sxs-lookup"><span data-stu-id="576f8-155">On the **Citrix GoToMeeting Domain and URLs** section, no need to perform any steps.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="576f8-157">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="576f8-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="576f8-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="576f8-159">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="576f8-161">En la sección Citrix GoToMeeting SAML Configuration (Configuración de Citrix GoToMeeting), haga clic en Configure Citrix GoToMeeting SAML (Configurar Citrix GoToMeeting SAML) para abrir la ventana Configurar inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="576f8-161">On the Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML to open Configure sign-on window.</span></span> <span data-ttu-id="576f8-162">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="576f8-162">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

6. <span data-ttu-id="576f8-163">En otra ventana del explorador, inicie sesión en su [Centro de organización de Citrix](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="576f8-163">In a different browser window, log in to your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="576f8-164">Haga clic en la pestaña **Proveedor de identidades** y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="576f8-164">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="576f8-165">![Configuración de SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="576f8-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="576f8-166">a.</span><span class="sxs-lookup"><span data-stu-id="576f8-166">a.</span></span> <span data-ttu-id="576f8-167">Seleccione **Manual**</span><span class="sxs-lookup"><span data-stu-id="576f8-167">Select **Manual**</span></span>

    <span data-ttu-id="576f8-168">b.</span><span class="sxs-lookup"><span data-stu-id="576f8-168">b.</span></span> <span data-ttu-id="576f8-169">En Azure Portal, en la página de diálogo **Configurar inicio de sesión único en Citrix GoToMeeting**, copie el valor **SAML Single Sign-On Service URL** (Dirección URL de servicio de inicio de sesión único de SAML) y péguelo en el cuadro de texto **Sign-in page URL** (Dirección URL de la página de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="576f8-169">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="576f8-170">c.</span><span class="sxs-lookup"><span data-stu-id="576f8-170">c.</span></span> <span data-ttu-id="576f8-171">En el Azure portal, en la página de diálogo **Configurar inicio de sesión único en Citrix GoToMeeting**, copie el valor **Sign-Out URL** (Dirección URL de cierre de sesión) y péguelo en el cuadro de texto **Sign-out Page URL** (Dirección URL de la página de cierre de sesión).</span><span class="sxs-lookup"><span data-stu-id="576f8-171">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="576f8-172">d.</span><span class="sxs-lookup"><span data-stu-id="576f8-172">d.</span></span> <span data-ttu-id="576f8-173">En Azure Portal, en la página de diálogo **Configurar inicio de sesión único en Citrix GoToMeeting**, copie el valor del **identificador de identidad de SAML** y péguelo en el cuadro de texto **Identity Provider Entity ID** (Id. de entidad del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="576f8-173">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="576f8-174">e.</span><span class="sxs-lookup"><span data-stu-id="576f8-174">e.</span></span> <span data-ttu-id="576f8-175">Para cargar el certificado descargado, haga clic en **Cargar certificado**.</span><span class="sxs-lookup"><span data-stu-id="576f8-175">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="576f8-176">f.</span><span class="sxs-lookup"><span data-stu-id="576f8-176">f.</span></span> <span data-ttu-id="576f8-177">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="576f8-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="576f8-178">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="576f8-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="576f8-179">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="576f8-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="576f8-180">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="576f8-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="576f8-181">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="576f8-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="576f8-182">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="576f8-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="576f8-184">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="576f8-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="576f8-185">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="576f8-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="576f8-187">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="576f8-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="576f8-189">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="576f8-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="576f8-191">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="576f8-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="576f8-193">a.</span><span class="sxs-lookup"><span data-stu-id="576f8-193">a.</span></span> <span data-ttu-id="576f8-194">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="576f8-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="576f8-195">b.</span><span class="sxs-lookup"><span data-stu-id="576f8-195">b.</span></span> <span data-ttu-id="576f8-196">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="576f8-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="576f8-197">c.</span><span class="sxs-lookup"><span data-stu-id="576f8-197">c.</span></span> <span data-ttu-id="576f8-198">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="576f8-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="576f8-199">d.</span><span class="sxs-lookup"><span data-stu-id="576f8-199">d.</span></span> <span data-ttu-id="576f8-200">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="576f8-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="576f8-201">Creación de un usuario de prueba de Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="576f8-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="576f8-202">En esta sección, creará un usuario llamado a Britta Simon en Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="576f8-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="576f8-203">Citrix GoToMeeting admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="576f8-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="576f8-204">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="576f8-204">There is no action item for you in this section.</span></span> <span data-ttu-id="576f8-205">Si el usuario no existe aún en Citrix GoToMeeting., se crea uno nuevo cuando se intenta acceder a esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="576f8-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt to access Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="576f8-206">Si necesita crear manualmente un usuario, póngase en contacto con el [equipo de soporte técnico de Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting).</span><span class="sxs-lookup"><span data-stu-id="576f8-206">If you need to create a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="576f8-207">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="576f8-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="576f8-208">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure mediante la concesión de acceso a Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="576f8-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix GoToMeeting.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="576f8-210">**Para asignar Britta Simon a Citrix GoToMeeting, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="576f8-210">**To assign Britta Simon to Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="576f8-211">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="576f8-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="576f8-213">En la lista de aplicaciones, seleccione **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="576f8-213">In the applications list, select **Citrix GoToMeeting**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="576f8-215">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="576f8-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="576f8-217">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="576f8-217">Click **Add** button.</span></span> <span data-ttu-id="576f8-218">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="576f8-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="576f8-220">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="576f8-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="576f8-221">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="576f8-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="576f8-222">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="576f8-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="576f8-223">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="576f8-223">Testing single sign-on</span></span>

<span data-ttu-id="576f8-224">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="576f8-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="576f8-225">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="576f8-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="576f8-226">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="576f8-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="576f8-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="576f8-227">Additional resources</span></span>

* [<span data-ttu-id="576f8-228">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="576f8-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="576f8-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="576f8-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="576f8-230">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="576f8-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

