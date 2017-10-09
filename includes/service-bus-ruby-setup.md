## <a name="create-a-ruby-application"></a>Creación de una aplicación de Ruby
Para obtener instrucciones, vea cómo [crear una aplicación de Ruby en Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-toouse-service-bus"></a>Configurar el Bus de servicio de aplicación tooUse
toouse Bus de servicio, descargar y usar el paquete de Azure Ruby hello, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.

### <a name="use-rubygems-tooobtain-hello-package"></a>Use el paquete de RubyGems tooobtain Hola
1. Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).
2. Escriba "indicador instalar azure" en el indicador de hello comando ventana tooinstall hello y dependencias.

### <a name="import-hello-package"></a>Importar paquete de Hola
Con su editor de texto que prefiera, agregar Hola después de la parte superior de toohello de hello Ruby en el que piensa toouse almacenamiento de archivo:

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>Configuración de una conexión del Bus de servicio
Valores de hello tooset del espacio de nombres, nombre del programa Hola a de código siguiente Hola de uso clave, clave, firmante y host:

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

Conjunto Hola espacio de nombres toohello valor creado en lugar de la dirección URL completa de Hola. Por ejemplo, utilice **"suespaciodenombresdeejemplo"**, no "suespaciodenombresdeejemplo.servicebus.windows.net".
