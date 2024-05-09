FROM nvcr.io/nvidia/pytorch:24.04-py3

ENV DEBIAN_FRONTEND=noninteractive \
    PIP_PREFER_BINARY=1 \
    DEBCONF_NOWARNINGS=yes
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update \
    && apt-get -y upgrade \
    && apt-get install -y \
        poppler-utils \
        libpoppler-dev \
        wget \
        curl \
        git \
        python3-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* /var/tmp/*

WORKDIR /resources

RUN pip install \
        networkx \
        transformers==4.30 \
        sentencepiece \
        pdf2image \
        fastapi[uvicorn] \
        uvicorn \
        PyPDF2 \
        matplotlib \
        timm \
        scipy \
        shapely \
        pyclipper \
        scikit-image \
        python-multipart \
        onnxruntime \
        requests \
        gradio

RUN pip install \
        "git+https://github.com/facebookresearch/detectron2.git"

RUN git clone https://github.com/microsoft/unilm.git /unilm \
        && sed -i 's/from collections import Iterable/from collections.abc import Iterable/' \
        /unilm/dit/object_detection/ditod/table_evaluation/data_structure.py

RUN wget https://github.com/adobe-fonts/source-han-serif/raw/release/OTF/Japanese/SourceHanSerif-Light.otf -P /resources/models \
        && mkdir -p /resources/models/unilm \
        && wget "https://huggingface.co/discus0434/publaynet-dit-base/resolve/main/publaynet_dit-b_cascade.pth" -P /resources/models/unilm
