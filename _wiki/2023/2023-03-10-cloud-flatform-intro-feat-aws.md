---
layout  : wiki
title   : How they reduce 80% cost by moving away from aws
date    : 2023-03-10 20:44:40 +0900
updated : 2023-03-10 20:44:40 +0900
resource: A7/953B01-621E-4081-B40C-2BCDA2ECBBC3
toc     : true
public  : true
parent  : [[/2023]]
latex   : true
---
* TOC
  {:toc}

### **Cloud**
1. If you buy PC or hardware or run a data center **Initial investment** It is expensive and difficult to operate unless you are an organization that can do infrastructure engineering. Cloud platforms can **use ready computing resources** to meet **the level of resources you want**, **only as much as you want**
2. Infrastructure provided in cloud form generally has a **'pay as you go'** concept. **Pay only as much as you use it**. If the hardware scale is too large or you no longer need a machine, you can just **click a few times** to change it to a smaller instance type with a smaller hardware size, or eliminate it.
3. There is already a lot **ready for infrastructure management. This is why even quite large organizations use cloud platforms, **because the number of server system engineers is at the level of operating expensive server rooms**.

You can set up Linux servers in minutes, multiplex servers, distribute traffic, transmit log metrics, Domain, automatically back up storage, Modify inbound/outbound access controls, and **increase and reduce servers based on traffic status** once in a few clicks.
4. 'Service-Level Agreements (SLAs)' **Guarantees infrastructure uptime**
   Receive. **Payback or credit** if you are not guaranteed the service level specified in the SLA
   You can **reward with money** through your back.
5. Using the **cloud is a great deal to gain from rapid deployment of infrastructure, easy automation, flexible capacity (scalability), reliability, cost benefits of economies of scale, easy deployment of applications around the world, and high levels of security and quality standards**

**Why most people use AWS**

- The organization is most familiar with AWS.
- AWS occupies more than 50% of the cloud platform market and is trusted by many large clients.
- **All kinds of operations are APIized** and **High-level libraries (AWS SDKs) that can access these APIs are well developed by language, so **The barriers to access resources** and **infrastructure control** at the code level are low.
- Once a new member is signed up for AWS, it is a bonus to provide **free tier** that allows you to **use key services for free within a certain limit** for 12 months. Google Cloud Platform and Azure are similar, but AWS offers the most generous free plan.

### selection of engines

- EC2(Elastic Compute Cloud)
- Beanstalk
- ECS(Elastic Container Service)
- ECS+Fargate
  -Lightsail
- Lambda

Since the text becomes redundant to list the pros and cons and each feature, let's post the concepts later, knowing that there are these kinds of engine choices when choosing AWS

### How did Prerender.io reduce server costs by 800K?

Checkout https://levelup.gitconnected.com/how-we-reduced-our-annual-server-costs-by-80-from-1m-to-200k-by-moving-away-from-aws-2b98cbd21b46 for detail contents

Reduce AWS dependency and manage cache data and traffic management as an in-house infrastructure. A service called Prerender itself provides a service that caches and renders JavaScript pages, allowing search engines to crawl and index pure HTML files.

Prerender used servers and services hosted by Amazon Web Services (AWS) to store pages that cache and render for clients.

Because all of this data processing was done on the server, 70,000 pages per minute on AWS resulted in astronomical server maintenance costs.

### Building Internal Infrastructure

**bare metal server**  
It migrated cached pages and traffic to its own internal servers and reduced reliance on AWS. It is expected to reduce hosting costs by 40%.
![Untitled](https://user-images.githubusercontent.com/72185011/208582361-d146f9d3-d90a-43f0-aba7-e28d3fe9e39f.png)

Bare metal servers are services that provide physical servers independently without virtualization. Performance-sensitive services can always operate reliably because they use a single server that is not affected by other cloud users. It is effective when large input/output occurs or requires fast response speed

Most server settings were performed on bare metal servers, and tests were conducted by migrating them little by little to small and controllable units before expansion. Most traffic workloads were successfully migrated from AWS.

**new monitoring dashboard**

It has developed a new dashboard that can identify errors or performance issues.

**minio**
![Untitled 1](https://user-images.githubusercontent.com/72185011/208582475-0547c044-f84e-4142-8a3b-efdaaf93e7e1.png)
After pouring traffic, the task of transferring cached data moved the data from S3 to minio and its own Cassandra clustering. However, according to the new CTO Zsolt Varga, there has been a large expenditure on transferring data.

"The true hidden price of AWS comes from the cost of traffic. They can sell reasonably priced storage and even upload it for free. But if you take it out, you'll have to pay a huge price**.

**Critical comments**

Do you really need a ridiculously complicated permission system? Do you really need 50,000 different types of instances available for possible future use? Do you really need to micro-manage complex setups involving ingress traffic, IPs, load balancers, firewalls, etc...?
Or do you just need a simple, straight-forward service at 1/10th the cost?

I run over 250 sites and customer-facing applications on Digital Ocean with 99.99% availability. My team doesn't need micro-managed permissions to various aspects of the service--just use the permissions available in Kubernetes

I've been screaming at developers for years about their dumb choices to use AWS, Google, or Azure. Maybe now some people will sit up and take notice.

-Aron-

And now you need an extra team of 5 DevOps engineers that will cost you 600-800K per year + 200K (hosting) + MORE HUMAN error

-[Alfonso Valdes Carrales](https://medium.com/@ponchovaldescarrales?source=responses-----2b98cbd21b46----2----------------------------)-

You can say that your AWS bill went down by 800k but to say you SAVED 800k is disingenuous. You could have reduced your AWS bill by $1M by migrating to Azure and it would have been a spicier headline…

-[natebourgoin](https://medium.com/@natebourgoin?source=responses-----2b98cbd21b46----3----------------------------)-

I once saved our company around $20,000/mo in a few hours after I noticed someone way overprovisioned a service that was running for a few years. It was my first new person power move.

-**[MashPotatoQuant](https://www.reddit.com/user/MashPotatoQuant/)-**

**The biggest money saver is, indeed, to know what you're doing.**

The catch is, if you know what you're doing, you are often better off with your own servers.

The extra labor cost is there, but if you do the math it's usually less than you think. When we looked at the price for running some stuff on EC2 instances instead of on-prem, we concluded that we might just as well hire a few persons to sit and stare at our on-prem servers all day long.

Also easily forgotten, there are corresponding labor costs for cloud too (you can't just let developers run wild and create instances high and low - you need ongoing efforts for structure, optimization, monitoring, guidelines, technology evaluation, etc etc).

-**[mbitsnbites](https://www.reddit.com/user/mbitsnbites/)-**

**reference**  
https://levelup.gitconnected.com/how-we-reduced-our-annual-server-costs-by-80-from-1m-to-200k-by-moving-away-from-aws-2b98cbd21b46  
https://www.reddit.com/r/programming/comments/xqipik/how_we_reduced_our_annual_server_costs_by_80_from/