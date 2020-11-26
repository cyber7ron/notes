# BloodHound

Bloodhound is a graphical interface that allows you to visually map out the network. This tool along with SharpHound which  takes the user, groups, trusts of the network and collects them into .json files to be used inside of Bloodhound.

#### Installing Bloodhound

```
Sudo apt install BloodHound
neo4j console #default credentials -> neo4j:neo4j

```
___ 

#### Getting Loot w/ Sharphound

```
powershell -ep bypass
. .\Path\to\SharpHound.ps1
Invoke-Bloodhound -CollectionMethod All -Domain <domain-name> -ZipFileName <filename.zip>

```

 Transfer the loot.zip folder to your Attacker Machine

* * * 

#### Mapping the network w/ BloodHound

1. Run `bloodhound` on kali machine
2. sign in using creds
3. import the zip file which we get from `sharphound` .
4. now you can view graphical network and select queries and much more things