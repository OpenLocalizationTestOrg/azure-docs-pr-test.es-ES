---
title: "Tutorial: Integración de Azure Active Directory con el Portal de administración en la nube de Microsoft Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el Portal de administración de la nube de Microsoft Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9596826e3dc1289b95009bf01ec8b86f823ef345
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="0e082-103">Tutorial: Integración de Azure Active Directory con el Portal de administración en la nube de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0e082-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="0e082-104">En este tutorial, aprenderá cómo toointegrate Portal de administración de la nube de Microsoft Azure con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e082-104">In this tutorial, you learn how toointegrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e082-105">Integración de Portal de administración de la nube de Microsoft Azure con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0e082-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e082-106">Puede controlar en Azure AD que tenga acceso tooCloud Portal de administración de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0e082-106">You can control in Azure AD who has access tooCloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="0e082-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCloud Portal de administración de Microsoft Azure (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e082-107">You can enable your users tooautomatically get signed-on tooCloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e082-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0e082-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0e082-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e082-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e082-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0e082-110">Prerequisites</span></span>

<span data-ttu-id="0e082-111">tooconfigure integración de Azure AD con el Portal de administración de la nube de Microsoft Azure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0e082-111">tooconfigure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need hello following items:</span></span>

- <span data-ttu-id="0e082-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e082-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e082-113">Un Portal de administración en la nube para suscripciones con inicio de sesión único habilitado de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0e082-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e082-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0e082-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e082-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0e082-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e082-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0e082-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e082-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e082-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e082-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0e082-118">Scenario description</span></span>
<span data-ttu-id="0e082-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0e082-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e082-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0e082-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e082-121">Agregar Portal de administración de la nube de Microsoft Azure desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0e082-121">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
2. <span data-ttu-id="0e082-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e082-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-hello-gallery"></a><span data-ttu-id="0e082-123">Agregar Portal de administración de la nube de Microsoft Azure desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0e082-123">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
<span data-ttu-id="0e082-124">integración de hello tooconfigure del Portal de administración de la nube de Microsoft Azure en Azure AD, necesita tooadd Portal de administración en la nube de Microsoft Azure de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0e082-124">tooconfigure hello integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need tooadd Cloud Management Portal for Microsoft Azure from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e082-125">**tooadd Portal de administración de nube de Microsoft Azure desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e082-125">**tooadd Cloud Management Portal for Microsoft Azure from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e082-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0e082-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e082-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0e082-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e082-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0e082-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0e082-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0e082-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0e082-133">En el cuadro de búsqueda de hello, escriba **Portal de administración de la nube de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="0e082-133">In hello search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="0e082-135">En el panel de resultados de hello, seleccione **Portal de administración de la nube de Microsoft Azure**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0e082-135">In hello results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e082-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e082-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e082-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Cloud Management Portal for Microsoft Azure con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0e082-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e082-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el Portal de administración de la nube de Microsoft Azure es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e082-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cloud Management Portal for Microsoft Azure is tooa user in Azure AD.</span></span> <span data-ttu-id="0e082-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el Portal de administración de la nube de Microsoft Azure debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0e082-140">In other words, a link relationship between an Azure AD user and hello related user in Cloud Management Portal for Microsoft Azure needs toobe established.</span></span>

<span data-ttu-id="0e082-141">En el Portal de administración de nube de Microsoft Azure, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e082-141">In Cloud Management Portal for Microsoft Azure, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e082-142">tooconfigure y prueba de inicio de sesión único en Azure AD con el Portal de administración en la nube de Microsoft Azure, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0e082-142">tooconfigure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e082-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0e082-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e082-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e082-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e082-145">**[Creación de un Portal de administración en la nube para el usuario de prueba de Microsoft Azure](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)**  -toohave un equivalente de Britta Simon en el Portal de administración de la nube de Microsoft Azure que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="0e082-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - toohave a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e082-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0e082-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e082-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0e082-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e082-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e082-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e082-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el Portal de administración de nube para aplicaciones de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0e082-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="0e082-150">**tooconfigure inicio de sesión único en Azure AD con el Portal de administración de la nube de Microsoft Azure, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e082-150">**tooconfigure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e082-151">En el portal de Azure, en Hola Hola **Portal de administración de la nube de Microsoft Azure** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0e082-151">In hello Azure portal, on hello **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0e082-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0e082-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="0e082-155">En hello **Portal de administración de nube de Microsoft Azure dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0e082-155">On hello **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="0e082-157">a.</span><span class="sxs-lookup"><span data-stu-id="0e082-157">a.</span></span> <span data-ttu-id="0e082-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="0e082-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="0e082-159">b.</span><span class="sxs-lookup"><span data-stu-id="0e082-159">b.</span></span> <span data-ttu-id="0e082-160">Hola **identificador** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="0e082-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="0e082-161">c.</span><span class="sxs-lookup"><span data-stu-id="0e082-161">c.</span></span> <span data-ttu-id="0e082-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="0e082-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="0e082-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0e082-163">These values are not real.</span></span> <span data-ttu-id="0e082-164">Actualizar estos valores con dirección URL de inicio de sesión en la dirección URL, el identificador y la respuesta del real Hola.</span><span class="sxs-lookup"><span data-stu-id="0e082-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="0e082-165">Póngase en contacto con [Portal de administración en la nube para el equipo de soporte técnico de Microsoft Azure Client](mailto:jczernuszka@newsignature.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="0e082-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="0e082-166">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0e082-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="0e082-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0e082-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e082-170">En hello **Portal de administración de nube de Microsoft Azure configuración** sección, haga clic en **configurar Portal de administración de nube de Microsoft Azure** tooopen **configurar inicio de sesión en**ventana.</span><span class="sxs-lookup"><span data-stu-id="0e082-170">On hello **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0e082-171">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="0e082-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="0e082-173">tooconfigure inicio de sesión único en **Portal de administración de la nube de Microsoft Azure** lado, necesita hello toosend descargado **certificado**, **dirección URL de cierre de sesión**, **SAML Single Sign-On dirección URL del servicio** y **Id. de entidad SAML** demasiado[Portal de administración en la nube para el equipo de soporte técnico de Microsoft Azure](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="0e082-173">tooconfigure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="0e082-174">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="0e082-174">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0e082-175">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0e082-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e082-176">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0e082-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e082-177">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e082-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e082-178">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e082-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e082-179">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0e082-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0e082-181">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e082-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e082-182">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0e082-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e082-184">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0e082-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e082-186">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e082-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e082-188">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0e082-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e082-190">a.</span><span class="sxs-lookup"><span data-stu-id="0e082-190">a.</span></span> <span data-ttu-id="0e082-191">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e082-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e082-192">b.</span><span class="sxs-lookup"><span data-stu-id="0e082-192">b.</span></span> <span data-ttu-id="0e082-193">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0e082-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e082-194">c.</span><span class="sxs-lookup"><span data-stu-id="0e082-194">c.</span></span> <span data-ttu-id="0e082-195">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0e082-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0e082-196">d.</span><span class="sxs-lookup"><span data-stu-id="0e082-196">d.</span></span> <span data-ttu-id="0e082-197">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0e082-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="0e082-198">Creación de un usuario de prueba para el Portal de administración en la nube de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0e082-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="0e082-199">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en Portal de administración en la nube de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0e082-199">hello objective of this section is toocreate a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="0e082-200">Trabaje con [Portal de administración en la nube para el equipo de soporte técnico de Microsoft Azure](mailto:jczernuszka@newsignature.com) a los usuarios de tooadd Hola Hola Portal de administración en la nube para la cuenta de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0e082-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) tooadd hello users in hello Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0e082-201">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e082-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0e082-202">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCloud Portal de administración de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0e082-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloud Management Portal for Microsoft Azure.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0e082-204">**tooassign Britta Simon tooCloud Portal de administración de Microsoft Azure, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e082-204">**tooassign Britta Simon tooCloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e082-205">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0e082-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0e082-207">En la lista de aplicaciones de hello, seleccione **Portal de administración de la nube de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="0e082-207">In hello applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="0e082-209">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e082-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0e082-211">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0e082-211">Click **Add** button.</span></span> <span data-ttu-id="0e082-212">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0e082-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0e082-214">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e082-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e082-215">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e082-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e082-216">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0e082-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e082-217">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0e082-217">Testing single sign-on</span></span>

<span data-ttu-id="0e082-218">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0e082-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="0e082-219">Al hacer clic en hello Portal de administración en la nube de icono de Microsoft Azure en el Panel de acceso de hello, obtendrá automáticamente ha iniciado sesión tooyour Portal de administración en la nube para aplicaciones de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0e082-219">When you click hello Cloud Management Portal for Microsoft Azure tile in hello Access Panel, you should get automatically signed-on tooyour Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="0e082-220">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0e082-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e082-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0e082-221">Additional resources</span></span>

* [<span data-ttu-id="0e082-222">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e082-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e082-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e082-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

