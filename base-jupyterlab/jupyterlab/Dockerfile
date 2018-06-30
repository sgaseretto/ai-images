FROM python:3

WORKDIR /jup

RUN pip install jupyter -U && pip install jupyterlab

EXPOSE 8888

# ENTRYPOINT ["jupyter", "lab","--ip=0.0.0.0","--allow-root"]
# CMD jupyter lab --ip=* --port=8888 --no-browser --notebook-dir=/opt/app/data --allow-root
CMD jupyter lab --ip=* --port=8888 --no-browser --allow-root
