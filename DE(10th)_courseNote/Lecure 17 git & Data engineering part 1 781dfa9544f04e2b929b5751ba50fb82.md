# Lecure 17 git & Data engineering part 1

- Assignment -ETL process （2:45）
    - 1.作业前注意点：（1：20）
        - data sql 要写出来
        - data flow要清楚
        - 数据长这样，怎么去构建它
    - 2. 写SDSD （solution data structure documentation）
    - 3. 要求
        - 不要求CICD pipeline
        - 要求data pipeline
        - 建议SQL完成
- 1. Aurora
    - 1.MySql 数据库，在其上面做了更改，但比传统MySQL效率会更高
        - 满足high speed的访问
            
            ![https://api2.mubu.com/v3/document_image/ba52f0ff-5574-43f5-85a8-9724d9772741-14086676.jpg](https://api2.mubu.com/v3/document_image/ba52f0ff-5574-43f5-85a8-9724d9772741-14086676.jpg)
            
    - 2.Scaling
        - storage volume增加到128TB ，
            
            ![https://api2.mubu.com/v3/document_image/b489c930-d883-4088-8475-8f4d1ab7a028-14086676.jpg](https://api2.mubu.com/v3/document_image/b489c930-d883-4088-8475-8f4d1ab7a028-14086676.jpg)
            
        - 数据非常可靠， 一个AZ 有两个copies， 可以有3个AZ，一共可以有6 个 copies of data。并且会self healing的功能
            
            ![https://api2.mubu.com/v3/document_image/5321141e-3413-47af-b463-189dbba7ff59-14086676.jpg](https://api2.mubu.com/v3/document_image/5321141e-3413-47af-b463-189dbba7ff59-14086676.jpg)
            
    - 3. Aurora 操作实验，aurora是要钱的（00:09:00 回放看老师怎么做）
        - 运行资源可选有弹性
            - 
                
                ![https://api2.mubu.com/v3/document_image/5326d572-7015-4867-89bc-c84a439cc5b3-14086676.jpg](https://api2.mubu.com/v3/document_image/5326d572-7015-4867-89bc-c84a439cc5b3-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/e06b7a24-28c5-4b0e-a260-f712fb7db55e-14086676.jpg](https://api2.mubu.com/v3/document_image/e06b7a24-28c5-4b0e-a260-f712fb7db55e-14086676.jpg)
                
        - add reader
            - 
                
                ![https://api2.mubu.com/v3/document_image/8a66267c-5067-4bb5-a5fd-481805cdf47b-14086676.jpg](https://api2.mubu.com/v3/document_image/8a66267c-5067-4bb5-a5fd-481805cdf47b-14086676.jpg)
                
        - 有15个 replicas
            - Replicas
                
                ![https://api2.mubu.com/v3/document_image/e2ee6784-65c7-4dd2-9a20-afcebb2b8a17-14086676.jpg](https://api2.mubu.com/v3/document_image/e2ee6784-65c7-4dd2-9a20-afcebb2b8a17-14086676.jpg)
                
            - 有15个不同的等级，如果main database挂了，直接用tier-0的replica promote成main database
                - 
                    
                    ![https://api2.mubu.com/v3/document_image/1b2fb607-f468-4588-bfe2-8310edf5dc06-14086676.jpg](https://api2.mubu.com/v3/document_image/1b2fb607-f468-4588-bfe2-8310edf5dc06-14086676.jpg)
                    
        - 连接Aurora是和🔗MySQL一样的
            - 
                
                ![https://api2.mubu.com/v3/document_image/87d10a89-89ac-4f77-9323-3534665937dc-14086676.jpg](https://api2.mubu.com/v3/document_image/87d10a89-89ac-4f77-9323-3534665937dc-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/0d819d37-7b34-4f44-bd5b-fe2b63f0c551-14086676.jpg](https://api2.mubu.com/v3/document_image/0d819d37-7b34-4f44-bd5b-fe2b63f0c551-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/7633b261-1fb4-4f53-90b2-8c029e9314c9-14086676.jpg](https://api2.mubu.com/v3/document_image/7633b261-1fb4-4f53-90b2-8c029e9314c9-14086676.jpg)
                
    - 4.Aurora Structure （与RDS的区别）
        - 0.架构， instance是计算的，storage是单独拿出来的，两者是分开的。storage volume是有multiple node的，这些不同的multiple node是被distribute到不同的AZ里面的。其次，Aurora会保留一些transaction log，传统数据库生产了transaction log，然后就apply到数据库上面，对disk产生这种读和写的操作，而Aurora是aws 背后的process，帮我们把transaction log apply到data storage上去，并不是写了一次就跟disk有一次交互，不是频繁的与disk做交互，它的速度当然会很快
            
            ![https://api2.mubu.com/v3/document_image/1820879c-58f4-484b-acaa-8377816830c4-14086676.jpg](https://api2.mubu.com/v3/document_image/1820879c-58f4-484b-acaa-8377816830c4-14086676.jpg)
            
        - RPO RTO ， downtime
            
            ![https://api2.mubu.com/v3/document_image/7ebe829a-7aad-4afe-9a9f-637822719b5a-14086676.jpg](https://api2.mubu.com/v3/document_image/7ebe829a-7aad-4afe-9a9f-637822719b5a-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/75795e87-95d8-4845-8336-43068cb1b0d5-14086676.jpg](https://api2.mubu.com/v3/document_image/75795e87-95d8-4845-8336-43068cb1b0d5-14086676.jpg)
            
        - 1.通过endpoint 来决定是只能读，还是读写都可以。read和write的endpoint是可以分开的。
            
            ![https://api2.mubu.com/v3/document_image/6d5a9541-5dd9-4829-bfaa-878d80af629d-14086676.jpg](https://api2.mubu.com/v3/document_image/6d5a9541-5dd9-4829-bfaa-878d80af629d-14086676.jpg)
            
        - 2.每个不同的data copies 不基于comput resource的，不是通过comput resource挂接起来的，能够独立存在，不同的AZ的人读到的6个 data copies都是最新的（这是与RDS的区别）
        - 3.同过transaction log缩短wait的时间
            - user wait的时间大大缩短
                
                ![https://api2.mubu.com/v3/document_image/49296f3c-7304-48a9-8968-1e33859edbf8-14086676.jpg](https://api2.mubu.com/v3/document_image/49296f3c-7304-48a9-8968-1e33859edbf8-14086676.jpg)
                
            - disk 访问也是一样（灰色小人）
                
                ![https://api2.mubu.com/v3/document_image/0f4c29f8-0aba-4d6c-b01a-6f2df45665dc-14086676.jpg](https://api2.mubu.com/v3/document_image/0f4c29f8-0aba-4d6c-b01a-6f2df45665dc-14086676.jpg)
                
            - 到底什么时候apply transaction log由AWS快
- 2.git
    - 看视频回放操作（40:00）
        
        ![https://api2.mubu.com/v3/document_image/b019e088-9140-441f-8e38-53c542d4205f-14086676.jpg](https://api2.mubu.com/v3/document_image/b019e088-9140-441f-8e38-53c542d4205f-14086676.jpg)
        
    - commands
        - basic commands
            
            ![https://api2.mubu.com/v3/document_image/66eec6a9-4694-43bd-a8f5-214a06d4d1de-14086676.jpg](https://api2.mubu.com/v3/document_image/66eec6a9-4694-43bd-a8f5-214a06d4d1de-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/7b11ea91-aeaf-441f-93e7-565df378b628-14086676.jpg](https://api2.mubu.com/v3/document_image/7b11ea91-aeaf-441f-93e7-565df378b628-14086676.jpg)
            
        - 做版本控制，先配置Git， 代码：git config --global [user.name](http://user.name/) 'Leo' user.email 'Hackylee1314@gmail.com'
        - 然后cat ~/.gitconfig 就能看到配置文件中的内容，
        - nano ~/.gitconfig 还可以对config文件进行修改
        - git init 初始化版本
            
            ![https://api2.mubu.com/v3/document_image/e7213b70-93dc-4c7d-8f74-fef7e6db51e5-14086676.jpg](https://api2.mubu.com/v3/document_image/e7213b70-93dc-4c7d-8f74-fef7e6db51e5-14086676.jpg)
            
        - git status 查看version更新的改变，哪些将要被committed的文件
        - git add <file> 将指定文件commit到Git上
            
            ![https://api2.mubu.com/v3/document_image/2ac6131c-863d-429f-89cc-d30acbdd4847-14086676.jpg](https://api2.mubu.com/v3/document_image/2ac6131c-863d-429f-89cc-d30acbdd4847-14086676.jpg)
            
        - git rm --cached <file> 将指定文件取消commit
            
            ![https://api2.mubu.com/v3/document_image/9b4293ee-0d2e-41bf-aa87-c8719a4f2ce3-14086676.jpg](https://api2.mubu.com/v3/document_image/9b4293ee-0d2e-41bf-aa87-c8719a4f2ce3-14086676.jpg)
            
        - git add . 所有更改的文件都会被commit上
            
            ![https://api2.mubu.com/v3/document_image/04727785-86a5-4989-8162-f10c986f3f2a-14086676.jpg](https://api2.mubu.com/v3/document_image/04727785-86a5-4989-8162-f10c986f3f2a-14086676.jpg)
            
        - git commit -m 'first commit' 。 commit 上去后一定要给个message,之后用status查看，就没有了更改的可能需要commit的file
            
            ![https://api2.mubu.com/v3/document_image/ffac3b50-30f2-47ec-89f1-d89088c31a1b-14086676.jpg](https://api2.mubu.com/v3/document_image/ffac3b50-30f2-47ec-89f1-d89088c31a1b-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/b60c8627-a910-49ce-ab52-81dd40306618-14086676.jpg](https://api2.mubu.com/v3/document_image/b60c8627-a910-49ce-ab52-81dd40306618-14086676.jpg)
            
        - touch .gitignore 会生成新的小图标，给git做version control去看或用到的一个file。在gitignore file里面写上任何不想做version control的file 就可以不对其做git update。如果sample data很大的话，不想sample data影响git传输，只需要做source code的版本控制
            
            ![https://api2.mubu.com/v3/document_image/7820cb46-f334-4c7c-882e-abbb5cae87cc-14086676.jpg](https://api2.mubu.com/v3/document_image/7820cb46-f334-4c7c-882e-abbb5cae87cc-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/2645c5dc-9b90-4b4e-a403-08ad220b35f4-14086676.jpg](https://api2.mubu.com/v3/document_image/2645c5dc-9b90-4b4e-a403-08ad220b35f4-14086676.jpg)
            
        - git checkout -b <new branch name> 创建新的branch。
        - git branch, 查看当前branch。
            
            ![https://api2.mubu.com/v3/document_image/343160f6-74d5-4911-8117-fbf7c54c38b3-14086676.jpg](https://api2.mubu.com/v3/document_image/343160f6-74d5-4911-8117-fbf7c54c38b3-14086676.jpg)
            
        - git checkout <branchName> 切换branch
        - git merge <branch name eg.feat/etl> --no-ff 将branch中做的更改版本合并到master branch中。
            
            ![https://api2.mubu.com/v3/document_image/ede3793f-5413-4706-96a1-e66a1fdbbcda-14086676.jpg](https://api2.mubu.com/v3/document_image/ede3793f-5413-4706-96a1-e66a1fdbbcda-14086676.jpg)
            
        - git branch -d <branch name> 删除branch
            
            ![https://api2.mubu.com/v3/document_image/d3982646-88ca-4a75-ab85-6bd82b28ce2c-14086676.jpg](https://api2.mubu.com/v3/document_image/d3982646-88ca-4a75-ab85-6bd82b28ce2c-14086676.jpg)
            
        - git push --set-upstream origin<branch name> 上传branch 到github
            
            ![https://api2.mubu.com/v3/document_image/427131da-3d82-46f8-bdf7-54d5100ea194-14086676.jpg](https://api2.mubu.com/v3/document_image/427131da-3d82-46f8-bdf7-54d5100ea194-14086676.jpg)
            
    - 工业中，每次都要git pull对我们的master branch进行update，然后建立新branch，进行开发，会加前缀，有feat/, 有bugfix/, 有hotfix/
        - 
            
            ![https://api2.mubu.com/v3/document_image/38ba130c-3e84-44a8-ab91-8fd215ca95da-14086676.jpg](https://api2.mubu.com/v3/document_image/38ba130c-3e84-44a8-ab91-8fd215ca95da-14086676.jpg)
            
    - pull request， 比较两个版本做的更改，并且合并master branch
        - 工业中一般会指定是谁可以review我们的code，然后发给他看
            
            ![https://api2.mubu.com/v3/document_image/180c8ebe-5e24-4759-a510-4ffed73aeb33-14086676.jpg](https://api2.mubu.com/v3/document_image/180c8ebe-5e24-4759-a510-4ffed73aeb33-14086676.jpg)
            
        - reviewer 看完后可以加个commit
            
            ![https://api2.mubu.com/v3/document_image/bf1c7a51-2df2-4333-baf0-3fcf2812cc19-14086676.jpg](https://api2.mubu.com/v3/document_image/bf1c7a51-2df2-4333-baf0-3fcf2812cc19-14086676.jpg)
            
        - merge pull request, 工业中一般用第二个squash and merge，两个或多个commits merge到main branch里
            
            ![https://api2.mubu.com/v3/document_image/65ff5dc7-b333-4bbc-a839-7127f98bbca3-14086676.jpg](https://api2.mubu.com/v3/document_image/65ff5dc7-b333-4bbc-a839-7127f98bbca3-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/76837a7e-eae3-41e0-86f0-83bd93884d9c-14086676.jpg](https://api2.mubu.com/v3/document_image/76837a7e-eae3-41e0-86f0-83bd93884d9c-14086676.jpg)
            
        - merge完所有需要更改的commit之后，可以删除branch
            
            ![https://api2.mubu.com/v3/document_image/0748df30-1fda-4b5e-903a-e09dad446d4a-14086676.jpg](https://api2.mubu.com/v3/document_image/0748df30-1fda-4b5e-903a-e09dad446d4a-14086676.jpg)
            
    - 工业中常见案例讲解：（两或多个人对一个repo操作,且有conflict怎么办，企业中最复杂的一种情况）
        - conflict，两个人对同一个文件做了修改，在不同时间merge branch到main 中，会conflict。
        - 1.创建两个branch，分别做一些commit
            - 
                
                ![https://api2.mubu.com/v3/document_image/c129fbb2-bdb2-4ce6-bbd9-8795dd4cf8dd-14086676.jpg](https://api2.mubu.com/v3/document_image/c129fbb2-bdb2-4ce6-bbd9-8795dd4cf8dd-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/524a838d-57dd-47e5-9bc2-65f9e8344479-14086676.jpg](https://api2.mubu.com/v3/document_image/524a838d-57dd-47e5-9bc2-65f9e8344479-14086676.jpg)
                
        - 2. create pull request for dev1
            - 
                
                ![https://api2.mubu.com/v3/document_image/0f76b995-7c73-417b-b3c9-f519cdaf60c1-14086676.jpg](https://api2.mubu.com/v3/document_image/0f76b995-7c73-417b-b3c9-f519cdaf60c1-14086676.jpg)
                
                ![https://api2.mubu.com/v3/document_image/4c62f5a1-1a80-47e7-9c18-d63261cd51a7-14086676.jpg](https://api2.mubu.com/v3/document_image/4c62f5a1-1a80-47e7-9c18-d63261cd51a7-14086676.jpg)
                
            - 先不管它，同时dev2也create pull request
                
                ![https://api2.mubu.com/v3/document_image/919bc789-7e06-4b91-9a86-1149ae7d37f9-14086676.jpg](https://api2.mubu.com/v3/document_image/919bc789-7e06-4b91-9a86-1149ae7d37f9-14086676.jpg)
                
        - 3. create pull request for dev2
            - 
                
                ![https://api2.mubu.com/v3/document_image/ababe4ff-4e29-4f18-9af1-35d92353e62a-14086676.jpg](https://api2.mubu.com/v3/document_image/ababe4ff-4e29-4f18-9af1-35d92353e62a-14086676.jpg)
                
        - 4. squash and merge for dev1
            - dev1的merge完，删掉branch
                
                ![https://api2.mubu.com/v3/document_image/8c1e607d-bd91-40f8-a933-670162d7229a-14086676.jpg](https://api2.mubu.com/v3/document_image/8c1e607d-bd91-40f8-a933-670162d7229a-14086676.jpg)
                
            - 删掉local的branch dev1
                
                ![https://api2.mubu.com/v3/document_image/6460567e-a449-45b4-a4d6-c47c99fb7af5-14086676.jpg](https://api2.mubu.com/v3/document_image/6460567e-a449-45b4-a4d6-c47c99fb7af5-14086676.jpg)
                
        - 5. squash and merge for dev2 ==> conflict
            - 出现conflict ，必须解决
                
                ![https://api2.mubu.com/v3/document_image/7c1c85b0-b595-4c6d-8e04-0d5b5837c957-14086676.jpg](https://api2.mubu.com/v3/document_image/7c1c85b0-b595-4c6d-8e04-0d5b5837c957-14086676.jpg)
                
            - 给发起者留言，plz resolve the conflicts
                
                ![https://api2.mubu.com/v3/document_image/f8330eb6-ea19-42fc-8e52-9e603c233e26-14086676.jpg](https://api2.mubu.com/v3/document_image/f8330eb6-ea19-42fc-8e52-9e603c233e26-14086676.jpg)
                
            - conflict 发起者怎么解决？
                - 1. 到local master branch去, 做一个操作 git pull, update remote master branch
                    
                    ![https://api2.mubu.com/v3/document_image/399e2bd5-60e0-412c-884c-fcbdd3bfde03-14086676.jpg](https://api2.mubu.com/v3/document_image/399e2bd5-60e0-412c-884c-fcbdd3bfde03-14086676.jpg)
                    
                - 2. git checkout 回 feature branch，做merge 会出现conflict，找到conflict；
                    
                    ![https://api2.mubu.com/v3/document_image/ef4ecfe1-b0aa-4d31-87b2-a11703eb9234-14086676.jpg](https://api2.mubu.com/v3/document_image/ef4ecfe1-b0aa-4d31-87b2-a11703eb9234-14086676.jpg)
                    
                - 3. accept both changes
                    
                    ![https://api2.mubu.com/v3/document_image/97b9d3e0-227e-46f5-9f5d-9b06e13f5ef9-14086676.jpg](https://api2.mubu.com/v3/document_image/97b9d3e0-227e-46f5-9f5d-9b06e13f5ef9-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/52c826c4-201e-4ce7-a2db-85d39fbe8392-14086676.jpg](https://api2.mubu.com/v3/document_image/52c826c4-201e-4ce7-a2db-85d39fbe8392-14086676.jpg)
                    
                    ![https://api2.mubu.com/v3/document_image/cabfb4fb-4504-4265-96e6-689b42656c5c-14086676.jpg](https://api2.mubu.com/v3/document_image/cabfb4fb-4504-4265-96e6-689b42656c5c-14086676.jpg)
                    
                - 4.做完conflict fix后，接下来就可以git add , commit , push了
                    
                    ![https://api2.mubu.com/v3/document_image/f0c9b505-e01b-4be7-85de-69b58b47cf10-14086676.jpg](https://api2.mubu.com/v3/document_image/f0c9b505-e01b-4be7-85de-69b58b47cf10-14086676.jpg)
                    
        - 6. 发起者解决完conflict后，dev2就可以merge了
            - 建议大家都用squash merge，merge完之后就可以删除branch了
                
                ![https://api2.mubu.com/v3/document_image/f4d56679-e4a2-4bf4-bf54-d930483c50b9-14086676.jpg](https://api2.mubu.com/v3/document_image/f4d56679-e4a2-4bf4-bf54-d930483c50b9-14086676.jpg)
                
            - squash merge 看起来比all merge要简洁些
                
                ![https://api2.mubu.com/v3/document_image/4e6d7a42-761b-47f7-9287-df85736a8e38-14086676.jpg](https://api2.mubu.com/v3/document_image/4e6d7a42-761b-47f7-9287-df85736a8e38-14086676.jpg)
                
            - 下图的是merge all的。
                
                ![https://api2.mubu.com/v3/document_image/15bc0a29-6303-4633-aada-be314016c240-14086676.jpg](https://api2.mubu.com/v3/document_image/15bc0a29-6303-4633-aada-be314016c240-14086676.jpg)
                
    - Repo (git) 树形结构
        - local
            
            ![https://api2.mubu.com/v3/document_image/eee4c3d0-fc67-461a-a1c3-1401720180ca-14086676.jpg](https://api2.mubu.com/v3/document_image/eee4c3d0-fc67-461a-a1c3-1401720180ca-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/740cbdfb-9814-46e8-889f-a4bf1213163b-14086676.jpg](https://api2.mubu.com/v3/document_image/740cbdfb-9814-46e8-889f-a4bf1213163b-14086676.jpg)
            
        - remote工业常用方法
            - 没做一个新feature，都是循环以下步骤：
                
                ![https://api2.mubu.com/v3/document_image/b2eec992-731b-49b9-a279-88d9eb0b208a-14086676.jpg](https://api2.mubu.com/v3/document_image/b2eec992-731b-49b9-a279-88d9eb0b208a-14086676.jpg)
                
                - git colne or pull
                - feature branch
                - git push
                - reviewer review (通过就到master中merge，不通过回去继续做)
                - 注意在每次做完feature branch准备merge到master branch之前，都要git pull一下最新的master branch。local feature branch 上做一个merge master，如果有conflict，就要解决 然后再git push
            - conflict处理
                
                ![https://api2.mubu.com/v3/document_image/e887bd9d-c1f3-49ac-a959-c306c4692303-14086676.jpg](https://api2.mubu.com/v3/document_image/e887bd9d-c1f3-49ac-a959-c306c4692303-14086676.jpg)
                
- ---Data Engineer pipeline----
    - 
        
        ![https://api2.mubu.com/v3/document_image/302a262c-28ee-4711-bd32-fb1fbc326b70-14086676.jpg](https://api2.mubu.com/v3/document_image/302a262c-28ee-4711-bd32-fb1fbc326b70-14086676.jpg)
        
- 1. Batch processing
    - 1. 什么是batch processing？
        - 例如最近一周或最近一个月的数据
            
            ![https://api2.mubu.com/v3/document_image/e4be9798-8d77-4e38-930d-85d3fb51dd94-14086676.jpg](https://api2.mubu.com/v3/document_image/e4be9798-8d77-4e38-930d-85d3fb51dd94-14086676.jpg)
            
    - 2. 什么时候用batch processing ?
        - 不需要实时分析的时候用，根据公司数据分析的频率来设置batch processing的频率，weekly，monthly， etc.
            
            ![https://api2.mubu.com/v3/document_image/d1f2938f-7fb3-44af-8e7e-c665c8859d2f-14086676.jpg](https://api2.mubu.com/v3/document_image/d1f2938f-7fb3-44af-8e7e-c665c8859d2f-14086676.jpg)
            
        - 适合不需要实时数据分析的情况
        - 海量数据进行机器学习
        - 海量数据进行整合，便于数据分析及可视化
    - 3. 例子
        - 拿出对我们有用的信息
            
            ![https://api2.mubu.com/v3/document_image/1f1bafc7-447a-41dd-91a9-ca8d8b6920da-14086676.jpg](https://api2.mubu.com/v3/document_image/1f1bafc7-447a-41dd-91a9-ca8d8b6920da-14086676.jpg)
            
        - SMS， 通过大数据对我们进行分析。campaign，不需要实时，法律只能一天一次邮件，batch会成为很好的选择
            
            ![https://api2.mubu.com/v3/document_image/388da9a1-36ec-4bbf-a5d5-da66bd3de276-14086676.jpg](https://api2.mubu.com/v3/document_image/388da9a1-36ec-4bbf-a5d5-da66bd3de276-14086676.jpg)
            
    - 4. challenges
        - 1. Data format and encoding
            - 是UTF -16 还是UTF -8？by default，我们都喜欢UTF-8.在设计data loading的时候，需要考虑到商业需求是不是会遇到这种多编码，多种data format的情况，所有需要设计一种process，有一定的ability去处理多编码多data format的issue。
                
                ![https://api2.mubu.com/v3/document_image/36356be8-c19b-43b6-992e-efa6b7c7b58e-14086676.jpg](https://api2.mubu.com/v3/document_image/36356be8-c19b-43b6-992e-efa6b7c7b58e-14086676.jpg)
                
        - 2. Orchestrating time slices
            - ETL 跑多久，先跑什么再跑什么，如果有些data 晚来了，或数据来的顺序不对，该怎么处理。
                
                ![https://api2.mubu.com/v3/document_image/3e2cfae6-b8e7-4a9a-b99d-d870e07206e6-14086676.jpg](https://api2.mubu.com/v3/document_image/3e2cfae6-b8e7-4a9a-b99d-d870e07206e6-14086676.jpg)
                
    - 5. Architecture
        - 需要理解思考：
            
            ![https://api2.mubu.com/v3/document_image/1bd131aa-513a-4c4b-9169-3df1dd564f34-14086676.jpg](https://api2.mubu.com/v3/document_image/1bd131aa-513a-4c4b-9169-3df1dd564f34-14086676.jpg)
            
            ![https://api2.mubu.com/v3/document_image/33847eed-fb3c-49d6-ae7a-2a145bd8c832-14086676.jpg](https://api2.mubu.com/v3/document_image/33847eed-fb3c-49d6-ae7a-2a145bd8c832-14086676.jpg)
            
        - 1. 需要怎样的data storage
            - 1. S3
                - 能保证很好的durability，
                    
                    ![https://api2.mubu.com/v3/document_image/29ad854d-2400-477e-b152-a549d0b15cd6-14086676.jpg](https://api2.mubu.com/v3/document_image/29ad854d-2400-477e-b152-a549d0b15cd6-14086676.jpg)
                    
            - 2. EBS
                - 可以attach到instance上，直接计算完保留在磁盘上读写速度快
                    
                    ![https://api2.mubu.com/v3/document_image/80546389-8c25-4ecd-90ed-59602b96c373-14086676.jpg](https://api2.mubu.com/v3/document_image/80546389-8c25-4ecd-90ed-59602b96c373-14086676.jpg)
                    
        - 2. 需要怎样的batch processing。能不能让运行的时间更短。
            - 1. Spark
                - 做大数据，考虑spark，支持多种program language，能做分布式计算，提高我们processing的performance。
                    
                    ![https://api2.mubu.com/v3/document_image/83279b1a-3233-424a-9c9a-3b8ef2e2f990-14086676.jpg](https://api2.mubu.com/v3/document_image/83279b1a-3233-424a-9c9a-3b8ef2e2f990-14086676.jpg)
                    
            - 2. ETL/ELT tools
                - 不想用大数据处理，snowflake 本身的performance很高，我们通过生产很多SQL statement，让它们在snowflake等数据库中去运行。可以prebuid 的一些connector ，不需要再去code，只要做些config就可以去跟别人打 交道了。
                    
                    ![https://api2.mubu.com/v3/document_image/f86b3093-dad6-43d3-bf73-ecee01327e94-14086676.jpg](https://api2.mubu.com/v3/document_image/f86b3093-dad6-43d3-bf73-ecee01327e94-14086676.jpg)
                    
        - 3. 需要怎样的analytical data store
            - 0.选取怎样的数据库呢?olap?oltp?
            - 1. Data warehouse -- 对数据进行优化存储，之后做数据分析会非常快
            - 2. Spark SQL
            - 3. HBase
                
                ![https://api2.mubu.com/v3/document_image/88bbc370-b8dd-4a0d-acd3-14fb9ace3b21-14086676.jpg](https://api2.mubu.com/v3/document_image/88bbc370-b8dd-4a0d-acd3-14fb9ace3b21-14086676.jpg)
                
        - 4. 需要怎样的Analysis and reporting
            - 0.传统的分析？机器学习？
            - 1. Power BI
            - 2. Tableau
            - 3. Amazon QuickSight
                
                ![https://api2.mubu.com/v3/document_image/40411dc0-ff8a-4186-b929-292187fbcf32-14086676.jpg](https://api2.mubu.com/v3/document_image/40411dc0-ff8a-4186-b929-292187fbcf32-14086676.jpg)
                
        - 5. 需要怎样的Orchestration
            - 0.整个pipeline怎么串联起来，什么时间跑什么job
            - 1. Oozie and Sqoop
            - 2. Amazon ClouldWatch
                
                ![https://api2.mubu.com/v3/document_image/ec6dd7d0-bf5b-4d8f-8a0b-6553b5c7439c-14086676.jpg](https://api2.mubu.com/v3/document_image/ec6dd7d0-bf5b-4d8f-8a0b-6553b5c7439c-14086676.jpg)
                
- 架构需要了解，但目前小白求职阶段，老师需要我们明白“以后工作了，人家给我们一个solution，我们要知道为什么要这么设计，或者我们可以去challenge它，有些地方欠考虑。”