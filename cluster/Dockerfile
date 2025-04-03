# syntax=docker/dockerfile:1.4
# amd64 required by occ
FROM --platform=linux/amd64 rayproject/ray:2.44.1-py310-cu121 AS base
ENV PYTHONUNBUFFERED=1

RUN python -m pip install --upgrade pip && \
    conda upgrade -n base -c defaults condA


COPY --chown=ray . .
RUN conda env create -f cluster/conda-env.yaml

RUN conda run -n minimal-example python --version
