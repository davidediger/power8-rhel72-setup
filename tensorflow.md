# Install cuDNN
sudo tar -xvf cudnn-8.0-linux-ppc64le-v5.1.tgz -C /usr/local

# Install OpenJDK 1.8
sudo yum install java-1.8.0-openjdk-devel
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH

# Build Bazel
wget https://github.com/bazelbuild/bazel/releases/download/0.4.4/bazel-0.4.4-dist.zip
mkdir bazel
cd bazel
unzip ../bazel-0.4.4-dist.zip
./compile.sh
export PATH=`pwd`/output:$PATH

# Build TensorFlow
git clone --recurse-submodules https://github.com/tensorflow/tensorflow
cd tensorflow/
git checkout v1.0.0
./configure
bazel build -c opt --config=cuda //tensorflow/tools/pip_package:build_pip_package
sudo pip install wheel
./bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
sudo pip install --upgrade /tmp/tensorflow_pkg/tensorflow-1.0.0-cp27-cp27mu-linux_ppc64le.whl



# Resources

https://developer.nvidia.com/cuda-downloads-power8

https://www.ibm.com/developerworks/community/blogs/fe313521-2e95-46f2-817d-44a4f27eba32/entry/Building_TensorFlow_on_OpenPOWER_Linux_Systems?lang=en

http://www.nvidia.com/object/gpu-accelerated-applications-tensorflow-installation.html


