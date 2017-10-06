---
título: aaa "lección complementaria tutorial de Analysis Services de Azure: seguridad dinámica | Descripción de Microsoft Docs": describe cómo toouse la seguridad dinámica utilizando fila filtra hello Azure tutorial de Analysis Services.
servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="supplemental-lesson---dynamic-security"></a>Lección complementaria: Seguridad dinámica

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección complementaria, creará un rol función que implementa la seguridad dinámica. Seguridad dinámica proporciona seguridad de nivel de fila en función de Id. de inicio de sesión o nombre del usuario de hello del usuario de hello ha iniciado sesión actualmente. 
  
tooimplement la seguridad dinámica, agregue un modelo de tooyour de tabla que contiene los nombres de usuario de Hola de los usuarios que pueden conectarse toohello modelo y examinar los datos y objetos del modelo. modelo de Hola que se crea con este tutorial está en contexto de Hola de Adventure Works; Sin embargo, toocomplete esta lección, debe agregar una tabla que contiene los usuarios de su propio dominio. No es necesario contraseñas Hola Hola nombres de usuario que se agregan. toocreate una tabla de EmployeeSecurity, con una pequeña muestra de los usuarios de su propio dominio, se usan Hola pegar, pegar datos de empleados desde una hoja de cálculo de Excel. En un escenario real, tabla de Hola que contiene los nombres de usuario normalmente sería una tabla de una base de datos real como origen de datos; Por ejemplo, una tabla DimEmployee real.  
  
tooimplement la seguridad dinámica, se utilizan dos funciones DAX: [función USERNAME (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) y [función LOOKUPVALUE (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Estas funciones, aplicadas en una fórmula de filtro de fila, se definen en un nuevo rol. Al usar la función LOOKUPVALUE de hello, fórmula Hola especifica un valor de tabla de EmployeeSecurity Hola. fórmula de Hello, a continuación, pasa el que la función de valor toohello USERNAME, que especifica el nombre de usuario de Hola de una sesión de usuario de Hola pertenece toothis rol. Hola usuario puede examinar los datos especificados por los filtros de fila del rol de Hola. En este escenario, puede especificar que los empleados de ventas solo pueden examinar los datos de ventas de Internet de territorios de ventas de hello en el que son miembros.  
  
Las tareas que son toothis único escenario de modelo tabular de Adventure Works, pero no se aplicarían necesariamente escenario real de tooa se identifican como tales. Cada tarea incluye información adicional que describa el propósito de Hola de tarea hello.  
  
Estimado toocomplete de tiempo en esta lección: **30 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema de la lección complementaria forma parte de un tutorial de modelado tabular, que debe completar en orden. Antes de realizar tareas de hello en esta lección complementaria, deberá haber finalizado todas las lecciones anteriores.  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>Agregar hello DimSalesTerritory tabla toohello proyecto de modelo Tabular de ventas de Internet de AW  
tooimplement la seguridad dinámica para este escenario de Adventure Works, debe agregar dos modelos de tooyour tablas adicionales. primera tabla de Hello agregará es DimSalesTerritory (como Sales Territory) de Hola misma base de datos AdventureWorksDW. Adelante aplicar una tabla de SalesTerritory de toohello de filtros de fila que define datos determinado Hola Hola usuario que inició sesión puede examinar.  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>tabla de tooadd hello DimSalesTerritory  
  
1.  En el Explorador de modelos tabulares, expanda **Orígenes de datos**, haga clic con el botón derecho en la conexión y, luego, haga clic en **Importar nuevas tablas**.  

    Si aparece el cuadro de diálogo de credenciales de suplantación de hello, escriba las credenciales de suplantación de Hola que usó en la lección 2: agregar datos.
  
2.  En el navegador, seleccione hello **DimSalesTerritory** de tabla y, a continuación, haga clic en **Aceptar**.    
  
3.  En el Editor de consultas, haga clic en hello **DimSalesTerritory** de consulta y, a continuación, quitar **SalesTerritoryAlternateKey** columna.  
  
7.  Haga clic en **Import**.  
  
    nueva tabla de Hola se agrega el área de trabajo de toohello modelo. Objetos y datos de tabla de origen DimSalesTerritory de hello, a continuación, se importan en el MT ventas AW.  
  
9. Después de tabla Hola se ha importado correctamente, haga clic en **cerrar**.  

## <a name="add-a-table-with-user-name-data"></a>Incorporación de una tabla con datos de nombres de usuario  
tabla DimEmployee de Hello en la base de datos de ejemplo de Hola AdventureWorksDW contiene usuarios del dominio de AdventureWorks de Hola. Los nombres de usuario no existen en su propio entorno. Debe crear una tabla en el modelo que contenga una pequeña muestra de usuarios reales de su organización (al menos tres). A continuación, agregar estos usuarios como miembros toohello nuevo rol. No necesita las contraseñas de Hola para nombres de usuario de ejemplo de Hola, pero necesita nombres de usuario de Windows reales de su propio dominio.  
  
#### <a name="tooadd-an-employeesecurity-table"></a>tooadd una tabla EmployeeSecurity  
  
1.  Abra Microsoft Excel para crear una hoja de cálculo.  
  
2.  Copie hello en la tabla, incluida la fila de encabezado de hello, siguiente y, a continuación, péguelo en la hoja de cálculo de Hola.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Reemplace Hola nombre, apellido y dominio ombre de usuario con nombres de hello e identificadores de inicio de sesión de tres usuarios de su organización. Colocar Hola mismo usuario en dos primeras filas de hello, EmployeeId 1, que muestra toomore a un territorio de ventas que pertenece este usuario. Deje Hola campos EmployeeId y SalesTerritoryId tal como están.  
  
4.  Guardar la hoja de cálculo de hello como **SampleEmployee**.  
  
5.  En la hoja de cálculo de hello, seleccionar todas las celdas de hello con datos de empleados, incluidos los encabezados de hello, a continuación, haga clic en datos de hello seleccionado y, a continuación, haga clic en **copia**.  
  
6.  En SSDT, haga clic en hello **editar** menú y, a continuación, haga clic en **pegar**.  
  
    Si está atenuado pegar, haga clic en cualquier columna de cualquier tabla en la ventana del Diseñador de modelos Hola e inténtelo de nuevo.  
  
7.  Hola **vista previa de pegado** cuadro de diálogo **nombre de la tabla**, tipo **EmployeeSecurity**.  
  
8.  En **toobe datos pegar**, compruebe los datos de hello incluyen todos los datos de usuario de Hola y encabezados de hoja de cálculo de hello SampleEmployee.  
  
9. Compruebe que la casilla **Usar primera fila como encabezados de columna** está activada y, luego, haga clic en **Aceptar**.  
  
    Se crea una nueva tabla denominada EmployeeSecurity con datos de empleado copiados desde la hoja de cálculo de hello SampleEmployee.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Creación de relaciones entre las tablas FactInternetSales, DimGeography y DimSalesTerritory  
tabla de FactInternetSales, DimGeography y DimSalesTerritory de Hello todos contiene una columna común, SalesTerritoryId. columna de SalesTerritoryId Hello en la tabla DimSalesTerritory de hello contiene valores con un identificador distinto para cada territorio de ventas.  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>relaciones de toocreate entre hello FactInternetSales, DimGeography y tabla de hello DimSalesTerritory  
  
1.  En la vista de diagrama de hello **DimGeography** de tabla, haga clic y mantenga en hello **SalesTerritoryId** columna y, a continuación, arrastre Hola cursor toohello **SalesTerritoryId** columna Hola **DimSalesTerritory** de tabla y, a continuación, la versión.  
  
2.  Hola **FactInternetSales** de tabla, haga clic y mantenga en hello **SalesTerritoryId** columna y, a continuación, arrastre Hola cursor toohello **SalesTerritoryId** columna Hola  **DimSalesTerritory** de tabla y, a continuación, la versión.  
  
    Hola aviso propiedad Active de esta relación es False, lo que significa que está inactivo. tabla de Hello FactInternetSales ya tiene otra relación activa.  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>Ocultar hello EmployeeSecurity tabla desde las aplicaciones cliente  
En esta tarea, Ocultar tabla EmployeeSecurity de hello, evitando que aparezca en la lista de campos de la aplicación cliente. Tenga en cuenta que ocultar una tabla no significa protegerla. Los usuarios todavía pueden consultar datos de la tabla EmployeeSecurity, si saben cómo. toosecure Hola EmployeeSecurity: datos de la tabla, impide que los usuarios tooquery capaz de cualquiera de sus datos, aplicar un filtro en una tarea posterior.  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>tabla de EmployeeSecurity toohide Hola desde aplicaciones cliente  
  
-   En el Diseñador de modelos de hello, en la vista de diagrama, haga clic en hello **empleado** encabezado de tabla y, a continuación, haga clic en **ocultar en las herramientas de cliente de**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Creación de un rol de usuario Empleados de ventas por territorio  
En esta tarea, creará un rol de usuario. Este rol incluye un filtro de fila define qué filas de la tabla DimSalesTerritory de hello son toousers visible. Hola, a continuación, aplicar filtro en la relación de uno a varios Hola dirección tooall otras tablas relacionada tooDimSalesTerritory. También aplica un filtro que protege Hola toda EmployeeSecurity la tabla de consultas por cualquier usuario que sea miembro del rol de Hola.  
  
> [!NOTE]  
> Hola empleados de ventas por el rol de territorio que creará en esta lección restringe los miembros toobrowse (o consultas) solo datos de ventas de hello toowhich de territorio de ventas al que pertenecen. Si agrega un usuario como un miembro toohello empleados de ventas por el rol de territorio que también existe como un miembro de un rol creado en [lección 11: crear Roles](../tutorials/aas-lesson-11-create-roles.md), obtendrá una combinación de permisos. Cuando un usuario es miembro de varios roles, permisos de Hola y filtros de fila definidos para cada rol son acumulativos. Es decir, usuario de hello tiene permisos mayores de hello determinados por la combinación de Hola de roles.  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>toocreate empleados de ventas por el rol de usuario de territorio  
  
1.  En SSDT, haga clic en hello **modelo** menú y, a continuación, haga clic en **Roles**.  
  
2.  En **Administrador de roles**, haga clic en **Nuevo**.  
  
    Un nuevo rol con hello agregar ninguna permiso es toohello lista.  
  
3.  Haga clic en nuevo rol de hello y, a continuación, en hello **nombre** columna, cambie el nombre de rol de hello demasiado**empleados de ventas por territorio**.  
  
4.  Hola **permisos** columna, haga clic en la lista desplegable de hello y, a continuación, seleccione hello **lectura** permiso.  
  
5.  Haga clic en hello **miembros** ficha y, a continuación, haga clic en **agregar**.  
  
6.  Hola **Seleccionar usuario o grupo** cuadro de diálogo **objeto de hello ENTRAR denominado tooselect**, escriba Hola primer ejemplo nombre de usuario que utilizó al crear la tabla de EmployeeSecurity Hola. Haga clic en **comprobar nombres** tooverify nombre de usuario de hello es válida y, a continuación, haga clic en **Aceptar**.  
  
    Repita este paso, agregar Hola otros nombres de usuario de ejemplo que utilizó al crear la tabla de EmployeeSecurity Hola.  
  
7.  Haga clic en hello **filtros de fila** ficha.  
  
8.  Para hello **EmployeeSecurity** tabla Hola **filtro DAX** columna, Hola de tipo siguiente fórmula:  
  
    ```
      =FALSE()  
    ```
  
    Esta fórmula especifica que todas las columnas resolverán toohello de condición booleana false. No hay columnas de tabla de hello EmployeeSecurity pueden ser consultadas por un miembro de hello empleados de ventas por el rol de usuario de territorio.  
  
9. Para hello **DimSalesTerritory** tabla, Hola de tipo siguiente fórmula:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    En esta fórmula, Hola función LOOKUPVALUE devuelve todos los valores de columna de hello DimEmployeeSecurity [SalesTerritoryId], donde hello EmployeeSecurity [LoginId] es Hola igual como Hola actual ha iniciado sesión nombre de usuario de Windows y EmployeeSecurity [ SalesTerritoryId] es Hola igual que hello DimSalesTerritory [SalesTerritoryId].  
  
    Hello conjunto de identificadores de territorio de ventas devueltos por LOOKUPVALUE es toorestrict usado Hola filas que se muestran en la tabla DimSalesTerritory Hola. Se muestran solo las filas donde hello SalesTerritoryID por fila Hola está en hello conjunto de identificadores devueltos por la función LOOKUPVALUE de Hola.  
  
10. En el Administrador de roles, haga clic en **Aceptar**.  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>Probar los empleados de ventas de Hola por el rol de usuario de territorio  
En esta tarea, se usa Hola analizar esta característica en la eficacia de hello tootest SSDT de hello empleados de ventas por el rol de usuario de territorio. Especifique uno de los nombres de usuario de hello agregó toohello EmployeeSecurity tabla y como un miembro del rol de Hola. Este nombre de usuario, a continuación, se utiliza como nombre de usuario efectivo de hello en conexión de hello creada entre Excel y Hola modelo.  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>Hola tootest empleados de ventas por el rol de usuario de territorio  
  
1.  En SSDT, haga clic en hello **modelo** menú y, a continuación, haga clic en **analizar en Excel**.  
  
2.  Hola **analizar en Excel** cuadro de diálogo **especificar Hola nombre o rol toouse tooconnect toohello modelo de usuario**, seleccione **otro usuario de Windows**y, a continuación, haga clic en **Examinar**.  
  
3.  Hola **Seleccionar usuario o grupo** cuadro de diálogo **escriba Hola objeto nombre tooselect**, escriba un nombre de usuario incluido en la tabla de EmployeeSecurity de hello y, a continuación, haga clic en **comprobar nombres**.  
  
4.  Haga clic en **Aceptar** tooclose hello **Seleccionar usuario o grupo** cuadro de diálogo y, a continuación, haga clic en **Aceptar** tooclose hello **analizar en Excel** cuadro de diálogo.  
  
    Excel se abre con un nuevo libro. Automáticamente se crea una tabla dinámica. Hola lista PivotTable Fields incluye la mayoría de campos de datos de hello disponibles en el nuevo modelo.  
  
    Tabla de aviso hello EmployeeSecurity no está visible en hello lista PivotTable Fields. Ocultó esta tabla de las herramientas de cliente en una tarea anterior.  
  
5.  Hola **campos** lista **∑ Internet Sales** (medidas), seleccione hello **InternetTotalSales** medida. medida de Hola se introduce en hello **valores** campos.  
  
6.  Seleccione hello **SalesTerritoryId** columna de hello **DimSalesTerritory** tabla. columna de Hola se introduce en hello **etiquetas de fila** campos.  
  
    Internet aviso cifras de ventas solo aparecen para hello una región toowhich Hola nombre de usuario efectivo que usó pertenece. Si selecciona otra columna, como la ciudad de la tabla de hello DimGeography como campo de etiqueta de fila, solo ciudades de usuario efectivo de hello territorio de ventas toowhich Hola pertenece se muestran.  
  
    Este usuario no se puede examinar o consultar los datos de ventas de Internet para otros territorios distintos Hola uno al que pertenecen. Esta restricción es porque el filtro de fila definido para la tabla DimSalesTerritory de hello, Hola empleados de ventas por el rol de usuario de territorio, hello protege los datos para todos los datos relacionados con los territorios de ventas de tooother.  
  
## <a name="see-also"></a>Otras referencias  
[Función USERNAME (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[Función LOOKUPVALUE (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[Función CUSTOMDATA (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  