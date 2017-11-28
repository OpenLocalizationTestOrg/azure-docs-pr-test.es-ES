---
title: "Tutorial: integración de Azure Active Directory con BetterWorks | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y BetterWorks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d6a5b167c0befbd0fe2c65bdd16abc35ed0a659c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="ea0ae-103">Tutorial: Integración de Azure Active Directory con BetterWorks</span><span class="sxs-lookup"><span data-stu-id="ea0ae-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="ea0ae-104">En este tutorial, obtendrá información sobre cómo integrar BetterWorks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea0ae-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea0ae-105">La integración de BetterWorks con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ea0ae-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ea0ae-106">Puede controlar en Azure AD quién tiene acceso a BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="ea0ae-107">Puede permitir que los usuarios inicien sesión automáticamente en BetterWorks (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea0ae-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ea0ae-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea0ae-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea0ae-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ea0ae-110">Prerequisites</span></span>

<span data-ttu-id="ea0ae-111">Para configurar la integración de Azure AD con BetterWorks, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ea0ae-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="ea0ae-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea0ae-113">Una suscripción habilitada para inicio de sesión único en BetterWorks</span><span class="sxs-lookup"><span data-stu-id="ea0ae-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea0ae-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea0ae-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ea0ae-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea0ae-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea0ae-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea0ae-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea0ae-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ea0ae-118">Scenario description</span></span>
<span data-ttu-id="ea0ae-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea0ae-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="ea0ae-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea0ae-121">Adición de BetterWorks desde la galería</span><span class="sxs-lookup"><span data-stu-id="ea0ae-121">Adding BetterWorks from the gallery</span></span>
2. <span data-ttu-id="ea0ae-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0ae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="ea0ae-123">Adición de BetterWorks desde la galería</span><span class="sxs-lookup"><span data-stu-id="ea0ae-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="ea0ae-124">Para configurar la integración de BetterWorks en Azure AD, es preciso agregar BetterWorks desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ea0ae-125">**Para agregar BetterWorks desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="ea0ae-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ea0ae-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ea0ae-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ea0ae-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ea0ae-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ea0ae-133">En el cuadro de búsqueda, escriba **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-133">In the search box, type **BetterWorks**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="ea0ae-135">En el panel de resultados, seleccione **BetterWorks** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea0ae-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0ae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea0ae-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con BetterWorks con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ea0ae-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ea0ae-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de BetterWorks para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="ea0ae-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="ea0ae-141">Para establecer la relación de vínculo, en BetterWorks, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ea0ae-142">Para configurar y probar el inicio de sesión único de Azure AD con BetterWorks, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ea0ae-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ea0ae-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ea0ae-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea0ae-145">**[Creación de un usuario de prueba en BetterWorks](#creating-a-betterworks-test-user)**: para tener un homólogo de Britta Simon en BetterWorks que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea0ae-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea0ae-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea0ae-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0ae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea0ae-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="ea0ae-150">**Para configurar el inicio de sesión único de Azure AD con BetterWorks, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ea0ae-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="ea0ae-151">En Azure Portal, en la página de integración de la aplicación **BetterWorks**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ea0ae-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="ea0ae-155">En la sección **Dominio y direcciones URL de BetterWorks**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="ea0ae-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="ea0ae-157">a.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-157">a.</span></span> <span data-ttu-id="ea0ae-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="ea0ae-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="ea0ae-159">b.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-159">b.</span></span> <span data-ttu-id="ea0ae-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://app.betterworks.com/saml2/acs/`.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="ea0ae-161">En la sección **Dominio y direcciones URL de BetterWorks**, si quiere configurar la aplicación en **SP initiated mode** (Modo iniciado por SP), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ea0ae-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="ea0ae-163">a.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-163">a.</span></span> <span data-ttu-id="ea0ae-164">Haga clic en la opción **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="ea0ae-165">b.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-165">b.</span></span> <span data-ttu-id="ea0ae-166">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://app.betterworks.com`.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea0ae-167">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-167">These are not real values.</span></span> <span data-ttu-id="ea0ae-168">Actualícelos con la dirección URL de respuesta, el identificador y la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="ea0ae-169">Póngase en contacto con el [equipo de soporte técnico de BetterWorks](mailto:support@betterworks.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
4. <span data-ttu-id="ea0ae-170">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="ea0ae-172">La aplicación BetterWorks espera que las aserciones SAML se encuentren en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ea0ae-173">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-173">Configure the following claims for this application.</span></span> <span data-ttu-id="ea0ae-174">Puede administrar el valor de estos atributos desde la pestaña "**Atributo**" de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="ea0ae-175">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-175">The following screenshot shows an example for this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="ea0ae-177">En el cuadro de diálogo **Atributos de token de SAML** , para cada fila de la tabla siguiente, realice los pasos que se indican a continuación:</span><span class="sxs-lookup"><span data-stu-id="ea0ae-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="ea0ae-178">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="ea0ae-178">Attribute Name</span></span> | <span data-ttu-id="ea0ae-179">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="ea0ae-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="ea0ae-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="ea0ae-180">saml_token</span></span>     | <span data-ttu-id="ea0ae-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="ea0ae-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="ea0ae-182">a.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-182">a.</span></span> <span data-ttu-id="ea0ae-183">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="ea0ae-186">b.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-186">b.</span></span> <span data-ttu-id="ea0ae-187">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="ea0ae-188">c.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-188">c.</span></span> <span data-ttu-id="ea0ae-189">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="ea0ae-190">d.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-190">d.</span></span> <span data-ttu-id="ea0ae-191">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-191">Click **Ok**.</span></span>

7. <span data-ttu-id="ea0ae-192">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ea0ae-192">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ea0ae-194">Para configurar el inicio de sesión único en **BetterWorks**, es preciso enviar los datos descargados de **XML de metadatos** al [equipo de soporte técnico de BetterWorks](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="ea0ae-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="ea0ae-195">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ea0ae-196">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ea0ae-197">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ea0ae-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea0ae-198">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0ae-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea0ae-199">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ea0ae-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ea0ae-201">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="ea0ae-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ea0ae-202">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea0ae-204">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea0ae-206">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea0ae-208">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ea0ae-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea0ae-210">a.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-210">a.</span></span> <span data-ttu-id="ea0ae-211">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea0ae-212">b.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-212">b.</span></span> <span data-ttu-id="ea0ae-213">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea0ae-214">c.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-214">c.</span></span> <span data-ttu-id="ea0ae-215">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ea0ae-216">d.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-216">d.</span></span> <span data-ttu-id="ea0ae-217">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="ea0ae-218">Creación de un usuario de prueba en BetterWorks</span><span class="sxs-lookup"><span data-stu-id="ea0ae-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="ea0ae-219">En esta sección, creará un usuario llamado Britta Simon en BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="ea0ae-220">Colabore con el [equipo de soporte técnico de BetterWorks](mailto:support@betterworks.com) para agregar los usuarios a la plataforma BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ea0ae-221">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0ae-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ea0ae-222">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ea0ae-224">**Para asignar Britta Simon a BetterWorks, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ea0ae-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="ea0ae-225">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ea0ae-227">En la lista de aplicaciones, seleccione **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-227">In the applications list, select **BetterWorks**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="ea0ae-229">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ea0ae-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-231">Click **Add** button.</span></span> <span data-ttu-id="ea0ae-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ea0ae-234">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ea0ae-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea0ae-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea0ae-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ea0ae-237">Testing single sign-on</span></span>

<span data-ttu-id="ea0ae-238">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ea0ae-239">Al hacer clic en el icono de BetterWorks en el panel de acceso, debería iniciar sesión automáticamente en su aplicación BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="ea0ae-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea0ae-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ea0ae-240">Additional resources</span></span>

* [<span data-ttu-id="ea0ae-241">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea0ae-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea0ae-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ea0ae-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

