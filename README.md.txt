
# TourPlaces App - Vagrant Cluster Deployment

This project is a Vagrant-based deployment of the [TourPlaces React App](https://github.com/cw-barry/Tour-Places-App.git) as part of the DevOps assignment (Week 8 Bonus). It simulates a scalable cluster with load balancing for high availability.

---

#Project Structure

- **Load Balancer**: Ubuntu 22.04, 2GB RAM, IP `192.168.70.100`
- **Web Servers**: 3 (then 4) Ubuntu 22.04, 1GB RAM each, IPs `192.168.70.101-104`
- **App Folder**: Cloned as `./frontend` and served from `/var/www/tour-app`

---

#Steps to Run

#Clone and Setup

git clone https://github.com/cw-barry/Tour-Places-App.git frontend