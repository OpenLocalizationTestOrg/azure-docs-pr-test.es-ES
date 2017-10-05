---
title: "Tutorial: Integración de Azure Active Directory con BenSelect | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y BenSelect."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: f8caa023da05863372b7ef92b47a92168445d741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="31069-103">Tutorial: Integración de Azure Active Directory con BenSelect</span><span class="sxs-lookup"><span data-stu-id="31069-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="31069-104">En este tutorial, obtendrá información sobre cómo integrar BenSelect con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31069-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31069-105">La integración de BenSelect con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="31069-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31069-106">Puede controlar en Azure AD quién tiene acceso a BenSelect.</span><span class="sxs-lookup"><span data-stu-id="31069-106">You can control in Azure AD who has access to BenSelect</span></span>
- <span data-ttu-id="31069-107">Puede permitir que los usuarios inicien sesión automáticamente en BenSelect (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31069-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31069-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="31069-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="31069-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31069-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31069-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="31069-110">Prerequisites</span></span>

<span data-ttu-id="31069-111">Para configurar la integración de Azure AD con BenSelect, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="31069-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

- <span data-ttu-id="31069-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31069-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31069-113">Una suscripción habilitada para el inicio de sesión único en BenSelect</span><span class="sxs-lookup"><span data-stu-id="31069-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31069-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="31069-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31069-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="31069-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31069-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="31069-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31069-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31069-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31069-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="31069-118">Scenario description</span></span>
<span data-ttu-id="31069-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="31069-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31069-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="31069-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31069-121">Adición de BenSelect desde la galería</span><span class="sxs-lookup"><span data-stu-id="31069-121">Adding BenSelect from the gallery</span></span>
2. <span data-ttu-id="31069-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31069-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="31069-123">Adición de BenSelect desde la galería</span><span class="sxs-lookup"><span data-stu-id="31069-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="31069-124">Para configurar la integración de BenSelect en Azure AD, es preciso agregar BenSelect desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="31069-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31069-125">**Para agregar BenSelect desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="31069-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31069-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31069-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31069-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="31069-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31069-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31069-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="31069-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31069-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="31069-133">En el cuadro de búsqueda, escriba **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="31069-133">In the search box, type **BenSelect**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="31069-135">En el panel de resultados, seleccione **BenSelect** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31069-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31069-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31069-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31069-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con BenSelect con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="31069-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="31069-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de BenSelect para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31069-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="31069-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de BenSelect.</span><span class="sxs-lookup"><span data-stu-id="31069-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="31069-141">Para establecer la relación de vínculo, en BenSelect, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="31069-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="31069-142">Para configurar y probar el inicio de sesión único de Azure AD con BenSelect, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="31069-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31069-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="31069-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="31069-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31069-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31069-145">**[Creación de un usuario de prueba de BenSelect](#creating-a-benselect-test-user)**: para tener un homólogo de Britta Simon en BenSelect vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31069-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="31069-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31069-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31069-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="31069-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31069-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31069-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31069-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación BenSelect.</span><span class="sxs-lookup"><span data-stu-id="31069-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="31069-150">**Para configurar el inicio de sesión único de Azure AD con BenSelect, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="31069-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="31069-151">En Azure Portal, en la página de integración de la aplicación **BenSelect**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="31069-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="31069-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="31069-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="31069-155">En la sección **Dominio y direcciones URL de BenSelect**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="31069-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="31069-157">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`.</span><span class="sxs-lookup"><span data-stu-id="31069-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="31069-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="31069-158">This value is not real.</span></span> <span data-ttu-id="31069-159">Actualice este valor con la dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="31069-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="31069-160">Póngase en contacto con el [equipo de soporte técnico de BenSelect](mailto:support@selerix.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="31069-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span></span>
 
4. <span data-ttu-id="31069-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="31069-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="31069-163">La aplicación BenSelect espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="31069-163">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="31069-164">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="31069-164">Configure the following claims for this application.</span></span> <span data-ttu-id="31069-165">Puede administrar los valores de estos atributos en la sección **Atributos de usuario** de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="31069-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="31069-166">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="31069-166">The following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="31069-168">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**:</span><span class="sxs-lookup"><span data-stu-id="31069-168">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="31069-169">a.</span><span class="sxs-lookup"><span data-stu-id="31069-169">a.</span></span> <span data-ttu-id="31069-170">En la lista desplegable **Identificador de usuario**, seleccione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="31069-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="31069-171">b.</span><span class="sxs-lookup"><span data-stu-id="31069-171">b.</span></span> <span data-ttu-id="31069-172">En la lista desplegable **Correo**, seleccione **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="31069-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="31069-173">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="31069-173">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="31069-175">En la sección **Configuración de BenSelect**, haga clic en **Configurar BenSelect** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="31069-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span></span> <span data-ttu-id="31069-176">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="31069-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="31069-178">Para configurar el inicio de sesión único en **BenSelect**, es preciso enviar los valores descargados de **Certificado (sin procesar)**, **Sign-Out URL (Dirección URL de cierre de sesión), SAML Entity ID (Identificador de entidad de SAML) y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de BenSelect ](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="31069-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="31069-179">Debe mencionar que esta integración requiere el algoritmo SHA256 (no se admite SHA1) para establecer el SSO en el servidor apropiado, como app2101.</span><span class="sxs-lookup"><span data-stu-id="31069-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="31069-180">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31069-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="31069-181">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="31069-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="31069-182">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31069-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31069-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31069-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="31069-184">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="31069-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="31069-186">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="31069-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31069-187">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31069-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31069-189">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="31069-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31069-191">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31069-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31069-193">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="31069-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31069-195">a.</span><span class="sxs-lookup"><span data-stu-id="31069-195">a.</span></span> <span data-ttu-id="31069-196">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31069-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31069-197">b.</span><span class="sxs-lookup"><span data-stu-id="31069-197">b.</span></span> <span data-ttu-id="31069-198">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31069-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31069-199">c.</span><span class="sxs-lookup"><span data-stu-id="31069-199">c.</span></span> <span data-ttu-id="31069-200">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="31069-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="31069-201">d.</span><span class="sxs-lookup"><span data-stu-id="31069-201">d.</span></span> <span data-ttu-id="31069-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="31069-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="31069-203">Creación de un usuario de prueba de BenSelect</span><span class="sxs-lookup"><span data-stu-id="31069-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="31069-204">El objetivo de esta sección es crear un usuario llamado Britta Simon en BenSelect.</span><span class="sxs-lookup"><span data-stu-id="31069-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="31069-205">Trabaje con el [equipo de soporte técnico de BenSelect](mailto:support@selerix.com) para agregar los usuarios en la cuenta de BenSelect.</span><span class="sxs-lookup"><span data-stu-id="31069-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="31069-206">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31069-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="31069-207">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a BenSelect.</span><span class="sxs-lookup"><span data-stu-id="31069-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="31069-209">**Para asignar Britta Simon a BenSelect, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="31069-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="31069-210">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31069-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="31069-212">En la lista de aplicaciones, seleccione **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="31069-212">In the applications list, select **BenSelect**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="31069-214">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="31069-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="31069-216">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="31069-216">Click **Add** button.</span></span> <span data-ttu-id="31069-217">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="31069-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="31069-219">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="31069-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="31069-220">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="31069-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31069-221">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="31069-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31069-222">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="31069-222">Testing single sign-on</span></span>

<span data-ttu-id="31069-223">En esta sección, probará la configuración de SSO de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="31069-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="31069-224">Al hacer clic en el icono de BenSelect en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación BenSelect.</span><span class="sxs-lookup"><span data-stu-id="31069-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31069-225">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="31069-225">Additional resources</span></span>

* [<span data-ttu-id="31069-226">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31069-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31069-227">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31069-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

