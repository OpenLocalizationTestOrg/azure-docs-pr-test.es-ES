## <a name="create-a-ruby-application"></a><span data-ttu-id="562ad-101">Creación de una aplicación de Ruby</span><span class="sxs-lookup"><span data-stu-id="562ad-101">Create a Ruby application</span></span>
<span data-ttu-id="562ad-102">Para obtener instrucciones, vea cómo [crear una aplicación de Ruby en Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="562ad-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="562ad-103">Configuración de la aplicación para usar el Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="562ad-103">Configure Your application to Use Service Bus</span></span>
<span data-ttu-id="562ad-104">Para usar Service Bus, descargue y use el paquete de Ruby de Azure, que incluye un conjunto de útiles bibliotecas que se comunican con los servicios REST de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="562ad-104">To use Service Bus, download and use the Azure Ruby package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="562ad-105">Uso de RubyGems para obtener el paquete</span><span class="sxs-lookup"><span data-stu-id="562ad-105">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="562ad-106">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="562ad-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="562ad-107">Escriba "gem install azure" en la ventana de comandos para instalar la gema y las dependencias.</span><span class="sxs-lookup"><span data-stu-id="562ad-107">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="562ad-108">Importación del paquete</span><span class="sxs-lookup"><span data-stu-id="562ad-108">Import the package</span></span>
<span data-ttu-id="562ad-109">Con el editor de texto que prefiera, agregue lo siguiente al principio del archivo de Ruby en el que pretenda utilizar el almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="562ad-109">Using your favorite text editor, add the following to the top of the Ruby file in which you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="562ad-110">Configuración de una conexión del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="562ad-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="562ad-111">Utilice el código siguiente para establecer los valores de espacio de nombres, nombre de la clave, clave, firmante y host:</span><span class="sxs-lookup"><span data-stu-id="562ad-111">Use the following code to set the values of namespace, name of the key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="562ad-112">Defina el valor del espacio de nombres en el valor que creó en lugar de hacerlo en la dirección URL completa.</span><span class="sxs-lookup"><span data-stu-id="562ad-112">Set the namespace value to the value you created rather than the entire URL.</span></span> <span data-ttu-id="562ad-113">Por ejemplo, utilice **"suespaciodenombresdeejemplo"**, no "suespaciodenombresdeejemplo.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="562ad-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
