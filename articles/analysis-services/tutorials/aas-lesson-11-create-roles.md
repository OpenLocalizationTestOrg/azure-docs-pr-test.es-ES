---
título: aaa "lección tutorial de Analysis Services de Azure 11: crear roles | Descripción de Microsoft Docs": describe cómo toocreate roles en Hola proyecto tutorial de Analysis Services de Azure. servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-11-create-roles"></a>Lección 11: Creación de roles

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, creará roles. Los roles proporcionan seguridad de objetos y datos de la base de datos de modelo limitando tooonly de acceso a los usuarios que sean miembros del rol. Cada rol se define con un permiso único: Ninguno, Lectura, Lectura y procesamiento, Procesamiento o Administrador. Los roles se pueden definir durante la creación del modelo mediante el Administrador de roles. Una vez implementado un modelo, puede administrar roles mediante SQL Server Management Studio (SSMS). más información, consulte toolearn [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).
  
> [!NOTE]  
> Creación de funciones es toocomplete no es necesario en este tutorial. De forma predeterminada, cuenta de hello que ha iniciado sesión con tiene privilegios de administrador en el modelo de Hola. Sin embargo, para otros usuarios en su toobrowse de organización mediante el uso de un cliente de informes, debe crear al menos un rol con lectura permisos y agregar los usuarios como miembros.  
  
Se crean tres roles:  
  
-   **Director de ventas** : este rol puede incluir a los usuarios de su organización para la que desea que objetos de modelo de tooall de permiso de lectura de toohave y los datos.  
  
-   **Analista de ventas EE. UU.** : este rol puede incluir a los usuarios de su organización para la que desea que sólo toobe toobrowse capaz de datos relacionados con toosales Hola Estados Unidos. Para este rol, use un toodefine de fórmulas de DAX un *filtro de fila*, lo que restringe los miembros toobrowse únicamente los datos de hello Estados Unidos.  
  
-   **Administrador** : este rol puede incluir a los usuarios para el que desea que los permisos de administrador de toohave, lo que permite acceso ilimitado y permisos de las tareas administrativas de tooperform en la base de datos de modelo de Hola.  
  
Dado que las cuentas de usuario y de grupo de Windows de su organización son únicas, puede agregar cuentas de su propia organización toomembers. Sin embargo, para este tutorial, también puede dejar a los miembros de hello en blanco. Probar el efecto Hola de cada rol más adelante en la lección 12: analizar en Excel.  
  
Estimado toocomplete de tiempo en esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 10: crear particiones](../tutorials/aas-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Creación de roles  
  
#### <a name="toocreate-a-sales-manager-user-role"></a>toocreate un rol de usuario de administrador de ventas  
  
1.  En el Explorador de modelos tabulares, haga clic con el botón derecho en **Roles** > **Roles**.  
  
2.  En el Administrador de roles, haga clic en **Nuevo**.  
  
3.  Haga clic en nuevo rol de hello y, a continuación, en hello **nombre** columna, cambie el nombre de rol de hello demasiado**Sales Manager**.  
  
4.  Hola **permisos** columna, haga clic en la lista desplegable de hello y, a continuación, seleccione hello **lectura** permiso. 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  Opcional: Haga clic en hello **miembros** ficha y, a continuación, haga clic en **agregar**. Hola **Seleccionar usuarios o grupos** diálogo cuadro, escriba Hola Windows usuarios o grupos de su organización desea tooinclude en función de Hola.  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a>toocreate un rol de usuario analista de ventas EE. UU.  
  
1.  En el Administrador de roles, haga clic en **Nuevo**.    
  
2.  Cambiar el nombre de rol de hello demasiado**analista de ventas EE. UU.**.  
  
3.  Asigne a este rol el permiso **Lectura**.  
  
4.  Haga clic en la pestaña Filtros de fila de hello y, a continuación, para hello **DimGeography** tabla solo, en una columna de filtro de DAX hello, Hola de tipo siguiente fórmula:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Fórmula de un filtro de fila debe resolver el valor de un valor booleano (verdadero/falso) tooa. Con esta fórmula, se especifica que sólo las filas con valor de código de región del país hello de "US" están usuario de toohello visible.  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  Opcional: Haga clic en hello **miembros** ficha y, a continuación, haga clic en **agregar**. Hola **Seleccionar usuarios o grupos** diálogo cuadro, escriba Hola Windows usuarios o grupos de su organización desea tooinclude en función de Hola.  
  
#### <a name="toocreate-an-administrator-user-role"></a>toocreate un rol de usuario de administrador  
  
1.  Haga clic en **Nuevo**.  
  
2.  Cambiar el nombre de rol de hello demasiado**administrador**.  
  
3.  Asigne a este rol el permiso **Administrador**.  
  
4.  Opcional: Haga clic en hello **miembros** ficha y, a continuación, haga clic en **agregar**. Hola **Seleccionar usuarios o grupos** diálogo cuadro, escriba Hola Windows usuarios o grupos de su organización desea tooinclude en función de Hola. 
  
  
## <a name="whats-next"></a>Pasos siguientes
[Lección 12: Analizar en Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)

  
  
