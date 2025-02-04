# Increase Swap Memory to 16GB on Ubuntu 22.04

This guide explains how to increase the swap memory on Ubuntu 22.04 from the current size (e.g., 2GB) to 16GB. Follow the steps below carefully.

---

## **1. Turn Off the Current Swap File**
Before making any changes, turn off the existing swap file:

```bash
sudo swapoff -v /swapfile
```

---

## **2. Remove the Existing Swap File**
Delete the current swap file:

```bash
sudo rm -f /swapfile
```

---

## **3. Create a New Swap File (16 GB)**
Create a new swap file with a size of 16GB:

### Using `fallocate` (Preferred Method):
```bash
sudo fallocate -l 16G /swapfile
```

### Alternative Method (if `fallocate` is unavailable):
```bash
sudo dd if=/dev/zero of=/swapfile bs=1G count=16
```

---

## **4. Set Correct Permissions**
Set the appropriate permissions for the swap file:

```bash
sudo chmod 600 /swapfile
```

---

## **5. Set Up the Swap File**
Set up the swap file:

```bash
sudo mkswap /swapfile
```

---

## **6. Enable the New Swap File**
Enable the swap file:

```bash
sudo swapon /swapfile
```

---

## **7. Verify the Swap Space**
Check the swap space to confirm the changes:

```bash
sudo swapon --show
free -h
```

---

## **8. Make the Change Persistent Across Reboots**
Ensure the new swap configuration persists after a reboot:

1. Open the `/etc/fstab` file:

   ```bash
   sudo nano /etc/fstab
   ```

2. Add the following line (or ensure it exists):

   ```plaintext
   /swapfile none swap sw 0 0
   ```

3. Save the file and exit.

---

## **Conclusion**
Your swap memory has been successfully increased to 16GB. You can verify it by running:

```bash
free -h
```

Enjoy your upgraded system performance!

===========================================================================================================================================================

# Increase Swap Memory to 30GB on Ubuntu (Permanent)

This guide explains how to increase swap memory to **30GB** on Ubuntu and make it permanent across reboots.

## Steps to Increase Swap Memory

### 1. Disable and Remove Existing Swap
```bash
sudo swapoff -a
sudo rm -f /swapfile
```

### 2. Create a New 30GB Swap File
```bash
sudo fallocate -l 30G /swapfile
```
If `fallocate` fails, use:
```bash
sudo dd if=/dev/zero of=/swapfile bs=1G count=30
```

### 3. Set Proper Permissions
```bash
sudo chmod 600 /swapfile
```

### 4. Format the Swap File
```bash
sudo mkswap /swapfile
```

### 5. Enable the Swap
```bash
sudo swapon /swapfile
```

### 6. Make the Swap Permanent
Add the following line to `/etc/fstab`:
```bash
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

### 7. Adjust Swappiness (Optional)
To optimize system performance, adjust the swappiness value:
```bash
echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### 8. Verify the Swap
Check if the swap is active:
```bash
free -h
```
Check if the swap is listed in `/etc/fstab`:
```bash
cat /etc/fstab
```

## Conclusion
After completing these steps, your **swap memory will be permanently set to 30GB** and persist across system reboots.
