The `file` and `kubernetes_logs` sources now reliably expire the checkpoints of files they stop watching. Previously, if a file's last read position was committed after its watcher had been removed, which is common when the pipeline is behind, the checkpoint was marked alive again and kept forever. On hosts with many rotating log files this grew `checkpoints.json` without bound, and because the whole file is rewritten every `glob_minimum_cooldown_ms`, it led to sustained high disk writes and CPU.

authors: initialed85
