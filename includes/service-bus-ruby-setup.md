## <a name="create-a-ruby-application"></a><span data-ttu-id="0f4cd-101">Creación de una aplicación de Ruby</span><span class="sxs-lookup"><span data-stu-id="0f4cd-101">Create a Ruby application</span></span>
<span data-ttu-id="0f4cd-102">Para obtener instrucciones, vea cómo [crear una aplicación de Ruby en Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="0f4cd-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="0f4cd-103">Configurar el Bus de servicio de aplicación tooUse</span><span class="sxs-lookup"><span data-stu-id="0f4cd-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="0f4cd-104">toouse Bus de servicio, descargar y usar el paquete de Azure Ruby hello, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f4cd-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="0f4cd-105">Use el paquete de RubyGems tooobtain Hola</span><span class="sxs-lookup"><span data-stu-id="0f4cd-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="0f4cd-106">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="0f4cd-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="0f4cd-107">Escriba "indicador instalar azure" en el indicador de hello comando ventana tooinstall hello y dependencias.</span><span class="sxs-lookup"><span data-stu-id="0f4cd-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="0f4cd-108">Importar paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="0f4cd-108">Import hello package</span></span>
<span data-ttu-id="0f4cd-109">Con su editor de texto que prefiera, agregar Hola después de la parte superior de toohello de hello Ruby en el que piensa toouse almacenamiento de archivo:</span><span class="sxs-lookup"><span data-stu-id="0f4cd-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="0f4cd-110">Configuración de una conexión del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="0f4cd-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="0f4cd-111">Valores de hello tooset del espacio de nombres, nombre del programa Hola a de código siguiente Hola de uso clave, clave, firmante y host:</span><span class="sxs-lookup"><span data-stu-id="0f4cd-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="0f4cd-112">Conjunto Hola espacio de nombres toohello valor creado en lugar de la dirección URL completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f4cd-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="0f4cd-113">Por ejemplo, utilice **"suespaciodenombresdeejemplo"**, no "suespaciodenombresdeejemplo.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="0f4cd-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
