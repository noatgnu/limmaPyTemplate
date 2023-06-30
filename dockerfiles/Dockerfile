FROM python:3.9
LABEL maintainer="tphung001@dundee.ac.uk"

LABEL \
      org.label-schema.name="dQ" \
      org.label-schema.description="Docker container for dQ" \
      org.label-schema.version="$DOCKER_IMAGE_VERSION" \
      org.label-schema.vcs-url="https://github.com/noatgnu/dQ" \
      org.label-schema.schema-version="1.0"

EXPOSE 8888
RUN mkdir /app
RUN mkdir /app/src
RUN mkdir /app/data

WORKDIR /app/src

RUN apt-get update
RUN apt-get upgrade -y

RUN pip install jupyter jupyterlab

RUN apt-get install libharfbuzz-dev  libfribidi-dev -y
RUN apt-get install -y --no-install-recommends r-base r-base-dev && rm -rf /var/lib/apt/lists/*
RUN R -e 'install.packages("devtools")'
RUN R -e "install.packages('BiocManager',dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages(c('remotes', 'dplyr', 'ggplot2'))"
RUN R -e "library('BiocManager');BiocManager::install('limma')"
#RUN R -e "remotes::install_github('PNNL-Comp-Mass-Spec/MSnSet.utils')"
RUN R -e 'install.packages("languageserver")'
RUN R -e 'install.packages("arrow")'
RUN R -e "install.packages(c('repr', 'IRdisplay','evaluate', 'crayon','pbdZMQ','uuid', 'digest', 'IRkernel'))"
RUN R -e "IRkernel::installspec()"
RUN pip install rpy2-arrow
RUN pip install jupyterlab-lsp
RUN pip install pandas statsmodels scikit-learn matplotlib seaborn missingpy


EXPOSE 8888

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--allow-root", "--no-browser"]