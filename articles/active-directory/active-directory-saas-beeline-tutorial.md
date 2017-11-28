---
title: "Tutorial: Integración de Azure Active Directory con BeeLine | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y BeeLine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 92f228d33980c21ad934185ab89d73795f7f69bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="6d552-103">Tutorial: Integración de Azure Active Directory con BeeLine</span><span class="sxs-lookup"><span data-stu-id="6d552-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="6d552-104">En este tutorial, aprenderá cómo toointegrate BeeLine con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d552-104">In this tutorial, you learn how toointegrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d552-105">Integración BeeLine con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6d552-105">Integrating BeeLine with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6d552-106">Puede controlar en Azure AD que tenga acceso tooBeeLine</span><span class="sxs-lookup"><span data-stu-id="6d552-106">You can control in Azure AD who has access tooBeeLine</span></span>
- <span data-ttu-id="6d552-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBeeLine (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d552-107">You can enable your users tooautomatically get signed-on tooBeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d552-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6d552-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6d552-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d552-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d552-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6d552-110">Prerequisites</span></span>

<span data-ttu-id="6d552-111">integración de Azure AD con BeeLine tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6d552-111">tooconfigure Azure AD integration with BeeLine, you need hello following items:</span></span>

- <span data-ttu-id="6d552-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d552-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d552-113">Una suscripción habilitada para inicio de sesión único en BeeLine</span><span class="sxs-lookup"><span data-stu-id="6d552-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d552-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6d552-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d552-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6d552-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d552-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6d552-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d552-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d552-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d552-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6d552-118">Scenario description</span></span>
<span data-ttu-id="6d552-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6d552-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d552-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="6d552-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d552-121">Agregar BeeLine desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6d552-121">Adding BeeLine from hello gallery</span></span>
2. <span data-ttu-id="6d552-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d552-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-hello-gallery"></a><span data-ttu-id="6d552-123">Agregar BeeLine desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6d552-123">Adding BeeLine from hello gallery</span></span>
<span data-ttu-id="6d552-124">integración de hello tooconfigure de BeeLine en Azure AD, deberá tooadd BeeLine de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="6d552-124">tooconfigure hello integration of BeeLine into Azure AD, you need tooadd BeeLine from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6d552-125">**tooadd BeeLine de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6d552-125">**tooadd BeeLine from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d552-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6d552-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6d552-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6d552-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6d552-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6d552-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="6d552-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d552-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="6d552-133">En el cuadro de búsqueda de hello, escriba **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="6d552-133">In hello search box, type **BeeLine**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="6d552-135">En el panel de resultados de hello, seleccione **BeeLine**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6d552-135">In hello results panel, select **BeeLine**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d552-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d552-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d552-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con BeeLine con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6d552-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6d552-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en BeeLine es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d552-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BeeLine is tooa user in Azure AD.</span></span> <span data-ttu-id="6d552-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en BeeLine debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="6d552-140">In other words, a link relationship between an Azure AD user and hello related user in BeeLine needs toobe established.</span></span>

<span data-ttu-id="6d552-141">En BeeLine, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d552-141">In BeeLine, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6d552-142">tooconfigure y prueba de inicio de sesión único en Azure AD con BeeLine, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6d552-142">tooconfigure and test Azure AD single sign-on with BeeLine, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6d552-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="6d552-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6d552-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d552-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d552-145">**[Crear un usuario de prueba BeeLine](#creating-a-beeline-test-user)**  -toohave un equivalente de Britta Simon en BeeLine que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="6d552-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - toohave a counterpart of Britta Simon in BeeLine that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6d552-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6d552-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d552-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6d552-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d552-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d552-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6d552-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación BeeLine.</span><span class="sxs-lookup"><span data-stu-id="6d552-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="6d552-150">**inicio de sesión único en Azure AD tooconfigure con BeeLine, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6d552-150">**tooconfigure Azure AD single sign-on with BeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d552-151">En el portal de Azure, en Hola Hola **BeeLine** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6d552-151">In hello Azure portal, on hello **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="6d552-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6d552-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="6d552-155">En hello **BeeLine dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6d552-155">On hello **BeeLine Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="6d552-157">a.</span><span class="sxs-lookup"><span data-stu-id="6d552-157">a.</span></span> <span data-ttu-id="6d552-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="6d552-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="6d552-159">b.</span><span class="sxs-lookup"><span data-stu-id="6d552-159">b.</span></span> <span data-ttu-id="6d552-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="6d552-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="6d552-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="6d552-161">These values are not real.</span></span> <span data-ttu-id="6d552-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="6d552-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="6d552-163">Póngase en contacto con [equipo de soporte técnico de BeeLine](https://www.beeline.com/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="6d552-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) tooget these values.</span></span>
 
4. <span data-ttu-id="6d552-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6d552-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="6d552-166">La aplicación de Beeline espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="6d552-166">Your Beeline application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="6d552-167">Trabaje con [equipo de soporte técnico de BeeLine](https://www.beeline.com/contact-us/) tooidentify primera Hola identificador de usuario correctos que se asignarán a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6d552-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first tooidentify hello correct user identifier which will be mapped into hello application.</span></span> <span data-ttu-id="6d552-168">Dedique también instrucciones de Hola de [equipo de soporte técnico de BeeLine](https://www.beeline.com/contact-us/) sobre Hola de atributo que deseen toouse para esta asignación.</span><span class="sxs-lookup"><span data-stu-id="6d552-168">Also please take hello guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about hello attribute which they want toouse for this mapping.</span></span> <span data-ttu-id="6d552-169">Puede administrar valor Hola de este atributo de hello **atributos de usuario** pestaña de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6d552-169">You can manage hello value of this attribute from hello **User Attributes** tab of hello application.</span></span> <span data-ttu-id="6d552-170">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="6d552-170">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="6d552-171">Aquí hemos asignamos hello **identificador de usuario** una notificación con hello **userprincipalname** atributo, que proporciona el identificador de usuario único, que será enviado toohello Beeline aplicación Hola cada SAML correcta Respuesta.</span><span class="sxs-lookup"><span data-stu-id="6d552-171">Here we have mapped hello **User Identifier** claim with hello **userprincipalname** attribute, which provides unique user ID, which will be sent toohello Beeline application in hello every successful SAML Response.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="6d552-173">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6d552-173">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6d552-175">En hello **BeeLine configuración** sección, haga clic en **configurar BeeLine** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="6d552-175">On hello **BeeLine Configuration** section, click **Configure BeeLine** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6d552-176">Hola copia **dirección URL de cierre de sesión** y **Id. de entidad SAML** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="6d552-176">Copy hello **Sign-Out URL** and **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="6d552-178">tooconfigure inicio de sesión único en **BeeLine** lado, necesita hello toosend descargado **Metadata XML** y **Id. de entidad SAML**, **URL de cierre de sesión**demasiado[equipo de soporte técnico de BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="6d552-178">tooconfigure single sign-on on **BeeLine** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** too[BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="6d552-179">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="6d552-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6d552-180">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="6d552-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6d552-181">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d552-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d552-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d552-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d552-183">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="6d552-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="6d552-185">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6d552-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d552-186">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6d552-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d552-188">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6d552-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d552-190">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d552-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d552-192">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="6d552-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d552-194">a.</span><span class="sxs-lookup"><span data-stu-id="6d552-194">a.</span></span> <span data-ttu-id="6d552-195">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6d552-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d552-196">b.</span><span class="sxs-lookup"><span data-stu-id="6d552-196">b.</span></span> <span data-ttu-id="6d552-197">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6d552-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6d552-198">c.</span><span class="sxs-lookup"><span data-stu-id="6d552-198">c.</span></span> <span data-ttu-id="6d552-199">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6d552-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6d552-200">d.</span><span class="sxs-lookup"><span data-stu-id="6d552-200">d.</span></span> <span data-ttu-id="6d552-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6d552-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="6d552-202">Creación de un usuario de prueba de BeeLine</span><span class="sxs-lookup"><span data-stu-id="6d552-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="6d552-203">En esta sección, creará un usuario llamado Britta Simon en Beeline.</span><span class="sxs-lookup"><span data-stu-id="6d552-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="6d552-204">Aplicación de BEELINE necesita todos los toobe de los usuarios de hello aprovisionado en aplicación hello antes de realizar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6d552-204">Beeline application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="6d552-205">Por lo que funcionan con hello [equipo de soporte técnico de BeeLine](https://www.beeline.com/contact-us/) tooprovision todos estos usuarios en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6d552-205">So work with hello [BeeLine support team](https://www.beeline.com/contact-us/) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6d552-206">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d552-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6d552-207">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBeeLine.</span><span class="sxs-lookup"><span data-stu-id="6d552-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBeeLine.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="6d552-209">**tooassign Britta Simon tooBeeLine, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6d552-209">**tooassign Britta Simon tooBeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d552-210">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6d552-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6d552-212">En la lista de aplicaciones de hello, seleccione **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="6d552-212">In hello applications list, select **BeeLine**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="6d552-214">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6d552-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="6d552-216">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6d552-216">Click **Add** button.</span></span> <span data-ttu-id="6d552-217">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6d552-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="6d552-219">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d552-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6d552-220">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6d552-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d552-221">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6d552-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6d552-222">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="6d552-222">Testing single sign-on</span></span>

<span data-ttu-id="6d552-223">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6d552-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="6d552-224">Al hacer clic en icono de Beeline Hola Hola Panel de acceso, deberá obtener la aplicación de Beeline tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="6d552-224">When you click hello Beeline tile in hello Access Panel, you should get automatically signed-on tooyour Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6d552-225">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6d552-225">Additional resources</span></span>

* [<span data-ttu-id="6d552-226">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d552-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d552-227">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d552-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

