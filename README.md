# EventhubHandler

handler for python logging library. You can push you logs to Azure Event Hub.

## Installation

```sh
pip install EventhubHandler
```

## Setup & Use

Handler reads settings from environment variables.

- `eh_ns_connection_string`: Azure Event hub primary connection string. **required**
- `eventhub_name`: event hub name. **required**
- `bulk_size`: max number of logs can send once. default 10. **optional**
- `frequency`: after x seconds thread sends logs. default 5 sec. **optional**

```python
import logging
logger = logging.getLogger()

eh = EventHubHandler()
formatter = JSONFormatter({"level": "levelname", 
                            "message": "message", 
                            "loggerName": "name", 
                            "processName": "processName",
                            "processID": "process", 
                            "threadName": "threadName", 
                            "threadID": "thread",
                            "timestamp": "asctime",
                            "exception": "exc_info"})

eh.setFormatter(formatter)
logger.addHandler(eh)

logger.info("Logging Happiness!!!")
```

## Advanced Use

If you want to add something in each log like **applicationName** then add like below,

```python
formatter = JSONFormatter({"level": "levelname",
                           "applicationName": ""})  # keep empty key 

# remember to add env variable `applicationName` with appropriate value
```

