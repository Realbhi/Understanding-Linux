### Services: Special Background Processes

Services are specialized processes that run in the background and start automatically during system boot.
Unlike regular processes that stop when the server restarts, services ensure critical applications (e.g., web servers like Apache, Nginx) restart automatically.

---

**Managing services is done via the systemctl command:**

lists running services.
```
systemctl list-units --type=service 
```

stops a service.
```
systemctl stop 
```

starts a service.
```
systemctl start 
```
