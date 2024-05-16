# Docker Compose Setup

## Services:

### MongoDB (db)
- Image: `mongo:latest`
- Container Name: `mongodb`
- Port Mapping: `27017:27017`
- Volume: `./mongodata:/data/db`
- Restart Policy: `unless-stopped`

### Redis Cache (redis-cache)
- Image: `redis:latest`
- Container Name: `redis`
- Port Mapping: `6379:6379`
- Volume: `./redis-data:/data`
- Restart Policy: `unless-stopped`

### RabbitMQ (rabbitmq)
- Image: `rabbitmq:3-management-alpine`
- Container Name: `rabbitmq`
- Port Mapping:
  - `5672:5672` (AMQP)
  - `15672:15672` (Management Plugin)
- Volumes:
  - `./rabbitmq-vol:/var/lib/rabbitmq/`
  - `./rabbitmq-logs:/var/log/rabbitmq`
- Networks: `rabbitmq_go_net`
- Restart Policy: `unless-stopped`

## Volumes:
- `mongodata`
- `redis-data`
- `rabbitmq-vol`
- `rabbitmq-logs`

## Networks:
- `rabbitmq_go_net`: Bridge network driver

## Usage:

1. **Start the Services:**
```bash
docker-compose up -d
```

2. **Connect to MongoDB:**
```bash
mongodb://127.0.0.1:27017
```

3. **Connect to Redis:**
```bash
127.0.0.1:6379
```

4. **Access RabbitMQ Management UI:**
- URL: amqp://localhost:15672
- Credentials: 
  - Username: `guest`
  - Password: `guest`
 