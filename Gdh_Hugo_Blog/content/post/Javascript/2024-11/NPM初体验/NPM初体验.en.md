---
date: '2024-11-11T13:05:12+08:00'
title: 'NPM Introduction'
description: ''
slug: 'js-npm-introduction'
image: "post/images/npm-logo.png"
categories:
    - Javascript
tags:
    - Javascript
draft: false
keywords:
    - javascript
    - npm
    - js-npm-introduction
---
## Brief Description

NPM, short for Node Package Manager, is a tool for managing and sharing JavaScript code packages. It is the default package manager for the Node.js platform, allowing developers to download and install various JavaScript packages and tools from the NPM repository. With NPM, developers can easily find, install, update, and remove dependencies, making the development and maintenance of JavaScript projects more efficient and convenient.

In addition to installing and managing packages, NPM also offers other features, such as publishing your own packages to the NPM repository, managing project dependencies, and running script commands. Developers can use NPM to build and manage their JavaScript projects and share their code with other developers.

Overall, NPM is a powerful tool that provides convenient package management functions for the JavaScript community, facilitating collaboration and knowledge sharing among developers.

## Example 1

I have briefly experienced the example.

This example is very simple; it uses the NPM command to generate a few predefined folders.

### Start Coding

#### Node.js

P.S: Ensure that Node.js is installed in the environment.

![image-20241111150607066](post/images/image-20241111150607066.png)

#### Create and enter the folder

```powershell
mkdir FolderCreator
 
cd FolderCreator
```

#### Initialize the npm project

```powershell

npm init -y

```

>`npm init -y` is a command used to quickly generate a package.json file for a project. In this command, `npm init` initializes a new Node.js project, while the `-y`flag indicates that default values should be used during the initialization process, eliminating the need for user input.
>Specifically, executing `npm init -y` automatically creates a default package.json file that contains some basic information, such as the project name, version number, author, and more. This allows for a quick setup of a simple project structure without having to answer various questions posed by npm init.
>Using the `npm init -y` command can save time, especially when creating temporary or experimental projects. Developers can then make manual adjustments and configurations as needed.

![image-20241111151220221](post/images/image-20241111151220221.png)

#### Create and edit the script file

![image-20241111151248347](post/images/image-20241111151248347.png)

```javascript
#!/usr/bin/env node
const fs = require('fs');
const path = require('path');
const folders = [
    '10 项目管理/10-01 要件定义',
    '10 项目管理/10-02 要件定义交付',
    '10 项目管理/10-03 项目主计划',
    '10 项目管理/10-04 项目周报',
    '10 项目管理/10-05 会议纪要',
    '20 业务调研及要件定义/20-01 调研计划',
    '20 业务调研及要件定义/20-02 调研会议资料',
    '20 业务调研及要件定义/20-03 调研会议会议纪要',
    '20 业务调研及要件定义/20-04 业务需求分析',
    '20 业务调研及要件定义/20-05 业务蓝图',
    '20 业务调研及要件定义/20-06 课题研讨',
    '20 业务调研及要件定义/20-07 功能设计/历史版本',
    '30 技术概要及详细设计',
    '40 系统测试和培训/40-01 系统测试',
    '40 系统测试和培训/40-02 用户培训',
    '50 系统上线/50-01 系统切换方案',
    '50 系统上线/50-02 用户及权限配置',
    '50 系统上线/50-03 数据初始化',
    '50 系统上线/50-04 系统上线汇报材料',
    '60 上线后运维',
    '70 配置相关',
    '80 数据清理/80-01 数据清理方案',
    '80 数据清理/80-02 数据清理模板',
    '80 数据清理/80-03 数据清理结果'
];
const rootPath = process.cwd();
folders.forEach(folder => {
    const fullPath = path.join(rootPath, folder);
    fs.mkdirSync(fullPath, { recursive: true });
});
```

#### Update package.json

In the package.json file, add a bin field to use this script as a command-line tool.

```json
"bin": {
    "create-folders": "./createFolders.js"
}
```

#### Add  #!/usr/bin/env node

At the top of the createFolders.js file, add `#!/usr/bin/env node`.

This line of code is a special comment called a shebang, which typically appears as the first line in script files on Unix-like systems.

It tells the operating system which interpreter to use to execute this script.

In this case, `#!/usr/bin/env node` means to use the Node.js interpreter from the environment to run this script.

#### Publish locally using npm link

Use the `npm link` command to publish the package globally (locally),

making it easy to call directly from the command line.

```powershell
npm link
```

#### Run the script (locally)

Create a new folder on the desktop, then enter the command in the command line

After running it, the predefined folders will be generated.

```powershell
create-folders
```

### Publishing

Publish the package you created to NPM. Here are the specific steps.

#### Create an NPM account

NPM Official Website：[https://www.npmjs.com](https://www.npmjs.com/)

#### Login NPM

Enter in the terminal `npm login`

#### Adjust package.json

- name : The name of the package, which needs to be unique.
- version
- description
- main : The entry file.
- bin : The path to the executable command tool.

Below is my package.json code.：

```json
{
  "name": "gdhblog_folder_creator",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "Donghai Gong",
  "license": "ISC",
  "description": "A simple tool to create a predefined folder structure in the current directory.",
  "bin": {
    "create-folders": "./createFolders.js"
  }
}
```

After adjusting the information in package.json, enter npm pack in the terminal to generate a .tgz file.

![image-20241111151814166](post/images/image-20241111151814166.png)

#### Publish NPM

Enter the code.

```powershell
npm publish
```

#### Remark

When publishing a package, choose between public or private:

- Public(default) : `npm publish`
- Private: Add `"private": "true"` in package.json

### Verification/Testing

After a few minutes, you will be able to see it on NPM. Next, I will demonstrate how to use it.

![image-20241111152003685](post/images/image-20241111152003685.png)

#### Create and enter a folder

```powershell
mkdir Test_FolderCreator
 
cd Test_FolderCreator
```

#### Install

``` shell
npm i gdhblog_foldercreator
```

- `npm`: The package management tool for the Node.js platform, used to download, install, and manage JavaScript packages
- `i`(abbreviated form) or `install`(full form): The command to install packages with npm.
- `gdhblog_foldercreator`: The name of the npm package to be installed.

![image-20241111152055177](post/images/image-20241111152055177.png)

#### Execute the command

This refers to the `bin` we configured earlier in the package.json file.

![image-20241111152131874](post/images/image-20241111152131874.png)
