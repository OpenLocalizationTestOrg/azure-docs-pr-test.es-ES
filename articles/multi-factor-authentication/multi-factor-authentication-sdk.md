---
title: kit de desarrollo de software de aaaMFA para aplicaciones personalizadas | Documentos de Microsoft
description: "Este artículo muestra cómo toodownload y uso Hola verificacion de tooenable de MFA de Azure SDK para las aplicaciones personalizadas."
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
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="884f5-103">Creación de Multi-Factor Authentication en aplicaciones personalizadas (SDK)</span><span class="sxs-lookup"><span data-stu-id="884f5-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="884f5-104">Hola permite del Kit de desarrollo de Software (SDK) de Azure Multi-factor Authentication de Hello en que crear verificacion directamente inicio de sesión o procesa transacciones de aplicaciones en su inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="884f5-104">hello Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into hello sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="884f5-105">Hola SDK de autenticación multifactor está disponible para C#, Visual Basic (. NET), Java, Perl, PHP y Ruby.</span><span class="sxs-lookup"><span data-stu-id="884f5-105">hello Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="884f5-106">Hola SDK proporciona un contenedor fino alrededor de verificación en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="884f5-106">hello SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="884f5-107">Todo lo que necesita toowrite el código, incluidos los archivos de código fuente comentado, archivos de ejemplo y un archivo Léame detallado incluye.</span><span class="sxs-lookup"><span data-stu-id="884f5-107">It includes everything you need toowrite your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="884f5-108">Cada SDK también incluye un certificado y clave privada para cifrar las transacciones que están tooyour único proveedor de autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="884f5-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique tooyour Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="884f5-109">Siempre y cuando tenga un proveedor, puede descargar Hola SDK en tantos idiomas y formatos como necesite.</span><span class="sxs-lookup"><span data-stu-id="884f5-109">As long as you have a provider, you can download hello SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="884f5-110">estructura de Hola de hello API Hola SDK de autenticación multifactor es simple.</span><span class="sxs-lookup"><span data-stu-id="884f5-110">hello structure of hello APIs in hello Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="884f5-111">Realizar una sola función llamada API tooan con parámetros de opción de multifactor hello (por ejemplo, el modo de comprobación) y los datos de usuario (por ejemplo, toocall de número de teléfono de Hola u Hola PIN número toovalidate).</span><span class="sxs-lookup"><span data-stu-id="884f5-111">Make a single function call tooan API with hello multi-factor option parameters (like verification mode) and user data (like hello telephone number toocall or hello PIN number toovalidate).</span></span> <span data-ttu-id="884f5-112">Hello API convierten llamada de función de hello en toohello de las solicitudes de servicios web servicio basado en la nube de Azure Multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="884f5-112">hello APIs translate hello function call into web services requests toohello cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="884f5-113">Todas las llamadas deben incluir un certificado privado de toohello de referencia que se incluye en todos los SDK.</span><span class="sxs-lookup"><span data-stu-id="884f5-113">All calls must include a reference toohello private certificate that is included in every SDK.</span></span>

<span data-ttu-id="884f5-114">Porque Hola API no tienen toousers acceso registrado en Azure Active Directory, debe proporcionar información de usuario en un archivo o una base de datos.</span><span class="sxs-lookup"><span data-stu-id="884f5-114">Because hello APIs do not have access toousers registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="884f5-115">Además, Hola API no proporcionan características de administración de inscripción o el usuario, por lo que necesita toobuild estos procesos en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="884f5-115">Also, hello APIs do not provide enrollment or user management features, so you need toobuild these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="884f5-116">toodownload Hola SDK, deberá toocreate un proveedor de autenticación multifactor de Azure incluso si tienen licencias de Azure MFA, AAD Premium o EMS.</span><span class="sxs-lookup"><span data-stu-id="884f5-116">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="884f5-117">Si crea un proveedor de autenticación multifactor de Azure para este propósito y ya tiene licencias, asegúrese de hello seguro toocreate proveedor con hello **por usuario habilitado** modelo.</span><span class="sxs-lookup"><span data-stu-id="884f5-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="884f5-118">A continuación, vincular directorio Hola de toohello del proveedor que contiene las licencias de MFA de Azure, Azure AD Premium o EMS de Hola.</span><span class="sxs-lookup"><span data-stu-id="884f5-118">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="884f5-119">Esta configuración garantiza que solo se le facturará si tiene más usuarios únicos mediante Hola SDK que número Hola de licencias que posee.</span><span class="sxs-lookup"><span data-stu-id="884f5-119">This configuration ensures that you are only billed if you have more unique users using hello SDK than hello number of licenses you own.</span></span>


## <a name="download-hello-sdk"></a><span data-ttu-id="884f5-120">Descargar Hola SDK</span><span class="sxs-lookup"><span data-stu-id="884f5-120">Download hello SDK</span></span>
<span data-ttu-id="884f5-121">Descargar hello Azure multifactor SDK requiere una [proveedor de autenticación multifactor de Azure](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="884f5-121">Downloading hello Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="884f5-122">Para ello, se necesita una suscripción de Azure completa, aunque se cuenten con licencias de Azure MFA, Azure AD Premium o Enterprise Mobility Suite.</span><span class="sxs-lookup"><span data-stu-id="884f5-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="884f5-123">Hola toodownload SDK, navegue toohello Portal de administración de varios factores.</span><span class="sxs-lookup"><span data-stu-id="884f5-123">toodownload hello SDK, navigate toohello Multi-Factor Management Portal.</span></span> <span data-ttu-id="884f5-124">Se pueden obtener acceso Hola portal mediante la administración del proveedor de autenticación multifactor directamente hello, o haciendo clic en hello **"Go toohello portal"** vínculo en la página de configuración de servicio de hello MFA.</span><span class="sxs-lookup"><span data-stu-id="884f5-124">You can reach hello portal either by managing hello Multi-Factor Auth Provider directly, or by clicking hello **"Go toohello portal"** link on hello MFA service settings page.</span></span>

### <a name="download-from-hello-azure-classic-portal"></a><span data-ttu-id="884f5-125">Descargar desde Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="884f5-125">Download from hello Azure classic portal</span></span>
1. <span data-ttu-id="884f5-126">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) como administrador.</span><span class="sxs-lookup"><span data-stu-id="884f5-126">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="884f5-127">Hola izquierda, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="884f5-127">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="884f5-128">En página de Active Directory de hello, en, seleccione superior hello **proveedores de autenticación multifactor**</span><span class="sxs-lookup"><span data-stu-id="884f5-128">On hello Active Directory page, at hello top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="884f5-129">En la parte inferior de hello seleccione **administrar**.</span><span class="sxs-lookup"><span data-stu-id="884f5-129">At hello bottom select **Manage**.</span></span> <span data-ttu-id="884f5-130">Se abrirá una nueva página.</span><span class="sxs-lookup"><span data-stu-id="884f5-130">A new page opens.</span></span>
5. <span data-ttu-id="884f5-131">En hello izquierdo, en la parte inferior de hello, haga clic en **SDK**.</span><span class="sxs-lookup"><span data-stu-id="884f5-131">On hello left, at hello bottom, click **SDK**.</span></span>
   <span data-ttu-id="884f5-132"><center>![Descargar](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="884f5-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="884f5-133">Seleccione Hola idioma que desee y haga clic en vínculos de descarga correspondientes Hola uno.</span><span class="sxs-lookup"><span data-stu-id="884f5-133">Select hello language you want and click one hello associated download links.</span></span>
7. <span data-ttu-id="884f5-134">Guardar archivo descargado Hola.</span><span class="sxs-lookup"><span data-stu-id="884f5-134">Save hello download.</span></span>

### <a name="download-from-hello-service-settings"></a><span data-ttu-id="884f5-135">Descargar de la configuración del servicio Hola</span><span class="sxs-lookup"><span data-stu-id="884f5-135">Download from hello service settings</span></span>
1. <span data-ttu-id="884f5-136">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) como administrador.</span><span class="sxs-lookup"><span data-stu-id="884f5-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="884f5-137">Hola izquierda, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="884f5-137">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="884f5-138">Haga doble clic en la instancia de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="884f5-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="884f5-139">Haga clic en superior de hello **configurar**</span><span class="sxs-lookup"><span data-stu-id="884f5-139">At hello top click **Configure**</span></span>
5. <span data-ttu-id="884f5-140">En Multi-Factor Authentication, seleccione **Administrar configuración del servicio**
   ![Descargar](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="884f5-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="884f5-141">En la página de configuración de servicios de hello, en la parte inferior de Hola de pantalla de bienvenida, haga clic en **Go toohello portal**.</span><span class="sxs-lookup"><span data-stu-id="884f5-141">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="884f5-142">Se abrirá una nueva página.</span><span class="sxs-lookup"><span data-stu-id="884f5-142">A new page opens.</span></span>
   <span data-ttu-id="884f5-143">![Descargar](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="884f5-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="884f5-144">En hello izquierdo, en la parte inferior de hello, haga clic en **SDK**.</span><span class="sxs-lookup"><span data-stu-id="884f5-144">On hello left, at hello bottom, click **SDK**.</span></span>
8. <span data-ttu-id="884f5-145">Seleccione Hola idioma que desee y haga clic en vínculos de descarga correspondientes Hola uno.</span><span class="sxs-lookup"><span data-stu-id="884f5-145">Select hello language you want and click one hello associated download links.</span></span>
9. <span data-ttu-id="884f5-146">Guardar archivo descargado Hola.</span><span class="sxs-lookup"><span data-stu-id="884f5-146">Save hello download.</span></span>

## <a name="whats-in-hello-sdk"></a><span data-ttu-id="884f5-147">¿Qué es Hola SDK</span><span class="sxs-lookup"><span data-stu-id="884f5-147">What's in hello SDK</span></span>
<span data-ttu-id="884f5-148">Hola SDK incluye Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="884f5-148">hello SDK includes hello following items:</span></span>

* <span data-ttu-id="884f5-149">**LÉAME**.</span><span class="sxs-lookup"><span data-stu-id="884f5-149">**README**.</span></span> <span data-ttu-id="884f5-150">Explica cómo toouse Hola a las API de autenticación multifactor en una aplicación nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="884f5-150">Explains how toouse hello Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="884f5-151">**Archivos de origen** para Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="884f5-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="884f5-152">**Certificado de cliente** que usar toocommunicate con hello servicio de la autenticación multifactor</span><span class="sxs-lookup"><span data-stu-id="884f5-152">**Client certificate** that you use toocommunicate with hello Multi-Factor Authentication service</span></span>
* <span data-ttu-id="884f5-153">**Clave privada** certificado Hola</span><span class="sxs-lookup"><span data-stu-id="884f5-153">**Private key** for hello certificate</span></span>
* <span data-ttu-id="884f5-154">**Resultados de la llamada.**</span><span class="sxs-lookup"><span data-stu-id="884f5-154">**Call results.**</span></span> <span data-ttu-id="884f5-155">Una lista de códigos de resultado de la llamada.</span><span class="sxs-lookup"><span data-stu-id="884f5-155">A list of call result codes.</span></span> <span data-ttu-id="884f5-156">tooopen este archivo, utilice una aplicación con formato de texto, como WordPad.</span><span class="sxs-lookup"><span data-stu-id="884f5-156">tooopen this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="884f5-157">Hola uso llamar tootest de códigos de resultado y solucionar problemas de implementación de saludo de la autenticación multifactor en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="884f5-157">Use hello call result codes tootest and troubleshoot hello implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="884f5-158">No son códigos de estado de autenticación.</span><span class="sxs-lookup"><span data-stu-id="884f5-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="884f5-159">**Ejemplos.**</span><span class="sxs-lookup"><span data-stu-id="884f5-159">**Examples.**</span></span> <span data-ttu-id="884f5-160">Código de ejemplo para una implementación básica de funcionamiento de Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="884f5-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="884f5-161">certificado de cliente de Hello es un certificado privado único que se generó especialmente para usted.</span><span class="sxs-lookup"><span data-stu-id="884f5-161">hello client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="884f5-162">No comparta ni pierda este archivo.</span><span class="sxs-lookup"><span data-stu-id="884f5-162">Do not share or lose this file.</span></span> <span data-ttu-id="884f5-163">Es la seguridad de hello tooensuring clave de las comunicaciones con el servicio de la autenticación multifactor de Hola.</span><span class="sxs-lookup"><span data-stu-id="884f5-163">It’s your key tooensuring hello security of your communications with hello Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="884f5-164">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="884f5-164">Code sample</span></span>
<span data-ttu-id="884f5-165">Este ejemplo de código muestra cómo llamar toouse Hola API Hola voz de modo estándar de SDK de Azure Multi-factor Authentication tooadd a la aplicación de tooyour de comprobación.</span><span class="sxs-lookup"><span data-stu-id="884f5-165">This code sample shows you how toouse hello APIs in hello Azure Multi-Factor Authentication SDK tooadd standard mode voice call verification tooyour application.</span></span> <span data-ttu-id="884f5-166">Modo estándar es una llamada de teléfono que Hola tooby de usuario responde presionando la tecla # de Hola.</span><span class="sxs-lookup"><span data-stu-id="884f5-166">Standard mode is a telephone call that hello user responds tooby pressing hello # key.</span></span>

<span data-ttu-id="884f5-167">Este ejemplo utiliza Hola C# .NET 2.0 SDK Multi-factor Authentication en una aplicación ASP.NET básica con lógica de servidor de C#, pero el proceso de hello es similar en otros lenguajes.</span><span class="sxs-lookup"><span data-stu-id="884f5-167">This example uses hello C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but hello process is similar in other languages.</span></span> <span data-ttu-id="884f5-168">Hola SDK incluye los archivos de origen, no archivos ejecutables, puede generar archivos de Hola y hace referencia a ellas o incluirlos directamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="884f5-168">Because hello SDK includes source files, not executable files, you can build hello files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="884f5-169">Al implementar la autenticación multifactor, use métodos adicionales de hello (llamada de teléfono o mensaje de texto) como comprobación secundaria o terciaria toosupplement su método de autenticación principal (nombre de usuario y contraseña).</span><span class="sxs-lookup"><span data-stu-id="884f5-169">When implementing Multi-Factor Authentication, use hello additional methods (phone call or text message) as secondary or tertiary verification toosupplement your primary authentication method (username and password).</span></span> <span data-ttu-id="884f5-170">Estos métodos no están diseñados como métodos de autenticación principal.</span><span class="sxs-lookup"><span data-stu-id="884f5-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="884f5-171">Información general del ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="884f5-171">Code Sample Overview</span></span>
<span data-ttu-id="884f5-172">Este código de ejemplo para una aplicación web simple demostración usa una llamada telefónica con un # respuesta clave tooverify Hola autenticación del usuario.</span><span class="sxs-lookup"><span data-stu-id="884f5-172">This sample code for a simple web demo application uses a telephone call with a # key response tooverify hello user's authentication.</span></span> <span data-ttu-id="884f5-173">Este factor de llamada de teléfono se conoce en la Multi-Factor Authentication como modo estándar.</span><span class="sxs-lookup"><span data-stu-id="884f5-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="884f5-174">código del lado cliente Hello no incluye los elementos específicos de la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="884f5-174">hello client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="884f5-175">Dado que los factores de autenticación adicionales de hello son independientes de autenticación principal hello, puede agregarlos sin cambiar la interfaz de inicio de sesión existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="884f5-175">Because hello additional authentication factors are independent of hello primary authentication, you can add them without changing hello existing sign-on interface.</span></span> <span data-ttu-id="884f5-176">Hola API Hola SDK multifactor le permite personalizar la experiencia del usuario hello, pero puede que no tenga toochange nada en absoluto.</span><span class="sxs-lookup"><span data-stu-id="884f5-176">hello APIs in hello Multi-Factor SDK let you customize hello user experience, but you might not need toochange anything at all.</span></span>

<span data-ttu-id="884f5-177">código del lado servidor Hello agrega la autenticación en modo estándar en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="884f5-177">hello server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="884f5-178">Crea un objeto PfAuthParams con parámetros de Hola que son necesarios para la comprobación de modo estándar: nombre de usuario, número de teléfono y el modo y Hola certificado de cliente de toohello de ruta de acceso (CertFilePath), que es necesario en cada llamada.</span><span class="sxs-lookup"><span data-stu-id="884f5-178">It creates a PfAuthParams object with hello parameters that are required for standard-mode verification: username, telephone number, and mode, and hello path toohello client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="884f5-179">Para ver una demostración de todos los parámetros de PfAuthParams, consulte el archivo de ejemplo de Hola Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="884f5-179">For a demonstration of all parameters in PfAuthParams, see hello Example file in hello SDK.</span></span>

<span data-ttu-id="884f5-180">A continuación, el código de hello pasa toohello pf_authenticate() función de hello PfAuthParams objeto.</span><span class="sxs-lookup"><span data-stu-id="884f5-180">Next, hello code passes hello PfAuthParams object toohello pf_authenticate() function.</span></span> <span data-ttu-id="884f5-181">valor devuelto de Hello indica Hola éxito o error de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="884f5-181">hello return value indicates hello success or failure of hello authentication.</span></span> <span data-ttu-id="884f5-182">Hola parámetros, callStatus y errorID, contienen información de resultado de llamada adicional.</span><span class="sxs-lookup"><span data-stu-id="884f5-182">hello out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="884f5-183">códigos de resultado de Hello llamada se documentan en el archivo de resultados de llamada de Hola Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="884f5-183">hello call result codes are documented in hello call results file in hello SDK.</span></span>

<span data-ttu-id="884f5-184">Esta implementación mínima puede escribirse en unas pocas líneas.</span><span class="sxs-lookup"><span data-stu-id="884f5-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="884f5-185">Sin embargo, en el código de producción, incluiría un tratamiento de errores más sofisticado, código de la base de datos adicional y una experiencia de usuario mejorada.</span><span class="sxs-lookup"><span data-stu-id="884f5-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="884f5-186">Código de cliente web</span><span class="sxs-lookup"><span data-stu-id="884f5-186">Web Client Code</span></span>
<span data-ttu-id="884f5-187">Hola aquí te mostramos código de cliente web de una página de demostración.</span><span class="sxs-lookup"><span data-stu-id="884f5-187">hello following is web client code for a demo page.</span></span>

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


### <a name="server-side-code"></a><span data-ttu-id="884f5-188">Código de servidor</span><span class="sxs-lookup"><span data-stu-id="884f5-188">Server-Side Code</span></span>
<span data-ttu-id="884f5-189">Hola después el código del lado servidor, la autenticación multifactor está configurada y se ejecute en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="884f5-189">In hello following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="884f5-190">Modo estándar (MODE_STANDARD) es que un usuario de llamada de teléfono toowhich Hola responde presionando la tecla # de Hola.</span><span class="sxs-lookup"><span data-stu-id="884f5-190">Standard mode (MODE_STANDARD) is a telephone call toowhich hello user responds by pressing hello # key.</span></span>

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
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
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
