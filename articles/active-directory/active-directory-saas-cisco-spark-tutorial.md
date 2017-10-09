---
title: "Tutorial: Integración de Azure Active Directory con Cisco Spark | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Cisco Spark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="70bb4-103">Tutorial: integración de Azure Active Directory con Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="70bb4-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="70bb4-104">En este tutorial, aprenderá cómo toointegrate Cisco inspirará con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70bb4-104">In this tutorial, you learn how toointegrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70bb4-105">Integración de Cisco Spark con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="70bb4-105">Integrating Cisco Spark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70bb4-106">Puede controlar en Azure AD que tenga acceso tooCisco Spark</span><span class="sxs-lookup"><span data-stu-id="70bb4-106">You can control in Azure AD who has access tooCisco Spark</span></span>
- <span data-ttu-id="70bb4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCisco Spark (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bb4-107">You can enable your users tooautomatically get signed-on tooCisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70bb4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="70bb4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70bb4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70bb4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70bb4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="70bb4-110">Prerequisites</span></span>

<span data-ttu-id="70bb4-111">integración de Azure AD con Cisco Spark tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="70bb4-111">tooconfigure Azure AD integration with Cisco Spark, you need hello following items:</span></span>

- <span data-ttu-id="70bb4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bb4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70bb4-113">Una suscripción habilitada para el inicio de sesión único en Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="70bb4-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70bb4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="70bb4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70bb4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="70bb4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70bb4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="70bb4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70bb4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70bb4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70bb4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="70bb4-118">Scenario description</span></span>
<span data-ttu-id="70bb4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="70bb4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70bb4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="70bb4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70bb4-121">Adición de Cisco Spark desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="70bb4-121">Adding Cisco Spark from hello gallery</span></span>
2. <span data-ttu-id="70bb4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bb4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-hello-gallery"></a><span data-ttu-id="70bb4-123">Adición de Cisco Spark desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="70bb4-123">Adding Cisco Spark from hello gallery</span></span>
<span data-ttu-id="70bb4-124">integración de hello tooconfigure de Cisco Spark en Azure AD, deberá tooadd Cisco Spark en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="70bb4-124">tooconfigure hello integration of Cisco Spark into Azure AD, you need tooadd Cisco Spark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70bb4-125">**tooadd Spark Cisco de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="70bb4-125">**tooadd Cisco Spark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70bb4-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="70bb4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70bb4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70bb4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="70bb4-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70bb4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="70bb4-133">En el cuadro de búsqueda de hello, escriba **Spark de Cisco**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-133">In hello search box, type **Cisco Spark**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="70bb4-135">En el panel de resultados de hello, seleccione **Spark Cisco**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="70bb4-135">In hello results panel, select **Cisco Spark**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70bb4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bb4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70bb4-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Cisco Spark con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="70bb4-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70bb4-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Cisco Spark es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70bb4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cisco Spark is tooa user in Azure AD.</span></span> <span data-ttu-id="70bb4-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Cisco Spark debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="70bb4-140">In other words, a link relationship between an Azure AD user and hello related user in Cisco Spark needs toobe established.</span></span>

<span data-ttu-id="70bb4-141">En Cisco Spark, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="70bb4-141">In Cisco Spark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="70bb4-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Cisco Spark, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="70bb4-142">tooconfigure and test Azure AD single sign-on with Cisco Spark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70bb4-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="70bb4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70bb4-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70bb4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70bb4-145">**[Crear un usuario de prueba de Cisco Spark](#creating-a-cisco-spark-test-user)**  -toohave un equivalente de Britta Simon en Spark Cisco que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="70bb4-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - toohave a counterpart of Britta Simon in Cisco Spark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70bb4-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="70bb4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70bb4-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="70bb4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70bb4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bb4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70bb4-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="70bb4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="70bb4-150">**inicio de sesión único en tooconfigure Azure AD con Cisco Spark, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="70bb4-150">**tooconfigure Azure AD single sign-on with Cisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="70bb4-151">En el portal de Azure, en Hola Hola **Spark Cisco** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-151">In hello Azure portal, on hello **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="70bb4-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="70bb4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="70bb4-155">En hello **Cisco Spark dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="70bb4-155">On hello **Cisco Spark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="70bb4-157">a.</span><span class="sxs-lookup"><span data-stu-id="70bb4-157">a.</span></span> <span data-ttu-id="70bb4-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="70bb4-158">In hello **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="70bb4-159">b.</span><span class="sxs-lookup"><span data-stu-id="70bb4-159">b.</span></span> <span data-ttu-id="70bb4-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="70bb4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70bb4-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="70bb4-161">This value is not real.</span></span> <span data-ttu-id="70bb4-162">Actualice este valor con hello identificador real.</span><span class="sxs-lookup"><span data-stu-id="70bb4-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="70bb4-163">Póngase en contacto con [equipo de soporte técnico de Cisco Spark cliente](https://support.ciscospark.com/) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="70bb4-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) tooget this value.</span></span> 
 
4. <span data-ttu-id="70bb4-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="70bb4-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="70bb4-166">Aplicación de Cisco Spark espera atributos específicos del toocontain de aserciones SAML Hola.</span><span class="sxs-lookup"><span data-stu-id="70bb4-166">Cisco Spark application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="70bb4-167">Configurar Hola siguientes atributos para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="70bb4-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="70bb4-168">Puede administrar valores de hello de estos atributos de hello **atributos de usuario** sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="70bb4-168">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="70bb4-169">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="70bb4-169">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="70bb4-171">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="70bb4-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="70bb4-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="70bb4-172">Attribute Name</span></span>  | <span data-ttu-id="70bb4-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="70bb4-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="70bb4-174">uid</span><span class="sxs-lookup"><span data-stu-id="70bb4-174">uid</span></span>    | <span data-ttu-id="70bb4-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="70bb4-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="70bb4-176">a.</span><span class="sxs-lookup"><span data-stu-id="70bb4-176">a.</span></span> <span data-ttu-id="70bb4-177">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70bb4-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="70bb4-180">b.</span><span class="sxs-lookup"><span data-stu-id="70bb4-180">b.</span></span> <span data-ttu-id="70bb4-181">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="70bb4-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="70bb4-182">c.</span><span class="sxs-lookup"><span data-stu-id="70bb4-182">c.</span></span> <span data-ttu-id="70bb4-183">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="70bb4-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="70bb4-184">d.</span><span class="sxs-lookup"><span data-stu-id="70bb4-184">d.</span></span> <span data-ttu-id="70bb4-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-185">Click **Ok**.</span></span>

7. <span data-ttu-id="70bb4-186">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="70bb4-186">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="70bb4-188">Inicie sesión en demasiado[administración de colaboración de nube de Cisco](https://admin.ciscospark.com/) con sus credenciales de administrador total.</span><span class="sxs-lookup"><span data-stu-id="70bb4-188">Sign in too[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="70bb4-189">Seleccione **configuración** y en hello **autenticación** sección, haga clic en **modificar**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-189">Select **Settings** and under hello **Authentication** section, click **Modify**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="70bb4-191">Seleccione **Integrate a 3rd-party identity provider. (Avanzado)**  y vaya toohello siguiente pantalla.</span><span class="sxs-lookup"><span data-stu-id="70bb4-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go toohello next screen.</span></span>

11. <span data-ttu-id="70bb4-192">En hello **importar metadatos de Idp** página, ya sea arrastrar y colocar el archivo de metadatos de hello Azure AD en la página de Hola o utilizar Hola archivo explorador opción toolocate y cargar archivo de metadatos de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70bb4-192">On hello **Import Idp Metadata** page, either drag and drop hello Azure AD metadata file onto hello page or use hello file browser option toolocate and upload hello Azure AD metadata file.</span></span> <span data-ttu-id="70bb4-193">Después, seleccione **Require certificate signed by a certificate authority in Metadata (more secure)** (Requerir certificado firmado por una entidad de certificación en metadatos [más seguro]) y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="70bb4-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="70bb4-195">Seleccione **Test SSO Connection** (Probar SSO de conexión) y cuando se abra una nueva pestaña de explorador, autentíquese con Azure AD mediante el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="70bb4-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="70bb4-196">Devolver toohello **administración de colaboración de nube de Cisco** pestaña del explorador. Si prueba Hola fue correcta, seleccione **esta prueba fue correcta. Enable Single Sign-On option** (Esta prueba se realizó correctamente. Habilite la opción de inicio de sesión único) y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="70bb4-196">Return toohello **Cisco Cloud Collaboration Management** browser tab. If hello test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="70bb4-197">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="70bb4-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70bb4-198">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="70bb4-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70bb4-199">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70bb4-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70bb4-200">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bb4-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="70bb4-201">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="70bb4-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="70bb4-203">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="70bb4-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70bb4-204">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="70bb4-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70bb4-206">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70bb4-208">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="70bb4-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70bb4-210">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="70bb4-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70bb4-212">a.</span><span class="sxs-lookup"><span data-stu-id="70bb4-212">a.</span></span> <span data-ttu-id="70bb4-213">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70bb4-214">b.</span><span class="sxs-lookup"><span data-stu-id="70bb4-214">b.</span></span> <span data-ttu-id="70bb4-215">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="70bb4-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70bb4-216">c.</span><span class="sxs-lookup"><span data-stu-id="70bb4-216">c.</span></span> <span data-ttu-id="70bb4-217">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70bb4-218">d.</span><span class="sxs-lookup"><span data-stu-id="70bb4-218">d.</span></span> <span data-ttu-id="70bb4-219">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="70bb4-220">Creación de un usuario de prueba de Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="70bb4-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="70bb4-221">En esta sección, creará un usuario llamado Britta Simon en Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="70bb4-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="70bb4-222">En esta sección, creará un usuario llamado Britta Simon en Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="70bb4-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="70bb4-223">Vaya toohello [administración de colaboración de nube de Cisco](https://admin.ciscospark.com/) con sus credenciales de administrador total.</span><span class="sxs-lookup"><span data-stu-id="70bb4-223">Go toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="70bb4-224">Haga clic en **Usuarios** y después en **Administrar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="70bb4-226">Hola **administrar usuario** ventana, seleccione **agregar o modificar los usuarios de forma manual** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-226">In hello **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="70bb4-227">Seleccione **Names and Email address** (Nombres y direcciones de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="70bb4-227">Select **Names and Email address**.</span></span> <span data-ttu-id="70bb4-228">A continuación, rellene el cuadro de texto de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="70bb4-228">Then, fill out hello textbox as follows:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="70bb4-230">a.</span><span class="sxs-lookup"><span data-stu-id="70bb4-230">a.</span></span> <span data-ttu-id="70bb4-231">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-231">In hello **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="70bb4-232">b.</span><span class="sxs-lookup"><span data-stu-id="70bb4-232">b.</span></span> <span data-ttu-id="70bb4-233">Hola **Last Name** cuadro de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-233">In hello **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="70bb4-234">c.</span><span class="sxs-lookup"><span data-stu-id="70bb4-234">c.</span></span> <span data-ttu-id="70bb4-235">Hola **dirección de correo electrónico** cuadro de texto, tipo  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="70bb4-235">In hello **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="70bb4-236">Haga clic en hello además de iniciar sesión tooadd Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70bb4-236">Click hello plus sign tooadd Britta Simon.</span></span> <span data-ttu-id="70bb4-237">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-237">Then, click **Next**.</span></span>

6. <span data-ttu-id="70bb4-238">Hola **agregar servicios a los usuarios** ventana, haga clic en **guardar** y, a continuación, **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-238">In hello **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70bb4-239">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bb4-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70bb4-240">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCisco Spark.</span><span class="sxs-lookup"><span data-stu-id="70bb4-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCisco Spark.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="70bb4-242">**tooassign Britta Simon tooCisco Spark, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="70bb4-242">**tooassign Britta Simon tooCisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="70bb4-243">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="70bb4-245">En la lista de aplicaciones de hello, seleccione **Spark de Cisco**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-245">In hello applications list, select **Cisco Spark**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="70bb4-247">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="70bb4-249">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-249">Click **Add** button.</span></span> <span data-ttu-id="70bb4-250">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="70bb4-252">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="70bb4-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70bb4-253">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70bb4-254">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="70bb4-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70bb4-255">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="70bb4-255">Testing single sign-on</span></span>

<span data-ttu-id="70bb4-256">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="70bb4-256">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="70bb4-257">Al hacer clic en icono de Cisco Spark Hola Hola Panel de acceso, deberá obtener la aplicación de Cisco Spark tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="70bb4-257">When you click hello Cisco Spark tile in hello Access Panel, you should get automatically signed-on tooyour Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70bb4-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="70bb4-258">Additional resources</span></span>

* [<span data-ttu-id="70bb4-259">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70bb4-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70bb4-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="70bb4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

