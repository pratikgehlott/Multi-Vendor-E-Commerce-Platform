# Multi-vendor marketplace backend

[![Buid](https://github.com/phyohtetarkar/marketplace-backend/actions/workflows/build.yml/badge.svg)](https://github.com/phyohtetarkar/marketplace-backend/actions/workflows/build.yml)  [![Buid (Native)](https://github.com/phyohtetarkar/marketplace-backend/actions/workflows/build-native.yml/badge.svg)](https://github.com/phyohtetarkar/marketplace-backend/actions/workflows/build-native.yml)

Multi-vendor e-commerce backend application project developed with [Spring boot](https://spring.io/projects/spring-boot/).

The application's business model is similar to Facebook Pages, where users can create shops and sell products through a subscription model. After users create their shops, an administrator must approve them, and users need to subscribe to a plan to start selling products.

**Features**:
<ul>
	<li>Banners</li>
	<li>
		Catalog
		<ul>
			<li>Categories (Multi-level support)</li>
			<li>Products (Variations support)</li>
		</ul>
	</li>
	<li>Orders</li>
	<li>Shopping cart</li>
	<li>Favorite products</li>
	<li>Vendors | Shops</li>
	<li>Subscription Plans</li>
	<li>Subscription Promo-codes</li>
	<li>Reviews</li>
	<li>Users</li>
</ul>


**Front-end website repository** => [Multi-vendor marketplace website](https://github.com/phyohtetarkar/marketplace-web/)


## Requirement

<ol>
	<li>Java (<b>Java 17</b> OR <b>Java 21</b> if you want to enable virtual thread)</li>
	<li>PostgreSQL</li>
	<li>2C2P Payment Gateway Credentials</li>
	<li>Firebase auth setup</li>
</ol>

## Setup

**This project use Firebase auth as authentication layer. So, you first need to setup firebase auth and manually create one owner account. Or you can use any other authentication providers like AWS Cognito, Auth0 etc., and setup accordingly.**

I use extra YML config files for different active profiles (e.g, dev, staging, prod). Here is example config for `env.development.yml` inside `/marketplace-application/src/main/resources/`

> [!NOTE]
> <b>super-user</b> config is required for owner account initialization.

```yml
app:
  database:
    url: jdbc:postgresql://localhost:5432/marketplace-db
    username: <username>
    password: <password>
  image:
    base-url: (http|https)://<your-domain>/images
    base-path: <image-base-path> # for storing uploaded image (e.g, /var/www/html/images)
  payment:
    merchant-id: <2c2p-merchant-id>
    merchant-sha-key: <2c2p-merchant-sha-key>
    token-request-url: <2c2p-payment-token-request-url>
  firebase:
    api-key: <firebase-api-key>
    jwk-set-uri: https://www.googleapis.com/service_accounts/v1/jwk/securetoken%40system.gserviceaccount.com
    issuer-uri: https://securetoken.google.com/<projectId>
  super-user:
    name: <owner-name>
    email: <owner-email-address> # The one you created from firebase auth
    uid: <firebase-auth-user-uid> # The one you created from firebase auth
  misc:
    website-url: http://localhost:3000 # for payment redirection
    cors-origins: # cors domains for font-end website
      - http://localhost:3000
```

## Build and run

**For JVM build**
```bash
cd marketplace-backend
./mvnw install && ./mvnw spring-boot:run -pl marketplace-application
```

**For native build**
```bash
cd marketplace-backend
./mvnw -Pnative clean package
```

JVM or Native build executable outputs can be found inside `/marketplace-application/target/` directory.

## Frontend rest apis

This backend produces three main API categories:

<ul>
	<li>Admin APIs</li>
	<li>Vendor APIs</li>
	<li>Consumer APIs</li>
</ul>

You can explore api docs via [OpenAPI 3 UI](https://springdoc.org/) path `http://localhost:8080/api-docs-ui`.

> [!NOTE]
> <b>Payment API</b> is only for 2c2p's server-to-server response so that left out from main API categories.

## Architecture

<img src="images/architecture.png">

<br/>
<br/>


## Screenshots

<img src="images/shop-dashboard.png">

<img src="images/product-detail.png">

<img src="images/admin-dashboard.png">


