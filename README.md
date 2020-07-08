# Mikrotik Reverse Proxy
Work http only
<ul>
  <li>Making Static DNS<br>
<pre>
[admin@tinktunktank] > / ip dns st pr    
Flags: D - dynamic, X - disabled 
 #    NAME            REGEXP           ADDRESS                                           TTL         
 0    m.tink.web.id                    192.168.100.1                                     1d          
 1    r.tink.web.id                    192.168.100.5                                     1d          
 2    www.da.tink....                  192.168.100.4                                     1d          
 3    www.r.tink.w...                  192.168.100.5                                     1d          
 4    w.tink.web.id                    192.168.100.10                                    1d          
 5    www.w.tink.w...                  192.168.100.10                                    1d          
 6    c.tink.web.id                    192.168.100.2                                     1d          
 7    www.c.tink.w...                  192.168.100.2                                     1d          
 8    da.tink.web.id                   192.168.100.4                                     1d          
[admin@tinktunktank] > 

</pre>
</li>  

  <li>Activating Web Proxy <br>
<pre>
[admin@tinktunktank] > / ip proxy set enabled=yes port=8080
</pre>
  </li>
    <li>Web Proxy<br>
  <pre>
[admin@tinktunktank] > / ip proxy access pr     
Flags: X - disabled 
 #   DST-PORT                     DST-HOST               PATH               METHOD  ACTION       HITS
 0   23-25                                                                          deny            0
 1                                m.tink.web.id                                     allow           0
 2                                r.tink.web.id                                     allow           8
 3                                www.r.tink.web.id                                 allow           0
 4                                w.tink.web.id                                     allow           2
 5                                www.w.tink.web.id                                 allow           0
 6                                c.tink.web.id                                     allow           0
 7                                www.c.tink.web.id                                 allow           2
 8                                da.tink.web.id                                    allow           2
 9                                www.da.tink.web.id                                allow           0
10                                                                                  deny           17
[admin@tinktunktank] >  
  </pre>
  </li>  
  <li>dstnat all con to web proxy <br>
<pre>
[admin@tinktunktank] > / ip fi na pr
Flags: X - disabled, I - invalid, D - dynamic 
 0    chain=dstnat action=dst-nat to-ports=8080 protocol=tcp dst-port=80 log=no log-prefix="" 
[admin@tinktunktank] > 
</pre>
  </li>  
</ul>  
