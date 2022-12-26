### Venv
Create a new virtual environment in pyhon3.7
```bash
python3.7 -m venv .venv
```
Activate the virtual environment
```bash
source .venv/bin/activate
```
### Start Kafka

1. Start Kafka with Docker Compose:

```bash
docker-compose -f ./local-test-kafka.yml up -d
```
### Run Python message subscriber with Dapr (Self Hosted Mode)


```bash
cd ./order-processor
pip3 install -r requirements.txt
```

2. Run the Python subscriber app with Dapr:

```bash
dapr run --app-id order-processor-sdk --components-path ../components/ --app-port 6001 -- uvicorn app:app --port 6002
```

3. To run with resiliency enabled (retry logic), run the following command:

```bash
dapr run --app-id order-processor-sdk --config ./config.yaml --components-path ../components/ --app-port 6001 -- uvicorn app:app --port 6002
```

### Run Python message publisher with Dapr (Self Hosted Mode)

1. Install dependencies:

```bash
cd ./checkout
pip3 install -r requirements.txt
```

3. Run the Python publisher app with Dapr:

```bash
dapr run --app-id checkout-sdk --components-path ../components/ -- python3 app.py
```
