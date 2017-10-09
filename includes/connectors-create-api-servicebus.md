### <a name="prerequisites"></a>Requisitos previos
Debe tener una cuenta de [Service Bus](https://azure.microsoft.com/services/service-bus/).  

Antes de poder usar su cuenta de Service Bus de Azure en una aplicación de lógica, debe autorizar la cuenta de hello lógica aplicación tooconnect tooyour service bus. Afortunadamente, puede hacer esto fácilmente desde dentro de la aplicación lógica en hello portal de Azure.  

Estos es Hola pasos tooauthorize su tooconnect de aplicación lógica tooyour cuenta de Bus de servicio:  

1. toocreate una tooService de conexión Bus, en el Diseñador de aplicaciones de la lógica de hello, seleccione **API administradas de Microsoft mostrar** en la lista desplegable de Hola. A continuación, escriba **bus de servicio** en el cuadro de búsqueda de Hola. Seleccione el desencadenador de Hola o acción que desea toouse.  
    ![Imagen 1 de conexión a Service Bus](./media/connectors-create-api-servicebus/servicebus-1.png)  
2. Si no ha creado ningún tooService conexiones Bus antes, estará tooprovide solicitada sus credenciales de Bus de servicio. Estas credenciales son utilizada tooauthorize su tooand de tooconnect de aplicación lógica tener acceso a datos de la cuenta de Bus de servicio. Conector de Bus de servicio de Hello necesita cadena de conexión de hello para el espacio de nombres de Bus de servicio de Hola. y también, permisos de **administración**. Una buena manera tooknow si la cadena de conexión es de espacio de nombres de Hola o una entidad específica si contiene Hola `EntityPath` parámetro. Si es así, no es cadena de conexión adecuada de Hola para una aplicación de lógica.  
    ![Cadena de conexión de Service Bus](./media/connectors-create-api-servicebus/connectionstring.png)
3. Después de haber recibido la cadena de conexión de hello para el espacio de nombres de hello, puede utilizarlo para hello conexión de API en las aplicaciones lógicas.  
    ![Imagen 2 de conexión a Bus de servicio](./media/connectors-create-api-servicebus/servicebus-2.png)  
4. Tenga en cuenta se ha creado la conexión de Hola y está ahora disponible tooproceed con hello otro pasos en la aplicación lógica.  
    ![Imagen 3 de conexión a Bus de servicio](./media/connectors-create-api-servicebus/servicebus-3.png)   

