---
order: 2
---

# Volumes

- Volumes are essential for persisting data between containers.
- Those volumes are shared between containers.
- Since the data inside the volumes are persistent, any damage or restart to the containers will not affect the data inside the volumes.
- Even if you delete the containers, the data inside the volumes will not be deleted.

!!! info
All volumes are kept inside `volumes/` directory in host machine.
!!!

### Volume definitions

+++ db/

- MongoDB's volume (used by `mongo` service)
- Persistent (will remain even if you terminate services/containers)
- Locally binded

  - That means host instance's `/volumes/db` directory is binded to the `mongo` container's `/data/db` directory.
  - And you need to manually create `/volumes/db` directory in host instance before running the project.

```MD
    db:
    driver: local
    driver_opts:
        type: "none"
        o: "bind"
        device: "../volumes/db"

```

!!! info
For detailed information about MongoDB, see [Database (MongoDB)](<../../database-(mongodb)>).
!!!

+++ uploads/

- Shared between `flask` and `nodejs` services
- `flask` will save images in this directory (R+W)
- `nodejs` will read images from this directory (R)
- Persistent (will remain even if you terminate services/containers)
- Locally binded

  - That means host instance's `/volumes/uploads` directory is binded to the `nodejs` container's `uploads/` directory, `flask` container's `instance/uploads/` directory.
  - And you need to manually create `/volumes/db` directory in host instance before running the project.

```MD
    uploads:
    driver: local
    driver_opts:
        type: "none"
        o: "bind"
        device: "../volumes/uploads"
```

+++
