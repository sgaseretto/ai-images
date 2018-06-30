FROM python:alpine

# Install required packages
RUN apk add --update --virtual=.build-dependencies alpine-sdk nodejs ca-certificates musl-dev gcc python-dev make cmake g++ gfortran libpng-dev freetype-dev libxml2-dev libxslt-dev
RUN apk add --update git

# Install Jupyter
RUN pip install jupyter
RUN pip install ipywidgets
RUN jupyter nbextension enable --py widgetsnbextension

# Install JupyterLab
RUN pip install jupyterlab && jupyter serverextension enable --py jupyterlab

# Additional packages for compatability (glibc)
RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub && \
  wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk && \
  wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-i18n-2.23-r3.apk && \
  wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-bin-2.23-r3.apk && \
  apk add --no-cache glibc-2.23-r3.apk glibc-bin-2.23-r3.apk glibc-i18n-2.23-r3.apk && \
  rm "/etc/apk/keys/sgerrand.rsa.pub" && \
  /usr/glibc-compat/bin/localedef --force --inputfile POSIX --charmap UTF-8 C.UTF-8 || true && \
  echo "export LANG=C.UTF-8" > /etc/profile.d/locale.sh && \
  ln -s /usr/include/locale.h /usr/include/xlocale.h

# Optional Clean-up
#  RUN apk del glibc-i18n && \
#  apk del .build-dependencies && \
#  rm glibc-2.23-r3.apk glibc-bin-2.23-r3.apk glibc-i18n-2.23-r3.apk && \
#  rm -rf /var/cache/apk/*

ENV LANG=C.UTF-8

# Install XGBoost library
# RUN git clone --recursive https://github.com/dmlc/xgboost && \
#     cd xgboost && \
#     make -j4 && \
#     cd python-package; python3 setup.py install

RUN pip install --upgrade setuptools
# Install Python Packages & Requirements (Done near end to avoid invalidating cache)
# COPY requirements.txt requirements.txt
# RUN pip install -r requirements.txt

# Basic Data Science and machine learning packages
RUN pip install cython && \
    pip install numpy && \
    pip install pandas && \
    pip install matplotlib && \
    pip install scipy && \
    pip install plotly && \
    pip install folium && \
    pip install seaborn && \
    pip install graphviz && \
    pip install scikit-learn

# Automated Feature Engineering
RUN pip install tsfresh && \
    pip install featuretools

# AutoML
RUN pip install deap && \
    pip install update_checker && \
    pip install tqdm && \
    pip install stopit && \
    pip install tpot

# Model Interpretation
RUN pip install lime

# Server
RUN pip install Flask && \
    pip install Flask_RESTful && \
    pip install requests && \
    pip install gunicorn && \
    pip install dash && \
    pip install dash-renderer && \
    pip install dash-html-components && \
    pip install dash-core-components

# Expose Jupyter port & cmd
EXPOSE 8888
RUN mkdir -p /opt/app/data
CMD jupyter lab --ip=* --port=8888 --no-browser --notebook-dir=/opt/app/data --allow-root