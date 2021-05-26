# Docker: Run containers

## Explore the Docker client options
With Docker cli client you can do all the work on the lowest level, this brings you as close as possible to the container technology.
Lets explore what we can do with docker cli. For that we look at the shipped documentation first:
```bash
man -k docker
docker (1)           - Docker image and container command line interface
docker-attach (1)    - Attach local standard input, output, and error streams to a running container
...
docker-container-kill (1) - Kill one or more running containers
docker-container-logs (1) - Fetch the logs of a container
docker-container-ls (1) - List containers
...
docker-container-rm (1) - Remove one or more containers
docker-container-run (1) - Run a command in a new container
docker-container-start (1) - Start one or more stopped containers
...
docker-container-stop (1) - Stop one or more running containers
docker-container-top (1) - Display the running processes of a container
...
docker-cp (1)        - Copy files/folders between a container and the local filesystem
docker-create (1)    - Create a new container
...
docker-exec (1)      - Run a command in a running container
...
docker-image (1)     - Manage images
...
docker-logs (1)      - Fetch the logs of a container
docker-manifest (1)  - Manage Docker image manifests and manifest lists
docker-manifest-annotate (1) - Add additional information to a local image manifest
docker-manifest-create (1) - Create a local manifest list for annotating and pushing to a registry
docker-manifest-inspect (1) - Display an image manifest, or manifest list
docker-manifest-push (1) - Push a manifest list to a repository
docker-manifest-rm (1) - Delete one or more manifest lists from local storage
docker-network (1)   - Manage networks
docker-network-connect (1) - Connect a container to a network
docker-network-create (1) - Create a network
docker-network-disconnect (1) - Disconnect a container from a network
docker-network-inspect (1) - Display detailed information on one or more networks
docker-network-ls (1) - List networks
docker-network-prune (1) - Remove all unused networks
docker-network-rm (1) - Remove one or more networks
docker-node (1)      - Manage Swarm nodes
docker-node-demote (1) - Demote one or more nodes from manager in the swarm
docker-node-inspect (1) - Display detailed information on one or more nodes
docker-node-ls (1)   - List nodes in the swarm
docker-node-promote (1) - Promote one or more nodes to manager in the swarm
docker-node-ps (1)   - List tasks running on one or more nodes, defaults to current node
docker-node-rm (1)   - Remove one or more nodes from the swarm
docker-node-update (1) - Update a node
docker-pause (1)     - Pause all processes within one or more containers
docker-plugin (1)    - Manage plugins
docker-plugin-create (1) - Create a plugin from a rootfs and configuration. Plugin data directory must contain config.json and rootfs directory.
docker-plugin-disable (1) - Disable a plugin
docker-plugin-enable (1) - Enable a plugin
docker-plugin-inspect (1) - Display detailed information on one or more plugins
docker-plugin-install (1) - Install a plugin
docker-plugin-ls (1) - List plugins
docker-plugin-push (1) - Push a plugin to a registry
docker-plugin-rm (1) - Remove one or more plugins
docker-plugin-set (1) - Change settings for a plugin
docker-plugin-upgrade (1) - Upgrade an existing plugin
docker-port (1)      - List port mappings or a specific mapping for the container
docker-ps (1)        - List containers
docker-pull (1)      - Pull an image or a repository from a registry
docker-push (1)      - Push an image or a repository to a registry
docker-rename (1)    - Rename a container
docker-restart (1)   - Restart one or more containers
docker-rm (1)        - Remove one or more containers
docker-rmi (1)       - Remove one or more images
docker-run (1)       - Run a command in a new container
docker-save (1)      - Save one or more images to a tar archive (streamed to STDOUT by default)
docker-search (1)    - Search the Docker Hub for images
docker-secret (1)    - Manage Docker secrets
docker-secret-create (1) - Create a secret from a file or STDIN as content
docker-secret-inspect (1) - Display detailed information on one or more secrets
docker-secret-ls (1) - List secrets
docker-secret-rm (1) - Remove one or more secrets
docker-service (1)   - Manage services
docker-service-create (1) - Create a new service
docker-service-inspect (1) - Display detailed information on one or more services
docker-service-logs (1) - Fetch the logs of a service or task
docker-service-ls (1) - List services
docker-service-ps (1) - List the tasks of one or more services
docker-service-rm (1) - Remove one or more services
docker-service-rollback (1) - Revert changes to a service's configuration
docker-service-scale (1) - Scale one or multiple replicated services
docker-service-update (1) - Update a service
docker-stack (1)     - Manage Docker stacks
docker-stack-deploy (1) - Deploy a new stack or update an existing stack
docker-stack-ls (1)  - List stacks
docker-stack-ps (1)  - List the tasks in the stack
docker-stack-rm (1)  - Remove one or more stacks
docker-stack-services (1) - List the services in the stack
docker-start (1)     - Start one or more stopped containers
docker-stats (1)     - Display a live stream of container(s) resource usage statistics
docker-stop (1)      - Stop one or more running containers
docker-swarm (1)     - Manage Swarm
docker-swarm-ca (1)  - Display and rotate the root CA
docker-swarm-init (1) - Initialize a swarm
docker-swarm-join (1) - Join a swarm as a node and/or manager
docker-swarm-join-token (1) - Manage join tokens
docker-swarm-leave (1) - Leave the swarm
docker-swarm-unlock (1) - Unlock swarm
docker-swarm-unlock-key (1) - Manage the unlock key
docker-swarm-update (1) - Update the swarm
docker-system (1)    - Manage Docker
docker-system-df (1) - Show docker disk usage
docker-system-events (1) - Get real time events from the server
docker-system-info (1) - Display system-wide information
docker-system-prune (1) - Remove unused data
docker-tag (1)       - Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
docker-top (1)       - Display the running processes of a container
docker-trust (1)     - Manage trust on Docker images
docker-trust-inspect (1) - Return low-level information about keys and signatures
docker-trust-key (1) - Manage keys for signing Docker images
docker-trust-key-generate (1) - Generate and load a signing key-pair
docker-trust-key-load (1) - Load a private key file for signing
docker-trust-revoke (1) - Remove trust for an image
docker-trust-sign (1) - Sign an image
docker-trust-signer (1) - Manage entities who can sign Docker images
docker-trust-signer-add (1) - Add a signer
docker-trust-signer-remove (1) - Remove a signer
docker-unpause (1)   - Unpause all processes within one or more containers
docker-update (1)    - Update configuration of one or more containers
docker-version (1)   - Show the Docker version information
docker-volume (1)    - Manage volumes
docker-volume-create (1) - Create a volume
docker-volume-inspect (1) - Display detailed information on one or more volumes
docker-volume-ls (1) - List volumes
docker-volume-prune (1) - Remove all unused local volumes
docker-volume-rm (1) - Remove one or more volumes
docker-wait (1)      - Block until one or more containers stop, then print their exit codes
dockerd (8)          - Enable daemon mode
Dockerfile (5)       - automate the steps of creating a Docker image
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjEzOTkzMTM0XX0=
-->