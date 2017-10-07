---
title: aaaHow toouse Queue storage from. Ruby | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate del servicio de cola de Azure de toouse hello y colas de delete y insert, obtener y eliminar mensajes. Los ejemplos están escritos en Ruby."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a>¿Cómo toouse Queue storage from. Ruby
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio almacenamiento de cola de Microsoft Azure. ejemplos de Hola se escriben con hello Ruby API de Azure.
Hello escenarios descritos se incluyen **insertar**, **leerlo**, **obtener**, y **eliminar** cola los mensajes, así como  **crear y eliminar colas**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Creación de una aplicación de Ruby
Cree una aplicación de Ruby. Para instrucciones, consulte [Aplicación web de Ruby on Rails en una máquina virtual de Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurar la aplicación tooAccess almacenamiento
toouse almacenamiento de Azure, necesitará toodownload y use Hola Ruby paquete de azure, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.

### <a name="use-rubygems-tooobtain-hello-package"></a>Use el paquete de RubyGems tooobtain Hola
1. Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).
2. Escriba "indicador instalar azure" en el indicador de hello comando ventana tooinstall hello y dependencias.

### <a name="import-hello-package"></a>Importar paquete de Hola
Utilice el editor de texto, agregue Hola después de la parte superior de toohello de hello archivo Ruby donde piensa toouse almacenamiento:

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>Configuración de una conexión de almacenamiento de Azure
módulo de Hello azure leerá las variables de entorno de hello **AZURE\_almacenamiento\_cuenta** y **AZURE\_almacenamiento\_ACCESS_KEY** para cuenta de almacenamiento de Azure de tooconnect tooyour la información necesaria. Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello antes de usar **Azure::QueueService** con hello siguiente código:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

tooobtain estos valores de un clásico o el Administrador de recursos de almacenamiento de la cuenta de hello portal de Azure:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Navegar por cuenta de almacenamiento toohello que desea toouse.
3. En la hoja de configuración de hello en hello derecho, haga clic en **teclas de acceso**.
4. En la hoja las claves de acceso Hola que aparece, podrá ver clave de acceso de hello 1 y 2 de clave de acceso. Puede usar cualquiera de estas. 
5. Haga clic en el Portapapeles de hello copia icono toocopy hello toohello clave. 

Estos valores desde un almacenamiento clásico tooobtain tenga en cuenta en el portal de Azure clásico hello:

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Navegar por cuenta de almacenamiento toohello que desea toouse.
3. Haga clic en **administrar claves de acceso** final Hola Hola del panel de exploración.
4. Hola pop cuadro de diálogo, verá el nombre de cuenta de almacenamiento de hello, clave de acceso principal y clave de acceso secundaria. Para las claves de acceso, puede usar Hola principal o secundario de Hola. 
5. Haga clic en el Portapapeles de hello copia icono toocopy hello toohello clave.

## <a name="how-to-create-a-queue"></a>Creación de una cola
Hello código siguiente se crea un **Azure::QueueService** objeto, lo que permite toowork con colas.

```ruby
azure_queue_service = Azure::QueueService.new
```

Hola de uso **create_queue()** método toocreate una cola con hello nombre especificado.

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Inserción de un mensaje en una cola
tooinsert un mensaje en una cola, use hello **create_message()** método toocreate un mensaje nuevo y agregue toohello cola.

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>Cómo: Ver en el siguiente mensaje de Hola
Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **peek\_messages()** método. De forma predeterminada, **peek\_messages()** inspecciona un único mensaje. También puede especificar cuántos mensajes desea toopeek.

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>Cómo: Hola siguiente mensaje de eliminación de cola
Puede borrar un mensaje de una cola en dos pasos.

1. Cuando se llama a **lista\_messages()**, obtener el siguiente mensaje de Hola en una cola de forma predeterminada. También puede especificar cuántos mensajes desea tooget. Hola mensajes procedentes de **lista\_messages()** se convierte en invisible tooany otro código que lee mensajes de esta cola. Pasar en tiempo de espera de visibilidad de hello en segundos como un parámetro.
2. toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a **delete_message()**.

Este proceso de dos pasos de la eliminación de un mensaje garantiza cuando los tooprocess se produce un error de código puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje e inténtelo de nuevo. Las llamadas de código **eliminar\_message()** justo después de que se ha procesado el mensaje de bienvenida.

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Cómo: Cambiar el contenido de Hola de un mensaje en cola
Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de Hola. código de Hello siguiente utiliza hello **update_message()** método tooupdate un mensaje. método Hello devolverá una tupla que contiene la confirmación de recepción de Hola Hola del mensaje de cola y un valor de hora de fecha UTC que representa al mensaje de saludo será visible en la cola de Hola.

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Opciones adicionales para extraer mensajes de la cola
Hay dos formas de personalizar la recuperación de mensajes de una cola.

1. En primer lugar, puede obtener un lote de mensajes.
2. Puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje.

ejemplo de código siguiente Hello usa Hola **lista\_messages()** tooget 15 mensajes de método en una llamada. A continuación, imprime y elimina cada mensaje. También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para cada mensaje.

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>Cómo: Obtener la longitud de la cola de Hola
Puede obtener una estimación del número de Hola de mensajes en cola de Hola. Hola **obtener\_cola\_metadata()** método pide número aproximado de mensajes de Hola de tooreturn de servicio de hello cola y los metadatos acerca de la cola de Hola.

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>Eliminación de una cola
toodelete una cola y todos los mensajes de Hola contenidas en ella, llamada hello **eliminar\_queue()** método hello en objetos de cola.

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn vínculos acerca de las tareas más complejas de almacenamiento.

* Visite hello [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Visite hello [Azure SDK para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repositorio en GitHub

Para obtener una comparación entre Hola el servicio de cola de Azure se describe en este artículo y colas de Bus de servicio de Azure descrito en hello [cómo toouse colas de Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) artículo, consulte [colas de Azure y colas de Bus de servicio: comparación y Contrastar](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
