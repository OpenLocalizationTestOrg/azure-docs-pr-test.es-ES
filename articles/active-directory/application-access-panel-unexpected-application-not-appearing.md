---
title: "Una aplicación asignada no aparece en el panel de acceso | Microsoft Docs"
description: "Solucionar por qué una aplicación no aparece en el panel de acceso"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 9ea5744d77b90929598ea5feb80c7bbdff3772fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="an-assigned-application-is-not-appearing-on-the-access-panel"></a><span data-ttu-id="4421b-103">Una aplicación asignada no aparece en el panel de acceso</span><span class="sxs-lookup"><span data-stu-id="4421b-103">An assigned application is not appearing on the access panel</span></span>

<span data-ttu-id="4421b-104">El panel de acceso es un portal basado en web que permite que un usuario con una cuenta profesional o educativa de Azure Active Directory (Azure AD) vea e inicie las aplicaciones basadas en la nube a las que el administrador de Azure AD le ha concedido acceso.</span><span class="sxs-lookup"><span data-stu-id="4421b-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="4421b-105">Estas aplicaciones se configuran en nombre del usuario en el portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4421b-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="4421b-106">La aplicación debe configurarse correctamente y asignarse al usuario o al grupo del que el usuario es miembro para poder ver la aplicación en el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4421b-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="4421b-107">El tipo de aplicaciones que un usuario puede ver se dividen en las siguientes categorías:</span><span class="sxs-lookup"><span data-stu-id="4421b-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="4421b-108">Aplicaciones de Office 365</span><span class="sxs-lookup"><span data-stu-id="4421b-108">Office 365 Applications</span></span>

-   <span data-ttu-id="4421b-109">Aplicaciones de Microsoft y de terceros configuradas con SSO basado en federación</span><span class="sxs-lookup"><span data-stu-id="4421b-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="4421b-110">Aplicaciones de SSO basado en contraseña</span><span class="sxs-lookup"><span data-stu-id="4421b-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="4421b-111">Aplicaciones con soluciones SSO existentes</span><span class="sxs-lookup"><span data-stu-id="4421b-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="4421b-112">Problemas generales para comprobar primero</span><span class="sxs-lookup"><span data-stu-id="4421b-112">General issues to check first</span></span>

-   <span data-ttu-id="4421b-113">Si se acaba de agregar una aplicación a un usuario, intente volver a iniciar sesión de entrada y salida en el panel de acceso del usuario después de unos minutos para ver si la aplicación se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="4421b-113">If an application was just added to a user, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is added.</span></span>

-   <span data-ttu-id="4421b-114">Si se acaba de quitar una licencia de un usuario o grupo del que el usuario es miembro, los cambios pueden tardar tiempo, en función del tamaño y la complejidad del grupo.</span><span class="sxs-lookup"><span data-stu-id="4421b-114">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="4421b-115">Espere un poco más de tiempo antes de iniciar sesión en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4421b-115">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-application-configuration"></a><span data-ttu-id="4421b-116">Problemas relacionados con la adición o configuración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4421b-116">Problems related to application configuration</span></span>

<span data-ttu-id="4421b-117">Puede que una aplicación no aparezca en el panel de acceso de un usuario porque no está configurada correctamente.</span><span class="sxs-lookup"><span data-stu-id="4421b-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="4421b-118">A continuación se muestran algunas maneras de solucionar problemas relacionados con la configuración de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="4421b-118">Below are some ways you can troubleshoot issues related to application configuration:</span></span>

-   [<span data-ttu-id="4421b-119">Configuración del inicio de sesión único federado para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-119">How to configure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="4421b-120">Configuración del inicio de sesión único federado para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="4421b-120">How to configure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="4421b-121">Configuración del inicio de sesión único con contraseña para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-121">How to configure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="4421b-122">Configuración del inicio de sesión único con contraseña para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="4421b-122">How to configure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="4421b-123">Configuración del inicio de sesión único federado para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-123">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="4421b-124">Todas las aplicaciones de la galería de Azure AD habilitadas con la funcionalidad de Enterprise Single Sign-On tienen un tutorial paso a paso disponible.</span><span class="sxs-lookup"><span data-stu-id="4421b-124">All applications in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="4421b-125">Para instrucciones detalladas paso a paso, acceda a la [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="4421b-125">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="4421b-126">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-126">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="4421b-127">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-127">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="4421b-128">Configuración de los valores de los metadatos de la aplicación en Azure AD (URL de inicio de sesión, identificador, URL de respuesta)</span><span class="sxs-lookup"><span data-stu-id="4421b-128">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="4421b-129">Selección del identificador de usuario e incorporación de los atributos de usuario para enviarlos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="4421b-129">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="4421b-130">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="4421b-131">Configuración de los valores de los metadatos de Azure AD en la aplicación (URL de inicio de sesión, emisor, URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="4421b-131">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="4421b-132">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-132">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="4421b-133">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-133">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-134">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **administrador global** o **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="4421b-134">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="4421b-135">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-135">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-136">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-136">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-137">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-137">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-138">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4421b-138">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="4421b-139">En el cuadro de texto **Escriba un nombre** de la sección **Agregar desde la galería**, escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-139">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="4421b-140">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4421b-140">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="4421b-141">Antes de agregar la aplicación, puede cambiar su nombre en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="4421b-141">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="4421b-142">Haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-142">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="4421b-143">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-143">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="4421b-144">Configuración del inicio de sesión único para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-144">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="4421b-145">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-145">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-146">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="4421b-146">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4421b-147">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-147">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-148">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-149">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-149">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-150">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4421b-150">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4421b-151">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="4421b-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4421b-152">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4421b-152">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4421b-153">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-153">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4421b-154">En la lista desplegable **Modo**, seleccione **Inicio de sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="4421b-154">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="4421b-155">Especifique los valores obligatorios en **Dominio y direcciones URL**.</span><span class="sxs-lookup"><span data-stu-id="4421b-155">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="4421b-156">El proveedor de la aplicación le proporcionará estos valores.</span><span class="sxs-lookup"><span data-stu-id="4421b-156">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="4421b-157">Para configurar la aplicación como SSO iniciado por el SP, la dirección URL de inicio de sesión es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="4421b-157">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="4421b-158">En algunas aplicaciones, el identificador también es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="4421b-158">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="4421b-159">Para configurar la aplicación como SSO iniciado por el IdP, la dirección URL de respuesta es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="4421b-159">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="4421b-160">En algunas aplicaciones, el identificador también es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="4421b-160">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="4421b-161">**Opcional:** haga clic en **Mostrar configuración avanzada de URL** si desea ver los valores opcionales.</span><span class="sxs-lookup"><span data-stu-id="4421b-161">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="4421b-162">En **Atributos de usuario**, seleccione el identificador único para los usuarios de la lista desplegable **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="4421b-162">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="4421b-163">**Opcional:** haga clic en **Ver y editar todos los demás atributos de usuario** para editar los atributos que se enviarán a la aplicación en el token de SAML cuando el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="4421b-163">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="4421b-164">Para agregar un atributo:</span><span class="sxs-lookup"><span data-stu-id="4421b-164">To add an attribute:</span></span>

   1. <span data-ttu-id="4421b-165">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="4421b-165">click **Add attribute**.</span></span> <span data-ttu-id="4421b-166">Escriba el **Nombre** y seleccione el **Valor** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="4421b-166">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="4421b-167">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-167">click **Save.**</span></span> <span data-ttu-id="4421b-168">En la tabla verá el nuevo atributo.</span><span class="sxs-lookup"><span data-stu-id="4421b-168">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="4421b-169">Haga clic en **Configurar &lt;nombre de la aplicación&gt;** para acceder a documentación sobre cómo configurar el inicio de sesión único en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-169">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="4421b-170">Además, tiene las direcciones URL de los metadatos y el certificado necesario para la instalación de SSO con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-170">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="4421b-171">Para guardar la configuración, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-171">click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="4421b-172">Asigne usuarios a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-172">Assign users to the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="4421b-173">Selección del identificador de usuario e incorporación de los atributos de usuario para enviarlos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="4421b-173">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="4421b-174">Para seleccionar el identificador de usuario o agregar atributos de usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-174">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-175">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="4421b-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4421b-176">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-177">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-178">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-179">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4421b-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4421b-180">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4421b-180">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4421b-181">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4421b-181">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4421b-182">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-182">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4421b-183">En la sección **Atributos de usuario**, seleccione el identificador único para los usuarios de la lista desplegable **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="4421b-183">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="4421b-184">La opción seleccionada debe coincidir con el valor esperado de la aplicación para autenticar al usuario.</span><span class="sxs-lookup"><span data-stu-id="4421b-184">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="4421b-185">AD Azure selecciona el formato del atributo NameID (Identificador de usuario) en función del valor seleccionado o del formato que solicite la aplicación en el elemento AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="4421b-185">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="4421b-186">Para más información, visite la sección NameIDPolicy del artículo [Protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="4421b-186">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="4421b-187">Para agregar atributos de usuario, haga clic en **Ver y editar todos los demás atributos de usuario** para editar los atributos que se enviarán a la aplicación en el token de SAML cuando el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="4421b-187">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="4421b-188">Para agregar un atributo:</span><span class="sxs-lookup"><span data-stu-id="4421b-188">To add an attribute:</span></span>

   1. <span data-ttu-id="4421b-189">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="4421b-189">click **Add attribute**.</span></span> <span data-ttu-id="4421b-190">Escriba el **Nombre** y seleccione el **Valor** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="4421b-190">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="4421b-191">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-191">click **Save.**</span></span> <span data-ttu-id="4421b-192">En la tabla verá el nuevo atributo.</span><span class="sxs-lookup"><span data-stu-id="4421b-192">You will see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="4421b-193">Descarga del certificado o los metadatos de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-193">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="4421b-194">Para descargar el certificado o los metadatos de la aplicación de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-194">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-195">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="4421b-195">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4421b-196">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-196">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-197">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-197">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-198">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-198">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-199">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4421b-199">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4421b-200">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="4421b-200">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4421b-201">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4421b-201">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4421b-202">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-202">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4421b-203">Vaya a la sección **Certificado de firma de SAML** y haga clic en el valor de la columna **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-203">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="4421b-204">Según lo que necesite la aplicación para configurar el inicio de sesión único, verá la opción para descargar el archivo XML de metadatos o el certificado.</span><span class="sxs-lookup"><span data-stu-id="4421b-204">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="4421b-205">Azure AD no proporciona una dirección URL para obtener los metadatos.</span><span class="sxs-lookup"><span data-stu-id="4421b-205">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="4421b-206">Solo se pueden recuperar como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="4421b-206">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="4421b-207">Configuración del inicio de sesión único federado para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="4421b-207">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="4421b-208">Para configurar una aplicación ajena a la galería, debe tener Azure AD Premium y que la aplicación admita SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="4421b-208">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="4421b-209">Para más información acerca de las versiones de Azure AD, visite [Precios de Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="4421b-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="4421b-210">Configuración de los valores de los metadatos de la aplicación en Azure AD (URL de inicio de sesión, identificador, URL de respuesta)</span><span class="sxs-lookup"><span data-stu-id="4421b-210">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="4421b-211">Selección del identificador de usuario e incorporación de los atributos de usuario para enviarlos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="4421b-211">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="4421b-212">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="4421b-213">Configuración de los valores de los metadatos de Azure AD en la aplicación (URL de inicio de sesión, emisor, URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="4421b-213">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="4421b-214">Configuración de los valores de los metadatos de la aplicación en Azure AD (URL de inicio de sesión, identificador, URL de respuesta)</span><span class="sxs-lookup"><span data-stu-id="4421b-214">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="4421b-215">Para configurar el inicio de sesión único para una aplicación ajena a la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-215">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-216">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="4421b-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4421b-217">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-218">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-219">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-219">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-220">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4421b-220">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="4421b-221">En la sección **Agregar aplicación propia**, haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="4421b-221">click **Non-gallery application** in the **Add your own app** section.</span></span>

7.  <span data-ttu-id="4421b-222">Escriba el nombre de la aplicación en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="4421b-222">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="4421b-223">Haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-223">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="4421b-224">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-224">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="4421b-225">En la lista desplegable **Modo**, seleccione **Inicio de sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="4421b-225">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="4421b-226">Especifique los valores obligatorios en **Dominio y direcciones URL**.</span><span class="sxs-lookup"><span data-stu-id="4421b-226">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="4421b-227">El proveedor de la aplicación le proporcionará estos valores.</span><span class="sxs-lookup"><span data-stu-id="4421b-227">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="4421b-228">Para configurar la aplicación como SSO iniciado por el IdP, escriba la dirección URL de respuesta y el identificador.</span><span class="sxs-lookup"><span data-stu-id="4421b-228">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2.  <span data-ttu-id="4421b-229">**Opcional:** para configurar la aplicación como SSO iniciado por el SP, la dirección URL de inicio de sesión es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="4421b-229">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="4421b-230">En **Atributos de usuario**, seleccione el identificador único para los usuarios de la lista desplegable **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="4421b-230">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="4421b-231">**Opcional:** haga clic en **Ver y editar todos los demás atributos de usuario** para editar los atributos que se enviarán a la aplicación en el token de SAML cuando el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="4421b-231">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="4421b-232">Para agregar un atributo:</span><span class="sxs-lookup"><span data-stu-id="4421b-232">To add an attribute:</span></span>

   1. <span data-ttu-id="4421b-233">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="4421b-233">click **Add attribute**.</span></span> <span data-ttu-id="4421b-234">Escriba el **Nombre** y seleccione el **Valor** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="4421b-234">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="4421b-235">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-235">Click **Save.**</span></span> <span data-ttu-id="4421b-236">En la tabla verá el nuevo atributo.</span><span class="sxs-lookup"><span data-stu-id="4421b-236">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="4421b-237">Haga clic en **Configurar &lt;nombre de la aplicación&gt;** para acceder a documentación sobre cómo configurar el inicio de sesión único en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-237">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="4421b-238">Además, tiene las direcciones URL de Azure AD y los certificados necesarios para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-238">Also, you has Azure AD URLs and certificate required for the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="4421b-239">Selección del identificador de usuario e incorporación de los atributos de usuario para enviarlos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="4421b-239">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="4421b-240">Para seleccionar el identificador de usuario o agregar atributos de usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-240">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-241">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="4421b-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4421b-242">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-243">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-244">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-244">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-245">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4421b-245">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4421b-246">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="4421b-246">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4421b-247">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4421b-247">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4421b-248">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-248">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4421b-249">En la sección **Atributos de usuario**, seleccione el identificador único para los usuarios de la lista desplegable **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="4421b-249">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="4421b-250">La opción seleccionada debe coincidir con el valor esperado de la aplicación para autenticar al usuario.</span><span class="sxs-lookup"><span data-stu-id="4421b-250">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="4421b-251">AD Azure selecciona el formato del atributo NameID (Identificador de usuario) en función del valor seleccionado o del formato que solicite la aplicación en el elemento AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="4421b-251">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="4421b-252">Para más información, visite la sección NameIDPolicy del artículo [Protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="4421b-252">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="4421b-253">Para agregar atributos de usuario, haga clic en **Ver y editar todos los demás atributos de usuario** para editar los atributos que se enviarán a la aplicación en el token de SAML cuando el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="4421b-253">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="4421b-254">Para agregar un atributo:</span><span class="sxs-lookup"><span data-stu-id="4421b-254">To add an attribute:</span></span>

   1. <span data-ttu-id="4421b-255">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="4421b-255">click **Add attribute**.</span></span> <span data-ttu-id="4421b-256">Escriba el **Nombre** y seleccione el **Valor** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="4421b-256">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="4421b-257">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-257">Click **Save.**</span></span> <span data-ttu-id="4421b-258">En la tabla verá el nuevo atributo.</span><span class="sxs-lookup"><span data-stu-id="4421b-258">You see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="4421b-259">Descarga del certificado o los metadatos de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-259">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="4421b-260">Para descargar el certificado o los metadatos de la aplicación de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-260">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-261">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="4421b-261">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4421b-262">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-262">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-263">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-263">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-264">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-264">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-265">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4421b-265">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4421b-266">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="4421b-266">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4421b-267">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4421b-267">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4421b-268">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-268">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4421b-269">Vaya a la sección **Certificado de firma de SAML** y haga clic en el valor de la columna **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-269">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="4421b-270">Según lo que necesite la aplicación para configurar el inicio de sesión único, verá la opción para descargar el archivo XML de metadatos o el certificado.</span><span class="sxs-lookup"><span data-stu-id="4421b-270">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="4421b-271">Azure AD no proporciona una dirección URL para obtener los metadatos.</span><span class="sxs-lookup"><span data-stu-id="4421b-271">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="4421b-272">Solo se pueden recuperar como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="4421b-272">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="4421b-273">Configuración del inicio de sesión único con contraseña para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-273">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="4421b-274">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-274">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="4421b-275">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-275">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="4421b-276">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="4421b-276">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="4421b-277">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4421b-277">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="4421b-278">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-278">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-279">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **administrador global** o **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="4421b-279">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="4421b-280">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-280">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-281">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-281">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-282">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-282">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-283">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4421b-283">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="4421b-284">En el cuadro de texto **Escriba un nombre** de la sección **Agregar desde la galería**, escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-284">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="4421b-285">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4421b-285">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="4421b-286">Antes de agregar la aplicación, puede cambiar su nombre en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="4421b-286">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="4421b-287">Haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-287">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="4421b-288">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-288">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="4421b-289">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="4421b-289">Configure the application for password single sign-on</span></span>

<span data-ttu-id="4421b-290">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-290">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-291">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="4421b-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4421b-292">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-293">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-294">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-294">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-295">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4421b-295">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4421b-296">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="4421b-296">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4421b-297">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4421b-297">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4421b-298">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-298">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4421b-299">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4421b-299">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4421b-300">[Asigne usuarios a la aplicación](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="4421b-300">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="4421b-301">Además, también puede proporcionar credenciales en nombre del usuario; para ello, seleccione las filas de los usuarios, haga clic en **Actualizar credenciales** y escriba el nombre de usuario y la contraseña en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="4421b-301">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="4421b-302">En caso contrario, se solicitará a los usuarios que especifiquen ellos mismos las credenciales al inicio.</span><span class="sxs-lookup"><span data-stu-id="4421b-302">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="4421b-303">Configuración del inicio de sesión único con contraseña para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="4421b-303">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="4421b-304">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-304">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="4421b-305">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="4421b-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="4421b-306">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="4421b-306">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="4421b-307">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="4421b-307">Add a non-gallery application</span></span>

<span data-ttu-id="4421b-308">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-308">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-309">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="4421b-309">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="4421b-310">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-310">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-311">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-311">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-312">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-312">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-313">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4421b-313">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="4421b-314">Haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="4421b-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="4421b-315">Escriba el nombre de la aplicación en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="4421b-315">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="4421b-316">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-316">Select **Add.**</span></span>

<span data-ttu-id="4421b-317">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-317">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="4421b-318">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="4421b-318">Configure the application for password single sign-on</span></span>

<span data-ttu-id="4421b-319">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-319">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-320">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="4421b-320">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4421b-321">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-321">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-322">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-322">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-323">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-323">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-324">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4421b-324">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="4421b-325">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="4421b-325">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4421b-326">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4421b-326">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4421b-327">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-327">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4421b-328">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4421b-328">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4421b-329">Escriba la **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="4421b-329">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="4421b-330">Es la dirección URL en la que los usuarios escriben su nombre de usuario y contraseña para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="4421b-330">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="4421b-331">Asegúrese de que los campos de inicio de sesión estén visibles en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="4421b-331">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="4421b-332">[Asigne usuarios a la aplicación](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="4421b-332">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="4421b-333">Además, también puede proporcionar credenciales en nombre del usuario; para ello, seleccione las filas de los usuarios, haga clic en **Actualizar credenciales** y escriba el nombre de usuario y la contraseña en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="4421b-333">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="4421b-334">En caso contrario, se solicitará a los usuarios que especifiquen ellos mismos las credenciales al inicio.</span><span class="sxs-lookup"><span data-stu-id="4421b-334">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="4421b-335">Problemas relacionados con la asignación de aplicaciones a los usuarios</span><span class="sxs-lookup"><span data-stu-id="4421b-335">Problems related to assigning applications to users</span></span>

<span data-ttu-id="4421b-336">Puede que un usuario no vea una aplicación en su Panel de acceso porque no ha sido asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-336">A user may not be seeing an application on their Access Panel because they are not assigned to the application.</span></span> <span data-ttu-id="4421b-337">A continuación se muestran algunas maneras de comprobarlo:</span><span class="sxs-lookup"><span data-stu-id="4421b-337">Below are some ways to check:</span></span>

-   [<span data-ttu-id="4421b-338">Comprobación de si un usuario está asignado a la aplicación</span><span class="sxs-lookup"><span data-stu-id="4421b-338">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="4421b-339">Asignación de un usuario a una aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="4421b-339">How to assign a user to an application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="4421b-340">Comprobación de si un usuario posee una licencia relacionada con la aplicación</span><span class="sxs-lookup"><span data-stu-id="4421b-340">Check if a user is assigned to a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="4421b-341">Asignación de una licencia a un usuario</span><span class="sxs-lookup"><span data-stu-id="4421b-341">How to assign a license to a user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="4421b-342">Comprobación de si un usuario está asignado a la aplicación</span><span class="sxs-lookup"><span data-stu-id="4421b-342">Check if a user is assigned to the application</span></span>

<span data-ttu-id="4421b-343">Para comprobar si un usuario está asignado a la aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-343">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-344">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="4421b-344">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4421b-345">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-345">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-346">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-346">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-347">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-347">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-348">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4421b-348">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="4421b-349">**Busque** el nombre de la aplicación en cuestión.</span><span class="sxs-lookup"><span data-stu-id="4421b-349">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="4421b-350">Haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4421b-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="4421b-351">Compruebe si el usuario está asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-351">Check to see if your user is assigned to the application.</span></span>

   * <span data-ttu-id="4421b-352">Si no, siga los pasos descritos en "Asignación de un usuario a una aplicación directamente" para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="4421b-352">If not follow the steps in “How to assign a user to an application directly” to do so.</span></span>

### <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="4421b-353">Asignación de un usuario a una aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="4421b-353">How to assign a user to an application directly</span></span>

<span data-ttu-id="4421b-354">Para asignar uno o varios usuarios a una aplicación directamente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-354">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-355">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="4421b-355">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="4421b-356">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-356">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-357">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-357">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-358">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-358">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-359">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4421b-359">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4421b-360">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="4421b-360">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4421b-361">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="4421b-361">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="4421b-362">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-362">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4421b-363">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4421b-363">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="4421b-364">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4421b-364">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="4421b-365">Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="4421b-365">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="4421b-366">Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="4421b-366">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="4421b-367">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="4421b-367">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="4421b-368">**Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="4421b-368">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="4421b-369">Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-369">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="4421b-370">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="4421b-370">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="4421b-371">Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="4421b-371">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="4421b-372">Tras un breve período, los usuarios que seleccionó podrán iniciar estas aplicaciones en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4421b-372">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="4421b-373">Comprobación de si un usuario posee una licencia relacionada con la aplicación</span><span class="sxs-lookup"><span data-stu-id="4421b-373">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="4421b-374">Para comprobar las licencias asignadas de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-374">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-375">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="4421b-375">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4421b-376">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-376">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-377">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-377">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-378">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="4421b-378">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4421b-379">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4421b-379">click **All users**.</span></span>

6.  <span data-ttu-id="4421b-380">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="4421b-380">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4421b-381">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el usuario.</span><span class="sxs-lookup"><span data-stu-id="4421b-381">click **Licenses** to see which licenses the user currently has assigned.</span></span>

  * <span data-ttu-id="4421b-382">Si el usuario está asignado a una licencia de Office, esto permitirá que las aplicaciones de Office aparezcan en el panel de acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="4421b-382">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-user-a-license"></a><span data-ttu-id="4421b-383">Asignación de una licencia a un usuario</span><span class="sxs-lookup"><span data-stu-id="4421b-383">How to assign a user a license</span></span> 

<span data-ttu-id="4421b-384">Para asignar una licencia a un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-384">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-385">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="4421b-385">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4421b-386">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-386">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-387">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-387">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-388">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="4421b-388">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4421b-389">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4421b-389">click **All users**.</span></span>

6.  <span data-ttu-id="4421b-390">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="4421b-390">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4421b-391">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el usuario.</span><span class="sxs-lookup"><span data-stu-id="4421b-391">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="4421b-392">Haga clic en el botón **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-392">click the **Assign** button.</span></span>

9.  <span data-ttu-id="4421b-393">Seleccione **uno o más productos** en la lista de productos disponibles.</span><span class="sxs-lookup"><span data-stu-id="4421b-393">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="4421b-394">**Opcional**: Haga clic en el elemento **Opciones de asignación** para asignar productos de forma granular.</span><span class="sxs-lookup"><span data-stu-id="4421b-394">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="4421b-395">Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="4421b-396">Haga clic en el botón **Asignar** para asignar estas licencias a este usuario.</span><span class="sxs-lookup"><span data-stu-id="4421b-396">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="4421b-397">Problemas relacionados con la asignación de aplicaciones a grupos</span><span class="sxs-lookup"><span data-stu-id="4421b-397">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="4421b-398">Puede que un usuario vea una aplicación en su Panel de acceso porque forme parte de un grupo al que se ha asignado esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="4421b-399">A continuación se muestran algunas maneras de comprobarlo:</span><span class="sxs-lookup"><span data-stu-id="4421b-399">Below are some ways to check:</span></span>

-   [<span data-ttu-id="4421b-400">Comprobación de la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="4421b-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="4421b-401">Asignación de una aplicación a un grupo directamente</span><span class="sxs-lookup"><span data-stu-id="4421b-401">How to assign an application to a group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="4421b-402">Comprobación de si un usuario es miembro de un grupo asignado a una licencia</span><span class="sxs-lookup"><span data-stu-id="4421b-402">Check if a user is part of group assigned to a license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="4421b-403">Asignación de una licencia a un grupo</span><span class="sxs-lookup"><span data-stu-id="4421b-403">How to assign a license to a group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="4421b-404">Comprobación de la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="4421b-404">Check a user’s group memberships</span></span>

<span data-ttu-id="4421b-405">Para comprobar la pertenencia de un grupo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-405">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-406">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="4421b-406">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4421b-407">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-407">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-408">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-408">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-409">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="4421b-409">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4421b-410">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4421b-410">click **All users**.</span></span>

6.  <span data-ttu-id="4421b-411">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="4421b-411">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4421b-412">Haga clic en **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="4421b-412">click **Groups**.</span></span>

8.  <span data-ttu-id="4421b-413">Compruebe si el usuario forma parte de un grupo que se ha asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-413">Check to see if your user is part of a Group assigned to the application.</span></span>

  * <span data-ttu-id="4421b-414">Si desea quitar el usuario del grupo, **haga clic en la fila** del grupo y seleccione Eliminar.</span><span class="sxs-lookup"><span data-stu-id="4421b-414">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="how-to-assign-an-application-to-a-group-directly"></a><span data-ttu-id="4421b-415">Asignación de una aplicación a un grupo directamente</span><span class="sxs-lookup"><span data-stu-id="4421b-415">How to assign an application to a group directly</span></span>

<span data-ttu-id="4421b-416">Para asignar uno o varios grupos a una aplicación directamente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-416">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-417">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="4421b-417">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="4421b-418">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-418">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-419">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-419">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-420">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4421b-420">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4421b-421">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4421b-421">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4421b-422">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="4421b-422">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4421b-423">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="4421b-423">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="4421b-424">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-424">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4421b-425">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4421b-425">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="4421b-426">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4421b-426">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="4421b-427">Escriba el **nombre completo** del grupo al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="4421b-427">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="4421b-428">Mantenga el puntero sobre el **grupo** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="4421b-428">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="4421b-429">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del grupo para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="4421b-429">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="4421b-430">**Opcional**: si desea **agregar más de un grupo**, escriba otro **nombre de grupo completo** o en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese grupo a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="4421b-430">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="4421b-431">Cuando haya terminado de seleccionar grupos, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4421b-431">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="4421b-432">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los grupos que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="4421b-432">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="4421b-433">Haga clic en el botón **Asignar** para asignar la aplicación a los grupos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="4421b-433">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="4421b-434">Tras un breve período, los usuarios que seleccionó podrán iniciar estas aplicaciones en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4421b-434">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-to-a-license"></a><span data-ttu-id="4421b-435">Comprobación de si un usuario es miembro de un grupo asignado a una licencia</span><span class="sxs-lookup"><span data-stu-id="4421b-435">Check if a user is part of group assigned to a license</span></span>

1.  <span data-ttu-id="4421b-436">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="4421b-436">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4421b-437">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-437">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-438">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-438">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-439">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="4421b-439">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4421b-440">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4421b-440">click **All users**.</span></span>

6.  <span data-ttu-id="4421b-441">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="4421b-441">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4421b-442">Haga clic en **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="4421b-442">click **Groups**.</span></span>

8.  <span data-ttu-id="4421b-443">Haga clic en la fila de un grupo específico.</span><span class="sxs-lookup"><span data-stu-id="4421b-443">click the row of a specific group.</span></span>

9.  <span data-ttu-id="4421b-444">Haga clic en **Licencias** para ver qué licencias tiene asignadas el grupo.</span><span class="sxs-lookup"><span data-stu-id="4421b-444">click **Licenses** to see which licenses the group has assigned to it.</span></span>

   * <span data-ttu-id="4421b-445">Si el grupo está asignado a una licencia de Office, esto permitirá que determinadas aplicaciones de Office aparezcan en el Panel de acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="4421b-445">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-license-to-a-group"></a><span data-ttu-id="4421b-446">Asignación de una licencia a un grupo</span><span class="sxs-lookup"><span data-stu-id="4421b-446">How to assign a license to a group</span></span>

<span data-ttu-id="4421b-447">Para asignar una licencia a un grupo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4421b-447">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="4421b-448">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="4421b-448">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4421b-449">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="4421b-449">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4421b-450">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4421b-450">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4421b-451">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="4421b-451">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4421b-452">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="4421b-452">click **All groups**.</span></span>

6.  <span data-ttu-id="4421b-453">**Busque** el grupo en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="4421b-453">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4421b-454">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el grupo.</span><span class="sxs-lookup"><span data-stu-id="4421b-454">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="4421b-455">Haga clic en el botón **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-455">click the **Assign** button.</span></span>

9.  <span data-ttu-id="4421b-456">Seleccione **uno o más productos** en la lista de productos disponibles.</span><span class="sxs-lookup"><span data-stu-id="4421b-456">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="4421b-457">**Opcional**: Haga clic en el elemento **Opciones de asignación** para asignar productos de forma granular.</span><span class="sxs-lookup"><span data-stu-id="4421b-457">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="4421b-458">Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4421b-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="4421b-459">Haga clic en el botón **Asignar** para asignar estas licencias a este grupo.</span><span class="sxs-lookup"><span data-stu-id="4421b-459">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="4421b-460">Esta operación puede tardar mucho tiempo, en función del tamaño y la complejidad del grupo.</span><span class="sxs-lookup"><span data-stu-id="4421b-460">This may take a long time, depending on the size and complexity of the group.</span></span>

>[!NOTE]
><span data-ttu-id="4421b-461">Para acelerar el proceso, considere la posibilidad de asignar temporalmente una licencia al usuario directamente.</span><span class="sxs-lookup"><span data-stu-id="4421b-461">To do this faster, consider temporarily assigning a license to the user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="4421b-462">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4421b-462">Next steps</span></span>
[<span data-ttu-id="4421b-463">Adición de nuevos usuarios a Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4421b-463">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

