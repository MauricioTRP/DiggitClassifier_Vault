Para trabajar en éste Workshop usaremos el siguiente [repositorio GitHub](https://github.com/MauricioTRP/DigitClassifier_Example) con código boilerplate que nos facilitará el trabajo.

Para ejecutar modelos TensorFlow Lite en una aplicación Android, es necesario implementar las siguientes dependencias: 

## libs.versions.toml

```toml
[versions]
# ... other versions
tensorFlowLite = "2.17.0"
litert = "1.4.0"

[libraries]
tensorflow-lite = { group = "org.tensorflow", name = "tensorflow-lite", version.ref = "tensorFlowLite" }
litert-support = { group = "com.google.ai.edge.litert", name = "litert-support", version.ref = "litert" }
litert-gpu = { group = "com.google.ai.edge.litert", name = "litert-gpu", version.ref = "litert" }

```

## build.gradle.kts (:app)

```kotlin
dependencies {
	// other dependencies
	implementation(libs.tensorflow.lite)
	implementation(libs.litert.support)
	implementation(libs.litert.gpu)
}
```

## Importación del modelo:

Android Studio Narwhal y Android Studio Otter permite importar modelos TensorFlow Lite, a la vez que configura las dependencias necesarias para revisar la documentación del modelo.

1. File > New

![[Screenshot 2025-11-03 at 2.34.21 AM.png]]

 Other > TensorFlow Lite Model
![[Screenshot 2025-11-03 at 2.33.46 AM.png]]

Buscamos en nuestro sistema de archivos el modelo que queremos importar, 
y marcamos la opción "add TensorFlo Lite GPU dependencies"

![[Screenshot 2025-11-03 at 2.36.36 AM.png]]

Ahora encontrarás una nueva carpeta ml, con el modelo. 

![[Screenshot 2025-11-03 at 2.38.22 AM.png]]

Una vez que se indexen las nuevas dependencias, encontrarás documentación del modelo a travez de la meta data que este tiene:
![[Screenshot 2025-11-03 at 2.39.37 AM.png]]


En caso de problemas con las dependencias agregadas, se pueden buscar las versiones en Maven

https://central.sonatype.com/artifact/org.tensorflow/tensorflow-lite-gpu?smo=true