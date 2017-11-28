---
title: "Tutorial: integración de Azure Active Directory con Lesson.ly | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Lesson.ly."
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
ms.openlocfilehash: 23b339dcc26471b42aaa7e1baadcb42500d6b7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="fb0eb-103">Tutorial: Integración de Azure Active Directory con Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="fb0eb-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="fb0eb-104">En este tutorial, aprenderá cómo toointegrate Lesson.ly con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb0eb-104">In this tutorial, you learn how toointegrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb0eb-105">Integración Lesson.ly con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fb0eb-105">Integrating Lesson.ly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fb0eb-106">Puede controlar en Azure AD que tenga acceso tooLesson.ly</span><span class="sxs-lookup"><span data-stu-id="fb0eb-106">You can control in Azure AD who has access tooLesson.ly</span></span>
- <span data-ttu-id="fb0eb-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLesson.ly (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb0eb-107">You can enable your users tooautomatically get signed-on tooLesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fb0eb-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fb0eb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fb0eb-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb0eb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb0eb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb0eb-110">Prerequisites</span></span>

<span data-ttu-id="fb0eb-111">integración de Azure AD con Lesson.ly tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fb0eb-111">tooconfigure Azure AD integration with Lesson.ly, you need hello following items:</span></span>

- <span data-ttu-id="fb0eb-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb0eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb0eb-113">Una suscripción habilitada para el inicio de sesión único en Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="fb0eb-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb0eb-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb0eb-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fb0eb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb0eb-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb0eb-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb0eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb0eb-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fb0eb-118">Scenario description</span></span>
<span data-ttu-id="fb0eb-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb0eb-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="fb0eb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb0eb-121">Agregar Lesson.ly desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fb0eb-121">Adding Lesson.ly from hello gallery</span></span>
2. <span data-ttu-id="fb0eb-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb0eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-hello-gallery"></a><span data-ttu-id="fb0eb-123">Agregar Lesson.ly desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fb0eb-123">Adding Lesson.ly from hello gallery</span></span>
<span data-ttu-id="fb0eb-124">integración de hello tooconfigure de Lesson.ly en Azure AD, deberá tooadd Lesson.ly de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-124">tooconfigure hello integration of Lesson.ly into Azure AD, you need tooadd Lesson.ly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fb0eb-125">**tooadd Lesson.ly de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb0eb-125">**tooadd Lesson.ly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb0eb-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fb0eb-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fb0eb-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="fb0eb-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="fb0eb-133">En el cuadro de búsqueda de hello, escriba **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-133">In hello search box, type **Lesson.ly**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="fb0eb-135">En el panel de resultados de hello, seleccione **Lesson.ly**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-135">In hello results panel, select **Lesson.ly**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fb0eb-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb0eb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fb0eb-138">En esta sección se configura y prueba el inicio de sesión único de Azure AD con Lesson.ly con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fb0eb-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fb0eb-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Lesson.ly es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lesson.ly is tooa user in Azure AD.</span></span> <span data-ttu-id="fb0eb-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Lesson.ly debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-140">In other words, a link relationship between an Azure AD user and hello related user in Lesson.ly needs toobe established.</span></span>

<span data-ttu-id="fb0eb-141">En Lesson.ly, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-141">In Lesson.ly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fb0eb-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Lesson.ly, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fb0eb-142">tooconfigure and test Azure AD single sign-on with Lesson.ly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fb0eb-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fb0eb-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb0eb-145">**[Crear un usuario de prueba Lesson.ly](#creating-a-lessonly-test-user)**  -toohave un equivalente de Britta Simon en Lesson.ly que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - toohave a counterpart of Britta Simon in Lesson.ly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb0eb-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb0eb-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fb0eb-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb0eb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fb0eb-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="fb0eb-150">**inicio de sesión único en Azure AD tooconfigure con Lesson.ly, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb0eb-150">**tooconfigure Azure AD single sign-on with Lesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb0eb-151">En el portal de Azure, en Hola Hola **Lesson.ly** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-151">In hello Azure portal, on hello **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="fb0eb-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="fb0eb-155">En hello **Lesson.ly dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fb0eb-155">On hello **Lesson.ly Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="fb0eb-157">a.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-157">a.</span></span> <span data-ttu-id="fb0eb-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="fb0eb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="fb0eb-159">Cuando se hace referencia a un tipo genérico nombre que **companyname** necesita toobe reemplazado por un nombre real.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-159">When referencing a generic name that **companyname** needs toobe replaced by an actual name.</span></span>
    
    <span data-ttu-id="fb0eb-160">b.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-160">b.</span></span> <span data-ttu-id="fb0eb-161">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="fb0eb-161">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="fb0eb-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-162">These values are not real.</span></span> <span data-ttu-id="fb0eb-163">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fb0eb-164">Póngase en contacto con [equipo de soporte técnico de cliente de Lesson.ly](mailto:dev@lessonly.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) tooget these values.</span></span> 

4. <span data-ttu-id="fb0eb-165">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="fb0eb-167">Hola Lesson.ly aplicación espera las aserciones de SAML de hello en un formato específico, lo que requiere tooyour de asignaciones de atributo personalizado de tooadd **atributos de Token SAML** configuration.hello siguiente captura de pantalla muestra un ejemplo para Este.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-167">hello Lesson.ly application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.hello following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="fb0eb-169">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en hello delante de la imagen y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fb0eb-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="fb0eb-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="fb0eb-170">Attribute Name</span></span>   | <span data-ttu-id="fb0eb-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="fb0eb-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="fb0eb-172">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="fb0eb-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="fb0eb-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="fb0eb-173">user.givenname</span></span> |
    | <span data-ttu-id="fb0eb-174">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="fb0eb-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="fb0eb-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="fb0eb-175">user.surname</span></span> |
    | <span data-ttu-id="fb0eb-176">urn:oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="fb0eb-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="fb0eb-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="fb0eb-177">user.mail</span></span> |

    <span data-ttu-id="fb0eb-178">a.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-178">a.</span></span> <span data-ttu-id="fb0eb-179">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="fb0eb-182">b.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-182">b.</span></span> <span data-ttu-id="fb0eb-183">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="fb0eb-184">c.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-184">c.</span></span> <span data-ttu-id="fb0eb-185">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="fb0eb-186">d.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-186">d.</span></span> <span data-ttu-id="fb0eb-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="fb0eb-188">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fb0eb-188">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fb0eb-190">En hello **Lesson.ly configuración** sección, haga clic en **configurar Lesson.ly** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-190">On hello **Lesson.ly Configuration** section, click **Configure Lesson.ly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fb0eb-191">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="fb0eb-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="fb0eb-193">inicio de sesión único en tooconfigure en **Lesson.ly** lado, necesita hello toosend descargado **Certificate(Base64)** y **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** demasiado[equipo de soporte técnico de Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="fb0eb-193">tooconfigure single sign-on on **Lesson.ly** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="fb0eb-194">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="fb0eb-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fb0eb-195">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fb0eb-196">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fb0eb-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fb0eb-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb0eb-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="fb0eb-198">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="fb0eb-200">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb0eb-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb0eb-201">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fb0eb-203">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fb0eb-205">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fb0eb-207">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="fb0eb-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fb0eb-209">a.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-209">a.</span></span> <span data-ttu-id="fb0eb-210">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb0eb-211">b.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-211">b.</span></span> <span data-ttu-id="fb0eb-212">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fb0eb-213">c.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-213">c.</span></span> <span data-ttu-id="fb0eb-214">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fb0eb-215">d.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-215">d.</span></span> <span data-ttu-id="fb0eb-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="fb0eb-217">Creación de un usuario de prueba de Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="fb0eb-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="fb0eb-218">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Lesson.ly toocreate.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-218">hello objective of this section is toocreate a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="fb0eb-219">Lesson.ly admite el aprovisionamiento Just-In-Time, que está habilitado de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fb0eb-220">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-220">There is no action item for you in this section.</span></span> <span data-ttu-id="fb0eb-221">Si no existe todavía, se creará un nuevo usuario durante un tooaccess intento Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-221">A new user will be created during an attempt tooaccess Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="fb0eb-222">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="fb0eb-222">If you need toocreate an user manually, you need toocontact hello [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fb0eb-223">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb0eb-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fb0eb-224">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLesson.ly.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLesson.ly.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="fb0eb-226">**tooassign Britta Simon tooLesson.ly, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fb0eb-226">**tooassign Britta Simon tooLesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb0eb-227">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fb0eb-229">En la lista de aplicaciones de hello, seleccione **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-229">In hello applications list, select **Lesson.ly**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="fb0eb-231">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="fb0eb-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-233">Click **Add** button.</span></span> <span data-ttu-id="fb0eb-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="fb0eb-236">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fb0eb-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb0eb-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fb0eb-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="fb0eb-239">Testing single sign-on</span></span>

<span data-ttu-id="fb0eb-240">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-240">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fb0eb-241">Al hacer clic en icono de Lesson.ly Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Lesson.ly aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb0eb-241">When you click hello Lesson.ly tile in hello Access Panel, you should get automatically signed-on tooyour Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb0eb-242">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fb0eb-242">Additional resources</span></span>

* [<span data-ttu-id="fb0eb-243">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb0eb-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb0eb-244">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb0eb-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

