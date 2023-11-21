# Use an official miniconda runtime as a parent image
FROM continuumio/miniconda3:latest

# Set the working directory inside the container
WORKDIR /app

# Copy the environment.yml file into the container at /app
COPY environment.yml /app/environment.yml
COPY notebooks /app/notebooks

# Create and activate the conda environment
RUN conda env create -f environment.yml && \
    echo "source activate $(head -1 environment.yml | cut -d' ' -f2)" > ~/.bashrc && \
    /bin/bash -c "source activate $(head -1 environment.yml | cut -d' ' -f2) && \
    python -m ipykernel install --user --name=$(head -1 environment.yml | cut -d' ' -f2) && \
    conda clean -afy"

# Expose the port for Jupyter Lab
EXPOSE 8888

# Start Jupyter Lab upon container launch
CMD ["bash", "-c", "source activate $(head -1 environment.yml | cut -d' ' -f2) && \
    jupyter lab --ip=0.0.0.0 --port=8888 --no-browser --allow-root --NotebookApp.token=''"]
