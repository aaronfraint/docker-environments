########################################################################
# GIS-data-science-stack Dockerfile
########################################################################

FROM continuumio/miniconda3
LABEL maintainer="Aaron Fraint <aaronfraint@altaplanning.com>"
LABEL url="https://altaplanning.com/services/analytics/"
LABEL description="Python environment for spatial data science work"

# configure conda and install packages in one RUN to keep image tidy
RUN conda config --set show_channel_urls true && \
	  conda config --set channel_priority strict && \
    conda config --prepend channels plotly && \
    conda config --prepend channels conda-forge && \
    conda update --yes -n base conda && \
    conda install --update-all --force-reinstall --yes jupyterlab osmnx pyproj=1.9.6 python-igraph pandana geoalchemy2 psycopg2 xlrd xlsxwriter seaborn plotly_express jupytext && \
    python -m ipykernel install --name alta --display-name "Python (alta)" && \
    conda clean --all --yes && \
    conda info --all && \
    conda list

# launch jupyter in the local working directory that we mount
WORKDIR /home/jovyan/work

# set default command to launch when container is run
CMD ["jupyter", "lab", "--ip='0.0.0.0'", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''"]

# to test, import OSMnx and print its version
RUN ipython -c "import osmnx; print(osmnx.__version__)"
