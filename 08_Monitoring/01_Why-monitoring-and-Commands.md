
### Importance of Monitoring :

Monitoring helps identify processes consuming excessive CPU, memory, or disk space, enabling proactive troubleshooting and performance optimization.

---

**Commands for Monitoring**

- ```top```                Real-time process monitoring showing CPU and memory usage, with dynamic updates every second.

- ```htop ```              Enhanced, user-friendly version of top with graphical interface and color-coded metrics.

- ```vmstat```             Reports system performance statistics including free memory, swap, and CPU usage; useful for diagnosing slow system complaints.

- ```free -h```            Displays memory usage in human-readable format; preferred for scripting and quick checks.

- ```nproc```              Displays the number of CPUs available on the system.

---

**Disk Space Monitoring**

- ```df -h```              Shows disk space usage per partition in human-readable format.

- ```du -sh```             Summarizes disk usage for specific directories to identify large files or folders.

- ```du -sh *```           show disk usage for all the files and folder individually inside the directory your in.

- `iostat`                 Display CPU and disk I/O statistics


Example: Checking /opt directory size and subfolders to locate large log files occupying disk space.

---

**Advanced Monitoring Tools**

- Integration with Prometheus and Grafana provides sophisticated metrics collection and visualization.
- Alerts via email or Slack can be configured for proactive incident management.
- Despite advanced tools, quick diagnostics often rely on the above command-line utilities.

---

**Network Monitoring**

- `ifconfig`              Show network interfaces (deprecated, use `ip a`)
  
- `ip a`                  Show network interface details
  
- `netstat -tulnp`        Show active connections and listening ports
  
- `ss -tulnp`             Alternative to `netstat` for socket statistics
  
- `ping hostname`         Test network connectivity
  
- `traceroute hostname`   Show network path to a host
  
- `nslookup domain`       Get DNS resolution details

---

**Log Monitoring**

- `tail -f /var/log/syslog`    Live monitoring of system logs
  
- `journalctl -f`              Live system logs for systemd-based distros
  
- `dmesg | tail`               View kernel logs
