### <a name="prerequisites"></a>Requisitos previos
* Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)
* Un [base de datos de SQL Azure](../articles/sql-database/sql-database-get-started.md) con su información de conexión, incluido el nombre del servidor hello, nombre de base de datos y nombre de usuario/contraseña. Esta información se incluye en la cadena de conexión de base de datos SQL de hello:
  
    Server=tcp:*yoursqlservername*.database.windows.net,1433;Initial Catalog=*yourqldbname*;Persist Security Info=False;User ID={your_username};Password={your_password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
  
    Más información sobre [Azure SQL Database](https://azure.microsoft.com/services/sql-database).

> [!NOTE]
> Cuando se crea una base de datos de SQL Azure, también puede crear bases de datos de ejemplo de Hola incluidas con SQL. 
> 
> 

Antes de usar la base de datos de SQL Azure en una aplicación de lógica, conectar tooyour base de datos SQL. Puede hacerlo fácilmente dentro de la aplicación lógica en hello portal de Azure.  

Conectar tooyour base de datos de SQL de Azure mediante Hola siguiendo los pasos:  

1. Cree una aplicación lógica. En el Diseñador de aplicaciones de la lógica de hello, agregar un desencadenador y, a continuación, agregue una acción. Seleccione **API administradas de Microsoft mostrar** Hola lista desplegable y, a continuación, escriba "sql" en el cuadro de búsqueda de Hola. Seleccione una de las acciones de hello:  
   
    ![paso de creación de conexión de SQL Azure](./media/connectors-create-api-sqlazure/sql-actions.png)
2. Si anteriormente no ha creado ninguna base de datos de las conexiones tooSQL, le pediremos detalles de la conexión de hello:  
   
    ![paso de creación de conexión de SQL Azure](./media/connectors-create-api-sqlazure/connection-details.png) 
3. Escriba los detalles de la base de datos SQL de Hola. Aquellas propiedades con un asterisco son obligatorias.
   
   | Propiedad | Detalles |
   | --- | --- |
   | Connect via Gateway (Conectar a través de puerta de enlace) |Deje esta opción desactivada. Esto se utiliza al conectarse tooan local de SQL Server. |
   | Nombre de la conexión * |Escriba cualquier nombre para la conexión. |
   | Nombre de SQL Server * |Especificar nombre de servidor hello; que es similar a *nombreDeServidor.baseDeDatos.Windows.NET*. nombre del servidor Hello es aparece en las propiedades de la base de datos SQL de Hola Hola portal de Azure y también se muestra en la cadena de conexión de Hola. |
   | Nombre de la base de datos SQL * |Escriba nombre Hola se le asignó la base de datos de SQL. Esto se muestra en las propiedades de base de datos SQL de hello en la cadena de conexión de hello: Initial Catalog =*yoursqldbname*. |
   | Nombre de usuario * |Escriba el nombre de usuario de Hola que creó cuando creó la base de datos SQL de Hola. Esto se muestra en las propiedades de la base de datos SQL de Hola Hola portal de Azure. |
   | Contraseña * |Escriba la contraseña de Hola que creó cuando creó la base de datos SQL de Hola. |
   
    Estas credenciales son tooauthorize usa su tooconnect de aplicación lógica y obtener acceso a los datos SQL. Una vez completado, los detalles de la conexión tener un aspecto similar siguiente toohello:  
   
    ![paso de creación de conexión de SQL Azure](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. Seleccione **Crear**. 
5. Se ha creado la conexión de anuncio Hola. Ahora, proceda con hello otro pasos de la aplicación lógica: 
   
    ![paso de creación de conexión de SQL Azure](./media/connectors-create-api-sqlazure/table.png)

