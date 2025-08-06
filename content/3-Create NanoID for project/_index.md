---
title : "Create NanoID for project "
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

We need to create unique id (Unique identifier) for our project, so that It won’t be any conflicts in the future.

{{% notice tip %}}
Make sure you are in the root directory of your project:
{{% /notice %}}

```
mkdir scripts
cd scripts
```
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID1.png?width=90pc)
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID2.png?width=90pc)

create generate_nanoid.py in scripts:
{{% notice info %}}
right click on "scripts" -> New file
{{% /notice %}}

or type in console:
````
code generate_nanoid.py
````
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID3.png?width=90pc)

Write script that create nanoid:
````
import nanoid
import nanoid_dictionary as nd

if __name__ == "__main__":
    alphabet = nd.lowercase + nd.numbers
    id = nanoid.generate(alphabet, 10)
    print(id)

````
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID4.png?width=90pc)


Then run:
````
python .\generate_nanoid.py
````
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID5.png?width=90pc)


{{% notice info %}}
Result: 6aqqepemzy
{{% /notice %}}
````
cd ..
code .env 
````
paste the nanoid code into the .env file:
````
 id=[your nanoid here]
 ````
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID6.png?width=90pc)

{{% notice tip %}}
Save (Ctr + S)
{{% /notice %}}
````
#Check id with cat:
cat .env
````
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID7.png?width=90pc)

### Content
<!--
3.1. [Connect to EC2 Public Server](3.1-public-instance/) \
3.2. [Cconnect to EC2 Private Server](3.2-private-instance/)
-->