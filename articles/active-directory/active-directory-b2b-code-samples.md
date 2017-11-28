---
title: "aaaAzure B2B de Active Directory código de colaboración y ejemplos de PowerShell | Documentos de Microsoft"
description: "Ejemplos de código y PowerShell para la colaboración B2B de Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 8e4f66fcb50d190899304831ea7ccd2203c5468c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-code-and-powershell-samples"></a><span data-ttu-id="17989-103">Ejemplos de código y PowerShell para la colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17989-103">Azure Active Directory B2B collaboration code and PowerShell samples</span></span>

## <a name="powershell-example"></a><span data-ttu-id="17989-104">Ejemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="17989-104">PowerShell example</span></span>
<span data-ttu-id="17989-105">Puede bulk-invitación organización de los usuarios externos tooan desde direcciones de correo electrónico que ha almacenado en una. Archivo CSV.</span><span class="sxs-lookup"><span data-stu-id="17989-105">You can bulk-invite external users tooan organization from email addresses that you have stored in a .CSV file.</span></span>

1. <span data-ttu-id="17989-106">Preparar Hola. CSV cree un nuevo archivo CSV de archivo y asígnele el nombre invitations.csv.</span><span class="sxs-lookup"><span data-stu-id="17989-106">Prepare hello .CSV file Create a new CSV file and name it invitations.csv.</span></span> <span data-ttu-id="17989-107">En este ejemplo, archivo hello se guarda en C:\data y contiene Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="17989-107">In this example, hello file is saved in C:\data, and contains hello following information:</span></span>
  
  <span data-ttu-id="17989-108">Nombre</span><span class="sxs-lookup"><span data-stu-id="17989-108">Name</span></span>                  |  <span data-ttu-id="17989-109">InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="17989-109">InvitedUserEmailAddress</span></span>
  --------------------- | --------------------------
  <span data-ttu-id="17989-110">Invitado de B2B de Gmail</span><span class="sxs-lookup"><span data-stu-id="17989-110">Gmail B2B Invitee</span></span>     | b2binvitee@gmail.com
  <span data-ttu-id="17989-111">Invitado de B2B de Outlook</span><span class="sxs-lookup"><span data-stu-id="17989-111">Outlook B2B invitee</span></span>   | b2binvitee@outlook.com


2. <span data-ttu-id="17989-112">Obtener toouse de PowerShell de Azure AD más reciente de Hola Hola nuevos cmdlets, debe instalar el módulo de PowerShell de Azure AD Hola actualizado, que puede descargar desde [Hola página de la versión del módulo de Powershell](https://www.powershellgallery.com/packages/AzureADPreview)</span><span class="sxs-lookup"><span data-stu-id="17989-112">Get hello latest Azure AD PowerShell toouse hello new cmdlets, you must install hello updated Azure AD PowerShell module, which you can download from [hello Powershell module's release page](https://www.powershellgallery.com/packages/AzureADPreview)</span></span>

3. <span data-ttu-id="17989-113">Inicie sesión en tooyour multiempresa</span><span class="sxs-lookup"><span data-stu-id="17989-113">Sign in tooyour tenancy</span></span>

    ```
    $cred = Get-Credential
    Connect-AzureAD -Credential $cred
    ```

4. <span data-ttu-id="17989-114">Ejecute el cmdlet de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="17989-114">Run hello PowerShell cmdlet</span></span>

  ```
  $invitations = import-csv C:\data\invitations.csv
  $messageInfo = New-Object Microsoft.Open.MSGraph.Model.InvitedUserMessageInfo
  $messageInfo.customizedMessageBody = “Hey there! Check this out. I created an invitation through PowerShell”
  foreach ($email in $invitations) {New-AzureADMSInvitation -InvitedUserEmailAddress $email.InvitedUserEmailAddress -InvitedUserDisplayName $email.Name -InviteRedirectUrl https://wingtiptoysonline-dev-ed.my.salesforce.com -InvitedUserMessageInfo $messageInfo -SendInvitationMessage $true}
  ```

<span data-ttu-id="17989-115">Este cmdlet envía una invitación toohello direcciones de correo electrónico en invitations.csv.</span><span class="sxs-lookup"><span data-stu-id="17989-115">This cmdlet sends an invitation toohello email addresses in invitations.csv.</span></span> <span data-ttu-id="17989-116">Algunas características adicionales de este cmdlet son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="17989-116">Additional features of this cmdlet include:</span></span>
- <span data-ttu-id="17989-117">Texto personalizado en el mensaje de correo electrónico de saludo</span><span class="sxs-lookup"><span data-stu-id="17989-117">Customized text in hello email message</span></span>
- <span data-ttu-id="17989-118">Incluya un nombre de presentación para hello invita usuario</span><span class="sxs-lookup"><span data-stu-id="17989-118">Including a display name for hello invited user</span></span>
- <span data-ttu-id="17989-119">Enviar mensajes tooCCs o suprimir los mensajes de correo electrónico por completo</span><span class="sxs-lookup"><span data-stu-id="17989-119">Sending messages tooCCs or suppressing email messages altogether</span></span>

## <a name="code-sample"></a><span data-ttu-id="17989-120">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="17989-120">Code sample</span></span>
<span data-ttu-id="17989-121">A continuación se ilustran cómo toocall Hola invitación API, en modo "solo de aplicación", URL de pago de hello tooget para toowhich de recursos de Hola que invita Hola usuario B2B.</span><span class="sxs-lookup"><span data-stu-id="17989-121">Here we illustrate how toocall hello invitation API, in "app-only" mode, tooget hello redemption URL for hello resource toowhich you are inviting hello B2B user.</span></span> <span data-ttu-id="17989-122">objetivo de Hello es toosend un correo electrónico de invitación personalizado.</span><span class="sxs-lookup"><span data-stu-id="17989-122">hello goal is toosend a custom invitation email.</span></span> <span data-ttu-id="17989-123">correo electrónico de Hello puede combinarse con un cliente HTTP, para que pueda personalizar su aspecto y enviarlo a través de la API Graph.</span><span class="sxs-lookup"><span data-stu-id="17989-123">hello email can be composed with an HTTP client, so you can customize how it looks and send it through Graph API.</span></span>

```
namespace SampleInviteApp
{
    using System;
    using System.Linq;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    class Program
    {
        /// <summary>
        /// Microsoft graph resource.
        /// </summary>
        static readonly string GraphResource = "https://graph.microsoft.com";
 
        /// <summary>
        /// Microsoft graph invite endpoint.
        /// </summary>
        static readonly string InviteEndPoint = "https://graph.microsoft.com/v1.0/invitations";
 
        /// <summary>
        ///  Authentication endpoint tooget token.
        /// </summary>
        static readonly string EstsLoginEndpoint = "https://login.microsoftonline.com";
 
        /// <summary>
        /// This is hello tenantid of hello tenant you want tooinvite users to.
        /// </summary>
        private static readonly string TenantID = "";
 
        /// <summary>
        /// This is hello application id of hello application that is registered in hello above tenant.
        /// hello required scopes are available in hello below link.
        /// https://developer.microsoft.com/graph/docs/api-reference/v1.0/api/invitation_post
        /// </summary>
        private static readonly string TestAppClientId = "";
 
        /// <summary>
        /// Client secret of hello application.
        /// </summary>
        private static readonly string TestAppClientSecret = @"
 
        /// <summary>
        /// This is hello email address of hello user you want tooinvite.
        /// </summary>
        private static readonly string InvitedUserEmailAddress = @"";
 
        /// <summary>
        /// This is hello display name of hello user you want tooinvite.
        /// </summary>
        private static readonly string InvitedUserDisplayName = @"";
 
        /// <summary>
        /// Main method.
        /// </summary>
        /// <param name="args">Optional arguments</param>
        static void Main(string[] args)
        {
            Invitation invitation = CreateInvitation();
            SendInvitation(invitation);
        }
 
        /// <summary>
        /// Create hello invitation object.
        /// </summary>
        /// <returns>Returns hello invitation object.</returns>
        private static Invitation CreateInvitation()
        {
            // Set hello invitation object.
            Invitation invitation = new Invitation();
            invitation.InvitedUserDisplayName = InvitedUserDisplayName;
            invitation.InvitedUserEmailAddress = InvitedUserEmailAddress;
            invitation.InviteRedirectUrl = "https://www.microsoft.com";
            invitation.SendInvitationMessage = true;
            return invitation;
        }
 
        /// <summary>
        /// Send hello guest user invite request.
        /// </summary>
        /// <param name="invitation">Invitation object.</param>
        private static void SendInvitation(Invitation invitation)
        {
            string accessToken = GetAccessToken();
 
            HttpClient httpClient = GetHttpClient(accessToken);
 
            // Make hello invite call. 
            HttpContent content = new StringContent(JsonConvert.SerializeObject(invitation));
            content.Headers.Add("ContentType", "application/json");
            var postResponse = httpClient.PostAsync(InviteEndPoint, content).Result;
            string serverResponse = postResponse.Content.ReadAsStringAsync().Result;
            Console.WriteLine(serverResponse);
        }
 
        /// <summary>
        /// Get hello HTTP client.
        /// </summary>
        /// <param name="accessToken">Access token</param>
        /// <returns>Returns hello Http Client.</returns>
        private static HttpClient GetHttpClient(string accessToken)
        {
            // setup http client.
            HttpClient httpClient = new HttpClient();
            httpClient.Timeout = TimeSpan.FromSeconds(300);
            httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
            httpClient.DefaultRequestHeaders.Add("client-request-id", Guid.NewGuid().ToString());
            Console.WriteLine(
                "CorrelationID for hello request: {0}",
                httpClient.DefaultRequestHeaders.GetValues("client-request-id").Single());
            return httpClient;
        }
 
        /// <summary>
        /// Get hello access token for our application tootalk toomicrosoft graph.
        /// </summary>
        /// <returns>Returns hello access token for our application tootalk toomicrosoft graph.</returns>
        private static string GetAccessToken()
        {
            string accessToken = null;
 
            // Get hello access token for our application tootalk toomicrosoft graph.
            try
            {
                AuthenticationContext testAuthContext =
                    new AuthenticationContext(string.Format("{0}/{1}", EstsLoginEndpoint, TenantID));
                AuthenticationResult testAuthResult = testAuthContext.AcquireTokenAsync(
                    GraphResource,
                    new ClientCredential(TestAppClientId, TestAppClientSecret)).Result;
                accessToken = testAuthResult.AccessToken;
            }
            catch (AdalException ex)
            {
                Console.WriteLine("An exception was thrown while fetching hello token: {0}.", ex);
                throw;
            }
 
            return accessToken;
        }
 
        /// <summary>
        /// Invitation class.
        /// </summary>
        public class Invitation
        {
            /// <summary>
            /// Gets or sets display name.
            /// </summary>
            public string InvitedUserDisplayName { get; set; }
 
            /// <summary>
            /// Gets or sets display name.
            /// </summary>
            public string InvitedUserEmailAddress { get; set; }
 
            /// <summary>
            /// Gets or sets a value indicating whether Invitation Manager should send hello email tooInvitedUser.
            /// </summary>
            public bool SendInvitationMessage { get; set; }
 
            /// <summary>
            /// Gets or sets invitation redirect URL
            /// </summary>
            public string InviteRedirectUrl { get; set; }
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="17989-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="17989-124">Next steps</span></span>

<span data-ttu-id="17989-125">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="17989-125">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="17989-126">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="17989-126">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="17989-127">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="17989-127">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="17989-128">Agregar un rol de tooa de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="17989-128">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="17989-129">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="17989-129">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="17989-130">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="17989-130">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="17989-131">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="17989-131">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="17989-132">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="17989-132">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="17989-133">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="17989-133">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="17989-134">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="17989-134">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="17989-135">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="17989-135">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
