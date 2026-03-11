![Banner](./docs/images/banner.png)

<div align="center">
  <div align="center">

[![Stars](https://img.shields.io/github/stars/aws-containers/retail-store-sample-app)](Stars)
![GitHub License](https://img.shields.io/github/license/aws-containers/retail-store-sample-app?color=green)
![Dynamic JSON Badge](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fraw.githubusercontent.com%2Faws-containers%2Fretail-store-sample-app%2Frefs%2Fheads%2Fmain%2F.release-please-manifest.json&query=%24%5B%22.%22%5D&label=release)
![GitHub Release Date](https://img.shields.io/github/release-date/aws-containers/retail-store-sample-app)

  </div>

  <strong>
  <h2>AWS Containers Retail Sample</h2>
  </strong>
</div>

This is a sample application designed to illustrate various concepts related to containers on AWS. It presents a sample retail store application including a product catalog, shopping cart and checkout.

It provides:

- A demo store-front application with themes, pages to show container and application topology information, generative AI chat bot and utility functions for experimentation and demos.
- An optional distributed component architecture using various languages and frameworks
- A variety of different persistence backends for the various components like MariaDB (or MySQL), DynamoDB and Redis
- The ability to run in different container orchestration technologies like Docker Compose, Kubernetes etc.
- Pre-built container images for both x86-64 and ARM64 CPU architectures
- All components instrumented for Prometheus metrics and OpenTelemetry OTLP tracing
- Support for Istio on Kubernetes
- Load generator which exercises all of the infrastructure

See the [features documentation](./docs/features.md) for more information.

**This project is intended for educational purposes only and not for production use**

![Screenshot](/docs/images/screenshot.png)

## Application Architecture

The application has been deliberately over-engineered to generate multiple de-coupled components. These components generally have different infrastructure dependencies, and may support multiple "backends" (example: Carts service supports MongoDB or DynamoDB).

![Architecture](/docs/images/architecture.png)

| Component                  | Language | Container Image                                                             | Helm Chart                                                                        | Description                             |
| -------------------------- | -------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------- |
| [UI](./src/ui/)            | Java     | [Link](https://gallery.ecr.aws/aws-containers/retail-store-sample-ui)       | [Link](https://gallery.ecr.aws/aws-containers/retail-store-sample-ui-chart)       | Store user interface                    |
| [Catalog](./src/catalog/)  | Go       | [Link](https://gallery.ecr.aws/aws-containers/retail-store-sample-catalog)  | [Link](https://gallery.ecr.aws/aws-containers/retail-store-sample-catalog-chart)  | Product catalog API                     |
| [Cart](./src/cart/)        | Java     | [Link](https://gallery.ecr.aws/aws-containers/retail-store-sample-cart)     | [Link](https://gallery.ecr.aws/aws-containers/retail-store-sample-cart-chart)     | User shopping carts API                 |
| [Orders](./src/orders)     | Java     | [Link](https://gallery.ecr.aws/aws-containers/retail-store-sample-orders)   | [Link](https://gallery.ecr.aws/aws-containers/retail-store-sample-orders-chart)   | User orders API                         |
| [Checkout](./src/checkout) | Node     | [Link](https://gallery.ecr.aws/aws-containers/retail-store-sample-checkout) | [Link](https://gallery.ecr.aws/aws-containers/retail-store-sample-checkout-chart) | API to orchestrate the checkout process |

## Quickstart

The following sections provide quickstart instructions for various platforms.

### Docker

This deployment method will run the application as a single container on your local machine using `docker`.

Pre-requisites:

- Docker installed locally

Run the container:

```
docker run -it --rm -p 8888:8080 public.ecr.aws/aws-containers/retail-store-sample-ui:1.0.0
```

Open the frontend in a browser window:

```
http://localhost:8888
```

To stop the container in `docker` use Ctrl+C.

### Docker Compose

This deployment method will run the application on your local machine using `docker-compose`.

Pre-requisites:

- Docker installed locally

Download the latest Docker Compose file and use `docker compose` to run the application containers:

```
wget https://github.com/aws-containers/retail-store-sample-app/releases/latest/download/docker-compose.yaml

DB_PASSWORD='<some password>' docker compose --file docker-compose.yaml up
```

Open the frontend in a browser window:

```
http://localhost:8888
```

To stop the containers in `docker compose` use Ctrl+C. To delete all the containers and related resources run:

```
docker compose -f docker-compose.yaml down
```

