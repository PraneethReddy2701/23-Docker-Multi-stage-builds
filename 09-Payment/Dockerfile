FROM python:3.9.23-alpine3.22 AS builder
WORKDIR /opt/server
RUN apk add --no-cache gcc  musl-dev linux-headers python3-dev
COPY payment.ini .
COPY *.py .
COPY requirements.txt .
RUN pip install --no-cache-dir --prefix=/usr/local -r requirements.txt
RUN pip3 install -r requirements.txt

FROM python:3.9.23-alpine3.22
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
USER roboshop
COPY --from=builder /opt/server /opt/server
COPY --from=builder /usr/local /usr/local
CMD ["uwsgi", "--ini", "payment.ini"]