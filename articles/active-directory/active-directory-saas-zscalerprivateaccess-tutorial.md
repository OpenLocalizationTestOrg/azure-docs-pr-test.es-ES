---
title: "Tutorial: Integración de Azure Active Directory con Zscaler Private Access (ZPA) | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y acceso privado de Zscaler (ZPA)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="82a9c-103">Tutorial: Integración de Azure Active Directory con Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="82a9c-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="82a9c-104">En este tutorial, aprenderá cómo toointegrate acceso privado de Zscaler (ZPA) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="82a9c-104">In this tutorial, you learn how toointegrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82a9c-105">Integración de acceso privada de Zscaler (ZPA) con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="82a9c-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="82a9c-106">Puede controlar en Azure AD que tenga acceso tooZscaler acceso privado (ZPA)</span><span class="sxs-lookup"><span data-stu-id="82a9c-106">You can control in Azure AD who has access tooZscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="82a9c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZscaler acceso privado (ZPA) (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a9c-107">You can enable your users tooautomatically get signed-on tooZscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="82a9c-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="82a9c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="82a9c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="82a9c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82a9c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="82a9c-110">Prerequisites</span></span>

<span data-ttu-id="82a9c-111">tooconfigure integración de Azure AD con Zscaler privada acceso (ZPA), necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="82a9c-111">tooconfigure Azure AD integration with Zscaler Private Access (ZPA), you need hello following items:</span></span>

- <span data-ttu-id="82a9c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a9c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82a9c-113">Una suscripción habilitada para el inicio de sesión único de Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="82a9c-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="82a9c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="82a9c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="82a9c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="82a9c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82a9c-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="82a9c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="82a9c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82a9c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="82a9c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="82a9c-118">Scenario description</span></span>
<span data-ttu-id="82a9c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="82a9c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82a9c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="82a9c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82a9c-121">Agregar acceso privado de Zscaler (ZPA) desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="82a9c-121">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
2. <span data-ttu-id="82a9c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a9c-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a><span data-ttu-id="82a9c-123">Agregar acceso privado de Zscaler (ZPA) desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="82a9c-123">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
<span data-ttu-id="82a9c-124">integración de hello tooconfigure de acceso privada de Zscaler (ZPA) en Azure AD, deberá tooadd acceso privado de Zscaler (ZPA) de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="82a9c-124">tooconfigure hello integration of Zscaler Private Access (ZPA) into Azure AD, you need tooadd Zscaler Private Access (ZPA) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="82a9c-125">**tooadd acceso privado de Zscaler (ZPA) desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="82a9c-125">**tooadd Zscaler Private Access (ZPA) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a9c-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="82a9c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="82a9c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="82a9c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="82a9c-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="82a9c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="82a9c-133">En el cuadro de búsqueda de hello, escriba **acceso privado de Zscaler (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-133">In hello search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="82a9c-135">En el panel de resultados de hello, seleccione **acceso privado de Zscaler (ZPA)**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="82a9c-135">In hello results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="82a9c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a9c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="82a9c-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zscaler Private Access (ZPA) con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="82a9c-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="82a9c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el acceso privado de Zscaler (ZPA) es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82a9c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Private Access (ZPA) is tooa user in Azure AD.</span></span> <span data-ttu-id="82a9c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el acceso privado de Zscaler (ZPA) debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="82a9c-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Private Access (ZPA) needs toobe established.</span></span>

<span data-ttu-id="82a9c-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** de acceso privada de Zscaler (ZPA).</span><span class="sxs-lookup"><span data-stu-id="82a9c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="82a9c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Zscaler privada acceso (ZPA), deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="82a9c-142">tooconfigure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="82a9c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="82a9c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="82a9c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82a9c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82a9c-145">**[Crear un usuario de prueba de Zscaler privada acceso (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave un equivalente de Britta Simon en Zscaler privada acceso (ZPA) que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="82a9c-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - toohave a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="82a9c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="82a9c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="82a9c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="82a9c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="82a9c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a9c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="82a9c-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación de Zscaler privada acceso (ZPA).</span><span class="sxs-lookup"><span data-stu-id="82a9c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="82a9c-150">**tooconfigure inicio de sesión único en Azure AD con acceso privado de Zscaler (ZPA), lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="82a9c-150">**tooconfigure Azure AD single sign-on with Zscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="82a9c-151">En el portal de administración de Azure de hello, en hello **acceso privado de Zscaler (ZPA)** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-151">In hello Azure Management portal, on hello **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="82a9c-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="82a9c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="82a9c-155">En hello **dominio Zscaler privada acceso (ZPA) y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="82a9c-155">On hello **Zscaler Private Access (ZPA) Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="82a9c-157">a.</span><span class="sxs-lookup"><span data-stu-id="82a9c-157">a.</span></span> <span data-ttu-id="82a9c-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="82a9c-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="82a9c-159">b.</span><span class="sxs-lookup"><span data-stu-id="82a9c-159">b.</span></span> <span data-ttu-id="82a9c-160">Hola **identificador** cuadro de texto, tipo:`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="82a9c-160">In hello **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="82a9c-161">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="82a9c-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="82a9c-162">Tendrá que tooupdate estos valores con hello real iniciar sesión en la dirección URL y el identificador.</span><span class="sxs-lookup"><span data-stu-id="82a9c-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="82a9c-163">Aquí le sugerimos toouse Hola valor único de dirección URL en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="82a9c-163">Here we suggest you toouse hello unique value of URL in hello Identifier.</span></span> <span data-ttu-id="82a9c-164">Póngase en contacto con [equipo de soporte técnico de Zscaler privada acceso (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="82a9c-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooget these values.</span></span>

4. <span data-ttu-id="82a9c-165">En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-165">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="82a9c-167">En hello **crear nuevo certificado** cuadro de diálogo, haga clic en el icono del calendario de Hola y seleccione un **fecha de expiración**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-167">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="82a9c-168">Luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-168">Then click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="82a9c-170">En hello **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado** y haga clic en **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="82a9c-170">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="82a9c-172">En la ventana emergente de hello **el certificado de sustitución** ventana, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-172">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="82a9c-174">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="82a9c-174">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="82a9c-176">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Zscaler Private Access (ZPA) como administrador.</span><span class="sxs-lookup"><span data-stu-id="82a9c-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="82a9c-177">Navegue demasiado**administrador** y, a continuación, haga clic en **configuración de Idp**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-177">Navigate too**Administrator** and then click **Idp Configuration**.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="82a9c-179">Hola **configuración de Idp** sección, haga clic en **agregar nueva configuración de IDP**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-179">In hello **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="82a9c-181">Hola **nueva configuración de IDP** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="82a9c-181">In hello **New IDP Configuration** section, perform hello following steps:</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="82a9c-183">a.</span><span class="sxs-lookup"><span data-stu-id="82a9c-183">a.</span></span> <span data-ttu-id="82a9c-184">Haga clic en **Select File** (Seleccionar archivo) y cargue su archivo de metadatos descargado.</span><span class="sxs-lookup"><span data-stu-id="82a9c-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="82a9c-185">b.</span><span class="sxs-lookup"><span data-stu-id="82a9c-185">b.</span></span> <span data-ttu-id="82a9c-186">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="82a9c-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="82a9c-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a9c-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="82a9c-188">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="82a9c-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="82a9c-190">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="82a9c-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="82a9c-191">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="82a9c-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="82a9c-193">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="82a9c-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="82a9c-195">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82a9c-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="82a9c-197">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="82a9c-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="82a9c-199">a.</span><span class="sxs-lookup"><span data-stu-id="82a9c-199">a.</span></span> <span data-ttu-id="82a9c-200">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82a9c-201">b.</span><span class="sxs-lookup"><span data-stu-id="82a9c-201">b.</span></span> <span data-ttu-id="82a9c-202">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="82a9c-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="82a9c-203">c.</span><span class="sxs-lookup"><span data-stu-id="82a9c-203">c.</span></span> <span data-ttu-id="82a9c-204">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="82a9c-205">d.</span><span class="sxs-lookup"><span data-stu-id="82a9c-205">d.</span></span> <span data-ttu-id="82a9c-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="82a9c-207">Creación de un usuario de prueba de Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="82a9c-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="82a9c-208">En esta sección, creará un usuario llamado Britta Simon en Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="82a9c-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="82a9c-209">Trabaje con [equipo de soporte técnico de Zscaler privada acceso (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooadd los usuarios de hello en la plataforma de hello Zscaler privada acceso (ZPA).</span><span class="sxs-lookup"><span data-stu-id="82a9c-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooadd hello users in hello Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="82a9c-210">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="82a9c-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="82a9c-211">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooZscaler acceso acceso privado (ZPA).</span><span class="sxs-lookup"><span data-stu-id="82a9c-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooZscaler Private Access (ZPA).</span></span>

![Asignar usuario][200] 

<span data-ttu-id="82a9c-213">**tooassign Britta Simon tooZscaler acceso privado (ZPA), lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="82a9c-213">**tooassign Britta Simon tooZscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="82a9c-214">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-214">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="82a9c-216">En la lista de aplicaciones de hello, seleccione **acceso privado de Zscaler (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-216">In hello applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="82a9c-218">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="82a9c-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-220">Click **Add** button.</span></span> <span data-ttu-id="82a9c-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="82a9c-223">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="82a9c-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="82a9c-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82a9c-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="82a9c-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="82a9c-226">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="82a9c-226">Testing single sign-on</span></span>

<span data-ttu-id="82a9c-227">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="82a9c-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="82a9c-228">Al hacer clic en icono de Zscaler privada acceso (ZPA) Hola Hola Panel de acceso, deberá obtener la aplicación de Zscaler privada acceso (ZPA) tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="82a9c-228">When you click hello Zscaler Private Access (ZPA) tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="82a9c-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="82a9c-229">Additional resources</span></span>

* [<span data-ttu-id="82a9c-230">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82a9c-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82a9c-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="82a9c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png