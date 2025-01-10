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
