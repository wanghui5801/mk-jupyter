
ARG BASE_IMAGE=quay.io/jupyter/datascience-notebook
FROM $BASE_IMAGE

RUN apt update && apt install -y cmake liblzma-dev lzma lzma-dev libpcre2-dev libbz2-dev zlib1g-dev

RUN mamba install --yes 'jupyterlab_rise' && \
    mamba install --yes -c conda-forge xz igraph && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

RUN mamba create -y -p "${CONDA_DIR}/envs/py38"  python=3.8  ipykernel && \
    mamba create -y -p "${CONDA_DIR}/envs/py39"  python=3.9  ipykernel && \
    mamba create -y -p "${CONDA_DIR}/envs/py310" python=3.10 ipykernel && \
    mamba clean --all -f -y

RUN "${CONDA_DIR}/envs/py38/bin/python"  -m ipykernel install --prefix=/opt/conda  \
        --name "python38"  --display-name "Python 3.8"  && \
    "${CONDA_DIR}/envs/py39/bin/python"  -m ipykernel install --prefix=/opt/conda  \
        --name "python39"  --display-name "Python 3.9"  && \
    "${CONDA_DIR}/envs/py310/bin/python" -m ipykernel install --prefix=/opt/conda  \
        --name "python310" --display-name "Python 3.10"

RUN rm -rf /opt/conda/share/jupyter/kernels/python3

RUN mkdir -p /etc/jupyter && \
    echo "c.KernelSpecManager.ensure_native_kernel = False" \
        >> /etc/jupyter/jupyter_server_config.py

RUN fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER ${NB_UID}
