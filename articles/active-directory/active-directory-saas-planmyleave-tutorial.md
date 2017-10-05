---
title: "Tutorial: integración de Azure Active Directory con PlanMyLeave | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="80687-103">Tutorial: Integración de Azure Active Directory con PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="80687-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="80687-104">En este tutorial, obtendrá información sobre cómo integrar PlanMyLeave con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80687-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80687-105">Integrar PlanMyLeave con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="80687-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="80687-106">Puede controlar en Azure AD quién tiene acceso a PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="80687-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="80687-107">Puede permitir que los usuarios inicien sesión automáticamente en PlanMyLeave (inicio de sesión único) con las cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80687-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="80687-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="80687-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="80687-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80687-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80687-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="80687-110">Prerequisites</span></span>

<span data-ttu-id="80687-111">Para configurar la integración de Azure AD con PlanMyLeave, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="80687-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="80687-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80687-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80687-113">Una suscripción habilitada para el inicio de sesión único en PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="80687-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="80687-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="80687-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="80687-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="80687-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80687-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="80687-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="80687-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80687-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="80687-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="80687-118">Scenario description</span></span>
<span data-ttu-id="80687-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="80687-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80687-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="80687-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80687-121">Agregar PlanMyLeave desde la galería</span><span class="sxs-lookup"><span data-stu-id="80687-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="80687-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80687-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="80687-123">Agregar PlanMyLeave desde la galería</span><span class="sxs-lookup"><span data-stu-id="80687-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="80687-124">Para configurar la integración de PlanMyLeave en Azure AD, deberá agregar PlanMyLeave desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="80687-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="80687-125">**Para agregar PlanMyLeave desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="80687-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="80687-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80687-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="80687-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="80687-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="80687-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="80687-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="80687-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80687-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="80687-133">En el cuadro de búsqueda, escriba **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="80687-133">In the search box, type **PlanMyLeave**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="80687-135">En el panel de resultados, seleccione **PlanMyLeave** y, después, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="80687-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="80687-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80687-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="80687-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con PlanMyLeave con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="80687-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="80687-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de PlanMyLeave para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80687-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="80687-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="80687-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="80687-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="80687-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="80687-142">Para configurar y probar el inicio de sesión único de Azure AD con PlanMyLeave, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="80687-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="80687-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="80687-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="80687-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80687-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80687-145">**[Creación de un usuario de prueba para PlanMyLeave](#creating-a-planmyleave-test-user)** : para tener un homólogo de Britta Simon en PlanMyLeave que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80687-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="80687-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80687-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80687-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="80687-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="80687-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80687-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="80687-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="80687-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="80687-150">**Para configurar el inicio de sesión único de Azure AD con PlanMyLeave, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="80687-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="80687-151">En el Portal de administración de Azure, en la página de integración de la aplicación **PlanMyLeave**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="80687-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="80687-153">En la página de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="80687-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="80687-155">En la sección **Dominio y direcciones URL de PlanMyLeave**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="80687-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="80687-157">a.</span><span class="sxs-lookup"><span data-stu-id="80687-157">a.</span></span> <span data-ttu-id="80687-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company-name>.planmyleave.com/Login.aspx`.</span><span class="sxs-lookup"><span data-stu-id="80687-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="80687-159">b.</span><span class="sxs-lookup"><span data-stu-id="80687-159">b.</span></span> <span data-ttu-id="80687-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<company-name>.planmyleave.com`.</span><span class="sxs-lookup"><span data-stu-id="80687-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="80687-161">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="80687-161">Please note that these are not the real values.</span></span> <span data-ttu-id="80687-162">Tendrá que actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="80687-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="80687-163">Póngase en contacto con el [equipo de soporte técnico de PlanMyLeave](mailto:support@planmyleave.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="80687-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="80687-164">En la sección **Certificado de firma de SAML**, haga clic en **Crear nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="80687-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="80687-166">En el cuadro de diálogo **Crear nuevo certificado**, haga clic en el icono del calendario y seleccione una valor en **Fecha de expiración**.</span><span class="sxs-lookup"><span data-stu-id="80687-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="80687-167">Luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="80687-167">Then click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="80687-169">En la sección **Certificado de firma de SAML**, seleccione **Make new certificate active** (Activar el nuevo certificado) y haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="80687-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="80687-171">En la ventana emergente **Rollover certificate** (Certificado de sustitución), haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="80687-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="80687-173">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="80687-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="80687-175">En la sección **Configuración de PlanMyLeave**, haga clic en **Configurar PlanMyLeave** para abrir la ventana **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="80687-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="80687-178">En otra ventana del explorador web, inicie sesión en como administrador en el inquilino de PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="80687-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="80687-179">Vaya a **Configuración del sistema**.</span><span class="sxs-lookup"><span data-stu-id="80687-179">Go to **System Setup**.</span></span> <span data-ttu-id="80687-180">Después, en la sección **Administración de seguridad**, haga clic en **Company SAML settings** (Configuración de SAML de la empresa).</span><span class="sxs-lookup"><span data-stu-id="80687-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="80687-182">En la sección **SAML Settings** (Configuración de SAML), haga clic en el icono del editor.</span><span class="sxs-lookup"><span data-stu-id="80687-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="80687-184">En la sección **Update SAML Settings** (Actualizar configuración de SAML), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="80687-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="80687-186">a.</span><span class="sxs-lookup"><span data-stu-id="80687-186">a.</span></span>  <span data-ttu-id="80687-187">En el cuadro de texto **URL de inicio de sesión**, coloque el valor de **Dirección URL del servicio de inicio de sesión único** en la ventana de configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80687-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="80687-188">b.</span><span class="sxs-lookup"><span data-stu-id="80687-188">b.</span></span>  <span data-ttu-id="80687-189">Abra el archivo de certificado descargado en el bloc de notas, copie solo el contenido comprendido entre ---Begin Certificate--- y ---End certificate---- en el portapapeles y, después, péguelo en el cuadro de texto **Certificado**.</span><span class="sxs-lookup"><span data-stu-id="80687-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="80687-190">c.</span><span class="sxs-lookup"><span data-stu-id="80687-190">c.</span></span> <span data-ttu-id="80687-191">Establezca "**Is Enable**" en "**Yes**".</span><span class="sxs-lookup"><span data-stu-id="80687-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="80687-192">d.</span><span class="sxs-lookup"><span data-stu-id="80687-192">d.</span></span> <span data-ttu-id="80687-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="80687-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="80687-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80687-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="80687-195">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80687-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="80687-197">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="80687-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="80687-198">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80687-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80687-200">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="80687-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="80687-202">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="80687-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80687-204">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="80687-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80687-206">a.</span><span class="sxs-lookup"><span data-stu-id="80687-206">a.</span></span> <span data-ttu-id="80687-207">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80687-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80687-208">b.</span><span class="sxs-lookup"><span data-stu-id="80687-208">b.</span></span> <span data-ttu-id="80687-209">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80687-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="80687-210">c.</span><span class="sxs-lookup"><span data-stu-id="80687-210">c.</span></span> <span data-ttu-id="80687-211">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="80687-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="80687-212">d.</span><span class="sxs-lookup"><span data-stu-id="80687-212">d.</span></span> <span data-ttu-id="80687-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="80687-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="80687-214">Crear un usuario de prueba de PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="80687-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="80687-215">El objetivo de esta sección es crear un usuario llamado Britta Simon en PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="80687-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="80687-216">PlanMyLeave admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="80687-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="80687-217">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="80687-217">There is no action item for you in this section.</span></span> <span data-ttu-id="80687-218">Durante un intento de acceder a PlanMyLeave se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="80687-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="80687-219">Si necesita crear manualmente un usuario, es preciso que se ponga contacto con el [equipo de soporte técnico de PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="80687-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="80687-220">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80687-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="80687-221">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="80687-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="80687-223">**Para asignar a Britta Simon a PlanMyLeave, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="80687-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="80687-224">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y seleccione **Aplicaciones empresariales**. Después, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="80687-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="80687-226">En la lista de aplicaciones, seleccione **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="80687-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="80687-228">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="80687-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="80687-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="80687-230">Click **Add** button.</span></span> <span data-ttu-id="80687-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="80687-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="80687-233">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="80687-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="80687-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="80687-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80687-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="80687-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="80687-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="80687-236">Testing single sign-on</span></span>

<span data-ttu-id="80687-237">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="80687-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="80687-238">Al hacer clic en el icono de PlanMyLeave en el panel de acceso, debería iniciar sesión automáticamente en la aplicación de PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="80687-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="80687-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="80687-239">Additional resources</span></span>

* [<span data-ttu-id="80687-240">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80687-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80687-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80687-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png