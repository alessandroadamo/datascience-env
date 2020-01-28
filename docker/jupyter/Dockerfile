ARG BASE_CONTAINER=jupyter/tensorflow-notebook
FROM $BASE_CONTAINER

# Install Packages
RUN pip install --upgrade pip

RUN pip install --quiet \
	minio==5.0.7 && \
	redis==3.3.11 && \
	h5py==2.10.0 && \
	bokeh==1.4.0 && \
	SQLAlchemy==1.3.13
	
RUN pip install --quiet imbalanced-learn==0.6.1 && \
	lightgbm==2.3.1
	
RUN echo "c.NotebookApp.token = ''" >> .jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.password = ''" >> .jupyter/jupyter_notebook_config.py
