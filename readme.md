# Docker and Python

For this assignment i have created a QR code that will navigate to my home page of github account on scanning.


## Setup
1.  Goto Docker.com and Install docker - [https://www.docker.com/get-started/](here)
2.  Signup for your own Docker account 

## Submission Requirements:

1. QR code for my profile is below mentioned

![QR for git profile](./QRCode_20241107131204.png)

2. the log of successfully creating the QR code below.

![Output log](./image.png)


### Building the Image

```sh
docker build -t qr_creator .
```
This command builds a Docker image named `qr_creator` from the Dockerfile in the current directory (`.`).

### Running the Container with Default Settings
```sh
docker run -d --name qr-run qr_creator
```

Runs your QR code generator application in detached mode (`-d`) with a container named `qr-run`.

### Setting Environment Variables for QR Code Customization

```sh
docker run -d --name qr-run \
  -e QR_DATA_URL='https://github.com/sharonekula/' \
  -e QR_CODE_DIR='qr_codes' \
  -e QR_CODE_FILENAME='profileQR.png' \
  -e FILL_COLOR='black' \
  -e BACK_COLOR='white' \
  qr_creator
```
Customizes the QR code generation settings through environment variables.

### Sharing a Volume for QR Code Output

```sh
docker run -d --name qr-run \
  -v /host/path/for/qr_codes:/app/qr_codes \
  qr_creator
```
Mounts a host directory to the container for storing QR codes.

### Combining Volume Sharing and Environment Variables

```sh
docker run -d --name qr-run \
  -e QR_CODE_DIR='qr_codes' \
  -e FILL_COLOR='black' \
  -e BACK_COLOR='white' \
  -v /host/path/for/qr_codes:/app/qr_codes \
  qr_creator
```

A comprehensive command that configures the QR code settings and mounts volumes for QR codes.

## Setting the arg for the url from the terminal
```sh
docker run -v .:/app qrcode --url https://github.com/sharonekula/
```
This is how you would set the url for the qr code

