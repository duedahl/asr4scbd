FROM pytorch/pytorch:2.7.0-cuda11.8-cudnn9-runtime@sha256:d27c2908f2d3a1fc514e206b2dbcddadc3d843ef5b792b20270f328a576c8c86

RUN pip install transformers==4.51.3
RUN pip install datasets==3.5.0
RUN pip install jiwer==3.1.0
RUN pip install evaluate==0.4.3
RUN pip install accelerate==1.7.0
RUN pip install librosa==0.11.0
RUN pip install wandb==0.19.11
RUN pip install matplotlib==3.10.3
RUN pip install optuna==4.4.0
RUN pip install omegaconf==2.3.0

WORKDIR /home

CMD ["/bin/bash"]