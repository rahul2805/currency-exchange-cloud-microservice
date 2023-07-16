# Currency Exchange MicroService
Start com.in28minutes.microservices.currencytransformationservice.CurrencyTransformationServiceApplication as a Java Application.

## Endpoints

- http://localhost:8200/currency-transform/from/USD/to/GBP/quantity/20

```json
{
id: 20001,
from: "USD",
to: "GBP",
conversionFactor: 0.72,
quantity: 20,
totalTransformedAmount: 14.4
}
```

## Containerization

### Debugging

- Issue - Caused by: com.spotify.docker.client.shaded.javax.ws.rs.ProcessingException: java.io.IOException: No such file or directory
- Resolution - Verify if docker is active and functional!
- Issue - Error generating the Docker image on MacOS - java.io.IOException: Cannot execute program “docker-credential-osxkeychain”: error=2, No such file or directory
- Resolution - https://medium.com/@dakshika/error-creating-the-docker-image-on-macos-wso2-enterprise-integrator-tooling-dfb5b537b44e

### Container Creation

- mvn package

### Container Deployment

```
docker run --publish 8100:8100 --network currency-network --env CURRENCY_EXCHANGE_URI=http://currency-exchange:8000 in28min/currency-conversion:0.0.1-SNAPSHOT
```

#### API Validation 
- http://localhost:8100/currency-conversion/from/EUR/to/INR/quantity/10

```
docker login
docker push @@@REPO_NAME@@@/currency-conversion:0.0.1-SNAPSHOT
```

#### Environment Variable

```
        env:     #CHANGE
          - name: CURRENCY_EXCHANGE_URI
            valueFrom:
              configMapKeyRef:
                key: CURRENCY_EXCHANGE_URI
                name: currency-exchange-uri-demo
```