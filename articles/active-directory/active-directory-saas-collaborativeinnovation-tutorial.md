---
title: "Tutorial: integración de Azure Active Directory con Collaborative Innovation | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Collaborative Innovation."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 5706ba9f4e7c92de77a0edc5146aa150de379c9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="8f0a7-103">Tutorial: integración de Azure Active Directory con Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="8f0a7-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="8f0a7-104">En este tutorial, aprenderá a integrar Collaborative Innovation con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f0a7-104">In this tutorial, you learn how to integrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f0a7-105">Integrar Collaborative Innovation con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8f0a7-105">Integrating Collaborative Innovation with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8f0a7-106">Puede controlar en Azure AD quién tiene acceso a Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="8f0a7-106">You can control in Azure AD who has access to Collaborative Innovation</span></span>
- <span data-ttu-id="8f0a7-107">Puede permitir que los usuarios inicien sesión automáticamente en Collaborative Innovation (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-107">You can enable your users to automatically get signed-on to Collaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f0a7-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8f0a7-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f0a7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f0a7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8f0a7-110">Prerequisites</span></span>

<span data-ttu-id="8f0a7-111">Para configurar la integración de Azure AD con Collaborative Innovation, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8f0a7-111">To configure Azure AD integration with Collaborative Innovation, you need the following items:</span></span>

- <span data-ttu-id="8f0a7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0a7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f0a7-113">Una suscripción habilitada para el inicio de sesión único de Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="8f0a7-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f0a7-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f0a7-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8f0a7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f0a7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f0a7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f0a7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f0a7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8f0a7-118">Scenario description</span></span>
<span data-ttu-id="8f0a7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f0a7-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="8f0a7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f0a7-121">Adición de Collaborative Innovation desde la galería</span><span class="sxs-lookup"><span data-stu-id="8f0a7-121">Adding Collaborative Innovation from the gallery</span></span>
2. <span data-ttu-id="8f0a7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0a7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-the-gallery"></a><span data-ttu-id="8f0a7-123">Adición de Collaborative Innovation desde la galería</span><span class="sxs-lookup"><span data-stu-id="8f0a7-123">Adding Collaborative Innovation from the gallery</span></span>
<span data-ttu-id="8f0a7-124">Para configurar la integración de Collaborative Innovation en Azure AD, deberá agregar Collaborative Innovation desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-124">To configure the integration of Collaborative Innovation into Azure AD, you need to add Collaborative Innovation from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8f0a7-125">**Para agregar Collaborative Innovation desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="8f0a7-125">**To add Collaborative Innovation from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8f0a7-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8f0a7-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8f0a7-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8f0a7-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8f0a7-133">En el cuadro de búsqueda, escriba **Collaborative Innovation**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-133">In the search box, type **Collaborative Innovation**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="8f0a7-135">En el panel de resultados, seleccione **Collaborative Innovation** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-135">In the results panel, select **Collaborative Innovation**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f0a7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0a7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f0a7-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Collaborative Innovation con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8f0a7-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8f0a7-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Collaborative Innovation para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Collaborative Innovation is to a user in Azure AD.</span></span> <span data-ttu-id="8f0a7-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-140">In other words, a link relationship between an Azure AD user and the related user in Collaborative Innovation needs to be established.</span></span>

<span data-ttu-id="8f0a7-141">Para establecer la relación de vínculo, en Collaborative Innovation, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-141">In Collaborative Innovation, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8f0a7-142">Para configurar y probar el inicio de sesión único de Azure AD con Collaborative Innovation, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8f0a7-142">To configure and test Azure AD single sign-on with Collaborative Innovation, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8f0a7-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8f0a7-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f0a7-145">**[Creación de un usuario de prueba de Collaborative Innovation](#creating-a-collaborative-innovation-test-user)**: para tener un homólogo de Britta Simon en Collaborative Innovation que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - to have a counterpart of Britta Simon in Collaborative Innovation that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f0a7-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f0a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f0a7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0a7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f0a7-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="8f0a7-150">**Para configurar el inicio de sesión único de Azure AD con Collaborative Innovation, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8f0a7-150">**To configure Azure AD single sign-on with Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="8f0a7-151">En Azure Portal, en la página de integración de la aplicación **Collaborative Innovation**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-151">In the Azure portal, on the **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8f0a7-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="8f0a7-155">En la sección **Dominio y direcciones URL de Collaborative Innovation**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8f0a7-155">On the **Collaborative Innovation Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="8f0a7-157">a.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-157">a.</span></span> <span data-ttu-id="8f0a7-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.foundry.<companyname>.com/`.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="8f0a7-159">b.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-159">b.</span></span> <span data-ttu-id="8f0a7-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="8f0a7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="8f0a7-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-161">These values are not real.</span></span> <span data-ttu-id="8f0a7-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8f0a7-163">Póngase en contacto con el [equipo de soporte técnico de cliente de Collaborative Innovation](https://www.unilever.com/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) to get these values.</span></span>  

4. <span data-ttu-id="8f0a7-164">La aplicación Collaborative Innovation espera que las aserciones SAML estén en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-164">Collaborative Innovation application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8f0a7-165">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="8f0a7-166">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8f0a7-167">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-167">The following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="8f0a7-169">En la sección **Atributos de usuario**, active la casilla **Ver y editar todos los demás atributos de usuario** para expandir los atributos.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="8f0a7-170">Realice los pasos siguientes en cada uno de los atributos mostrados:</span><span class="sxs-lookup"><span data-stu-id="8f0a7-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="8f0a7-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="8f0a7-171">Attribute Name</span></span> | <span data-ttu-id="8f0a7-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="8f0a7-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="8f0a7-173">givenname</span><span class="sxs-lookup"><span data-stu-id="8f0a7-173">givenname</span></span> | <span data-ttu-id="8f0a7-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8f0a7-174">user.givenname</span></span> |
    | <span data-ttu-id="8f0a7-175">surname</span><span class="sxs-lookup"><span data-stu-id="8f0a7-175">surname</span></span> | <span data-ttu-id="8f0a7-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="8f0a7-176">user.surname</span></span> |
    | <span data-ttu-id="8f0a7-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="8f0a7-177">emailaddress</span></span> | <span data-ttu-id="8f0a7-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8f0a7-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="8f0a7-179">name</span><span class="sxs-lookup"><span data-stu-id="8f0a7-179">name</span></span> | <span data-ttu-id="8f0a7-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8f0a7-180">user.userprincipalname</span></span> |

    <span data-ttu-id="8f0a7-181">a.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-181">a.</span></span> <span data-ttu-id="8f0a7-182">Haga clic en el atributo para abrir la ventana **Editar atributo**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-182">Click the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="8f0a7-184">b.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-184">b.</span></span> <span data-ttu-id="8f0a7-185">Elimine el valor de la dirección URL en **Espacio de nombres**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="8f0a7-186">c.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-186">c.</span></span> <span data-ttu-id="8f0a7-187">Haga clic en **Aceptar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-187">Click **Ok** to save the setting.</span></span>

6. <span data-ttu-id="8f0a7-188">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="8f0a7-190">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8f0a7-190">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8f0a7-192">Para configurar el inicio de sesión único en **Collaborative Innovation**, debe enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Collaborative Innovation](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="8f0a7-192">To configure single sign-on on **Collaborative Innovation** side, you need to send the downloaded **Metadata XML** to [Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="8f0a7-193">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8f0a7-194">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8f0a7-195">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8f0a7-196">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f0a7-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f0a7-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0a7-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f0a7-198">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8f0a7-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8f0a7-200">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="8f0a7-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8f0a7-201">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f0a7-203">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f0a7-205">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f0a7-207">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="8f0a7-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f0a7-209">a.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-209">a.</span></span> <span data-ttu-id="8f0a7-210">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f0a7-211">b.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-211">b.</span></span> <span data-ttu-id="8f0a7-212">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f0a7-213">c.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-213">c.</span></span> <span data-ttu-id="8f0a7-214">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8f0a7-215">d.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-215">d.</span></span> <span data-ttu-id="8f0a7-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="8f0a7-217">Creación de un usuario de prueba de Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="8f0a7-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="8f0a7-218">Para permitir que los usuarios de Azure AD inicien sesión en Collaborative Innovation, se les deben aprovisionar en Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-218">To enable Azure AD users to log in to Collaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="8f0a7-219">En caso de esta aplicación, el aprovisionamiento es automático ya que la aplicación admite el aprovisionamiento de usuarios Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-219">In case of this application provisioning is automatic as the application supports just in time user provisioning.</span></span> <span data-ttu-id="8f0a7-220">Por tanto no hay ninguna necesidad de realizar ningún paso aquí.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-220">So there is no need to perform any steps here.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8f0a7-221">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0a7-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8f0a7-222">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Collaborative Innovation.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8f0a7-224">**Para asignar a Britta Simon a Collaborative Innovation, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8f0a7-224">**To assign Britta Simon to Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="8f0a7-225">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8f0a7-227">En la lista de aplicaciones, seleccione **Collaborative Innovation**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-227">In the applications list, select **Collaborative Innovation**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="8f0a7-229">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8f0a7-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-231">Click **Add** button.</span></span> <span data-ttu-id="8f0a7-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8f0a7-234">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8f0a7-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f0a7-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f0a7-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8f0a7-237">Testing single sign-on</span></span>

<span data-ttu-id="8f0a7-238">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8f0a7-239">Al hacer clic en el icono de Collaborative Innovation en el Panel de acceso, accederá a la página de inicio de sesión de la aplicación Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="8f0a7-239">When you click the Collaborative Innovation tile in the Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="8f0a7-240">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f0a7-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8f0a7-241">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8f0a7-241">Additional resources</span></span>

* [<span data-ttu-id="8f0a7-242">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f0a7-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f0a7-243">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8f0a7-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

