# Add bonescript api and enable UART pins as services to start after boot
## Copy service files to /lib/systemd/system/

```
sudo cp nubeio-bonescript-api.service /lib/systemd/system/
sudo cp nubeio-enable-uart-pins.service /lib/systemd/system/
sudo cp nubeio-enable-uart-pins.timer /lib/systemd/system/
```

## Create symlink for both services

```
sudo ln -s /lib/systemd/system/nubeio-bonescript-api.service /etc/systemd/system/multi-user.target.wants/nubeio-bonescript-api.service
sudo ln -s /lib/systemd/system/nubeio-enable-uart-pins.timer /etc/systemd/system/multi-user.target.wants/nubeio-enable-uart-pins.timer
```

## Enable the new systemd services
```
sudo systemctl daemon-reload
sudo systemctl enable nubeio-bonescript-api.service
sudo systemctl enable nubeio-enable-uart-pins.timer
```

## Reboot and test
```
sudo reboot now
sudo systemctl status nubeio-bonescript-api.service
sudo systemctl status nubeio-enable-uart-pins.timer
```

# Disable UART pin service

Version 1.4 of the Nube iO Edge Controller does not need the UART pins enabled and doing so conflicts with the pins for R1. 

## Delete service files at /lib/systemd/system/
```
sudo rm /lib/systemd/system/nubeio-enable-uart-pins.service
sudo rm /lib/systemd/system/nubeio-enable-uart-pins.timer
```

## Disable the systemd services
```
sudo systemctl daemon-reload
sudo systemctl disable nubeio-enable-uart-pins.timer
```

## Reboot and test
```
sudo reboot now
sudo systemctl status nubeio-enable-uart-pins.timer
```
