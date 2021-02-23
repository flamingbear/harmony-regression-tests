FROM continuumio/miniconda3:4.9.2

ARG sub_dir
ARG notebook
ENV env_sub_dir=$sub_dir
ENV env_notebook=$notebook

WORKDIR /root

COPY .netrc .netrc
RUN mkdir ./${sub_dir}
COPY ${sub_dir}/environment-linux-64.conda.lock ./${sub_dir}
RUN ls ${sub_dir}

RUN conda create -n papermill --file ./${sub_dir}/environment-linux-64.conda.lock

ENTRYPOINT export PATH=/opt/conda/envs/papermill/bin:$PATH; mkdir /root/output/${env_sub_dir}; conda activate papermilll; papermill --cwd ${env_sub_dir} ${env_sub_dir}/${env_notebook} /root/output/${env_sub_dir}/Results.ipynb -p harmony_host_url $harmony_host_url
