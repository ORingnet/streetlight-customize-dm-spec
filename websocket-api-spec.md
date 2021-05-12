WebSocket API Spec
===

## Device metric event

* Subscribe event: `subscribe:DEVICE_METRIC_EVENT`
* Message event: `DEVICE_METRIC_EVENT`

### Payload

```json5
{
  "type": "DEVICE_METRIC_EVENT",
  "data": {
    "id": "delete_me_01",
    "metrics": {
      "realtime": true,
      "brightness": 100,
      "voltage": 240,
      "current": 306.2493806242823,
      "powerFactor": 0.05781231705582801,
      "power": 4249.196709792471,
      "cellId": "51565954",
      "rssi": -55.192584441190284,
      "rsrp": -46.924688467526906,
      "rsrq": -54.40212776005038,
      "snr": null,
      "temperature": 2.5596294498444716,
      "lumen": 3074,
      "xAxis": 0.7216741126173136,
      "yAxis": 0.37811002873483535,
      "zAxis": 0.2221974656302963,
      "timestamp": 1569895681
    }
  }
}
```

## Device desired state event

* Subscribe event: `subscribe:DEVICE_DESIRED_STATE_EVENT`
* Message event: `DEVICE_DESIRED_STATE_EVENT`

### Payload

```json5
{
  "type": "DEVICE_DESIRED_STATE_EVENT",
  "data": {
    "id": "delete_me_01",
    "state": {
      "brightness": 100,
      "schedule": [
        {
          "time": "23:59",
          "brightness": 100
        },
        {
          "time": "00:00",
          "brightness": 0
        }
      ],
      "reportDelay": 240,
      "reportInterval": 600
    }
  }
}
```

## Device report state event

* Subscribe event: `subscribe:DEVICE_REPORTED_STATE_EVENT`
* Message event: `DEVICE_REPORTED_STATE_EVENT`

### Payload

```json5
{
  "type": "DEVICE_REPORTED_STATE_EVENT",
  "data": {
    "id": "delete_me_01",
    "state": {
      "brightness": 100,
      "schedule": [
        {
          "time": "23:59",
          "brightness": 100
        },
        {
          "time": "00:00",
          "brightness": 0
        }
      ],
      "reportDelay": 240,
      "reportInterval": 600
    }
  }
}
```

## Device last data time event

* Subscribe event: `subscribe:DEVICE_LAST_DATA_TIME_EVENT`
* Message event: `DEVICE_LAST_DATA_TIME_EVENT`

### Payload

```json5
{
  "type": "DEVICE_LAST_DATA_TIME_EVENT",
  "data": {
    "id": "delete_me_01",
    "timestamp": 1569982566
  }
}
```

### Example

```javascript
import io from 'socket.io-client';

enum WebsocketEvent {
  DEVICE_METRIC_EVENT = 'DEVICE_METRIC_EVENT',
  DEVICE_DESIRED_STATE_EVENT = 'DEVICE_DESIRED_STATE_EVENT',
  DEVICE_REPORTED_STATE_EVENT = 'DEVICE_REPORTED_STATE_EVENT',
  DEVICE_LAST_DATA_TIME_EVENT = 'DEVICE_LAST_DATA_TIME_EVENT',
}

const ioClient = io.connect('http://localhost:3000');

ioClient.on('connect', () => {
  ioClient.emit(`subscribe:${WebsocketEvent.DEVICE_METRIC_EVENT}`);
  ioClient.emit(`subscribe:${WebsocketEvent.DEVICE_DESIRED_STATE_EVENT}`);
  ioClient.emit(`subscribe:${WebsocketEvent.DEVICE_REPORTED_STATE_EVENT}`);
  ioClient.emit(`subscribe:${WebsocketEvent.DEVICE_LAST_DATA_TIME_EVENT}`);
});

ioClient.on(WebsocketEvent.DEVICE_METRIC_EVENT, (data) => {
  console.log(`receive ${WebsocketEvent.DEVICE_METRIC_EVENT}:::`, data);
});

ioClient.on(WebsocketEvent.DEVICE_DESIRED_STATE_EVENT, (data) => {
  console.log(`receive ${WebsocketEvent.DEVICE_DESIRED_STATE_EVENT}:::`, data);
});

ioClient.on(WebsocketEvent.DEVICE_REPORTED_STATE_EVENT, (data) => {
  console.log(`receive ${WebsocketEvent.DEVICE_REPORTED_STATE_EVENT}:::`, data);
});

ioClient.on(WebsocketEvent.DEVICE_LAST_DATA_TIME_EVENT, (data) => {
  console.log(`receive ${WebsocketEvent.DEVICE_LAST_DATA_TIME_EVENT}:::`, data);
});
```
