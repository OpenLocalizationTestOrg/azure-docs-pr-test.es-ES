Ahora que ha agregado un desencadenador, su toodo tiempo algo interesante con datos de hello generadas por el desencadenador de Hola. Siga estos Hola de tooadd pasos **SharePoint Online - crear archivo** acción. Esta acción creará un archivo en SharePoint Online cada hora Hola nuevo elemento desencadenador se activa. 

tooconfigure Hola esta acción, deberá hello tooprovide siguiente información. Proporcionar esta información, observará que es datos toouse fácil generados por el desencadenador de hello como entrada para algunas de las propiedades de hello para el nuevo archivo de hello:

| Propiedad Crear archivo | Descripción |
| --- | --- |
| Dirección URL del sitio |Se trata de hello URL del sitio de SharePoint Online Hola donde desee toocreate Hola nuevo archivo. Seleccionar sitio de hello en lista de hello presentado. |
| Ruta de acceso a la carpeta |Esto es Hola carpeta (en la dirección URL del sitio seleccionado en el paso anterior de Hola Hola) donde se colocará el nuevo archivo de Hola. Busque y seleccione la carpeta de Hola. |
| Nombre de archivo |Este es el nombre de Hola de archivo hello va a crear. |
| Contenido del archivo |contenido de Hola que se escribirá el archivo toohello. |

1. Seleccione **+ nuevo paso** acción de hello tooadd.  
   ![Imagen 1 de acción de SharePoint Online](./media/connectors-create-api-sharepointonline/action-1.png)  
2. Seleccione hello **agregar una acción** vínculo. Este cuadro de búsqueda de hello abre donde puede buscar cualquier acción desea que tootake. En este ejemplo, nos interesan las acciones de SharePoint.    
   ![Imagen 2 de acción de SharePoint Online](./media/connectors-create-api-sharepointonline/action-2.png)    
3. Escriba *sharepoint* toosearch para acciones relacionadas tooSharePoint.
4. Seleccione **SharePoint Online - crear archivo** como Hola tootake de acción.   **Tenga en cuenta**: será solicitada tooauthorize su tooaccess de aplicación lógica SharePoint cuenta si no ha creado previamente un tooSharePoint de conexión en línea.    
   ![Imagen 3 de acción de SharePoint Online](./media/connectors-create-api-sharepointonline/action-3.png)    
5. Hola **crear archivo** controlar se abre.   
   ![Imagen 4 de acción de SharePoint Online](./media/connectors-create-api-sharepointonline/action-4.png)     
6. Seleccione **dirección URL del sitio** y examinar toofind Hola sitio que desee que el archivo de hello toocreate.     
   ![Imagen 5 de acción de SharePoint Online](./media/connectors-create-api-sharepointonline/action-5.png)  
7. Seleccione **ruta de acceso de carpeta** y examinar las carpetas hello toofind donde se colocará el nuevo archivo de Hola.  
   ![Imagen 6 de acción de SharePoint Online](./media/connectors-create-api-sharepointonline/action-6.png)  
8. Hola seleccione **nombre de archivo** controlar y escriba Hola nombre de archivo hello desea toocreate. En este caso, puede escribir el nombre del archivo de hello directamente o puede usar cualquiera de las propiedades de Hola de desencadenador de Hola que creó anteriormente. Para ello, seleccione Propiedades de lista de Hola de **salidas de cuando se crea un nuevo elemento**. Esta lista es la única pantalla después de seleccionar hello **nombre de archivo** control. En este tutorial, seleccioné identificador (Id. de Hola de nuevo elemento de lista hello) como nombre de hello del archivo hello creando hello **SharePoint Online - crear archivo** acción.    
   ![Imagen 7 de acción de SharePoint Online](./media/connectors-create-api-sharepointonline/action-7.png)  
9. Seleccione hello **el contenido del archivo** controlar y escriba el contenido de Hola que se escribirá el archivo toohello que se va a crear. Para el contenido del archivo de hello, tenga en cuenta que puede utilizar cualquiera de las propiedades de Hola de desencadenador de Hola que creó anteriormente. Simplemente seleccione Propiedades de hello en lista de hello presentado. O bien, puede especificar hello **el contenido del archivo** texto directamente en el control de Hola. En este ejemplo, se han seleccionado algunas propiedades y se han agregado espacios y un guión entre cada propiedad.        
   ![Imagen 8 de acción de SharePoint Online](./media/connectors-create-api-sharepointonline/action-8.png)  
10. Guardar el flujo de trabajo de hello cambios tooyour  
11. Enhorabuena, ahora tiene una aplicación totalmente funcional lógica que se desencadena cuando se agrega un nuevo elemento lista de SharePoint Online tooa. aplicación Hello, a continuación, creará un archivo, usar algunas de las propiedades de Hola Hola nuevo elemento de lista.  Ahora puede probar mediante la creación de un nuevo elemento de lista de SharePoint de Hola. 

