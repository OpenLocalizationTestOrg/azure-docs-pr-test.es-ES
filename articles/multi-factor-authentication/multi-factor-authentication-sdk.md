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
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>Creación de Multi-Factor Authentication en aplicaciones personalizadas (SDK)

Hola permite del Kit de desarrollo de Software (SDK) de Azure Multi-factor Authentication de Hello en que crear verificacion directamente inicio de sesión o procesa transacciones de aplicaciones en su inquilino de Azure AD.

Hola SDK de autenticación multifactor está disponible para C#, Visual Basic (. NET), Java, Perl, PHP y Ruby. Hola SDK proporciona un contenedor fino alrededor de verificación en dos pasos. Todo lo que necesita toowrite el código, incluidos los archivos de código fuente comentado, archivos de ejemplo y un archivo Léame detallado incluye. Cada SDK también incluye un certificado y clave privada para cifrar las transacciones que están tooyour único proveedor de autenticación multifactor. Siempre y cuando tenga un proveedor, puede descargar Hola SDK en tantos idiomas y formatos como necesite.

estructura de Hola de hello API Hola SDK de autenticación multifactor es simple. Realizar una sola función llamada API tooan con parámetros de opción de multifactor hello (por ejemplo, el modo de comprobación) y los datos de usuario (por ejemplo, toocall de número de teléfono de Hola u Hola PIN número toovalidate). Hello API convierten llamada de función de hello en toohello de las solicitudes de servicios web servicio basado en la nube de Azure Multi-factor Authentication. Todas las llamadas deben incluir un certificado privado de toohello de referencia que se incluye en todos los SDK.

Porque Hola API no tienen toousers acceso registrado en Azure Active Directory, debe proporcionar información de usuario en un archivo o una base de datos. Además, Hola API no proporcionan características de administración de inscripción o el usuario, por lo que necesita toobuild estos procesos en la aplicación.

> [!IMPORTANT]
> toodownload Hola SDK, deberá toocreate un proveedor de autenticación multifactor de Azure incluso si tienen licencias de Azure MFA, AAD Premium o EMS. Si crea un proveedor de autenticación multifactor de Azure para este propósito y ya tiene licencias, asegúrese de hello seguro toocreate proveedor con hello **por usuario habilitado** modelo. A continuación, vincular directorio Hola de toohello del proveedor que contiene las licencias de MFA de Azure, Azure AD Premium o EMS de Hola. Esta configuración garantiza que solo se le facturará si tiene más usuarios únicos mediante Hola SDK que número Hola de licencias que posee.


## <a name="download-hello-sdk"></a>Descargar Hola SDK
Descargar hello Azure multifactor SDK requiere una [proveedor de autenticación multifactor de Azure](multi-factor-authentication-get-started-auth-provider.md).  Para ello, se necesita una suscripción de Azure completa, aunque se cuenten con licencias de Azure MFA, Azure AD Premium o Enterprise Mobility Suite.  Hola toodownload SDK, navegue toohello Portal de administración de varios factores. Se pueden obtener acceso Hola portal mediante la administración del proveedor de autenticación multifactor directamente hello, o haciendo clic en hello **"Go toohello portal"** vínculo en la página de configuración de servicio de hello MFA.

### <a name="download-from-hello-azure-classic-portal"></a>Descargar desde Hola portal de Azure clásico
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) como administrador.
2. Hola izquierda, seleccione **Active Directory**.
3. En página de Active Directory de hello, en, seleccione superior hello **proveedores de autenticación multifactor**
4. En la parte inferior de hello seleccione **administrar**. Se abrirá una nueva página.
5. En hello izquierdo, en la parte inferior de hello, haga clic en **SDK**.
   <center>![Descargar](./media/multi-factor-authentication-sdk/download.png)</center>
6. Seleccione Hola idioma que desee y haga clic en vínculos de descarga correspondientes Hola uno.
7. Guardar archivo descargado Hola.

### <a name="download-from-hello-service-settings"></a>Descargar de la configuración del servicio Hola
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) como administrador.
2. Hola izquierda, seleccione **Active Directory**.
3. Haga doble clic en la instancia de Azure AD.
4. Haga clic en superior de hello **configurar**
5. En Multi-Factor Authentication, seleccione **Administrar configuración del servicio**
   ![Descargar](./media/multi-factor-authentication-sdk/download2.png)
6. En la página de configuración de servicios de hello, en la parte inferior de Hola de pantalla de bienvenida, haga clic en **Go toohello portal**. Se abrirá una nueva página.
   ![Descargar](./media/multi-factor-authentication-sdk/download3a.png)
7. En hello izquierdo, en la parte inferior de hello, haga clic en **SDK**.
8. Seleccione Hola idioma que desee y haga clic en vínculos de descarga correspondientes Hola uno.
9. Guardar archivo descargado Hola.

## <a name="whats-in-hello-sdk"></a>¿Qué es Hola SDK
Hola SDK incluye Hola siguientes elementos:

* **LÉAME**. Explica cómo toouse Hola a las API de autenticación multifactor en una aplicación nueva o existente.
* **Archivos de origen** para Multi-Factor Authentication
* **Certificado de cliente** que usar toocommunicate con hello servicio de la autenticación multifactor
* **Clave privada** certificado Hola
* **Resultados de la llamada.** Una lista de códigos de resultado de la llamada. tooopen este archivo, utilice una aplicación con formato de texto, como WordPad. Hola uso llamar tootest de códigos de resultado y solucionar problemas de implementación de saludo de la autenticación multifactor en su aplicación. No son códigos de estado de autenticación.
* **Ejemplos.** Código de ejemplo para una implementación básica de funcionamiento de Multi-Factor Authentication.

> [!WARNING]
> certificado de cliente de Hello es un certificado privado único que se generó especialmente para usted. No comparta ni pierda este archivo. Es la seguridad de hello tooensuring clave de las comunicaciones con el servicio de la autenticación multifactor de Hola.

## <a name="code-sample"></a>Código de ejemplo
Este ejemplo de código muestra cómo llamar toouse Hola API Hola voz de modo estándar de SDK de Azure Multi-factor Authentication tooadd a la aplicación de tooyour de comprobación. Modo estándar es una llamada de teléfono que Hola tooby de usuario responde presionando la tecla # de Hola.

Este ejemplo utiliza Hola C# .NET 2.0 SDK Multi-factor Authentication en una aplicación ASP.NET básica con lógica de servidor de C#, pero el proceso de hello es similar en otros lenguajes. Hola SDK incluye los archivos de origen, no archivos ejecutables, puede generar archivos de Hola y hace referencia a ellas o incluirlos directamente en la aplicación.

> [!NOTE]
> Al implementar la autenticación multifactor, use métodos adicionales de hello (llamada de teléfono o mensaje de texto) como comprobación secundaria o terciaria toosupplement su método de autenticación principal (nombre de usuario y contraseña). Estos métodos no están diseñados como métodos de autenticación principal.

### <a name="code-sample-overview"></a>Información general del ejemplo de código
Este código de ejemplo para una aplicación web simple demostración usa una llamada telefónica con un # respuesta clave tooverify Hola autenticación del usuario. Este factor de llamada de teléfono se conoce en la Multi-Factor Authentication como modo estándar.

código del lado cliente Hello no incluye los elementos específicos de la autenticación multifactor. Dado que los factores de autenticación adicionales de hello son independientes de autenticación principal hello, puede agregarlos sin cambiar la interfaz de inicio de sesión existente de Hola. Hola API Hola SDK multifactor le permite personalizar la experiencia del usuario hello, pero puede que no tenga toochange nada en absoluto.

código del lado servidor Hello agrega la autenticación en modo estándar en el paso 2. Crea un objeto PfAuthParams con parámetros de Hola que son necesarios para la comprobación de modo estándar: nombre de usuario, número de teléfono y el modo y Hola certificado de cliente de toohello de ruta de acceso (CertFilePath), que es necesario en cada llamada. Para ver una demostración de todos los parámetros de PfAuthParams, consulte el archivo de ejemplo de Hola Hola SDK.

A continuación, el código de hello pasa toohello pf_authenticate() función de hello PfAuthParams objeto. valor devuelto de Hello indica Hola éxito o error de autenticación de Hola. Hola parámetros, callStatus y errorID, contienen información de resultado de llamada adicional. códigos de resultado de Hello llamada se documentan en el archivo de resultados de llamada de Hola Hola SDK.

Esta implementación mínima puede escribirse en unas pocas líneas. Sin embargo, en el código de producción, incluiría un tratamiento de errores más sofisticado, código de la base de datos adicional y una experiencia de usuario mejorada.

### <a name="web-client-code"></a>Código de cliente web
Hola aquí te mostramos código de cliente web de una página de demostración.

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


### <a name="server-side-code"></a>Código de servidor
Hola después el código del lado servidor, la autenticación multifactor está configurada y se ejecute en el paso 2. Modo estándar (MODE_STANDARD) es que un usuario de llamada de teléfono toowhich Hola responde presionando la tecla # de Hola.

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
