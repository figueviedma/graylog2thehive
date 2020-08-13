# graylog2thehive

Create alerts in [The Hive](https://github.com/TheHive-Project/TheHive) from your [Graylog](https://github.com/Graylog2/graylog2-server/) alerts, to be turned into Hive cases.

Simple Python flask app that runs as a web server, and accepts POST requests from your Graylog notifications.


Initial configuration:
* Clone the git repo `git clone https://github.com/figueviedma/graylog2thehive.git /opt/graylog2thehive`
* If planning to use SSL, remove comments and configure the certificate paths in `app.py`
* Set your Hive API key in `init.d/graylog2thehive.service` for the `HIVE_SECRET_KEY`
* Set your Hive and Graylog URLs in `config.py`
* **Optional**: `app/__init__.py`, configure any other IP, hash, URL, or filename fields in place of src_ip and dst_ip to include them as artifacts/observables in your alert


Installation script:
```
yum -y install epel-release 
yum -y install git python3 python-pip
pip install --upgrade pip
pip install -r requirements.txt
cp init.d/graylog2thehive.service /etc/systemd/system/graylog2thehive.service
systemctl enable graylog2thehive
systemctl start graylog2thehive
```

* Runs at https://0.0.0.0:5000, accepts POST requests
  * Point your Graylog `Legacy Alarm Callback` to `https://[YOURSERVER].com:5000/create_alert`
  * Point your Graylog `HTTP Notification` to `https://[YOURSERVER].com:5000/create_alert_http`
