# Convolutional Neural Network (CNN)

<p align="center">
    <img src="contents/overview cnn.ppm" alt="overview cnn" width="480" style="vertical-align:middle">
</p>

## Input + Convolution Backbone

### Convolution Layer

Convolution → Ektraksi Ciri (Feature Extraction)

<p align="center">
    <img src="contents/convolution.gif" alt="convolution" width="360" style="vertical-align:left">
    <img src="contents/convolution.png" alt="convolution" width="640" style="vertical-align:right">
</p>

```
tf.keras.layers.Conv2D(
    filters,
    kernel_size,
    strides=(1, 1),
    padding='valid',
    activation=None,
    input_shape=(height, width, channel)
)
```

- filters → dimensi ruang output → jumlah filter output dalam konvolusi
- kernel_size → ukuran spasial dari filter (lebar/tinggi)
- stride → besar pergeseran filter dalam konvolusi
- padding → jumlah penambahan nol pada gambar
    - valid → tidak ada padding
    - same → padding nol merata kiri/kanan/atas/bawah
- activation → fungsi aktivasi untuk digunakan
- input_shape → input gambar

### Pooling Layer

Pooling → downsampling / mengurangi dimensi → menyimpan informasi penting

<p align="center">
    <img src="contents/pooling.png" alt="pooling" width="640" style="vertical align:middle">
</p>

```
tf.keras.layers.MaxPool2D(
    pool_size=(2, 2),
    strides=None,
    padding='valid',
)
```

- pool_size → ukuran pool
- strides → besar pergeseran
- padding → jumlah penambahan nol pada gambar
    - valid → tidak ada padding
    - same → padding nol merata kiri/kanan/atas/bawah

## Classifier Head (ANN)

### Flatten dan Global Average Pooling

Flatten dan Global Average Pooling → input layer

<p align="center">
    <img src="contents/fully connected layer vs global average pooling.png" alt="fully connected layer vs global average pooling" width="640" style="vertical align:middle">
</p>

|   Fully Connected Layer    |    Global Average Pooling                |
|            ---             |                       ---                |
|      hxwxd (1 dimension)   |               d (1 dimension)            |
| tf.keras.layers.Flatten()  | tf.keras.layers.GlobalAveragePooling2D() |

### Hidden Layer

  ```
    tf.keras.layers.Dense(units, activation=None)
  ```
  - units → dimensi ruang output
  - activation → fungsi aktivasi untuk digunakan → relu
  
  Dropout → proses mencegah terjadinya overfitting dan juga mempercepat proses learning.
  
  <p align="center">
    <img src="contents/dropout.jpg" alt="dropout" width="640" style="vertical-align:middle">
  </p>
  
  ```
  tf.keras.layers.Dropout(rate)
  ```
  
### Output Layer

  ```
    tf.keras.layers.Dense(units, activation=None)
  ```
  - units → dimensi ruang output
  - activation → fungsi aktivasi untuk digunakan

    | activation  | output/class mode | loss function | 
    |     ---     |        ---        |     ---       |
    |   sigmoid   |      binary       |  binary_crossentropy → 0/1 |
    |   softmax   |   categorical     |     categorical_crossentropy → [1 0 0] |
    |   softmax   |   categorical     |  sparse_categorical_crossentropy → [1] |
