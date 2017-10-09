Ahora que ha agregado una condición, su toodo tiempo algo interesante con datos de hello generadas por el desencadenador de Hola. Siga estos Hola de tooadd pasos **Salesforce - obtener el objeto** acción. Esta acción obtendrá los datos de hello cada vez que se crea un nuevo cliente potencial. También agregará una segunda acción que va a usar datos de Hola de hello Salesforce - Get un toosend de acción de objeto un correo electrónico mediante el conector de hello Office 365.  

tooconfigure Hola esta acción, deberá hello tooprovide siguiente información. Observará que resulta datos toouse fácil generados por el desencadenador de hello como entrada para algunas de las propiedades de hello para el nuevo archivo de hello:

| Propiedad Crear archivo | Description |
| --- | --- |
| Tipo de objeto |Se trata de tipo hello del objeto de Salesforce que le interesen. Algunos ejemplos son clientes potenciales, cuentas, etc. |
| Id. de objeto |Representa un identificador de objeto de Hola. |

1. Seleccione el vínculo **Add an action** (Agregar una acción). Este cuadro de búsqueda de hello abre donde puede buscar cualquier acción desea que tootake. En este ejemplo, nos interesan las acciones de Salesforce.      
   ![Imagen 1 de acción de Salesforce](./media/connectors-create-api-salesforce/action-1.png)  
2. Escriba *salesforce* toosearch para acciones relacionadas toosalesforce.
3. Seleccione **Salesforce - obtener el objeto** como Hola tootake de acción.   **Tenga en cuenta**: será solicitada tooauthorize su tooaccess de aplicación lógica su Salesforce cuenta si aún no lo hecho previamente.    
   ![Imagen 2 de acción de Salesforce](./media/connectors-create-api-salesforce/action-2.png)    
4. Hola **obtener el objeto** controlar se abre.  
5. Seleccione *provocar* como tipo de objeto de Hola.
6. Seleccione hello **Id. de objeto** control.
7. Seleccione **...**  tooexpand lista de Hola de tokens que puede utilizarse como entrada para las acciones.       
   ![Imagen 3 de acción de Salesforce](./media/connectors-create-api-salesforce/action-3.png)    
8. Seleccione **Lead ID** (Id. de cliente potencial); el control se abre.   
   ![Imagen 4 de acción de Salesforce](./media/connectors-create-api-salesforce/action-4.png)     
9. Observa que ese token de identificador del cliente potencial Hola ahora está en hello control de Id. de objeto, que indica que Hola Get acción objeto buscará un cliente potencial con un identificador que es el Id. de cliente potencial de toohello igual de clientes potenciales que desencadenó esta aplicación lógica.  
   ![Imagen 5 de acción de Salesforce](./media/connectors-create-api-salesforce/action-5.png)  
10. Guarde el trabajo. ¡Eso es todo, ha agregado la aplicación lógica de tooyour de acción de objeto de hello Get. El control Get object (Obtener objeto) debe tener este aspecto:     
    ![Imagen 6 de acción de Salesforce](./media/connectors-create-api-salesforce/action-6.png)  

Ahora que ha agregado un tooget acción un cliente potencial, puede que desee toodo algo interesante con cliente potencial de hello recién creado. En una empresa, puede que desee toosend un toonotify de correo electrónico una lista de distribución que se ha creado un nuevo cliente potencial. Vamos a usar Office 365 Hola conector toosend un correo electrónico con algunos información relevante de Hola de nuevo objeto de cliente potencial hello en Salesforce.  

1. Seleccione **agregar una acción** , a continuación, escriba *correo electrónico* en control de búsqueda de Hola. Esto filtra Hola acciones toothose toosending relacionado y recibir correo electrónico.  
2. Seleccione hello **Office 365 Outlook - envíe un correo electrónico** elemento de la lista. Si no ha creado ya un *conexión* tooyour cuenta de Office 365, que se van a ser solicitada tooenter su toocreate de credenciales de Office 365 TI ahora. Cuando termine, Hola **enviar un correo electrónico** controlar se abre.        
   ![Imagen 7 de acción de Salesforce](./media/connectors-create-api-salesforce/action-7.png)  
3. Escriba la dirección de correo electrónico de Hola que desearía Hola de tooin de correo electrónico de toosend **a** control.
4. Hola **asunto** de control, escriba *nuevo cliente potencial creado* : seleccione esta opción, a continuación, hello *empresa* símbolo (token). Esto mostrará hello *empresa* campo de hello nuevo cliente potencial creada en Salesforce.  
5. Hola **cuerpo** (control), puede seleccionar cualquiera de los tokens de Hola de hello nuevo responsable del objeto y puede escribir cualquier texto que desea toodisplay en cuerpo Hola de Hola correo electrónico. Este es un ejemplo:  
   ![Imagen 8 de acción de Salesforce](./media/connectors-create-api-salesforce/action-8.png)   
6. Guarde el flujo de trabajo.  

Eso es todo. Ahora la aplicación lógica está completa.  

Ahora, puede probar la aplicación lógica: en Salesforce, cree un nuevo cliente potencial que cumpla la condición de Hola que creó.  Si ha seguido completamente este tutorial, solo tiene que crear un cliente potencial con una dirección de correo electrónico que contenga *amazon.com*. Después de unos segundos debe activarse la aplicación lógica y resultados de hello pueden parecer toothis similar:  
![Imagen 9 de acción de Salesforce](./media/connectors-create-api-salesforce/action-9.png)  

