---
title: "Tutorial: integración de Azure Active Directory con IdeaScale | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="36318-103">Tutorial: integración de Azure Active Directory con IdeaScale</span><span class="sxs-lookup"><span data-stu-id="36318-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="36318-104">En este tutorial, aprenderá cómo toointegrate IdeaScale con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36318-104">In this tutorial, you learn how toointegrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36318-105">Integración de IdeaScale con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="36318-105">Integrating IdeaScale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="36318-106">Puede controlar en Azure AD que tenga acceso tooIdeaScale</span><span class="sxs-lookup"><span data-stu-id="36318-106">You can control in Azure AD who has access tooIdeaScale</span></span>
- <span data-ttu-id="36318-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooIdeaScale (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36318-107">You can enable your users tooautomatically get signed-on tooIdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36318-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="36318-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="36318-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36318-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36318-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="36318-110">Prerequisites</span></span>

<span data-ttu-id="36318-111">integración de Azure AD con IdeaScale tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="36318-111">tooconfigure Azure AD integration with IdeaScale, you need hello following items:</span></span>

- <span data-ttu-id="36318-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36318-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36318-113">Una suscripción habilitada para el inicio de sesión único en IdeaScale</span><span class="sxs-lookup"><span data-stu-id="36318-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36318-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="36318-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36318-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="36318-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36318-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="36318-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36318-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36318-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36318-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="36318-118">Scenario description</span></span>
<span data-ttu-id="36318-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="36318-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36318-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="36318-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36318-121">Agregar IdeaScale desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="36318-121">Adding IdeaScale from hello gallery</span></span>
2. <span data-ttu-id="36318-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36318-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-hello-gallery"></a><span data-ttu-id="36318-123">Agregar IdeaScale desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="36318-123">Adding IdeaScale from hello gallery</span></span>
<span data-ttu-id="36318-124">integración de hello tooconfigure de IdeaScale en Azure AD, deberá tooadd IdeaScale de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="36318-124">tooconfigure hello integration of IdeaScale into Azure AD, you need tooadd IdeaScale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="36318-125">**tooadd IdeaScale de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="36318-125">**tooadd IdeaScale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="36318-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="36318-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36318-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="36318-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="36318-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="36318-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="36318-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36318-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="36318-133">En el cuadro de búsqueda de hello, escriba **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="36318-133">In hello search box, type **IdeaScale**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="36318-135">En el panel de resultados de hello, seleccione **IdeaScale**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="36318-135">In hello results panel, select **IdeaScale**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36318-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36318-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36318-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con IdeaScale con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="36318-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="36318-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en IdeaScale es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36318-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IdeaScale is tooa user in Azure AD.</span></span> <span data-ttu-id="36318-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en IdeaScale debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="36318-140">In other words, a link relationship between an Azure AD user and hello related user in IdeaScale needs toobe established.</span></span>

<span data-ttu-id="36318-141">En IdeaScale, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="36318-141">In IdeaScale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="36318-142">tooconfigure y prueba de inicio de sesión único en Azure AD con IdeaScale, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="36318-142">tooconfigure and test Azure AD single sign-on with IdeaScale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="36318-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="36318-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="36318-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36318-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36318-145">**[Creación de un usuario de prueba de IdeaScale](#creating-an-ideascale-test-user)**  -toohave un equivalente de Britta Simon en IdeaScale que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="36318-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - toohave a counterpart of Britta Simon in IdeaScale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="36318-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="36318-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36318-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="36318-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36318-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36318-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36318-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="36318-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="36318-150">**inicio de sesión único en Azure AD tooconfigure con IdeaScale, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="36318-150">**tooconfigure Azure AD single sign-on with IdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="36318-151">En el portal de Azure, en Hola Hola **IdeaScale** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="36318-151">In hello Azure portal, on hello **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="36318-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="36318-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="36318-155">En hello **IdeaScale dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="36318-155">On hello **IdeaScale Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="36318-157">a.</span><span class="sxs-lookup"><span data-stu-id="36318-157">a.</span></span> <span data-ttu-id="36318-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="36318-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="36318-159">b.</span><span class="sxs-lookup"><span data-stu-id="36318-159">b.</span></span> <span data-ttu-id="36318-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="36318-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="36318-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="36318-161">These values are not real.</span></span> <span data-ttu-id="36318-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="36318-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="36318-163">Póngase en contacto con [equipo de soporte técnico de cliente de IdeaScale](http://support.ideascale.com/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="36318-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="36318-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="36318-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="36318-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="36318-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="36318-168">En hello **configuración de IdeaScale** sección, haga clic en **configurar IdeaScale** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="36318-168">On hello **IdeaScale Configuration** section, click **Configure IdeaScale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="36318-169">Hola copia **dirección URL de cierre de sesión y el Id. de entidad SAML** de hello **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="36318-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="36318-171">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía IdeaScale tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="36318-171">In a different web browser window, log in tooyour IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="36318-172">Vaya demasiado**configuración de la Comunidad**.</span><span class="sxs-lookup"><span data-stu-id="36318-172">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="36318-173">![Configuración de la Comunidad](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Configuración de la Comunidad")</span><span class="sxs-lookup"><span data-stu-id="36318-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="36318-174">Vaya demasiado**seguridad \> configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="36318-174">Go too**Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="36318-175">![Configuración de inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="36318-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="36318-176">En **Single-Signon Type** (Tipo de inicio de sesión único), seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="36318-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="36318-177">![Tipo de inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Tipo de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="36318-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="36318-178">En hello **configuración de inicio de sesión único** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="36318-178">On hello **Single Signon Settings** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="36318-179">![Configuración de inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="36318-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="36318-180">a.</span><span class="sxs-lookup"><span data-stu-id="36318-180">a.</span></span> <span data-ttu-id="36318-181">En **Id. de entidad de SAML IdP** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="36318-181">In **SAML IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="36318-182">b.</span><span class="sxs-lookup"><span data-stu-id="36318-182">b.</span></span> <span data-ttu-id="36318-183">Copie el contenido de hello del archivo de metadatos descargado desde el portal de Azure y péguelo en hello **metadatos SAML IdP** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="36318-183">Copy hello content of your downloaded metadata file from Azure portal, and paste it into hello **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="36318-184">c.</span><span class="sxs-lookup"><span data-stu-id="36318-184">c.</span></span> <span data-ttu-id="36318-185">En **URL de cierre de sesión** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="36318-185">In **Logout Success URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="36318-186">d.</span><span class="sxs-lookup"><span data-stu-id="36318-186">d.</span></span> <span data-ttu-id="36318-187">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="36318-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="36318-188">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="36318-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="36318-189">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="36318-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="36318-190">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36318-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36318-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36318-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="36318-192">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="36318-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="36318-194">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="36318-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="36318-195">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="36318-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36318-197">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="36318-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36318-199">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="36318-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36318-201">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="36318-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36318-203">a.</span><span class="sxs-lookup"><span data-stu-id="36318-203">a.</span></span> <span data-ttu-id="36318-204">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36318-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36318-205">b.</span><span class="sxs-lookup"><span data-stu-id="36318-205">b.</span></span> <span data-ttu-id="36318-206">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="36318-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36318-207">c.</span><span class="sxs-lookup"><span data-stu-id="36318-207">c.</span></span> <span data-ttu-id="36318-208">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="36318-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="36318-209">d.</span><span class="sxs-lookup"><span data-stu-id="36318-209">d.</span></span> <span data-ttu-id="36318-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="36318-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="36318-211">Creación de un usuario de prueba de IdeaScale</span><span class="sxs-lookup"><span data-stu-id="36318-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="36318-212">toolog de los usuarios de Azure AD tooenable en IdeaScale, se les deben aprovisionar en tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="36318-212">tooenable Azure AD users toolog into IdeaScale, they must be provisioned in tooIdeaScale.</span></span> <span data-ttu-id="36318-213">En caso de hello de IdeaScale, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="36318-213">In hello case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="36318-214">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="36318-214">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="36318-215">Inicie sesión en tooyour **IdeaScale** como administrador.</span><span class="sxs-lookup"><span data-stu-id="36318-215">Log in tooyour **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="36318-216">Vaya demasiado**configuración de la Comunidad**.</span><span class="sxs-lookup"><span data-stu-id="36318-216">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="36318-217">![Configuración de la Comunidad](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Configuración de la Comunidad")</span><span class="sxs-lookup"><span data-stu-id="36318-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="36318-218">Vaya demasiado**configuración básica \> miembro administración**.</span><span class="sxs-lookup"><span data-stu-id="36318-218">Go too**Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="36318-219">Haga clic en **Agregar miembro**.</span><span class="sxs-lookup"><span data-stu-id="36318-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="36318-220">![Administración de miembros](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Administración de miembros")</span><span class="sxs-lookup"><span data-stu-id="36318-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="36318-221">En la sección Agregar nuevo miembro hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="36318-221">In hello Add New Member section, perform hello following steps:</span></span>
   
    <span data-ttu-id="36318-222">![Agregar nuevo miembro](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Agregar nuevo miembro")</span><span class="sxs-lookup"><span data-stu-id="36318-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="36318-223">a.</span><span class="sxs-lookup"><span data-stu-id="36318-223">a.</span></span> <span data-ttu-id="36318-224">Hola **direcciones de correo electrónico** cuadro de texto, dirección de correo electrónico de tipo hello de una cuenta válida de AAD que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="36318-224">In hello **Email Addresses** textbox, type hello email address of a valid AAD account you want tooprovision.</span></span>
   
    <span data-ttu-id="36318-225">b.</span><span class="sxs-lookup"><span data-stu-id="36318-225">b.</span></span> <span data-ttu-id="36318-226">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="36318-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="36318-227">titular de la cuenta de Hello Azure Active Directory Obtiene un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="36318-227">hello Azure Active Directory account holder gets an email with a link tooconfirm hello account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="36318-228">Puede usar cualquier otra IdeaScale usuario cuenta herramienta de creación o las API proporcionadas por IdeaScale tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="36318-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="36318-229">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="36318-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="36318-230">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="36318-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIdeaScale.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="36318-232">**tooassign Britta Simon tooIdeaScale, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="36318-232">**tooassign Britta Simon tooIdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="36318-233">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="36318-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="36318-235">En la lista de aplicaciones de hello, seleccione **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="36318-235">In hello applications list, select **IdeaScale**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="36318-237">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="36318-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="36318-239">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="36318-239">Click **Add** button.</span></span> <span data-ttu-id="36318-240">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="36318-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="36318-242">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="36318-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="36318-243">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="36318-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36318-244">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="36318-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="36318-245">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="36318-245">Testing single sign-on</span></span>


<span data-ttu-id="36318-246">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="36318-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="36318-247">Al hacer clic en icono de IdeaScale Hola Hola Panel de acceso, deberá obtener la aplicación de IdeaScale tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="36318-247">When you click hello IdeaScale tile in hello Access Panel, you should get automatically signed-on tooyour IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="36318-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="36318-248">Additional resources</span></span>

* [<span data-ttu-id="36318-249">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36318-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36318-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="36318-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

