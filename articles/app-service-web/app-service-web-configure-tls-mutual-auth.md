---
title: "aaaHow tooConfigure TLS autenticación mutua para la aplicación Web"
description: "Obtenga información acerca de cómo tooconfigure el cliente de toouse la aplicación web de certificado de autenticación en TLS."
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
ms.openlocfilehash: 8aeb9b35058fac50b8b38f6428207ad4a82d8637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a>¿Cómo tooConfigure TLS autenticación mutua para la aplicación Web
## <a name="overview"></a>Información general
Puede restringir el acceso tooyour web de Azure aplicación habilitando diferentes tipos de autenticación para él. Por lo tanto, toodo unidireccional es tooauthenticate mediante un certificado de cliente cuando la solicitud de hello es a través de TLS/SSL. Este mecanismo se denomina autenticación mutua de TLS o la autenticación de certificado de cliente y este artículo se detalla cómo toosetup la autenticación de certificado de cliente de web app toouse.

> **Nota:** Si accede a su sitio a través de HTTP y no de HTTPS, no recibirá ningún certificado de cliente. Por lo que si la aplicación requiere certificados de cliente no debe permitir las solicitudes de aplicación de tooyour a través de HTTP.
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a>Configuración de la aplicación web para la autenticación de certificado de cliente
los certificados de cliente de toorequire de aplicación web que necesita tooadd Hola clientCertEnabled sitio configuración de la aplicación web y establecer tootrue de toosetup. Esta opción no está actualmente disponible a través de la experiencia de administración de hello en hello Portal y Hola API de REST necesitará toobe utiliza tooaccomplish.

Puede usar hello [ARMClient herramienta](https://github.com/projectkudu/ARMClient) toomake se toocraft fácil Hola llamada API de REST. Después de iniciar sesión con la herramienta de hello, necesitará hello tooissue siguiente comando:

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

Reemplazar todo el contenido de {} con información de la aplicación web y la creación de un archivo denominan enableclientcert.json con hello después JSON contenido:

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

Asegúrese de que toochange valor hello toowherever "location" es la aplicación web ubicados p. ej. Ee.uu. Central Norte u oeste de EE. UU. etcetera.

También puede usar https://resources.azure.com tooflip hello `clientCertEnabled` propiedad demasiado`true`.

> **Nota:** si ejecuta ARMClient desde Powershell, deberá tooescape Hola símbolo @ para un archivo JSON Hola con un acento invertido ".
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a>Hola al tener acceso al certificado desde el Web aplicación cliente
Si está utilizando ASP.NET y configurar la autenticación de certificado de cliente de aplicación toouse, certificado Hola estarán disponible a través de hello **HttpRequest.ClientCertificate** propiedad. Para otras pilas de la aplicación, certificado de cliente de hello estará disponible en la aplicación a través de un valor codificado en base64 en encabezado de solicitud de Hola "X-ARR-ClientCert". La aplicación puede crear un certificado a partir de este valor y luego usarlo con fines de autenticación y autorización en la aplicación.

## <a name="special-considerations-for-certificate-validation"></a>Consideraciones especiales sobre la validación de certificados
certificado de cliente de Hola se envía toohello aplicación no pasa por ninguna validación de la plataforma de aplicaciones Web de Azure Hola. Validar el certificado es responsabilidad de Hola de hello web app. Este es el código de ASP.NET de ejemplo que valida las propiedades del certificado para la autenticación.

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
            // Read hello certificate from hello header into an X509Certificate2 object
            // Display properties of hello certificate on hello page
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
                // In this example we will only accept hello certificate as a valid certificate if all hello conditions below are met:
                // 1. hello certificate is not expired and is active for hello current time on server.
                // 2. hello subject name of hello certificate has hello common name nildevecc
                // 3. hello issuer name of hello certificate has hello common name nildevecc and organization name Microsoft Corp
                // 4. hello thumbprint of hello certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained tooa Trusted Root Authority (or revoked) on hello server 
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

                // If you also want tootest if hello certificate chains tooa Trusted Root Authority you can uncomment hello code below
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
