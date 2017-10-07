---
title: "Tutorial: integración de Azure Active Directory con Collaborative Innovation | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la innovación de colaboración."
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
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="063c4-103">Tutorial: integración de Azure Active Directory con Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="063c4-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="063c4-104">En este tutorial, aprenderá cómo toointegrate innovación en colaboración con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="063c4-104">In this tutorial, you learn how toointegrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="063c4-105">Integración de innovación de colaboración con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="063c4-105">Integrating Collaborative Innovation with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="063c4-106">Puede controlar en Azure AD que tenga acceso tooCollaborative innovación</span><span class="sxs-lookup"><span data-stu-id="063c4-106">You can control in Azure AD who has access tooCollaborative Innovation</span></span>
- <span data-ttu-id="063c4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCollaborative innovación (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="063c4-107">You can enable your users tooautomatically get signed-on tooCollaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="063c4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="063c4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="063c4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="063c4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="063c4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="063c4-110">Prerequisites</span></span>

<span data-ttu-id="063c4-111">integración de Azure AD con innovación colaboración tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="063c4-111">tooconfigure Azure AD integration with Collaborative Innovation, you need hello following items:</span></span>

- <span data-ttu-id="063c4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="063c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="063c4-113">Una suscripción habilitada para el inicio de sesión único de Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="063c4-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="063c4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="063c4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="063c4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="063c4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="063c4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="063c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="063c4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="063c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="063c4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="063c4-118">Scenario description</span></span>
<span data-ttu-id="063c4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="063c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="063c4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="063c4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="063c4-121">Adición de innovación de colaboración de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="063c4-121">Adding Collaborative Innovation from hello gallery</span></span>
2. <span data-ttu-id="063c4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="063c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-hello-gallery"></a><span data-ttu-id="063c4-123">Adición de innovación de colaboración de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="063c4-123">Adding Collaborative Innovation from hello gallery</span></span>
<span data-ttu-id="063c4-124">integración de hello tooconfigure de innovación de colaboración en Azure AD, deberá tooadd innovación colaboración de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="063c4-124">tooconfigure hello integration of Collaborative Innovation into Azure AD, you need tooadd Collaborative Innovation from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="063c4-125">**tooadd colaboración innovación de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="063c4-125">**tooadd Collaborative Innovation from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="063c4-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="063c4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="063c4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="063c4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="063c4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="063c4-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="063c4-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="063c4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="063c4-133">En el cuadro de búsqueda de hello, escriba **innovación colaboración**.</span><span class="sxs-lookup"><span data-stu-id="063c4-133">In hello search box, type **Collaborative Innovation**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="063c4-135">En el panel de resultados de hello, seleccione **innovación colaboración**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="063c4-135">In hello results panel, select **Collaborative Innovation**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="063c4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="063c4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="063c4-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Collaborative Innovation con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="063c4-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="063c4-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en colaboración innovación es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="063c4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Collaborative Innovation is tooa user in Azure AD.</span></span> <span data-ttu-id="063c4-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en colaboración innovación debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="063c4-140">In other words, a link relationship between an Azure AD user and hello related user in Collaborative Innovation needs toobe established.</span></span>

<span data-ttu-id="063c4-141">En colaboración innovación, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="063c4-141">In Collaborative Innovation, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="063c4-142">tooconfigure y prueba de inicio de sesión único en Azure AD con colaboración innovación, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="063c4-142">tooconfigure and test Azure AD single sign-on with Collaborative Innovation, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="063c4-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="063c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="063c4-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="063c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="063c4-145">**[Crear un usuario de prueba de innovación colaboración](#creating-a-collaborative-innovation-test-user) ** -toohave un equivalente de Britta Simon en colaboración innovación que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="063c4-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - toohave a counterpart of Britta Simon in Collaborative Innovation that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="063c4-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="063c4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="063c4-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="063c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="063c4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="063c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="063c4-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de innovación de colaboración.</span><span class="sxs-lookup"><span data-stu-id="063c4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="063c4-150">**inicio de sesión único en tooconfigure Azure AD con colaboración innovación, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="063c4-150">**tooconfigure Azure AD single sign-on with Collaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="063c4-151">En el portal de Azure, en Hola Hola **innovación colaboración** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="063c4-151">In hello Azure portal, on hello **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="063c4-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="063c4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="063c4-155">En hello **colaboración de innovación de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="063c4-155">On hello **Collaborative Innovation Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="063c4-157">a.</span><span class="sxs-lookup"><span data-stu-id="063c4-157">a.</span></span> <span data-ttu-id="063c4-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="063c4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="063c4-159">b.</span><span class="sxs-lookup"><span data-stu-id="063c4-159">b.</span></span> <span data-ttu-id="063c4-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="063c4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="063c4-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="063c4-161">These values are not real.</span></span> <span data-ttu-id="063c4-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="063c4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="063c4-163">Póngase en contacto con [equipo de soporte técnico de cliente de colaboración innovación](https://www.unilever.com/contact/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="063c4-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) tooget these values.</span></span>  

4. <span data-ttu-id="063c4-164">Aplicación de colaboración innovación espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="063c4-164">Collaborative Innovation application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="063c4-165">Configure Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="063c4-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="063c4-166">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="063c4-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="063c4-167">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="063c4-167">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="063c4-169">Haga clic en **ver y editar todos los demás atributos de usuario** checkbox en hello **atributos de usuario** sección atributos de hello tooexpand.</span><span class="sxs-lookup"><span data-stu-id="063c4-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="063c4-170">Realizar Hola siguiendo los pasos en cada uno de los atributos de muestra de Hola-</span><span class="sxs-lookup"><span data-stu-id="063c4-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="063c4-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="063c4-171">Attribute Name</span></span> | <span data-ttu-id="063c4-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="063c4-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="063c4-173">givenname</span><span class="sxs-lookup"><span data-stu-id="063c4-173">givenname</span></span> | <span data-ttu-id="063c4-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="063c4-174">user.givenname</span></span> |
    | <span data-ttu-id="063c4-175">surname</span><span class="sxs-lookup"><span data-stu-id="063c4-175">surname</span></span> | <span data-ttu-id="063c4-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="063c4-176">user.surname</span></span> |
    | <span data-ttu-id="063c4-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="063c4-177">emailaddress</span></span> | <span data-ttu-id="063c4-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="063c4-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="063c4-179">name</span><span class="sxs-lookup"><span data-stu-id="063c4-179">name</span></span> | <span data-ttu-id="063c4-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="063c4-180">user.userprincipalname</span></span> |

    <span data-ttu-id="063c4-181">a.</span><span class="sxs-lookup"><span data-stu-id="063c4-181">a.</span></span> <span data-ttu-id="063c4-182">Haga clic en Hola de hello atributo tooopen **Editar atributo** ventana.</span><span class="sxs-lookup"><span data-stu-id="063c4-182">Click hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="063c4-184">b.</span><span class="sxs-lookup"><span data-stu-id="063c4-184">b.</span></span> <span data-ttu-id="063c4-185">Eliminar el valor de dirección URL de Hola de hello **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="063c4-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="063c4-186">c.</span><span class="sxs-lookup"><span data-stu-id="063c4-186">c.</span></span> <span data-ttu-id="063c4-187">Haga clic en **Aceptar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="063c4-187">Click **Ok** toosave hello setting.</span></span>

6. <span data-ttu-id="063c4-188">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="063c4-188">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="063c4-190">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="063c4-190">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="063c4-192">tooconfigure inicio de sesión único en **innovación colaboración** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de colaboración innovación](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="063c4-192">tooconfigure single sign-on on **Collaborative Innovation** side, you need toosend hello downloaded **Metadata XML** too[Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="063c4-193">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="063c4-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="063c4-194">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="063c4-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="063c4-195">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="063c4-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="063c4-196">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="063c4-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="063c4-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="063c4-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="063c4-198">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="063c4-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="063c4-200">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="063c4-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="063c4-201">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="063c4-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="063c4-203">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="063c4-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="063c4-205">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="063c4-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="063c4-207">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="063c4-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="063c4-209">a.</span><span class="sxs-lookup"><span data-stu-id="063c4-209">a.</span></span> <span data-ttu-id="063c4-210">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="063c4-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="063c4-211">b.</span><span class="sxs-lookup"><span data-stu-id="063c4-211">b.</span></span> <span data-ttu-id="063c4-212">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="063c4-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="063c4-213">c.</span><span class="sxs-lookup"><span data-stu-id="063c4-213">c.</span></span> <span data-ttu-id="063c4-214">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="063c4-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="063c4-215">d.</span><span class="sxs-lookup"><span data-stu-id="063c4-215">d.</span></span> <span data-ttu-id="063c4-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="063c4-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="063c4-217">Creación de un usuario de prueba de Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="063c4-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="063c4-218">toolog de los usuarios de Azure AD tooenable en tooCollaborative innovación, se les deben aprovisionar en innovación de colaboración.</span><span class="sxs-lookup"><span data-stu-id="063c4-218">tooenable Azure AD users toolog in tooCollaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="063c4-219">En el caso de esta aplicación el aprovisionamiento es automática como aplicación hello admite justo a tiempo el aprovisionamiento de usuarios.</span><span class="sxs-lookup"><span data-stu-id="063c4-219">In case of this application provisioning is automatic as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="063c4-220">Modo que no hay ninguna necesidad de tooperform todos los pasos aquí.</span><span class="sxs-lookup"><span data-stu-id="063c4-220">So there is no need tooperform any steps here.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="063c4-221">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="063c4-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="063c4-222">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCollaborative innovación.</span><span class="sxs-lookup"><span data-stu-id="063c4-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCollaborative Innovation.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="063c4-224">**tooassign Britta Simon tooCollaborative innovación, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="063c4-224">**tooassign Britta Simon tooCollaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="063c4-225">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="063c4-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="063c4-227">En la lista de aplicaciones de hello, seleccione **innovación colaboración**.</span><span class="sxs-lookup"><span data-stu-id="063c4-227">In hello applications list, select **Collaborative Innovation**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="063c4-229">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="063c4-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="063c4-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="063c4-231">Click **Add** button.</span></span> <span data-ttu-id="063c4-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="063c4-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="063c4-234">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="063c4-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="063c4-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="063c4-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="063c4-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="063c4-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="063c4-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="063c4-237">Testing single sign-on</span></span>

<span data-ttu-id="063c4-238">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="063c4-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="063c4-239">Al hacer clic en icono de innovación de colaboración de Hola Hola Panel de acceso, deberá obtener la página de inicio de sesión de aplicación de innovación de colaboración.</span><span class="sxs-lookup"><span data-stu-id="063c4-239">When you click hello Collaborative Innovation tile in hello Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="063c4-240">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="063c4-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="063c4-241">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="063c4-241">Additional resources</span></span>

* [<span data-ttu-id="063c4-242">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="063c4-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="063c4-243">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="063c4-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

