---
title: "Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Symantec Web Security Service (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: d0738bb750a82863b2f77540e8e7b94cca4b64e3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="c14f6-103">Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="c14f6-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="c14f6-104">En este tutorial, obtendrá información sobre cómo integrar Symantec Web Security Service (WSS) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c14f6-104">In this tutorial, you learn how to integrate Symantec Web Security Service (WSS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c14f6-105">La integración de Symantec Web Security Service (WSS) con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c14f6-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c14f6-106">Puede controlar en Azure AD quién tiene acceso a Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="c14f6-106">You can control in Azure AD who has access to Symantec Web Security Service (WSS)</span></span>
- <span data-ttu-id="c14f6-107">Puede permitir que los usuarios inicien sesión automáticamente en Symantec Web Security Service (WSS) (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c14f6-107">You can enable your users to automatically get signed-on to Symantec Web Security Service (WSS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c14f6-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c14f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c14f6-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c14f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c14f6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c14f6-110">Prerequisites</span></span>

<span data-ttu-id="c14f6-111">Para configurar la integración de Azure AD con Symantec Web Security Service (WSS), necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c14f6-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span></span>

- <span data-ttu-id="c14f6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c14f6-113">Una suscripción de Symantec Web Security Service (WSS) con inicio de sesión único habilitado</span><span class="sxs-lookup"><span data-stu-id="c14f6-113">A Symantec Web Security Service (WSS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c14f6-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c14f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c14f6-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c14f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c14f6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c14f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c14f6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c14f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c14f6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c14f6-118">Scenario description</span></span>
<span data-ttu-id="c14f6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c14f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c14f6-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="c14f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c14f6-121">Agregar Symantec Web Security Service (WSS) desde la galería</span><span class="sxs-lookup"><span data-stu-id="c14f6-121">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
2. <span data-ttu-id="c14f6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-the-gallery"></a><span data-ttu-id="c14f6-123">Agregación de Symantec Web Security Service (WSS) desde la galería</span><span class="sxs-lookup"><span data-stu-id="c14f6-123">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
<span data-ttu-id="c14f6-124">Para configurar la integración de Symantec Web Security Service (WSS) en Azure AD, es preciso agregar Symantec Web Security Service (WSS) desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="c14f6-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c14f6-125">**Para agregar Symantec Web Security Service (WSS) desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="c14f6-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c14f6-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c14f6-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c14f6-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c14f6-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c14f6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c14f6-133">En el cuadro de búsqueda, escriba **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-133">In the search box, type **Symantec Web Security Service (WSS)**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. <span data-ttu-id="c14f6-135">En el panel de resultados, seleccione **Symantec Web Security Service (WSS)** y, después, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c14f6-135">In the results panel, select **Symantec Web Security Service (WSS)**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c14f6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c14f6-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Symantec Web Security Service (WSS) con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c14f6-138">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c14f6-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Symantec Web Security Service (WSS) para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c14f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span></span> <span data-ttu-id="c14f6-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="c14f6-140">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span></span>

<span data-ttu-id="c14f6-141">Para establecer la relación de vínculo, en Symantec Web Security Service (WSS), asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-141">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c14f6-142">Para configurar y probar el inicio de sesión único de Azure AD con Symantec Web Security Service (WSS), es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c14f6-142">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c14f6-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="c14f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c14f6-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c14f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c14f6-145">**[Creación de un usuario de prueba de Symantec Web Security Service (WSS)](#creating-a-symantec-web-security-service-wss-test-user)**: Para tener un homólogo de Britta Simon en Symantec Web Security Service (WSS) que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c14f6-145">**[Creating a Symantec Web Security Service (WSS) test user](#creating-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c14f6-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c14f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c14f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c14f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c14f6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c14f6-149">En esta sección habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación de Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="c14f6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="c14f6-150">**Para configurar el inicio de sesión único de Azure AD con Symantec Web Security Service (WSS), siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="c14f6-150">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="c14f6-151">En Azure Portal, en la página de integración de la aplicación de **Symantec Web Security Service (WSS)**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-151">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c14f6-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c14f6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="c14f6-155">En la sección **Dominio y direcciones URL de Symantec Web Security Service (WSS)**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c14f6-155">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="c14f6-157">a.</span><span class="sxs-lookup"><span data-stu-id="c14f6-157">a.</span></span> <span data-ttu-id="c14f6-158">En el cuadro de texto **Dirección URL de inicio de sesión**, indique la dirección URL que quiere bloquear según la directiva de bloqueo de Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="c14f6-158">In the **Sign-on URL** textbox, mention the url, which you want to block according to the blocking policy of the Symantec Web Security Service (WSS).</span></span>  
    
    <span data-ttu-id="c14f6-159">b.</span><span class="sxs-lookup"><span data-stu-id="c14f6-159">b.</span></span> <span data-ttu-id="c14f6-160">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="c14f6-160">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c14f6-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c14f6-161">These values are not real.</span></span> <span data-ttu-id="c14f6-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="c14f6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c14f6-163">Póngase en contacto con el [equipo de soporte técnico de clientes de Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="c14f6-163">Contact [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) to get these values.</span></span> 

4. <span data-ttu-id="c14f6-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c14f6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="c14f6-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c14f6-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c14f6-168">Para configurar el inicio de sesión único en el lado de **Symantec Web Security Service (WSS)**, es necesario enviar el **XML de metadatos** descargado al [equipo de soporte técnico de Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="c14f6-168">To configure single sign-on on **Symantec Web Security Service (WSS)** side, you need to send the downloaded **Metadata XML** to [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="c14f6-169">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c14f6-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c14f6-170">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c14f6-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c14f6-171">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c14f6-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c14f6-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14f6-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="c14f6-173">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c14f6-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c14f6-175">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c14f6-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c14f6-176">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c14f6-178">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c14f6-180">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c14f6-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c14f6-182">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c14f6-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c14f6-184">a.</span><span class="sxs-lookup"><span data-stu-id="c14f6-184">a.</span></span> <span data-ttu-id="c14f6-185">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c14f6-186">b.</span><span class="sxs-lookup"><span data-stu-id="c14f6-186">b.</span></span> <span data-ttu-id="c14f6-187">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c14f6-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c14f6-188">c.</span><span class="sxs-lookup"><span data-stu-id="c14f6-188">c.</span></span> <span data-ttu-id="c14f6-189">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c14f6-190">d.</span><span class="sxs-lookup"><span data-stu-id="c14f6-190">d.</span></span> <span data-ttu-id="c14f6-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-191">Click **Create**.</span></span>
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="c14f6-192">Crear un usuario de prueba de Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="c14f6-192">Creating a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="c14f6-193">En esta sección, creará un usuario llamado Britta Simon en Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="c14f6-193">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="c14f6-194">Trabaje con el [equipo de soporte técnico de Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us) para agregar los usuarios a la plataforma de Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="c14f6-194">Work with [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) to add the users in the Symantec Web Security Service (WSS) platform.</span></span> <span data-ttu-id="c14f6-195">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c14f6-195">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="c14f6-196">Además de los detalles del usuario, es necesario enviar la dirección IP pública del equipo desde el que está intentando obtener acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c14f6-196">Also along with the user details you need to send the public IPaddress of the machine from which you are trying to access the application.</span></span>

> [!NOTE]
> <span data-ttu-id="c14f6-197">[Haga clic aquí](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) para obtener la dirección IP pública del equipo.</span><span class="sxs-lookup"><span data-stu-id="c14f6-197">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c14f6-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14f6-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c14f6-199">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="c14f6-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c14f6-201">**Para asignar a Britta Simon a Symantec Web Security Service (WSS), siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="c14f6-201">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="c14f6-202">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c14f6-204">En la lista de aplicaciones, seleccione **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-204">In the applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. <span data-ttu-id="c14f6-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c14f6-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-208">Click **Add** button.</span></span> <span data-ttu-id="c14f6-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c14f6-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c14f6-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c14f6-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c14f6-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c14f6-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c14f6-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c14f6-214">Testing single sign-on</span></span>

<span data-ttu-id="c14f6-215">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c14f6-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c14f6-216">Al hacer clic en el icono de Symantec Web Security Service (WSS) en el panel de acceso, se le redirigirá a la página de bloqueo para la que se ha configurado la directiva de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="c14f6-216">When you click the Symantec Web Security Service (WSS) tile in the Access Panel, you get redirected to the blocking page for which the blocking policy has been configured.</span></span>
<span data-ttu-id="c14f6-217">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c14f6-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c14f6-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c14f6-218">Additional resources</span></span>

* [<span data-ttu-id="c14f6-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c14f6-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c14f6-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c14f6-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

