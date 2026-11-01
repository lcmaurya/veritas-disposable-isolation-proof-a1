# Disposable synthetic isolation proof

This public repository must contain only this README and `.github/workflows/isolation-proof.yml`. No private project checkout, source, credentials, personal files, model, training data or previous artifacts belong here.

The workflow is manual-only, `permissions: {}`, standard GitHub-hosted `ubuntu-24.04`,8-minute job limit, no checkout, no external Actions, no installs and no image pulls. It only accepts its exact expected public `owner/veritas-disposable-isolation-proof-a1` target, main branch, first run attempt.

The trusted host orchestrator constructs a small local Docker image from the runner's already-installed `/usr/bin/python3.12`, its public system stdlib/linked libraries and the embedded synthetic checker. It imports a local tarball using Docker's documented image-import mechanism. No third-party image is downloaded or accepted by tag. The actual admitted system-file hashes and local image ID are recorded. If required preinstalled tools, cgroup-v2 or controls are unavailable, it stops without installation/fallback/retry.

The child has UID/GID65534, no network, read-only root, zero capabilities, no-new-privileges, private PID/cgroup namespaces, no host bind mounts/devices/sockets/ports,1 CPU,256MiB memory,32 PIDs,192MiB address space,1/2s CPU rlimit,8MiB temporary disk and a30s execution timeout. Checks include host-only synthetic canary denial, synthetic environment/FD noninheritance, no host project/control paths, direct network denial, memory allocation rejection, CPU-time termination and bounded fork denial. Only synthetic localhost canary traffic is used. No real secret is read or printed.

The runner's own GitHub job token is not treated as proof of secret-free execution. No token/secrets/context are passed to the child; child env/FDs and rootfs admission are checked independently. The Docker client uses a new empty config directory rather than the runner home. Credentials are never requested.

Only after OWNER manual push, verify the public repository, exact workflow hash and scope before one manual dispatch. Enter the exact repository slug in `expected_repository`. Do not rerun failed jobs. No automatic push/PR/schedule triggers exist. No model task is authorized by a successful synthetic check.

Receipts are exported in job logs as `PUBLIC_SYNTHETIC_RECEIPTS_BASE64_BEGIN` / `..._END` with SHA256 and bytes; this avoids any upload action or token-bearing API call. Logs contain public runtime metadata and synthetic results only. The job deletes its own temporary container/image/files. A future reviewer must verify all individual checks and cleanup; a launched container or a green skipped job is not security PASS.

This proves only the listed controls in the observed run. It is not proof against kernel vulnerabilities or authorization to load models, acquire packages or integrate production.
