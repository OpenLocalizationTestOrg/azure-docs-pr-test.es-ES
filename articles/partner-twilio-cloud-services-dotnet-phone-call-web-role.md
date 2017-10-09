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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="4a946-104">Cómo toomake un teléfono llamar a con Twilio en un rol web en Azure</span><span class="sxs-lookup"><span data-stu-id="4a946-104">How toomake a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="4a946-105">Esta guía demuestra cómo toouse Twilio toomake una llamada desde una página web hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="4a946-105">This guide demonstrates how toouse Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="4a946-106">aplicación resultante de Hello solicita una llamada de hello usuario toomake con hello dado el número y el mensaje, tal y como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a946-106">hello resulting application prompts hello user toomake a call with hello given number and message, as shown in hello following screenshot.</span></span>

![Formulario de llamada de Azure con Twilio y ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="4a946-108"><a name="twilio-prereqs"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4a946-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="4a946-109">Se necesita toodo Hola siguiente código de hello toouse en este tema:</span><span class="sxs-lookup"><span data-stu-id="4a946-109">You will need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="4a946-110">Adquirir una cuenta de Twilio y la autenticación de token de hello [Twilio consola][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="4a946-110">Acquire a Twilio account and authentication token from hello [Twilio Console][twilio_console].</span></span> <span data-ttu-id="4a946-111">tooget en marcha con Twilio, inicio de sesión en [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="4a946-111">tooget started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="4a946-112">Puede estudiar los precios en [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="4a946-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="4a946-113">Para obtener información acerca de la API proporcionada por Twilio hello, consulte [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="4a946-113">For information about hello API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="4a946-114">Agregar hello *biblioteca .NET de Twilio* rol web de tooyour.</span><span class="sxs-lookup"><span data-stu-id="4a946-114">Add hello *Twilio .NET libary* tooyour web role.</span></span> <span data-ttu-id="4a946-115">Vea **proyecto de rol web de tooadd hello Twilio bibliotecas tooyour**, más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="4a946-115">See **tooadd hello Twilio libraries tooyour web role project**, later in this topic.</span></span>

<span data-ttu-id="4a946-116">Debe saber cómo crear un [rol web básico en Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="4a946-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="4a946-117"><a name="howtocreateform"></a>Creación de un formulario web para hacer una llamada</span><span class="sxs-lookup"><span data-stu-id="4a946-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="4a946-118"><a id="use_nuget"></a>tooadd hello Twilio bibliotecas tooyour proyecto de rol web:</span><span class="sxs-lookup"><span data-stu-id="4a946-118"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour web role project:</span></span>

1. <span data-ttu-id="4a946-119">Abra su solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4a946-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="4a946-120">Haga clic con el botón secundario en **Referencias**.</span><span class="sxs-lookup"><span data-stu-id="4a946-120">Right-click **References**.</span></span>
3. <span data-ttu-id="4a946-121">Haga clic en **Administración de paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4a946-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="4a946-122">Haga clic en **En línea**.</span><span class="sxs-lookup"><span data-stu-id="4a946-122">Click **Online**.</span></span>
5. <span data-ttu-id="4a946-123">En el cuadro en línea de la búsqueda de hello, escriba *twilio*.</span><span class="sxs-lookup"><span data-stu-id="4a946-123">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="4a946-124">Haga clic en **instalar** en el paquete de Twilio Hola.</span><span class="sxs-lookup"><span data-stu-id="4a946-124">Click **Install** on hello Twilio package.</span></span>

<span data-ttu-id="4a946-125">Hola siguiente código muestra cómo los datos de usuario de tooretrieve para realizar una llamada del formulario toocreate un sitio web.</span><span class="sxs-lookup"><span data-stu-id="4a946-125">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="4a946-126">En este ejemplo, se crea un rol web de ASP.NET denominado **TwilioCloud**.</span><span class="sxs-lookup"><span data-stu-id="4a946-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

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

## <span data-ttu-id="4a946-127"><a id="howtocreatecode"></a>Cómo: crear Hola código toomake Hola llamada</span><span class="sxs-lookup"><span data-stu-id="4a946-127"><a id="howtocreatecode"></a>How to: Create hello code toomake hello call</span></span>
<span data-ttu-id="4a946-128">Hola código siguiente, que se llama cuando el usuario de hello completa formulario hello, crea el mensaje de bienvenida de llamada y genera Hola llamada.</span><span class="sxs-lookup"><span data-stu-id="4a946-128">hello following code, which is called when hello user completes hello form, creates hello call message and generates hello call.</span></span> <span data-ttu-id="4a946-129">En este ejemplo, se ejecuta código de hello Hola onclick controlador de eventos del botón de hello en forma de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a946-129">In this example, hello code is run in hello onclick event handler of hello button on hello form.</span></span> <span data-ttu-id="4a946-130">(Use la cuenta de Twilio y la autenticación de token en lugar de valores de marcador de posición de hello asignados demasiado`accountSID` y `authToken` en el siguiente código de hello.)</span><span class="sxs-lookup"><span data-stu-id="4a946-130">(Use your Twilio account and authentication token instead of hello placeholder values assigned too`accountSID` and `authToken` in hello code below.)</span></span>

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

<span data-ttu-id="4a946-131">se realiza la llamada de Hola y el punto de conexión de hello Twilio, versión de API y estado de la llamada de Hola se muestran.</span><span class="sxs-lookup"><span data-stu-id="4a946-131">hello call is made, and hello Twilio endpoint, API version, and hello call status are displayed.</span></span> <span data-ttu-id="4a946-132">Hola siguientes salida de muestra de captura de pantalla de un ejemplo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="4a946-132">hello following screenshot shows output from a sample run.</span></span>

![Respuesta de llamada de Azure con Twilio y ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="4a946-134">Encontrará más información sobre TwiML en [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="4a946-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="4a946-135">Encontrará más información sobre &lt;Say&gt; y otros verbos de Twilio en [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="4a946-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="4a946-136"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a946-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="4a946-137">Este código se proporcionó tooshow funcionalidad básica con Twilio en un rol web ASP.NET en Azure.</span><span class="sxs-lookup"><span data-stu-id="4a946-137">This code was provided tooshow you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="4a946-138">Antes de implementar tooAzure en producción, puede que desee tooadd más control de errores o con otras características.</span><span class="sxs-lookup"><span data-stu-id="4a946-138">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="4a946-139">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4a946-139">For example:</span></span>

* <span data-ttu-id="4a946-140">En lugar de utilizar un formulario web Forms, puede usar el almacenamiento de blobs de Azure o un números de teléfono de toostore de instancia de base de datos de SQL Azure y llamar a texto.</span><span class="sxs-lookup"><span data-stu-id="4a946-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance toostore phone numbers and call text.</span></span> <span data-ttu-id="4a946-141">Para obtener información acerca del uso de Blobs de Azure, consulte [cómo toouse Hola servicio de almacenamiento de blobs de Azure en .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="4a946-141">For information about using Blobs in Azure, see [How toouse hello Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="4a946-142">Para obtener información sobre el uso de la base de datos SQL, consulte [cómo toouse SQL Azure base de datos en aplicaciones .NET][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="4a946-142">For information about using SQL Database, see [How toouse Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="4a946-143">Puede usar `RoleEnvironment.getConfigurationSettings` tooretrieve Hola Id. de cuenta de Twilio y la autenticación de token de opciones de configuración de su implementación, en lugar de valores de hello codificar de forma rígida en el formulario.</span><span class="sxs-lookup"><span data-stu-id="4a946-143">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in your form.</span></span> <span data-ttu-id="4a946-144">Para obtener información acerca de hello `RoleEnvironment` de clases, consulte [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="4a946-144">For information about hello `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="4a946-145">Lea las directrices de seguridad de hello Twilio en [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="4a946-145">Read hello Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="4a946-146">Obtenga más información sobre Twilio en [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="4a946-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="4a946-147"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="4a946-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="4a946-148">Cómo toouse Twilio para capacidades de voz y SMS de Azure</span><span class="sxs-lookup"><span data-stu-id="4a946-148">How toouse Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

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
