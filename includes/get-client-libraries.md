### <a name="install-via-composer"></a><span data-ttu-id="c4f17-101">Instalación mediante el compositor</span><span class="sxs-lookup"><span data-stu-id="c4f17-101">Install via Composer</span></span>
1. <span data-ttu-id="c4f17-102">[Instalación de Git][install-git]</span><span class="sxs-lookup"><span data-stu-id="c4f17-102">[Install Git][install-git].</span></span> <span data-ttu-id="c4f17-103">Tenga en cuenta que en Windows, también debe agregar variable de entorno PATH de hello Git tooyour ejecutable.</span><span class="sxs-lookup"><span data-stu-id="c4f17-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="c4f17-104">Cree un archivo denominado **composer.json** en Hola raíz del proyecto y agregue Hola después tooit de código:</span><span class="sxs-lookup"><span data-stu-id="c4f17-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="c4f17-105">Descargue **[composer.phar][composer-phar]** en la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c4f17-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="c4f17-106">Abra un símbolo del sistema y ejecute el siguiente comando en la raíz del proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="c4f17-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
