<h1>Re-launching-Employee-Directory-App</h1>

<h2>Description</h2>
we are going to create a VPC, create four subnets, create a route table for the public subnets, and then we will attach an internet gateway to the VPC and then relaunch the employee directory application in the new VPC.
<br />


<h2>Program walk-through:</h2>

1. I am in the VPC dashboard here, and I'm going to click on Create VPC, I'm going to select VPC only, and give this VPC a name. Moreover,  enter in the CIDR range for this VPC,  I'm going to give the CIDR range
to be 10.1.0.0/16.
then I'm going to scroll down and click Create VPC.
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741803643/Screenshot_2025-03-10_175108_pgqg2r.png"/>

<br />

2. - The next thing I will do is create the subnets, I'm gonna select the subnets on the left-hand navigation and then I'm gonna click Create subnet, adding, we'll select a VPC for this, and we will select the VPC we just created, app-vpc.
for our first subnet, I will give this a name, Public Subnet 1, and then select the availability zone which will be us-west-2a, And then we'll give this a CIDR range
which is gonna be 10.1.1.0/24.
- We can go ahead and add our next subnet we're gonna have a public and a private subnet in each availability zone.
So we'll create our private one next, so Private Subnet 1, availability zone, same one us-west-2a, and then providing the CIDR range, we'll say this is 10.1.2.0/24.
- Next one is gonna be Public Subnet 2, put it in us-west-2b, and for the subnet range we can put 10.1.3.0/24.
- Create one more subnet which will be our Private Subnet 2, select the availability zone us-west-2b, and give this the CIDR range of 10.1.4.0/24.
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741803867/Screenshot_2025-03-10_175417_p6xn5y.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741804073/Screenshot_2025-03-10_182246_mi42pv.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741805190/Screenshot_2025-03-10_182409_lardzz.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741805916/Screenshot_2025-03-11_184421_ezkl4u.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741806473/Screenshot_2025-03-11_184534_tr0pwm.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741806811/Screenshot_2025-03-11_184602_unxgcf.png"/>
<br />

3. - Create an internet gateway,  give this a name, then click Create internet gateway.
   - Select the new internet gateway that we just created, and we want to attach this to a VPC, then we'll select our app VPC and then click Attach to internet gateway.
   (For internet gateways and one internet gateway, can only ever be attached to one VPC)
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741808789/Screenshot_2025-03-11_185303_n0tfo8.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741811507/Screenshot_2025-03-11_185451_pidtfy.png"/>
<br />

4.Configure our route tables
- You can see  two route tables already, the main route tables for both of VPCs, default VPC, and  app-vpc, which we can scroll to the right and expand this and read that VPC.
-  click create route table and give this route table a name the save it. adding,  associate this with our app-vpc and then click Create route table.
-  Route table that's been created, now add a route that will allow any subnet that has this route table associated with it.
-  Add a route that will allow traffic from the internet, 0.0.0.0/0.
-  To where? The internet gateway, and the internet gateway we wanna choose the one that we just created and then we'll click save changes
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741814029/Screenshot_2025-03-11_185540_t2lp7t.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741814039/Screenshot_2025-03-11_185627_qn7wf9.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741814054/Screenshot_2025-03-11_185652_s5ctfe.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741814066/Screenshot_2025-03-11_185729_x2hgi7.png"/>
<br />

 5. - Now associate these subnets with the route table, click Subnet associations and then scroll down, we currently have this
associated with no subnets.
- I'm going click Edit subnet associationsand then I'm going to select, the first two public subnets only, (So there's nothing inherently about a subnet
that makes it public or private), 
- Click Save associations here, and then we can scroll back down, click on the subnet association's tab, and we can now see that we have our two public subnets associated with this route table.
- Review the routes, clicking back on the routes tab, we can see we have our local route and we have our route to the internet through the internet gateway.
  
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741816940/Screenshot_2025-03-11_185748_u2j6m6.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741816952/Screenshot_2025-03-11_185819_d2ch4t.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741816962/Screenshot_2025-03-11_185901_t2a5tw.png"/>
<br />

6. - The last step here is let's go ahead and relaunch our employee directory application, I'm going to navigate over to the EC2 console, So what I'm going to select actions and then Image and templates.
In addition, I will select Launch more like this, and what this does is brings you to a page that has a lot of the configurations for that original instance so you don't have to go through and reselect all of the configurations.
- Call this Employee Directory App 2, We can see we have the Linux 2 AMI selected here and we also have out t2.micro selected.
  For the key pair, we do have to select, that we want to proceed without a key pair again, and there under network settings, it is where we're gonna make most of our changes.
- We're going to select the new app-vpc that we just created, and then we're going to select what public subnet we want to launch into, Public Subnet 1 or Public Subnet 2, We're gonna go ahead and select Public Subnet 1 and then we're also ensuring that this auto-assigned public IP is set to enable.
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741821306/Screenshot_2025-03-11_190906_kaqjz3.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741821317/Screenshot_2025-03-11_194743_gm5hjs.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741821335/Screenshot_2025-03-11_194829_hqc3xx.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741821347/Screenshot_2025-03-11_194840_wvi70d.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741821532/Screenshot_2025-03-11_194937_akgvwr.png"/>
<br />

7. we can select our security group, currently we have the security group that was created previously associated with this instance and it's giving us an error saying that we can't use the security group with this subnet.
That's because the security group is tied to the VPC, create a new security group that will be associated with this new VPC, not the default VPC.
Click Create security group and then we will leave the default for the name and, do the same thing that we did when we created our original security group.
Allow both HTTP traffic on port 80 from the internet and adding a second rule, allow HTTPS traffic on port 443 from anywhere.
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741822173/Screenshot_2025-03-11_195101_rhzg2h.png"/>
<br />

8-  scroll down to the advanced details and expand, you can see that the role has been prepopulated, that's great, let's take a look at that user data, you can see that its also prepopulated.
Now we can click Launch instance, click on the instance ID, see that this is in the pending state, wait a few minutes and come back and try to access it through the public IP address.
If we can access it, that means that all of our network configurations were configured correctly.
If we copy the IP address to paste it into a new tab off screen, we can see that we can now access the Employee Directory application at the IP address of the new instance that was launched into our new app-vpc.
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741822320/Screenshot_2025-03-11_195145_uvk5m8.png"/>
<img src="https://res.cloudinary.com/dk3bkl3ji/image/upload/v1741822344/Screenshot_2025-03-11_195505_mnfy7k.png"/>










