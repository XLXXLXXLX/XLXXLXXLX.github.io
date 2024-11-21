在`~/m2/settings.xml`中：
```xml
<settings>
 <proxies>
     <proxy> 
       <id>workProxy</id> 
       <active>true</active> 
       <protocol>http</protocol>
       <!--   <username>admin</username>       -->
       <!--   <password> admin</password>        -->
       <host>127.0.0.1</host>
       <port>10809</port>   
       <nonProxyHosts>local.net|some.host.com</nonProxyHosts>    
     </proxy>
 </proxies>
</settings>
```