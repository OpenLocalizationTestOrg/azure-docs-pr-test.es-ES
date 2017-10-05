---
title: "Habilitación del inicio de sesión único entre aplicaciones en iOS mediante ADAL | Microsoft Docs"
description: "Cómo utilizar las características del SDK de ADAL para habilitar el inicio de sesión único entre las aplicaciones. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 73b8ed7e6a153a0790f7eae9bd51bb2e554ae72e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="e0cca-103">Habilitación del inicio de sesión único entre aplicaciones en iOS mediante ADAL</span><span class="sxs-lookup"><span data-stu-id="e0cca-103">How to enable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="e0cca-104">Actualmente, los clientes esperan disfrutar de un inicio de sesión único que les permita escribir sus credenciales una sola vez y que esas credenciales se propaguen automáticamente entre las diferentes aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e0cca-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="e0cca-105">La dificultad de escribir el nombre de usuario y contraseña en una pantalla pequeña, a menudo combinado con un factor adicional (2FA) como una llamada de teléfono o un código de mensaje de texto, provoca una rápida insatisfacción si el usuario tiene que hacer esto más de una vez para su producto.</span><span class="sxs-lookup"><span data-stu-id="e0cca-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="e0cca-106">Además, si aplica una plataforma de identidad que puedan usar otras aplicaciones, como cuentas Microsoft o una cuenta de trabajo de Office 365, los clientes esperan que las credenciales estén disponibles para todas sus aplicaciones, independientemente del proveedor.</span><span class="sxs-lookup"><span data-stu-id="e0cca-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="e0cca-107">La plataforma de Microsoft Identity, junto con los SDK correspondientes, se ocupa de este trabajo ingrato y le ofrece la posibilidad de satisfacer a sus clientes con el inicio de sesión único, ya sea dentro de su propio conjunto de aplicaciones o, como sucede con nuestra funcionalidad de agente y las aplicaciones de Authenticator, en todo el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e0cca-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="e0cca-108">Este tutorial le indicará cómo configurar nuestro SDK dentro de la aplicación para proporcionar esta ventaja a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="e0cca-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="e0cca-109">Este tutorial se aplica a:</span><span class="sxs-lookup"><span data-stu-id="e0cca-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="e0cca-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0cca-110">Azure Active Directory</span></span>
* <span data-ttu-id="e0cca-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="e0cca-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="e0cca-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="e0cca-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="e0cca-113">Acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0cca-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="e0cca-114">En el documento anterior se considera que tiene conocimientos acerca de cómo [aprovisionar aplicaciones en el portal heredado para Azure Active Directory](active-directory-how-to-integrate.md) y que ha integrado su aplicación con el [SDK de iOS de Microsoft Identity](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="e0cca-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="e0cca-115">Conceptos de inicio de sesión único en la plataforma de Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="e0cca-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="e0cca-116">Agentes de Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="e0cca-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="e0cca-117">Microsoft proporciona aplicaciones para todas las plataformas móviles que permiten el traspaso de credenciales entre aplicaciones de distintos proveedores, y habilita características mejoradas especiales que requieren un único lugar seguro desde el que validar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="e0cca-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="e0cca-118">A estas aplicaciones las llamamos **agentes**.</span><span class="sxs-lookup"><span data-stu-id="e0cca-118">We call these **brokers**.</span></span> <span data-ttu-id="e0cca-119">En iOS y Android, estos agentes se consiguen a través de aplicaciones descargables que los clientes instalan de forma independiente o bien se insertan en el dispositivo gracias a una empresa que administra el dispositivo de manera total o parcial para sus empleados.</span><span class="sxs-lookup"><span data-stu-id="e0cca-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="e0cca-120">Gracias a estos agentes, es posible administrar la seguridad de solo unas aplicaciones o bien del dispositivo en su totalidad, en función de lo que decidan los administradores de TI.</span><span class="sxs-lookup"><span data-stu-id="e0cca-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="e0cca-121">En Windows, esta funcionalidad se proporciona mediante un selector de cuentas integrado en el sistema operativo, que se conoce técnicamente como agente de autenticación web.</span><span class="sxs-lookup"><span data-stu-id="e0cca-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="e0cca-122">Para más información sobre el uso que hacemos de estos agentes y la percepción que tendrán de ellos sus clientes durante el proceso de inicio de sesión para la plataforma Microsoft Identity, siga leyendo.</span><span class="sxs-lookup"><span data-stu-id="e0cca-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="e0cca-123">Patrones para iniciar sesión en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="e0cca-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="e0cca-124">El acceso a credenciales en los dispositivos sigue dos patrones básicos para la plataforma Microsoft Identity:</span><span class="sxs-lookup"><span data-stu-id="e0cca-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="e0cca-125">Inicios de sesión no asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="e0cca-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="e0cca-126">Inicios de sesión asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="e0cca-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="e0cca-127">Inicios de sesión no asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="e0cca-127">Non-broker assisted logins</span></span>
<span data-ttu-id="e0cca-128">Los inicios de sesión no asistidos por agente son experiencias de inicio de sesión que ocurren en línea con la aplicación y usan el almacenamiento local en el dispositivo para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="e0cca-129">Este almacenamiento puede compartirse entre las aplicaciones, pero las credenciales están estrechamente vinculadas a la aplicación o al conjunto de aplicaciones que usan esa credencial.</span><span class="sxs-lookup"><span data-stu-id="e0cca-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="e0cca-130">Probablemente haya experimentado esto en muchas aplicaciones móviles en las que escribe un nombre de usuario y una contraseña en la propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="e0cca-131">Estos inicios de sesión tienen las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e0cca-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="e0cca-132">La experiencia de usuario se desarrolla por completo dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="e0cca-133">Las credenciales se pueden compartir entre aplicaciones que estén firmadas por el mismo certificado, proporcionando una experiencia de inicio de sesión único para el conjunto de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e0cca-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="e0cca-134">Se proporciona el control de la experiencia de inicio de sesión a la aplicación antes y después del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e0cca-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="e0cca-135">Estos inicios de sesión tienen las siguientes desventajas:</span><span class="sxs-lookup"><span data-stu-id="e0cca-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="e0cca-136">El usuario no puede experimentar el inicio de sesión único entre todas las aplicaciones que usan una identidad de Microsoft Identity, solo en aquellas identidades de Microsoft Identity que su aplicación ha configurado.</span><span class="sxs-lookup"><span data-stu-id="e0cca-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="e0cca-137">La aplicación no se puede usar con las características empresariales más avanzadas, como el acceso condicional, ni utilizar el conjunto de aplicaciones de InTune.</span><span class="sxs-lookup"><span data-stu-id="e0cca-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="e0cca-138">La aplicación no admite la autenticación basada en certificados para usuarios empresariales.</span><span class="sxs-lookup"><span data-stu-id="e0cca-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="e0cca-139">A continuación se representa el funcionamiento de los SDK de Microsoft Identity con el almacenamiento compartido de sus aplicaciones para habilitar el inicio de sesión único:</span><span class="sxs-lookup"><span data-stu-id="e0cca-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="e0cca-140">Inicios de sesión asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="e0cca-140">Broker assisted logins</span></span>
<span data-ttu-id="e0cca-141">Los inicios de sesión asistidos por agente son experiencias de inicio de sesión que se producen dentro de la aplicación del agente y usan el almacenamiento y la seguridad del agente para compartir las credenciales entre todas las aplicaciones del dispositivo que se aplican a la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="e0cca-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="e0cca-142">Esto significa que las aplicaciones dependen del agente para que los usuarios inicien sesión.</span><span class="sxs-lookup"><span data-stu-id="e0cca-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="e0cca-143">En iOS y Android, estos agentes se consiguen a través de aplicaciones descargables que los clientes instalan de forma independiente o bien se insertan en el dispositivo gracias a una empresa que administra el dispositivo para sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="e0cca-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="e0cca-144">Un ejemplo de este tipo de aplicación es la aplicación Microsoft Authenticator en iOS.</span><span class="sxs-lookup"><span data-stu-id="e0cca-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="e0cca-145">En Windows, esta funcionalidad se proporciona mediante un selector de cuentas integrado en el sistema operativo, que se conoce técnicamente como agente de autenticación web.</span><span class="sxs-lookup"><span data-stu-id="e0cca-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="e0cca-146">La experiencia varía según la plataforma y a veces puede ser problemática para los usuarios si no se administra correctamente.</span><span class="sxs-lookup"><span data-stu-id="e0cca-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="e0cca-147">Quizá este modelo le resulte más familiar si tiene instalada la aplicación Facebook y usa Facebook Connect desde otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="e0cca-148">La plataforma Microsoft Identity utiliza este mismo modelo.</span><span class="sxs-lookup"><span data-stu-id="e0cca-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="e0cca-149">En el caso de iOS, esto da lugar a una animación de "transición" en la que la aplicación se envía a un segundo plano y las aplicaciones de Microsoft Authenticator vienen al primer plano para que el usuario seleccione la cuenta en la que quiere iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="e0cca-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="e0cca-150">En el caso de Android y Windows, el selector de cuentas se muestra sobre la aplicación, lo cual interrumpe menos la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="e0cca-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="e0cca-151">¿Cómo se invoca el agente?</span><span class="sxs-lookup"><span data-stu-id="e0cca-151">How the broker gets invoked</span></span>
<span data-ttu-id="e0cca-152">Si se instala un agente compatible en el dispositivo, como la aplicación Microsoft Authenticator, los SDK de Microsoft Identity se ocuparán automáticamente de la tarea de invocar al agente cuando un usuario indique que quiere iniciar sesión con alguna de las cuentas de la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="e0cca-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="e0cca-153">Esta cuenta podría tratarse de una cuenta personal de Microsoft, una cuenta profesional o educativa o una cuenta que especifique y hospede en Azure mediante nuestros productos B2C y B2B.</span><span class="sxs-lookup"><span data-stu-id="e0cca-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="e0cca-154">Cómo se garantiza que la aplicación es válida</span><span class="sxs-lookup"><span data-stu-id="e0cca-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="e0cca-155">La necesidad de asegurar la identidad de una llamada de la aplicación al agente es fundamental para la seguridad que proporcionamos en los inicios de sesión asistidos por agente.</span><span class="sxs-lookup"><span data-stu-id="e0cca-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="e0cca-156">Ni IOS ni Android exigen identificadores únicos que solo son válidos para una aplicación determinada, por lo que aplicaciones malintencionadas pueden "suplantar" un identificador de la aplicación legítima y recibir los tokens destinados a la aplicación legítima.</span><span class="sxs-lookup"><span data-stu-id="e0cca-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="e0cca-157">Para asegurarse de que siempre se comunica con la aplicación correcta en tiempo de ejecución, le pedimos al desarrollador que proporcione un redirectURI personalizado al registrar su aplicación con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0cca-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="e0cca-158">**A continuación se describe cómo los desarrolladores deben diseñar este URI de redirección.**</span><span class="sxs-lookup"><span data-stu-id="e0cca-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="e0cca-159">Este redirectURI personalizado contiene el identificador de paquete de la aplicación y la App Store de Apple garantiza que es único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-159">This custom redirectURI contains the Bundle ID of the application and is ensured to be unique to the application by the Apple App Store.</span></span> <span data-ttu-id="e0cca-160">Cuando una aplicación llama al agente, este solicita al sistema operativo iOS que le proporcione el identificador de paquete que llamó al agente.</span><span class="sxs-lookup"><span data-stu-id="e0cca-160">When an application calls the broker, the broker asks the iOS operating system to provide it with the Bundle ID that called the broker.</span></span> <span data-ttu-id="e0cca-161">El agente proporciona este identificador a Microsoft en la llamada a nuestro sistema de identidad.</span><span class="sxs-lookup"><span data-stu-id="e0cca-161">The broker provides this Bundle ID to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="e0cca-162">Si el identificador de paquete de la aplicación no coincide con el identificador de paquete que el desarrollador nos ha proporcionado durante el registro, denegaremos el acceso a los tokens del recurso que está solicitando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-162">If the Bundle ID of the application does not match the Bundle ID provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="e0cca-163">Esta comprobación asegura que solo la aplicación registrada por el desarrollador recibe los tokens.</span><span class="sxs-lookup"><span data-stu-id="e0cca-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="e0cca-164">**El desarrollador tiene la opción de elegir si el SDK de Microsoft Identity llama al agente o usa el flujo sin asistencia del agente.**</span><span class="sxs-lookup"><span data-stu-id="e0cca-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="e0cca-165">Sin embargo, si el desarrollador decide no usar el flujo asistido por agente, no podrá beneficiarse del uso de las credenciales de SSO que el usuario puede ya haber agregado en el dispositivo; además, impide que la aplicación se use con las características empresariales que Microsoft proporciona a sus clientes, como el acceso condicional, las funcionalidades de administración de Intune y la autenticación basada en certificados.</span><span class="sxs-lookup"><span data-stu-id="e0cca-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="e0cca-166">Estos inicios de sesión tienen las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e0cca-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="e0cca-167">El usuario experimenta el inicio de sesión único en todas sus aplicaciones, con independencia del proveedor.</span><span class="sxs-lookup"><span data-stu-id="e0cca-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="e0cca-168">La aplicación puede usar las características empresariales más avanzadas, como el acceso condicional, o usar el conjunto de productos de InTune.</span><span class="sxs-lookup"><span data-stu-id="e0cca-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="e0cca-169">La aplicación puede admitir la autenticación basada en certificados para los usuarios empresariales.</span><span class="sxs-lookup"><span data-stu-id="e0cca-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="e0cca-170">La experiencia de inicio de sesión es mucho más segura, ya que tanto la identidad de la aplicación como el usuario se verifican por parte de la aplicación de agente con algoritmos de seguridad y sistemas de cifrado adicionales.</span><span class="sxs-lookup"><span data-stu-id="e0cca-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="e0cca-171">Estos inicios de sesión tienen las siguientes desventajas:</span><span class="sxs-lookup"><span data-stu-id="e0cca-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="e0cca-172">En iOS, el usuario pasa por un proceso externo a la experiencia de la aplicación mientras se eligen las credenciales.</span><span class="sxs-lookup"><span data-stu-id="e0cca-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="e0cca-173">Se pierde la capacidad de administrar la experiencia de inicio de sesión para los clientes dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="e0cca-174">A continuación se representa el funcionamiento de los SDK de Microsoft Identity con las aplicaciones de agente para habilitar el inicio de sesión único:</span><span class="sxs-lookup"><span data-stu-id="e0cca-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+
```

<span data-ttu-id="e0cca-175">Una vez que disponga de toda esta información, probablemente pueda entender e implementar mejor el inicio de sesión único en la aplicación mediante los SDK y la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="e0cca-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="e0cca-176">Habilitación del SSO entre aplicaciones mediante ADAL</span><span class="sxs-lookup"><span data-stu-id="e0cca-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="e0cca-177">Ahora vamos a usar el SDK de iOS de ADAL para:</span><span class="sxs-lookup"><span data-stu-id="e0cca-177">Here we use the ADAL iOS SDK to:</span></span>

* <span data-ttu-id="e0cca-178">Activar el SSO no asistido por agente para su conjunto de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e0cca-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="e0cca-179">Activar la compatibilidad para el SSO asistido por agente</span><span class="sxs-lookup"><span data-stu-id="e0cca-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="e0cca-180">Activación del SSO para el SSO no asistido por agente</span><span class="sxs-lookup"><span data-stu-id="e0cca-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="e0cca-181">En el caso del SSO entre aplicaciones no asistido por agente, los SDK de Microsoft Identity administran automáticamente gran parte de la complejidad que entraña este proceso.</span><span class="sxs-lookup"><span data-stu-id="e0cca-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="e0cca-182">Esto incluye la búsqueda del usuario adecuado en la memoria caché y el mantenimiento de una lista de usuarios que han iniciado sesión en la que se pueden realizar consultas.</span><span class="sxs-lookup"><span data-stu-id="e0cca-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="e0cca-183">Para habilitar el SSO entre aplicaciones de las que es el propietario debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e0cca-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="e0cca-184">Garantizar que todas las aplicaciones utilizan el mismo identificador de cliente o aplicación</span><span class="sxs-lookup"><span data-stu-id="e0cca-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="e0cca-185">Garantizar que todas las aplicaciones comparten el mismo certificado de firma de Apple para que sea posible compartir los llaveros.</span><span class="sxs-lookup"><span data-stu-id="e0cca-185">Ensure that all of your applications share the same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="e0cca-186">Solicitar los mismos permisos de llaveros para cada una de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e0cca-186">Request the same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="e0cca-187">Indicar a los SDK de Microsoft Identity cuál es el llavero compartido que quiere que utilicemos.</span><span class="sxs-lookup"><span data-stu-id="e0cca-187">Tell the Microsoft Identity SDKs about the shared keychain you want us to use.</span></span>

#### <a name="using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="e0cca-188">Uso del mismo identificador de cliente o aplicación para todas las aplicaciones de su conjunto</span><span class="sxs-lookup"><span data-stu-id="e0cca-188">Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="e0cca-189">A fin de que la plataforma Microsoft Identity sepa que puede compartir tokens entre las aplicaciones, es necesario que todas ellas tengan el mismo identificador de cliente o aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-189">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="e0cca-190">Se trata del identificador único que se le suministró al registrar su primera aplicación en el portal.</span><span class="sxs-lookup"><span data-stu-id="e0cca-190">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="e0cca-191">Quizás se pregunte cómo se puede identificar a las diferentes aplicaciones en el servicio Microsoft Identity si todas utilizan el mismo identificador.</span><span class="sxs-lookup"><span data-stu-id="e0cca-191">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="e0cca-192">Pues bien, esto es posible gracias a los **URI de redirección**.</span><span class="sxs-lookup"><span data-stu-id="e0cca-192">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="e0cca-193">Cada aplicación puede tener varios URI de redirección registrados en el portal de incorporación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-193">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="e0cca-194">Cada una de las aplicaciones de su conjunto tendrá diferentes URI de redirección.</span><span class="sxs-lookup"><span data-stu-id="e0cca-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="e0cca-195">A continuación se muestra un ejemplo típico de su aspecto:</span><span class="sxs-lookup"><span data-stu-id="e0cca-195">An example of how this looks is below:</span></span>

<span data-ttu-id="e0cca-196">URI de redirección de la aplicación 1: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="e0cca-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="e0cca-197">URI de redirección de la aplicación 2: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="e0cca-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="e0cca-198">URI de redirección de la aplicación 3: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="e0cca-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="e0cca-199">....</span><span class="sxs-lookup"><span data-stu-id="e0cca-199">....</span></span>

<span data-ttu-id="e0cca-200">Estos están anidados en el mismo identificador de cliente o aplicación y se consultan en función del URI de redirección que nos devuelve en su configuración del SDK.</span><span class="sxs-lookup"><span data-stu-id="e0cca-200">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="e0cca-201">*Tenga en cuenta que el formato de estos URI de redirección se explica a continuación. Puede usar cualquier URI de redirección, a menos que desee utilizar el agente, en cuyo caso debe tener un aspecto como el anterior*</span><span class="sxs-lookup"><span data-stu-id="e0cca-201">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="e0cca-202">Permitir el uso compartido de llaveros entre aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e0cca-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="e0cca-203">La habilitación del uso compartido de llaveros está fuera del ámbito de este documento; sin embargo, Apple lo trata en su documento [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html)(Incorporación de funcionalidades).</span><span class="sxs-lookup"><span data-stu-id="e0cca-203">Enabling keychain sharing is beyond the scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="e0cca-204">Lo importante es que decida cómo desea llamar a su llavero y agregar esa funcionalidad en todas sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e0cca-204">What is important is that you decide what you want your keychain to be called and add that capability across all your applications.</span></span>

<span data-ttu-id="e0cca-205">Cuando haya configurado los derechos correctamente, verá un archivo en el directorio del proyecto llamado `entitlements.plist` , que contiene algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e0cca-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like the following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="e0cca-206">Una vez que haya habilitado los derechos del llavero en cada una de las aplicaciones y esté listo para usar el SSO, informe al SDK de Microsoft Identity acerca del llavero usando el siguiente valor en `ADAuthenticationSettings` :</span><span class="sxs-lookup"><span data-stu-id="e0cca-206">Once you have the keychain entitlement enabled in each of your applications, and you are ready to use SSO, tell the Microsoft Identity SDK about your keychain by using the following setting in your `ADAuthenticationSettings` with the following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="e0cca-207">Cuando se comparte un llavero entre aplicaciones, cualquiera de ellas puede eliminar usuarios o, peor aún, eliminar todos los tokens de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-207">When you share a keychain across your applications any application can delete users or worse delete all the tokens across your application.</span></span> <span data-ttu-id="e0cca-208">Esto puede resultar especialmente problemático si tiene aplicaciones que dependen de los tokens para hacer el trabajo en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="e0cca-208">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="e0cca-209">Compartir un llavero implica ser muy cuidadoso en todas y cada una de las operaciones de eliminación realizadas a través de los SDK de Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="e0cca-209">Sharing a keychain means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="e0cca-210">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="e0cca-210">That's it!</span></span> <span data-ttu-id="e0cca-211">El SDK de Microsoft Identity ahora compartirá las credenciales entre todas sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e0cca-211">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="e0cca-212">La lista de usuarios también se compartirá entre las instancias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-212">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="e0cca-213">Activación del SSO para el SSO asistido por agente</span><span class="sxs-lookup"><span data-stu-id="e0cca-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="e0cca-214">La capacidad de una aplicación de usar cualquier agente que esté instalado en el dispositivo está **desactivada de forma predeterminada**.</span><span class="sxs-lookup"><span data-stu-id="e0cca-214">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="e0cca-215">Para poder utilizar la aplicación con el agente debe realizar algunos pasos de configuración adicionales y agregar código a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-215">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="e0cca-216">Los pasos que debe seguir son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0cca-216">The steps to follow are:</span></span>

1. <span data-ttu-id="e0cca-217">Habilitar el modo de agente en la llamada al código de la aplicación para el SDK de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0cca-217">Enable broker mode in your application code's call to the MS SDK.</span></span>
2. <span data-ttu-id="e0cca-218">Establecer un nuevo URI de redirección e indicarlo tanto en la aplicación como en el registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-218">Establish a new redirect URI and provide that to both the app and your app registration.</span></span>
3. <span data-ttu-id="e0cca-219">Registrar un esquema de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="e0cca-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="e0cca-220">Compatibilidad con iOS 9: agregar un permiso al archivo info.plist.</span><span class="sxs-lookup"><span data-stu-id="e0cca-220">iOS9 Support: Add a permission to your info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="e0cca-221">Paso 1: Habilitar el modo de agente en la aplicación</span><span class="sxs-lookup"><span data-stu-id="e0cca-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="e0cca-222">La capacidad de la aplicación de utilizar el agente se activa al crear el "contexto" o la configuración inicial del objeto de autenticación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-222">The ability for your application to use the broker is turned on when you create the "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="e0cca-223">Para ello, configure el tipo de credenciales en el código:</span><span class="sxs-lookup"><span data-stu-id="e0cca-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See the ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="e0cca-224">El valor `AD_CREDENTIALS_AUTO` permitirá al SDK de Microsoft Identity llamar al agente, `AD_CREDENTIALS_EMBEDDED` impedirá que el SDK de Microsoft Identity llame al agente.</span><span class="sxs-lookup"><span data-stu-id="e0cca-224">The `AD_CREDENTIALS_AUTO` setting will allow the Microsoft Identity SDK to try to call out to the broker, `AD_CREDENTIALS_EMBEDDED` will prevent the Microsoft Identity SDK from calling to the broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="e0cca-225">Paso 2: Registrar un esquema de dirección URL</span><span class="sxs-lookup"><span data-stu-id="e0cca-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="e0cca-226">La plataforma Microsoft Identity utiliza direcciones URL para invocar al agente y, a continuación, devolver el control a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-226">The Microsoft Identity platform uses URLs to invoke the broker and then return control back to your application.</span></span> <span data-ttu-id="e0cca-227">Para terminar este viaje de ida y vuelta se requiere un esquema de dirección URL registrado para la aplicación del que tenga conocimiento la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="e0cca-227">To finish that round trip you need a URL scheme registered for your application that the Microsoft Identity platform will know about.</span></span> <span data-ttu-id="e0cca-228">Esto puede sumarse a otros esquemas de aplicación que haya registrado previamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-228">This can be in addition to any other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="e0cca-229">Se recomienda dotar al esquema de dirección URL de unas características bastante únicas para minimizar las posibilidades de que otra aplicación use el mismo esquema de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="e0cca-229">We recommend making the URL scheme fairly unique to minimize the chances of another app using the same URL scheme.</span></span> <span data-ttu-id="e0cca-230">Apple no exige que los esquemas de dirección URL registrados en el almacén de aplicaciones sean únicos.</span><span class="sxs-lookup"><span data-stu-id="e0cca-230">Apple does not enforce the uniqueness of URL schemes that are registered in the app store.</span></span>
> 
> 

<span data-ttu-id="e0cca-231">A continuación, se muestra un ejemplo del aspecto que podría tener esto en la configuración de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="e0cca-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="e0cca-232">También es posible hacerlo en XCode del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e0cca-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="e0cca-233">Paso 3: Establecer un nuevo URI de redirección con el esquema de dirección URL</span><span class="sxs-lookup"><span data-stu-id="e0cca-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="e0cca-234">Para garantizar que siempre se devuelvan los tokens de credencial a la aplicación correcta, es necesario asegurarse de que se llama a la aplicación de tal manera que el sistema operativo iOS pueda verificarla.</span><span class="sxs-lookup"><span data-stu-id="e0cca-234">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the iOS operating system can verify.</span></span> <span data-ttu-id="e0cca-235">El sistema operativo iOS informa a las aplicaciones de agente de Microsoft sobre el identificador de agrupación que lo llama.</span><span class="sxs-lookup"><span data-stu-id="e0cca-235">The iOS operating system reports to the Microsoft broker applications the Bundle ID of the application calling it.</span></span> <span data-ttu-id="e0cca-236">Este sistema no se puede suplantar por ninguna aplicación malintencionada.</span><span class="sxs-lookup"><span data-stu-id="e0cca-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="e0cca-237">Por lo tanto, se aprovecha este elemento junto con el URI de la aplicación de agente para garantizar que los tokens se devuelven a la aplicación correcta.</span><span class="sxs-lookup"><span data-stu-id="e0cca-237">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="e0cca-238">Es necesario establecer este URI de redirección único en la aplicación y configurarlo como URI de redirección en nuestro portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="e0cca-238">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="e0cca-239">Para ser correcto, el URI de redirección debe presentar el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="e0cca-239">Your redirect URI must be in the proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="e0cca-240">Por ejemplo, *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="e0cca-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="e0cca-241">Este URI de redirección debe especificarse en el registro de la aplicación mediante [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e0cca-241">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="e0cca-242">Para más información sobre el registro de aplicaciones de Azure AD, consulte [Integración con Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="e0cca-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-to-support-certificate-based-authentication"></a><span data-ttu-id="e0cca-243">Paso 3a: Agregar un URI de redirección a la aplicación y al portal de desarrolladores para admitir la autenticación basada en certificados</span><span class="sxs-lookup"><span data-stu-id="e0cca-243">Step 3a: Add a redirect URI in your app and dev portal to support certificate based authentication</span></span>
<span data-ttu-id="e0cca-244">Para admitir la autenticación basada en certificados, se requiere el registro de un segundo elemento "msauth"en la aplicación y en [Azure Portal](https://portal.azure.com/) para controlar la autenticación de certificados si desea agregar esa compatibilidad a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-244">To support cert based authentication a second "msauth"  needs to be registered in your application and the [Azure portal](https://portal.azure.com/) to handle certificate authentication if you wish to add that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="e0cca-245">Por ejemplo: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="e0cca-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-to-your-app"></a><span data-ttu-id="e0cca-246">Paso 4: iOS 9: Agregar un parámetro de configuración a la aplicación</span><span class="sxs-lookup"><span data-stu-id="e0cca-246">Step 4: iOS9: Add a configuration parameter to your app</span></span>
<span data-ttu-id="e0cca-247">ADAL usa – canOpenURL: para comprobar si el agente está instalado en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e0cca-247">ADAL uses –canOpenURL: to check if the broker is installed on the device.</span></span> <span data-ttu-id="e0cca-248">En iOS 9, Apple ha bloqueado los esquemas que puede consultar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0cca-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="e0cca-249">Debe agregar "msauth" a la sección LSApplicationQueriesSchemes de `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="e0cca-249">You will need to add “msauth” to the LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="e0cca-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="e0cca-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="e0cca-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="e0cca-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="e0cca-252">Ya ha configurado el SSO.</span><span class="sxs-lookup"><span data-stu-id="e0cca-252">You've configured SSO!</span></span>
<span data-ttu-id="e0cca-253">Ahora, el SDK de Microsoft Identity compartirá automáticamente las credenciales entre las aplicaciones e invocará al agente si está presente en su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e0cca-253">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

