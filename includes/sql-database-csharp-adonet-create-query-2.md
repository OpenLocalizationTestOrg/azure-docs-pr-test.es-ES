
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="f8cc0-101">Ejemplo de programa C#</span><span class="sxs-lookup"><span data-stu-id="f8cc0-101">C# program example</span></span>

<span data-ttu-id="f8cc0-102">Hola siguientes secciones de este artículo presentan un programa de C# que utiliza la base de datos SQL de toohello de instrucciones de ADO.NET toosend Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-102">hello next sections of this article present a C# program that uses ADO.NET toosend Transact-SQL statements toohello SQL database.</span></span> <span data-ttu-id="f8cc0-103">programa Hello C# realiza Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="f8cc0-103">hello C# program performs hello following actions:</span></span>

1. <span data-ttu-id="f8cc0-104">[Se conecta utilizando ADO.NET de base de datos SQL tooour](#cs_1_connect).</span><span class="sxs-lookup"><span data-stu-id="f8cc0-104">[Connects tooour SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="f8cc0-105">[Crea tablas](#cs_2_createtables).</span><span class="sxs-lookup"><span data-stu-id="f8cc0-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="f8cc0-106">[Rellena las tablas de hello con datos, mediante la emisión de instrucciones T-SQL INSERT](#cs_3_insert).</span><span class="sxs-lookup"><span data-stu-id="f8cc0-106">[Populates hello tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="f8cc0-107">[Actualiza datos mediante una combinación](#cs_4_updatejoin).</span><span class="sxs-lookup"><span data-stu-id="f8cc0-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="f8cc0-108">[Elimina datos mediante una combinación](#cs_5_deletejoin).</span><span class="sxs-lookup"><span data-stu-id="f8cc0-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="f8cc0-109">[Selecciona filas de datos mediante una combinación](#cs_6_selectrows).</span><span class="sxs-lookup"><span data-stu-id="f8cc0-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="f8cc0-110">Cierra la conexión de hello (que quita cualquier tabla temporal de tempdb).</span><span class="sxs-lookup"><span data-stu-id="f8cc0-110">Closes hello connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="f8cc0-111">contiene el programa Hola C#:</span><span class="sxs-lookup"><span data-stu-id="f8cc0-111">hello C# program contains:</span></span>

- <span data-ttu-id="f8cc0-112">C# base de datos de código tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-112">C# code tooconnect toohello database.</span></span>
- <span data-ttu-id="f8cc0-113">Métodos que devuelven el código fuente de hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-113">Methods that return hello T-SQL source code.</span></span>
- <span data-ttu-id="f8cc0-114">Dos métodos que envían Hola base de datos de T-SQL toohello.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-114">Two methods that submit hello T-SQL toohello database.</span></span>

#### <a name="toocompile-and-run"></a><span data-ttu-id="f8cc0-115">toocompile y ejecución</span><span class="sxs-lookup"><span data-stu-id="f8cc0-115">toocompile and run</span></span>

<span data-ttu-id="f8cc0-116">Este programa C# es lógicamente un archivo .cs.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="f8cc0-117">Pero aquí programa Hola físicamente se divide en varios bloques de código, toomake cada bloque toosee más fácil y comprender.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-117">But here hello program is physically divided into several code blocks, toomake each block easier toosee and understand.</span></span> <span data-ttu-id="f8cc0-118">toocompile y ejecutar este programa, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8cc0-118">toocompile and run this program, do hello following:</span></span>

1. <span data-ttu-id="f8cc0-119">Cree un proyecto C# en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="f8cc0-120">debe ser el tipo de proyecto de Hello un *consola* aplicación de algo parecido a Hola después de jerarquía: **plantillas** > **Visual C#** > **Escritorio clásico de Windows** > **(.NET Framework) de la aplicación de consola**.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-120">hello project type should be a *console* application, from something like hello following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="f8cc0-121">En el archivo hello **Program.cs**, borrar Hola starter pequeñas líneas de código.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-121">In hello file **Program.cs**, erase hello small starter lines of code.</span></span>
3. <span data-ttu-id="f8cc0-122">En Program.cs, copiar y pegar de hello siguiente bloques, en Hola la misma secuencia que se van a mostrar aquí.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-122">Into Program.cs, copy and paste each of hello following blocks, in hello same sequence they are presented here.</span></span>
4. <span data-ttu-id="f8cc0-123">En Program.cs, siguiente de hello editar valores de hello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="f8cc0-123">In Program.cs, edit hello following values in hello **Main** method:</span></span>

   - <span data-ttu-id="f8cc0-124">**cb.DataSource**</span><span class="sxs-lookup"><span data-stu-id="f8cc0-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="f8cc0-125">**cd.UserID**</span><span class="sxs-lookup"><span data-stu-id="f8cc0-125">**cd.UserID**</span></span>
   - <span data-ttu-id="f8cc0-126">**cb.Password**</span><span class="sxs-lookup"><span data-stu-id="f8cc0-126">**cb.Password**</span></span>
   - <span data-ttu-id="f8cc0-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="f8cc0-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="f8cc0-128">Comprobar dicho ensamblado hello **System.Data.dll** se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-128">Verify that hello assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="f8cc0-129">tooverify, expanda hello **referencias** nodo Hola **el Explorador de soluciones** panel.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-129">tooverify, expand hello **References** node in hello **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="f8cc0-130">programa de hello toobuild en Visual Studio, haga clic en hello **generar** menú.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-130">toobuild hello program in Visual Studio, click hello **Build** menu.</span></span>
7. <span data-ttu-id="f8cc0-131">programa de hello toorun desde Visual Studio, haga clic en hello **iniciar** botón.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-131">toorun hello program from Visual Studio, click hello **Start** button.</span></span> <span data-ttu-id="f8cc0-132">resultados del informe Hola se muestran en una ventana cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-132">hello report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="f8cc0-133">Tiene la opción de hello de la edición de hello T-SQL tooadd inicial  **#**  toohello nombres de tabla que crea tablas temporales como en **tempdb**.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-133">You have hello option of editing hello T-SQL tooadd a leading **#** toohello table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="f8cc0-134">Esto puede ser útil como demostración, cuando no haya ninguna base de datos de prueba disponible.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="f8cc0-135">Tablas temporales se eliminan automáticamente cuando se cierra la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-135">Temporary tables are deleted automatically when hello connection closes.</span></span> <span data-ttu-id="f8cc0-136">Todas las REFERENCIAS a claves externas no se aplican para las tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="f8cc0-137">Bloque de C# 1: conectar mediante ADO.NET</span><span class="sxs-lookup"><span data-stu-id="f8cc0-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="f8cc0-138">Siguiente</span><span class="sxs-lookup"><span data-stu-id="f8cc0-138">Next</span></span>](#cs_2_createtables)


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
### <a name="c-block-2-t-sql-toocreate-tables"></a><span data-ttu-id="f8cc0-139">Bloque de C# 2: tablas de toocreate de T-SQL</span><span class="sxs-lookup"><span data-stu-id="f8cc0-139">C# block 2: T-SQL toocreate tables</span></span>

- <span data-ttu-id="f8cc0-140">[Anterior](#cs_1_connect)&nbsp; / &nbsp;[Siguiente](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="f8cc0-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

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

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="f8cc0-141">Diagrama de relaciones de entidades (ERD)</span><span class="sxs-lookup"><span data-stu-id="f8cc0-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="f8cc0-142">Hello instrucciones CREATE TABLE anteriores implican hello **referencias** palabra clave toocreate una *clave externa* relación (FK) entre dos tablas.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-142">hello preceding CREATE TABLE statements involve hello **REFERENCES** keyword toocreate a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="f8cc0-143">Si usas tempdb, comente hello `--REFERENCES` palabra clave con un par de guiones iniciales.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-143">If you are using tempdb, comment out hello `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="f8cc0-144">A continuación figura un ERD que muestra la relación de hello entre dos tablas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-144">Next is an ERD that displays hello relationship between hello two tables.</span></span> <span data-ttu-id="f8cc0-145">Hola valores de hello #tabEmployee.DepartmentCode *secundarios* columna son toohello limita los valores presentes en hello #tabDepartment.Department *primario* columna.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-145">hello values in hello #tabEmployee.DepartmentCode *child* column are limited toohello values present in hello #tabDepartment.Department *parent* column.</span></span>

![ERD que muestra la clave externa](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a><span data-ttu-id="f8cc0-147">Bloque de C# 3: datos de tooinsert de T-SQL</span><span class="sxs-lookup"><span data-stu-id="f8cc0-147">C# block 3: T-SQL tooinsert data</span></span>

- <span data-ttu-id="f8cc0-148">[Anterior](#cs_2_createtables)&nbsp; / &nbsp;[Siguiente](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="f8cc0-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


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
### <a name="c-block-4-t-sql-tooupdate-join"></a><span data-ttu-id="f8cc0-149">Bloque de C# 4: combinación tooupdate de T-SQL</span><span class="sxs-lookup"><span data-stu-id="f8cc0-149">C# block 4: T-SQL tooupdate-join</span></span>

- <span data-ttu-id="f8cc0-150">[Anterior](#cs_3_insert)&nbsp; / &nbsp;[Siguiente](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="f8cc0-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


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
### <a name="c-block-5-t-sql-toodelete-join"></a><span data-ttu-id="f8cc0-151">Bloque de C# 5: combinación toodelete de T-SQL</span><span class="sxs-lookup"><span data-stu-id="f8cc0-151">C# block 5: T-SQL toodelete-join</span></span>

- <span data-ttu-id="f8cc0-152">[Anterior](#cs_4_updatejoin)&nbsp; / &nbsp;[Siguiente](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="f8cc0-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


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
### <a name="c-block-6-t-sql-tooselect-rows"></a><span data-ttu-id="f8cc0-153">Bloque de C# 6: filas de T-SQL tooselect</span><span class="sxs-lookup"><span data-stu-id="f8cc0-153">C# block 6: T-SQL tooselect rows</span></span>

- <span data-ttu-id="f8cc0-154">[Anterior](#cs_5_deletejoin)&nbsp; / &nbsp;[Siguiente](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="f8cc0-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


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
### <a name="c-block-6b-executereader"></a><span data-ttu-id="f8cc0-155">Bloque de C# 6b: ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="f8cc0-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="f8cc0-156">[Anterior](#cs_6_selectrows)&nbsp; / &nbsp;[Siguiente](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="f8cc0-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="f8cc0-157">Este método es toorun diseñada Hola T-SQL instrucción SELECT que se compila en hello **Build_6_Tsql_SelectEmployees** método.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-157">This method is designed toorun hello T-SQL SELECT statement that is built by hello **Build_6_Tsql_SelectEmployees** method.</span></span>


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
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="f8cc0-158">Bloque de C# 7: ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="f8cc0-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="f8cc0-159">[Anterior](#cs_6b_datareader)&nbsp; / &nbsp;[Siguiente](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="f8cc0-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="f8cc0-160">Se llama a este método para las operaciones que modifican el contenido de las tablas de datos de hello sin devolver ninguna fila de datos.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-160">This method is called for operations that modify hello data content of tables without returning any data rows.</span></span>


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
### <a name="c-block-8-actual-test-output-toohello-console"></a><span data-ttu-id="f8cc0-161">Bloque de C# 8: consola de toohello prueba real de salida</span><span class="sxs-lookup"><span data-stu-id="f8cc0-161">C# block 8: Actual test output toohello console</span></span>

- [<span data-ttu-id="f8cc0-162">Anterior</span><span class="sxs-lookup"><span data-stu-id="f8cc0-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="f8cc0-163">Esta sección captura el resultado de hello que Hola programa envía toohello consola.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-163">This section captures hello output that hello program sent toohello console.</span></span> <span data-ttu-id="f8cc0-164">Solo los valores de guid de hello varían entre ejecuciones de pruebas.</span><span class="sxs-lookup"><span data-stu-id="f8cc0-164">Only hello guid values vary between test runs.</span></span>


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
