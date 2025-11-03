Ahora que tenemos cargado el modelo, y las respectivas dependencias al proyecto, podremos asignar espacio en memoria para los tensores input/output, formatear data para ser usada por el modelo, y correr la inferencia.

## `DigitClassifier.kt`

Esta clase es la encargada de cargar el modelo, los tensores y ejecutar la inferencia.

```kotlin
class DigitClassifier(
	private val context: Context
) {
	fun classify(bitmap: Bitmap) {}
	
	fun classifyAsync(bitmap: Bitmap) {}
	
	companion object {  
	    private const val MODEL_NAME = "mnist.tflite"  
	    const val INPUT_WIDTH = 28  
	    const val INPUT_HEIGHT = 28  
	}
}

```

1. Carga de modelo y procesador de imagen según input requerido del modelo (imagen blanco y negro de 28x28), lo usaremos más tarde para procesar la imagen cargada en el tensor

```kotlin
class DigitClassifier(
	private val context: Context
) {
	private val model: Mnist.newInstance(context)
	private val inputImageProcessor: ImageProcessor = ImageProcessor.Builder()
		.add(ResizeOp(INPUT_HEIGHT, INPUT_WIDHT, ResizeOp.ResizeMethod.BILINEAR))
		.add(TransformToGrayscaleOp())
		.add(NormalizeOp(0.0f, 255.0f))
		.build()
		
	// ...
}
```

2. Definir Tensor (input) y cargamos data a ser procesada

```kotlin
class DigitClassifier(
	private val context: Context
) {
	// ...
	
	fun classify(bitmap: Bitmap): String {
		// Allocate tensor (input data)
		// As data on the tensor we're using FLOAT numbers
		// to represent the Image as input data
		val tensorImage = TensorImage(DataType.FLOAT32)
		
		// Load bitmap to the tensor
		tensorImage.load(bitmap)
	}
}

```

3. Procesamos data para ser pasada al modelo, y luego procesamos la data con el modelo
```kotlin
class DigitClassifier(
	private val context: Context
) {
	// ...
	
	fun classify(bitmap: Bitmap): String {
		// Allocate tensor (input data)
		// As data on the tensor we're using FLOAT numbers
		// to represent the Image as input data
		val tensorImage = TensorImage(DataType.FLOAT32)
		
		// Load bitmap to the tensor
		tensorImage.load(bitmap)
		
		// Image Procesing to be used by model
		val processedImage = inputImageProcessor.process(tensorImage)
		
		// model process
		val outputs = model.process(processedImage.tensorBuffer)
		val outputFeature0 = outputs.outputFeature0AsTensorBuffer // provided by Mnist model API and LiteRT Support Library
	}
}

```

4. Una vez que tenemos el output (predicción del modelo) debemos procesar la información de manera que tenga sentido en el contexto de la aplicación

```kotlin
class DigitClassifier(
	private val context: Context
) {
	// ...
	
	fun classify(bitmap: Bitmap): String {
		// ...
		// model process
		val outputs = model.process(processedImage.tensorBuffer)
		val outputFeature0 = outputs.outputFeature0AsTensorBuffer // provided by Mnist model API and LiteRT Support Library
		
		val probabilities = outputFeature0.floatArray
		// La probabilidad más alta en éste contexto representa el 
		// posible número retornado al ejecutar la inferencia
		val maxProbability = probabilities.maxOrNull()
		if (maxProbability == null) return ""
		
		val predictedDigit = probabilities.indexOfFirst(maxProbability::equals)
		
		return predictedDigit.toString()
		
	}
}

```