# fanctl

Fan control CLI for QNAP TS-853 running OpenMediaVault (Debian 13).

Controls the Fintek F71869A Super I/O chip via sysfs.

## Install

```bash
sudo cp fanctl /usr/local/bin/fanctl
```

**Load the kernel module on boot:**

```bash
echo f71882fg | sudo tee -a /etc/modules
sudo modprobe f71882fg
```

## Usage

```
sudo fanctl status        # temps, PWM values, fan RPMs
sudo fanctl run           # automatic control loop (Ctrl+C to stop)
sudo fanctl speed 45%     # manual: set fans to 45%
sudo fanctl speed 180     # manual: set raw PWM value (0–255)
sudo fanctl auto          # return control to hardware
sudo fanctl help          # show all commands
```

## Fan curve (run mode)

| Temp     | PWM       |
|----------|-----------|
| < 35°C   | 60        |
| 35–45°C  | 60–120    |
| 45–55°C  | 120–180   |
| 55–65°C  | 180–255   |
| > 65°C   | 255       |

PWM is only updated when the target changes by more than 5. On exit, control is returned to hardware automatically.
