---
title: "Tutorial: Integración de Azure Active Directory con iLMS | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 22c72020200138e78835ed7dd2661f18b824c785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="ad099-103">Tutorial: Integración de Azure Active Directory con iLMS</span><span class="sxs-lookup"><span data-stu-id="ad099-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="ad099-104">En este tutorial, obtendrá información sobre cómo integrar iLMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad099-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad099-105">Integrar iLMS con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ad099-105">Integrating iLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ad099-106">Puede controlar en Azure AD quién tiene acceso a iLMS.</span><span class="sxs-lookup"><span data-stu-id="ad099-106">You can control in Azure AD who has access to iLMS</span></span>
- <span data-ttu-id="ad099-107">Puede permitir que los usuarios inicien sesión automáticamente en iLMS (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad099-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad099-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ad099-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ad099-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad099-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad099-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ad099-110">Prerequisites</span></span>

<span data-ttu-id="ad099-111">Para configurar la integración de Azure AD con iLMS, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ad099-111">To configure Azure AD integration with iLMS, you need the following items:</span></span>

- <span data-ttu-id="ad099-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad099-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad099-113">Una suscripción habilitada para inicio de sesión único en iLMS</span><span class="sxs-lookup"><span data-stu-id="ad099-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad099-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ad099-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad099-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ad099-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad099-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ad099-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ad099-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad099-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad099-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ad099-118">Scenario description</span></span>
<span data-ttu-id="ad099-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ad099-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad099-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="ad099-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad099-121">Adición de iLMS desde la galería</span><span class="sxs-lookup"><span data-stu-id="ad099-121">Adding iLMS from the gallery</span></span>
2. <span data-ttu-id="ad099-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad099-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-the-gallery"></a><span data-ttu-id="ad099-123">Adición de iLMS desde la galería</span><span class="sxs-lookup"><span data-stu-id="ad099-123">Adding iLMS from the gallery</span></span>
<span data-ttu-id="ad099-124">Para configurar la integración de iLMS en Azure AD, debe agregar iLMS desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="ad099-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ad099-125">**Para agregar iLMS desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="ad099-125">**To add iLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ad099-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad099-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad099-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ad099-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ad099-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ad099-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ad099-131">Haga clic en el botón **Nueva aplicación** en la parte superior del cuadro de diálogo para agregar la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad099-131">To add new application, click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ad099-133">En el cuadro de búsqueda, escriba **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="ad099-133">In the search box, type **iLMS**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="ad099-135">En el panel de resultados, seleccione **iLMS** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad099-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad099-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad099-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad099-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con iLMS con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ad099-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad099-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de iLMS para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad099-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span></span> <span data-ttu-id="ad099-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de iLMS.</span><span class="sxs-lookup"><span data-stu-id="ad099-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span></span>

<span data-ttu-id="ad099-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en iLMS.</span><span class="sxs-lookup"><span data-stu-id="ad099-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span></span>

<span data-ttu-id="ad099-142">Para configurar y probar el inicio de sesión único de Azure AD con iLMS, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ad099-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ad099-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="ad099-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ad099-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad099-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad099-145">**[Creación de un usuario de prueba de iLMS](#creating-an-ilms-test-user)**: para tener un homólogo de Britta Simon en iLMS que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad099-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ad099-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad099-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad099-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ad099-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad099-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad099-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad099-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación iLMS.</span><span class="sxs-lookup"><span data-stu-id="ad099-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="ad099-150">**Para configurar el inicio de sesión único de Azure AD con iLMS, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ad099-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="ad099-151">En Azure Portal, en la página de integración de la aplicación **iLMS**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ad099-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ad099-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ad099-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="ad099-155">En la sección **Dominio y direcciones URL de iLMS**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="ad099-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="ad099-157">a.</span><span class="sxs-lookup"><span data-stu-id="ad099-157">a.</span></span> <span data-ttu-id="ad099-158">En el cuadro de texto **Identificador**, pegue el valor del **identificador** que ha copiado de la sección **Proveedor de servicios** de la configuración de SAML en el portal de administración de iLMS.</span><span class="sxs-lookup"><span data-stu-id="ad099-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="ad099-159">b.</span><span class="sxs-lookup"><span data-stu-id="ad099-159">b.</span></span> <span data-ttu-id="ad099-160">En el cuadro de texto **URL de respuesta**, pegue el valor de **Endpoint (URL)** (Punto de conexión [URL]) que ha copiado de la sección **Proveedor de servicios** de la configuración de SAML en el portal de administración de iLMS, que tiene el siguiente patrón `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`.</span><span class="sxs-lookup"><span data-stu-id="ad099-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="ad099-161">"123456" es un valor de ejemplo del identificador.</span><span class="sxs-lookup"><span data-stu-id="ad099-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="ad099-162">Active **Mostrar configuración avanzada de URL**, si desea volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="ad099-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="ad099-164">En el cuadro de texto **URL de inicio de sesión**, pegue el valor de **Endpoint (URL)** (Punto de conexión [URL]) que ha copiado de la sección **Proveedor de servicios** de la configuración de SAML en el portal de administración de iLMS, como `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`.</span><span class="sxs-lookup"><span data-stu-id="ad099-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="ad099-165">Para habilitar el aprovisionamiento JIT, la aplicación iLMS espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="ad099-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ad099-166">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad099-166">Configure the following claims for this application.</span></span> <span data-ttu-id="ad099-167">Puede administrar los valores de estos atributos en la sección **Atributos de usuario** de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ad099-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="ad099-168">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="ad099-168">The following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="ad099-170">Cree los atributos **department, region** y **division** y agregue el nombre de estos atributos en iLMS.</span><span class="sxs-lookup"><span data-stu-id="ad099-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span></span> <span data-ttu-id="ad099-171">Todos estos atributos mostrados anteriormente son obligatorios.</span><span class="sxs-lookup"><span data-stu-id="ad099-171">All these attributes shown above are required.</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="ad099-172">Debe habilitar **Create Un-recognized User Account** (Crear una cuenta de usuario no reconocida) en iLMS para asignar estos atributos.</span><span class="sxs-lookup"><span data-stu-id="ad099-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span></span> <span data-ttu-id="ad099-173">Siga las instrucciones [aquí](http://support.inspiredelearning.com/customer/portal/articles/2204526) para hacerse una idea de la configuración de los atributos.</span><span class="sxs-lookup"><span data-stu-id="ad099-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span></span>

6. <span data-ttu-id="ad099-174">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo Token SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ad099-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="ad099-175">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="ad099-175">Attribute Name</span></span> | <span data-ttu-id="ad099-176">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="ad099-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="ad099-177">division</span><span class="sxs-lookup"><span data-stu-id="ad099-177">division</span></span> | <span data-ttu-id="ad099-178">user.department</span><span class="sxs-lookup"><span data-stu-id="ad099-178">user.department</span></span> |
    | <span data-ttu-id="ad099-179">region</span><span class="sxs-lookup"><span data-stu-id="ad099-179">region</span></span> | <span data-ttu-id="ad099-180">user.state</span><span class="sxs-lookup"><span data-stu-id="ad099-180">user.state</span></span> |
    | <span data-ttu-id="ad099-181">department</span><span class="sxs-lookup"><span data-stu-id="ad099-181">department</span></span> | <span data-ttu-id="ad099-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="ad099-182">user.jobtitle</span></span> |

    <span data-ttu-id="ad099-183">a.</span><span class="sxs-lookup"><span data-stu-id="ad099-183">a.</span></span> <span data-ttu-id="ad099-184">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="ad099-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="ad099-187">b.</span><span class="sxs-lookup"><span data-stu-id="ad099-187">b.</span></span> <span data-ttu-id="ad099-188">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="ad099-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ad099-189">c.</span><span class="sxs-lookup"><span data-stu-id="ad099-189">c.</span></span> <span data-ttu-id="ad099-190">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="ad099-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ad099-191">d.</span><span class="sxs-lookup"><span data-stu-id="ad099-191">d.</span></span> <span data-ttu-id="ad099-192">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ad099-192">Click **Ok**</span></span>

7. <span data-ttu-id="ad099-193">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ad099-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="ad099-195">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ad099-195">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="ad099-197">En otra ventana del explorador web, regístrese en el **Portal de administración de iLMS** como administrador.</span><span class="sxs-lookup"><span data-stu-id="ad099-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="ad099-198">Haga clic en **SSO:SAML** en **Settings** (Configuración) para abrir la configuración de SAML y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ad099-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="ad099-200">a.</span><span class="sxs-lookup"><span data-stu-id="ad099-200">a.</span></span> <span data-ttu-id="ad099-201">Expanda la sección **Service Provider** (Proveedor de servicios) y copie los valores **Identifier** (Identificador) y **Endpoint (URL)** (Punto de conexión [URL]).</span><span class="sxs-lookup"><span data-stu-id="ad099-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="ad099-203">b.</span><span class="sxs-lookup"><span data-stu-id="ad099-203">b.</span></span> <span data-ttu-id="ad099-204">En la sección **Identity Provider** (Proveedor de identidades), haga clic en **Import Metadata** (Importar metadatos).</span><span class="sxs-lookup"><span data-stu-id="ad099-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="ad099-205">c.</span><span class="sxs-lookup"><span data-stu-id="ad099-205">c.</span></span> <span data-ttu-id="ad099-206">Seleccione el archivo de **metadatos** descargado de Azure Portal en la sección **Certificado de firma de SAML**.</span><span class="sxs-lookup"><span data-stu-id="ad099-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="ad099-208">d.</span><span class="sxs-lookup"><span data-stu-id="ad099-208">d.</span></span> <span data-ttu-id="ad099-209">Si desea habilitar el aprovisionamiento JIT para crear cuentas de iLMS para usuarios no reconocidos, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad099-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="ad099-210">Active **Create Un-recognized User Account** (Crear cuenta de usuario no reconocido).</span><span class="sxs-lookup"><span data-stu-id="ad099-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="ad099-212">Asigne los atributos de Azure AD a los atributos de iLMS.</span><span class="sxs-lookup"><span data-stu-id="ad099-212">Map the attributes in Azure AD with the attributes in iLMS.</span></span> <span data-ttu-id="ad099-213">En la columna de atributos, especifique el nombre de los atributos o el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ad099-213">In the attribute column, specify the attributes name or the default value.</span></span>

    <span data-ttu-id="ad099-214">e.</span><span class="sxs-lookup"><span data-stu-id="ad099-214">e.</span></span> <span data-ttu-id="ad099-215">Vaya a la pestaña **Business Rules** (Reglas empresariales) y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad099-215">Go to **Business Rules** tab and perform the following steps:</span></span> 
        
       ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="ad099-217">Active **Create Un-recognized Regions, Divisions and Departments** (Crear regiones, divisiones y departamentos no reconocidos) para crear regiones, divisiones y departamentos que todavía no existen en el momento del inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ad099-217">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="ad099-218">Active **Update User Profile During Sign-in** (Actualizar perfil de usuario durante el inicio de sesión) para especificar si es necesario actualizar el perfil del usuario con cada inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ad099-218">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="ad099-219">Si la opción **"Update Blank Values for Non Mandatory Fields in User Profile"** (Actualizar valores en blanco para campos no obligatorios del perfil de usuario), los campos opcionales del perfil que estén en blanco al iniciar sesión darán lugar a que el perfil del usuario de iLMS contenga valores en blanco en dichos campos.</span><span class="sxs-lookup"><span data-stu-id="ad099-219">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span></span>
        
       - <span data-ttu-id="ad099-220">Active **Send Error Notification Email** (Enviar correo electrónico de notificación de errores) y escriba la dirección de correo electrónico del usuario en la que desea recibir el correo electrónico de notificación de errores.</span><span class="sxs-lookup"><span data-stu-id="ad099-220">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span></span>

11. <span data-ttu-id="ad099-221">Haga clic en el botón **Save** (Guardar) para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="ad099-221">Click **Save** button to save the settings.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="ad099-223">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad099-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ad099-224">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ad099-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ad099-225">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad099-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad099-226">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad099-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad099-227">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ad099-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ad099-229">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="ad099-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ad099-230">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad099-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad099-232">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ad099-232">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad099-234">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="ad099-234">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad099-236">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ad099-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad099-238">a.</span><span class="sxs-lookup"><span data-stu-id="ad099-238">a.</span></span> <span data-ttu-id="ad099-239">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad099-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad099-240">b.</span><span class="sxs-lookup"><span data-stu-id="ad099-240">b.</span></span> <span data-ttu-id="ad099-241">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad099-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad099-242">c.</span><span class="sxs-lookup"><span data-stu-id="ad099-242">c.</span></span> <span data-ttu-id="ad099-243">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ad099-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ad099-244">d.</span><span class="sxs-lookup"><span data-stu-id="ad099-244">d.</span></span> <span data-ttu-id="ad099-245">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ad099-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="ad099-246">Creación de un usuario de prueba de iLMS</span><span class="sxs-lookup"><span data-stu-id="ad099-246">Creating an iLMS test user</span></span>

<span data-ttu-id="ad099-247">La aplicación admite aprovisionamiento de usuarios Just-In-Time y, tras la autenticación, los usuarios se crean automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad099-247">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="ad099-248">JIT funcionará si ha marcado la casilla **Create Un-recognized User Account** (Crear cuenta de usuario no reconocido) durante la configuración de SAML en el portal de administración de iLMS.</span><span class="sxs-lookup"><span data-stu-id="ad099-248">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="ad099-249">Si debe crear un usuario manualmente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ad099-249">If you need to create an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="ad099-250">Regístrese en el sitio de la compañía de iLMS como administrador.</span><span class="sxs-lookup"><span data-stu-id="ad099-250">Log in to your iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="ad099-251">Haga clic en **"Register User"** (Registrar usuario) en la pestaña **Users** (Usuarios) para abrir la página **Register User** (Registrar usuario).</span><span class="sxs-lookup"><span data-stu-id="ad099-251">Click **“Register User”** under **Users** tab to open **Register User** page.</span></span> 
   
   ![Agregar empleado](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="ad099-253">En la página **"Register User"** (Registrar usuario), realice los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="ad099-253">On the **“Register User”** page, perform the following steps.</span></span>

    ![Agregar empleado](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="ad099-255">a.</span><span class="sxs-lookup"><span data-stu-id="ad099-255">a.</span></span> <span data-ttu-id="ad099-256">En el cuadro de texto **First Name** (Nombre), escriba el nombre Britta.</span><span class="sxs-lookup"><span data-stu-id="ad099-256">In the **First Name** textbox, type the first name Britta.</span></span>
   
    <span data-ttu-id="ad099-257">b.</span><span class="sxs-lookup"><span data-stu-id="ad099-257">b.</span></span> <span data-ttu-id="ad099-258">En el cuadro de texto **Last Name** (Apellido), escriba el apellido Simon.</span><span class="sxs-lookup"><span data-stu-id="ad099-258">In the **Last Name** textbox, type the last name Simon.</span></span>

    <span data-ttu-id="ad099-259">c.</span><span class="sxs-lookup"><span data-stu-id="ad099-259">c.</span></span> <span data-ttu-id="ad099-260">En el cuadro de texto **Email ID** (Id. de correo electrónico), escriba la dirección de correo electrónico de la cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad099-260">In the **Email ID** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="ad099-261">d.</span><span class="sxs-lookup"><span data-stu-id="ad099-261">d.</span></span> <span data-ttu-id="ad099-262">En el menú desplegable **Region** (Región), seleccione el valor de la región.</span><span class="sxs-lookup"><span data-stu-id="ad099-262">In the **Region** dropdown, select the value for region.</span></span>

    <span data-ttu-id="ad099-263">e.</span><span class="sxs-lookup"><span data-stu-id="ad099-263">e.</span></span> <span data-ttu-id="ad099-264">En el menú desplegable **Division** (División), seleccione el valor de la división.</span><span class="sxs-lookup"><span data-stu-id="ad099-264">In the **Division** dropdown, select the value for division.</span></span>

    <span data-ttu-id="ad099-265">f.</span><span class="sxs-lookup"><span data-stu-id="ad099-265">f.</span></span> <span data-ttu-id="ad099-266">En el menú desplegable **Department** (Departamento), seleccione el valor del departamento.</span><span class="sxs-lookup"><span data-stu-id="ad099-266">In the **Department** dropdown, select the value for department.</span></span>

    <span data-ttu-id="ad099-267">g.</span><span class="sxs-lookup"><span data-stu-id="ad099-267">g.</span></span> <span data-ttu-id="ad099-268">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ad099-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ad099-269">Puede enviar un correo electrónico de registro al usuario si selecciona la casilla **Send Registration Mail** (Enviar correo electrónico de registro).</span><span class="sxs-lookup"><span data-stu-id="ad099-269">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ad099-270">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad099-270">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ad099-271">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a iLMS.</span><span class="sxs-lookup"><span data-stu-id="ad099-271">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ad099-273">**Para asignar el usuario Britta Simon a iLMS, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ad099-273">**To assign Britta Simon to iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="ad099-274">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ad099-274">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ad099-276">En la lista de aplicaciones, seleccione **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="ad099-276">In the applications list, select **iLMS**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="ad099-278">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ad099-278">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ad099-280">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ad099-280">Click **Add** button.</span></span> <span data-ttu-id="ad099-281">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ad099-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ad099-283">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ad099-283">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ad099-284">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ad099-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad099-285">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ad099-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad099-286">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ad099-286">Testing single sign-on</span></span>

<span data-ttu-id="ad099-287">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ad099-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ad099-288">Al hacer clic en el icono de iLMS en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de iLMS.</span><span class="sxs-lookup"><span data-stu-id="ad099-288">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad099-289">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ad099-289">Additional resources</span></span>

* [<span data-ttu-id="ad099-290">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad099-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad099-291">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad099-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

