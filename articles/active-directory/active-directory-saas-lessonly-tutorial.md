---
title: "Tutorial: integración de Azure Active Directory con Lesson.ly | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Lesson.ly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fc1e1b2de0a138dbe88d794f802b002321948ab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="c1689-103">Tutorial: Integración de Azure Active Directory con Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="c1689-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="c1689-104">En este tutorial se aprende a integrar Lesson.ly con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1689-104">In this tutorial, you learn how to integrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1689-105">Integrar Lesson.ly con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c1689-105">Integrating Lesson.ly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c1689-106">Puede controlar en Azure AD quién tiene acceso a Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="c1689-106">You can control in Azure AD who has access to Lesson.ly</span></span>
- <span data-ttu-id="c1689-107">Puede permitir que los usuarios inicien sesión automáticamente en Lesson.ly (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1689-107">You can enable your users to automatically get signed-on to Lesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1689-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c1689-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c1689-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1689-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1689-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c1689-110">Prerequisites</span></span>

<span data-ttu-id="c1689-111">Para configurar la integración de Azure AD con Lesson.ly, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c1689-111">To configure Azure AD integration with Lesson.ly, you need the following items:</span></span>

- <span data-ttu-id="c1689-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1689-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1689-113">Una suscripción habilitada para el inicio de sesión único en Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="c1689-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1689-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c1689-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1689-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c1689-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1689-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c1689-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1689-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1689-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1689-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c1689-118">Scenario description</span></span>
<span data-ttu-id="c1689-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c1689-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1689-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="c1689-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1689-121">Adición de Lesson.ly desde la galería</span><span class="sxs-lookup"><span data-stu-id="c1689-121">Adding Lesson.ly from the gallery</span></span>
2. <span data-ttu-id="c1689-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1689-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-the-gallery"></a><span data-ttu-id="c1689-123">Adición de Lesson.ly desde la galería</span><span class="sxs-lookup"><span data-stu-id="c1689-123">Adding Lesson.ly from the gallery</span></span>
<span data-ttu-id="c1689-124">Para configurar la integración de Lesson.ly en Azure AD, es preciso agregar Lesson.ly desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="c1689-124">To configure the integration of Lesson.ly into Azure AD, you need to add Lesson.ly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c1689-125">**Para agregar Lesson.ly desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c1689-125">**To add Lesson.ly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c1689-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1689-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1689-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c1689-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c1689-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c1689-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c1689-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c1689-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c1689-133">En el cuadro de búsqueda, escriba **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="c1689-133">In the search box, type **Lesson.ly**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="c1689-135">En el panel de resultados, seleccione **Lesson.ly** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c1689-135">In the results panel, select **Lesson.ly**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1689-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1689-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1689-138">En esta sección se configura y prueba el inicio de sesión único de Azure AD con Lesson.ly con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c1689-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c1689-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Lesson.ly para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1689-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lesson.ly is to a user in Azure AD.</span></span> <span data-ttu-id="c1689-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="c1689-140">In other words, a link relationship between an Azure AD user and the related user in Lesson.ly needs to be established.</span></span>

<span data-ttu-id="c1689-141">Para establecer la relación de vínculo, en Lesson.ly, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c1689-141">In Lesson.ly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c1689-142">Para configurar y probar el inicio de sesión único de Azure AD con Lesson.ly, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c1689-142">To configure and test Azure AD single sign-on with Lesson.ly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c1689-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="c1689-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c1689-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1689-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1689-145">**[Creación de un usuario de prueba de Lesson.ly](#creating-a-lessonly-test-user)**: para tener un homólogo de Britta Simon en Lesson.ly vinculado a la representación de usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1689-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - to have a counterpart of Britta Simon in Lesson.ly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1689-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1689-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1689-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c1689-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1689-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1689-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1689-149">En esta sección se habilita el inicio de sesión único de Azure AD en Azure Portal y se configura el inicio de sesión único en la aplicación Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="c1689-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="c1689-150">**Para configurar el inicio de sesión único de Azure AD con Lesson.ly, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c1689-150">**To configure Azure AD single sign-on with Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="c1689-151">En Azure Portal, en la página de integración de la aplicación **Lesson.ly**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c1689-151">In the Azure portal, on the **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c1689-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c1689-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="c1689-155">En la sección **Dominio y direcciones URL de Lesson.ly**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c1689-155">On the **Lesson.ly Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="c1689-157">a.</span><span class="sxs-lookup"><span data-stu-id="c1689-157">a.</span></span> <span data-ttu-id="c1689-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="c1689-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="c1689-159">Cuando se hace referencia a un nombre genérico, debe reemplazar **nombreDeCompañía** por un nombre real.</span><span class="sxs-lookup"><span data-stu-id="c1689-159">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span></span>
    
    <span data-ttu-id="c1689-160">b.</span><span class="sxs-lookup"><span data-stu-id="c1689-160">b.</span></span> <span data-ttu-id="c1689-161">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="c1689-161">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="c1689-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c1689-162">These values are not real.</span></span> <span data-ttu-id="c1689-163">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="c1689-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c1689-164">Contacte con el [equipo de soporte técnico de cliente de Lesson.ly](mailto:dev@lessonly.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="c1689-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) to get these values.</span></span> 

4. <span data-ttu-id="c1689-165">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c1689-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="c1689-167">La aplicación Lesson.ly espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los **atributos del token de SAML**. La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="c1689-167">The Lesson.ly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.The following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="c1689-169">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo del token de SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c1689-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="c1689-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="c1689-170">Attribute Name</span></span>   | <span data-ttu-id="c1689-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="c1689-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="c1689-172">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="c1689-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="c1689-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c1689-173">user.givenname</span></span> |
    | <span data-ttu-id="c1689-174">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="c1689-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="c1689-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="c1689-175">user.surname</span></span> |
    | <span data-ttu-id="c1689-176">urn:oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="c1689-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="c1689-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="c1689-177">user.mail</span></span> |

    <span data-ttu-id="c1689-178">a.</span><span class="sxs-lookup"><span data-stu-id="c1689-178">a.</span></span> <span data-ttu-id="c1689-179">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="c1689-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c1689-182">b.</span><span class="sxs-lookup"><span data-stu-id="c1689-182">b.</span></span> <span data-ttu-id="c1689-183">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="c1689-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="c1689-184">c.</span><span class="sxs-lookup"><span data-stu-id="c1689-184">c.</span></span> <span data-ttu-id="c1689-185">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="c1689-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c1689-186">d.</span><span class="sxs-lookup"><span data-stu-id="c1689-186">d.</span></span> <span data-ttu-id="c1689-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c1689-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="c1689-188">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c1689-188">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c1689-190">En la sección **Configuración de Lesson.ly**, haga clic en **Configurar Lesson.ly** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="c1689-190">On the **Lesson.ly Configuration** section, click **Configure Lesson.ly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c1689-191">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="c1689-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="c1689-193">Para configurar el inicio de sesión único en **Lesson.ly**, es preciso enviar el **Certificado (Base64)** descargado, la **dirección URL de cierre de sesión, el identificador de identidad de SAML y la dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="c1689-193">To configure single sign-on on **Lesson.ly** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="c1689-194">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c1689-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c1689-195">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c1689-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c1689-196">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c1689-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1689-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1689-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1689-198">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c1689-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c1689-200">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c1689-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c1689-201">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1689-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1689-203">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c1689-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1689-205">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c1689-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1689-207">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c1689-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1689-209">a.</span><span class="sxs-lookup"><span data-stu-id="c1689-209">a.</span></span> <span data-ttu-id="c1689-210">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1689-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1689-211">b.</span><span class="sxs-lookup"><span data-stu-id="c1689-211">b.</span></span> <span data-ttu-id="c1689-212">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1689-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1689-213">c.</span><span class="sxs-lookup"><span data-stu-id="c1689-213">c.</span></span> <span data-ttu-id="c1689-214">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c1689-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c1689-215">d.</span><span class="sxs-lookup"><span data-stu-id="c1689-215">d.</span></span> <span data-ttu-id="c1689-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c1689-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="c1689-217">Creación de un usuario de prueba de Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="c1689-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="c1689-218">El objetivo de esta sección es crear un usuario llamado a Britta Simon en Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="c1689-218">The objective of this section is to create a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="c1689-219">Lesson.ly admite el aprovisionamiento Just-In-Time, que está habilitado de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c1689-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="c1689-220">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="c1689-220">There is no action item for you in this section.</span></span> <span data-ttu-id="c1689-221">Durante un intento de acceder a Lesson.ly se creará un nuevo usuario, si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="c1689-221">A new user will be created during an attempt to access Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="c1689-222">Si necesita crear un usuario manualmente, es preciso que contacte con el [equipo de soporte técnico de Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="c1689-222">If you need to create an user manually, you need to contact the [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c1689-223">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1689-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c1689-224">En esta sección se habilita a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="c1689-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lesson.ly.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c1689-226">**Para asignar Britta Simon a Lesson.ly, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c1689-226">**To assign Britta Simon to Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="c1689-227">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c1689-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c1689-229">En la lista de aplicaciones, seleccione **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="c1689-229">In the applications list, select **Lesson.ly**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="c1689-231">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c1689-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c1689-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c1689-233">Click **Add** button.</span></span> <span data-ttu-id="c1689-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c1689-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c1689-236">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c1689-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c1689-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c1689-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1689-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c1689-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1689-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c1689-239">Testing single sign-on</span></span>

<span data-ttu-id="c1689-240">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c1689-240">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c1689-241">Al hacer clic en el icono de Lesson.ly en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="c1689-241">When you click the Lesson.ly tile in the Access Panel, you should get automatically signed-on to your Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c1689-242">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c1689-242">Additional resources</span></span>

* [<span data-ttu-id="c1689-243">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1689-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1689-244">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c1689-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

