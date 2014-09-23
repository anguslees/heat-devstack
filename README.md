heat-devstack
=============

OpenStack all-in-one devstack node constructed using heat.  Tested on
Rackspace public cloud

```
heat stack-create \
  -u https://raw.githubusercontent.com/anguslees/heat-devstack/master/devstack.yaml \
  -P key_name=$existing_ssh_key \
  devstack
```

After about 15 minutes, you should be able to find a working horizon
dashboard at the URL given by `heat output-show devstack horizon_url`.
You can log in using `demo` or `admin` with the password given by
`heat output-show devstack admin_password`.

`eval $(eval echo $(heat output-show devstack openrc))` will set a few
environment variables used by many OpenStack command line tools.  (The
double eval is necessary to remove an extra layer of quoting added by
the heat command line tool.)

Troubleshooting
---------------

If you think it has failed (or are curious), you can log into the
devstack host using `nova ssh devstack-devstack`.  Output from the
cloud-init script is in `/var/log/cloud-init-output.log` and devstack
logs are in `/opt/stack/logs`.
