
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a>Ejemplo de programa C#

Hola siguientes secciones de este artículo presentan un programa de C# que utiliza la base de datos SQL de toohello de instrucciones de ADO.NET toosend Transact-SQL. programa Hello C# realiza Hola siguientes acciones:

1. [Se conecta utilizando ADO.NET de base de datos SQL tooour](#cs_1_connect).
2. [Crea tablas](#cs_2_createtables).
3. [Rellena las tablas de hello con datos, mediante la emisión de instrucciones T-SQL INSERT](#cs_3_insert).
4. [Actualiza datos mediante una combinación](#cs_4_updatejoin).
5. [Elimina datos mediante una combinación](#cs_5_deletejoin).
6. [Selecciona filas de datos mediante una combinación](#cs_6_selectrows).
7. Cierra la conexión de hello (que quita cualquier tabla temporal de tempdb).

contiene el programa Hola C#:

- C# base de datos de código tooconnect toohello.
- Métodos que devuelven el código fuente de hello T-SQL.
- Dos métodos que envían Hola base de datos de T-SQL toohello.

#### <a name="toocompile-and-run"></a>toocompile y ejecución

Este programa C# es lógicamente un archivo .cs. Pero aquí programa Hola físicamente se divide en varios bloques de código, toomake cada bloque toosee más fácil y comprender. toocompile y ejecutar este programa, Hola siguientes:

1. Cree un proyecto C# en Visual Studio.
    - debe ser el tipo de proyecto de Hello un *consola* aplicación de algo parecido a Hola después de jerarquía: **plantillas** > **Visual C#** > **Escritorio clásico de Windows** > **(.NET Framework) de la aplicación de consola**.
3. En el archivo hello **Program.cs**, borrar Hola starter pequeñas líneas de código.
3. En Program.cs, copiar y pegar de hello siguiente bloques, en Hola la misma secuencia que se van a mostrar aquí.
4. En Program.cs, siguiente de hello editar valores de hello **Main** método:

   - **cb.DataSource**
   - **cd.UserID**
   - **cb.Password**
   - **InitialCatalog**

5. Comprobar dicho ensamblado hello **System.Data.dll** se hace referencia. tooverify, expanda hello **referencias** nodo Hola **el Explorador de soluciones** panel.
6. programa de hello toobuild en Visual Studio, haga clic en hello **generar** menú.
7. programa de hello toorun desde Visual Studio, haga clic en hello **iniciar** botón. resultados del informe Hola se muestran en una ventana cmd.exe.

> [!NOTE]
> Tiene la opción de hello de la edición de hello T-SQL tooadd inicial  **#**  toohello nombres de tabla que crea tablas temporales como en **tempdb**. Esto puede ser útil como demostración, cuando no haya ninguna base de datos de prueba disponible. Tablas temporales se eliminan automáticamente cuando se cierra la conexión de Hola. Todas las REFERENCIAS a claves externas no se aplican para las tablas temporales.
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a>Bloque de C# 1: conectar mediante ADO.NET

- [Siguiente](#cs_2_createtables)


```csharp
using System;
using System.Data.SqlClient;   // System.Data.dll 
//using System.Data;           // For:  SqlDbType , ParameterDirection

namespace csharp_db_test
{
   class Program
   {
      static void Main(string[] args)
      {
         try
         {
            var cb = new SqlConnectionStringBuilder();
            cb.DataSource = "your_server.database.windows.net";
            cb.UserID = "your_user";
            cb.Password = "your_password";
            cb.InitialCatalog = "your_database";

            using (var connection = new SqlConnection(cb.ConnectionString))
            {
               connection.Open();

               Submit_Tsql_NonQuery(connection, "2 - Create-Tables",
                  Build_2_Tsql_CreateTables());

               Submit_Tsql_NonQuery(connection, "3 - Inserts",
                  Build_3_Tsql_Inserts());

               Submit_Tsql_NonQuery(connection, "4 - Update-Join",
                  Build_4_Tsql_UpdateJoin(),
                  "@csharpParmDepartmentName", "Accounting");

               Submit_Tsql_NonQuery(connection, "5 - Delete-Join",
                  Build_5_Tsql_DeleteJoin(),
                  "@csharpParmDepartmentName", "Legal");

               Submit_6_Tsql_SelectEmployees(connection);
            }
         }
         catch (SqlException e)
         {
            Console.WriteLine(e.ToString());
         }
         Console.WriteLine("View hello report output here, then press any key tooend hello program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-toocreate-tables"></a>Bloque de C# 2: tablas de toocreate de T-SQL

- [Anterior](#cs_1_connect)&nbsp; / &nbsp;[Siguiente](#cs_3_insert)

```csharp
      static string Build_2_Tsql_CreateTables()
      {
         return @"
DROP TABLE IF EXISTS tabEmployee;
DROP TABLE IF EXISTS tabDepartment;  -- Drop parent table last.


CREATE TABLE tabDepartment
(
   DepartmentCode  nchar(4)          not null
      PRIMARY KEY,
   DepartmentName  nvarchar(128)     not null
);

CREATE TABLE tabEmployee
(
   EmployeeGuid    uniqueIdentifier  not null  default NewId()
      PRIMARY KEY,
   EmployeeName    nvarchar(128)     not null,
   EmployeeLevel   int               not null,
   DepartmentCode  nchar(4)              null
      REFERENCES tabDepartment (DepartmentCode)  -- (REFERENCES would be disallowed on temporary tables.)
);
";
      }
```

#### <a name="entity-relationship-diagram-erd"></a>Diagrama de relaciones de entidades (ERD)

Hello instrucciones CREATE TABLE anteriores implican hello **referencias** palabra clave toocreate una *clave externa* relación (FK) entre dos tablas.  Si usas tempdb, comente hello `--REFERENCES` palabra clave con un par de guiones iniciales.

A continuación figura un ERD que muestra la relación de hello entre dos tablas de Hola. Hola valores de hello #tabEmployee.DepartmentCode *secundarios* columna son toohello limita los valores presentes en hello #tabDepartment.Department *primario* columna.

![ERD que muestra la clave externa](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a>Bloque de C# 3: datos de tooinsert de T-SQL

- [Anterior](#cs_2_createtables)&nbsp; / &nbsp;[Siguiente](#cs_4_updatejoin)


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- hello company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- hello company has these employees, each in one department.
INSERT INTO tabEmployee
   (EmployeeName, EmployeeLevel, DepartmentCode)
      VALUES
   ('Alison'  , 19, 'acct'),
   ('Barbara' , 17, 'hres'),
   ('Carol'   , 21, 'acct'),
   ('Deborah' , 24, 'legl'),
   ('Elle'    , 15, null);
";
      }
```


<a name="cs_4_updatejoin"/>
### <a name="c-block-4-t-sql-tooupdate-join"></a>Bloque de C# 4: combinación tooupdate de T-SQL

- [Anterior](#cs_3_insert)&nbsp; / &nbsp;[Siguiente](#cs_5_deletejoin)


```csharp
      static string Build_4_Tsql_UpdateJoin()
      {
         return @"
DECLARE @DName1  nvarchar(128) = @csharpParmDepartmentName;  --'Accounting';


-- Promote everyone in one department (see @parm...).
UPDATE empl
   SET
      empl.EmployeeLevel += 1
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName1;
";
      }
```


<a name="cs_5_deletejoin"/>
### <a name="c-block-5-t-sql-toodelete-join"></a>Bloque de C# 5: combinación toodelete de T-SQL

- [Anterior](#cs_4_updatejoin)&nbsp; / &nbsp;[Siguiente](#cs_6_selectrows)


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size hello Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband hello Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-tooselect-rows"></a>Bloque de C# 6: filas de T-SQL tooselect

- [Anterior](#cs_5_deletejoin)&nbsp; / &nbsp;[Siguiente](#cs_6b_datareader)


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all hello final Employees.
SELECT
      empl.EmployeeGuid,
      empl.EmployeeName,
      empl.EmployeeLevel,
      empl.DepartmentCode,
      dept.DepartmentName
   FROM
      tabEmployee   as empl
      LEFT OUTER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   ORDER BY
      EmployeeName;
";
      }
```


<a name="cs_6b_datareader"/>
### <a name="c-block-6b-executereader"></a>Bloque de C# 6b: ExecuteReader

- [Anterior](#cs_6_selectrows)&nbsp; / &nbsp;[Siguiente](#cs_7_executenonquery)

Este método es toorun diseñada Hola T-SQL instrucción SELECT que se compila en hello **Build_6_Tsql_SelectEmployees** método.


```csharp
      static void Submit_6_Tsql_SelectEmployees(SqlConnection connection)
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("Now, SelectEmployees (6)...");

         string tsql = Build_6_Tsql_SelectEmployees();

         using (var command = new SqlCommand(tsql, connection))
         {
            using (SqlDataReader reader = command.ExecuteReader())
            {
               while (reader.Read())
               {
                  Console.WriteLine("{0} , {1} , {2} , {3} , {4}",
                     reader.GetGuid(0),
                     reader.GetString(1),
                     reader.GetInt32(2),
                     (reader.IsDBNull(3)) ? "NULL" : reader.GetString(3),
                     (reader.IsDBNull(4)) ? "NULL" : reader.GetString(4));
               }
            }
         }
      }
```


<a name="cs_7_executenonquery"/>
### <a name="c-block-7-executenonquery"></a>Bloque de C# 7: ExecuteNonQuery

- [Anterior](#cs_6b_datareader)&nbsp; / &nbsp;[Siguiente](#cs_8_output)

Se llama a este método para las operaciones que modifican el contenido de las tablas de datos de hello sin devolver ninguna fila de datos.


```csharp
      static void Submit_Tsql_NonQuery(
         SqlConnection connection,
         string tsqlPurpose,
         string tsqlSourceCode,
         string parameterName = null,
         string parameterValue = null
         )
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("T-SQL too{0}...", tsqlPurpose);

         using (var command = new SqlCommand(tsqlSourceCode, connection))
         {
            if (parameterName != null)
            {
               command.Parameters.AddWithValue(  // Or, use SqlParameter class.
                  parameterName,
                  parameterValue);
            }
            int rowsAffected = command.ExecuteNonQuery();
            Console.WriteLine(rowsAffected + " = rows affected.");
         }
      }
   } // EndOfClass
}
```


<a name="cs_8_output"/>
### <a name="c-block-8-actual-test-output-toohello-console"></a>Bloque de C# 8: consola de toohello prueba real de salida

- [Anterior](#cs_7_executenonquery)

Esta sección captura el resultado de hello que Hola programa envía toohello consola. Solo los valores de guid de hello varían entre ejecuciones de pruebas.


```text
[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>> csharp_db_test.exe

=================================
Now, CreateTables (10)...

=================================
Now, Inserts (20)...

=================================
Now, UpdateJoin (30)...
2 rows affected, by UpdateJoin.

=================================
Now, DeleteJoin (40)...

=================================
Now, SelectEmployees (50)...
0199be49-a2ed-4e35-94b7-e936acf1cd75 , Alison , 20 , acct , Accounting
f0d3d147-64cf-4420-b9f9-76e6e0a32567 , Barbara , 17 , hres , Human Resources
cf4caede-e237-42d2-b61d-72114c7e3afa , Carol , 22 , acct , Accounting
cdde7727-bcfd-4f72-a665-87199c415f8b , Elle , 15 , NULL , NULL

[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>>
```
