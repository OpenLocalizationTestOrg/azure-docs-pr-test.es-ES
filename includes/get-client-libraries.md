### <a name="install-via-composer"></a>Instalación mediante el compositor
1. [Instalación de Git][install-git] Tenga en cuenta que en Windows, también debe agregar variable de entorno PATH de hello Git tooyour ejecutable. 
2. Cree un archivo denominado **composer.json** en Hola raíz del proyecto y agregue Hola después tooit de código:
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. Descargue **[composer.phar][composer-phar]** en la raíz del proyecto.
4. Abra un símbolo del sistema y ejecute el siguiente comando en la raíz del proyecto de Hola
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
