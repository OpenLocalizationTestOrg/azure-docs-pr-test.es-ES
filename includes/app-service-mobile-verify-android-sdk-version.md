Debido a desarrollo continuo, versión de SDK de Android Hola instalada en Android Studio podría no coincidir versión hello en el código de hello. Hola Android SDK que se hace referencia en este tutorial es Hola 23, versión más reciente en el momento de Hola de escritura. número de versión de Hola puede aumentar a medida que nuevas versiones de hello SDK aparecen y se recomienda usar la versión más reciente de hello disponible.

Dos síntomas de error de coincidencia de la versión son los siguientes:

- Al generar o volver a generar el proyecto de hello, pueda recibir mensajes de error de Gradle como "**no se pudo toofind destino Google Inc.:Google APIs:n**".
- Los objetos de Android estándar del código que deben resolverse según las instrucciones `import` pueden generar mensajes de error.

Si aparece cualquiera de estos, versión de Hola de hello Android SDK instalado en Android Studio podría no coincidir Hola SDK destino Hola Descargar proyecto. versión de hello tooverify, que Hola siguientes cambios:

1. En Android Studio, haga clic en **Herramientas** > **Android** > **Administrador de SDK**. Si no ha instalado la versión más reciente de Hola de hello Platform SDK, a continuación, haga clic en tooinstall se. Tome nota del número de versión de Hola.
2. En hello **el Explorador de proyectos** ficha **secuencias de comandos de Gradle**, abra archivo hello **build.gradle (modeule: aplicación)**. Asegúrese de que hello **compileSdkVersion** y **buildToolsVersion** se establecen toohello última versión del SDK instalado. etiquetas de Hello podrían tener este aspecto:

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. En hello, Android Studio Explorador de proyectos, nodo de proyecto de Hola de menú contextual, elija **propiedades**y en la columna izquierda de hello, elija **Android**. Asegúrese de que hello **destino de compilación del proyecto** se establece toohello misma versión SDK que hello **targetSdkVersion**.

En Android Studio, archivo de manifiesto de hello ya no es destino de Hola de toospecify usado SDK y versión mínima del SDK, a diferencia del caso de hello Eclipse.
