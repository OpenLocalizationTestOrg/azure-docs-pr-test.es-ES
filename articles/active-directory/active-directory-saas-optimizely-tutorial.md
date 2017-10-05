---
title: "Tutorial: integración de Azure Active Directory con Optimizely | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 4d6f6da6bace09fbd6ab105530a1162653675c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="42e10-103">Tutorial: integración de Azure Active Directory con Optimizely</span><span class="sxs-lookup"><span data-stu-id="42e10-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="42e10-104">En este tutorial, obtendrá información sobre cómo integrar Optimizely con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42e10-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42e10-105">La integración de Optimizely con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="42e10-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42e10-106">Puede controlar en Azure AD quién tiene acceso a Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42e10-106">You can control in Azure AD who has access to Optimizely</span></span>
- <span data-ttu-id="42e10-107">Puede permitir que los usuarios inicien sesión automáticamente en Optimizely (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42e10-107">You can enable your users to automatically get signed-on to Optimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42e10-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="42e10-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="42e10-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42e10-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42e10-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="42e10-110">Prerequisites</span></span>

<span data-ttu-id="42e10-111">Para configurar la integración de Azure AD con Optimizely, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="42e10-111">To configure Azure AD integration with Optimizely, you need the following items:</span></span>

- <span data-ttu-id="42e10-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42e10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42e10-113">Una suscripción habilitada para el inicio de sesión único en Optimizely</span><span class="sxs-lookup"><span data-stu-id="42e10-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42e10-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="42e10-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42e10-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="42e10-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42e10-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="42e10-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42e10-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42e10-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42e10-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="42e10-118">Scenario description</span></span>
<span data-ttu-id="42e10-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="42e10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42e10-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="42e10-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42e10-121">Adición de Optimizely desde la galería</span><span class="sxs-lookup"><span data-stu-id="42e10-121">Adding Optimizely from the gallery</span></span>
2. <span data-ttu-id="42e10-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42e10-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-the-gallery"></a><span data-ttu-id="42e10-123">Adición de Optimizely desde la galería</span><span class="sxs-lookup"><span data-stu-id="42e10-123">Adding Optimizely from the gallery</span></span>
<span data-ttu-id="42e10-124">Para configurar la integración de Optimizely en Azure AD, es preciso agregar Optimizely desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="42e10-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42e10-125">**Para agregar Optimizely desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="42e10-125">**To add Optimizely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42e10-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42e10-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42e10-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="42e10-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42e10-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="42e10-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="42e10-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42e10-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="42e10-133">En el cuadro de búsqueda, escriba **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="42e10-133">In the search box, type **Optimizely**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="42e10-135">En el panel de resultados, seleccione **Optimizely** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="42e10-135">In the results panel, select **Optimizely**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42e10-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42e10-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42e10-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Optimizely con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="42e10-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="42e10-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Optimizely para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42e10-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span></span> <span data-ttu-id="42e10-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42e10-140">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span></span>

<span data-ttu-id="42e10-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como valor del **nombre de usuario** en Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42e10-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span></span>

<span data-ttu-id="42e10-142">Para configurar y probar el inicio de sesión único de Azure AD con Optimizely, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="42e10-142">To configure and test Azure AD single sign-on with Optimizely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42e10-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="42e10-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42e10-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42e10-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42e10-145">**[Creación de un usuario de prueba de Optimizely](#creating-an-optimizely-test-user)**: el objetivo es tener un homólogo de Britta Simon en Optimizely que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42e10-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="42e10-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42e10-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42e10-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="42e10-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42e10-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42e10-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42e10-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42e10-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="42e10-150">**Para configurar el inicio de sesión único de Azure AD con Optimizely, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="42e10-150">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="42e10-151">En la página de integración de la aplicación **Optimizely** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="42e10-151">In the Azure portal, on the **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="42e10-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="42e10-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="42e10-155">En la sección **Dominio y direcciones URL de Optimizely**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="42e10-155">On the **Optimizely Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="42e10-157">a.</span><span class="sxs-lookup"><span data-stu-id="42e10-157">a.</span></span> <span data-ttu-id="42e10-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://app.optimizely.net/<instance name>`.</span><span class="sxs-lookup"><span data-stu-id="42e10-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="42e10-159">b.</span><span class="sxs-lookup"><span data-stu-id="42e10-159">b.</span></span> <span data-ttu-id="42e10-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="42e10-160">In the **Identifier** textbox, type a URL using the following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42e10-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="42e10-161">These values are not the real.</span></span> <span data-ttu-id="42e10-162">El valor se actualizará con la dirección URL de inicio de sesión y el identificador reales, que se explican más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="42e10-162">You will update the value with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="42e10-163">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="42e10-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="42e10-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="42e10-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42e10-167">En la sección **Configuración de Optimizely**, haga clic en **Configurar Optimizely** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="42e10-167">On the **Optimizely Configuration** section, click **Configure Optimizely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="42e10-168">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="42e10-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="42e10-170">Para configurar el inicio de sesión único en **Optimizely**, póngase en contacto con el administrador de su cuenta de Optimizely y proporcione el **certificado (Base64)** descargado y la **dirección URL del servicio de inicio de sesión único de SAML**.</span><span class="sxs-lookup"><span data-stu-id="42e10-170">To configure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide the downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="42e10-171">En respuesta a su correo electrónico, Optimizely proporciona la URL de inicio de sesión (SSO iniciado por el proveedor de servicios) y los valores de Identificador (Id. de entidad del proveedor de servicios).</span><span class="sxs-lookup"><span data-stu-id="42e10-171">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="42e10-172">a.</span><span class="sxs-lookup"><span data-stu-id="42e10-172">a.</span></span> <span data-ttu-id="42e10-173">Copie la **URL de inicio de sesión único iniciado por SP** que proporciona Optimizely y péguela en el cuadro de texto **URL de inicio de sesión** en la sección **Dominio y direcciones URL de Optimizely** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="42e10-173">Copy the **SP-initiated SSO URL** provided by Optimizely, and paste into the **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="42e10-174">b.</span><span class="sxs-lookup"><span data-stu-id="42e10-174">b.</span></span> <span data-ttu-id="42e10-175">Copie el **identificador de entidad del proveedor de servicios** que proporciona Optimizely y péguelo en el cuadro de texto **Identificador** de la sección **Dominio y direcciones URL de Optimizely** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="42e10-175">Copy the **Service Provider Entity ID** provided by Optimizely, and paste into the **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="42e10-176">En una ventana de explorador diferente, inicie sesión en su aplicación de Optimizely como administrador.</span><span class="sxs-lookup"><span data-stu-id="42e10-176">In a different browser window, sign-on to your Optimizely application.</span></span>

10. <span data-ttu-id="42e10-177">Haga clic en el nombre de la cuenta de la parte superior derecha y, después, en **Configuración de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="42e10-177">Click you account name in the top right corner and then **Account Settings**.</span></span>
   
    ![Inicio de sesión único de Azure AD ](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="42e10-179">En la pestaña Cuenta, active la casilla **Habilitar SSO** que se encuentra debajo de Inicio de sesión único en la sección **Información general**.</span><span class="sxs-lookup"><span data-stu-id="42e10-179">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span></span>
   
    ![Inicio de sesión único de Azure AD ](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="42e10-181">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="42e10-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="42e10-182">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="42e10-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42e10-183">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="42e10-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42e10-184">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42e10-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42e10-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42e10-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="42e10-186">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="42e10-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="42e10-188">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="42e10-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42e10-189">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42e10-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42e10-191">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="42e10-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42e10-193">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42e10-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42e10-195">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="42e10-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42e10-197">a.</span><span class="sxs-lookup"><span data-stu-id="42e10-197">a.</span></span> <span data-ttu-id="42e10-198">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42e10-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42e10-199">b.</span><span class="sxs-lookup"><span data-stu-id="42e10-199">b.</span></span> <span data-ttu-id="42e10-200">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42e10-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="42e10-201">c.</span><span class="sxs-lookup"><span data-stu-id="42e10-201">c.</span></span> <span data-ttu-id="42e10-202">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="42e10-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="42e10-203">d.</span><span class="sxs-lookup"><span data-stu-id="42e10-203">d.</span></span> <span data-ttu-id="42e10-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="42e10-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="42e10-205">Creación de un usuario de prueba de Optimizely</span><span class="sxs-lookup"><span data-stu-id="42e10-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="42e10-206">En esta sección, creará un usuario llamado Britta Simon en Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42e10-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="42e10-207">En la página principal, seleccione la pestaña **Colaboradores**.</span><span class="sxs-lookup"><span data-stu-id="42e10-207">On the home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="42e10-208">Para agregar un nuevo colaborador, haga clic en **New Collaborator** (Nuevo colaborador).</span><span class="sxs-lookup"><span data-stu-id="42e10-208">To add new collaborator to the project, click **New Collaborator**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="42e10-210">Escriba la dirección de correo electrónico y asígnele un rol.</span><span class="sxs-lookup"><span data-stu-id="42e10-210">Fill in the email address and assign them a role.</span></span> <span data-ttu-id="42e10-211">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="42e10-211">Click **Invite**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="42e10-213">El usuario recibirá una invitación por correo electrónico,</span><span class="sxs-lookup"><span data-stu-id="42e10-213">They receive an email invite.</span></span> <span data-ttu-id="42e10-214">con la que debe iniciar sesión en Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42e10-214">Using the email address, they have to log in to Optimizely.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="42e10-215">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42e10-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="42e10-216">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42e10-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Optimizely.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="42e10-218">**Para asignar Britta Simon a Optimizely, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="42e10-218">**To assign Britta Simon to Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="42e10-219">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="42e10-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="42e10-221">En la lista de aplicaciones, seleccione **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="42e10-221">In the applications list, select **Optimizely**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="42e10-223">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="42e10-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="42e10-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="42e10-225">Click **Add** button.</span></span> <span data-ttu-id="42e10-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="42e10-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="42e10-228">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="42e10-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42e10-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="42e10-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42e10-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="42e10-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42e10-231">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="42e10-231">Testing single sign-on</span></span>

<span data-ttu-id="42e10-232">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="42e10-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="42e10-233">Al hacer clic en el icono de Optimizely en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42e10-233">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="42e10-234">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="42e10-234">Additional resources</span></span>

* [<span data-ttu-id="42e10-235">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42e10-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42e10-236">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42e10-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

