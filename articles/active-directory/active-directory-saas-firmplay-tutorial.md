---
title: "Tutorial: Integración de Azure Active Directory con FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y FirmPlay - Employee Advocacy for Recruiting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3cddd5b9508159089bf344dbb3882d462799747c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="0f81b-103">Tutorial: Integración de Azure Active Directory con FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="0f81b-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="0f81b-104">En este tutorial, aprenderá a integrar FirmPlay - Employee Advocacy for Recruiting con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0f81b-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0f81b-105">La integración de FirmPlay - Employee Advocacy for Recruiting con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0f81b-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0f81b-106">Puede controlar en Azure AD que tenga acceso a FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="0f81b-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="0f81b-107">Puede permitir que los usuarios inicien sesión automáticamente en FirmPlay - Employee Advocacy for Recruiting (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f81b-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0f81b-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f81b-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="0f81b-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0f81b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f81b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0f81b-110">Prerequisites</span></span>

<span data-ttu-id="0f81b-111">Para configurar la integración de Azure AD con FirmPlay - Employee Advocacy for Recruiting, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0f81b-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="0f81b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f81b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0f81b-113">Una suscripción habilitada para inicio de sesión única de FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="0f81b-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="0f81b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0f81b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="0f81b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0f81b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f81b-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0f81b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0f81b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f81b-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="0f81b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0f81b-118">Scenario description</span></span>
<span data-ttu-id="0f81b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0f81b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0f81b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="0f81b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0f81b-121">Adición de FirmPlay - Employee Advocacy for Recruiting desde la galería</span><span class="sxs-lookup"><span data-stu-id="0f81b-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
2. <span data-ttu-id="0f81b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f81b-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="0f81b-123">Adición de FirmPlay - Employee Advocacy for Recruiting desde la galería</span><span class="sxs-lookup"><span data-stu-id="0f81b-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="0f81b-124">Para configurar la integración de FirmPlay - Employee Advocacy for Recruiting en Azure AD, debe agregar FirmPlay - Employee Advocacy for Recruiting de la galería a la lista de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0f81b-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0f81b-125">**Para agregar FirmPlay - Employee Advocacy for Recruiting desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0f81b-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0f81b-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0f81b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0f81b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0f81b-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0f81b-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0f81b-133">En el cuadro de búsqueda, escriba **FirmPlay - Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="0f81b-135">En el panel de resultados, seleccione **FirmPlay - Employee Advocacy for Recruiting** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0f81b-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0f81b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f81b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0f81b-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con FirmPlay - Employee Advocacy for Recruiting utilizando usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0f81b-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0f81b-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de FirmPlay - Employee Advocacy for Recruiting para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f81b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="0f81b-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="0f81b-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="0f81b-141">Esta relación de vínculo se establece asignando el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="0f81b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="0f81b-142">Para configurar y probar el inicio de sesión único de Azure AD con FirmPlay - Employee Advocacy for Recruiting, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0f81b-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0f81b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="0f81b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0f81b-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0f81b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0f81b-145">**[Creación de un usuario de prueba de FirmPlay - Employee Advocacy for Recruiting](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**: para tener un equivalente de Britta Simon en FirmPlay - Employee Advocacy for Recruiting que esté vinculado a la representación de Azure AD de ese usuario.</span><span class="sxs-lookup"><span data-stu-id="0f81b-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="0f81b-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f81b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0f81b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0f81b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0f81b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f81b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0f81b-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="0f81b-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="0f81b-150">**Para configurar el inicio de sesión único de Azure AD con FirmPlay - Employee Advocacy for Recruiting, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0f81b-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="0f81b-151">En el Portal de administración de Azure, en la página de integración de la aplicación **FirmPlay - Employee Advocacy for Recruiting**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0f81b-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0f81b-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="0f81b-155">En la sección **Dominio y direcciones URL de FirmPlay - Employee Advocacy for Recruiting**, en el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL usando el patrón siguiente: `https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="0f81b-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="0f81b-157">Tenga en cuenta que este no es el valor real.</span><span class="sxs-lookup"><span data-stu-id="0f81b-157">Please note that this is not the real value.</span></span> <span data-ttu-id="0f81b-158">Tiene que actualizar este valor con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="0f81b-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="0f81b-159">Póngase en contacto con [FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="0f81b-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

4. <span data-ttu-id="0f81b-160">En la sección **Certificado de firma de SAML**, haga clic en **Crear nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="0f81b-162">En el cuadro de diálogo **Crear nuevo certificado**, haga clic en el icono del calendario y seleccione una valor en **Fecha de expiración**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="0f81b-163">Luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-163">Then click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="0f81b-165">En la sección **Certificado de firma de SAML**, seleccione **Make new certificate active** (Activar el nuevo certificado) y haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="0f81b-167">En la ventana emergente **Rollover certificate** (Certificado de sustitución), haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0f81b-169">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0f81b-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="0f81b-171">En la sección **FirmPlay - Employee Advocacy for Recruiting**, haga clic en **Configurar FirmPlay - Employee Advocacy for Recruiting** para abrir el cuadro de diálogo **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="0f81b-174">Para configurar el inicio de sesión único para su aplicación, póngase en contacto con el equipo de soporte técnico de [FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) y proporcione lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0f81b-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="0f81b-175">• El **archivo de certificado** descargado</span><span class="sxs-lookup"><span data-stu-id="0f81b-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="0f81b-176">• La **dirección URL de servicio de inicio de sesión único de SAML**</span><span class="sxs-lookup"><span data-stu-id="0f81b-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="0f81b-177">• El **identificador de entidad de SAML**</span><span class="sxs-lookup"><span data-stu-id="0f81b-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="0f81b-178">• La **dirección URL de cierre de sesión**</span><span class="sxs-lookup"><span data-stu-id="0f81b-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0f81b-179">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f81b-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="0f81b-180">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0f81b-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0f81b-182">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="0f81b-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0f81b-183">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0f81b-185">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0f81b-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0f81b-187">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0f81b-189">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0f81b-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0f81b-191">a.</span><span class="sxs-lookup"><span data-stu-id="0f81b-191">a.</span></span> <span data-ttu-id="0f81b-192">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0f81b-193">b.</span><span class="sxs-lookup"><span data-stu-id="0f81b-193">b.</span></span> <span data-ttu-id="0f81b-194">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0f81b-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0f81b-195">c.</span><span class="sxs-lookup"><span data-stu-id="0f81b-195">c.</span></span> <span data-ttu-id="0f81b-196">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0f81b-197">d.</span><span class="sxs-lookup"><span data-stu-id="0f81b-197">d.</span></span> <span data-ttu-id="0f81b-198">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="0f81b-199">Creación de un usuario de prueba de FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="0f81b-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="0f81b-200">En esta sección, creará un usuario llamado a Britta Simon en FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="0f81b-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="0f81b-201">Trabaje con [FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) para agregar usuarios a la plataforma FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="0f81b-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0f81b-202">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f81b-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0f81b-203">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="0f81b-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0f81b-205">**Para asignar a Britta Simon a FirmPlay - Employee Advocacy for Recruiting desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0f81b-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="0f81b-206">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y seleccione **Aplicaciones empresariales**. Después, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0f81b-208">En la lista de aplicaciones, seleccione **FirmPlay - Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="0f81b-210">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0f81b-212">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-212">Click **Add** button.</span></span> <span data-ttu-id="0f81b-213">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0f81b-215">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0f81b-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0f81b-216">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0f81b-217">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0f81b-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="0f81b-218">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0f81b-218">Testing single sign-on</span></span>

<span data-ttu-id="0f81b-219">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0f81b-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0f81b-220">Al hacer clic en el icono de FirmPlay - Employee Advocacy for Recruiting en el Panel de acceso, debe iniciar sesión automáticamente en FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="0f81b-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0f81b-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0f81b-221">Additional resources</span></span>

* [<span data-ttu-id="0f81b-222">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f81b-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f81b-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0f81b-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png