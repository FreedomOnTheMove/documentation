# Freedom on the Move - AWS Infrastructure Documentation

## CloudFront Content Delivery

The project uses Amazon CloudFront to deliver content globally with low latency. There are five CloudFront distributions configured:

### CloudFront Distributions Overview

1. **E1YHIFGA9Q5QM**
   - **Status:** Enabled
   - **Description:** Legacy Crowdsourcing Application
   - **Type:** Standard
   - **Domain Name:** de7xvyzrci6ce.cloudfront.net
   - **Alternate Domain Names:** crowdsourcing.freedomonthemove.org, app.freedomonthemove.org
   - **Origin:** fotm-legacy-crowdsourcing-app (S3 bucket)

2. **E2VAVZOPSJGR2T**
   - **Status:** Enabled
   - **Description:** Legacy distribution for folks that hotlinked to us.
   - **Type:** Standard
   - **Domain Name:** d1y52jo8xcufpn.cloudfront.net
   - **Alternate Domain Names:** source-materials.freedomonthemove.org
   - **Origin:** assets.freedomonthemove.org (S3 bucket)

3. **E2DPQGVS9OCPVC**
   - **Status:** Enabled
   - **Description:** Not specified
   - **Type:** Standard
   - **Domain Name:** dpcdr1tr05614.cloudfront.net
   - **Alternate Domain Names:** database.freedomonthemove.org
   - **Origin:** database.freedomonthemove.org (S3 bucket)

4. **E37GJ23X2Q9IE1**
   - **Status:** Enabled
   - **Description:** Not specified
   - **Type:** Standard
   - **Domain Name:** d37dr0ktkb760v.cloudfront.net
   - **Alternate Domain Names:** tiles.freedomonthemove.org
   - **Origin:** tiles.freedomonthemove.org (S3 bucket)

5. **E3ELOZYSQ32U5H**
   - **Status:** Enabled
   - **Description:** Not specified
   - **Type:** Standard
   - **Domain Name:** d2aff6d2tcpi.cloudfront.net
   - **Alternate Domain Names:** assets.freedomonthemove.org
   - **Origin:** assets.freedomonthemove.org (S3 bucket)

## CloudFront Architecture

1. **Domain-based Content Organization:** Each CloudFront distribution is associated with a specific subdomain
   - crowdsourcing.freedomonthemove.org / app.freedomonthemove.org: Crowdsourcing interface
   - database.freedomonthemove.org: Database search interface
   - tiles.freedomonthemove.org: Map tiles
   - assets.freedomonthemove.org: Static assets, namely the actual advertisement images
      - source-materials.freedomonthemove.org: an alias for assets.freedomonthemove.org. source-materials was the original hostname before moving to the library. This only exists for people that hotlinked to us.

2. **S3 Origin Integration:** Each CloudFront distribution is configured with an S3 bucket as its origin

