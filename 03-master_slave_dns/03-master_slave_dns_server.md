

### 1- MASTER DNS SERVER



#### فایل `/etc/bind/named.conf.local` در DNS Master



```plaintext
zone "mrtqvi.local" {
    type master;
    file "/etc/bind/zones/db.mrtqvi.local";
    allow-transfer { 192.168.41.55; };
};
```



#### فایل `/etc/bind/zones/db.mrtqvi.local` در DNS Master



```plaintext
$TTL    604800
@       IN      SOA     ns1.mrtqvi.local. admin.mrtqvi.local. (
                        2024051901 ; Serial
                        604800     ; Refresh
                        86400      ; Retry
                        2419200    ; Expire
                        604800 )   ; Negative Cache TTL

@       IN      NS      ns1.mrtqvi.local.
@       IN      NS      ns2.mrtqvi.local.
ns1     IN      A       192.168.41.54
ns2     IN      A       192.168.41.55
@       IN      A       192.168.41.54
www     IN      A       192.168.1.10
```



### 2. SLAVE DNS SERVER



#### فایل `/etc/bind/named.conf.local` در DNS Slave

```plaintext
zone "mrtqvi.local" {
    type slave;
    masters { 192.168.41.54; };
    file "/var/cache/bind/db.mrtqvi.local";
};
```



### 3. تست DNS Slave

###  

```bash
nslookup www.mrtqvi.local 192.168.41.55
```



```plaintext
;; ANSWER SECTION:
www.mrtqvi.local.   604800  IN  A   192.168.1.10
```
