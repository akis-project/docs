---
order: 1
---

# Networks

- Networks are used to connect containers together.
- Containers can communicate with each other if they are in the same network.
  - e.g. react service can send requests to nodejs service because they are in the same network. it can use `http://nodejs:5001` to send requests. Notice that base url can be either container name or container ip address.

### Network definitions

Nothing fancy. Networks between services should be set `internal: true` If you want to connect to MongoDB instance from public internet, e.g. from MongoDB Compass, set `internal: false`

```md
    react-nodejs-network:
        driver: bridge
        ipam:
            driver: default
            config: - subnet: 172.16.1.0/28

    nodejs-mongo-network:
        driver: bridge
        internal: false # False to allow access from internet
        ipam:
            driver: default
            config:
            - subnet: 172.16.2.0/29

    nodejs-flask-network:
        driver: bridge
        internal: false # False to allow access from internet
        ipam:
            driver: default
            config:
            - subnet: 172.16.3.0/29
```
