# Lecture08 AWS Messaging

- 0. 导读
    - 1.本节课操作很多，两个重点Lambda和SQS
    - 2.思维导图
        - 
            
            ![https://api2.mubu.com/v3/document_image/369ee5d1-163b-490f-b2a4-0d70851e7be5-14086676.jpg](https://api2.mubu.com/v3/document_image/369ee5d1-163b-490f-b2a4-0d70851e7be5-14086676.jpg)
            
- 1. EBS
    - terminate instance之后还会将数据留在EBS中
    - terminate instance 后要记得手动删掉EBS（EBS会有cost）
    - EBS，做完实验过后，不要留EBS
        
        ![https://api2.mubu.com/v3/document_image/9c5907a6-f00a-4277-9286-556d76e4fb59-14086676.jpg](https://api2.mubu.com/v3/document_image/9c5907a6-f00a-4277-9286-556d76e4fb59-14086676.jpg)
        
        ![https://api2.mubu.com/v3/document_image/7bc7a3bd-8051-453f-8f1e-b1147e4932ca-14086676.jpg](https://api2.mubu.com/v3/document_image/7bc7a3bd-8051-453f-8f1e-b1147e4932ca-14086676.jpg)
        
- 2. Lambda
    - 1. aws的一个service，compute service
        - 
            
            ![https://api2.mubu.com/v3/document_image/42ae64be-5a3d-4f1d-9fe4-74c9ee03a065-14086676.jpg](https://api2.mubu.com/v3/document_image/42ae64be-5a3d-4f1d-9fe4-74c9ee03a065-14086676.jpg)
            
        - 只用upload code就行了，不用考虑操作系统等问题。
            - 
                
                ![https://api2.mubu.com/v3/document_image/94d41bc5-3e21-4cb5-88bb-77b9f719043d-14086676.jpg](https://api2.mubu.com/v3/document_image/94d41bc5-3e21-4cb5-88bb-77b9f719043d-14086676.jpg)
                
        - Event-driven compute service, 事件会触发response 去运行lambda.
        - Lambda 还可以Scheduling 现在在eventBridge 里
            - 
                
                ![https://api2.mubu.com/v3/document_image/16615d2c-4f33-408a-b056-eb0c24794369-14086676.jpg](https://api2.mubu.com/v3/document_image/16615d2c-4f33-408a-b056-eb0c24794369-14086676.jpg)
                
        - API Gateway
        - example
            
            ![https://api2.mubu.com/v3/document_image/606b7c8d-e210-4ba0-91ab-17d48a5dca94-14086676.jpg](https://api2.mubu.com/v3/document_image/606b7c8d-e210-4ba0-91ab-17d48a5dca94-14086676.jpg)
            
    - 2、lambda 特点
        - 1. 上传代码特点
            - 1.直接写
            - 2. Zip打包上传
            - 3. S3 上传代码
                
                ![https://api2.mubu.com/v3/document_image/9aa29af7-bb40-49a6-8869-17f41d3ae952-14086676.jpg](https://api2.mubu.com/v3/document_image/9aa29af7-bb40-49a6-8869-17f41d3ae952-14086676.jpg)
                
        - Layers 可以使我们使用其它的包，例如panda
        - lambda 时长和运行memory设置
            
            ![https://api2.mubu.com/v3/document_image/021b53c0-78ba-443e-a6de-33b92f58e020-14086676.jpg](https://api2.mubu.com/v3/document_image/021b53c0-78ba-443e-a6de-33b92f58e020-14086676.jpg)
            
        - Asynchronous (0:48)
            
            ![https://api2.mubu.com/v3/document_image/4979a33f-013d-4937-9762-8838214d17a9-14086676.jpg](https://api2.mubu.com/v3/document_image/4979a33f-013d-4937-9762-8838214d17a9-14086676.jpg)
            
        - runtime setting
            
            ![https://api2.mubu.com/v3/document_image/457f6c5e-ef1b-4a30-bc4f-efff4cdc6b38-14086676.jpg](https://api2.mubu.com/v3/document_image/457f6c5e-ef1b-4a30-bc4f-efff4cdc6b38-14086676.jpg)
            
        - file system，共享磁盘一样，不想放到S3 或Database 中
            
            ![https://api2.mubu.com/v3/document_image/80409814-7583-4f3f-a3e8-ffd3a239aea5-14086676.jpg](https://api2.mubu.com/v3/document_image/80409814-7583-4f3f-a3e8-ffd3a239aea5-14086676.jpg)
            
        - state machine
            
            ![https://api2.mubu.com/v3/document_image/dfcbe8ea-558f-46aa-9454-6d9aa3109006-14086676.jpg](https://api2.mubu.com/v3/document_image/dfcbe8ea-558f-46aa-9454-6d9aa3109006-14086676.jpg)
            
        - AB test 中可能会用到version，不同的访问者使用不同的lambda
            
            ![https://api2.mubu.com/v3/document_image/46b426e2-dcc2-414d-82e0-6d3157a5dc6e-14086676.jpg](https://api2.mubu.com/v3/document_image/46b426e2-dcc2-414d-82e0-6d3157a5dc6e-14086676.jpg)
            
- 3.Lambda 实验
    - 1. Lambda 与 EC2 交互，自动开启EC2 (lecture 8 00:57:00)
        - 
            
            ![https://api2.mubu.com/v3/document_image/369bd94e-a8d0-474c-a07e-96544aeec094-14086676.jpg](https://api2.mubu.com/v3/document_image/369bd94e-a8d0-474c-a07e-96544aeec094-14086676.jpg)
            
    - 作业，running state 状态，用lambda自动关闭EC2
    - 2. Lambda 与 S3 交互。测试trigger lambda function （lecture 8 1:22:00）
        - boto3 client与resource的区别在于，client更底层
        - S3 中上传文件时(注意上传的文件名不能有空格不能是中文，否者会报404，无法找到object），触发lambda function, 将文件复制到source s3中
            - 
                
                ![https://api2.mubu.com/v3/document_image/a6b22758-356e-414a-bdc0-0c86ab6e5c21-14086676.jpg](https://api2.mubu.com/v3/document_image/a6b22758-356e-414a-bdc0-0c86ab6e5c21-14086676.jpg)
                
        - 用环境变量，替代hardcode: dest_bucket =“jr202203-lee-dst”. (lecture 8 1:25)
            - os.environ['DEST_BUCKET'], 同时需要在config中配置环境变量
                
                ![https://api2.mubu.com/v3/document_image/b8620b3f-7bb1-4a2e-a05d-0defbd2a502a-14086676.jpg](https://api2.mubu.com/v3/document_image/b8620b3f-7bb1-4a2e-a05d-0defbd2a502a-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/d87c23ec-42f6-4ba5-a8e2-857e3e67240e-14086676.jpg](https://api2.mubu.com/v3/document_image/d87c23ec-42f6-4ba5-a8e2-857e3e67240e-14086676.jpg)
                
    - 3. Lambda 与 EC2 ， S3 交互，注意开role权限
        - 1.没有给role权限，lambda无法访问s3，只能写log
            - 
                
                ![https://api2.mubu.com/v3/document_image/db04f835-a8ca-4539-b188-fc395fc55c0a-14086676.jpg](https://api2.mubu.com/v3/document_image/db04f835-a8ca-4539-b188-fc395fc55c0a-14086676.jpg)
                
        - 2.在lambda中给s3访问读写权限
            - add s3fullaccess policy
                
                ![https://api2.mubu.com/v3/document_image/9feab066-5619-4521-8a79-1e4ffa883977-14086676.jpg](https://api2.mubu.com/v3/document_image/9feab066-5619-4521-8a79-1e4ffa883977-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/713fabe8-a7cf-4f42-a6fe-786e37765b1c-14086676.jpg](https://api2.mubu.com/v3/document_image/713fabe8-a7cf-4f42-a6fe-786e37765b1c-14086676.jpg)
                
        - 活用boto3包
- 4.lambda总结
    - 1. 需要记住
        
        ![https://api2.mubu.com/v3/document_image/5e5045f6-65e2-4831-9d27-bc157c1e160b-14086676.jpg](https://api2.mubu.com/v3/document_image/5e5045f6-65e2-4831-9d27-bc157c1e160b-14086676.jpg)
        
    - 2. How is Lambda Priced
        - 
            
            ![https://api2.mubu.com/v3/document_image/5f7d3813-7d92-4cf1-83a2-c0845e42cafc-14086676.jpg](https://api2.mubu.com/v3/document_image/5f7d3813-7d92-4cf1-83a2-c0845e42cafc-14086676.jpg)
            
    - 3.
        
        ![https://api2.mubu.com/v3/document_image/5fac68a9-de3b-4cf8-b823-82e739597d07-14086676.jpg](https://api2.mubu.com/v3/document_image/5fac68a9-de3b-4cf8-b823-82e739597d07-14086676.jpg)
        
- 5. SNS
    - 帮我们发notification给subscriber
        
        ![https://api2.mubu.com/v3/document_image/2823c967-c18b-4678-b8eb-583f8c0b6582-14086676.jpg](https://api2.mubu.com/v3/document_image/2823c967-c18b-4678-b8eb-583f8c0b6582-14086676.jpg)
        
    - 当有人把message push到 SNS topic ， lambda trigger一个notification
    - pub-sub model
        
        ![https://api2.mubu.com/v3/document_image/3d538958-3ec9-4c0b-be97-28ccb1273d4b-14086676.jpg](https://api2.mubu.com/v3/document_image/3d538958-3ec9-4c0b-be97-28ccb1273d4b-14086676.jpg)
        
    - 没有延迟，立即给所有的subscriber发notification
        
        ![https://api2.mubu.com/v3/document_image/54289e66-ce97-4440-94db-4de71b8fbe34-14086676.jpg](https://api2.mubu.com/v3/document_image/54289e66-ce97-4440-94db-4de71b8fbe34-14086676.jpg)
        
    - SNS benefits
        - no polling ， 不需要去拿
            
            ![https://api2.mubu.com/v3/document_image/6cd00ac3-1374-4890-872f-d655a15fd52d-14086676.jpg](https://api2.mubu.com/v3/document_image/6cd00ac3-1374-4890-872f-d655a15fd52d-14086676.jpg)
            
        - API 简单，很容易integration
        - 不同协议的信息传递，非常灵活
        - PAYG
        - 容易配置
        - Managed service 可以保持高availiability
- 6. SQS
    - queue 是一个临时的message 等待处理的repository
    - 一个buffer介于接收数据等待处理和产生数据saving数据之间。
    - SNS 发到Topic后立马发给subscriber，SQS先储存到buffer中，什么时候处理是有之后的process确定什么时候处理的
        
        ![https://api2.mubu.com/v3/document_image/0ddfe56e-9617-4c9b-98ec-11bde6b445c6-14086676.jpg](https://api2.mubu.com/v3/document_image/0ddfe56e-9617-4c9b-98ec-11bde6b445c6-14086676.jpg)
        
    - SQS Features （知道就行）
        
        ![https://api2.mubu.com/v3/document_image/092e502e-79f0-4b9b-9c99-7a5a04646264-14086676.jpg](https://api2.mubu.com/v3/document_image/092e502e-79f0-4b9b-9c99-7a5a04646264-14086676.jpg)
        
        - decouple application components的意思是，假设有component A 和componentB， componentA 做完一项内容后，放在SQS中，继续做后面的内容，不用等component B 空闲下来能做componentA完成的项目后，才能继续做后续的内容。
            - 如果不SQS：A ——>B , B如果没有空闲下来， A就一直在被这个任务占据，不能处理其它任务，直到B开始处理AB要处理的任务，A才开始释放出来，做别的任务
            - 有SQS后： A-->B , B没哟空闲下来，A处理完这个任务后，可以把这个任务丢到SQS中，B有没有空闲都不会让A被这个任务占据，使得A 可以处理其它的任务，无疑这会提高处理效率。
        - standard queue不能保证顺序，message A， B， C 可能先拿到message B ，可处理多次。 FIFO有顺序，只处理一次。FIFO enforces ordering in which messages are sent and received, and avoids that a message is processed multiple times.
    - SQS key facts
        - 要去拿，Pull，不同SNS 是push based的。
            
            ![https://api2.mubu.com/v3/document_image/f7f5da3a-3daa-4193-ad7d-f169bcb8105c-14086676.jpg](https://api2.mubu.com/v3/document_image/f7f5da3a-3daa-4193-ad7d-f169bcb8105c-14086676.jpg)
            
        - 储存text data
        - 至少处理一次
        - message最多存14天在queue里，是一个temperaly 的repository，默认保留时间是4天
    - SNS VS SQS
        
        ![https://api2.mubu.com/v3/document_image/ad42e85e-706a-4cdc-83c3-7b8cdf9f4fd6-14086676.jpg](https://api2.mubu.com/v3/document_image/ad42e85e-706a-4cdc-83c3-7b8cdf9f4fd6-14086676.jpg)
        
        - SQS 比较经典的，能decoupling 2 application components
        - SNS是不存数据的，SQS是会存数据的。
        - consumer type SNS 是不一样的，例如email，SMS发出去； 而SQS发出的message 接收的consumer （process）是一样的, 被一个consumer处理一次。
- 7. SNS实验
    - topic -》subscriber--》message details
        
        ![https://api2.mubu.com/v3/document_image/852695b2-892c-44af-87de-aa56671cf7b1-14086676.jpg](https://api2.mubu.com/v3/document_image/852695b2-892c-44af-87de-aa56671cf7b1-14086676.jpg)
        
    - 这个message协议可以也可以设置成Lambda，让它trigger一个function
        
        ![https://api2.mubu.com/v3/document_image/d273e874-cabd-4968-b21e-edeb9ec9f637-14086676.jpg](https://api2.mubu.com/v3/document_image/d273e874-cabd-4968-b21e-edeb9ec9f637-14086676.jpg)
        
    - message details，可以identical payload for all delivery 也可以Custom payload for each delivery protocol (不同类型的subscriber接受不同的信息)
        
        ![https://api2.mubu.com/v3/document_image/6a9a9f55-566d-4db5-818f-ac39d1892535-14086676.jpg](https://api2.mubu.com/v3/document_image/6a9a9f55-566d-4db5-818f-ac39d1892535-14086676.jpg)
        
    - publish message 之后手机和邮箱就能收到刚刚编辑的message
- 8.sqs 实验。重点！！SQS config visible 等等的time
    - 1. visibility timeout
        - 蓝人A 拿到message 1 对其processing，message 1 就会从visible 变成invisible, 对绿人B 就看不到message 1 了只能看到message 2，它是message visible的时间长度
            
            ![https://api2.mubu.com/v3/document_image/bbed1ab0-e488-4a72-8baf-50947fac8faf-14086676.jpg](https://api2.mubu.com/v3/document_image/bbed1ab0-e488-4a72-8baf-50947fac8faf-14086676.jpg)
            
        - Visibility timeout，当“我”处理时，不要被别的process看到，多少时间后又会被visible 。
            
            ![https://api2.mubu.com/v3/document_image/805cbda9-cbdc-440f-bac4-58e95a99bd7a-14086676.jpg](https://api2.mubu.com/v3/document_image/805cbda9-cbdc-440f-bac4-58e95a99bd7a-14086676.jpg)
            
        - 这样做的目的是：
        - 1. 确保不被重复process;
        - 2. 如果message长时间没有处理完的话，SQS assume 这个process自己time out了，queue message没有被真正的处理，所以会让这个message重新变得avaliable起来。
    - 2. message retention period
        - message在SQS中保留的时间，例如保留四天，四天之后删除
            
            ![https://api2.mubu.com/v3/document_image/fa828e6f-1f8f-4d13-90a1-aa6ebbf18626-14086676.jpg](https://api2.mubu.com/v3/document_image/fa828e6f-1f8f-4d13-90a1-aa6ebbf18626-14086676.jpg)
            
    - 3. delivery delay
        - user push message 给SQS，在SQS中invisible的时间长度，0-15minus
        - 小红人发出一个message，不想立刻被小黄人处理这个message， 例如delay 30分钟（这里是假设，实际最长不超过15分钟），那小黄人，只有在30分钟后才能拿到这个message
            
            ![https://api2.mubu.com/v3/document_image/83beb079-7564-4555-85de-8efd6decae78-14086676.jpg](https://api2.mubu.com/v3/document_image/83beb079-7564-4555-85de-8efd6decae78-14086676.jpg)
            
        - message还不在queue里
    - 4. Maximum message size
    - 5. receive message wait time
        - 小绿人问SQS有没有message，等待的最大时间。例如小绿人去SQS中拿queue，如果有就立即返回，如果没有，小绿人等十秒，如果这十秒以内，有了message，小绿拿到后立马返回，如果没有message，小绿就一直等，直到等够10秒才会返回。
            
            ![https://api2.mubu.com/v3/document_image/315d66b9-dcfc-41d5-b57d-5d5f96616eab-14086676.jpg](https://api2.mubu.com/v3/document_image/315d66b9-dcfc-41d5-b57d-5d5f96616eab-14086676.jpg)
            
        - 防止频繁询问message（API call），类似设定一个loop，10s wait time，每隔10s访问一次，不然就会Loop（例如设置0.01秒重新访问）一结束就访问，不停的“轰炸”服务器，浪费资源和产生cost
    - 6. Dead-letter queue
        - 如果message 没有deliver 出去，会丢到Dead-letter queue。for some reasons, 不知道message为什么没有deliver 出去，一般来Dead-letter queue看看出了什么问题。
        - 如果这个queue是FIFO，那Dead letter queue也是FIFO dead letter queue，如果是Standard queue，那Dead letter queue也是Standard dead letter queue
    - 7. SQS FIFO Deduplication scope (如何做deduplication)
        - 1. Queue 选项： 所有的message都不能有冗余重复
            
            ![https://api2.mubu.com/v3/document_image/97fd039f-110e-4998-a2e8-6a19685b1af4-14086676.jpg](https://api2.mubu.com/v3/document_image/97fd039f-110e-4998-a2e8-6a19685b1af4-14086676.jpg)
            
        - 2. Message group： 要加Message group ID，group内不能有冗余，group之间可以有冗余。例如小黄人拿Message Group 1， 是排好序了的，一定拿1-2-3-4；拿message group 2 时，一定是5-6-7-8；但是小黄人同时从两个group里拿的时候，我可能拿到的是5-6-1-2-3-7-4-8，group2 中的5、6虽然是后进入到SQS 的，但是“我”也可能先拿到5-6，因为message group是不一样的。这就是message group的一个作用。
            
            ![https://api2.mubu.com/v3/document_image/ca2a5a3f-fd0e-48d3-a70a-31fa5f7b6036-14086676.jpg](https://api2.mubu.com/v3/document_image/ca2a5a3f-fd0e-48d3-a70a-31fa5f7b6036-14086676.jpg)
            
    - 8. Content-based deduplication
        - 发message的时候，SQS会给message一个ID，通过识别ID不同判断message不同
            
            ![https://api2.mubu.com/v3/document_image/f60c79a7-a337-4495-a763-1dc3dae83f01-14086676.jpg](https://api2.mubu.com/v3/document_image/f60c79a7-a337-4495-a763-1dc3dae83f01-14086676.jpg)
            
        - 不勾选是通过deduplication ID 判断两个queue是否一样，如果勾选了是通过内容来判断queue是否一样
            
            ![https://api2.mubu.com/v3/document_image/d122ef32-a065-41ff-88da-dda8eb9e1f68-14086676.jpg](https://api2.mubu.com/v3/document_image/d122ef32-a065-41ff-88da-dda8eb9e1f68-14086676.jpg)
            
    - 9. 基本实验操作：
        - 1.建SQS
            - 
                
                ![https://api2.mubu.com/v3/document_image/4504220b-9b75-4844-ae0d-67cb0d80bd14-14086676.jpg](https://api2.mubu.com/v3/document_image/4504220b-9b75-4844-ae0d-67cb0d80bd14-14086676.jpg)
                
        - 2. 将这个SQS subscribe to SNS topic
            - 
                
                ![https://api2.mubu.com/v3/document_image/5465017b-121c-4031-aa16-3059817a8cb5-14086676.jpg](https://api2.mubu.com/v3/document_image/5465017b-121c-4031-aa16-3059817a8cb5-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/1d048950-4ca7-4bb5-a758-aade97352a1d-14086676.jpg](https://api2.mubu.com/v3/document_image/1d048950-4ca7-4bb5-a758-aade97352a1d-14086676.jpg)
                
        - 3. send and receive messages
            - 1.send message
                
                ![https://api2.mubu.com/v3/document_image/2d487c8a-ccee-47c4-92d8-4054a4e54d4d-14086676.jpg](https://api2.mubu.com/v3/document_image/2d487c8a-ccee-47c4-92d8-4054a4e54d4d-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/1ef8b8d4-2efd-4397-b1f3-fc26cbc6d5f8-14086676.jpg](https://api2.mubu.com/v3/document_image/1ef8b8d4-2efd-4397-b1f3-fc26cbc6d5f8-14086676.jpg)
                
            - 2.send完之后，就可以retrieve 这个message
                - 点击Poll for message就可以拿到刚刚的message
                    
                    ![https://api2.mubu.com/v3/document_image/68ad8a4a-423f-4d4b-b053-e5d4bbed122d-14086676.jpg](https://api2.mubu.com/v3/document_image/68ad8a4a-423f-4d4b-b053-e5d4bbed122d-14086676.jpg)
                    
                - 点开这个message就会出现Details，Body， Attributes等信息（attributes就跟meta data一样，可以在之前send中添加）
                    
                    ![https://api2.mubu.com/v3/document_image/97e68f9e-7970-4373-aabf-dff1246ed935-14086676.jpg](https://api2.mubu.com/v3/document_image/97e68f9e-7970-4373-aabf-dff1246ed935-14086676.jpg)
                    
        - 4. 在 SNS中publish message给SQS
            - SNS中publish message
                
                ![https://api2.mubu.com/v3/document_image/d581090e-f979-4106-bbfd-89a3d79663ca-14086676.jpg](https://api2.mubu.com/v3/document_image/d581090e-f979-4106-bbfd-89a3d79663ca-14086676.jpg)
                
        - 5. 再poll for message ， 就能看到新的message， 通过JSON的解析，拿到相应的内容
            - 查看Body
                
                ![https://api2.mubu.com/v3/document_image/816a7d36-6b1d-4bce-b18a-1ed4899ff6fc-14086676.jpg](https://api2.mubu.com/v3/document_image/816a7d36-6b1d-4bce-b18a-1ed4899ff6fc-14086676.jpg)
                
            - body 的内容：
                - {
                - "Type" : "Notification",
                - "MessageId" : "dc80d5fe-fbc9-5f07-8437-8f039cdb89ef",
                - "TopicArn" : "arn:aws:sns:ap-southeast-2:017047278558:MyTopic",
                - "Message" : "Sample message for Amazon SQS endpoints",
                - "Timestamp" : "2022-05-17T09:03:14.924Z",
                - "SignatureVersion" : "1",
                - "Signature" : "NhQOMS0wsqnbhBcs1LzHaxfGYOe9IO6SezuNiMm6ML3ywHZ8gxHERB8rVz9u8TqZ7gf2bM1DUYoj2DEqnVxTXbF8Sxm4d3WGmaHI/JkjDA+eDuQG86sq53lwoMCVzU4+16/yMkDAVvDIbtMAqsZjh3tS85PQvSuGnHXx3hWhY3tKpqqL3+HBq82dRretIO6YNp2KE+ercosCTaAvPKzDGlC+0wyfGvg7pVTXtcPY6Eu6I8Yl0CTaNJWmnKFY/xW8MgMmRSU06MricGzJMyOcicNJjCughk8rFNiRHmuVyy3D6h5K/HhAph/A+GhWDpaSQqcC4HbhlmmskSMMuI1FfQ==",
                - "SigningCertURL" : "https://sns.ap-southeast-2.amazonaws.com/SimpleNotificationService-7ff5318490ec183fbaddaa2a969abfda.pem",
                - "UnsubscribeURL" : "https://sns.ap-southeast-2.amazonaws.com/?Action=Unsubscribe&SubscriptionArn=arn:aws:sns:ap-southeast-2:017047278558:MyTopic:15e9def6-95a6-4761-b7ea-8fe2708baf04"
                - }
            - 
        - 6. SQS FIFO type 操作不同
            - 1. 建SQS FIFO类型 时， 与Standard的不同点
                - 1.必须要在name中加.fifo
                    
                    ![https://api2.mubu.com/v3/document_image/c4fc217e-0739-4679-9295-4c2a932505ee-14086676.jpg](https://api2.mubu.com/v3/document_image/c4fc217e-0739-4679-9295-4c2a932505ee-14086676.jpg)
                    
                - 2. 注意有与Standard不同的两个地方
                    - 1.Deduplication scope 和 2. Content-based deduplication （上一大节点的7.8点有详细解释）
                        
                        ![https://api2.mubu.com/v3/document_image/6b8f168a-9d76-4fc5-a785-451f28d5a574-14086676.jpg](https://api2.mubu.com/v3/document_image/6b8f168a-9d76-4fc5-a785-451f28d5a574-14086676.jpg)
                        
            - 2. 实验--不勾选Content-based duplication ID
                - 1.要手动添加Message deduplication ID, 而且每个不同的message 必须要设定不同的Message deduplication ID（Message Group ID 设置成不同的ID是没用的）， 不然message将会是第一次使用Message deduplication ID的Body。
                    - 
                        
                        ![https://api2.mubu.com/v3/document_image/5c3dc642-f70a-4578-9671-f200487fc880-14086676.jpg](https://api2.mubu.com/v3/document_image/5c3dc642-f70a-4578-9671-f200487fc880-14086676.jpg)
                        
                        ![https://api2.mubu.com/v3/document_image/0ef1c719-83c6-469a-a242-b35be1b86647-14086676.jpg](https://api2.mubu.com/v3/document_image/0ef1c719-83c6-469a-a242-b35be1b86647-14086676.jpg)
                        
                - 2. Message deduplication ID相同，message group不同，message就发不出来了，还是第一次创Message deduplication ID的message
                    - 第一次
                        
                        ![https://api2.mubu.com/v3/document_image/3bc405e6-4846-4b49-b693-e42bcc38d32b-14086676.jpg](https://api2.mubu.com/v3/document_image/3bc405e6-4846-4b49-b693-e42bcc38d32b-14086676.jpg)
                        
                    - 第二次该group ID结果与第一次body内容相同，md1g2并未上传更新，被去重了
                        
                        ![https://api2.mubu.com/v3/document_image/9bfc1f06-d15a-4fc1-a4b4-405faae60ad9-14086676.jpg](https://api2.mubu.com/v3/document_image/9bfc1f06-d15a-4fc1-a4b4-405faae60ad9-14086676.jpg)
                        
                    - 第三次，只改Group ID同样被去重了
                        
                        ![https://api2.mubu.com/v3/document_image/bc79dcee-4179-48af-8bfb-901d1e26001d-14086676.jpg](https://api2.mubu.com/v3/document_image/bc79dcee-4179-48af-8bfb-901d1e26001d-14086676.jpg)
                        
                - 3.设置不同的Message deduplication ID，但是相同的Message Group ID后，message也能send出来，且body内容可以改变了，不会被去重
                    - 
                        
                        ![https://api2.mubu.com/v3/document_image/13817e6f-3a12-4ae5-aebd-14e6947e04fc-14086676.jpg](https://api2.mubu.com/v3/document_image/13817e6f-3a12-4ae5-aebd-14e6947e04fc-14086676.jpg)
                        
                - 总结，Message deduplication ID > Message group ID, 通过Message deduplication ID发送不同的message，即message是根据Message deduplication ID来判断去不去重的
            - 3. 实验--勾选Content-based duplication ID ，比较方便
                - 勾选Content-based duplication ID ，就不必强制输入Content-based duplication ID ，变成optional的了。因为，AWS会根据内容进行算法转换，形成唯一的Content-based duplication ID
                    
                    ![https://api2.mubu.com/v3/document_image/63841c43-0dc3-462e-8618-aaf760306109-14086676.jpg](https://api2.mubu.com/v3/document_image/63841c43-0dc3-462e-8618-aaf760306109-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/a2cda757-1c58-4dfa-9707-7cdf84928cfa-14086676.jpg](https://api2.mubu.com/v3/document_image/a2cda757-1c58-4dfa-9707-7cdf84928cfa-14086676.jpg)
                    
    - 10. 与lambda联动操作：
        - 1. 建一个SQS event trigger的 lambda function
        - 2. 写一个看SQS message的Python script
            - [https://www.notion.so/AWS-Lambda-653891eb6afd46deb4d998b7289e5edf#f6ef4c4088294ddfa32ab11fa8e3d787](https://www.notion.so/AWS-Lambda-653891eb6afd46deb4d998b7289e5edf)
        - 3. 给lambda SQS权限
            - 点击Edit，进入basic setting，选择role
                
                ![https://api2.mubu.com/v3/document_image/afa79007-4e2e-43e8-821a-5e676f023969-14086676.jpg](https://api2.mubu.com/v3/document_image/afa79007-4e2e-43e8-821a-5e676f023969-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/a346ff5f-4e9c-4824-8c57-cf5fdd533442-14086676.jpg](https://api2.mubu.com/v3/document_image/a346ff5f-4e9c-4824-8c57-cf5fdd533442-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/584795e3-6407-439e-8efb-2736f2584f83-14086676.jpg](https://api2.mubu.com/v3/document_image/584795e3-6407-439e-8efb-2736f2584f83-14086676.jpg)
                
        - 4. 添加SQS trigger
            - 
                
                ![https://api2.mubu.com/v3/document_image/c5602ca9-e086-4516-a690-b7c85b760fab-14086676.jpg](https://api2.mubu.com/v3/document_image/c5602ca9-e086-4516-a690-b7c85b760fab-14086676.jpg)
                
        - 5.在SQS中send message就能在Lambda中trigger出来
            - 
                
                ![https://api2.mubu.com/v3/document_image/75ab2326-0888-4622-89b4-12a0c555b801-14086676.jpg](https://api2.mubu.com/v3/document_image/75ab2326-0888-4622-89b4-12a0c555b801-14086676.jpg)
                
        - 6. 在Monitor CloudWatch 中就可以看到SQS event的详细内容了
            - SQS event的详细内容
                
                ![https://api2.mubu.com/v3/document_image/31fb5cac-2bd9-46c1-b5ea-2f17551b02ca-14086676.jpg](https://api2.mubu.com/v3/document_image/31fb5cac-2bd9-46c1-b5ea-2f17551b02ca-14086676.jpg)
                
            - receiptHandle 是当我们retrieve SQS message的时候， visible timeout，我们处理完后，在visible timeout结束后，别人又可以看到这个queue，这是不对的，我们需要receiptHandle 去把这个message删掉。
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/16a2a68e-b7be-4e61-ac44-fcabcfdc4cc5-14086676.jpg](https://api2.mubu.com/v3/document_image/16a2a68e-b7be-4e61-ac44-fcabcfdc4cc5-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/4964acef-1a41-4c9d-8cde-1bd831f5e400-14086676.jpg](https://api2.mubu.com/v3/document_image/4964acef-1a41-4c9d-8cde-1bd831f5e400-14086676.jpg)
                    
            - 如果我们用SQS 去trigger lambda，lambda会帮我们把这个trigger完了的SQS message给删掉，我们去SQS中poll 这个message是poll不到的，因为被lambda处理完自动删掉了。
            - 但我们有时不是用SQS 去trigger lambda的，是在trigger lambda之后，去取SQS message，这时就需要receiptHandle删除SQS message。
    - 11. 完整SNS - SQS - Lambda联动
        - 1. SQS订阅SNS的topic后，在SNS 中publish message
            - 注意这里一定要在SQS中订阅SNS中的topic。如果在SNS中去添加subscription，实验多次，发现SQS是不能trigger lambda的。
                - 在SNS中订阅，lambda一直不能monitor
                    
                    ![https://api2.mubu.com/v3/document_image/d6a9c0cc-2ae2-48f7-a679-8aa605f38ce1-14086676.jpg](https://api2.mubu.com/v3/document_image/d6a9c0cc-2ae2-48f7-a679-8aa605f38ce1-14086676.jpg)
                    
                - 在SQS中添加订阅topic，就可以在lambda中monitor。不知是不是bug?
                    
                    ![https://api2.mubu.com/v3/document_image/fcec4a03-fdda-4798-8b4d-c164f3758f81-14086676.jpg](https://api2.mubu.com/v3/document_image/fcec4a03-fdda-4798-8b4d-c164f3758f81-14086676.jpg)
                    
            - publish message
                
                ![https://api2.mubu.com/v3/document_image/9d2ed986-550d-4312-9700-c1612838a45c-14086676.jpg](https://api2.mubu.com/v3/document_image/9d2ed986-550d-4312-9700-c1612838a45c-14086676.jpg)
                
        - 2. publish message 后，send message给SQS，最后trigger lambda。
            - 这里可以看到lambda中提取的信息已经可以在log里看到了
                
                ![https://api2.mubu.com/v3/document_image/c051cc6a-3a0a-491a-b943-5b1dba3b8aad-14086676.jpg](https://api2.mubu.com/v3/document_image/c051cc6a-3a0a-491a-b943-5b1dba3b8aad-14086676.jpg)
                
            - 3. 补充：
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/e231432d-6db2-46c1-9d8d-2becb7dd2886-14086676.jpg](https://api2.mubu.com/v3/document_image/e231432d-6db2-46c1-9d8d-2becb7dd2886-14086676.jpg)
                    
- 作业
    - Have a look at boto3 package
    - Self-learning how to send, retrieve and delete message from sqs