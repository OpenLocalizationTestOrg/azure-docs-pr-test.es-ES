---
title: "Tutorial: Integración de Azure Active Directory con ServiceChannel | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 7e1dad18ff0ae9a9102b789b2cb32e7b96ed3d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="09483-103">Tutorial: Integración de Azure Active Directory con ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="09483-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="09483-104">En este tutorial, obtendrá información sobre cómo integrar ServiceChannel con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="09483-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="09483-105">La integración de ServiceChannel con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="09483-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="09483-106">Puede controlar en Azure AD quién tiene acceso a ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="09483-106">You can control in Azure AD who has access to ServiceChannel</span></span>
- <span data-ttu-id="09483-107">Puede habilitar que los usuarios inicien sesión automáticamente en ServiceChannel (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09483-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="09483-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="09483-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="09483-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="09483-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09483-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="09483-110">Prerequisites</span></span>

<span data-ttu-id="09483-111">Para configurar la integración de Azure AD con ServiceChannel, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="09483-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span></span>

- <span data-ttu-id="09483-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="09483-112">An Azure AD subscription</span></span>
- <span data-ttu-id="09483-113">Una suscripción habilitada para inicio de sesión único en ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="09483-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="09483-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="09483-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="09483-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="09483-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="09483-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="09483-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="09483-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="09483-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="09483-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="09483-118">Scenario description</span></span>
<span data-ttu-id="09483-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="09483-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="09483-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="09483-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="09483-121">Agregar ServiceChannel desde la galería</span><span class="sxs-lookup"><span data-stu-id="09483-121">Adding ServiceChannel from the gallery</span></span>
2. <span data-ttu-id="09483-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="09483-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-the-gallery"></a><span data-ttu-id="09483-123">Agregar ServiceChannel desde la galería</span><span class="sxs-lookup"><span data-stu-id="09483-123">Adding ServiceChannel from the gallery</span></span>
<span data-ttu-id="09483-124">Para configurar la integración de ServiceChannel en Azure AD, deberá agregar ServiceChannel desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="09483-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="09483-125">**Para agregar ServiceChannel desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="09483-125">**To add ServiceChannel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="09483-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="09483-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="09483-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="09483-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="09483-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="09483-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="09483-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="09483-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="09483-133">En el cuadro de búsqueda, escriba **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="09483-133">In the search box, type **ServiceChannel**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="09483-135">En el panel de resultados, seleccione **ServiceChannel** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="09483-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="09483-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="09483-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="09483-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con ServiceChannel con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="09483-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="09483-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ServiceChannel para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09483-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span></span> <span data-ttu-id="09483-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="09483-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span></span>

<span data-ttu-id="09483-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="09483-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span></span>

<span data-ttu-id="09483-142">Para configurar y probar el inicio de sesión único de Azure AD con ServiceChannel, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="09483-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="09483-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="09483-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="09483-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09483-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="09483-145">**[Creación de un usuario de prueba de ServiceChannel](#creating-a-servicechannel-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09483-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="09483-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09483-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="09483-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="09483-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="09483-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="09483-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="09483-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="09483-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="09483-150">**Para configurar el inicio de sesión único de Azure AD con ServiceChannel, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="09483-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="09483-151">En el Portal de administración de Azure, en la página de integración de la aplicación **ServiceChannel**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="09483-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="09483-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="09483-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="09483-155">En la sección **Dominio y direcciones URL de ServiceChannel**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="09483-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="09483-157">a.</span><span class="sxs-lookup"><span data-stu-id="09483-157">a.</span></span> <span data-ttu-id="09483-158">En el cuadro de texto **Identificador**, escriba el valor como `http://adfs.<domain>.com/adfs/service/trust`.</span><span class="sxs-lookup"><span data-stu-id="09483-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="09483-159">b.</span><span class="sxs-lookup"><span data-stu-id="09483-159">b.</span></span> <span data-ttu-id="09483-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<customer domain>.servicechannel.com/saml/acs`.</span><span class="sxs-lookup"><span data-stu-id="09483-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="09483-161">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="09483-161">Please note that these are not the real values.</span></span> <span data-ttu-id="09483-162">Estos valores se tienen que actualizar con los valores reales de Identificador y URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="09483-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="09483-163">Aquí le recomendamos que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="09483-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="09483-164">Póngase en contacto con el [equipo de soporte técnico de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="09483-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span></span>

4. <span data-ttu-id="09483-165">La aplicación ServiceChannel espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token de SAML.</span><span class="sxs-lookup"><span data-stu-id="09483-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="09483-166">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="09483-166">The following screenshot shows an example for this.</span></span> <span data-ttu-id="09483-167">**NameIdentifier (identificador de usuario)** es la única notificación obligatoria y el valor predeterminado es **user.userprincipalname**, pero ServiceChannel espera que se le asigne **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="09483-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span></span> <span data-ttu-id="09483-168">Si va a habilitar el aprovisionamiento de usuarios Just-In-Time, debe agregar las siguientes notificaciones tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="09483-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span></span> <span data-ttu-id="09483-169">La notificación **role** debe asignarse a **user.assignedroles**, que contiene el rol del usuario.</span><span class="sxs-lookup"><span data-stu-id="09483-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span></span>  

    <span data-ttu-id="09483-170">Puede consultar la guía de ServiceChannel [aquí](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) para obtener más información sobre las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="09483-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="09483-172">Haga clic [aquí](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) para saber cómo configurar el valor **Role** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09483-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) to know how to configure **Role** in Azure AD</span></span>

5. <span data-ttu-id="09483-173">En la sección **Atributos de usuario**, haga clic en **Ver y editar todos los demás atributos de usuario** y establezca los atributos.</span><span class="sxs-lookup"><span data-stu-id="09483-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span>

    | <span data-ttu-id="09483-174">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="09483-174">Attribute Name</span></span> | <span data-ttu-id="09483-175">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="09483-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="09483-176">Rol</span><span class="sxs-lookup"><span data-stu-id="09483-176">Role</span></span>| <span data-ttu-id="09483-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="09483-177">user.assignedroles</span></span> |

    <span data-ttu-id="09483-178">a.</span><span class="sxs-lookup"><span data-stu-id="09483-178">a.</span></span> <span data-ttu-id="09483-179">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="09483-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="09483-182">b.</span><span class="sxs-lookup"><span data-stu-id="09483-182">b.</span></span> <span data-ttu-id="09483-183">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="09483-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="09483-184">c.</span><span class="sxs-lookup"><span data-stu-id="09483-184">c.</span></span> <span data-ttu-id="09483-185">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="09483-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="09483-186">d.</span><span class="sxs-lookup"><span data-stu-id="09483-186">d.</span></span> <span data-ttu-id="09483-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="09483-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="09483-188">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="09483-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="09483-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="09483-190">Click **Save**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="09483-192">En la sección **Configuración de ServiceChannel**, haga clic en **Configurar ServiceChannel** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="09483-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="09483-193">Tome nota del **Id. de entidad de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="09483-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span></span>

9. <span data-ttu-id="09483-194">Para configurar el inicio de sesión único en el lado de **ServiceChannel**, debe enviar el **certificado (Base64)** descargado y el **Id. de entidad de SAML** al [equipo de soporte técnico de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="09483-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="09483-195">Ellos realizarán esta operación para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="09483-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="09483-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="09483-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="09483-197">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09483-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="09483-199">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="09483-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="09483-200">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="09483-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="09483-202">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="09483-202">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="09483-204">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="09483-204">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="09483-206">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="09483-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="09483-208">a.</span><span class="sxs-lookup"><span data-stu-id="09483-208">a.</span></span> <span data-ttu-id="09483-209">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="09483-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="09483-210">b.</span><span class="sxs-lookup"><span data-stu-id="09483-210">b.</span></span> <span data-ttu-id="09483-211">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09483-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="09483-212">c.</span><span class="sxs-lookup"><span data-stu-id="09483-212">c.</span></span> <span data-ttu-id="09483-213">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="09483-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="09483-214">d.</span><span class="sxs-lookup"><span data-stu-id="09483-214">d.</span></span> <span data-ttu-id="09483-215">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="09483-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="09483-216">Crear un usuario de prueba de ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="09483-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="09483-217">La aplicación admite aprovisionamiento de usuarios Just-In-Time y, tras la autenticación, los usuarios se crearán automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="09483-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="09483-218">Para el aprovisionamiento de usuario completo, póngase en contacto con el [equipo de soporte técnico de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="09483-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="09483-219">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="09483-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="09483-220">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="09483-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="09483-222">**Para asignar Britta Simon a ServiceChannel, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="09483-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="09483-223">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="09483-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="09483-225">En la lista de aplicaciones, seleccione **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="09483-225">In the applications list, select **ServiceChannel**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="09483-227">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="09483-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="09483-229">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="09483-229">Click **Add** button.</span></span> <span data-ttu-id="09483-230">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="09483-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="09483-232">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="09483-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="09483-233">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="09483-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="09483-234">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="09483-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="09483-235">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="09483-235">Testing single sign-on</span></span>

<span data-ttu-id="09483-236">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="09483-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="09483-237">Al hacer clic en el icono de ServiceChannel en el panel de acceso, debería iniciar sesión automáticamente en la aplicación ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="09483-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="09483-238">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="09483-238">Additional resources</span></span>

* [<span data-ttu-id="09483-239">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09483-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="09483-240">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="09483-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png