1. En una nueva ventana, inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el panel izquierdo de hello, haga clic en **New**, haga clic en **bases de datos**y, a continuación, en **base de datos de Azure Cosmos**, haga clic en **crear**.
   
   ![Hello Azure portal panel de las bases de datos](./media/cosmos-db-create-dbaccount/create-nosql-db-databases-json-tutorial-1.png)

3. En hello **nueva cuenta** hoja, especificar configuración de Hola que desee para esta cuenta de base de datos de Azure Cosmos. 

    Con Azure Cosmos DB, puede elegir uno de cuatro modelos de programación: Gremlin (grafo), MongoDB, SQL (DocumentDB) y Table (clave-valor), cada uno de los cuales requiere actualmente una cuenta independiente.
    
    En este artículo de inicio rápido se programa contra Hola API de documentos, elija **SQL (documentos)** tal y como rellene el formulario de Hola. Si tiene datos de grafos para una aplicación de redes sociales, datos de clave/valor (tabla) o datos migrados desde una aplicación de MongoDB, debe tener en cuenta que Azure Cosmos DB puede proporcionar una plataforma de servicio de base de datos distribuida globalmente y de alta disponibilidad para todas las aplicaciones críticas.

    Complete los campos de hello en hello **nueva cuenta** hoja, con la información de Hola Hola siguiente captura de pantalla como una guía de los valores puede ser diferente de los valores de hello en captura de pantalla de Hola.
 
    ![hoja de Hello nueva cuenta de base de datos de Azure Cosmos](./media/cosmos-db-create-dbaccount/create-nosql-db-databases-json-tutorial-2.png)

    Configuración|Valor sugerido|Descripción
    ---|---|---
    ID|*Valor único*|Un nombre único que identifica esta cuenta de Azure Cosmos DB. Dado que *documents.azure.com* es toohello anexado ID que proporcione toocreate su URI, utilice un único pero identificación Id. Id. de Hello puede contener solo letras minúsculas, números y caracteres de guión (-) de Hola y debe contener 3 too50 caracteres.
    API|SQL (DocumentDB)|Se programa contra Hola [DocumentDB API](../articles/documentdb/documentdb-introduction.md) más adelante en este artículo.|
    La suscripción|*Su suscripción*|Hola suscripción de Azure que desea toouse para esta cuenta de base de datos de Azure Cosmos. 
    Grupo de recursos|*Hola mismo valor que el Id.*|Hola nuevo grupo de recursos nombre de su cuenta. Para simplificar, puede usar Hola mismo nombre como su identificador. 
    Ubicación|*usuarios de Hello región más cercanos tooyour*|Hola ubicación geográfica en la que toohost su cuenta de base de datos de Azure Cosmos. Elegir ubicación de Hola que sea más cercano toogive de los usuarios de tooyour ellos Hola toohello más rápido acceso a los datos.
4. Haga clic en **crear** cuenta de hello toocreate.
5. En la barra de herramientas superior hello, haga clic en hello **notificaciones** icono ![icono de notificación de hello](./media/cosmos-db-create-dbaccount/notification-icon.png) proceso de implementación de toomonitor Hola.

    ![Hello Azure panel notificaciones del portal](./media/cosmos-db-create-dbaccount-graph/azure-documentdb-nosql-notification.png)

6.  Cuando la ventana de notificaciones de hello indica ventana de notificación de hello implementación Hola se ha realizado correctamente, cierre y abra Hola nueva cuenta de hello **todos los recursos** icono Hola panel. 

    ![Hola cuenta de DocumentDB en hello que todos los recursos en mosaico](./media/cosmos-db-create-dbaccount/all-resources.png)
 
