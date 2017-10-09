1. En una nueva ventana, inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda hello, haga clic en **New**, haga clic en **bases de datos**y, a continuación, en **base de datos de Azure Cosmos**, haga clic en **crear**.
   
   ![Captura de pantalla de portal de Azure, resaltado más servicios y base de datos de Azure Cosmos Hola](./media/cosmos-db-create-dbaccount-table/create-nosql-db-databases-json-tutorial-1.png)

3. Hola **nueva cuenta** hoja, especifican la configuración deseada de Hola para hello cuenta de base de datos de Azure Cosmos. 

    Con Azure Cosmos DB, puede elegir uno de cuatro modelos de programación: Gremlin (grafo), MongoDB, SQL (DocumentDB) y Table (clave-valor). 
    
    En esta guía de inicio rápido se deberá estar programando con hello API de tabla por lo que podrá elegir **tabla (clave-valor)** tal y como rellene el formulario de Hola. Pero si tiene datos de grafos para una aplicación de redes sociales, datos de documentos de una aplicación de catálogo o datos migrados desde una aplicación de MongoDB, debe tener en cuenta que Azure Cosmos DB puede proporcionar una plataforma de servicio de base de datos distribuida globalmente y de alta disponibilidad para todas las aplicaciones críticas.

    Rellene la nueva hoja de cuenta Hola con información de Hola de captura de pantalla de hello como guía. Puede elegir valores únicos que configure su cuenta, por lo que sus valores no coincidan exactamente Hola captura de pantalla. 
 
    ![Captura de pantalla de hoja de la nueva base de datos de Azure Cosmos de Hola](./media/cosmos-db-create-dbaccount-table/create-nosql-db-databases-json-tutorial-2.png)

    Configuración|Valor sugerido|Descripción
    ---|---|---
    ID|*Valor único*|Un nombre único elegir cuenta de base de datos de Azure Cosmos hello tooidentify. *Documents.Azure.com* es Id. de toohello anexado proporcione toocreate su URI, por lo que usar un identificador único pero identificable. Id. de Hello puede contener solo letras minúsculas, números y hello '-' caracteres y debe tener entre 3 y 50 caracteres.
    API|Tabla (clave-valor)|Se deberá estar programando con hello [API tabla](../articles/cosmos-db/table-introduction.md) más adelante en este artículo.|
    La suscripción|*Su suscripción*|Hola suscripción de Azure que quiere toouse de cuenta de base de datos de Azure Cosmos Hola. 
    Grupo de recursos|*Hola mismo valor que el Id.*|Hola nuevo recurso nombre de grupo para su cuenta. Para simplificar, puede usar Hola mismo nombre como su identificador. 
    Ubicación|*usuarios de Hello región más cercanos tooyour*|Hola ubicación geográfica en la que toohost su cuenta de base de datos de Azure Cosmos. Elegir ubicación de hello más cercanos usuarios tooyour toogive ellos Hola toohello más rápido acceso a los datos.   

4. Haga clic en **crear** cuenta de hello toocreate.
5. En la barra de herramientas de hello, haga clic en **notificaciones** toomonitor proceso de implementación de Hola.

    ![Notificación Implementación iniciada](./media/cosmos-db-create-dbaccount-table/notification.png)

6.  Una vez completada la implementación de hello, nueva cuenta de hello abierto de hello todos los recursos en mosaico. 

    ![Cuenta de DocumentDB en hello que todos los recursos en mosaico](./media/cosmos-db-create-dbaccount-table/all-resources.png)
