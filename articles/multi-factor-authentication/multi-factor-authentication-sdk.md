---
title: Kit de desarrollo de software MFA para aplicaciones personalizadas | Microsoft Docs
description: "En este artículo se muestra cómo descargar y usar el SDK de Azure MFA para comprobar en dos pasos sus aplicaciones personalizadas."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 281f9c61a30a20027f69808600373aa272255ef6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="3d964-103">Creación de Multi-Factor Authentication en aplicaciones personalizadas (SDK)</span><span class="sxs-lookup"><span data-stu-id="3d964-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="3d964-104">El Kit de desarrollo de Software (SDK) de Multi-Factor Authentication de Azure le permite generar una comprobación en dos pasos directamente en los procesos de inicio de sesión o transacción de las aplicaciones de su inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d964-104">The Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into the sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="3d964-105">El SDK de Multi-Factor Authentication está disponible para C#, Visual Basic (.NET), Java, Perl, PHP y Ruby.</span><span class="sxs-lookup"><span data-stu-id="3d964-105">The Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="3d964-106">El SDK proporciona un contenedor fino en torno a la comprobación en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="3d964-106">The SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="3d964-107">Incluye todo lo que necesita para escribir su código, incluidos los archivos de código fuente comentados, los archivos de ejemplo y un archivo Léame detallado.</span><span class="sxs-lookup"><span data-stu-id="3d964-107">It includes everything you need to write your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="3d964-108">Cada SDK también incluye un certificado y una clave privada para cifrar transacciones que son únicos para su proveedor de Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="3d964-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique to your Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="3d964-109">Siempre y cuando tenga un proveedor, puede descargar el SDK en tantos idiomas y formatos como necesite.</span><span class="sxs-lookup"><span data-stu-id="3d964-109">As long as you have a provider, you can download the SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="3d964-110">La estructura de las API del SDK de Multi-Factor Authentication es sencilla.</span><span class="sxs-lookup"><span data-stu-id="3d964-110">The structure of the APIs in the Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="3d964-111">Cree una llamada de función única a una API con los parámetros de la opción de varios factores (como el modo de comprobación) y los datos de usuario (como el número de teléfono al que llamar o el número PIN que validar).</span><span class="sxs-lookup"><span data-stu-id="3d964-111">Make a single function call to an API with the multi-factor option parameters (like verification mode) and user data (like the telephone number to call or the PIN number to validate).</span></span> <span data-ttu-id="3d964-112">Las API convierten la llamada de función en solicitudes de servicios web al servicio Azure Multi-Factor Authentication basado en la nube.</span><span class="sxs-lookup"><span data-stu-id="3d964-112">The APIs translate the function call into web services requests to the cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="3d964-113">Todas las llamadas deben incluir una referencia al certificado privado que se incluye en todos los SDK.</span><span class="sxs-lookup"><span data-stu-id="3d964-113">All calls must include a reference to the private certificate that is included in every SDK.</span></span>

<span data-ttu-id="3d964-114">Dado que las API no tienen acceso a los usuarios registrados en Azure Active Directory, debe proporcionar información de usuario en un archivo o una base de datos.</span><span class="sxs-lookup"><span data-stu-id="3d964-114">Because the APIs do not have access to users registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="3d964-115">Además, las API no proporcionan funciones de administración de inscripciones o usuarios, por lo que necesitará crear estos procesos en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d964-115">Also, the APIs do not provide enrollment or user management features, so you need to build these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d964-116">Para descargar el SDK, debe crear un proveedor de Multi-Factor Auth de Azure, incluso si tiene licencias de Azure MFA, AAD Premium o EMS.</span><span class="sxs-lookup"><span data-stu-id="3d964-116">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="3d964-117">Si crea un proveedor de Multi-Factor Auth de Azure para este propósito y ya tiene licencias, asegúrese de crear el proveedor con el modelo **Por usuario habilitado**.</span><span class="sxs-lookup"><span data-stu-id="3d964-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure to create the Provider with the **Per Enabled User** model.</span></span> <span data-ttu-id="3d964-118">A continuación, vincule el proveedor al directorio que contiene las licencias de Azure MFA, Azure AD Premium o EMS.</span><span class="sxs-lookup"><span data-stu-id="3d964-118">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="3d964-119">Gracias a esta configuración, se asegura de que no se le cobrará, salvo que tenga más usuarios únicos mediante el SDK que el número de licencias que posee.</span><span class="sxs-lookup"><span data-stu-id="3d964-119">This configuration ensures that you are only billed if you have more unique users using the SDK than the number of licenses you own.</span></span>


## <a name="download-the-sdk"></a><span data-ttu-id="3d964-120">Descarga del SDK</span><span class="sxs-lookup"><span data-stu-id="3d964-120">Download the SDK</span></span>
<span data-ttu-id="3d964-121">Para descargar el SDK de Azure Multi-Factor, se requiere un [proveedor de autenticación multifactor](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="3d964-121">Downloading the Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="3d964-122">Para ello, se necesita una suscripción de Azure completa, aunque se cuenten con licencias de Azure MFA, Azure AD Premium o Enterprise Mobility Suite.</span><span class="sxs-lookup"><span data-stu-id="3d964-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="3d964-123">Para descargar el SDK, vaya al Portal de administración de Multi-Factor.</span><span class="sxs-lookup"><span data-stu-id="3d964-123">To download the SDK, navigate to the Multi-Factor Management Portal.</span></span> <span data-ttu-id="3d964-124">Puede tener acceso al portal administrando directamente el proveedor de Multi-Factor Auth o haciendo clic en el vínculo **"Ir al portal"** de la página de configuración del servicio MFA.</span><span class="sxs-lookup"><span data-stu-id="3d964-124">You can reach the portal either by managing the Multi-Factor Auth Provider directly, or by clicking the **"Go to the portal"** link on the MFA service settings page.</span></span>

### <a name="download-from-the-azure-classic-portal"></a><span data-ttu-id="3d964-125">Descarga desde el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="3d964-125">Download from the Azure classic portal</span></span>
1. <span data-ttu-id="3d964-126">Inicie sesión como administrador en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3d964-126">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="3d964-127">En la parte izquierda, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3d964-127">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="3d964-128">En la parte superior de la página Active Directory, seleccione **Proveedores de Multi-Factor Auth**</span><span class="sxs-lookup"><span data-stu-id="3d964-128">On the Active Directory page, at the top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="3d964-129">En la parte inferior, seleccione **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="3d964-129">At the bottom select **Manage**.</span></span> <span data-ttu-id="3d964-130">Se abrirá una nueva página.</span><span class="sxs-lookup"><span data-stu-id="3d964-130">A new page opens.</span></span>
5. <span data-ttu-id="3d964-131">A la izquierda, en la parte inferior, haga clic en **SDK**.</span><span class="sxs-lookup"><span data-stu-id="3d964-131">On the left, at the bottom, click **SDK**.</span></span>
   <span data-ttu-id="3d964-132"><center>![Descargar](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="3d964-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="3d964-133">Seleccione el idioma que desee y haga clic en uno de los vínculos de descarga asociados.</span><span class="sxs-lookup"><span data-stu-id="3d964-133">Select the language you want and click one the associated download links.</span></span>
7. <span data-ttu-id="3d964-134">Guarde el archivo descargado.</span><span class="sxs-lookup"><span data-stu-id="3d964-134">Save the download.</span></span>

### <a name="download-from-the-service-settings"></a><span data-ttu-id="3d964-135">Descarga desde la configuración del servicio</span><span class="sxs-lookup"><span data-stu-id="3d964-135">Download from the service settings</span></span>
1. <span data-ttu-id="3d964-136">Inicie sesión como administrador en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3d964-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="3d964-137">En la parte izquierda, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3d964-137">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="3d964-138">Haga doble clic en la instancia de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d964-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="3d964-139">En la parte superior, haga clic en **Configurar**</span><span class="sxs-lookup"><span data-stu-id="3d964-139">At the top click **Configure**</span></span>
5. <span data-ttu-id="3d964-140">En Multi-Factor Authentication, seleccione **Administrar configuración del servicio**
   ![Descargar](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="3d964-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="3d964-141">En la parte inferior de la página de configuración de servicios, haga clic en **Ir al portal**.</span><span class="sxs-lookup"><span data-stu-id="3d964-141">On the services settings page, at the bottom of the screen click **Go to the portal**.</span></span> <span data-ttu-id="3d964-142">Se abrirá una nueva página.</span><span class="sxs-lookup"><span data-stu-id="3d964-142">A new page opens.</span></span>
   <span data-ttu-id="3d964-143">![Descargar](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="3d964-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="3d964-144">A la izquierda, en la parte inferior, haga clic en **SDK**.</span><span class="sxs-lookup"><span data-stu-id="3d964-144">On the left, at the bottom, click **SDK**.</span></span>
8. <span data-ttu-id="3d964-145">Seleccione el idioma que desee y haga clic en uno de los vínculos de descarga asociados.</span><span class="sxs-lookup"><span data-stu-id="3d964-145">Select the language you want and click one the associated download links.</span></span>
9. <span data-ttu-id="3d964-146">Guarde el archivo descargado.</span><span class="sxs-lookup"><span data-stu-id="3d964-146">Save the download.</span></span>

## <a name="whats-in-the-sdk"></a><span data-ttu-id="3d964-147">Qué contiene el SDK</span><span class="sxs-lookup"><span data-stu-id="3d964-147">What's in the SDK</span></span>
<span data-ttu-id="3d964-148">El SDK incluye los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3d964-148">The SDK includes the following items:</span></span>

* <span data-ttu-id="3d964-149">**LÉAME**.</span><span class="sxs-lookup"><span data-stu-id="3d964-149">**README**.</span></span> <span data-ttu-id="3d964-150">Explica cómo usar las API de Multi-Factor Authentication en una aplicación nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="3d964-150">Explains how to use the Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="3d964-151">**Archivos de origen** para Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3d964-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="3d964-152">**Certificado de cliente** que se usa para comunicarse con el servicio Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3d964-152">**Client certificate** that you use to communicate with the Multi-Factor Authentication service</span></span>
* <span data-ttu-id="3d964-153">**Clave privada** para el certificado</span><span class="sxs-lookup"><span data-stu-id="3d964-153">**Private key** for the certificate</span></span>
* <span data-ttu-id="3d964-154">**Resultados de la llamada.**</span><span class="sxs-lookup"><span data-stu-id="3d964-154">**Call results.**</span></span> <span data-ttu-id="3d964-155">Una lista de códigos de resultado de la llamada.</span><span class="sxs-lookup"><span data-stu-id="3d964-155">A list of call result codes.</span></span> <span data-ttu-id="3d964-156">Para abrir este archivo, use una aplicación con formato de texto, como WordPad.</span><span class="sxs-lookup"><span data-stu-id="3d964-156">To open this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="3d964-157">Use los códigos de resultado de la llamada para probar y solucionar problemas de la implementación de Multi-Factor Authentication en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d964-157">Use the call result codes to test and troubleshoot the implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="3d964-158">No son códigos de estado de autenticación.</span><span class="sxs-lookup"><span data-stu-id="3d964-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="3d964-159">**Ejemplos.**</span><span class="sxs-lookup"><span data-stu-id="3d964-159">**Examples.**</span></span> <span data-ttu-id="3d964-160">Código de ejemplo para una implementación básica de funcionamiento de Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="3d964-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="3d964-161">El certificado de cliente es un certificado privado único que se generó especialmente para usted.</span><span class="sxs-lookup"><span data-stu-id="3d964-161">The client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="3d964-162">No comparta ni pierda este archivo.</span><span class="sxs-lookup"><span data-stu-id="3d964-162">Do not share or lose this file.</span></span> <span data-ttu-id="3d964-163">Es su clave para garantizar la seguridad de las comunicaciones con el servicio Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="3d964-163">It’s your key to ensuring the security of your communications with the Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="3d964-164">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3d964-164">Code sample</span></span>
<span data-ttu-id="3d964-165">Este ejemplo de código muestra cómo usar las API en el SDK de Azure Multi-Factor Authentication para agregar comprobación de llamadas de voz de modo estándar a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d964-165">This code sample shows you how to use the APIs in the Azure Multi-Factor Authentication SDK to add standard mode voice call verification to your application.</span></span> <span data-ttu-id="3d964-166">El modo estándar es una llamada de teléfono a la que el usuario responde presionando la tecla #.</span><span class="sxs-lookup"><span data-stu-id="3d964-166">Standard mode is a telephone call that the user responds to by pressing the # key.</span></span>

<span data-ttu-id="3d964-167">Este ejemplo usa el SDK de Multi-Factor Authentication C# .NET 2.0 en una aplicación ASP.NET básica con lógica de servidor de C#, pero el proceso es similar en otros idiomas.</span><span class="sxs-lookup"><span data-stu-id="3d964-167">This example uses the C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but the process is similar in other languages.</span></span> <span data-ttu-id="3d964-168">Dado que el SDK incluye archivos de origen, no archivos ejecutables, puede generar los archivos y hacer referencia a ellos o incluirlos directamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d964-168">Because the SDK includes source files, not executable files, you can build the files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="3d964-169">Al implementar Multi-Factor Authentication, use métodos adicionales (llamada de teléfono o mensaje de texto) como la comprobación secundaria o terciaria para complementar el método de autenticación principal (nombre de usuario y contraseña).</span><span class="sxs-lookup"><span data-stu-id="3d964-169">When implementing Multi-Factor Authentication, use the additional methods (phone call or text message) as secondary or tertiary verification to supplement your primary authentication method (username and password).</span></span> <span data-ttu-id="3d964-170">Estos métodos no están diseñados como métodos de autenticación principal.</span><span class="sxs-lookup"><span data-stu-id="3d964-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="3d964-171">Información general del ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="3d964-171">Code Sample Overview</span></span>
<span data-ttu-id="3d964-172">Este código de ejemplo para una aplicación de demostración web sencilla usa una llamada telefónica con una respuesta de clave # para comprobar la autenticación del usuario.</span><span class="sxs-lookup"><span data-stu-id="3d964-172">This sample code for a simple web demo application uses a telephone call with a # key response to verify the user's authentication.</span></span> <span data-ttu-id="3d964-173">Este factor de llamada de teléfono se conoce en la Multi-Factor Authentication como modo estándar.</span><span class="sxs-lookup"><span data-stu-id="3d964-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="3d964-174">El código de cliente no incluye ningún elemento específico de Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="3d964-174">The client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="3d964-175">Dado que los factores de autenticación adicionales son independientes de la autenticación principal, puede agregarlos sin cambiar la interfaz de inicio de sesión existente.</span><span class="sxs-lookup"><span data-stu-id="3d964-175">Because the additional authentication factors are independent of the primary authentication, you can add them without changing the existing sign-on interface.</span></span> <span data-ttu-id="3d964-176">Las API del SDK multifactor le permiten personalizar la experiencia del usuario, pero es posible que no tenga que cambiar nada en absoluto.</span><span class="sxs-lookup"><span data-stu-id="3d964-176">The APIs in the Multi-Factor SDK let you customize the user experience, but you might not need to change anything at all.</span></span>

<span data-ttu-id="3d964-177">El código de servidor agrega autenticación de modo estándar en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="3d964-177">The server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="3d964-178">Crea un objeto PfAuthParams con los parámetros necesarios para la comprobación de modo estándar: nombre de usuario, número de teléfono y modo, y la ruta de acceso al certificado de cliente (CertFilePath), que es necesario en cada llamada.</span><span class="sxs-lookup"><span data-stu-id="3d964-178">It creates a PfAuthParams object with the parameters that are required for standard-mode verification: username, telephone number, and mode, and the path to the client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="3d964-179">Para obtener una demostración de todos los parámetros en PfAuthParams, consulte el archivo de ejemplo en el SDK.</span><span class="sxs-lookup"><span data-stu-id="3d964-179">For a demonstration of all parameters in PfAuthParams, see the Example file in the SDK.</span></span>

<span data-ttu-id="3d964-180">A continuación, el código pasa el objeto PfAuthParams a la función pf_authenticate().</span><span class="sxs-lookup"><span data-stu-id="3d964-180">Next, the code passes the PfAuthParams object to the pf_authenticate() function.</span></span> <span data-ttu-id="3d964-181">El valor devuelto indica el éxito o fracaso de la autenticación.</span><span class="sxs-lookup"><span data-stu-id="3d964-181">The return value indicates the success or failure of the authentication.</span></span> <span data-ttu-id="3d964-182">Los parámetros de salida, callStatus y errorID, contienen información adicional del resultado de la llamada.</span><span class="sxs-lookup"><span data-stu-id="3d964-182">The out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="3d964-183">Los códigos de resultado de la llamada se documentan en el archivo de resultados de la llamada en el SDK.</span><span class="sxs-lookup"><span data-stu-id="3d964-183">The call result codes are documented in the call results file in the SDK.</span></span>

<span data-ttu-id="3d964-184">Esta implementación mínima puede escribirse en unas pocas líneas.</span><span class="sxs-lookup"><span data-stu-id="3d964-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="3d964-185">Sin embargo, en el código de producción, incluiría un tratamiento de errores más sofisticado, código de la base de datos adicional y una experiencia de usuario mejorada.</span><span class="sxs-lookup"><span data-stu-id="3d964-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="3d964-186">Código de cliente web</span><span class="sxs-lookup"><span data-stu-id="3d964-186">Web Client Code</span></span>
<span data-ttu-id="3d964-187">A continuación se facilita código de cliente web para una página de demostración.</span><span class="sxs-lookup"><span data-stu-id="3d964-187">The following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="3d964-188">Código de servidor</span><span class="sxs-lookup"><span data-stu-id="3d964-188">Server-Side Code</span></span>
<span data-ttu-id="3d964-189">En el siguiente código de servidor, Multi-Factor Authentication se configura y ejecuta en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="3d964-189">In the following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="3d964-190">El modo estándar (MODE_STANDARD) es una llamada de teléfono a la que el usuario responde presionando la tecla #.</span><span class="sxs-lookup"><span data-stu-id="3d964-190">Standard mode (MODE_STANDARD) is a telephone call to which the user responds by pressing the # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate the username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from the user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains the private key for the client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
