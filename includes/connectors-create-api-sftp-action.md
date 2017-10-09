Ahora que ha agregado un desencadenador, su toodo tiempo algo interesante con datos de hello generadas por el desencadenador de Hola. Siga estos tooadd pasos un hello **SFTP - carpeta de extracción** acción. Esta acción extraerá el contenido de Hola de un archivo si se cumplen las condiciones de hello definidas. 

tooconfigure Hola esta acción, deberá hello tooprovide siguiente información. Observará que resulta datos toouse fácil generados por el desencadenador de hello como entrada para algunas de las propiedades de hello para el nuevo archivo de hello:

| SFTP - extract folder property (SFTP: extraer propiedad de carpeta) | Descripción |
| --- | --- |
| Ruta de acceso del archivo de origen |Se trata de ruta de acceso de hello para el archivo hello se extraen. Puede seleccionar uno de los tokens de Hola desde una acción anterior o examinar ruta de archivo de hello SFTP server toofind Hola. |
| Ruta de acceso a la carpeta de destino |Se trata de ruta de acceso de Hola donde se colocarán los archivos de hello extraído. Puede seleccionar uno de los tokens de Hola de una acción anterior como ruta de acceso de destino de Hola o examinar el servidor SFTP de Hola y seleccione una ruta de acceso. |
| ¿Sobrescribir? |Indica si un archivo con hello mismo nombre de archivo extraído de Hola se encuentra en la ruta de acceso de carpeta de destino de hello si se deben sobrescribir archivos existentes de Hola o no. |

Vamos a empezar a agregar archivos de Hola de tooextract de acción de hello si condición Hola definido anteriormente, se evalúa como demasiado*True*. 

1. Seleccione **Add an action**(Agregar una acción).        
   ![Imagen 6 de condición de acción de SFTP](./media/connectors-create-api-sftp/condition-6.png)   
2. Seleccione hello **SFTP - carpeta de extracción** acción      
   ![Imagen 7 de condición de acción de SFTP](./media/connectors-create-api-sftp/condition-7.png)   
3. Seleccione **Ruta de acceso del archivo de origen**            .  
   ![Imagen 9 de condición de acción de SFTP](./media/connectors-create-api-sftp/condition-9.png)   
4. Seleccione hello **ruta de acceso del archivo** símbolo (token). Esto indica que se usará la ruta de acceso de archivo de hello del archivo de Hola que Hola desencadenador encuentra como ruta de acceso de archivo de archivo de origen de Hola.           
   ![Imagen 10 de condición de acción de SFTP](./media/connectors-create-api-sftp/condition-10.png)   
5. Seleccione **Ruta de acceso de la carpeta de destino**         .  
   ![Imagen 11 de condición de acción de SFTP](./media/connectors-create-api-sftp/condition-11.png)   
6. Seleccione hello **ruta de acceso del archivo** símbolo (token). Esto indica que se usará la ruta de acceso de archivo de hello del archivo de Hola que Hola desencadenador encontró como ruta de acceso de destino de Hola para hello extraer archivos.   
7. Escriba *\ExtractedFile* en hello **ruta de acceso de carpeta de destino** control. Ello justo después del token de ruta de acceso de archivo Hola Hola control de ruta de acceso de carpeta de destino.         
   ![Imagen 12 de condición de acción de SFTP](./media/connectors-create-api-sftp/condition-12.png)   
8. Escriba *True* Hola **sobrescribir?* tooindicate de control que se deben sobrescribir archivos existentes si tienen Hola mismo nombre como Hola extrajo los archivos.      
   ![Imagen 13 de condición de acción de SFTP](./media/connectors-create-api-sftp/condition-13.png)   
9. Guardar el flujo de trabajo de hello cambios tooyour  

