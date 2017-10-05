---
title: "Tutorial: Integración de Azure Active Directory con Blackboard Learn | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Blackboard Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: c2b7638e99fa46ff41a7f2202bdf0e7a2b017c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="9604c-103">Tutorial: Integración de Azure Active Directory con Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="9604c-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="9604c-104">En este tutorial, obtendrá información sobre cómo integrar Blackboard Learn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9604c-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9604c-105">La integración de Blackboard Learn con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9604c-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9604c-106">Puede controlar en Azure AD quién tiene acceso a Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9604c-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="9604c-107">Puede permitir que los usuarios inicien sesión automáticamente en Blackboard Learn (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9604c-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9604c-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9604c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9604c-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9604c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9604c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9604c-110">Prerequisites</span></span>

<span data-ttu-id="9604c-111">Para configurar la integración de Azure AD con Blackboard Learn, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9604c-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="9604c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9604c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9604c-113">Una suscripción habilitada para el inicio de sesión único de Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="9604c-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9604c-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9604c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9604c-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9604c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9604c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9604c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9604c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9604c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9604c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9604c-118">Scenario description</span></span>
<span data-ttu-id="9604c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9604c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9604c-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="9604c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9604c-121">Adición de Blackboard Learn desde la galería</span><span class="sxs-lookup"><span data-stu-id="9604c-121">Adding Blackboard Learn from the gallery</span></span>
2. <span data-ttu-id="9604c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9604c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="9604c-123">Adición de Blackboard Learn desde la galería</span><span class="sxs-lookup"><span data-stu-id="9604c-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="9604c-124">Para configurar la integración de Blackboard Learn en Azure AD, es preciso agregar Blackboard Learn desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="9604c-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9604c-125">**Para agregar Blackboard Learn desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9604c-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9604c-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9604c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9604c-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9604c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9604c-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9604c-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9604c-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9604c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9604c-133">En el cuadro de búsqueda, escriba **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="9604c-133">In the search box, type **Blackboard Learn**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="9604c-135">En el panel de resultados, seleccione **Blackboard Learn** y, después, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9604c-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9604c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9604c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9604c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Blackboard Learn con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9604c-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9604c-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Blackboard Learn para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9604c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="9604c-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9604c-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="9604c-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como valor del **nombre de usuario** en Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9604c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="9604c-142">Para configurar y probar el inicio de sesión único de Azure AD con Blackboard Learn, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9604c-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9604c-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="9604c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9604c-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9604c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9604c-145">**[Creación de un usuario de prueba de Blackboard Learn](#creating-a-blackboard-learn-test-user)**: para tener un homólogo de Britta Simon en Blackboard Learn que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9604c-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9604c-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9604c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9604c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9604c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9604c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9604c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9604c-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9604c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="9604c-150">**Para configurar el inicio de sesión único de Azure AD con Blackboard Learn, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9604c-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="9604c-151">En Azure Portal, en la página de integración de la aplicación **Blackboard Learn**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9604c-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9604c-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9604c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="9604c-155">En la sección **Dominio y direcciones URL de Blackboard Learn**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9604c-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="9604c-157">a.</span><span class="sxs-lookup"><span data-stu-id="9604c-157">a.</span></span> <span data-ttu-id="9604c-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.blackboard.com/`.</span><span class="sxs-lookup"><span data-stu-id="9604c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="9604c-159">b.</span><span class="sxs-lookup"><span data-stu-id="9604c-159">b.</span></span> <span data-ttu-id="9604c-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="9604c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="9604c-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9604c-161">These values are not real.</span></span> <span data-ttu-id="9604c-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9604c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9604c-163">Póngase en contacto con [el equipo de soporte al cliente de Blackboard Learn](https://www.blackboard.com/support/index.aspx) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="9604c-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

4. <span data-ttu-id="9604c-164">La aplicación Blackboard Learn espera que las aserciones SAML estén en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="9604c-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="9604c-165">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="9604c-165">Configure the following claims for this application.</span></span> <span data-ttu-id="9604c-166">Puede administrar los valores de estos atributos en la sección **Atributos de usuario** de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9604c-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="9604c-167">La siguiente captura de pantalla muestra un ejemplo al respecto.</span><span class="sxs-lookup"><span data-stu-id="9604c-167">The following screenshot shows an example about it.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="9604c-169">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="9604c-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="9604c-170">Aquí asignamos el atributo Userprincipalname como el atributo de usuario único, pero puede asignarlo al valor adecuado que distinga de manera única el usuario de la organización y que se asigne al campo de nombre de usuario de Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9604c-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="9604c-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="9604c-171">Attribute Name</span></span> | <span data-ttu-id="9604c-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="9604c-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="9604c-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="9604c-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="9604c-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="9604c-174">user.userprincipalname</span></span> |

    <span data-ttu-id="9604c-175">a.</span><span class="sxs-lookup"><span data-stu-id="9604c-175">a.</span></span> <span data-ttu-id="9604c-176">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="9604c-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9604c-179">b.</span><span class="sxs-lookup"><span data-stu-id="9604c-179">b.</span></span> <span data-ttu-id="9604c-180">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="9604c-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="9604c-181">c.</span><span class="sxs-lookup"><span data-stu-id="9604c-181">c.</span></span> <span data-ttu-id="9604c-182">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="9604c-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9604c-183">d.</span><span class="sxs-lookup"><span data-stu-id="9604c-183">d.</span></span> <span data-ttu-id="9604c-184">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9604c-184">Click **Ok**.</span></span>

4. <span data-ttu-id="9604c-185">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9604c-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="9604c-187">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9604c-187">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9604c-189">En la sección **Configuración de Blackboard Learn**, haga clic en **Configurar Blackboard Learn** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="9604c-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9604c-190">Copie el **identificador de entidad de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="9604c-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="9604c-192">Para configurar el inicio de sesión único en **Blackboard Learn**, debe enviar el **XML de metadatos** descargado y el **identificador de entidad de SAML** al [soporte técnico de Blackboard Learn](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="9604c-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="9604c-193">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9604c-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9604c-194">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9604c-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9604c-195">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9604c-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9604c-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9604c-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="9604c-197">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9604c-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9604c-199">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9604c-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9604c-200">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9604c-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9604c-202">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9604c-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9604c-204">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9604c-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9604c-206">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9604c-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9604c-208">a.</span><span class="sxs-lookup"><span data-stu-id="9604c-208">a.</span></span> <span data-ttu-id="9604c-209">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9604c-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9604c-210">b.</span><span class="sxs-lookup"><span data-stu-id="9604c-210">b.</span></span> <span data-ttu-id="9604c-211">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9604c-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="9604c-212">c.</span><span class="sxs-lookup"><span data-stu-id="9604c-212">c.</span></span> <span data-ttu-id="9604c-213">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9604c-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9604c-214">d.</span><span class="sxs-lookup"><span data-stu-id="9604c-214">d.</span></span> <span data-ttu-id="9604c-215">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9604c-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="9604c-216">Creación de un usuario de prueba de Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="9604c-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="9604c-217">En esta sección, creará un usuario llamado Britta Simon en Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9604c-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="9604c-218">Compatibilidad de aplicaciones de Blackboard Learn para el aprovisionamiento de usuarios justo a tiempo.</span><span class="sxs-lookup"><span data-stu-id="9604c-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="9604c-219">Asegúrese de que ha configurado las notificaciones, tal y como se describe en la sección **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="9604c-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9604c-220">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9604c-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9604c-221">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9604c-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9604c-223">**Para asignar Britta Simon a Blackboard Learn, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9604c-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="9604c-224">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9604c-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9604c-226">En la lista de aplicaciones, seleccione **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="9604c-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="9604c-228">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9604c-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9604c-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9604c-230">Click **Add** button.</span></span> <span data-ttu-id="9604c-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9604c-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9604c-233">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9604c-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9604c-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9604c-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9604c-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9604c-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9604c-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9604c-236">Testing single sign-on</span></span>

<span data-ttu-id="9604c-237">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9604c-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9604c-238">Al hacer clic en el icono de Blackboard Learn en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="9604c-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="9604c-239">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9604c-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9604c-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9604c-240">Additional resources</span></span>

* [<span data-ttu-id="9604c-241">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9604c-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9604c-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9604c-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

