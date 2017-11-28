---
title: "Tutorial: Integración de Azure Active Directory con Datahug | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="28580-103">Tutorial: Integración de Azure Active Directory con Datahug</span><span class="sxs-lookup"><span data-stu-id="28580-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="28580-104">En este tutorial, aprenderá cómo toointegrate Datahug con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28580-104">In this tutorial, you learn how toointegrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28580-105">Integración Datahug con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="28580-105">Integrating Datahug with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="28580-106">Puede controlar en Azure AD que tenga acceso tooDatahug</span><span class="sxs-lookup"><span data-stu-id="28580-106">You can control in Azure AD who has access tooDatahug</span></span>
- <span data-ttu-id="28580-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooDatahug (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28580-107">You can enable your users tooautomatically get signed-on tooDatahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28580-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="28580-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="28580-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte.</span><span class="sxs-lookup"><span data-stu-id="28580-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="28580-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="28580-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28580-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="28580-111">Prerequisites</span></span>

<span data-ttu-id="28580-112">integración de Azure AD con Datahug tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="28580-112">tooconfigure Azure AD integration with Datahug, you need hello following items:</span></span>

- <span data-ttu-id="28580-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28580-113">An Azure AD subscription</span></span>
- <span data-ttu-id="28580-114">Una suscripción habilitada para inicio de sesión único en Datahug</span><span class="sxs-lookup"><span data-stu-id="28580-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28580-115">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="28580-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28580-116">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="28580-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28580-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="28580-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28580-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28580-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28580-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="28580-119">Scenario description</span></span>
<span data-ttu-id="28580-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="28580-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28580-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="28580-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28580-122">Agregar Datahug desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="28580-122">Adding Datahug from hello gallery</span></span>
2. <span data-ttu-id="28580-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28580-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-hello-gallery"></a><span data-ttu-id="28580-124">Agregar Datahug desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="28580-124">Adding Datahug from hello gallery</span></span>
<span data-ttu-id="28580-125">integración de hello tooconfigure de Datahug en Azure AD, deberá tooadd Datahug de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="28580-125">tooconfigure hello integration of Datahug into Azure AD, you need tooadd Datahug from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="28580-126">**tooadd Datahug de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="28580-126">**tooadd Datahug from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="28580-127">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="28580-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28580-129">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="28580-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="28580-130">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="28580-130">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="28580-132">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28580-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="28580-134">En el cuadro de búsqueda de hello, escriba **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="28580-134">In hello search box, type **Datahug**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="28580-136">En el panel de resultados de hello, seleccione **Datahug**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="28580-136">In hello results panel, select **Datahug**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28580-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28580-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28580-139">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Datahug con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="28580-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="28580-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Datahug es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28580-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Datahug is tooa user in Azure AD.</span></span> <span data-ttu-id="28580-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Datahug debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="28580-141">In other words, a link relationship between an Azure AD user and hello related user in Datahug needs toobe established.</span></span>

<span data-ttu-id="28580-142">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Datahug.</span><span class="sxs-lookup"><span data-stu-id="28580-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Datahug.</span></span>

<span data-ttu-id="28580-143">tooconfigure y prueba de inicio de sesión único en Azure AD con Datahug, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="28580-143">tooconfigure and test Azure AD single sign-on with Datahug, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="28580-144">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="28580-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="28580-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28580-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28580-146">**[Crear un usuario de prueba Datahug](#creating-a-datahug-test-user)**  -toohave un equivalente de Britta Simon en Datahug que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="28580-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - toohave a counterpart of Britta Simon in Datahug that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="28580-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="28580-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28580-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="28580-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28580-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28580-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28580-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Datahug.</span><span class="sxs-lookup"><span data-stu-id="28580-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="28580-151">**inicio de sesión único en Azure AD tooconfigure con Datahug, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="28580-151">**tooconfigure Azure AD single sign-on with Datahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="28580-152">En el portal de Azure, en Hola Hola **Datahug** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="28580-152">In hello Azure portal, on hello **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="28580-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="28580-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="28580-156">En hello **Datahug dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="28580-156">On hello **Datahug Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="28580-158">a.</span><span class="sxs-lookup"><span data-stu-id="28580-158">a.</span></span> <span data-ttu-id="28580-159">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="28580-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="28580-160">b.</span><span class="sxs-lookup"><span data-stu-id="28580-160">b.</span></span> <span data-ttu-id="28580-161">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="28580-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="28580-162">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="28580-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="28580-163">Si desea que aplicación de hello tooconfigure en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="28580-163">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="28580-165">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="28580-165">In hello **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="28580-166">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="28580-166">These values are not hello real.</span></span> <span data-ttu-id="28580-167">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="28580-167">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="28580-168">A continuación, se recomienda toouse Hola único valor de cadena en hello identificador y la dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="28580-168">Here we suggest you toouse hello unique value of string in hello Identifier and Reply URL.</span></span> <span data-ttu-id="28580-169">Póngase en contacto con [equipo de soporte técnico de cliente de Datahug](http://datahug.com/about/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="28580-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) tooget these values.</span></span> 

5. <span data-ttu-id="28580-170">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="28580-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="28580-172">Comprobar **"Mostrar configuración de firma de certificado avanzada"** y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="28580-172">Check **“Show advanced certificate signing settings”** and perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="28580-174">a.</span><span class="sxs-lookup"><span data-stu-id="28580-174">a.</span></span> <span data-ttu-id="28580-175">En **Opciones de firma**, seleccione **Firmar aserción SAML**.</span><span class="sxs-lookup"><span data-stu-id="28580-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="28580-176">b.</span><span class="sxs-lookup"><span data-stu-id="28580-176">b.</span></span> <span data-ttu-id="28580-177">En **Algoritmo de firma**, seleccione **SHA-1**.</span><span class="sxs-lookup"><span data-stu-id="28580-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="28580-178">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="28580-178">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="28580-180">En hello **Datahug configuración** sección, haga clic en **configurar Datahug** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="28580-180">On hello **Datahug Configuration** section, click **Configure Datahug** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="28580-181">Hola copia **Id. de entidad SAML** y **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="28580-181">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="28580-183">tooconfigure inicio de sesión único en **Datahug** lado, necesita hello toosend descargado **Metadata XML**, **Id. de entidad SAML** y **servicio de inicio de sesión único de SAML Dirección URL** demasiado[Datahug compatibilidad](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="28580-183">tooconfigure single sign-on on **Datahug** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="28580-184">Establecen esta aplicación se pueden instalar toohave Hola configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="28580-184">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="28580-185">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="28580-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="28580-186">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="28580-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="28580-187">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28580-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28580-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="28580-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="28580-189">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="28580-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="28580-191">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="28580-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="28580-192">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="28580-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28580-194">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="28580-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28580-196">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="28580-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28580-198">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="28580-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28580-200">a.</span><span class="sxs-lookup"><span data-stu-id="28580-200">a.</span></span> <span data-ttu-id="28580-201">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28580-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28580-202">b.</span><span class="sxs-lookup"><span data-stu-id="28580-202">b.</span></span> <span data-ttu-id="28580-203">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="28580-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28580-204">c.</span><span class="sxs-lookup"><span data-stu-id="28580-204">c.</span></span> <span data-ttu-id="28580-205">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="28580-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="28580-206">d.</span><span class="sxs-lookup"><span data-stu-id="28580-206">d.</span></span> <span data-ttu-id="28580-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="28580-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="28580-208">Creación de un usuario de prueba de Datahug</span><span class="sxs-lookup"><span data-stu-id="28580-208">Creating a Datahug test user</span></span>

<span data-ttu-id="28580-209">toolog de los usuarios de Azure AD tooenable en tooDatahug, se les deben aprovisionar en Datahug.</span><span class="sxs-lookup"><span data-stu-id="28580-209">tooenable Azure AD users toolog in tooDatahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="28580-210">En Datahug, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="28580-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="28580-211">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="28580-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="28580-212">Inicie sesión en tooyour Datahug sitio de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="28580-212">Log in tooyour Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="28580-213">Mantenga el mouse sobre hello **engranaje** en la esquina superior derecha de Hola y haga clic en **configuración**</span><span class="sxs-lookup"><span data-stu-id="28580-213">Hover over hello **cog** in hello top right-hand corner and click **Settings**</span></span>
   
   ![Agregar empleado](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="28580-215">Elija **personas** y haga clic en hello **agregar usuarios** ficha</span><span class="sxs-lookup"><span data-stu-id="28580-215">Choose **People** and click hello **Add Users** tab</span></span>

    ![Agregar empleado](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="28580-217">Escriba correo electrónico Hola de persona Hola le gustaría toocreate una cuenta de y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="28580-217">Type hello email of hello person you would like toocreate an account for and click **Add**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="28580-219">Puede enviar toouser de correo electrónico de registro seleccionando **enviar correo electrónico de bienvenida** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="28580-219">You can send registration mail toouser by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="28580-220">Si va a crear una cuenta de Salesforce no enviar correo electrónico de bienvenida Hola.</span><span class="sxs-lookup"><span data-stu-id="28580-220">If you are creating an account for Salesforce do not send hello welcome email.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="28580-221">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="28580-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="28580-222">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooDatahug.</span><span class="sxs-lookup"><span data-stu-id="28580-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDatahug.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="28580-224">**tooassign Britta Simon tooDatahug, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="28580-224">**tooassign Britta Simon tooDatahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="28580-225">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="28580-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="28580-227">En la lista de aplicaciones de hello, seleccione **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="28580-227">In hello applications list, select **Datahug**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="28580-229">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="28580-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="28580-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="28580-231">Click **Add** button.</span></span> <span data-ttu-id="28580-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="28580-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="28580-234">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="28580-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="28580-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="28580-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28580-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="28580-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="28580-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="28580-237">Testing single sign-on</span></span>

<span data-ttu-id="28580-238">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="28580-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="28580-239">Al hacer clic en icono de Datahug Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Datahug aplicación.</span><span class="sxs-lookup"><span data-stu-id="28580-239">When you click hello Datahug tile in hello Access Panel, you should get automatically signed-on tooyour Datahug application.</span></span> <span data-ttu-id="28580-240">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="28580-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="28580-241">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="28580-241">Additional resources</span></span>

* [<span data-ttu-id="28580-242">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28580-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28580-243">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="28580-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

