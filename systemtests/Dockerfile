FROM python:3.7-alpine3.10 as builder

RUN apk add --no-cache gettext
RUN pip3 install wheel

COPY requirements.txt /tmp/requirements.txt
RUN pip wheel -w /wheelhouse -r /tmp/requirements.txt

FROM python:3.7-alpine3.10

COPY --from=builder /wheelhouse /wheelhouse
COPY requirements.txt /tmp/requirements.txt

RUN pip install -r /tmp/requirements.txt --no-index --find-links /wheelhouse

COPY . /systemtests
WORKDIR /systemtests

ENTRYPOINT ["py.test", "-c", "pytest.cfg"]
