# Lecture 10 VPC networking

- 1. VPC
    - 1.AWS Definition
        - 建立自己的局域网。非常简单的set up 我们的network. 可以方便的对安全性进行设置。
            
            ![https://api2.mubu.com/v3/document_image/64d8ab0b-8b91-472d-bf4c-645a24809ddb-14086676.jpg](https://api2.mubu.com/v3/document_image/64d8ab0b-8b91-472d-bf4c-645a24809ddb-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/1300eefc-f144-4333-9827-8083d8dc3e0f-14086676.jpg](https://api2.mubu.com/v3/document_image/1300eefc-f144-4333-9827-8083d8dc3e0f-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/32355557-0ea6-43d9-a04c-df52d1d78eee-14086676.jpg](https://api2.mubu.com/v3/document_image/32355557-0ea6-43d9-a04c-df52d1d78eee-14086676.jpg)
            
        - 划分很多子网，并将某些子网变成private or public。
    - 2.VPC组成图
        - region based service
            
            ![https://api2.mubu.com/v3/document_image/d225e99e-13a2-4f70-bfc1-4dafaea2eace-14086676.jpg](https://api2.mubu.com/v3/document_image/d225e99e-13a2-4f70-bfc1-4dafaea2eace-14086676.jpg)
            
        - 
    - 3.internal IP range (for IP v4)
        - 人为规定了三个IP range
            
            ![https://api2.mubu.com/v3/document_image/b866f651-3953-451a-bfd3-8b8f766d3a44-14086676.jpg](https://api2.mubu.com/v3/document_image/b866f651-3953-451a-bfd3-8b8f766d3a44-14086676.jpg)
            
        - [CIDR.xyz](http://cidr.xyz/) 网段划分
            
            ![https://api2.mubu.com/v3/document_image/b0f14701-3841-4aeb-854a-74831166ffd7-14086676.jpg](https://api2.mubu.com/v3/document_image/b0f14701-3841-4aeb-854a-74831166ffd7-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/2c6fa5c5-16e2-4ae6-9c42-e7a29ead83bf-14086676.jpg](https://api2.mubu.com/v3/document_image/2c6fa5c5-16e2-4ae6-9c42-e7a29ead83bf-14086676.jpg)
            
            - 这个网站可以查询有多少个可用IP。
    - 4. VPC能干什么
        - 可以让想访问public internet的instance 就放在public的子网里。等等，如下
            
            ![https://api2.mubu.com/v3/document_image/5fa016eb-8b06-4301-a58b-147c00724a76-14086676.jpg](https://api2.mubu.com/v3/document_image/5fa016eb-8b06-4301-a58b-147c00724a76-14086676.jpg)
            
    - 5.Default VPC
        - 
            
            ![https://api2.mubu.com/v3/document_image/e5a03e8f-6ac3-4803-ae52-ad0eaf93d9bb-14086676.jpg](https://api2.mubu.com/v3/document_image/e5a03e8f-6ac3-4803-ae52-ad0eaf93d9bb-14086676.jpg)
            
    - 6. VPC peering
        - 一定是两个互相打交道的VPC peering。
            
            ![https://api2.mubu.com/v3/document_image/a99a7c94-44f1-475b-9979-63af1cf86455-14086676.jpg](https://api2.mubu.com/v3/document_image/a99a7c94-44f1-475b-9979-63af1cf86455-14086676.jpg)
            
        - VPC Transitive peering
            
            ![https://api2.mubu.com/v3/document_image/01121a05-d509-4e00-9bed-a707ab998f19-14086676.jpg](https://api2.mubu.com/v3/document_image/01121a05-d509-4e00-9bed-a707ab998f19-14086676.jpg)
            
    - 6. Summary
        - 逻辑上的datacenter 局域网在AWS上
            
            ![https://api2.mubu.com/v3/document_image/491b6a9c-f771-47f1-ae9f-56841f20b1f5-14086676.jpg](https://api2.mubu.com/v3/document_image/491b6a9c-f771-47f1-ae9f-56841f20b1f5-14086676.jpg)
            
    - NAT gateway
        - 
            
            ![https://api2.mubu.com/v3/document_image/6f1e05fb-af9e-4f84-aff9-86434a7c552d-14086676.jpg](https://api2.mubu.com/v3/document_image/6f1e05fb-af9e-4f84-aff9-86434a7c552d-14086676.jpg)
            
- VPC AWS操作（00：24）
    - Network ACLs (network access control lists)
        - 控制inbound。default 的状态下，inbound和outbound允许所有的traffic
            
            ![https://api2.mubu.com/v3/document_image/9ecd607e-3401-4f61-9fd5-8a1f8ba913ea-14086676.jpg](https://api2.mubu.com/v3/document_image/9ecd607e-3401-4f61-9fd5-8a1f8ba913ea-14086676.jpg)
            
    - CREATE VPC
        - 给vpc 设定CIDR
            - 
                
                ![https://api2.mubu.com/v3/document_image/8ebc8e99-9673-40e5-abc7-3593c05af75b-14086676.jpg](https://api2.mubu.com/v3/document_image/8ebc8e99-9673-40e5-abc7-3593c05af75b-14086676.jpg)
                
        - 新建的VPC Internet gateway是没有的,只有default有，说明custom 的VPC是没有访问Internet的能力的。default 的VPC可以访问Internet
        - 默认是没有子网的，需要创建子网
            - create subnet
                
                ![https://api2.mubu.com/v3/document_image/c75414e8-d76e-4afa-816e-55a11ee2553d-14086676.jpg](https://api2.mubu.com/v3/document_image/c75414e8-d76e-4afa-816e-55a11ee2553d-14086676.jpg)
                
            - 原本有256-2=254 （减掉broadcast地址和Internet地址），但是子网只有251个available address，为什么？
                - 需要一个路由器当IP address，一个DNS，一个预留给AWS未来用的。所以只有251个available address
                    
                    ![https://api2.mubu.com/v3/document_image/4d86a117-5826-42f0-9d64-5fae0c072e87-14086676.jpg](https://api2.mubu.com/v3/document_image/4d86a117-5826-42f0-9d64-5fae0c072e87-14086676.jpg)
                    
        - 建一个Internet gateway， attach vpc
            - 一个VPC只能有一个Internet gateway
                
                ![https://api2.mubu.com/v3/document_image/498e0569-9ac5-4cbf-a970-09558794307f-14086676.jpg](https://api2.mubu.com/v3/document_image/498e0569-9ac5-4cbf-a970-09558794307f-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/06d9bc54-b73b-4a4a-882b-a25a6943392e-14086676.jpg](https://api2.mubu.com/v3/document_image/06d9bc54-b73b-4a4a-882b-a25a6943392e-14086676.jpg)
                
            - IGW 实际上就是一个EC2 instance
                
                ![https://api2.mubu.com/v3/document_image/084b2b58-ab85-476e-bc66-e4406615f442-14086676.jpg](https://api2.mubu.com/v3/document_image/084b2b58-ab85-476e-bc66-e4406615f442-14086676.jpg)
                
        - 在route Tables中告诉VPC访问Internet
            - 如果新建的VPC没有指明需要用的路由表的话，将会连到main （default）route table上
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/85ed8a1b-c0b8-4d10-9f62-ea9d4ada4964-14086676.jpg](https://api2.mubu.com/v3/document_image/85ed8a1b-c0b8-4d10-9f62-ea9d4ada4964-14086676.jpg)
                    
            - 需要新建一个route table
                - local 连VPC畅通无阻，外部通过0.0.0.0/0 Internet gateway访问Internet
                    - 
                        
                        ![https://api2.mubu.com/v3/document_image/79c5a47d-9f96-4e6e-980e-4459ed46e12f-14086676.jpg](https://api2.mubu.com/v3/document_image/79c5a47d-9f96-4e6e-980e-4459ed46e12f-14086676.jpg)
                        
                - 想让subnet public出去，可以在Explicit Subnet association, 点击Edit subnet associations
                    - Edit subnet associations
                        
                        ![https://api2.mubu.com/v3/document_image/6a58a843-5b69-4e9b-9acd-482de0fd5006-14086676.jpg](https://api2.mubu.com/v3/document_image/6a58a843-5b69-4e9b-9acd-482de0fd5006-14086676.jpg)
                        
                    - 选择想要public 的子网，save association就可以public 出去了
                        
                        ![https://api2.mubu.com/v3/document_image/2d1a413b-0dd5-43d9-9ea9-bfecbe41edac-14086676.jpg](https://api2.mubu.com/v3/document_image/2d1a413b-0dd5-43d9-9ea9-bfecbe41edac-14086676.jpg)
                        
                    - default的10.0.2.0就是private的subnet，10.0.1.0 explicit 成public子网
                        
                        ![https://api2.mubu.com/v3/document_image/c9b0fdcb-6705-49bf-a091-c0f5d421445f-14086676.jpg](https://api2.mubu.com/v3/document_image/c9b0fdcb-6705-49bf-a091-c0f5d421445f-14086676.jpg)
                        
                - 但是外部internent 需要subnet 的IP address，因此还需要给这个subnet配置一个IP address
                    - 
                        
                        ![https://api2.mubu.com/v3/document_image/b084da75-9d9f-40c7-afef-771ea83a127d-14086676.jpg](https://api2.mubu.com/v3/document_image/b084da75-9d9f-40c7-afef-771ea83a127d-14086676.jpg)
                        
                        ![https://api2.mubu.com/v3/document_image/cd138432-977a-484d-b504-9ed482e543b9-14086676.jpg](https://api2.mubu.com/v3/document_image/cd138432-977a-484d-b504-9ed482e543b9-14086676.jpg)
                        
    - 配置完了网络，才能配置EC2 ，server不然public IP不会自动生成
    - 访问public 子网
        - 终端：ssh -i 'xx.perm' ec2-user@instance子网IPadress
    - 访问private子网
        - 通过先访问public instance再去访问private 子网instance
            - scp将pem复制: scp -i ExBoto3.pem ./ExBoto3.pem ec2-user@18.234.73.202:~/
                
                ![https://api2.mubu.com/v3/document_image/99bf326a-2658-434b-977c-49c1da81bca8-14086676.jpg](https://api2.mubu.com/v3/document_image/99bf326a-2658-434b-977c-49c1da81bca8-14086676.jpg)
                
                - scp是secure copy的简写，用于在Linux下进行远程拷贝文件的命令，和它类似的命令有cp，不过cp只是在本机进行拷贝不能跨服务器，而且scp传输是加密的。
            - ssh 进public instance，再ssh进private instance中（复制private子网的private IP address）
                
                ![https://api2.mubu.com/v3/document_image/e0b3aacc-1d30-403a-a6b8-e62a059bd2a3-14086676.jpg](https://api2.mubu.com/v3/document_image/e0b3aacc-1d30-403a-a6b8-e62a059bd2a3-14086676.jpg)
                
            - 但是这样还不行，sudo yum update, private 打补丁失败
                
                ![https://api2.mubu.com/v3/document_image/d55c76b0-d418-4b2e-b6ec-5e88f54c5b4d-14086676.jpg](https://api2.mubu.com/v3/document_image/d55c76b0-d418-4b2e-b6ec-5e88f54c5b4d-14086676.jpg)
                
            - 新建一个NAT gateway (固定的public IP address）
                - Elastic IPs 是一个public的IPv4 address. 因为public Instance 在stop 后重新启动，public IP address 会发生改变，所以需要一个static的IP address（Elastic IP address)。注意：Elastic IP 申请不要钱，但是如果申请了没有连server，空在那里不用，将会被charge
                - net gateway 内网能访问外网，外网不能访问内网，单向的。
                    
                    ![https://api2.mubu.com/v3/document_image/2d47e035-b36e-47ea-9f39-6305bdaed8b7-14086676.jpg](https://api2.mubu.com/v3/document_image/2d47e035-b36e-47ea-9f39-6305bdaed8b7-14086676.jpg)
                    
                - 注意Net Gatway是要添加到public的subnet上的
                    
                    ![https://api2.mubu.com/v3/document_image/9a14899c-57c9-452f-968a-592a963dc22b-14086676.jpg](https://api2.mubu.com/v3/document_image/9a14899c-57c9-452f-968a-592a963dc22b-14086676.jpg)
                    
                - 在route table 中private IP address所在的route table 中edit route, 连到0.0.0.0/0，自动生成Target nat-0477027344e7f858c
                    
                    ![https://api2.mubu.com/v3/document_image/79f04fbd-5645-4149-a98b-7a666bac80a9-14086676.jpg](https://api2.mubu.com/v3/document_image/79f04fbd-5645-4149-a98b-7a666bac80a9-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/1cb34453-8778-48f9-be5d-b33e010e0f9b-14086676.jpg](https://api2.mubu.com/v3/document_image/1cb34453-8778-48f9-be5d-b33e010e0f9b-14086676.jpg)
                    
                - subnet ID 要与private rote table 相联系 association，两种方式。
                    - 方式一，在subnet中添加
                        
                        ![https://api2.mubu.com/v3/document_image/694b208c-a2dc-43c4-945d-c52353db4944-14086676.jpg](https://api2.mubu.com/v3/document_image/694b208c-a2dc-43c4-945d-c52353db4944-14086676.jpg)
                        
                    - 方式二，在route table 中添加
                        
                        ![https://api2.mubu.com/v3/document_image/df8be8ae-f056-475c-b1d0-ec0b812d1bd1-14086676.jpg](https://api2.mubu.com/v3/document_image/df8be8ae-f056-475c-b1d0-ec0b812d1bd1-14086676.jpg)
                        
                - 将生成的NAT 添加到private subnet的路由中（explicit subnet association )
                    
                    ![https://api2.mubu.com/v3/document_image/6f9e88bc-7913-4fa8-8a55-109e63a04e20-14086676.jpg](https://api2.mubu.com/v3/document_image/6f9e88bc-7913-4fa8-8a55-109e63a04e20-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/c6b60d71-6ca8-4409-9bc7-e2d3fc3c5cfe-14086676.jpg](https://api2.mubu.com/v3/document_image/c6b60d71-6ca8-4409-9bc7-e2d3fc3c5cfe-14086676.jpg)
                    
            - 再次sudo yum update, 现在Private instance 可以访问Internet 了，可以打补丁了
                
                ![https://api2.mubu.com/v3/document_image/ab6f3787-32ed-473f-a82c-bfe2b263db23-14086676.jpg](https://api2.mubu.com/v3/document_image/ab6f3787-32ed-473f-a82c-bfe2b263db23-14086676.jpg)
                
    - what we have now
        
        ![https://api2.mubu.com/v3/document_image/6fbe0654-561a-4be4-8e7d-fbe57a414c4f-14086676.jpg](https://api2.mubu.com/v3/document_image/6fbe0654-561a-4be4-8e7d-fbe57a414c4f-14086676.jpg)
        
    - Network control list ACL
        - 创建Network ACL
        - 实验，退出private IP，进入public IP， 安装http -y
            
            ![https://api2.mubu.com/v3/document_image/13da83f6-6357-4b31-acf5-9f8b78a3cb86-14086676.jpg](https://api2.mubu.com/v3/document_image/13da83f6-6357-4b31-acf5-9f8b78a3cb86-14086676.jpg)
            
        - 改变subnet associate
            
            ![https://api2.mubu.com/v3/document_image/cce2f21c-9da3-4b89-b746-a8be1973e7ed-14086676.jpg](https://api2.mubu.com/v3/document_image/cce2f21c-9da3-4b89-b746-a8be1973e7ed-14086676.jpg)
            
        - 在server上做出网页
            
            ![https://api2.mubu.com/v3/document_image/608584c3-1c5f-4d03-8eac-93bd8439bf60-14086676.jpg](https://api2.mubu.com/v3/document_image/608584c3-1c5f-4d03-8eac-93bd8439bf60-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/3c923787-4c6c-44e1-b09e-68e78673d2d1-14086676.jpg](https://api2.mubu.com/v3/document_image/3c923787-4c6c-44e1-b09e-68e78673d2d1-14086676.jpg)
            
        - inbound rule和outbound rule 是不联动的
            - 修改inbound rule
                
                ![https://api2.mubu.com/v3/document_image/ccd5e15b-fa8a-47dd-8475-9d6f498204e0-14086676.jpg](https://api2.mubu.com/v3/document_image/ccd5e15b-fa8a-47dd-8475-9d6f498204e0-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/478b5016-0759-4bf8-82ae-ee9f0d1deb2e-14086676.jpg](https://api2.mubu.com/v3/document_image/478b5016-0759-4bf8-82ae-ee9f0d1deb2e-14086676.jpg)
                
            - 除了修改inbound rule还要修改outbound rule。并且的多加一条，port range是1024-65535。因为1024之前的port都是被reserve了的，例如80 是HTTP，
                
                ![https://api2.mubu.com/v3/document_image/ecc600cf-a32c-4a70-915c-367e6d0d99c6-14086676.jpg](https://api2.mubu.com/v3/document_image/ecc600cf-a32c-4a70-915c-367e6d0d99c6-14086676.jpg)
                
            - 再去访问public instance的public IP address，出现网页
                
                ![https://api2.mubu.com/v3/document_image/ee6ace6a-afe0-497c-8d46-d560cff80a0f-14086676.jpg](https://api2.mubu.com/v3/document_image/ee6ace6a-afe0-497c-8d46-d560cff80a0f-14086676.jpg)
                
            - 改inbound rule使其HTTP不能访问，并且Rule number是有优先级之分的，rule number越小，越优先，优先执行rule number小的rule
                
                ![https://api2.mubu.com/v3/document_image/077bd1a8-1666-43a0-a192-2ac2c81d73a1-14086676.jpg](https://api2.mubu.com/v3/document_image/077bd1a8-1666-43a0-a192-2ac2c81d73a1-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/a5051b08-39d2-40f1-9c12-072205f8fa95-14086676.jpg](https://api2.mubu.com/v3/document_image/a5051b08-39d2-40f1-9c12-072205f8fa95-14086676.jpg)
                
            - 设计rule的时候不要1，2，3，4这样设，一定要留有buffer以给将来留下更改的空间，最好100，200，这样留有buffer的设置
                
                ![https://api2.mubu.com/v3/document_image/97c85de5-7af3-4a50-81f0-48afee466e6b-14086676.jpg](https://api2.mubu.com/v3/document_image/97c85de5-7af3-4a50-81f0-48afee466e6b-14086676.jpg)
                
            - port range 2:23
                
                ![https://api2.mubu.com/v3/document_image/11fa7c85-2cc5-4cb6-a420-b2fbfdc411ac-14086676.jpg](https://api2.mubu.com/v3/document_image/11fa7c85-2cc5-4cb6-a420-b2fbfdc411ac-14086676.jpg)
                
            - network ACL 中inbound和outbound rule更改是立即生效的。
        - 如果想将subnet 更改ACL，只需要在要加到的ACL下面edit subnet association就可以了，把想要的subnet加进来，subnet就会从原来的ACL中退出。
            
            ![https://api2.mubu.com/v3/document_image/ed7c83db-848f-439f-9090-2a9884d807ac-14086676.jpg](https://api2.mubu.com/v3/document_image/ed7c83db-848f-439f-9090-2a9884d807ac-14086676.jpg)
            
        - summary
            
            ![https://api2.mubu.com/v3/document_image/ffc63656-bea7-487f-a7d7-3855a362a37e-14086676.jpg](https://api2.mubu.com/v3/document_image/ffc63656-bea7-487f-a7d7-3855a362a37e-14086676.jpg)
            
- VPC endpoint
    - endpoint可以允许我们通过私有网络去访问AWS 的一些server 而不用通过NAT gateway，不走公有网络，更安全更快
        
        ![https://api2.mubu.com/v3/document_image/9bd33286-3b1d-44f0-a236-152743c6231e-14086676.jpg](https://api2.mubu.com/v3/document_image/9bd33286-3b1d-44f0-a236-152743c6231e-14086676.jpg)
        
    - 实验：
        - 为了让private instance不用net gateway连网，在Edit route中remove掉NAT gateway.
            - 
                
                ![https://api2.mubu.com/v3/document_image/5df3e855-af46-4f17-9aa2-f95274e7ff42-14086676.jpg](https://api2.mubu.com/v3/document_image/5df3e855-af46-4f17-9aa2-f95274e7ff42-14086676.jpg)
                
        - create endpoint
            - 创建 Gatway与想要连的subnet关联，这里用的是private subnet。
                
                ![https://api2.mubu.com/v3/document_image/3a2ff096-caa0-4f54-9aac-2e8ef4facb07-14086676.jpg](https://api2.mubu.com/v3/document_image/3a2ff096-caa0-4f54-9aac-2e8ef4facb07-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/67b134f1-5119-44a4-b492-1f9402c54963-14086676.jpg](https://api2.mubu.com/v3/document_image/67b134f1-5119-44a4-b492-1f9402c54963-14086676.jpg)
                
            - 
                
                ![https://api2.mubu.com/v3/document_image/c69dbc9e-6dd9-4fea-a456-2f463926680f-14086676.jpg](https://api2.mubu.com/v3/document_image/c69dbc9e-6dd9-4fea-a456-2f463926680f-14086676.jpg)
                
        - 创建了Endpoint之后，会再route table中的route中出现
            - 
                
                ![https://api2.mubu.com/v3/document_image/439b90dd-6f6f-477d-9bc7-a3053d5aab98-14086676.jpg](https://api2.mubu.com/v3/document_image/439b90dd-6f6f-477d-9bc7-a3053d5aab98-14086676.jpg)
                
        - 现在，private instance 就无法访问Internet了，但是可以通过endpoint访问S3
            - 
                
                ![https://api2.mubu.com/v3/document_image/774eef21-225f-4b09-8916-0ceceb2dd545-14086676.jpg](https://api2.mubu.com/v3/document_image/774eef21-225f-4b09-8916-0ceceb2dd545-14086676.jpg)
                
    - EC2 通过NAT gateway 访问S3的方式
        - 
            
            ![https://api2.mubu.com/v3/document_image/d47361fb-868f-406c-aacf-620a3bc252f8-14086676.jpg](https://api2.mubu.com/v3/document_image/d47361fb-868f-406c-aacf-620a3bc252f8-14086676.jpg)
            
    - 通过Endpoint 在AWS服务内部，跳过NAT gateway访问S3
        
        ![https://api2.mubu.com/v3/document_image/6cb15d56-49df-4c23-8928-9a94a6d89819-14086676.jpg](https://api2.mubu.com/v3/document_image/6cb15d56-49df-4c23-8928-9a94a6d89819-14086676.jpg)
        
- VPC clean up 否则会产生费用
    - step 1.首先要terminate EC2 instance
    - 2. 删除Endpoint
    - 3.删除Internet Gateway
        - 先要detach internet gateway
            - 然后在route table中去除association , 保证route table没有在用，从而可以删除route table
                
                ![https://api2.mubu.com/v3/document_image/1aafdd10-d6de-4a0d-b6ed-8f48823d9b92-14086676.jpg](https://api2.mubu.com/v3/document_image/1aafdd10-d6de-4a0d-b6ed-8f48823d9b92-14086676.jpg)
                
            - 删掉NET gateway
            - 最后才能 detach internet gateway
        - 再delete Internet Gateway
    - 4. release Elastic IP address
        - 
            
            ![https://api2.mubu.com/v3/document_image/2acb198a-d22b-46ef-962b-a13f93c10a63-14086676.jpg](https://api2.mubu.com/v3/document_image/2acb198a-d22b-46ef-962b-a13f93c10a63-14086676.jpg)
            
- VPN （2：26）
    - 创建VPN
        
        ![https://api2.mubu.com/v3/document_image/c7fcd891-9237-4c1e-8c0a-c5a8269756b7-14086676.jpg](https://api2.mubu.com/v3/document_image/c7fcd891-9237-4c1e-8c0a-c5a8269756b7-14086676.jpg)
        
        ![https://api2.mubu.com/v3/document_image/167efbad-9756-47c8-ad02-af68ac776f2c-14086676.jpg](https://api2.mubu.com/v3/document_image/167efbad-9756-47c8-ad02-af68ac776f2c-14086676.jpg)
        
    - 
        
        ![https://api2.mubu.com/v3/document_image/e4df33b2-5d11-478e-9539-17ed3b34782d-14086676.jpg](https://api2.mubu.com/v3/document_image/e4df33b2-5d11-478e-9539-17ed3b34782d-14086676.jpg)
        
- VPC 的精华，在未来工作中，安全性设计上是非常有用的，架构师必备
    
    ![https://api2.mubu.com/v3/document_image/5e292d51-66b4-47ae-90c2-76b2ee9c80f1-14086676.jpg](https://api2.mubu.com/v3/document_image/5e292d51-66b4-47ae-90c2-76b2ee9c80f1-14086676.jpg)