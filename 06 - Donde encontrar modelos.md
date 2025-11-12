Existen diversos sitios especializados que funcionan como repositorio de modelos AI, con versiones quantizadas para su uso en Edge Devices, para este workshop proponemos tres plataformas:

- [Kaggle](https://www.kaggle.com/models?framework=tfLite)
- [HuggingFace](https://huggingface.co)
- [TensorFlow Model Gardener](https://github.com/tensorflow/models)

## ¿Qué hacer si no se encuentra un modelo compatible?

En el caso de encontrar un modelo TensorFlow que se ajusta a nuestro caso de uso, es posible [convertir modelos](https://ai.google.dev/edge/litert/models/convert#model_conversion) a un formato TensorFlow Lite (no está en el alcance del WorkShop)

Puedes seguir este [Colab](https://colab.research.google.com/github/tensorflow/examples/blob/master/lite/codelabs/digit_classifier/ml/step2_train_ml_model.ipynb), donde se muestra el proceso de entrenamiento y de data augmentation para el modelo de reconocimiento de dígitos escritos a mano
