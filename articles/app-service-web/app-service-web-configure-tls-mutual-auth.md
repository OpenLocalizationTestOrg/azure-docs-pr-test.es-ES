---
title: "Configuración de la autenticación mutua de TLS para una aplicación web"
description: "Aprenda a configurar la aplicación web para que use la autenticación de certificado de cliente en TLS."
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: db69852cffd1ff331ac4a640b04ea4360d00bf75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-tls-mutual-authentication-for-web-app"></a><span data-ttu-id="2d71b-103">Configuración de la autenticación mutua de TLS para una aplicación web</span><span class="sxs-lookup"><span data-stu-id="2d71b-103">How To Configure TLS Mutual Authentication for Web App</span></span>
## <a name="overview"></a><span data-ttu-id="2d71b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="2d71b-104">Overview</span></span>
<span data-ttu-id="2d71b-105">Puede restringir el acceso a la aplicación web de Azure habilitando para este diferentes tipos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="2d71b-105">You can restrict access to your Azure web app by enabling different types of authentication for it.</span></span> <span data-ttu-id="2d71b-106">Una manera de hacerlo es autenticar con un certificado de cliente cuando la solicitud sea a través de TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="2d71b-106">One way to do so is to authenticate using a client certificate when the request is over TLS/SSL.</span></span> <span data-ttu-id="2d71b-107">Este mecanismo se denomina autenticación mutua de TLS o autenticación de certificado de cliente, y en este artículo se detalla cómo configurar la aplicación web para que use la autenticación de certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="2d71b-107">This mechanism is called TLS mutual authentication or client certificate authentication and this article will detail how to setup your web app to use client certificate authentication.</span></span>

> <span data-ttu-id="2d71b-108">**Nota:** Si accede a su sitio a través de HTTP y no de HTTPS, no recibirá ningún certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="2d71b-108">**Note:** If you access your site over HTTP and not HTTPS, you will not receive any client certificate.</span></span> <span data-ttu-id="2d71b-109">Por lo tanto, si la aplicación requiere certificados de cliente, no debe permitir las solicitudes a la aplicación mediante HTTP.</span><span class="sxs-lookup"><span data-stu-id="2d71b-109">So if your application requires client certificates you should not allow requests to your application over HTTP.</span></span>
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a><span data-ttu-id="2d71b-110">Configuración de la aplicación web para la autenticación de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="2d71b-110">Configure Web App for Client Certificate Authentication</span></span>
<span data-ttu-id="2d71b-111">Para configurar la aplicación web para que exija certificados de cliente, debe agregar la configuración del sitio clientCertEnabled para la aplicación web y establecerla como verdadera.</span><span class="sxs-lookup"><span data-stu-id="2d71b-111">To setup your web app to require client certificates you need to add the clientCertEnabled site setting for your web app and set it to true.</span></span> <span data-ttu-id="2d71b-112">Esta configuración no está actualmente disponible a través de la experiencia de administración en el portal, y a tal efecto deberá usarse la API de REST.</span><span class="sxs-lookup"><span data-stu-id="2d71b-112">This setting is not currently available through the management experience in the Portal, and the REST API will need to be used to accomplish this.</span></span>

<span data-ttu-id="2d71b-113">Puede usar la [herramienta ARMClient](https://github.com/projectkudu/ARMClient) para simplificar la creación de la llamada a la API de REST.</span><span class="sxs-lookup"><span data-stu-id="2d71b-113">You can use the [ARMClient tool](https://github.com/projectkudu/ARMClient) to make it easy to craft the REST API call.</span></span> <span data-ttu-id="2d71b-114">Después de iniciar sesión con la herramienta, deberá emitir el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2d71b-114">After you log in with the tool you will need to issue the following command:</span></span>

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

<span data-ttu-id="2d71b-115">y reemplazar todo lo que aparezca entre {} por la información de la aplicación web, y crear un archivo llamado enableclientcert.json con el siguiente contenido JSON:</span><span class="sxs-lookup"><span data-stu-id="2d71b-115">replacing everything in {} with information for your web app and creating a file called enableclientcert.json with the following JSON content:</span></span>

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

<span data-ttu-id="2d71b-116">Asegúrese de cambiar el valor de "location" por aquel en el que se encuentra su aplicación web, por ejemplo, Centro y norte de EE. UU. o Oeste de EE. UU., etc.</span><span class="sxs-lookup"><span data-stu-id="2d71b-116">Make sure to change the value of "location" to wherever your web app is located e.g. North Central US or West US etc.</span></span>

<span data-ttu-id="2d71b-117">También puede utilizar https://resources.azure.com para voltear la propiedad `clientCertEnabled` a `true`.</span><span class="sxs-lookup"><span data-stu-id="2d71b-117">You can also use https://resources.azure.com to flip the `clientCertEnabled` property to `true`.</span></span>

> <span data-ttu-id="2d71b-118">**Nota**: Si ejecuta ARMClient desde PowerShell, debe usar la secuencia de escape del símbolo @ del archivo JSON con una tilde aguda \`.</span><span class="sxs-lookup"><span data-stu-id="2d71b-118">**Note:** If you run ARMClient from Powershell, you will need to escape the @ symbol for the JSON file with a back tick \`.</span></span>
> 
> 

## <a name="accessing-the-client-certificate-from-your-web-app"></a><span data-ttu-id="2d71b-119">Acceso al certificado de cliente desde la aplicación web</span><span class="sxs-lookup"><span data-stu-id="2d71b-119">Accessing the Client Certificate From Your Web App</span></span>
<span data-ttu-id="2d71b-120">Si está usando ASP.NET y configura la aplicación para usar la autenticación de certificado de cliente, el certificado estará disponible a través de la propiedad **HttpRequest.ClientCertificate** .</span><span class="sxs-lookup"><span data-stu-id="2d71b-120">If you are using ASP.NET and configure your app to use client certificate authentication, the certificate will be available through the **HttpRequest.ClientCertificate** property.</span></span> <span data-ttu-id="2d71b-121">Para otras pilas de aplicación, el certificado de cliente estará disponible en la aplicación mediante un valor codificado en base64 en el encabezado de solicitud "X-ARR-ClientCert".</span><span class="sxs-lookup"><span data-stu-id="2d71b-121">For other application stacks, the client cert will be available in your app through a base64 encoded value in the "X-ARR-ClientCert" request header.</span></span> <span data-ttu-id="2d71b-122">La aplicación puede crear un certificado a partir de este valor y luego usarlo con fines de autenticación y autorización en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2d71b-122">Your application can create a certificate from this value and then use it for authentication and authorization purposes in your application.</span></span>

## <a name="special-considerations-for-certificate-validation"></a><span data-ttu-id="2d71b-123">Consideraciones especiales sobre la validación de certificados</span><span class="sxs-lookup"><span data-stu-id="2d71b-123">Special Considerations for Certificate Validation</span></span>
<span data-ttu-id="2d71b-124">El certificado de cliente que se envía a la aplicación no pasa ninguna validación de la plataforma de aplicaciones web de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d71b-124">The client certificate that is sent to the application does not go through any validation by the Azure Web Apps platform.</span></span> <span data-ttu-id="2d71b-125">La validación de este certificado es la responsabilidad de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2d71b-125">Validating this certificate is the responsibility of the web app.</span></span> <span data-ttu-id="2d71b-126">Este es el código de ASP.NET de ejemplo que valida las propiedades del certificado para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="2d71b-126">Here is sample ASP.NET code that validates certificate properties for authentication purposes.</span></span>

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read the certificate from the header into an X509Certificate2 object
            // Display properties of the certificate on the page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept the certificate as a valid certificate if all the conditions below are met:
                // 1. The certificate is not expired and is active for the current time on server.
                // 2. The subject name of the certificate has the common name nildevecc
                // 3. The issuer name of the certificate has the common name nildevecc and organization name Microsoft Corp
                // 4. The thumbprint of the certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained to a Trusted Root Authority (or revoked) on the server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want to test if the certificate chains to a Trusted Root Authority you can uncomment the code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }
