# Could not load dynamic library 'cudart64_110.dll'的解决方法

问题本质就是GPU调用问题

tensorflow要调用GPU对程序进行训练, 但是并没有找到相应的驱动文件

## Tensorflow 2.1+

### What's going on?

With the new Tensorflow 2.1 release, the default tensorflow pip package contains both CPU and GPU versions of TF. In previous TF versions, not finding the CUDA libraries would emit an error and raise an exception, while now the library dynamically searches for the correct CUDA version and, if it doesn't find it, emits the warning (The W in the beginning stands for warnings, errors have an E (or F for fatal errors) and falls back to CPU-only mode. In fact, this is also written in the log as an info message right after the warning (do note that if you have a higher minimum log level that the default, you might not see info messages). The full log is (emphasis mine):

> 2020-01-20 12:27:44.554767: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'cudart64_101.dll'; dlerror: cudart64_101.dll not found
>
> 2020-01-20 12:27:44.554964: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.

### Should I worry? How do I fix it?

#### First

> If you don't have a CUDA-enabled GPU on your machine, or if you don't care about not having GPU acceleration, no need to worry. If, on the other hand, you installed tensorflow and wanted GPU acceleration, check your CUDA installation (TF 2.1 requires CUDA **10.1**, *not* 10.2 or 10.0).
>
> If you just want to get rid of the warning, you can [adapt TF's logging level](https://stackoverflow.com/questions/35911252/disable-tensorflow-debugging-information) to suppress warnings, but that might be overkill, as it will silence *all* warnings.

#### second

> To install the prerequisites for GPU support in TensorFlow 2.1:
>
> 1. Install your latest GPU drivers.
> 2. Install CUDA 10.1.
>    - If the CUDA installer reports "you are installing an older driver version", you may wish to choose a custom installation and deselect some components. Indeed, note that software bundled with CUDA including GeForce Experience, PhysX, a Display Driver, and Visual Studio integration are not required by TensorFlow.
>    - Also note that TensorFlow requires a specific version of the CUDA Toolkit unless you build from source; for TensorFlow 2.1 and 2.2, this is currently version 10.1.
> 3. Install cuDNN.
>    1. [Download cuDNN](https://developer.nvidia.com/rdp/cudnn-archive) v7.6.4 for CUDA 10.1. This will require you to sign up to the NVIDIA Developer Program.
>    2. Unzip to a suitable location and add the bin directory to your PATH.
> 4. Install tensorflow by `pip install tensorflow`.
> 5. You [may need to restart your PC](https://stackoverflow.com/a/51112550/604687).

#### third

> In a `conda` environment, this is what solved my problem (I was missing `cudart64-100.dll`:
>
> 1. Downloaded it from [dll-files.com/CUDART64_100.DLL](https://www.dll-files.com/search/?q=CUDART64_100.DLL)
> 2. Put it in my conda environment at `C:\Users\<user>\Anaconda3\envs\<env name>\Library\bin`
>
> That's all it took! You can double check if it's working:
>
> ```py
> import tensorflow as tf
> tf.config.experimental.list_physical_devices('GPU')
> ```

## Tensorflow 1.X or 2.0:

Your CUDA setup is broken, ensure you have the correct version installed.



