FROM armdocker.rnd.ericsson.se/dockerhub-ericsson-remote/python:3.9-slim

WORKDIR /work-dir
COPY . ./

ENV PIP_INDEX_URL="https://arm.sero.gic.ericsson.se/artifactory/api/pypi/proj-radiosw-pypi-local/simple"
ENV PIP_EXTRA_INDEX_URL="https://arm.sero.gic.ericsson.se/artifactory/api/pypi/pypi-remote/simple"

RUN pip install product-diagnostics-platform==0.1.79

CMD ["pdp", "--proxy-headers", "--forwarded-allow-ips", "'*'", "--host", "0.0.0.0"]
