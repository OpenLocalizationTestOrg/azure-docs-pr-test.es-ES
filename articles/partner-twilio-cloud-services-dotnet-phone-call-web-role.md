---
title: "aaaHow toomake una llamada de teléfono de Twilio (. NET) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomake una llamada de teléfono así como enviar un SMS de mensajes con el servicio de API de Twilio de hello en Azure. Los ejemplos de código están escritos en .NET."
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 857d89961c563a51fef944f4a72828036af79b43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a>Cómo toomake un teléfono llamar a con Twilio en un rol web en Azure
Esta guía demuestra cómo toouse Twilio toomake una llamada desde una página web hospedada en Azure. aplicación resultante de Hello solicita una llamada de hello usuario toomake con hello dado el número y el mensaje, tal y como se muestra en la siguiente captura de pantalla de Hola.

![Formulario de llamada de Azure con Twilio y ASP.NET][twilio_dotnet_basic_form]

## <a name="twilio-prereqs"></a>Requisitos previos
Se necesita toodo Hola siguiente código de hello toouse en este tema:

1. Adquirir una cuenta de Twilio y la autenticación de token de hello [Twilio consola][twilio_console]. tooget en marcha con Twilio, inicio de sesión en [https://www.twilio.com/try-twilio][try_twilio]. Puede estudiar los precios en [http://www.twilio.com/pricing][twilio_pricing]. Para obtener información acerca de la API proporcionada por Twilio hello, consulte [http://www.twilio.com/voice/api][twilio_api].
2. Agregar hello *biblioteca .NET de Twilio* rol web de tooyour. Vea **proyecto de rol web de tooadd hello Twilio bibliotecas tooyour**, más adelante en este tema.

Debe saber cómo crear un [rol web básico en Azure][azure_webroles_get_started].

## <a name="howtocreateform"></a>Creación de un formulario web para hacer una llamada
<a id="use_nuget"></a>tooadd hello Twilio bibliotecas tooyour proyecto de rol web:

1. Abra su solución en Visual Studio.
2. Haga clic con el botón secundario en **Referencias**.
3. Haga clic en **Administración de paquetes de NuGet**.
4. Haga clic en **En línea**.
5. En el cuadro en línea de la búsqueda de hello, escriba *twilio*.
6. Haga clic en **instalar** en el paquete de Twilio Hola.

Hola siguiente código muestra cómo los datos de usuario de tooretrieve para realizar una llamada del formulario toocreate un sitio web. En este ejemplo, se crea un rol web de ASP.NET denominado **TwilioCloud**.

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <a id="howtocreatecode"></a>Cómo: crear Hola código toomake Hola llamada
Hola código siguiente, que se llama cuando el usuario de hello completa formulario hello, crea el mensaje de bienvenida de llamada y genera Hola llamada. En este ejemplo, se ejecuta código de hello Hola onclick controlador de eventos del botón de hello en forma de Hola. (Use la cuenta de Twilio y la autenticación de token en lugar de valores de marcador de posición de hello asignados demasiado`accountSID` y `authToken` en el siguiente código de hello.)

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // hello placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of hello Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve hello account, used later tooretrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve hello values entered by hello user.
                var too= PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using hello Twilio message and hello user-entered
                // text. You must replace spaces in hello user's text with '%20'
                // toomake hello text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display hello endpoint, API version, and hello URL for hello message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"hello URL is {url}");

                // Place hello call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

se realiza la llamada de Hola y el punto de conexión de hello Twilio, versión de API y estado de la llamada de Hola se muestran. Hola siguientes salida de muestra de captura de pantalla de un ejemplo de ejecución.

![Respuesta de llamada de Azure con Twilio y ASP.NET][twilio_dotnet_basic_form_output]

Encontrará más información sobre TwiML en [http://www.twilio.com/docs/api/twiml][twiml]. Encontrará más información sobre &lt;Say&gt; y otros verbos de Twilio en [http://www.twilio.com/docs/api/twiml/say][twilio_say].

## <a id="nextsteps"></a>Pasos siguientes
Este código se proporcionó tooshow funcionalidad básica con Twilio en un rol web ASP.NET en Azure. Antes de implementar tooAzure en producción, puede que desee tooadd más control de errores o con otras características. Por ejemplo:

* En lugar de utilizar un formulario web Forms, puede usar el almacenamiento de blobs de Azure o un números de teléfono de toostore de instancia de base de datos de SQL Azure y llamar a texto. Para obtener información acerca del uso de Blobs de Azure, consulte [cómo toouse Hola servicio de almacenamiento de blobs de Azure en .NET][howto_blob_storage_dotnet]. Para obtener información sobre el uso de la base de datos SQL, consulte [cómo toouse SQL Azure base de datos en aplicaciones .NET][howto_sql_azure_dotnet].
* Puede usar `RoleEnvironment.getConfigurationSettings` tooretrieve Hola Id. de cuenta de Twilio y la autenticación de token de opciones de configuración de su implementación, en lugar de valores de hello codificar de forma rígida en el formulario. Para obtener información acerca de hello `RoleEnvironment` de clases, consulte [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].
* Lea las directrices de seguridad de hello Twilio en [https://www.twilio.com/docs/security][twilio_docs_security].
* Obtenga más información sobre Twilio en [https://www.twilio.com/docs][twilio_docs].

## <a name="seealso"></a>Otras referencias
* [Cómo toouse Twilio para capacidades de voz y SMS de Azure](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
