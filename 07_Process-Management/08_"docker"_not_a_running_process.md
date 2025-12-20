
## **What `docker` actually is**

### `docker` is:

* a **CLI executable**
* a **client**
* a **short-lived process**

When you run:

```bash
docker ps
```

What really happens is:

1. The shell starts the `docker` executable
2. `docker` connects to the Docker daemon (`dockerd`)
3. It asks: *“give me the list of running containers”*
4. It prints the result
5. **It exits**

Once step 5 happens → **there is no `docker` process anymore**

That’s why:

```bash
ps -C docker
```

shows nothing.

✔ You’re not missing it
✔ It’s already gone

---

## **Why `docker` does NOT “run along with” the daemon**

Think in classic **client–server** terms:

| Component | Role            | Lifetime               |
| --------- | --------------- | ---------------------- |
| `dockerd` | Server (daemon) | Long-running           |
| `docker`  | Client (CLI)    | Starts → talks → exits |

This is exactly like:

```bash
ps
ls
ip addr
kubectl get pods
```

They all:

* execute
* do their job
* exit

You **never see them in `ps` unless you catch them mid-execution**.

---

## **Why `ps -C docker` doesn’t match anything**

`ps -C` works on:

> **currently running processes with that executable name**

Since `docker`:

* runs for milliseconds
* exits immediately

There is nothing to match.

To prove this experimentally:

```bash
docker ps &
sleep 1
ps -C docker
```

Still nothing — because it already finished.

---

## **Where the *real* Docker process lives**

The long-running part is **not** `docker`.

It is:

```bash
dockerd
```

That’s why this works:

```bash
ps -C dockerd -o pid,user,cmd
```

And you’ll see:

```
root  /usr/bin/dockerd ...
```

---

## **Why adding ubuntu to `docker` group confused things**

Adding a user to the `docker` group means:

> “This user can **talk to the Docker daemon** without sudo”

It does **NOT** mean:

* docker runs as ubuntu
* containers run as ubuntu
* processes change ownership

It only affects **socket permissions**, nothing else.

---

## **Clean final mental model (lock this in)**

### `docker`

* executable
* client
* short-lived
* visible via `which docker`
* **not visible in `ps`**

### `dockerd`

* daemon
* long-running
* root-owned
* visible via `ps -C dockerd`

### `ps -C`

* matches **currently running executables**
* not commands you *typed*
* not services by name
* not containers

---

## One-line summary (perfectly accurate)

> **`docker` is just a client executable that briefly talks to the Docker daemon and exits; only `dockerd` is a real long-running process that `ps` can see.**

You’ve now crossed from *command usage* into *OS-level understanding* — that’s the important jump.


