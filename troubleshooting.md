# Troubleshooting Guide

---

## Issue: Cannot Access Nexus UI

### Check container:

```bash
docker ps
```

If not running:

```bash
docker logs nexus
```

Check firewall settings.

---

## Issue: Docker Push Fails (Connection Refused)

Ensure:

- Port 8083 is open
- Docker daemon has insecure registry configured
- Correct IP address used

---

## Issue: Login Fails

Verify:

- Correct admin password
- Correct repository port
- Repository is Docker (hosted)

---

## Issue: Server Selection Timeout

Check:

- Nexus container is running
- Ports are mapped correctly
- Firewall allows access

---

## Debugging Commands

Check logs:

```bash
docker logs nexus
```

Check running containers:

```bash
docker ps
```

Check volumes:

```bash
docker volume ls
```

---

## Common Learning Mistakes

- Forgetting to restart Docker after editing daemon.json
- Forgetting to open firewall ports
- Tagging image incorrectly
- Not logging in before pushing

---

## Note

Debug layer by layer:

1. Container running?
2. Port exposed?
3. Firewall open?
4. Docker configured?
5. Image tagged correctly?

Always isolate the failing layer.

