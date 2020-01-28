ARG BASE_CONTAINER=jupyter/tensorflow-notebook
FROM $BASE_CONTAINER

# Install Packages
RUN pip install --upgrade pip

COPY requirements.txt /tmp/
RUN pip install --requirement /tmp/requirements.txt && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
	
RUN echo "c.NotebookApp.token = ''" >> .jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.password = ''" >> .jupyter/jupyter_notebook_config.py
