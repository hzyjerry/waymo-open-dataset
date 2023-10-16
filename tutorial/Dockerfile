FROM tensorflow/tensorflow:latest-py3

RUN apt-get update && apt-get install -y \
  git build-essential wget vim findutils curl \
  pkg-config zip g++ zlib1g-dev unzip python3 python3-pip

RUN apt-get install -y wget golang npm
# RUN go install https://github.com/bazelbuild/bazelisk@latest
RUN npm install -g @bazel/bazelisk

RUN apt-get update \
    && apt-get install -y wget

RUN pip install jupyter matplotlib jupyter_http_over_ws jupyter_http_over_ws

RUN pip install patchelf==0.17.2.1

RUN git clone https://github.com/hzyjerry/waymo-open-dataset.git waymo-od
WORKDIR /waymo-od/src

EXPOSE 8888

# TODO: npm install bazelisk
# TODO: pip install patchelf
# TODO: disable tests
# TODO: need to move this directory
RUN mv ../tutorial waymo_open_dataset/
RUN waymo_open_dataset/pip_pkg_scripts/build.sh

RUN pip install jupyter notebook
RUN python3 -m ipykernel.kernelspec

CMD ["bash", "-c", "bazel run -c opt //waymo_open_dataset/tutorial:jupyter_kernel"]
