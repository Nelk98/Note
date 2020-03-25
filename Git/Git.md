# Git

## 1.	开发流程

![](.\media\Snipaste_2020-03-25_11-04-14.jpg)

- ==本地仓库 -> 远程仓库（共享仓库）==
- Git有本地仓库、SVN没有
- SVN是必须连接到远程仓库才能提交、修改

![](.\media\Snipaste_2020-03-25_11-08-56.jpg)



## 2.	本地仓库

- 在本地创建仓库文件夹

- ==git init==

![](.\media\Snipaste_2020-03-25_11-40-08.jpg)



- 使用tortoiseGit 

![](.\media\Snipaste_2020-03-25_12-44-34.jpg)

- ==git commit -m "提交日志"==



## 3.	远程仓库

- ==ssh-keygen -t ras 生成 ssh秘钥盾==



![](.\media\Snipaste_2020-03-25_12-49-47.jpg)



- 将公钥内容复制添加到git上

![](.\media\Snipaste_2020-03-25_12-50-17.jpg)



- 连接远程仓库  SSH / https

  ```shell
  git remote add origin git@github.com:Nelk98/Notes.git
  ```
  
  ```shell
  git remote add origin https://github.com/Nelk98/Note.git
  ```

![](.\media\Snipaste_2020-03-25_13-15-57.jpg)











